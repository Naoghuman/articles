03 Stabilization from the prototype
===



Intention
---

In the last articles I show first how to setup the new project with another 
[GitHub] project from me [Project-Template-afterburnerfx-Naoghuman] and what are 
the advantages are from using this template -> [01 Setup the project]. Then I 
describes the steps and decisions which I make during the implementation from 
the first `prototype` -> [02 Create first prototype].

In this article I will describe how I stablilizate the prototype. Also some new 
features like `user can now handle the application with KeyEvents` or the 
implementation from the library [Ikonli] are handled.

 Click on the picture to see the `SokubanFX v0.2.0-PROTOTYPE` in action :smile: in YouTube.
[![sokubanfx_v0.2.0-PROTOTYPE.png][sokubanfx_v0.2.0-PROTOTYPE]](https://youtu.be/iKBfqk0ANj8 "SokubanFX v0.2.0-PROTOTYPE")

You can download the new version here: [SokubanFX-v0.2.0-PROTOTYPE_2016-05-08_18-44.zip]


Content
---

* [Stabilization from the prototype](#Stabilization)
    * [Stabilize the prototype with JUnit tests](#StabilizeJUnit)
    * [Stabilize the prototype with Refactoring](#StabilizeRefactoring)
* [New Features in SokubanFX v0.2.0-PROTOTYPE](#NewFeatures)
    * [User can now handle the application with KeyEvents](#UserKeyEvents)
    * [Implementation from the library Ikonli for icons](#LibraryIkonli)
    * [Change internal functionalities to lambda expressions](#LambdaExpressions)
* [Conclusion](#Conclusion)
* [About the autor](#Autor)
    * [Contact](#Contact)
* [Articles in this series](#Articles)



Stabilization from the prototype<a name="Stabilization" />
---

In this part I will describe the steps how to stabilize the project.


##### Stabilize the prototype with JUnit tests<a name="StabilizeJUnit" />

Creating from new [JUnit] tests with [NetBeans IDE] is really easy because the 
IDE have a nice feature which is:  
The action `Test for Existing Class` under `New` -> `Unit Tests`:
* This wizard will generate automatically a [JUnit] for an existing class.
* Select the class which should be tested.
* The wizard fill automatically the test package and name for the new test class.
* Check the options under `Method Access Levels`, `Generated Code` and `Generated 
  Comments`.
* That was it :smile: .

![wizard-new-test-for-existing-class.png][wizard-new-test-for-existing-class]


So the basic test classes and methods are really fast generated.

![test-packages.png][test-packages]

Lets have together a look on the [JUnit] tests in the class `CollisionCheckerTest`:
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
        assertNotNull("Instance from CollisionChecker must != NULL", result); // NOI18N
    }
    
    @Test
    public void checkCollisionPlayerBoxWallWithDirectionDOWN() {
        // direction
        final EDirection direction = EDirection.DOWN;
        
        // There is a box before the player (y=11) and no second box (y!=12) before the first box
        boxes.clear();
        boxes.add(Coordinates.getDefault(10,  2));
        boxes.add(Coordinates.getDefault(10, 11)); // Box before the player!
        boxes.add(Coordinates.getDefault(10, 15));
        mapModel.setBoxes(boxes);
        
        walls.clear(); // No walls!
        mapModel.setWalls(walls);
        
        ECollisionResult result = CollisionChecker.getDefault().checkCollisionPlayerBoxWall(direction, mapModel);
        assertEquals("There is a box before the player (y=11) and no second box (y!=12) before the first box -> CollisionResult.PLAYER_AGAINST__BOX_NONE", ECollisionResult.PLAYER_AGAINST__BOX_NONE, result);
        
        // There is a box before the player (y=11) and a wall at (y=12)
        boxes.clear();
        boxes.add(Coordinates.getDefault(10,  1));
        boxes.add(Coordinates.getDefault(10, 11)); // // Box before the player!
        boxes.add(Coordinates.getDefault(10, 15));
        mapModel.setBoxes(boxes);
        
        walls.clear();
        walls.add(Coordinates.getDefault(10,  2));
        walls.add(Coordinates.getDefault(10, 12)); // Wall before the Box!
        walls.add(Coordinates.getDefault(10, 14));
        mapModel.setWalls(walls);
        
        result = CollisionChecker.getDefault().checkCollisionPlayerBoxWall(direction, mapModel);
        assertEquals("There is a box before the player (y=11) and a wall at (y=12) -> CollisionResult.PLAYER_AGAINST__BOX_WALL", ECollisionResult.PLAYER_AGAINST__BOX_WALL, result);
    }
    
    ...
}
```

* First for every test the player position is set to `10,10` in the method `setUp()`.
* Then all possible collisions (player -> (box -> '', box, place, wall), wall) 
  will be tested in own methods.
* The combination player -> '' is check in the first part from every 
  `checkCollisionXY()` method.


Here are a list with all `checkCollisionXY` methods:
```java
    public void checkCollisionPlayerBoxBoxWithDirectionDOWN()
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
```

Plz have a look into the source code from the class [CollisionCheckerTest] if 
you are interest into the implementation details from these methods.


In the class `MapMovementTest` I will test if a map is finished after a user 
movement or not:
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

* First the positions from the boxes are defined.
* Then the positions from the places are defined.
* With the call from `mm.isMapFinish()` in the class `MomventResult` the engine will 
  check if all boxes are on a place.
    * If so the map is finished otherwise not.


##### Stabilize the prototype with Refactoring<a name="StabilizeRefactoring" />

One really important part for me in development from an application is `refactoring`. 
It's so important for me that I can say that my programming style is founded on this 
topic:
* See [Refactoring - Improving the Design of Existing Code] by [Martin Fowler] for 
  more information.

Also I find it helpful to have the main points from [Clean Code Developer] 
&#40;:de:&#41; in mind during the stabilization.

So what for `refactorings` can be done to stabilize the program :question:
* Delete unnecessary files.
* Start with documentation &#40;at first with the project ReadMe&#41;.
* Update the dependencies for included libraries.
* Create templates if possible &#40;for example for the realease notes&#41;.
* Check the package structure and move classes if needed.
* Check the names from classes, interfaces and enums and rename them if needed.
* Switch from [Java] classes to [JavaFX] classes when possible.
* Move functionalities from classes to new classes -> [Single Responsibility Principle (SRP)].
* Check layout in views and simplified if possible.
* ...

In general things are done when they are ready :laughing: .  
But here are 3 points which helps me to decided when to goto the next phase in 
the program development.
* The time is over which I planned for the actual phase (version).
* The top :five: `dirtiest` areas in the application are cleaned.
* Points which I haven't the time to cleanup are noted for the next release.

In general (2).  
Normally in my private projects I implement, fix following issues in one release 
&#40;so one release needs 2-3 weeks&#41;:
* 1 new feature
* and / or 1 enhancement.
* 3 - 4 bug fixes.
* 5 - 7 refactorings.



New Features in SokubanFX v0.2.0-PROTOTYPE<a name="NewFeatures" />
---

In this section I will write what is new in SokubanFx v0.2.0.


##### User can now handle the application with KeyEvents<a name="UserKeyEvents" />

In the new version 0.2.0 from [SokubanFX] the user has the possibility to 
handle the application with KeyEvents.

```java
public class StartApplication extends Application implements IActionConfiguration, IApplicationConfiguration {

    @Override
    public void start(Stage primaryStage) throws Exception {
        final ApplicationView applicationView = new ApplicationView();
        final ApplicationPresenter applicationPresenter = applicationView.getRealPresenter();
        
        final Scene scene = new Scene(applicationView.getView(), 1280, 720);
        scene.setOnKeyReleased((KeyEvent event) -> { // 1
            this.onKeyReleased(event);
        });
        ...
    }

    private void onKeyReleased(KeyEvent event) {
        // Listen to Application events
        final KeyCode keyCode = event.getCode();
        if (keyCode == KeyCode.ESCAPE) {  // 2
            event.consume();
            this.onCloseRequest();
            
            return;
        }
        
        // MainMenu
        if (keyCode == KeyCode.BACK_SPACE) { // 3
            event.consume();
            final boolean isMainMenuShown = PreferencesFacade.INSTANCE.getBoolean(
                    IMainMenuConfiguration.PROP__MAIN_MENU_IS_SHOWN,
                    IMainMenuConfiguration.PROP__MAIN_MENU_IS_SHOWN__DEFAULT_VALUE);
            ActionFacade.INSTANCE.handle(isMainMenuShown ? ON_ACTION__HIDE_MAINMENU : ON_ACTION__SHOW_MAINMENU);
            
            return;
        }
        
        // Preview
        final boolean shouldOnKeyReleaseForPreview = PreferencesFacade.INSTANCE.getBoolean(
                IPreviewConfiguration.PROP__KEY_RELEASED__FOR_PREVIEW, 
                IPreviewConfiguration.PROP__KEY_RELEASED__FOR_PREVIEW__DEFAULT_VALUE);
        if (shouldOnKeyReleaseForPreview) { // 4
            final TransferData transferData = new TransferData();
            transferData.setActionId(ON_ACTION__KEY_RELEASED__FOR_PREVIEW);
            transferData.setObject(event);

            ActionFacade.INSTANCE.handle(transferData);
        }
        
        // Game
        final boolean isGameViewInitialize = PreferencesFacade.INSTANCE.getBoolean(
                IGameConfiguration.PROP__GAMEVIEW_IS_INITIALZE, 
                IGameConfiguration.PROP__GAMEVIEW_IS_INITIALZE__DEFAULT_VALUE);
        final boolean shouldOnKeyReleaseForGameView = PreferencesFacade.INSTANCE.getBoolean(
                IGameConfiguration.PROP__KEY_RELEASED__FOR_GAMEVIEW, 
                IGameConfiguration.PROP__KEY_RELEASED__FOR_GAMEVIEW__DEFAULT_VALUE);
        if (isGameViewInitialize && shouldOnKeyReleaseForGameView) { // 5
            final TransferData transferData = new TransferData();
            transferData.setActionId(ON_ACTION__KEY_RELEASED__FOR_GAME);
            transferData.setObject(event);

            ActionFacade.INSTANCE.handle(transferData);
        }
    }

    ...
}
```

1. Adds an [EventHandler<? super KeyEvent>] to the [Scene] which catch all 
   KeyEvents from the user.
2. In all views from the application the user can close the application 
   with the key `ESCAPE`.
3. Also in all views the menu can be shown when the user press the key `BACK_SPACE`.
4. All other KeyEvents will be checked first if the `preview modus` is activ. If 
   so then the event will delegate to the preview view.
5. At last it will be checked if the `game mode` is active. If so then...

In this example I will show what happen if the action `ON_ACTION__KEY_RELEASED__FOR_GAME` 
is fired:
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {

    @Override
    public void registerActions() {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Register actions in GamePresenter"); // NOI18N
        
        this.registerOnActionDisplayMap();
        this.registerOnKeyReleased(); // 1
    }

    private void registerOnKeyReleased() {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Register on KeyReleased"); // NOI18N
        
        ActionFacade.INSTANCE.register( // 2
                ON_ACTION__KEY_RELEASED__FOR_GAME,
                (ActionEvent event) -> {
                    final TransferData transferData = (TransferData) event.getSource();
                    final KeyEvent keyEvent = (KeyEvent) transferData.getObject();
                    this.onKeyRelease(keyEvent);
                }
        );
    }
    
    /*
     * KeyEvents in GameView
     * W UP        -> move up
     * S DOWN      -> move down
     * A LEFT      -> move left
     * D RIGHT     -> move right
     * ENTER SPACE -> reset map
     * 
     * BACKSPACE   -> not needed - catched in ApplicationView (shows the menu)
     * ESC         -> not needed - catched in ApplicationView (close the application)
     */
    private void onKeyRelease(KeyEvent keyEvent) { // 3
        final KeyCode keyCode = keyEvent.getCode();
        LoggerFacade.INSTANCE.debug(this.getClass(), "On KeyRelease: " + keyCode); // NOI18N
        
        if (
                keyCode.equals(KeyCode.ENTER)
                || keyCode.equals(KeyCode.SPACE)
        ) {
            this.onActionButtonResetMap();
            return;
        }
        
        if (!listenToKeyEvents) {
            return;
        }
        
        switch(keyCode) {
            case W:
            case UP:    { this.onActionButtonUp();    break; }
            case S:
            case DOWN:  { this.onActionButtonDown();  break; }
            case A:
            case LEFT:  { this.onActionButtonLeft();  break; }
            case D:
            case RIGHT: { this.onActionButtonRight(); break; }
        }
    }

    ...

}
```

1. All possible actions from the class `GamePresenter` will be registered in the 
   method `registerActions()`.
2. Shows the registration from the action `ON_ACTION__KEY_RELEASED__FOR_GAME`.
3. If the above described action is triggered, then the KeyEvent will be evaluated 
   like the `JavaDoc` said. Only actions to move the player or reset the map will 
   be accept.


##### Implementation from the library Ikonli for icons<a name="LibraryIkonli" />

For [SokubanFX] I decided to use the icon font [Ikonli]. Although there 
are another excellent icon fonts like [FontAwesomeFX] or [ControlFX] I decided 
to give [Ikonli] a try :smile: .

[Ikonli] have a very well documented [Ikonli Guide] where momentary :two::one: 
(version 1.5.0) icon-sets are listed :exclamation:

Here is the official project description:

> Ikonli provides icon packs that can be used in Java applications.
> Currently Swing and JavaFX UI toolkits are supported.

To use the icon font in the project we need to include following dependencies in 
the `pom.xml`:
```xml
<dependencies>
    <dependency>
        <groupId>org.kordamp.ikonli</groupId>
        <artifactId>ikonli-core</artifactId> // 1
        <version>1.5.0</version>
    </dependency>
    <dependency>
        <groupId>org.kordamp.ikonli</groupId>
        <artifactId>ikonli-javafx</artifactId> // 2
        <version>1.5.0</version>
    </dependency>
    <dependency>
        <groupId>org.kordamp.ikonli</groupId>
        <artifactId>ikonli-elusive-pack</artifactId> // 3
        <version>1.5.0</version>
    </dependency>

    ...
</dependencies>
```

1. `ikonli-core` defines the `engine` from the icon font. Without this library 
   nothings will work :smile: .
2. Because [SokubanFX] is a [JavaFX 8] application we include `ikonli-javafx`.
3. First choose is the icon-set `ikonli-elusive-pack`. Maybe I will change this later 
   :question:

Here is the first example how to use the iconfont [Ikonli] in the application:
```java
public class PreviewPresenter implements Initializable, IActionConfiguration, IRegisterActions {

    private void initializeButtonPlayGame() {
        LoggerFacade.INSTANCE.info(this.getClass(), "Initialize button PlayGame"); // NOI18N
        
        lPlayGame.setText(null);
        lPlayGame.setCursor(Cursor.HAND);
        
        final FontIcon fiPlayAlt = new FontIcon(Elusive.PLAY_ALT); // 1
        fiPlayAlt.setIconSize(56);
        lPlayGame.setGraphic(fiPlayAlt); // 2
    }

    ...
}
```

1. It's really easy to get the icon.
2. In this case I will added the icon to a [Label] as graphic.

And the result will look like:

![icon-font-preview.png][icon-font-preview]


And in the next example we can see how to add some icons to the play-buttons:
```java
public class GamePresenter implements Initializable, IActionConfiguration, IRegisterActions {

    private void initializeButtons() {
        LoggerFacade.INSTANCE.info(this.getClass(), "Initialize buttons"); // NOI18N
        // 1
        this.initializeButton(bMovePlayerDown, Elusive.ARROW_DOWN, "Move player down"); // NOI18N
        this.initializeButton(bMovePlayerLeft, Elusive.ARROW_LEFT, "Move player left"); // NOI18N
        this.initializeButton(bMovePlayerRight, Elusive.ARROW_RIGHT, "Move player right"); // NOI18N
        this.initializeButton(bMovePlayerUp, Elusive.ARROW_UP, "Move player up"); // NOI18N
        
        this.initializeButton(bResetMap, Elusive.REFRESH, "Reset the map"); // NOI18N
    }
    
    private void initializeButton(Button btn, Ikon icon, String tooltip) { // 2
        final FontIcon fi = new FontIcon(icon);
        fi.setIconSize(24);
        btn.setGraphic(fi);
        btn.setText(null);
        btn.setTooltip(new Tooltip(tooltip));
    }

    ...
}
```

1. For every play-[Button] the method `initializeButton(...)` will be called.
2. In the method `initializeButton(Button, Ikon, String)` the icon and a tooltip 
   will be added to the [Button].

And the result looks like:

![icon-font-game.png][icon-font-game]


##### Change internal functionalities to lambda expressions<a name="LambdaExpressions" />

New in [Java 8] are [Lambda Expressions] which are really interesting and powerful. 

Here is a very simple example how to stream over every `item` in an [ObservableList]:
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

1. This [Lambda Expressions] streams simple over every `item` in the 
   [ObservableList]<String> mapAsStrings.
2. For every `item` in the [ObservableList] a new formated label will be added 
   to the [VBox] vbMap.

The next example will show first the `old way` how to iterate over a list, check 
something and if okay then update the iterated `item`:
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

Then after the conversion from the `for-each` iteration to the [Lambda Expressions] 
we have:
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
   the item `coordinatesFounded` will be updated.

In the last example from this section again first time the `old way` will be shown 
how to check if all `boxes` are on a `place`, that mean if so then the map is `finished`.
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



Conclusion<a name="Conclusion" />
---

`JUnit` tests, `refactoring`, `clean code` and `bug fixing` are the key points to 
stabilize an application from my view. In every release I will spend between 50% 
and 60% from the time to this topics. The rest is reserved for new features or 
enhancements.

For me this works very well and for you?

Download:  
[SokubanFX-v0.2.0-PROTOTYPE_2016-05-08_18-44.zip]

YouTube:
[![sokubanfx_v0.2.0-PROTOTYPE.png][sokubanfx_v0.2.0-PROTOTYPE]](https://youtu.be/iKBfqk0ANj8 "SokubanFX v0.2.0-PROTOTYPE")



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
[icon-font-game]:https://cloud.githubusercontent.com/assets/8161815/15988997/4835c344-3067-11e6-9f0c-41efe4f44829.png
[icon-font-preview]:https://cloud.githubusercontent.com/assets/8161815/15988994/3ee05ba6-3067-11e6-824e-f3a90fc4cd84.png
[keyevents-in-sokubanfx]:https://cloud.githubusercontent.com/assets/8161815/15549769/6c4ad966-22ae-11e6-898b-20c2ecad5309.png
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
[Button]:https://docs.oracle.com/javase/8/javafx/api/index.html?javafx/scene/control/Button.html
[Clean Code Developer]:http://clean-code-developer.de/
[CollisionCheckerTest]:https://github.com/Naoghuman/SokubanFX/blob/prototype-v0.2.0/src/test/java/com/github/naoghuman/sokubanfx/map/collision/CollisionCheckerTest.java
[ControlFX]:http://fxexperience.com/controlsfx/
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
[EventHandler<? super KeyEvent>]:https://docs.oracle.com/javase/8/javafx/api/javafx/event/EventHandler.html
[FontAwesomeFX]:https://bitbucket.org/Jerady/fontawesomefx
[Geertjan Wielenga]:https://blogs.oracle.com/geertjan/entry/welcome_to_me
[General Public License 3.0]:http://www.gnu.org/licenses/gpl-3.0.en.html
[GitHub]:https://github.com/
[H+D International Group]:https://www.hud.de/en/
[Help for Multilingual NetBeans Platform Applications]:https://dzone.com/articles/multilingual-netbeans-platform-applications
[Ikonli]:https://github.com/aalmiray/ikonli
[Ikonli Guide]:http://aalmiray.github.io/ikonli/
[Issue]:https://github.com/Naoghuman/articles/issues
[Java]:https://en.wikipedia.org/wiki/Java_%28programming_language%29
[Java 8]:https://www.java.com/en/download/faq/java8.xml
[JavaFX]:http://docs.oracle.com/javase/8/javase-clienttechnologies.htm
[JavaFX 2.0]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_2.0
[JavaFX 8]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_8
[JUnit]:http://junit.org/junit4/
[Lambda Expressions]:https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html
[Label]:https://docs.oracle.com/javase/8/javafx/api/index.html?javafx/scene/control/Label.html
[Martin Fowler]:http://martinfowler.com/
[NetBeans IDE]:https://netbeans.org/
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin
[ObservableList]:https://docs.oracle.com/javase/8/javafx/api/javafx/collections/ObservableList.html
[Optional<T>]:https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html
[Project-Template-afterburnerfx-Naoghuman]:https://github.com/Naoghuman/Project-Templates/tree/master/Project-Template-afterburnerfx-Naoghuman
[Refactoring - Improving the Design of Existing Code]:http://martinfowler.com/books/refactoring.html
[Scene]:https://docs.oracle.com/javase/8/javafx/api/javafx/scene/Scene.html
[Single Responsibility Principle (SRP)]:https://en.wikipedia.org/wiki/Single_responsibility_principle
[SokubanFX]:https://github.com/Naoghuman/SokubanFX
[SokubanFX v0.2.0-PROTOTYPE]:https://youtu.be/iKBfqk0ANj8
[SokubanFX-v0.2.0-PROTOTYPE_2016-05-08_18-44.zip]:https://github.com/Naoghuman/SokubanFX/releases/tag/v0.2.0
[Sokuban-Clone]:https://github.com/Naoghuman/sokuban-clone
[Swing2D]:https://docs.oracle.com/javase/tutorial/2d/
[VBox]:https://docs.oracle.com/javase/8/javafx/api/javafx/scene/layout/VBox.html
