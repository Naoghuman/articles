Overview Naoghuman's JavaFX projects
===



Intention
---

In this article I want to give an `overiew` about my [JavaFx] `plugins`, `libraries`, 
`games` and `applications` and how they work together.
* The `Tier 0: Extras` section contains on the one side the [NetBeansIDE-AfterburnerFX-Plugin] 
  which supports the [JavaFX] development in a [Maven] context in conjunction 
  with the library [afterburner.fx] from [Adam Bien]. On the other side also the 
  project `Incubator` where I hold on my ideas for new projects.
* The `Tier 1: Core Libraries` section contains all core libraries from me 
  which I used in all my projects depends on the concrete case.
* The `Tier 2: Extended Libraries` section contains libraries which depends 
  on one or more libraries from the section `Tier 1: Core Libraries`.
* In the last `Tier 3: Applications / Games` section I list different `applications` 
  and `games` from me where I used the libraries from the sections `Tier 1: Core Libraries` 
  and `Tier 2: Extended Libraries`.

_Image:_ Overview Naoghuman's JavaFX projects  
![overview-naoghumans-javafx-projects-v1.png][overview-naoghumans-javafx-projects-v1]

> __Hint__  
> Every entry in every `Tier` have following subsections: Description, Examples, 
> Conclusion and then the Details.  
> Exception is the `NetBeansIDE-AfterburnerFX-Plugin` where I added a subsection `Press`.



Content
---

