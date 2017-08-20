Overview Naoghuman's JavaFX projects in GitHub
===



Intention
---

In this article I want to give an `overiew` about my [JavaFx] `plugins`, `libraries`, 
`games` and `applications` and how they work together.
* The `basement` from my projects are the libraries in [Core Libraries].
* Next I have [Extended Libraries] which depends on one or more from the `Core Libraries`.
* In the [Games] and [Applications] I used then the `Core Libraries` and `Extended Libraries` 
  if needed.

_Image:_ Overview Naoghuman's JavaFX projects in GitHub  
![overview-naoghumans-javafx-projects-in-github-v1.png][overview-naoghumans-javafx-projects-in-github-v1]

> __Hint__  
> All `plugins`, `libraries`, `games` and `projects` from me (Naoghuman) are 
> licensed under [General Public License 3.0].



Content
---

* [Plugins](#Pl)
    - [NetBeansIDE-AfterburnerFX-Plugin _(Stable)_](#NeBeAfPl)
* [Core Libraries](#CoLi)
    - [Lib-Logger _(Stable)_](#LiLo)
    - [Lib-Action _(Stable)_](#LiAc)
    - [Lib-Database-ObjectDB _(Stable)_](#LiDaOb)
    - [Lib-Preferences _(Stable)_](#LiPre)
    - [Lib-Properties _(Stable)_](#LiPro)
* [Extended Libraries](#ExLi)
    - [Lib-Tag _(Stable)_](#LiTa)
    - [Lib-Tile _(Stable)_](#LiTi)
    - [Lib-Emoticon _(Stable)_](#LiEm)
    - [Lib-Testdata _(Development)_](#LiTe)
    - [Lib-Sampler _(Prototpye)_](#LiSa)
    - [Lib-Map _(Prototype)_](#LiMa)
* [Games](#Gam)
    - [SokubanFX _(Development)_](#SoFx)
    - [StepByStep _(Prototpye)_](#StBySt)
* [Applications](#App)
    - [ABC-List _(Development)_](#AbLi)
    - [HabitFX _(Development)_](#HaFx)
    - [Competency Matrix _(Prototpye)_](#CoMa)
    - [Concentration _(Planed)_](#Con)
    - [TypeWriter _(Planed)_](#TyWr)
* [About the autor](#Autor)
    - [Contact](#Contact)
* [Other articles from me](#OtherArticles)



Plugins<a name="Pl" />
---

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
| Last release | [1.5.0] _(Stable, 6 releases)_ |
| Licence | [General Public License 3.0] |
| Since | Sep 22, 2015 |



Core Libraries<a name="CoLi" />
---

TODO

### Lib-Logger _(Stable)_<a name="LiLo" />

> __Library description__  
> `Lib-Logger` is a library for `easy` logging with the [Apache Log4j 2] in a 
> [JavaFX] &amp; [Maven] desktop application.

_Image:_ [UML] Lib-Logger  
![UML-diagram_Lib-Logger_v0.5.1_2017-07-19_23-44.png][UML-diagram_Lib-Logger_v0.5.1_2017-07-19_23-44]


**Example**  
After including the library into your [Maven] project with
```java
<dependency>
    <groupId>com.github.naoghuman</groupId>
    <artifactId>lib-logger</artifactId>
    <version>0.5.1</version>
</dependency>
```

put also the file `log4j2.xml` into the default resource package `src/main/resources` 
in your project. Then logging is simple:
```java
public static final void loadResourcesInCache() {
    LoggerFacade.getDefault().debug(TemplateLoader.class, "Load resources in cache"); // NOI18N

    ...
}

// which will print in the console and in the configured `xy.log` file:
2017-05-27 08:56:53,757  DEBUG Load resources in cache     [TemplateLoader]
```

**Conclusion**  
With the library `Lib-Logger it's really easy to integrate the feature `logging` 
into your `library`, `game` and / or `application`.  


**Library details**  

| GitHub | [Lib-Logger] |
| --- | --- |
| Since | Jul 13, 2014 |
| Releases | [Lib-Logger Releases] _(13 releases)_ |
| Last release | [Lib-Logger v0.5.1] _(Stable)_ |
| Licence | [General Public License 3.0] |


### Lib-Action _(Stable)_<a name="LiAc" />

### Lib-Database-ObjectDB _(Stable)_<a name="LiDaOb" />

### Lib-Preferences _(Stable)_<a name="LiPre" />

### Lib-Properties _(Stable)_<a name="LiPro" />



Extended Libraries<a name="ExLi" />
---

### Lib-Tag _(Stable)_<a name="LiTa" />

### Lib-Tile _(Stable)_<a name="LiTi" />

### Lib-Emoticon _(Stable)_<a name="LiEm" />

### Lib-Testdata _(Development)_<a name="LiTe" />

### Lib-Sampler_(Prototpye)_<a name="LiSa" />

### Lib-Map_(Prototype)_<a name="LiMa" />



Games<a name="Gam" />
---

### SokubanFX _(Development)_<a name="SoFx" />

### StepByStep _(Prototpye)_<a name="StBySt" />



Applications<a name="App" />
---

### ABC-List _(Development)_<a name="AbLi" />

### HabitFX _(Development)_<a name="HaFx" />

### Competency Matrix _(Prototpye)_<a name="CoMa" />

### Concentration _(Planed)_<a name="Con" />

### TypeWriter _(Planed)_<a name="TyWr" />



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
[UML-diagram_Lib-Logger_v0.5.1_2017-07-19_23-44]:https://user-images.githubusercontent.com/8161815/28390956-64b5d38a-6cdc-11e7-84b7-153ace99fc3e.png
[video-netBeanside-afterburnerfx-plugin]:https://cloud.githubusercontent.com/assets/8161815/15169398/3b51c3de-173b-11e6-8a8f-39cc6b826260.png



[//]: # (Links)
[1.5.0]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin/releases/tag/v1.5.0
[Adam Bien]:http://www.adam-bien.com/roller/abien/
[Afterburner.fx NetBeans Plugin Release]:http://www.adam-bien.com/roller/abien/entry/afterburner_fx_netbeans_plugin_release
[afterburner.fx]:https://github.com/AdamBien/afterburner.fx
[Apache Log4j 2]:https://logging.apache.org/log4j/2.0/index.html
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
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
[Lib-Logger]:https://github.com/Naoghuman/lib-logger
[Lib-Logger Releases]:https://github.com/Naoghuman/lib-logger/releases
[Lib-Logger v0.5.1]:https://github.com/Naoghuman/lib-logger/releases/tag/v0.5.1
[Maven]:http://maven.apache.org/
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans IDE]:https://netbeans.org/
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin
[UML]:https://en.wikipedia.org/wiki/Unified_Modeling_Language
