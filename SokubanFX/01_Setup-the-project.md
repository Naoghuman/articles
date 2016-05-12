01 Setup the project
===



<br />
Intention
---

In `2008` I wrote a little game `Sokuban Clone` with [Java] and [Swing2D].

![sokuban-clone.png][sokuban-clone]
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
    * [Tweak the project template](#TweakTemplate)  
      [_Tweak the project &#40;name, properties, packages...&#41;_](#TweakProject)  
      [_Update different files like `log4j2.xml`, `application.properties`, `application.fxml`..._](#UpdateFiles)  
      [_Update the JavaDoc &#40;license, autor&#41; if needed_](#UpdateJavaDoc)  
      [_Last steps..._](#LastSteps)
    * [What is the advance from the template?](#AdvanceTemplate)
* [Conclusion](#Conclusion)
* [About the autor](#Autor)
* [Articles in this series](#Articles)
    * [01 Setup the project](#SetupProject)
    * _(not started)_ [02 Create first prototype](#CreatePrototype)
    * _(not started)_ [03 Stabilization from the prototype](#StabilizationPrototype)
    * _(not started)_ [04 Extend the prototype](#ExtendPrototype)
* [Contact](#Contact)



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
##### _Update different files like `log4j2.xml`, `application.properties`, application.fxml..._<a name="UpdateFiles" />

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
  [Maven Central] available.


<br />
#### What is the advance from the template?<a name="AdvanceTemplate" />

After the preperation from the project template we will have a well configured 
minimal desktop application with following advantages:

* With the [javafx-maven-plugin] an executable jar file can be easily created.
    * See the commentary over the injection from the plugin in the `pom.xml` how 
      to create with the simple maven command `mvn jfx:jar` the exceutable jar 
      and all needed libraries.
* Included is the library [afterburner.fx] which is really helpful by the 
  development from [JavaFX] applications.
* Action events can be easily `registered` and `handled` with the library [lib-action].
* With the library [lib-database-objectdb] an `ObjectDB` database is integrated 
  into the project.
* The `log framework` [log4j2] is integrated into the project with good support 
  from the library [lib-logger].
* Integration from the file `application.properties` with helpful support from 
  the library [lib-properties].
* Automatically generation from the file `Preferences.properties` with helpful 
  support from the library [lib-preferences]. 



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
Articles in this series<a name="Articles" />
---

* This article series described how I create the game [SokubanFX] with [JavaFX] 
  and [NetBeans IDE].
* The articles in this series are licensed under [General Public License 3.0].


<br />
##### 01 Setup the project<a name="SetupProject" />

The article [01 Setup the project] describes the steps how to setup a new project 
in [GitHub] with my project template and what are the advantages from using this
template [Project-Template-afterburnerfx-Naoghuman].


<br />
##### 02 Create first prototype<a name="CreatePrototype" />

_(not started)_ The article [02 Create first prototype] describes the steps and 
decisions which I make during the implementation from the first `prototype`.


<br />
##### 03 Stabilization from the prototype<a name="StabilizationPrototype" />

_(not started)_ The article [03 Stabilization from the prototype] describes the 
steps how I stabilize the prototype.


<br />
##### 04 Extend the prototype<a name="ExtendPrototype" />

_(not started)_ The article [04 Extend the prototype] describes the steps to 
extend the prototype.



<br />
Contact<a name="Contact" />
---

Any question? Some helpful criticism?
* Please write an [Issue] or
* send me an `email` to <peter.rogge@yahoo.de>



[//]: # (Images)
[sokuban-clone]:https://cloud.githubusercontent.com/assets/8161815/12365174/72d57abc-bbd3-11e5-84d8-80c5d647b897.png



[//]: # (Links)
[01 Setup the project]:01_Setup-the-project.md
[02 Create first prototype]:02_Create-first-prototype.md
[03 Stabilization from the prototype]:03_Stabilization-from-the-prototype.md
[04 Extend the prototype]:04_Extend-the-prototype.md
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
[Swing2D]:https://docs.oracle.com/javase/tutorial/2d/
