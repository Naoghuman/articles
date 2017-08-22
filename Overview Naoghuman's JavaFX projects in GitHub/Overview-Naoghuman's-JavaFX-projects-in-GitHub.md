Overview Naoghuman's JavaFX projects in GitHub
===



Intention
---

In this article I want to give an `overiew` about my [JavaFx] `plugins`, `libraries`, 
`games` and `applications` and how they work together.
* The `Tier 0: Plugins` section contains a [NetBeansIDE-AfterburnerFX-Plugin] 
  which supports the [JavaFX] development in a [Maven] context in conjunction 
  with the library [afterburner.fx] from [Adam Bien].
* The `Tier 1: Core Libraries` section contains all core libraries from me 
  which I used in all my projects depends on the concrete case.
* The `Tier 2: Extended Libraries` section contains libraries which depends 
  on one or more libraries from the section `Tier 1: Core Libraries`.
* In the last `Tier 3: Applications / Games` section I list different `applications` 
  and `games` from me where I used the libraries from the sections `Tier 1: Core Libraries` 
  and `Tier 2: Extended Libraries`.

_Image:_ Overview Naoghuman's JavaFX projects in GitHub  
![overview-naoghumans-javafx-projects-in-github-v1.png][overview-naoghumans-javafx-projects-in-github-v1]

> __Hint__  
> Every entry in every `Tier` follows the same structure -> description, examples, 
> conclusion and then the details. Exception is the `NetBeansIDE-AfterburnerFX-Plugin` 
> where I added a subsection `Press`.



Content
---

