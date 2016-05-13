02 Create first prototype
===



<br />
Intention
---

In the last article [01 Setup the project] I show how to setup the new project 
with another [GitHub] project from me [Project-Template-afterburnerfx-Naoghuman] 
and what are the advantages are from using this template.

In this article I describes the steps and decisions which I make during the 
implementation from the first `prototype`. Click on the picture to see the 
`SokubanFX v0.1.0-PROTOTYPE` in action ![emoticon_smile.png][emoticon_smile] in 
YouTube.

[![sokubanfx_v0.1.0-PROTOTYPE.png][sokubanfx_v0.1.0-PROTOTYPE]](https://www.youtube.com/watch?v=Kp1vWjLTIvY "SokubanFX v0.1.0-PROTOTYPE")

<br/>
You can download the `prototype` here: [SokubanFX-0.1.0-PROTOTYPE_2016-04-30_08-22.zip]



<br />
Content
---

* [Create first prototype](#CreateFirstPrototype)
    * [Basic functionalities from the project](#BasicFunctionalities)
    * [Project structure](#ProjectStructure)
    * [Functionalities like collision, movement...](#Functionalities)
    * [Persistence from the maps](#PersistenceMaps)
    * [Textbased maps in views](#TextbasedMaps)
* [Conclusion](#Conclusion)
* [About the autor](#Autor)
    * [Contact](#Contact)
* [Articles in this series](#Articles)



<br />
Create first prototype<a name="CreateFirstPrototype" />
---

Like I said in the section `Intention` here are the steps and decisions which I 
make during the implementation from the first `prototype` from [SokubanFX].


<br />
##### Basic functionalities from the project<a name="BasicFunctionalities" />

Because I used my project template [Project-Template-afterburnerfx-Naoghuman] to  
create the [SokubanFX] project all basic functionalities which I want was 
implemented ![emoticon_smile.png][emoticon_smile] .

> Logging, Database-Handling, ActionEvent-Handling, Properties-Handling and support 
> for the [JavaFX] development, easy generation from an executable jar file.

For more detailed informations plz see the article [01 Setup the project].


<br />
##### Project structure<a name="ProjectStructure" />

TODO clean code


<br />
##### Functionalities like collision, movement...<a name="Functionalities" />

What are the basic funcitionalities for the game? Loading and converting a 
map I will described in the article a little later.  
So I will speak in this section about `collision` and `movement`.

Following workflow is given:
* User want to move the player, for example he press the key DOWN.
* Now all possible collisions must be checked, before something can moved or not.
* With the `CheckMovementResult` then the movement from the player (and optional 
  a box) will be done or not.
* Finally after a successful move the game should be checked if the map is finished.
  If so the next map can be shown.

<br />
`GamePresenter.java` - user press the key DOWN
```java
public void onActionButtonDown() {
    LoggerFacade.INSTANCE.debug(this.getClass(), "On action Button down"); // NOI18N
        
    final CheckMovementResult checkMovementResult = MapFacade.INSTANCE.playerMoveTo(EDirection.DOWN, actualMapModel);
    this.evaluatePlayerMoveTo(checkMovementResult);
        
    final boolean shouldCheckIfMapIsFinished = checkMovementResult.isCheckIsMapFinish();
    if (shouldCheckIfMapIsFinished) {
        final boolean isMapFinish = MapFacade.INSTANCE.isMapFinish(actualMapModel);
        this.evaluateIsMapFinish(isMapFinish);
    }
}
```

<br />
`MapMovement.java` - check possible collisions return what happen
```java
public CheckMovementResult checkMovePlayerTo(EDirection direction, MapModel mapModel) {
    LoggerFacade.INSTANCE.debug(this.getClass(), "Check move player to direction: " + direction.toString()); // NOI18N

    // Player -> Wall
    final CollisionResult collisionResultCheckCollisionPlayerWall = CollisionChecker.getDefault().checkCollisionPlayerWall(direction, mapModel);
    final CheckMovementResult checkMovementResult = CheckMovementResult.getDefault();
    if (collisionResultCheckCollisionPlayerWall.equals(CollisionResult.PLAYER_AGAINST__WALL)) {
        checkMovementResult.setAnimation(EAnimation.WHAT_HAPPEN);
        checkMovementResult.setMovement(EMovement.NONE);
            
        return checkMovementResult;
    }
	
	// and do all other collision checks also here.
}
```

<br />
`CollisionResult.java` - shows what collisions are possible
```java
public enum CollisionResult {
    
    NONE,                      // ...
    PLAYER_AGAINST__BOX,       // player -> box
    PLAYER_AGAINST__BOX_BOX,   // player -> box -> box
    PLAYER_AGAINST__BOX_NONE,  // player -> box -> none
    PLAYER_AGAINST__BOX_PLACE, // player -> box -> place
    PLAYER_AGAINST__BOX_PLACE_AND_FINISH, // player -> box -> place -> finish
    PLAYER_AGAINST__BOX_WALL,  // player -> box -> wall
    PLAYER_AGAINST__WALL;      // player -> wall
    
}
```

<br />
`GamePresenter.java` - if a new map be should shown
```java
private void displayMap() {
    LoggerFacade.INSTANCE.debug(this.getClass(), "Display Map"); // NOI18N
        
    lMapInfo.setText("Map " + actualMapModel.getLevel()); // NOI18N
        
    final List<String> mapAsStrings = MapFacade.INSTANCE.convertMapCoordinatesToStrings(actualMapModel);
    taMapDisplay.setText(null);
    mapAsStrings.stream().forEach((line) -> {
        taMapDisplay.appendText(line);
        taMapDisplay.appendText("\n"); // NOI18N
    });
}
```


<br />
##### Persistence from the maps<a name="PersistenceMaps" />

In my old [Java] [Swing2D] game [Sokuban-Clone] the maps are persist as txt-files.

TODO screenshot folder maps + one map open

<br />
The maps was readed with:
```java
public final boolean loadTileMap(int level)
{
    ArrayList<String> lines = new ArrayList();
    
    int w = 0;
    int h = 0;
    
    String line = null;
    BufferedReader reader = null;
    try
    {
      reader = new BufferedReader(new InputStreamReader(
        ClassLoader.getSystemResourceAsStream(
        "maps/map" + level + ".txt")));
      while (Boolean.TRUE.booleanValue())
	  {
        line = reader.readLine();
        if (line == null)
		{
          reader.close(); break;
        }
        if (!line.startsWith("#"))
		{
          lines.add(line);
          w = Math.max(w, line.length());
        }
      }
    }
    catch (IOException e)
    {
      e.printStackTrace();
    }
	
    ...
}
```

In the method are a lot of more code for converting the map but that
* isn't relevant for reading the map from a txt-file and
* wasn't a good decision which I made 2008
    * see [Single Responsibility Principle (SRP)]
    * see [Separation of Concerns (SoC)]


<br />
In [SokubanFX] I decide to be a little lazy and use for all maps one properties-file.

TODO screenshot from the package with maps.properties and the open file.

So its really easy to read a map and convert it to a `List<String>`:
```java
class MapLoader implements IMapConfiguration {
    
    MapLoader() {
        this.init();
    }
    
    // Register the maps.properties file as a ResourceBundle.
    private void init() {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Init MapLoader"); // NOI18N
        
        PropertiesFacade.INSTANCE.register(KEY__MAP__RESOURCE_BUNDLE);
    }
    
    // Returns the mapped value from the key.
    private String getProperty(String propertyKey) {
        return PropertiesFacade.INSTANCE.getProperty(KEY__MAP__RESOURCE_BUNDLE, propertyKey);
    }
	
    /**
     * Loads the map from the ResourceBundle and returns the converted map as a List<String>.
     * 
     * @param level Which map should be loaded?
     * return The converted map as a list from strings. 
     */
    public List<String> loadMapAsStrings(int level) {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Load map as Strings: " + level); // NOI18N
        
        final List<String> mapAsStrings = FXCollections.observableArrayList();
        final String mapAsString = this.getProperty(KEY__MAP__POINT + level);
        final String[] splits = mapAsString.split(";"); // NOI18N
        mapAsStrings.addAll(Arrays.asList(splits));
        
        return mapAsStrings;
    }

}
```


<br />
##### Textbased maps in views<a name="TextbasedMaps" />

Because we are in a prototype I deside for me

TODO add one screenshot. left -> preview-map, right -> game-map



<br />
Conclusion<a name="Conclusion" />
---

TODO write conclusion



<br />
About the autor<a name="Autor" />
---

Let me introduce myself. My name is `Peter Rogge` and I'm a software developer 
in Wolfsburg, Germany.

Since `2008` I work by [H+D International Group] which is an IT- and engineering 
service provider represented nationally and internationally in over 20 locations 
with the head-quarters in Wolfsburg, Germany.


<br />
In my free time I investigate between `2009` an `2012` some time in [NetBeans RCP] &#40;Rich 
Client Platform&#41; development.  
See  
* The `interview` [Help for Multilingual NetBeans Platform Applications] &#40;09.2009&#41; with 
  [Geertjan Wielenga] and me.
* The `book` [NetBeans Platform 6.9 Developer's Guide] &#40;08.2010&#41; which I helped to 
  translate from Germany to English.

<br />
Since `2011` I change my focus to [JavaFX] -> [JavaFX 2.0] to [JavaFX 8] although in `2015` 
I saw a video from [Adam Bien] where he mention he would love to write a [NetBeans RCP] 
plugin for his library [afterburner.fx] when he had more time.  
So I decided to do this:
* See the [GitHub] project [NetBeansIDE-AfterburnerFX-Plugin] &#40;since 09.2015&#41; which is 
  really helpful to speed up the development in combination with the library [afterburner.fx]
  in [JavaFX] application.
* The `interview` [Afterburner.fx NetBeans Plugin Release] &#40;11.2015&#41; with [Adam Bien] and me.
* Have a look in the `video` [DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive] where 
  [Adam Bien] introduce my plugin &#40;at 48:00&#41;.


<br />
##### Contact<a name="Contact" />

Any question? Some helpful criticism?
* Please write an [Issue] or
* send me an `email` to <peter.rogge@yahoo.de>



<br />
Articles in this series<a name="Articles" />
---

* This article series described how I create the game [SokubanFX] with [JavaFX] 
  and [NetBeans IDE].
* The articles in this series are licensed under [General Public License 3.0].

<br />
* **&#40;updated&#41;** The article [01 Setup the project] describes the steps 
  how to setup a new project in [GitHub] with my project template and what are 
  the advantages from using this template [Project-Template-afterburnerfx-Naoghuman].
* **&#40;new&#41;** The article [02 Create first prototype] describes the steps and 
  decisions which I make during the implementation from the first `prototype`.
* _(not started)_ The article [03 Stabilization from the prototype] describes the 
  steps how I stabilize the prototype.
* _(not started)_ The article [04 Extend the prototype] describes the steps to 
  extend the prototype.



[//]: # (Images)
[emoticon_smile]:https://cloud.githubusercontent.com/assets/8161815/10268707/76d6c5f2-6ac1-11e5-9330-15a8943f1b0d.png
[emoticon_grin]:https://cloud.githubusercontent.com/assets/8161815/10268709/7b073800-6ac1-11e5-85b3-d0e342acc403.png
[emoticon_tongue]:https://cloud.githubusercontent.com/assets/8161815/10268706/741f41fe-6ac1-11e5-88ea-1b4d807b2283.png
[sokubanfx_v0.1.0-PROTOTYPE]:https://cloud.githubusercontent.com/assets/8161815/15157275/305a7ba6-16eb-11e6-9b1f-737c9a0ca2b8.png


[//]: # (Links)
[01 Setup the project]:01_Setup-the-project.md
[02 Create first prototype]:02_Create-first-prototype.md
[03 Stabilization from the prototype]:03_Stabilization-from-the-prototype.md
[04 Extend the prototype]:04_Extend-the-prototype.md
[Adam Bien]:http://www.adam-bien.com/roller/abien/
[Afterburner.fx NetBeans Plugin Release]:http://www.adam-bien.com/roller/abien/entry/afterburner_fx_netbeans_plugin_release
[afterburner.fx]:https://github.com/AdamBien/afterburner.fx
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
[Geertjan Wielenga]:https://blogs.oracle.com/geertjan/entry/welcome_to_me
[General Public License 3.0]:http://www.gnu.org/licenses/gpl-3.0.en.html
[GitHub]:https://github.com/
[Issue]:https://github.com/Naoghuman/articles/issues
[H+D International Group]:https://www.hud.de/en/
[Help for Multilingual NetBeans Platform Applications]:
[Java]:https://en.wikipedia.org/wiki/Java_%28programming_language%29
[JavaFX]:http://docs.oracle.com/javase/8/javase-clienttechnologies.htm
[JavaFX 2.0]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_2.0
[JavaFX 8]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_8
[NetBeans IDE]:https://netbeans.org/
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin
[Project-Template-afterburnerfx-Naoghuman]:https://github.com/Naoghuman/Project-Templates/tree/master/Project-Template-afterburnerfx-Naoghuman
[Separation of Concerns (SoC)]:https://en.wikipedia.org/wiki/Separation_of_concerns
[Single Responsibility Principle (SRP)]:https://en.wikipedia.org/wiki/Single_responsibility_principle
[SokubanFX]:https://github.com/Naoghuman/SokubanFX
[Sokuban-Clone]:https://github.com/Naoghuman/sokuban-clone
[SokubanFX-0.1.0-PROTOTYPE_2016-04-30_08-22.zip]:https://github.com/Naoghuman/SokubanFX/releases/tag/v0.1.0
[Swing2D]:https://docs.oracle.com/javase/tutorial/2d/
