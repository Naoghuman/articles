01 Setup the project
===



<br />
Intention
---

In `2008` I wrote a little game [Sokuban-Clone] with [Java] and [Swing2D].

![sokuban-clone.png][sokuban-clone-png]
* [GitHub] project: https://github.com/Naoghuman/sokuban-clone  
* Download: https://github.com/Naoghuman/sokuban-clone/releases


<br />
In `April 2016` I decided to rewrite the game in [JavaFX].

In this first article I will write down the steps how I setup the new project with 
another [GitHub] project from me `Project-Template-afterburnerfx-Naoghuman` and 
what are the advantages from using this template:
* [GitHub] project: https://github.com/Naoghuman/Project-Templates
* Download: https://github.com/Naoghuman/Project-Templates/releases



<br />
Content
---

* [Setup the project](#SetupTheProject)
    * [Download the project template](#DownloadTemplate)
    * **&#40;updated&#41;** [Tweak the project template](#TweakTemplate)  
      [_Tweak the project &#40;name, properties, packages...&#41;_](#TweakProject)  
      [_Update different files like `log4j2.xml`, `application.properties`, `application.fxml`..._](#UpdateFiles)  
      [_Update the JavaDoc &#40;license, autor&#41; if needed_](#UpdateJavaDoc)  
      [_Last steps..._](#LastSteps)
    * **&#40;updated&#41;** [What is the advantages from using the template?](#AdvanceTemplate)  
      [_The advantage from javafx-maven-plugin_](#AdvJavMavPlu)  
      [_The advantage from afterburner.fx_](#AdvAft)  
      [_The advantage from lib-action_](#AdvLibAct)  
      [_The advantage from lib-database-objectdb_](#AdvLibDatObj)  
      [_The advantage from lib-logger_](#AdvLibLog)  
      [_The advantage from lib-preferences_](#AdvLibPre)  
      [_The advantage from lib-properties_](#AdvLibPro)
* **&#40;new&#41;** [Conclusion](#Conclusion)
* [About the autor](#Autor)
    * [Contact](#Contact)
* [Articles in this series](#Articles)



<br />
Setup the project<a name="SetupTheProject" />
---

In this section I will explain how to download the project template 
[Project-Template-afterburnerfx-Naoghuman] and then after installation into the 
[NetBeans IDE] or another from you preferred IDE how to tweak it for the new 
requirements for the game `SokubanFX`.

A demo from the minimal project template can be found under 
https://github.com/Naoghuman/Project-Templates/releases/tag/v0.1.0.
* Unzip the `zip` file to a folder from your choose and doubleclick the `jar` file.


<br />
##### Download the project template<a name="DownloadTemplate" />

There are two possiblilities to `included` the project template into your 
preferred IDE &#40;for me that is [NetBeans IDE]&#41;:

a) Download the `source code` from https://github.com/Naoghuman/Project-Templates/releases/tag/v0.1.0.
* Unzip the source code to your workspace and open the project within the [NetBeans IDE].

b) Clone the project with https://github.com/Naoghuman/Project-Templates.git
* Navigate into the new created project `Project-Templates`.
* Copy and paste there the project `Project-Template-afterburnerfx-Naoghuman` 
  to a new destination.


<br />
##### Tweak the project template<a name="TweakTemplate" />

In the project is a file `Tweak-Project-Template.txt` where the steps are listed 
which are necessary to tweak the template.


<br />
##### _Tweak the project &#40;name, properties, packages...&#41;_<a name="TweakProject" />

* Rename the project `name` (display name, artefactID and folder).
* Update the `packages` in the folders `Source Packages/` and `Other Sources/`.
* Open the project `properties` window to tweak following parameters.
   * `General`-> GroupId, ArtefactId, Version, Name, Description.
   * `Run` -> Update the start class.
   * `License Header` -> If you don't want the pre-choosen [General Public License 3.0].

<br />
##### _Update different files like `log4j2.xml`, `application.properties`, `application.fxml`..._<a name="UpdateFiles" />

* Update the reference in the tag `fx:controller` in the file 
  `Source Packages/yourpackage/application/application.fxml`.
* Refactore the `path` from the parameter `KEY__APPLICATION__RESOURCE_BUNDLE` 
  from the interface `IApplicationConfiguration` in the folder 
  `Source Packages/yourpackage/configuration/`.
* Update the file `application.properties` in the folder `Other Sources/yourpackage/application/`
  if needed.
* Update the file `log4j2.xml` in the default package from `Other Sources/` if 
  needed.

<br />
##### _Update the JavaDoc &#40;license, autor&#41; if needed_<a name="UpdateJavaDoc" />

* If your project license different from [General Public License 3.0] which is 
  preselect in the project template then you can refactore the `licence` in all 
  java files and `application.properties` with following steps:
    * Change in the project under `properties` the license.
    * Generate a new java file.
    * Copy and paste the new generated license as needed.  
      Another possiblitiy is to use the `Replace...`, `Replace in Projects...` 
      function under `Edit` in the main menu.
* Rename the `autor` in all `java` files and `application.properties`.
    * Same here -> `Replace...`, `Replace in Projects...`.

<br />
##### _Last steps..._<a name="LastSteps" />

* Move the folder 'me' to your `local` maven repository.
* The folder contains my above described libraries which are `momentary` not in 
  [Maven Central] available. I plan for the future to upload my libraries to the 
  [Maven Central], then this step wouldn't be necessary anymore.


<br />
#### **&#40;updated&#41;** What is the advantages from using the template?<a name="AdvanceTemplate" />

After the preperation from the project template we will have a well configured 
minimal [JavaFX], [Maven] desktop application with following below listed 
advantages. Also every library have for its own great functionalities its the 
interaction from all libraries in the working project which is the greatest 
advantage :innocent: from the template.


<br />
##### _The advantage from javafx-maven-plugin_<a name="AdvJavMavPlu" />

* An interactive guide `how to configured` the plugin can be found under:  
  https://javafx-maven-plugin.github.io/
* Copy and paste the configuration into your `pom.xml`.
* Now execute the command `mvn jfx:jar` into your project folder and magically 
  the jar file will be generated with all needed libraries.

![generated-jar-file.png][generated-jar-file]


<br />
##### _The advantage from afterburner.fx_<a name="AdvAft" />

* Included is the library [afterburner.fx] which is really helpful by the 
  development from [JavaFX] applications.

With the library 'afterburner.fx' its possible to do something like:
```java
final List<CategoryModel> categoryModels = SqlFacade.INSTANCE.getCategorySqlProvider().findAll(matrixModel.getId());
final List<Parent> categoryThumbnailViews = FXCollections.observableArrayList();
for (CategoryModel categoryModel : categoryModels) {
    final CategoryThumbnailView categoryThumbnailView = new CategoryThumbnailView();
    final CategoryThumbnailPresenter categoryThumbnailPresenter = categoryThumbnailView.getRealPresenter();
    categoryThumbnailPresenter.initialize(categoryModel);
    categoryThumbnailViews.add(categoryThumbnailView.getView());
}
```


<br />
One more advantage from the `usage` from [afterburner.fx] with [NetBeans IDE] is 
that you can use a plugin from me which helps zu generate the files:

![generated-files-plugin.png][generated-files-plugin]

The plugin is available above the `Update Center` from [NetBeans IDE] or in the 
[GitHub] project:  
https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin/releases


<br />
##### _The advantage from lib-action_<a name="AdvLibAct" />

* Action events can be easily `registered` and `handled` with the library [lib-action].

For example have a look here how to `register` an action:
```java
public class ApplicationPresenter implements Initializable, IActionConfiguration, IRegisterActions {
    ...

    @Override
    public void registerActions() {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Register actions in ApplicationPresenter"); // NOI18N
        
        this.registerOnActionChangeToGameView();
        this.registerOnActionHideMainMenu();
        this.registerOnActionShowMainMenu();
    }

    private void registerOnActionChangeToGameView() {
        LoggerFacade.INSTANCE.debug(this.getClass(), "Register on action change to GameView");
        
        ActionFacade.INSTANCE.register(
                ON_ACTION__CHANGE_TO_GAMEVIEW,
                (ActionEvent event) -> {
                    PreferencesFacade.INSTANCE.putBoolean(
                            IPreviewConfiguration.PROP__KEY_RELEASED__FOR_PREVIEW, 
                            Boolean.FALSE);
        
                    this.onActionChangeToGameView();
                }
        );
    }

    private void onActionChangeToGameView() {
        ...

        final GameView gameView = new GameView();
        final GamePresenter gamePresenter = gameView.getRealPresenter();
        gamePresenter.registerActions();

        ...
    }

    ...
}
```

1. With the interface `com.github.naoghuman.lib.action.api.IRegisterActions` the 
   developer override the method `registerActions()`.
2. In this method all individual actions will be registered.
3. If the `View` should be instantiate, then over the `Presenter` the method 
   `registerActions()` will be called and then all actions registered.
4. Acces to the action can be done with the `action-key`. In this case is that 
   `ON_ACTION__CHANGE_TO_GAMEVIEW`.

```java
public class PreviewPresenter implements Initializable, IActionConfiguration, IRegisterActions {
    ...

    public void onActionStartGame() {
        LoggerFacade.INSTANCE.debug(this.getClass(), "On action start Game"); // NOI18N
        
        if (ptShowNextRandomMap.getStatus().equals(Animation.Status.RUNNING)) {
            ptShowNextRandomMap.stop();
        }
        
        ActionFacade.INSTANCE.handle(ON_ACTION__CHANGE_TO_GAMEVIEW);
    }

    ...
}
```

Its also possible to define `com.github.naoghuman.lib.action.api.TransferData` 
which can store for example `data models`. For more informations plz see:  
https://github.com/Naoghuman/lib-action


<br />
##### _The advantage from lib-database-objectdb_<a name="AdvLibDatObj" />

* With the library [lib-database-objectdb] an `ObjectDB` database is integrated 
  into the project.


```java
```
<br />
##### _The advantage from lib-logger_<a name="AdvLibLog" />

* The `log framework` [log4j2] is integrated into the project with good support 
  from the library [lib-logger].


```java
```
<br />
##### _The advantage from lib-preferences_<a name="AdvLibPre" />

* Automatically generation from the file `Preferences.properties` with helpful 
  support from the library [lib-preferences].


```java
```
<br />
##### _The advantage from lib-properties_<a name="AdvLibPro" />

* Integration from the file `application.properties` with helpful support from 
  the library [lib-properties].


```java
```


<br />
**&#40;new&#41;** Conclusion<a name="Conclusion" />
---

It seems there are many points which should be updated in the project template. 
For me it takes 10min and all things are done and the project with above listed 
advantages :smile: is ready.



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
[generated-jar-file]:https://cloud.githubusercontent.com/assets/8161815/15264356/c327cbda-1972-11e6-8719-1af408843d91.png
[generated-files-plugin]:https://cloud.githubusercontent.com/assets/8161815/15264601/3525b25e-1975-11e6-85d1-74fac8aa2196.png
[sokuban-clone-png]:https://cloud.githubusercontent.com/assets/8161815/12365174/72d57abc-bbd3-11e5-84d8-80c5d647b897.png



[//]: # (Links)
[01 Setup the project]:01_Setup-the-project.md
[02 Create first prototype]:02_Create-first-prototype.md
[03 Stabilization from the prototype]:03_Stabilization-from-the-prototype.md
[Adam Bien]:http://www.adam-bien.com/roller/abien/
[Afterburner.fx NetBeans Plugin Release]:http://www.adam-bien.com/roller/abien/entry/afterburner_fx_netbeans_plugin_release
[afterburner.fx]:https://github.com/AdamBien/afterburner.fx
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
[General Public License 3.0]:http://www.gnu.org/licenses/gpl-3.0.en.html
[Geertjan Wielenga]:https://blogs.oracle.com/geertjan/entry/welcome_to_me
[GitHub]:https://github.com/
[Help for Multilingual NetBeans Platform Applications]:https://dzone.com/articles/multilingual-netbeans-platform-applications
[H+D International Group]:https://www.hud.de/en/
[Issue]:https://github.com/Naoghuman/articles/issues
[Java]:https://en.wikipedia.org/wiki/Java_%28programming_language%29
[javafx-maven-plugin]:https://github.com/javafx-maven-plugin/javafx-maven-plugin
[JavaFX 2.0]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_2.0
[JavaFX 8]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_8
[JavaFX]:http://docs.oracle.com/javase/8/javase-clienttechnologies.htm
[lib-action]:https://github.com/Naoghuman/lib-action
[lib-database-objectdb]:https://github.com/Naoghuman/lib-database-objectdb
[lib-logger]:https://github.com/Naoghuman/lib-logger
[lib-properties]:https://github.com/Naoghuman/lib-properties
[lib-preferences]:https://github.com/Naoghuman/lib-preferences
[log4j2]:http://logging.apache.org/log4j/2.x/
[Maven]:https://maven.apache.org/
[Maven Central]:http://search.maven.org/
[NetBeans IDE]:https://netbeans.org/
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin
[Project-Template-afterburnerfx-Naoghuman]:https://github.com/Naoghuman/Project-Templates/tree/master/Project-Template-afterburnerfx-Naoghuman
[SokubanFX]:https://github.com/Naoghuman/SokubanFX
[Sokuban-Clone]:https://github.com/Naoghuman/sokuban-clone
[Swing2D]:https://docs.oracle.com/javase/tutorial/2d/