* [Tier 0: Plugins](#Ti0Pl)
    - [NetBeansIDE-AfterburnerFX-Plugin _(Stable)_](#NeBeAfPl)
* [Tier 1: Core Libraries](#Ti1CoLi)
    - [Lib-Logger _(Stable)_](#LiLo)
    - [Lib-Action _(Stable)_](#LiAc)
    - [Lib-Database-ObjectDB _(Stable)_](#LiDaOb)
    - [Lib-Preferences _(Stable)_](#LiPre)
    - [Lib-Properties _(Stable)_](#LiPro)
* [Tier 2: Extended Libraries](#Ti2ExLi)
    - [Lib-Tag _(Stable)_](#LiTa)
    - [Lib-Tile _(Stable)_](#LiTi)
    - [Lib-Emoticon _(Stable)_](#LiEm)
    - [Lib-Testdata _(Development)_](#LiTe)
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



Tier 0: Plugins<a name="Ti0Pl" />
---

TODO

### NetBeansIDE-AfterburnerFX-Plugin _(Stable)_<a name="NeBeAfPl" />

> __Plugin description__  
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


**Example**  
The following picture shows all possible files which can be generate in one slide 
with the new wizard after installing the plugin in your [NetBeans IDE].

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


**Plugin details**  

| GitHub | [NetBeansIDE-AfterburnerFX-Plugin] |
| --- | --- |
| Since | Sep 22, 2015 |
| Releases | [NetBeansIDE-AfterburnerFX-Plugin Releases] _(6 releases)_ |
| Last release | [1.5.0] _(Stable)_ |
| Licence | [General Public License 3.0] |



Tier 1: Core Libraries<a name="Ti1CoLi" />
---

TODO

### Lib-Logger _(Stable)_<a name="LiLo" />

> __Library description__  
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


**Library details**  

| GitHub | [Lib-Logger] |
| --- | --- |
| Since | Jul 13, 2014 |
| Releases | [Lib-Logger Releases] _(13 releases)_ |
| Last release | [Lib-Logger v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Action _(Stable)_<a name="LiAc" />

> __Library description__  
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


**Library details**  

| GitHub | [Lib-Action] |
| --- | --- |
| Since | Jul 26, 2014 |
| Releases | [Lib-Action Releases] _(15 releases)_ |
| Last release | [Lib-Action v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Database-ObjectDB _(Stable)_<a name="LiDaOb" />

> __Library description__  
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


**Library details**  

| GitHub | [Lib-Database-ObjectDB] |
| --- | --- |
| Since | Nov 25, 2014 |
| Releases | [Lib-Database-ObjectDB Releases] _(11 releases)_ |
| Last release | [Lib-Database-ObjectDB v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Preferences _(Stable)_<a name="LiPre" />

> __Library description__  
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


**Library details**  

| GitHub | [Lib-Preferences] |
| --- | --- |
| Since | Jul 16, 2014 |
| Releases | [Lib-Preferences Releases] _(11 releases)_ |
| Last release | [Lib-Preferences v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Properties _(Stable)_<a name="LiPro" />

> __Library description__  
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


**Library details**  

| GitHub | [Lib-Properties] |
| --- | --- |
| Since | Jul 18, 2014 |
| Releases | [Lib-Properties Releases] _(12 releases)_ |
| Last release | [Lib-Properties v0.5.0] _(Stable)_ |
| Licence | [General Public License 3.0] |



Tier 2: Extended Libraries<a name="Ti2ExLi" />
---

### Lib-Tag _(Stable)_<a name="LiTa" />

### Lib-Tile _(Stable)_<a name="LiTi" />

### Lib-Emoticon _(Stable)_<a name="LiEm" />

### Lib-Testdata _(Development)_<a name="LiTe" />

### Lib-Sampler_(Prototpye)_<a name="LiSa" />

### Lib-Map_(Prototype)_<a name="LiMa" />


Tier 3: Applications / Games<a name="Ti3ApGa" />
---

TODO

### Application ABC-List _(Development)_<a name="ApAbLi" />

### Application HabitFX _(Development)_<a name="ApHaFx" />

### Application Competency Matrix _(Prototpye)_<a name="ApCoMa" />

### Application Concentration _(Planed)_<a name="ApCon" />

### Application TypeWriter _(Planed)_<a name="ApTyWr" />

### Game SokubanFX _(Development)_<a name="GaSoFx" />

### Game StepByStep _(Prototpye)_<a name="GaStBySt" />






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
[plugin-3-primary-files]:https://cloud.githubusercontent.com/assets/8161815/23524833/a4122dca-ff8c-11e6-8200-77395646fbb0.png
[plugin-6-generated-files]:https://cloud.githubusercontent.com/assets/8161815/23524879/c901106a-ff8c-11e6-97b1-31ba03b7b679.png
[UML-diagram_Lib-Action_v0.5.1_2017-07-22_23-42]:https://user-images.githubusercontent.com/8161815/28494737-a28b46f6-6f37-11e7-8c66-01083545c092.png
[UML-diagram_Lib-Database-ObjectDB_v0.5.1_2017-07-30_15-34]:https://user-images.githubusercontent.com/8161815/28753983-b1feefba-753c-11e7-9233-3a4a16f9a1ad.png
[UML-diagram_Lib-Logger_v0.5.1_2017-07-19_23-44]:https://user-images.githubusercontent.com/8161815/28390956-64b5d38a-6cdc-11e7-84b7-153ace99fc3e.png
[UML-diagram_Lib-Preferences_v0.5.1_2017-08-02_22-04]:https://user-images.githubusercontent.com/8161815/28892584-c3b4afd0-77ce-11e7-8d52-65c4cc491c88.png
[UML-diagram_Lib-Properties_v0.5.0_2017-07-17_21-17]:https://user-images.githubusercontent.com/8161815/28286098-5c85b802-6b37-11e7-8db0-47eed1156c43.png
[video-netBeanside-afterburnerfx-plugin]:https://cloud.githubusercontent.com/assets/8161815/15169398/3b51c3de-173b-11e6-8a8f-39cc6b826260.png



[//]: # (Links)
[1.5.0]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin/releases/tag/v1.5.0
[ActionEvent]:http://docs.oracle.com/javase/8/javafx/api/javafx/event/ActionEvent.html
[Adam Bien]:http://www.adam-bien.com/roller/abien/
[Afterburner.fx NetBeans Plugin Release]:http://www.adam-bien.com/roller/abien/entry/afterburner_fx_netbeans_plugin_release
[afterburner.fx]:https://github.com/AdamBien/afterburner.fx
[Apache Log4j 2]:https://logging.apache.org/log4j/2.0/index.html
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
[EventHandler]:http://docs.oracle.com/javase/8/javafx/api/javafx/event/EventHandler.html
[Geertjan Wielenga]:https://blogs.oracle.com/geertjan/entry/welcome_to_me
[General Public License 3.0]:http://www.gnu.org/licenses/gpl-3.0.en.html
[GitHub]:https://github.com/
[H+D International Group]:https://www.hud.de/en/
[Help for Multilingual NetBeans Platform Applications]:https://dzone.com/articles/multilingual-netbeans-platform-applications
[Issue]:https://github.com/Naoghuman/articles/issues
[Java]:https://en.wikipedia.org/wiki/Java_%28programming_language%29
[JavaFX]:http://docs.oracle.com/javase/8/javase-clienttechnologies.htm
[JavaFX 2.0]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_2.0
[JavaFX 8]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_8
[Lib-Action]:https://github.com/Naoghuman/lib-action
[Lib-Action Releases]:https://github.com/Naoghuman/lib-action/releases
[Lib-Action v0.5.1]:https://github.com/Naoghuman/lib-action/releases/tag/v0.5.1
[Lib-Database-ObjectDB]:https://github.com/Naoghuman/lib-database-objectdb
[Lib-Database-ObjectDB Releases]:https://github.com/Naoghuman/lib-database-objectdb/releases
[Lib-Database-ObjectDB v0.5.1]:https://github.com/Naoghuman/lib-database-objectdb/releases/tag/v0.5.1
[Lib-Logger]:https://github.com/Naoghuman/lib-logger
[Lib-Logger Releases]:https://github.com/Naoghuman/lib-logger/releases
[Lib-Logger v0.5.1]:https://github.com/Naoghuman/lib-logger/releases/tag/v0.5.1
[Lib-Preferences]:https://github.com/Naoghuman/lib-preferences
[Lib-Preferences Releases]:https://github.com/Naoghuman/lib-preferences/releases
[Lib-Preferences v0.5.1]:https://github.com/Naoghuman/lib-preferences/releases/tag/v0.5.1
[Lib-Properties]:https://github.com/Naoghuman/lib-properties
[Lib-Properties Releases]:https://github.com/Naoghuman/lib-properties/releases
[Lib-Properties v0.5.0]:https://github.com/Naoghuman/lib-properties/releases/tag/v0.5.0
[Maven]:http://maven.apache.org/
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans IDE]:https://netbeans.org/
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin
[NetBeansIDE-AfterburnerFX-Plugin Releases]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin/releases
[ObjectDB]:http://www.objectdb.com/
[properties]:http://en.wikipedia.org/wiki/.properties
[UML]:https://en.wikipedia.org/wiki/Unified_Modeling_Language