* [Tier 0: Extras](#Ti0Pl)
    - [NetBeansIDE-AfterburnerFX-Plugin _(Stable)_](#NeBeAfPl)
    - [Incubator _(Prototype/Planed)_](#Incu)
* [Tier 1: Core Libraries](#Ti1CoLi)
    - [Lib-Logger _(Stable)_](#LiLo)
    - [Lib-Action _(Stable)_](#LiAc)
    - [Lib-Database-ObjectDB _(Stable)_](#LiDaOb)
    - [Lib-Preferences _(Stable)_](#LiPre)
    - [Lib-Properties _(Stable)_](#LiPro)
* [Tier 2: Extended Libraries](#Ti2ExLi)
    - [Lib-Tag _(Development)_](#LiTa)
    - [Lib-Tile _(Development)_](#LiTi)
    - [Lib-Emoticon _(Early Development)_](#LiEm)
    - [Lib-Testdata _(Early Development)_](#LiTe)
    - [Lib-Sampler _(Prototpye)_](#LiSa)
    - [Lib-Map _(Prototype)_](#LiMa)
* [Tier 3: Applications / Games](#Ti3ApGa)
    - [Application ABC-List _(Development)_](#ApAbLi)
    - [Application HabitFX _(Development)_](#ApHaFx)
    - [Application Competency Matrix _(Prototpye)_](#ApCoMa)
    - [Application Concentration _(Planed)_](#ApCon)
    - [Application TypeWriter _(Planed)_](#ApTyWr)
    - [Game SokubanFX _(Development)_](#GaSoFx)
    - [Game StepByStep _(Prototpye)_](#GaStBySt)
* [About the autor](#Autor)
    - [Contact](#Contact)
* [Other articles from me](#OtherArticles)



Tier 0: Extras<a name="Ti0Pl" />
---

TODO

### NetBeansIDE-AfterburnerFX-Plugin _(Stable)_<a name="NeBeAfPl" />

> __Description__  
> The `NetBeansIDE-AfterburnerFX-Plugin` is a [NetBeans IDE] plugin which supports
> the file generation in **convention** with the library [afterburner.fx] in a [JavaFX] 
> project.
> 
> The following primary files `[FileName].fxml`, `[FileName]Presenter.java`, `[FileName]View.java` 
> and optional `[FileName].css`, `[FileName].properties` and `configuration.properties` 
> can be created in a new wizard.  
> One conditional is that *[FileName].toLowerCase()* must be **equals** with the *last* choosen package name.

_Image:_ Shows the view `3. Primary Files` from the new wizard  
![plugin-3-primary-files.png][plugin-3-primary-files]


**Examples**  
The following picture shows all possible files which can be generate in one slide 
with the new wizard after installing the plugin in your [NetBeans IDE].

TODO add more info -> installation over netbeans, image show wizard

_Image:_ Shows an example from `generated` files  
![plugin-6-generated-files.png][plugin-6-generated-files]


**Press**  
* `Interview` with `Adam Bien` about me and the plugin: [Afterburner.fx NetBeans Plugin Release]
* `Adam Bien` introduced my plugin in one of his videos 
  `DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive` &#40;see at 48:00)&#41;:

_Image:_ Click on the image will open the `YouTube` video  
[![video-netBeanside-afterburnerfx-plugin.png][video-netBeanside-afterburnerfx-plugin]](https://www.youtube.com/watch?v=WsV7kSSSOGs "NetBeansIDE-AfterburnerFX-Plugin")


**Conclusion**  
With the plugin [NetBeansIDE-AfterburnerFX-Plugin] I'm able to quickly generate 
the basic files in context from a [JavaFX] and [Maven] and [afterburner.fx] project.


**Details**  

| GitHub | [NetBeansIDE-AfterburnerFX-Plugin] |
| --- | --- |
| Since | Sep 22, 2015 |
| Releases | [NetBeansIDE-AfterburnerFX-Plugin Releases] _(6 releases)_ |
| Last release | [1.5.0] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Incubator _(Prototype/Planed)_<a name="Incu" />

> __Description__  
> The project `Incubator` contains my dreams, ideas and projects which are on the 
> way to become reality or not :smile: .

_Image:_ Overview Incubator  
![incubator.png][incubator]


**Examples**  
* `Lib-Tag`, `Lib-Testdata`, `StepByStep`...


**Conclusion**  
The project `Incubator` is a good place for all ideas. Sometimes I try something 
and a day, a month or a year later I start a real project like `Lib-Tag` for example.


**Details**  
No releases are available in `Incubator`.


Tier 1: Core Libraries<a name="Ti1CoLi" />
---

TODO

### Lib-Logger _(Stable)_<a name="LiLo" />

> __Description__  
> `Lib-Logger` is a library for `easy` logging with the [Apache Log4j 2] in a 
> [JavaFX] &amp; [Maven] desktop application.

_Image:_ [UML] Lib-Logger  
![UML-diagram_Lib-Logger_v0.5.1_2017-07-19_23-44.png][UML-diagram_Lib-Logger_v0.5.1_2017-07-19_23-44]


**Examples**  
After including the library into your [Maven] project with
```java
<!-- https://mvnrepository.com/artifact/com.github.naoghuman/lib-logger -->
<dependency>
    <groupId>com.github.naoghuman</groupId>
    <artifactId>lib-logger</artifactId>
    <version>0.5.1</version>
</dependency>
```

put also the file `log4j2.xml` into the default resource package `src/main/resources` 
in your project.  
Then logging is really simple like:
```java
public static final void loadResourcesInCache() {
    LoggerFacade.getDefault().debug(TemplateLoader.class, "Load resources in cache"); // NOI18N

    ...
}

// which will print in the console and in the configured `xy.log` file:
2017-05-27 08:56:53,757  DEBUG Load resources in cache     [TemplateLoader]
```

Here is an example output from the application [ABC-List] (`/log/application.log`):
```java
2017-08-22 05:32:54,469  DEBUG Load properties: /com/github/naoghuman/abclist/i18n/application.properties     [LibProperties]
2017-08-22 05:32:54,476  DEBUG Load properties: /com/github/naoghuman/abclist/i18n/converter.properties     [LibProperties]
2017-08-22 05:32:54,477  INFO  
################################################################################
Start ABC-List v0.4.0-SNAPSHOT.
################################################################################     [LibLogger]
2017-08-22 05:32:54,478  DEBUG   Init preferences file     [LibPreferences]
2017-08-22 05:32:54,479  DEBUG Initialize ObjectDB with database: application     [LibDatabase]
2017-08-22 05:32:54,660  INFO  Initialize ApplicationPresenter     [ApplicationPresenter]
2017-08-22 05:32:54,771  INFO  Initialize [Navigation] buttons     [ApplicationPresenter]
2017-08-22 05:32:54,804  INFO  Initialize [Navigation] [TabPane]     [ApplicationPresenter]
2017-08-22 05:32:54,806  INFO  Initialize [Navigation] tab [Links]     [ApplicationPresenter]
2017-08-22 05:32:54,812  INFO  Initialize [Navigation] tab [Terms]     [ApplicationPresenter]
2017-08-22 05:32:54,814  INFO  Initialize [Navigation] tab [Topics]     [ApplicationPresenter]
2017-08-22 05:32:54,820  INFO  Initialize [WelcomeView]     [ApplicationPresenter]
2017-08-22 05:32:54,859  INFO  Initialize WelcomePresenter     [WelcomePresenter]
2017-08-22 05:32:54,860  DEBUG Register actions in [ApplicationPresenter]     [ApplicationPresenter]
2017-08-22 05:32:54,860  DEBUG Register on action open [Exercise]     [ApplicationPresenter]
2017-08-22 05:32:54,861  DEBUG Register action: ACTION__APPLICATION__OPEN_EXERCISE     [ILibAction]
2017-08-22 05:32:54,861  DEBUG Register on action open [Term]     [ApplicationPresenter]
2017-08-22 05:32:54,862  DEBUG Register action: ACTION__APPLICATION__OPEN_TERM     [ILibAction]
2017-08-22 05:32:54,862  DEBUG On action refresh [Navigation] tab [Topics]     [ApplicationPresenter]
2017-08-22 05:32:54,864  DEBUG Add CrudService: DEFAULT     [LibDatabase]
2017-08-22 05:32:55,162  DEBUG Find by named query: Topic.findAll     [CrudService]
2017-08-22 05:32:55,324  DEBUG   + Need 00:00:00.456 for [10000] entities in [findAllTopics()]     [SqlProvider]
2017-08-22 05:32:58,631  DEBUG Shutdown ObjectDB     [LibDatabase]
2017-08-22 05:32:58,631  DEBUG Shutdown EntityManager: DEFAULT     [CrudService]
2017-08-22 05:32:58,642  DEBUG Shutdown EntityManagerFactory     [LibDatabase]
2017-08-22 05:32:58,691  INFO  
################################################################################
Stop ABC-List v0.4.0-SNAPSHOT.
################################################################################     [LibLogger]
```


**Conclusion**  
With the library `Lib-Logger` it's really easy to integrate the feature `logging` 
into your `library`, `game` and / or `application`.  


**Details**  

| GitHub | [Lib-Logger] |
| --- | --- |
| Since | Jul 13, 2014 |
| Releases | [Lib-Logger Releases] _(13 releases)_ |
| Last release | [Lib-Logger v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Action _(Stable)_<a name="LiAc" />

> __Description__  
> `Lib-Action` is a library for `easy` storing and accessing actions 
> ([EventHandler]&lt;[ActionEvent]&gt;) in a [JavaFX] &amp; [Maven] desktop 
> application.

_Image:_ [UML] Lib-Action  
![UML-diagram_Lib-Action_v0.5.1_2017-07-22_23-42.png][UML-diagram_Lib-Action_v0.5.1_2017-07-22_23-42]


**Examples**  
After including the library into your [Maven] project with
```java
<!-- https://mvnrepository.com/artifact/com.github.naoghuman/lib-action -->
<dependency>
    <groupId>com.github.naoghuman</groupId>
    <artifactId>lib-action</artifactId>
    <version>0.5.1</version>
</dependency>
```

see following example how to `register` an `action`:
```java
public class ApplicationPresenter implements RegisterActions ... {
    @Override
    public void initialize(URL location, ResourceBundle resources) {
        // This method will be executed during the initialization from the class 
        // ApplicationPresenter. So all methods in this method will be registered 
        // during the initialization.
        this.register();
        ...
    }
    ...
    @Override
    public void register() {
        LoggerFacade.getDefault().debug(this.getClass(), "Register actions in [ApplicationPresenter]"); // NOI18N
        
        this.registerOnActionOpenTerm();
        ...
    }
    ...
    private void registerOnActionOpenTerm() {
        LoggerFacade.getDefault().debug(this.getClass(), "Register on action open [Term]"); // NOI18N
        
        ActionHandlerFacade.getDefault().register(
                ACTION__APPLICATION__OPEN_TERM,
                (ActionEvent event) -> {
                    final TransferData transferData = (TransferData) event.getSource();
                    final Optional<Long> entityId = transferData.getLong();
                    if (entityId.isPresent()) {
                        this.onActionOpenTermWithId(entityId);
                    }
                });
    }
}
```

The above registered action can be easly `executed` with following statement:
```java
private Label getLabel(Term term) {
    final Label label = new Label(term.getTitle());
    label.setOnMouseClicked(event -> {
            if (event.getClickCount() == 2) {
                final TransferData transferData = new TransferData();
                transferData.setActionId(ACTION__APPLICATION__OPEN_TERM);
                transferData.setObject(term);
                
                ActionFacade.getDefault().handle(transferData);
            }
        });
}
```


**Conclusion**  
With the library `Lib-Action` it's really easy to register actions 
([EventHandler]&lt;[ActionEvent]&gt;) in your `library`, `game` and / or 
`application`.


**Details**  

| GitHub | [Lib-Action] |
| --- | --- |
| Since | Jul 26, 2014 |
| Releases | [Lib-Action Releases] _(15 releases)_ |
| Last release | [Lib-Action v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Database-ObjectDB _(Stable)_<a name="LiDaOb" />

> __Description__  
> `Lib-Database-ObjectDB` is a library for easy accessing an [ObjectDB] database 
> in a [JavaFX] &amp; [Maven] desktop application.

_Image:_ [UML] Lib-Database-ObjectDB  
![UML-diagram_Lib-Database-ObjectDB_v0.5.1_2017-07-30_15-34.png][UML-diagram_Lib-Database-ObjectDB_v0.5.1_2017-07-30_15-34]


**Examples**  
Including the library into a [Maven] project can done with:
```java
<!-- https://mvnrepository.com/artifact/com.github.naoghuman/lib-database-objectdb -->
<dependency>
    <groupId>com.github.naoghuman</groupId>
    <artifactId>lib-database-objectdb</artifactId>
    <version>0.5.1</version>
</dependency>
```

How to `register` an database:
```java
public class StartApplication extends Application {
    ...
    @Override
    public void init() throws Exception {
        // Register the resource-bundle
        PropertiesFacade.getDefault().register(KEY__APPLICATION__RESOURCE_BUNDLE);
        ...
        // Register the database
        DatabaseFacade.getDefault().register(Properties.getPropertyForApplication(KEY__APPLICATION__DATABASE));
    }
}

public interface IPropertiesConfiguration {
    public static final String KEY__APPLICATION__RESOURCE_BUNDLE = "/com/github/naoghuman/abclist/i18n/application.properties"; // NOI18N
    public static final String KEY__TESTDATA_APPLICATION__DATABASE = "application.database"; // NOI18N
    ...
}
```

How to create and update an `Exercise`:
```java
public class SqlProvider ... {
    public void createExercise(final Exercise exercise) {
        final StopWatch stopWatch = new StopWatch();
        stopWatch.start();
                
        ExerciseSqlService.getDefault().create(exercise);
        
        stopWatch.split();
        this.printToLog(stopWatch.toSplitString(), 1, "createExercise(Exercise)"); // NOI18N
        stopWatch.stop();
    }
    ...
    public void updateExercise(final Exercise exercise) {
        final StopWatch stopWatch = new StopWatch();
        stopWatch.start();
        
        ExerciseSqlService.getDefault().update(exercise);
        
        stopWatch.split();
        this.printToLog(stopWatch.toSplitString(), 1, "updateExercise(Exercise)"); // NOI18N
        stopWatch.stop();
    }
}

final class ExerciseSqlService ... {
    void create(Exercise exercise) {
        if (Objects.equals(exercise.getId(), DEFAULT_ID)) {
            exercise.setId(System.currentTimeMillis());
            DatabaseFacade.getDefault().getCrudService().create(exercise);
        }
        else {
            this.update(exercise);
        }
    }
    ...
    void update(Exercise exercise) {
        DatabaseFacade.getDefault().getCrudService().update(exercise);
    }
}
```


**Conclusion**  
With the library `Lib-Database-ObjectDB` it's really easy to register an database 
and perform `CRUD` operations with an entity.


**Details**  

| GitHub | [Lib-Database-ObjectDB] |
| --- | --- |
| Since | Nov 25, 2014 |
| Releases | [Lib-Database-ObjectDB Releases] _(11 releases)_ |
| Last release | [Lib-Database-ObjectDB v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Preferences _(Stable)_<a name="LiPre" />

> __Description__  
> `Lib-Preferences` is a library for `easy` storing simple data to a 
> Preferences.[properties] file in a [JavaFX] &amp; [Maven] desktop application.

_Image:_ [UML] Preferences  
![UML-diagram_Lib-Preferences_v0.5.1_2017-08-02_22-04.png][UML-diagram_Lib-Preferences_v0.5.1_2017-08-02_22-04]


**Examples**  
Including the library into a [Maven] project can done with:
```java
<!-- https://mvnrepository.com/artifact/com.github.naoghuman/lib-preferences -->
<dependency>
    <groupId>com.github.naoghuman</groupId>
    <artifactId>lib-preferences</artifactId>
    <version>0.5.1</version>
</dependency>
```

```java
/**
 * Putting a {@code value} in the file {@code Preferences.properties} in 
 * {@code ApplicationContext} will write in this case following statement in 
 * the file:<br>
 * {@code com.github.naoghuman.lib.preferences.internal.my.string.key2=y}
 * <p>
 * Searching / writing in {@code ApplicationContext} means in this case that 
 * the engine search / write a {@code key=my.string.key2} with a prefix 
 * {@code com.github.naoghuman.lib.preferences.internal}. So the complete {@code key}
 * for the search / to write is {@code com.github.naoghuman.lib.preferences.internal.my.string.key2}.
 * <p>
 * Because the search engine find the {@code key} in the file not the {@code default} 
 * value {@code x} will be returned instead the stored value {@code y} will used.
 */
@Test
public void putStringInApplicationContext() {
    PreferencesFacade.getDefault().put("my.string.key2", "y");

    final String storedValue = PreferencesFacade.getDefault().get("my.string.key2", "x");
    assertEquals("y", storedValue);
}
```

```java
/**
 * Putting a {@code value} in the file {@code Preferences.properties} in 
 * {@code ApplicationContext} will write in this case following statement in 
 * the file:<br>
 * {@code com.github.naoghuman.lib.preferences.internal.my.string.key2=y}
 * <p>
 * Searching / writing in {@code ApplicationContext} means in this case that 
 * the engine search / write a {@code key=my.string.key2} with a prefix 
 * {@code com.github.naoghuman.lib.preferences.internal}. So the complete {@code key}
 * for the search / to write is {@code com.github.naoghuman.lib.preferences.internal.my.string.key2}.
 * <p>
 * Because the search engine find the {@code key} in the file not the {@code default} 
 * value {@code x} will be returned instead the stored value {@code y} will used.
 */
@Test
public void putStringInApplicationContext() {
    PreferencesFacade.getDefault().put("my.string.key2", "y");
        
    final String storedValue = PreferencesFacade.getDefault().get("my.string.key2", "x");
    assertEquals("y", storedValue);
}
```


**Conclusion**  
With the library `Preferences` it's really easy to write and read `simple data` in a 
`Preferences.properties` file.


**Details**  

| GitHub | [Lib-Preferences] |
| --- | --- |
| Since | Jul 16, 2014 |
| Releases | [Lib-Preferences Releases] _(11 releases)_ |
| Last release | [Lib-Preferences v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Properties _(Stable)_<a name="LiPro" />

> __Description__  
> `Lib-Properties` is a library for `easy` loading [properties] files in a [JavaFX] 
> &amp; [Maven] desktop application.

_Image:_ [UML] Lib-Properties  
![UML-diagram_Lib-Properties_v0.5.0_2017-07-17_21-17.png][UML-diagram_Lib-Properties_v0.5.0_2017-07-17_21-17]


**Examples**  
Including the library into a [Maven] project can be done with:
```java
<!-- https://mvnrepository.com/artifact/com.github.naoghuman/lib-properties -->
<dependency>
    <groupId>com.github.naoghuman</groupId>
    <artifactId>lib-properties</artifactId>
    <version>0.5.0</version>
</dependency>
```

How to `register` a resource bundle:
```java
public interface IApplicationConfiguration {
    ...
    public static final String DBW__RESOURCE_BUNDLE = "/de/pro/dbw/application/DreamBetterWorlds.properties"; // NOI18N
}

public class DreamBetterWorlds extends Application implements IApplicationConfiguration, IPreferencesConfiguration {
    @Override
    public void init() throws Exception {
        PropertiesFacade.getDefault().register(DBW__RESOURCE_BUNDLE);
        ...
    }

    ...
}
```

How to `access` a value from the resource bundle:
```java

public class DreamBetterWorlds extends Application implements IApplicationConfiguration, IPreferencesConfiguration {
    private static final String KEY__APPLICATION__TITLE = "application.title"; // NOI18N
    ...

    @Override
    public void start(Stage stage) throws Exception {
        stage.setTitle(this.getProperty(KEY__APPLICATION__TITLE));
        ...
    }

    private String getProperty(String propertyKey) {
        return PropertiesFacade.getDefault().getProperty(DBW__RESOURCE_BUNDLE, propertyKey);
    }
    ...
}
```


**Conclusion**  
With the library `Lib-Properties` it's really easy to register an `properties` file 
and access values from it.


**Details**  

| GitHub | [Lib-Properties] |
| --- | --- |
| Since | Jul 18, 2014 |
| Releases | [Lib-Properties Releases] _(12 releases)_ |
| Last release | [Lib-Properties v0.5.0] _(Stable)_ |
| Licence | [General Public License 3.0] |



Tier 2: Extended Libraries<a name="Ti2ExLi" />
---

TODO








### Lib-Tag _(Development)_<a name="LiTa" />

> __Description__  
> `Lib-Tag` is a library to use and handle easily [Tag]s in your a [JavaFX] &amp; 
> [Maven] application.  
> A `Tag` is basically a simple [String] which can be used for example in a [Button], 
> [Label] or another [JavaFX] components. Suchlike tagged topics can be easily searched 
> or analysed for a `Tag`.

  
**Examples**  

Written in [JavaFX] and [NetBeans IDE] the project contains several sub-libraries 
for specific tasks. Momentary with `0.2.0` following sub-libraries are available:
* The sub-library `Lib-Tag-Core` contains the core functionalities from the project.
* The sub-library `Lib-Tag-Components` allowed to show [Tag]s in different [JavaFX] 
  gui components.

_[Lib-Tag-Core]_  
The sub-library `Lib-Tag-Core` contains the core functionalities to perform the 
CRUD (`Create`, `Read`, `Update` and `Delete`) operations for a [Tag].

_Image:_ [UML] Lib-Tag-Core  
![overview_lib-tag-core_2017-05-25_19-23.png][overview_lib-tag-core_2017-05-25_19-23]

Example how to use the fluent builder [TagBuilder] to create a [Tag]:
```java
/**
 * With the fluent builder {@code TagBuilder} its possible to create a 
 * {@code Tag}.
 * <ul>
 * <li>The first two attributes {@code id} and {@code title} are mandory.</li>
 * <li>The other attributes are {@code optional}.</li>
 * <li>All defined values will be validate against the {@code Interface}
 * {@code Validator}.</li>
 * </ul>
 */
final Tag tag = TagBuilder.create()
        .id(Tag.DEFAULT_ID)               // mandory (NOT NULL)
        .title("title")                   // mandory (NOT NULL && NOT EMPTY)
        .generationTime(Long.MIN_VALUE)   // optional
        .description("description")       // optional
        .style("style")                   // optional
        .build();
```

_[Lib-Tag-Components]_  
The sub-library `Lib-Tag-Components` contains different possibilities to show a 
[Tag] in different [JavaFX] gui components.
* Currently a `Tag` can be represented as a [Button] or a [Label].
* A list of `Tag`s can be shown in the container [FlowPane].

_Image:_ [UML] Lib-Tag-Components  
![UML-diagram_Lib-Tag-Components_v0.2.0_2017-07-22_18-07.png][UML-diagram_Lib-Tag-Components_v0.2.0_2017-07-22_18-07]

Class [TagComponentsFacade]:
```java
/**
 * Over the {@code Class} {@link com.github.naoghuman.lib.tag.components.core.TagComponentsFacade} 
 * the developer have access to several possibilities to show a {@link  com.github.naoghuman.lib.tag.core.Tag} 
 * in different {@code JavaFX} gui components.<br>
 * Momentary following possibilities exists:
 * <p>
 * Show a {@code Tag} as a
 * <ul>
 * <li>JavaFX {@link javafx.scene.control.Button}.</li>
 * <li>JavaFX {@link javafx.scene.control.Label}.</li>
 * </ul>
 * Show a {@link java.util.List} of {@code Tag}s in a
 * <ul>
 * <li>JavaFX {@link javafx.scene.layout.FlowPane}.</li>
 * </ul>
 * 
 * @author Naoghuman
 * @since  0.2.0
 * @see    com.github.naoghuman.lib.tag.components.core.TagButton
 * @see    com.github.naoghuman.lib.tag.components.core.TagFlowPane
 * @see    com.github.naoghuman.lib.tag.components.core.TagLabel
 */
public final class TagComponentsFacade implements TagButton, TagFlowPane, TagLabel
```


**Conclusion**  
With the libraries from `Lib-Tag` it's easy for the developer to integrate the 
feature [Tag] in their `applications`.


**Details**  

| GitHub | [Lib-Tag] |
| --- | --- |
| Since | Mar 09, 2017 |
| Releases | [Lib-Tag Releases] _(2 releases)_ |
| Last release | [Lib-Tag v0.2.0] _(Development)_ |
| Licence | [General Public License 3.0] | 










### Lib-Tile _(Development)_<a name="LiTi" />

> __Description__  
> `Lib-Tile` is a multi [Maven] project written in [JavaFX] and [NetBeans IDE] 
> and provides the functionalities to use and handle easily [Tile]s in your [JavaFX] 
> application.  
> A [Tile] is per definition a little transparent [Image] which overlay a 
> background-color or -image with the help of repetitions from the image in a layer.


**Examples**  

_Image:_ Crimson Night &#040;Dark / Landscape&#041; with different tile images
![different-tile-images_v0.3.0.png][different-tile-images_v0.3.0]

> __Hint__  
> Normally only one [Tile] can shown simultaneously. For demonstration purpose 
> I have merge different [Tile]s in one picture.

Like in the subsection `Description` mentioned is `Lib-Tile` a multi [Maven] project. 
Currently following submodules are available:  

_[Lib-Tile-Core]_  
The library `Lib-Tile-Core` provides the API to load a [Tile] (which is per definition 
a little transparent Image) as a [Background] or an [Image] with a concrete implementation 
from a [TileLoader].  

The main point to access the functionalities from this `API` is the class 
[TileProvider]. For example with the method `TileProvider#loadAsBackground(TileLoader, Tile)` 
the developer can load a [Tile] as a [Background].

Class [TileProvider]:
```java
/**
 * The singleton {@code TileProvider} allowed the developer access to all relevant 
 * methods in context from the {@code API} from the library {@code Lib-Tile-Core}.
 * <p>
 * For example with the methods {@code getDefaultTile(XY)} a concrete instance from 
 * the {@code Inteface} {@link com.github.naoghuman.lib.tile.core.Tile} can be created.
 * <br>
 * With the method {@code getDefaultValidator()} the developer have access to a 
 * default implementation from the {@code Inteface} 
 * {@link com.github.naoghuman.lib.tile.core.TileValidator}.
 *
 * @author Naoghuman
 * @since  0.2.0
 * @see    com.github.naoghuman.lib.tile.core.Tile
 * @see    com.github.naoghuman.lib.tile.core.TileValidator
 */
public final class TileProvider
```

_[Lib-Tile-TransparentTextures]_  
With the library `Lib-Tile-TransparentTextures` the developer have access to the 
tileset `Transparent Textures` from the internet page https://www.transparenttextures.com/ 
through the enum `TransparentTexturesTile`. Momentary that are `396` [Tile]s.

The tile images from this tileset are outsourced in a own library 
[Lib-Tile-TransparentTextures-Images] to reduce the size from this library. One 
more advance is that you can use an `own` [TileLoader] in combination with the 
library `Lib-Tile-TransparentTextures`. So you don't need to include the hole 
library (with all 396 images) [Lib-Tile-TransparentTextures-Images] into your 
project which size is momenatry `13MB`.

Class [TransparentTexturesTile]:
```java
/**
 * The class {@code TransparentTexturesTileSet} is a collection from 
 * {@link com.github.naoghuman.lib.tile.core.Tile}s which representated the 
 * {@code Tileset} from the internet page <a href="https://www.transparenttextures.com/">https://www.transparenttextures.com/</a>.
 * <p>
 * The individual {@link com.github.naoghuman.lib.tile.core.Tile} can be loaded 
 * with the class {@link com.github.naoghuman.lib.tile.core.TileProvider}.
 * <br>
 * See there the methods
 * <ul>
 * <li>{@link com.github.naoghuman.lib.tile.core.TileProvider#loadAsBackground(com.github.naoghuman.lib.tile.core.TileLoader, com.github.naoghuman.lib.tile.core.Tile)}</li>
 * <li>{@link com.github.naoghuman.lib.tile.core.TileProvider#loadAsImage(com.github.naoghuman.lib.tile.core.TileLoader, com.github.naoghuman.lib.tile.core.Tile)}</li>
 * </ul>
 * 
 * @author Naoghuman
 * @since 0.2.0
 * @see com.github.naoghuman.lib.tile.core.Tile
 * @see com.github.naoghuman.lib.tile.core.TileLoader
 * @see com.github.naoghuman.lib.tile.core.TileProvider
 */
public final class TransparentTexturesTileSet extends TileSet {
    
    private static final String SCOPE = TransparentTexturesTileLoader.getDefault().getScope();

    /**
     * The <code>Java</code> representation from the tile: 3Px Tile
     */
    public static final Tile TT_3PX_TILE = TileProvider.getDefault().getDefaultTile(SCOPE, "tt-3px-tile.png", "3Px Tile", 100, 100, "Gre3g", "http://gre3g.livejournal.com/"); // NOI18N
    
    /**
     * The <code>Java</code> representation from the tile: 45 Degree Fabric (Dark)
     */
    public static final Tile TT_45_DEGREE_FABRIC_DARK = TileProvider.getDefault().getDefaultTile(SCOPE, "tt-45-degree-fabric-dark.png", "45 Degree Fabric (Dark)", 315, 315, "Atle Mo", "http://atle.co/"); // NOI18N
    
    ...
}
```

_[Lib-Tile-TransparentTextures-Images]_  
The library `Lib-Tile-TransparentTextures-Images` contains all 396 images from 
the tileset `Transparent Textures`.
* All images from this library are wrapped in [Tile]s in the class [TransparentTexturesTileSet] 
  which is is located in the library [Lib-Tile-TransparentTextures].
* The images can be loaded over the class [TileProvider] from the library [Lib-Tile-Core] 
  as an [Background] or [Image].
* With the separation from the implementation ([Tile]s) in the library [Lib-Tile-TransparentTextures] 
  and the images in [Lib-Tile-TransparentTextures-Images] the developer can create 
  `reduced` and / or `mixed` [TileSet]s. See the examples in the library [Lib-Tile-Customized-Examples]
  for more information.

Class [TransparentTexturesTileLoader]:
```java
/**
 * The class {@code TransparentTexturesTileLoader} allowed to load a
 * {@link com.github.naoghuman.lib.tile.core.Tile} with the help from the class
 * {@link com.github.naoghuman.lib.tile.core.TileProvider}.
 * <p>
 * A {@code TileLoader} supports a {@code Tile} if gollowing conditions are true:
 * <ul>
 * <li>If the {@code scope} from both ({@code Tile} and {@code TileLoader}) are equals.</li>
 * <li>If this {@code TileLoader} supports the {@code prefix} from the {@code Tile}.</li>
 * </ul>
 * 
 * @author Naoghuman
 * @since 0.2.0
 * @see com.github.naoghuman.lib.tile.core.Tile
 * @see com.github.naoghuman.lib.tile.core.TileLoader
 * @see com.github.naoghuman.lib.tile.core.TileProvider
 */
public final class TransparentTexturesTileLoader extends TileLoader
```

_[Lib-Tile-Customized-Examples]_  
The library `Lib-Tile-Customized-Examples` provides different examples about 
`CustomizedTileSets`. There will be following demonstrations:
* An example which shows how to implemente a `reduced` [TileSet]. A reduced TileSet 
  contains different predefined `Tiles` from an existing `TileSet` which is in this
  example `TransparentTextures`.
* The next example _(will be implemented in the future)_ shows an `mixed` TileSet. 
  A mixed TileSet contains predefined and own Tiles.
* The last example _(will be implemented in the future)_ shows an `own` TileSet. 
  Like `own` means this example contains only own Tiles.

Class [CustomizedExampleReducedTileSet]:
```java
/**
 * TODO
 * 
 * @author Naoghuman
 * @since  0.2.0
 */
public final class CustomizedExampleReducedTileSet extends TileSet
```


**Conclusion**  
With the libraries around `Lib-Tile` it's for the developer easily possible to load 
and managed `Tiles` in their applications, games.


**Details**  

| GitHub | [Lib-Tile] |
| --- | --- |
| Since | Aug 02, 2016 |
| Releases | [Lib-Tile Releases] _(2 releases)_ |
| Last release | [Lib-Tile v0.2.0] _(Development)_ |
| Licence | [General Public License 3.0] |


### Lib-Emoticon _(Early Development)_<a name="LiEm" />

> __Description__  
> `Lib-Emoticon` is a multi [Maven] project written in [JavaFX] and [NetBeans IDE] 
> and provides the functionalities to use and handle easily [Emoticon]s as [Image]s 
> in your JavaFX application.

_Image:_ Demo application v0.1.0-SNAPSHOT  
![demo-application-v0.1.0-SNAPSHOT.png][demo-application-v0.1.0-SNAPSHOT]


**Examples**  

Written in [JavaFX] and [NetBeans IDE] the project contains several sublibraries 
for specific tasks. Momentary with the version `0.1.0-SNAPSHOT` following submodules 
are available:
* The sublibrary `Lib-Emoticon-Core` contains the core functionalities from the 
  project to load an [Emoticon] as an [Image].
* The sublibrary `Lib-Emoticon-Emoji` allowed the developer to have access to the 
  emoticonset [Emoji cheat sheet] through the class [EmojiEmoticonSet].
* The sublibrary `Lib-Emoticon-Emoji-Images` contains the [Image]s from the 
  emoticonset  [Emoji cheat sheet]. Currently that are `882` images.
* The sublibrary `Lib-Emoticon-Demo` contains a little [JavaFX] application which 
  demonstrate the functionalities from the previvous mentioned sublibraries.

_[Lib-Emoticon-Core]_  

The sublibrary `Lib-Emoticon-Core` provides the API to load an [Emoticon] as 
an [Image] with a concrete implementation from an [EmoticonLoader].

_[Lib-Emoticon-Emoji]_  

With the sublibrary `Lib-Emoticon-Emoji` the developer have access to the 
emoticonset [Emoji cheat sheet] through the class [EmojiEmoticonSet]. Momentary 
that are `882` [Emoticon]s.

_[Lib-Emoticon-Emoji-Images]_  

The sublibrary `Lib-Emoticon-Emoji-Images` contains all images from the 
emoticonset [Emoji cheat sheet]. Currently that are `882` images.

_[Lib-Emoticon-Demo]_  

The library 'Lib-Emoticon-Demo' contains a little [JavaFX] application which 
demonstrate the functionalities from the previvous mentioned sublibraries.


**Conclusion**  
With the libraries around `Lib-Emoticon` it's for the developer easily to load 
and managed `Emoticons` in their applications, games.


**Details**  

> __Hint__  
> This project is in early development and no releases are available.

| GitHub | [Lib-Emoticon] |
| --- | --- |
| Since | Feb 16, 2017 |
| Releases | [Lib-Emoticon Releases] _(0 releases)_ |
| Last release | -------- |
| Licence | [General Public License 3.0] |


### Lib-Testdata _(Early Development)_<a name="LiTe" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  


### Lib-Sampler _(Prototpye)_<a name="LiSa" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  


### Lib-Map _(Prototype)_<a name="LiMa" />


Tier 3: Applications / Games<a name="Ti3ApGa" />
---

TODO

### Application ABC-List _(Development)_<a name="ApAbLi" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  


### Application HabitFX _(Development)_<a name="ApHaFx" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  


### Application Competency Matrix _(Prototpye)_<a name="ApCoMa" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  


### Application Concentration _(Planed)_<a name="ApCon" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  


### Application TypeWriter _(Planed)_<a name="ApTyWr" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  


### Game SokubanFX _(Development)_<a name="GaSoFx" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  


### Game StepByStep _(Prototpye)_<a name="GaStBySt" />

> __Description__  

**Examples**  

**Conclusion**  

**Details**  



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



Other articles from me<a name="OtherArticles" />
---

TODO



[//]: # (Images)
[demo-application-v0.1.0-SNAPSHOT]:https://cloud.githubusercontent.com/assets/8161815/23338535/c417558c-fc0d-11e6-9338-8622dfcc74d7.png
[different-tile-images_v0.3.0]:https://user-images.githubusercontent.com/8161815/29042867-12cc8c62-7bb9-11e7-8780-c6c3e68a2374.png
[incubator]:https://user-images.githubusercontent.com/8161815/29682630-f7ecc2bc-890b-11e7-99ba-4f7d31711513.png
[overview_lib-tag-core_2017-05-25_19-23]:https://cloud.githubusercontent.com/assets/8161815/26462105/c35caf22-417f-11e7-9831-fd6fadda85cb.png
[plugin-3-primary-files]:https://cloud.githubusercontent.com/assets/8161815/23524833/a4122dca-ff8c-11e6-8200-77395646fbb0.png
[plugin-6-generated-files]:https://cloud.githubusercontent.com/assets/8161815/23524879/c901106a-ff8c-11e6-97b1-31ba03b7b679.png
[UML-diagram_Lib-Action_v0.5.1_2017-07-22_23-42]:https://user-images.githubusercontent.com/8161815/28494737-a28b46f6-6f37-11e7-8c66-01083545c092.png
[UML-diagram_Lib-Database-ObjectDB_v0.5.1_2017-07-30_15-34]:https://user-images.githubusercontent.com/8161815/28753983-b1feefba-753c-11e7-9233-3a4a16f9a1ad.png
[UML-diagram_Lib-Logger_v0.5.1_2017-07-19_23-44]:https://user-images.githubusercontent.com/8161815/28390956-64b5d38a-6cdc-11e7-84b7-153ace99fc3e.png
[UML-diagram_Lib-Preferences_v0.5.1_2017-08-02_22-04]:https://user-images.githubusercontent.com/8161815/28892584-c3b4afd0-77ce-11e7-8d52-65c4cc491c88.png
[UML-diagram_Lib-Properties_v0.5.0_2017-07-17_21-17]:https://user-images.githubusercontent.com/8161815/28286098-5c85b802-6b37-11e7-8db0-47eed1156c43.png
[UML-diagram_Lib-Tag-Components_v0.2.0_2017-07-22_18-07]:https://user-images.githubusercontent.com/8161815/28492739-f0c22878-6f08-11e7-9b92-3d95f33990cb.png
[video-netBeanside-afterburnerfx-plugin]:https://cloud.githubusercontent.com/assets/8161815/15169398/3b51c3de-173b-11e6-8a8f-39cc6b826260.png



[//]: # (Links)
[1.5.0]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin/releases/tag/v1.5.0
[ActionEvent]:http://docs.oracle.com/javase/8/javafx/api/javafx/event/ActionEvent.html
[Adam Bien]:http://www.adam-bien.com/roller/abien/
[Afterburner.fx NetBeans Plugin Release]:http://www.adam-bien.com/roller/abien/entry/afterburner_fx_netbeans_plugin_release
[afterburner.fx]:https://github.com/AdamBien/afterburner.fx
[Apache Log4j 2]:https://logging.apache.org/log4j/2.0/index.html
[Background]:https://docs.oracle.com/javase/8/javafx/api/javafx/scene/layout/Background.html
[Button]:https://docs.oracle.com/javase/8/javafx/api/javafx/scene/control/Button.html
[CustomizedExampleReducedTileSet]:https://github.com/Naoghuman/lib-tile/blob/master/Lib-Tile-Customized-Examples/src/main/java/com/github/naoghuman/lib/tile/customized/examples/reducedtileset/CustomizedExampleReducedTileSet.java
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
[Emoji cheat sheet]:http://www.webpagefx.com/tools/emoji-cheat-sheet/
[EmojiEmoticonSet]:https://github.com/Naoghuman/lib-emoticon/blob/master/Lib-Emoticon-Emoji/src/main/java/com/github/naoghuman/lib/emoticon/emoji/EmojiEmoticonSet.java
[Emoticon]:https://en.wikipedia.org/wiki/List_of_emoticons
[EmoticonLoader]:https://github.com/Naoghuman/lib-emoticon/blob/master/Lib-Emoticon-Core/src/main/java/com/github/naoghuman/lib/emoticon/core/EmoticonLoader.java
[EmoticonSet]:https://github.com/Naoghuman/lib-emoticon/blob/master/Lib-Emoticon-Core/src/main/java/com/github/naoghuman/lib/emoticon/core/EmoticonSet.java
[EventHandler]:http://docs.oracle.com/javase/8/javafx/api/javafx/event/EventHandler.html
[FlowPane]:https://docs.oracle.com/javase/8/javafx/api/javafx/scene/layout/FlowPane.html
[Geertjan Wielenga]:https://blogs.oracle.com/geertjan/entry/welcome_to_me
[General Public License 3.0]:http://www.gnu.org/licenses/gpl-3.0.en.html
[GitHub]:https://github.com/
[H+D International Group]:https://www.hud.de/en/
[Help for Multilingual NetBeans Platform Applications]:https://dzone.com/articles/multilingual-netbeans-platform-applications
[Image]:https://docs.oracle.com/javase/8/javafx/api/javafx/scene/image/Image.html
[Issue]:https://github.com/Naoghuman/articles/issues
[Java]:https://en.wikipedia.org/wiki/Java_%28programming_language%29
[JavaFX]:http://docs.oracle.com/javase/8/javase-clienttechnologies.htm
[JavaFX 2.0]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_2.0
[JavaFX 8]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_8
[Label]:https://docs.oracle.com/javase/8/javafx/api/javafx/scene/control/Label.html
[Lib-Action]:https://github.com/Naoghuman/lib-action
[Lib-Action Releases]:https://github.com/Naoghuman/lib-action/releases
[Lib-Action v0.5.1]:https://github.com/Naoghuman/lib-action/releases/tag/v0.5.1
[Lib-Database-ObjectDB]:https://github.com/Naoghuman/lib-database-objectdb
[Lib-Database-ObjectDB Releases]:https://github.com/Naoghuman/lib-database-objectdb/releases
[Lib-Database-ObjectDB v0.5.1]:https://github.com/Naoghuman/lib-database-objectdb/releases/tag/v0.5.1
[Lib-Emoticon]:https://github.com/Naoghuman/lib-emoticon
[Lib-Emoticon-Core]:https://github.com/Naoghuman/lib-emoticon/tree/master/Lib-Emoticon-Core
[Lib-Emoticon-Demo]:https://github.com/Naoghuman/lib-emoticon/tree/master/Lib-Emoticon-Demo
[Lib-Emoticon-Emoji]:https://github.com/Naoghuman/lib-emoticon/tree/master/Lib-Emoticon-Emoji
[Lib-Emoticon-Emoji-Images]:https://github.com/Naoghuman/lib-emoticon/tree/master/Lib-Emoticon-Emoji-Images
[Lib-Emoticon Releases]:https://github.com/Naoghuman/lib-emoticon/releases
[Lib-Logger]:https://github.com/Naoghuman/lib-logger
[Lib-Logger Releases]:https://github.com/Naoghuman/lib-logger/releases
[Lib-Logger v0.5.1]:https://github.com/Naoghuman/lib-logger/releases/tag/v0.5.1
[Lib-Preferences]:https://github.com/Naoghuman/lib-preferences
[Lib-Preferences Releases]:https://github.com/Naoghuman/lib-preferences/releases
[Lib-Preferences v0.5.1]:https://github.com/Naoghuman/lib-preferences/releases/tag/v0.5.1
[Lib-Properties]:https://github.com/Naoghuman/lib-properties
[Lib-Properties Releases]:https://github.com/Naoghuman/lib-properties/releases
[Lib-Properties v0.5.0]:https://github.com/Naoghuman/lib-properties/releases/tag/v0.5.0
[Lib-Tag]:https://github.com/Naoghuman/lib-tag/tree/master/lib-tag
[Lib-Tag-Core]:https://github.com/Naoghuman/lib-tag/tree/master/lib-tag-core
[Lib-Tag-Components]:https://github.com/Naoghuman/lib-tag/tree/master/lib-tag-components
[Lib-Tag Releases]:https://github.com/Naoghuman/lib-tag/tree/master/lib-tag/releases
[Lib-Tag v0.2.0]:https://github.com/Naoghuman/lib-tag/tree/master/lib-tag/releases/v0.2.0
[Lib-Tile]:https://github.com/Naoghuman/lib-tile
[Lib-Tile Releases]:https://github.com/Naoghuman/lib-tile/releases
[Lib-Tile v0.2.0]:https://github.com/Naoghuman/lib-tile/releases/tag/v0.2.0
[Lib-Tile-Core]:https://github.com/Naoghuman/lib-tile/tree/master/Lib-Tile-Core
[Lib-Tile-Customized-Examples]:https://github.com/Naoghuman/lib-tile/tree/master/Lib-Tile-Customized-Examples
[Lib-Tile-TransparentTextures]:https://github.com/Naoghuman/lib-tile/tree/master/Lib-Tile-TransparentTextures
[Lib-Tile-TransparentTextures-Images]:https://github.com/Naoghuman/lib-tile/tree/master/Lib-Tile-TransparentTextures-Images
[Maven]:http://maven.apache.org/
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans IDE]:https://netbeans.org/
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin
[NetBeansIDE-AfterburnerFX-Plugin Releases]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin/releases
[ObjectDB]:http://www.objectdb.com/
[properties]:http://en.wikipedia.org/wiki/.properties
[String]:https://docs.oracle.com/javase/8/docs/api/java/lang/String.html
[Tag]:https://github.com/Naoghuman/lib-tag/blob/master/lib-tag-core/src/main/java/com/github/naoghuman/lib/tag/core/Tag.java
[TagBuilder]:https://github.com/Naoghuman/lib-tag/blob/master/lib-tag-core/src/main/java/com/github/naoghuman/lib/tag/core/TagBuilder.java
[TagComponentsFacade]:https://github.com/Naoghuman/lib-tag/blob/master/lib-tag-components/src/main/java/com/github/naoghuman/lib/tag/components/core/TagComponentsFacade.java
[Tile]:https://github.com/Naoghuman/lib-tile/blob/master/Lib-Tile-Core/src/main/java/com/github/naoghuman/lib/tile/core/Tile.java
[TileLoader]:https://github.com/Naoghuman/lib-tile/blob/master/Lib-Tile-Core/src/main/java/com/github/naoghuman/lib/tile/core/TileLoader.java
[TileProvider]:https://github.com/Naoghuman/lib-tile/blob/master/Lib-Tile-Core/src/main/java/com/github/naoghuman/lib/tile/core/TileProvider.java
[TileSet]:https://github.com/Naoghuman/lib-tile/blob/master/Lib-Tile-Core/src/main/java/com/github/naoghuman/lib/tile/core/TileSet.java
[TransparentTexturesTile]:https://github.com/Naoghuman/lib-tile/blob/master/Lib-Tile-TransparentTextures/src/main/java/com/github/naoghuman/lib/tile/transparenttextures/TransparentTexturesTile.java
[TransparentTexturesTileLoader]:https://github.com/Naoghuman/lib-tile/blob/master/Lib-Tile-TransparentTextures/src/main/java/com/github/naoghuman/lib/tile/transparenttextures/images/TransparentTexturesTileLoader.java
[TransparentTexturesTileSet]:https://github.com/Naoghuman/lib-tile/blob/master/Lib-Tile-TransparentTextures/src/main/java/com/github/naoghuman/lib/tile/transparenttextures/TransparentTexturesTileSet.java
[UML]:https://en.wikipedia.org/wiki/Unified_Modeling_Language
