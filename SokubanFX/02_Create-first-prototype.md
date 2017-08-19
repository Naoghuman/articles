02 Create first prototype
===



Intention
---

In the last article [01 Setup the project] I show how to setup the new project 
with another [GitHub] project from me [Project-Template-afterburnerfx-Naoghuman] 
and what are the advantages from using this template.

In this article I will describes the steps and decisions which I make during the 
implementation from the first `prototype`. Click on the picture to see the 
`SokubanFX v0.1.0-PROTOTYPE` in action :smile: in YouTube.

[![sokubanfx_v0.1.0-PROTOTYPE.png][sokubanfx_v0.1.0-PROTOTYPE]](https://www.youtube.com/watch?v=Kp1vWjLTIvY "SokubanFX v0.1.0-PROTOTYPE")

You can download the `prototype` here: [SokubanFX-0.1.0-PROTOTYPE_2016-04-30_08-22.zip]



Content
---

* [Create first prototype](#CreateFirstPrototype)
    * [Basic functionalities from the project](#BasicFunctionalities)
    * [Functionalities like collision, evaluation, movement...](#Functionalities)
    * [Persistence from the maps](#PersistenceMaps)
    * [Textbased maps in views](#TextbasedMaps)
* [Conclusion](#Conclusion)
* [About the autor](#Autor)
    * [Contact](#Contact)
* [Articles in this series](#Articles)



Create first prototype<a name="CreateFirstPrototype" />
---

Like I said in the section `Intention` here are the steps and decisions which I 
make during the implementation from the first `prototype` from my new [JavaFX], 
[Maven] game [SokubanFX].

> So here is the `importants` decision from me -> no game-engine :flushed: .

Normally a game have a game-loop which runs with xy fps. The engine will then 
loops over the `update()` and `render()` methods. [JavaFX] comes with own 
classes around this topic like [Animation] -> the parent class from [Timeline] 
and [Transition].

If the functionality from this classes and all sub-classes not enough, then I 
have the possibility to use the class [AnimationTimer] which triggers the 
method `handle(long)` in every frame (which leeds then to a game-engine :grin: ).


##### Basic functionalities from the project<a name="BasicFunctionalities" />

Because I used my project template [Project-Template-afterburnerfx-Naoghuman] to 
create the [SokubanFX] project all basic functionalities which I want was almost 
implemented :grinning: :sunglasses: .

> Logging, ActionEvent- and Properties-Handling,  support for the [JavaFX] 
> development, easy generation from an executable jar file aso.

For more detailed informations plz see the article [01 Setup the project].


##### Functionalities like collision, evaluation, movement...<a name="Functionalities" />

In this section I will speak about `collision`, `evaluation` and `movement`. 
Beside `loading` and `converting` a map &#40;which I described later in this 
article&#41; this are the main funcitionalities in the game.

Following workflow is given:  
a) User want to move the player, for example he pressed the key DOWN.  
b) Now all possible collisions must be checked, before something can moved or not.  
c) With the `CheckMovementResult` then the evaluation from the player (and optional 
   a box) will be done or not.  
d) Now the map with eventually new coordinates can be displayed.  
e) Finally after a successful move the game should be checked if the map is finished.
   If so the next map can be shown.

a) User pressed the key DOWN
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {

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
    ...
}
```

b) Check possible collisions -> returns what happen.
```java
public class MapMovement {
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
	
	// and do all other collision checks here also.
    }
    ...
}
```

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

c) Evalutate the `CheckMovementResult` -> new `Coordinates` for the player and 
   optional a box.
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {
    private void evaluatePlayerMoveTo(CheckMovementResult checkMovementResult) {
        // Animation will here done later
        
        final EMovement movement = checkMovementResult.getMovement();
        if (
                movement.equals(EMovement.PLAYER)
                || movement.equals(EMovement.PLAYER_AND_BOX)
        ) {
            // Update player
            final Coordinates player = actualMapModel.getPlayer();
            player.setX(player.getTranslateX());
            player.setY(player.getTranslateY());
            
            if (movement.equals(EMovement.PLAYER)) {
                this.displayMap();
                return;
            }
            
            // Update box
            final Coordinates boxToMove = movement.getCoordinatesBoxToMove();
            final List<Coordinates> boxes = actualMapModel.getBoxes();
            for (Coordinates box : boxes) {
                if (
                        box.getX() == boxToMove.getX()
                        && box.getY() == boxToMove.getY()
                ) {
                    box.setX(boxToMove.getTranslateX());
                    box.setY(boxToMove.getTranslateY());
                }
            }
            
            this.displayMap();
        }
    }
    ...
}
```

d) Display the map -> shows the actual updated map.
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {
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
    ...
}
```

e) Finally evaluate if the map is finished. If yes show the new map.
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {
    private void evaluateIsMapFinish(boolean isMapFinish) {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Evaluate is Map finish"); // NOI18N
        
        // Keep going :)
        if (!isMapFinish) {
            return;
        }
        
        // Map is finish !!
        final int actualMap = PreferencesFacade.INSTANCE.getInt(
                IMapConfiguration.PROP__ACTUAL_MAP,
                IMapConfiguration.PROP__ACTUAL_MAP__DEFAULT_VALUE);
        PreferencesFacade.INSTANCE.putInt(
                IMapConfiguration.PROP__ACTUAL_MAP,
                actualMap + 1);
        
        // load next map
        this.loadActualMap();
        this.displayMap();
    }
    ...
}
```


##### Persistence from the maps<a name="PersistenceMaps" />

In my old [Java] [Swing2D] game [Sokuban-Clone] the maps are persist as txt-files.

![sokuban-clone-map-txt.png][sokuban-clone-map-txt]

This maps was readed with:
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
* wasn't a good decision which I made `2008`...
    * see [Single Responsibility Principle (SRP)]
    * see [Separation of Concerns (SoC)]

In [SokubanFX] I decide to be a little lazy and use for all maps one properties-file.

![sokuban-map-properties.png][sokuban-map-properties]

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
     * Loads the map from the ResourceBundle and returns the loaded map as a List<String>.
     * 
     * @param level Which map should be loaded?
     * return The loaded map as a list from strings. 
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


##### Textbased maps in views<a name="TextbasedMaps" />

Because we are in a prototype I decided for me to show the game without `graphics`, 
means `text based`:

`Preview` view
![preview-view.png][preview-view]

`Game` view
![game-view.png][game-view]

Loading a map from the `.properties` file as `List<String>`:
```java
class MapLoader implements IMapConfiguration {
    public List<String> loadMapAsStrings(int level) {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Load map as Strings: " + level); // NOI18N
        
        final List<String> mapAsStrings = FXCollections.observableArrayList();
        final String mapAsString = this.getProperty(KEY__MAP__POINT + level);
        final String[] splits = mapAsString.split(";"); // NOI18N
        mapAsStrings.addAll(Arrays.asList(splits));
        
        return mapAsStrings;
    }
    ...
}
```

Converting a `List<String>` to a `MapModel`:
```java
public class MapConverter {
    public MapModel convertStringsToMap(final int level, final List<String> mapAsStrings) {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Convert strings to MapModel"); // NOI18N
        
        final MapModel mapModel = new MapModel();
        mapModel.setLevel(level);
        mapModel.setMapAsStrings(mapAsStrings);
        
        int columns = 0;
        int rows = 0;
        for (String line : mapAsStrings) {
            for (int x = 0; x < line.length(); x++) {
                columns = Math.max(columns, x + 1);
                
                final Character c = line.charAt(x);
                final int x1 = x + 1;
                final int y1 = rows + 1;
                switch(c) {
                    case 'A': // NOI18N
                    case 'B': { mapModel.addWall(x1, y1);   break; } // NOI18N
                    
                    case '0': { mapModel.setPlayer(x1, y1); break; } // NOI18N
                    case '1': { mapModel.addBox(x1, y1);    break; } // NOI18N
                    case '2': { mapModel.addPlace(x1, y1);  break; } // NOI18N
                    
                    case '-': // NOI18N
                    default: { }
                }
            }
            
            rows = rows + 1;
        }
        
        mapModel.setColumns(columns);
        mapModel.setRows(rows);
        
        return mapModel;
    }
    ...
}
```

Converting a `MapModel` to a `List<String>`:
```java
public class MapConverter {
    public List<String> convertMapCoordinatesToStrings(MapModel mapModel) {
        final List<String> mapAsStrings = FXCollections.observableArrayList();
        final int columns = mapModel.getColumns();
        final int rows = mapModel.getRows();
        final int level = mapModel.getLevel();
        
        final Coordinates player = mapModel.getPlayer();
        final List<Coordinates> boxes = mapModel.getBoxes();
        final List<Coordinates> places = mapModel.getPlaces();
        final List<Coordinates> walls = mapModel.getWalls();

        // - = Empty sign
        for (int ro = 0; ro < rows; ro++) {
            final StringBuilder sb = new StringBuilder();
            for (int col = 0; col < columns; col++) {
                sb.append("-"); // NOI18N
            }
            mapAsStrings.add(sb.toString());
        }
        
        // A, B = Walls from the level
        for (int ro = 1; ro <= rows; ro++) {
            for (int col = 1; col <= columns; col++) {
                for (Coordinates wall : walls) {
                    if (wall.getX() == col && wall.getY() == ro) {
                        final StringBuilder sb = new StringBuilder();
                        sb.append(mapAsStrings.get(ro - 1));
                        sb.replace(col - 1, col, level % 2 != 0 ? "A" : "B"); // NOI18N
                        mapAsStrings.remove(ro - 1);
                        mapAsStrings.add(ro - 1, sb.toString());
                    }
                }
            }
        }

        ...
    }
    ...
}
```



Conclusion<a name="Conclusion" />
---

With the decisions to read the maps from a `.properties` file and show the maps 
as `text-based` I was be able to focused my energie on the main functionalities 
in the game like `collisions`, `evaluations` and `movement`.  
So I have my prototype in a few hours implemented :thumbsup: .

Download:  
[SokubanFX-0.1.0-PROTOTYPE_2016-04-30_08-22.zip]

YouTube:
[![sokubanfx_v0.1.0-PROTOTYPE.png][sokubanfx_v0.1.0-PROTOTYPE]](https://www.youtube.com/watch?v=Kp1vWjLTIvY "SokubanFX v0.1.0-PROTOTYPE")



About the autor<a name="Autor" />
---

Let me introduce myself. My name is `Peter Rogge` and I'm a software developer 
in Wolfsburg, Germany.

Since `2008` I work by [H+D International Group] which is an IT- and engineering 
service provider represented nationally and internationally in over 20 locations 
with the head-quarters in Wolfsburg, Germany.


In my free time I investigate between `2009` an `2012` some time in [NetBeans RCP] 
&#40;Rich Client Platform&#41; development.  
See  
* The `interview` [Help for Multilingual NetBeans Platform Applications] 
  &#40;09.2009&#41; with [Geertjan Wielenga] and me.
* The `book` [NetBeans Platform 6.9 Developer's Guide] &#40;08.2010&#41; which I 
  helped to translate from Germany to English.

<br />
Since `2011` I change my focus to [JavaFX] &#40;[JavaFX 2.0] - [JavaFX 8]&#41;. 
Although in `2015` I saw a video from [Adam Bien] where he mention he would love 
to write a [NetBeans RCP] plugin for his library [afterburner.fx] when he had 
more time.  
So I decided to do this:
* See the [GitHub] project [NetBeansIDE-AfterburnerFX-Plugin] &#40;since 09.2015&#41; 
  which is really helpful to speed up the development from [JavaFX] applications 
  in combination with the library [afterburner.fx].
* The `interview` [Afterburner.fx NetBeans Plugin Release] &#40;11.2015&#41; 
  with [Adam Bien] and me.
* Have a look in the `video` [DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive] 
  where [Adam Bien] introduce my plugin &#40;at 48:00&#41;.


##### Contact<a name="Contact" />

Any question? Some helpful criticism?
* Please write an [Issue] or
* send me an `email` to <peter.rogge@yahoo.de>



Articles in this series<a name="Articles" />
---

* This article series described how I create the game [SokubanFX] with [JavaFX] 
  and [NetBeans IDE] inspired by my [Java] [Swing2D] game [Sokuban-Clone] which 
  I wrote `2008`.
* All articles in this series are licensed under [General Public License 3.0].


##### Articles

* The article [01 Setup the project] describes the steps how to setup a new project 
  in [GitHub] with my project template and what are the advantages from using this 
  template [Project-Template-afterburnerfx-Naoghuman].
* The article [02 Create first prototype] describes the steps and decisions which 
  I make during the implementation from the first `prototype`.
* The article [03 Stabilization from the prototype] describes the steps how I 
  stabilize the prototype.



[//]: # (Images)
[sokuban-clone-map-txt]:https://cloud.githubusercontent.com/assets/8161815/15273067/655c12dc-1a8e-11e6-97b2-34dc48d8ec2f.png
[sokuban-map-properties]:https://cloud.githubusercontent.com/assets/8161815/15273091/1d577e76-1a8f-11e6-8436-2268932e30b0.png
[sokubanfx_v0.1.0-PROTOTYPE]:https://cloud.githubusercontent.com/assets/8161815/15157275/305a7ba6-16eb-11e6-9b1f-737c9a0ca2b8.png



[//]: # (Links)
[01 Setup the project]:01_Setup-the-project.md
[02 Create first prototype]:02_Create-first-prototype.md
[03 Stabilization from the prototype]:03_Stabilization-from-the-prototype.md
[Adam Bien]:http://www.adam-bien.com/roller/abien/
[Afterburner.fx NetBeans Plugin Release]:http://www.adam-bien.com/roller/abien/entry/afterburner_fx_netbeans_plugin_release
[afterburner.fx]:https://github.com/AdamBien/afterburner.fx
[Animation]:https://docs.oracle.com/javase/8/javafx/api/javafx/animation/Animation.html
[AnimationTimer]:https://docs.oracle.com/javase/8/javafx/api/javafx/animation/AnimationTimer.html
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
[game-view]:https://cloud.githubusercontent.com/assets/8161815/15275677/33cb69ae-1ad2-11e6-9591-12e6f95e5ab1.png
[Geertjan Wielenga]:https://blogs.oracle.com/geertjan/entry/welcome_to_me
[General Public License 3.0]:http://www.gnu.org/licenses/gpl-3.0.en.html
[GitHub]:https://github.com/
[Issue]:https://github.com/Naoghuman/articles/issues
[H+D International Group]:https://www.hud.de/en/
[Help for Multilingual NetBeans Platform Applications]:https://dzone.com/articles/multilingual-netbeans-platform-applications
[Java]:https://en.wikipedia.org/wiki/Java_%28programming_language%29
[JavaFX]:http://docs.oracle.com/javase/8/javase-clienttechnologies.htm
[JavaFX 2.0]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_2.0
[JavaFX 8]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_8
[Maven]:https://maven.apache.org/
[NetBeans IDE]:https://netbeans.org/
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin
[preview-view]:https://cloud.githubusercontent.com/assets/8161815/15275673/2e051eac-1ad2-11e6-9fd1-b3c893f03cff.png
[Project-Template-afterburnerfx-Naoghuman]:https://github.com/Naoghuman/Project-Templates/tree/master/Project-Template-afterburnerfx-Naoghuman
[Separation of Concerns (SoC)]:https://en.wikipedia.org/wiki/Separation_of_concerns
[Single Responsibility Principle (SRP)]:https://en.wikipedia.org/wiki/Single_responsibility_principle
[SokubanFX]:https://github.com/Naoghuman/SokubanFX
[Sokuban-Clone]:https://github.com/Naoghuman/sokuban-clone
[SokubanFX-0.1.0-PROTOTYPE_2016-04-30_08-22.zip]:https://github.com/Naoghuman/SokubanFX/releases/tag/v0.1.0
[Swing2D]:https://docs.oracle.com/javase/tutorial/2d/
[Timeline]:https://docs.oracle.com/javase/8/javafx/api/javafx/animation/Timeline.html
[Transition]:https://docs.oracle.com/javase/8/javafx/api/javafx/animation/Transition.html
