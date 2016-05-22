03 Stabilization from the prototype
===



<br />
Intention
---

In the last articles I show first how to setup the new project with another 
[GitHub] project from me [Project-Template-afterburnerfx-Naoghuman] and what are 
the advantages are from using this template -> [01 Setup the project]. Then I 
describes the steps and decisions which I make during the implementation from 
the first `prototype` -> [02 Create first prototype].

In this article I described how I stablilizate the prototype. Also some new features 
like `user can now handle the application with KeyEvents` or the implementation from 
the library [Ikonli].

 Click on the picture to see the `SokubanFX v0.2.0-PROTOTYPE` in action :smile: in YouTube.
[![sokubanfx_v0.2.0-PROTOTYPE.png][sokubanfx_v0.2.0-PROTOTYPE]](https://youtu.be/iKBfqk0ANj8 "SokubanFX v0.2.0-PROTOTYPE")

<br/>
You can download the new version here: [SokubanFX-v0.2.0-PROTOTYPE_2016-05-08_18-44.zip]


<br />
Content
---

* (v) TODO [Stabilization from the prototype](#Stabilization)
    * (v) [Stabilize with JUnit tests](#StabilizeJUnit)
    * ( ) TODO REWRITE [Stabilize with Refactoring](#StabilizeRefactoring)
* ( ) TODO [New Features in SokubanFX v0.2.0-PROTOTYPE](#NewFeatures)
    * (v) [Change internal to lambda expressions](#LambdaExpressions)
    * ( ) [User can now handle the application with KeyEvents](#UserKeyEvents)
    * ( ) [Implement the library Ikonli for icons](#LibraryIkonli)
    * ( ) [In the Preview all 10sec a new random map will be now shown](#PreviewRandomMap)
* TODO ( ) [Conclusion](#Conclusion)
* (v) [About the autor](#Autor)
    * (v) [Contact](#Contact)
* ( ) [Articles in this series](#Articles)
    * ( ) TODO If this article ready, then change the additional informations
	      in (xy) in all articles + ReadMe (articles, SokubanFX)



<br />
Stabilization from the prototype<a name="Stabilization" />
---

In this part I describes the steps how to stabilize the project.


<br />
##### Stabilize with JUnit tests<a name="StabilizeJUnit" />

The [NetBeans IDE] have a nice feature -> Create new [JUnit] `Test for Existing Class` 
under `New` -> `Unit Tests`.
* This wizard will generate automatically a [JUnit] for an existing class.
* Select the class which should be tested.
* The wizard fill automatically the test package and name for the new test class.
* Check the options under `Method Access Levels`, `Generated Code` and `Generated 
  Comments`.
* That was it :smile: .

![wizard-new-test-for-existing-class.png][wizard-new-test-for-existing-class]


<br />
So the basic classes and methods are really fast generated.

![test-packages.png][test-packages]

<br />
```java
public class CollisionCheckerTest {
    
    private MapModel mapModel;
    
    private ObservableList<Coordinates> boxes;
    private ObservableList<Coordinates> places;
    private ObservableList<Coordinates> walls;
    
    @Before
    public void setUp() {
        mapModel = new MapModel();
        mapModel.setPlayer(10, 10);
        
        boxes = FXCollections.observableArrayList();
        places = FXCollections.observableArrayList();
        walls = FXCollections.observableArrayList();
    }

    @Test
    public void getDefault() {
        CollisionChecker result = CollisionChecker.getDefault();
        assertNotNull("Instance from CollisionChecker muss != NULL", result); // NOI18N
    }
    
    @Test
    public void checkCollisionPlayerBoxWallWithDirectionDOWN() {
        // direction
        final EDirection direction = EDirection.DOWN;
        
        // There is a box before the player (y=11) and no second box (y!=12) before the first box
        boxes.clear();
        boxes.add(Coordinates.getDefault(10,  2));
        boxes.add(Coordinates.getDefault(10, 11)); // <--- 1.
        boxes.add(Coordinates.getDefault(10, 15));
        mapModel.setBoxes(boxes);
        
        walls.clear();
        mapModel.setWalls(walls);
        
        ECollisionResult result = CollisionChecker.getDefault().checkCollisionPlayerBoxWall(direction, mapModel);
        assertEquals("There is a box before the player (y=11) and no second box (y!=12) before the first box -> CollisionResult.PLAYER_AGAINST__BOX_NONE", ECollisionResult.PLAYER_AGAINST__BOX_NONE, result);
        
        // There is a box before the player (y=11) and a wall at (y=12)
        boxes.clear();
        boxes.add(Coordinates.getDefault(10,  1));
        boxes.add(Coordinates.getDefault(10, 11)); // <--- 1.
        boxes.add(Coordinates.getDefault(10, 15));
        mapModel.setBoxes(boxes);
        
        walls.clear();
        walls.add(Coordinates.getDefault(10,  2));
        walls.add(Coordinates.getDefault(10, 12)); // <--- 2.
        walls.add(Coordinates.getDefault(10, 14));
        mapModel.setWalls(walls);
        
        result = CollisionChecker.getDefault().checkCollisionPlayerBoxWall(direction, mapModel);
        assertEquals("There is a box before the player (y=11) and a wall at (y=12) -> CollisionResult.PLAYER_AGAINST__BOX_WALL", ECollisionResult.PLAYER_AGAINST__BOX_WALL, result);
    }
    
    // and for all other combination also a unit test is be created:
    public void checkCollisionPlayerBoxBoxWithDirectionLEFT()
    public void checkCollisionPlayerBoxBoxWithDirectionRIGHT()
    public void checkCollisionPlayerBoxBoxWithDirectionUP()
    public void checkCollisionPlayerBoxPlaceWithDirectionDOWN()
    public void checkCollisionPlayerBoxPlaceWithDirectionLEFT()
    public void checkCollisionPlayerBoxPlaceWithDirectionRIGHT()
    public void checkCollisionPlayerBoxPlaceWithDirectionUP()
    public void checkCollisionPlayerBoxWallWithDirectionDOWN()
    public void checkCollisionPlayerBoxWallWithDirectionLEFT()
    public void checkCollisionPlayerBoxWallWithDirectionRIGHT()
    public void checkCollisionPlayerBoxWallWithDirectionUP()
    public void checkCollisionPlayerBoxWithDirectionDOWN()
    public void checkCollisionPlayerBoxWithDirectionLEFT()
    public void checkCollisionPlayerBoxWithDirectionRIGHT()
    public void checkCollisionPlayerBoxWithDirectionUP()
    public void checkCollisionPlayerWallWithDirectionDOWN()
    public void checkCollisionPlayerWallWithDirectionLEFT()
    public void checkCollisionPlayerWallWithDirectionRIGHT()
    public void checkCollisionPlayerWallWithDirectionUP()

}
```


<br />
```java
public class MapMovementTest {

    @Test
    public void testCheckIsMapFinishFalse() {
        MapMovement mm = new MapMovement();
        
        MapModel mmo = new MapModel();
        ObservableList<Coordinates> boxes = FXCollections.observableArrayList();
        boxes.add(Coordinates.getDefault(5, 5));
        boxes.add(Coordinates.getDefault(15, 15));
//        boxes.add(Coordinates.getDefault(25, 25)); // <-- not all boxes are on places
        mmo.setBoxes(boxes);
        
        ObservableList<Coordinates> places = FXCollections.observableArrayList();
        places.add(Coordinates.getDefault(5, 5));
        places.add(Coordinates.getDefault(15, 15));
        places.add(Coordinates.getDefault(25, 25));
        mmo.setPlaces(places);
        
        MovementResult mr = mm.checkIsMapFinish(mmo);
        
        assertFalse(mr.isMapFinish());
    }

    @Test
    public void testCheckIsMapFinishTrue() {
        MapMovement mm = new MapMovement();
        
        MapModel mmo = new MapModel();
        ObservableList<Coordinates> boxes = FXCollections.observableArrayList();
        boxes.add(Coordinates.getDefault(5, 5));
        boxes.add(Coordinates.getDefault(15, 15));
        boxes.add(Coordinates.getDefault(25, 25)); // <-- all boxes are on places
        mmo.setBoxes(boxes);
        
        ObservableList<Coordinates> places = FXCollections.observableArrayList();
        places.add(Coordinates.getDefault(5, 5));
        places.add(Coordinates.getDefault(15, 15));
        places.add(Coordinates.getDefault(25, 25));
        mmo.setPlaces(places);
        
        MovementResult mr = mm.checkIsMapFinish(mmo);
        
        assertTrue(mr.isMapFinish());
    }

    /*
        Not needed, because the method is in CollisionCheckerTest#checkCollisionPlayerXyz(...)
        tested.
    */
//    @Test
//    public void testCheckMovePlayerTo() {
//        MapMovement instance = new MapMovement();
//        MovementResult result = instance.checkMovePlayerTo(direction, mapModel);
//    }
    
}
```

<br />
```java
public class MovementResultTest {

    @Test
    public void testGetDefault() {
        MovementResult mr = MovementResult.getDefault();
        
        assertEquals(EAnimation.NONE, mr.getAnimation());
        assertNotNull(mr.getBoxToMove());
        assertEquals(Coordinates.getDefault(), mr.getBoxToMove());
        assertEquals(EMovement.NONE, mr.getMovement());
        assertNotNull(mr.getPlayerToMove());
        assertEquals(Coordinates.getDefault(), mr.getPlayerToMove());
        assertFalse(mr.isMapFinish());
    }

    @Test
    public void getBoxToMove() {
        MovementResult mr = MovementResult.getDefault();
        
        assertNotNull(mr.getBoxToMove());
        assertEquals(Coordinates.getDefault(), mr.getBoxToMove());
    }

    @Test
    public void setBoxToMove() {
        MovementResult mr = MovementResult.getDefault();
        mr.setBoxToMove(Coordinates.getDefault(2, 7));
        
        assertNotNull(mr.getBoxToMove());
        assertEquals(2, mr.getBoxToMove().getX());
        assertEquals(7, mr.getBoxToMove().getY());
    }

    @Test
    public void getPlayerToMove() {
        MovementResult mr = MovementResult.getDefault();
        
        assertNotNull(mr.getPlayerToMove());
        assertEquals(Coordinates.getDefault(), mr.getPlayerToMove());
    }

    @Test
    public void setPlayerToMove() {
        MovementResult mr = MovementResult.getDefault();
        mr.setPlayerToMove(Coordinates.getDefault(2, 7));
        
        assertNotNull(mr.getPlayerToMove());
        assertEquals(2, mr.getPlayerToMove().getX());
        assertEquals(7, mr.getPlayerToMove().getY());
    }

    @Test
    public void isMapFinish() {
        MovementResult mr = MovementResult.getDefault();
        
        assertFalse(mr.isMapFinish());
    }

    @Test
    public void setIsMapFinish() {
        MovementResult mr = MovementResult.getDefault();
        mr.setIsMapFinish(true);
        
        assertTrue(mr.isMapFinish());
    }

    @Test
    public void getAnimation() {
        MovementResult mr = MovementResult.getDefault();
        
        assertEquals(EAnimation.NONE, mr.getAnimation());
    }

    @Test
    public void setAnimation() {
        MovementResult mr = MovementResult.getDefault();
        mr.setAnimation(EAnimation.REALLY_GREAT);
        
        assertEquals(EAnimation.REALLY_GREAT, mr.getAnimation());
    }

    @Test
    public void getMovement() {
        MovementResult mr = MovementResult.getDefault();
        
        assertEquals(EMovement.NONE, mr.getMovement());
    }

    @Test
    public void setMovement() {
        MovementResult mr = MovementResult.getDefault();
        mr.setMovement(EMovement.PLAYER_AND_BOX);
        
        assertEquals(EMovement.PLAYER_AND_BOX, mr.getMovement());
    }
    
}
```


<br />
##### Stabilize with Refactoring<a name="StabilizeRefactoring" />

One important part for me in stabilzation from a prototype is `refactoring`:
* [Refactoring - Improving the Design of Existing Code] by [Martin Fowler].

Also I find it helpful to have the main points from [Clean Code Developer] 
&#40;:de:&#41; in mind during the stabilization.

<br />
So what can be done to stabilize the program :question:
* Delete unnecessary files.
* Start with documentation (at first with the project ReadMe).
* Update the dependencies to included libraries.
* Update the release notes.
* Check the package structure and move classes if needed.
* Switch from [Java] classes to [JavaFX] classes when possible.
* Check the names from classes, interfaces and enums and rename it if needed.
* Move functionalities from classes to new classes -> [Single Responsibility Principle (SRP)].
* Check layout in views and simplified if possible.
* and more...

<br />
In generall things are done when they are ready :laughing: .  
But here are 3 points which helps me to decided when to go to the next phase in 
the program development.
* The time is over which I planned for the stabilization.
* The top :five: areas are cleaned.
* Points which I havn't the time to cleanup are noted. 



<br />
New Features in SokubanFX v0.2.0-PROTOTYPE<a name="NewFeatures" />
---

In this section I will list what is new in SokubanFx v0.2.0.


<br />
##### Change internal to lambda expressions<a name="LambdaExpressions" />

First internal I switch to [Lambda Expressions] which are new in [Java 8].

<br />
Here a very simple example how to stream over every `item` in a [ObservableList]:
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {

    private void displayMap() {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Display Map"); // NOI18N
        
        vbMap.getChildren().clear();
        vbMap.getChildren().add(this.getLabel("Map: " + actualMapModel.getLevel())); // NOI18N
        vbMap.getChildren().add(this.getLabel("")); // NOI18N
        
        final ObservableList<String> mapAsStrings = MapFacade.INSTANCE.convertMapCoordinatesToStrings(actualMapModel);
        mapAsStrings.stream() // 1
                .forEach(line -> { // 2
                    vbMap.getChildren().add(this.getLabel(line));
                });
    }

    private Label getLabel(String text) {
        final Label label = new Label(text);
        label.setFont(new Font("Monospaced Regular", 16.0d));
        
        return label;
    }
    ...

}
```

1. This [Lambda Expressions] streams simple over every `item` in the [ObservableList]<String> mapAsStrings.
2. For every `item` in the [ObservableList] a new formated label will be added to the [VBox] vbMap.

<br />
Next example shows how to iterate over a list, check something and if okay then 
update the `coordinatesFounded`:
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {

    private Coordinates calculateFoundedCoordinates(Coordinates coordinatesToCheck, ObservableList<Coordinates> listCoordinates) {
        final Coordinates coordinatesFounded = Coordinates.getDefault();
        if (!Coordinates.isDefault(coordinatesToCheck)) {
            for (Coordinates coordinates : listCoordinates) { // 1 
                if ( // 2
                        coordinates.getX() == coordinatesToCheck.getX()
                        && coordinates.getY() == coordinatesToCheck.getY()
                ) {
                    coordinatesFounded.setX(coordinates.getX()); // 3
                    coordinatesFounded.setY(coordinates.getY());
                    
                    break; // 4
                }
            }
        }
      
        return coordinatesFounded;
    }
    ...

}
```

1. For every existing `coordinates` will be checked
2. if the `coordinates`&#40;x, y&#41; equals to the &#40;x, y&#41; parameters 
   from the `coordinatesToCheck`.
3. If so then the `coordinatesFounded` will be updated.
4. Because we have updated the `coordinatesFounded` we can leave the `for-each` 
   iteration.

<br />
After the conversion from the `for-each` iteration to a [Lambda Expressions] we have:
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {

    private Coordinates calculateFoundedCoordinates(Coordinates coordinatesToCheck, ObservableList<Coordinates> listCoordinates) {
        final Coordinates coordinatesFounded = Coordinates.getDefault();
        if (!Coordinates.isDefault(coordinatesToCheck)) {
            listCoordinates.stream() // 1
                    .filter(coordinates -> { // 2
                        final boolean shouldCoordinatesUpdate = 
                                coordinates.getX() == coordinatesToCheck.getX()
                                && coordinates.getY() == coordinatesToCheck.getY(); 
                        return shouldCoordinatesUpdate;
                    })
                    .findFirst() // 3
                    .ifPresent(coordinates -> { // 4
                        coordinatesFounded.setX(coordinates.getX());
                        coordinatesFounded.setY(coordinates.getY());
                    });
        }
      
        return coordinatesFounded;
    }
    ...

}
```

1. Over every existing `item` in the [ObservableList]<String> `listCoordinates` 
   will be streamed.
2. Then for every founded `item` will be checked &#40;filter&#41; if the 
   `coordinates`&#40;x, y&#41; equals to the &#40;x, y&#41; parameters from the 
   `coordinatesToCheck`.
3. For the `first` match an [Optional<T>] will be returned.
4. If the [Optional<T>] is not `null` &#40;means `ifPresent==true`&#41; then 
   `coordinatesFounded` will be updated.

<br />
In the next example the shown method will check if all `boxes` are on a `place`, 
that mean if so then the map is `finished`.
```java
public class CollisionChecker {

    public ECollisionResult checkCollisionPlayerBoxPlaceFinish(MapModel mapModel) {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Check collision 'player -> box -> place -> finish'"); // NOI18N
        
        final ObservableList<Coordinates> places = mapModel.getPlaces();
        final ObservableList<Coordinates> boxes = mapModel.getBoxes();
        
        int counter = 0;
        for (Coordinates place : places) { // 1
            for (Coordinates box : boxes) { // 2
                if (
                        place.getX() == box.getX() // 3
                        && place.getY() == box.getY()
                ) {
                    ++counter; // 4
                    break; // 5
                }
            }
        }
        
        // All boxes are on places?
        final int maxPlaces = places.size();
        final boolean allBoxesAreOnPlaces = (maxPlaces == counter);
        ECollisionResult collisionResult = ECollisionResult.NONE;
        if (allBoxesAreOnPlaces) { // 6
            collisionResult = ECollisionResult.PLAYER_AGAINST__BOX_PLACE_AND_FINISH;
        }
        
        return collisionResult;
    }
    ...

}
```

1. Iterate over every `place`.
2. Iterate over every `box`.
3. Check if a box is on a place.
4. Increment the `counter` for places which have a box on it.
5. Leave the iteration from the boxes and start the next iteration with a new place.
6. Check if the map is `finished` &#40;all boxes are on the places&#41;.

<br />
After the conversion to a [Lambda Expressions] we have following algorithm:
```java
public class CollisionChecker {

    public ECollisionResult checkCollisionPlayerBoxPlaceFinish(MapModel mapModel) {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Check collision 'player -> box -> place -> finish'"); // NOI18N
        
        final ObservableList<Coordinates> places = mapModel.getPlaces();
        final ObservableList<Coordinates> boxes = mapModel.getBoxes();
        
        final AtomicInteger counter = new AtomicInteger(0);
        places.forEach(place -> { // 1
            boxes.stream() // 2
                    .filter(box -> { // 3
                        final boolean shouldCounterIncrement = 
                                place.getX() == box.getX()
                                && place.getY() == box.getY();
                        return shouldCounterIncrement;
                    })
                    .findFirst() // 4
                    .ifPresent(box -> { // 5
                        counter.set(counter.get() + 1);
                    });
        });
        
        // All boxes are on places?
        final int maxPlaces = places.size();
        final boolean allBoxesAreOnPlaces = (maxPlaces == counter.get());
        ECollisionResult collisionResult = ECollisionResult.NONE;
        if (allBoxesAreOnPlaces) { // 6
            collisionResult = ECollisionResult.PLAYER_AGAINST__BOX_PLACE_AND_FINISH;
        }
        
        return collisionResult;
    }
    ...

}
```

1. Iterate over every `place`.
2. Stream through all `boxes`.
3. Then for every `box` will be checked &#40;filter&#41; if the `place`&#40;x, y&#41; 
   equals to the `box`&#40;x, y&#41;.
4. For the `first` match an [Optional<T>] will be returned.
5. If the [Optional<T>] is not `null` &#40;means `ifPresent==true`&#41; then 
   `counter` will be increased by one.
6. Check if the map is `finished` &#40;all boxes are on the places&#41;.


<br />
##### User can now handle the application with KeyEvents<a name="UserKeyEvents" />


<br />
##### Implement the library Ikonli for icons<a name="LibraryIkonli" />


<br />
##### In the Preview all 10sec a new random map will be now shown<a name="PreviewRandomMap" />











<br />
Conclusion<a name="Conclusion" />
---

1) Stabilization

2) Some new features

Download:  
[SokubanFX-v0.2.0-PROTOTYPE_2016-05-08_18-44.zip]

YouTube:
[![sokubanfx_v0.2.0-PROTOTYPE.png][sokubanfx_v0.2.0-PROTOTYPE]](https://youtu.be/iKBfqk0ANj8 "SokubanFX v0.2.0-PROTOTYPE")









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
  and [NetBeans IDE] inspired by my [Java] [Swing2D] game [Sokuban-Clone] which 
  I wrote `2008`.
* The articles in this series are licensed under [General Public License 3.0].


<br />
##### Articles
* **&#40;updated&#41;** The article [01 Setup the project] describes the steps 
  how to setup a new project in [GitHub] with my project template and what are 
  the advantages from using this template [Project-Template-afterburnerfx-Naoghuman].
* **&#40;new&#41;** The article [02 Create first prototype] describes the steps and 
  decisions which I make during the implementation from the first `prototype`.
* _&#40;not started&#41;_ The article [03 Stabilization from the prototype] 
  describes the steps how I stabilize the prototype.



[//]: # (Images)
[sokubanfx_v0.2.0-PROTOTYPE]:https://cloud.githubusercontent.com/assets/8161815/15447479/e90b31d0-1f43-11e6-864e-d77b5c4cc7df.png
[test-packages]:https://cloud.githubusercontent.com/assets/8161815/15449322/7fd7d9e8-1f7a-11e6-916a-a324655bbacc.png
[wizard-new-test-for-existing-class]:https://cloud.githubusercontent.com/assets/8161815/15449372/6573d96a-1f7c-11e6-858d-57ee8e8a18b8.png



[//]: # (Links)
[01 Setup the project]:01_Setup-the-project.md
[02 Create first prototype]:02_Create-first-prototype.md
[03 Stabilization from the prototype]:03_Stabilization-from-the-prototype.md
[Adam Bien]:http://www.adam-bien.com/roller/abien/
[Afterburner.fx NetBeans Plugin Release]:http://www.adam-bien.com/roller/abien/entry/afterburner_fx_netbeans_plugin_release
[afterburner.fx]:https://github.com/AdamBien/afterburner.fx
[Clean Code Developer]:http://clean-code-developer.de/
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
[Geertjan Wielenga]:https://blogs.oracle.com/geertjan/entry/welcome_to_me
[General Public License 3.0]:http://www.gnu.org/licenses/gpl-3.0.en.html
[GitHub]:https://github.com/
[H+D International Group]:https://www.hud.de/en/
[Help for Multilingual NetBeans Platform Applications]:https://dzone.com/articles/multilingual-netbeans-platform-applications
[Ikonli]:https://github.com/aalmiray/ikonli
[Issue]:https://github.com/Naoghuman/articles/issues
[Java]:https://en.wikipedia.org/wiki/Java_%28programming_language%29
[Java 8]:https://www.java.com/en/download/faq/java8.xml
[JavaFX]:http://docs.oracle.com/javase/8/javase-clienttechnologies.htm
[JavaFX 2.0]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_2.0
[JavaFX 8]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_8
[JUnit]:http://junit.org/junit4/
[Lambda Expressions]:https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html
[Martin Fowler]:http://martinfowler.com/
[NetBeans IDE]:https://netbeans.org/
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin
[ObservableList]:https://docs.oracle.com/javase/8/javafx/api/javafx/collections/ObservableList.html
[Optional<T>]:https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html
[Project-Template-afterburnerfx-Naoghuman]:https://github.com/Naoghuman/Project-Templates/tree/master/Project-Template-afterburnerfx-Naoghuman
[Refactoring - Improving the Design of Existing Code]:http://martinfowler.com/books/refactoring.html
[Single Responsibility Principle (SRP)]:https://en.wikipedia.org/wiki/Single_responsibility_principle
[SokubanFX]:https://github.com/Naoghuman/SokubanFX
[SokubanFX v0.2.0-PROTOTYPE]:https://youtu.be/iKBfqk0ANj8
[SokubanFX-v0.2.0-PROTOTYPE_2016-05-08_18-44.zip]:https://github.com/Naoghuman/SokubanFX/releases/tag/v0.2.0
[Sokuban-Clone]:https://github.com/Naoghuman/sokuban-clone
[Swing2D]:https://docs.oracle.com/javase/tutorial/2d/
[VBox]:https://docs.oracle.com/javase/8/javafx/api/javafx/scene/layout/VBox.html
