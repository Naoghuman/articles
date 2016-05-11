Lessons learned - an analyse from the video series `Java EE Microservice` from [Adam Bien]
===



<br />
Intention
---

TODO What is the reason, informations over run...

Screenshoot

Offizielle Beschreibung der Video Serie.
A small pizza team deploys a WAR on a lean application server running on Java 8 
within Docker -- and you can call your reasonable app a "microservice". This 
workshop focuses on creation, deployment, robustness, monitoring and communication 
of reasonable WARs using nothing but vanilla Java EE 7, Java 8 and Docker.

Link https://vimeo.com/ondemand/microservices
rent, buy all...

github https://github.com/AdamBien/javaeemicro.services



<br />
Content
---

* [About the autor](#Autor)
* TODO auflistung der tools (tools, libraries, links)
* [Lessons](#Lessons)
    1. [Java 8 Basics - Method References &#40;02:29&#41;](#Lesson1)
    2. [How Expensive Is A Thread? &#40;03:16&#41;](#Lesson2)
    3. [Thread Pools For Robustness &#40;02:58&#41;](#Lesson3)
    4. [Introducing Callables &#40;03:39&#41;](#Lesson4)
    5. [Parallelization With Callable &#40;02:38&#41;](#Lesson5)
    6. [Backpressure And Thread Pools &#40;05:51&#41;](#Lesson6)
    7. [Built-In Task Rejection Policies &#40;01:55&#41;](#Lesson7)
    8. [Custom Overload Policies &#40;02:45&#41;](#Lesson8)
    9. [Building Pipelines With CompletableFutures &#40;02:54&#41;](#Lesson9)
    10. [Data Transformations &#40;01:40&#41;](#Lesson10)
    11. [Combining Pipelines &#40;03:23&#41;](#Lesson11)
    12. [Asynchronous Data Transformations &#40;02:26&#41;](#Lesson12)
    13. [Reuse With Pipeline Composition &#40;03:40&#41;](#Lesson13)
    14. [Transforming Exceptions Into Valid Results &#40;03:43&#41;](#Lesson14)
    15. [CompletableFuture And Exception Handling &#40;02:16&#41;](#Lesson15)
    16. [Configuring The CompletableFuture &#40;05:06&#41;](#Lesson16)
    17. [Custom Thread Pools and CompletableFuture &#40;01:32&#41;](#Lesson17)
    18. [Client-Server JAX-RS Programming &#40;03:38&#41;](#Lesson18)
    19. [JAX-RS Client And The CompletableFuture &#40;02:09&#41;](#Lesson19)
    20. [Sending Data To Server &#40;01:45&#41;](#Lesson20)
    21. [Transfomer -- The Introduction &#40;04:33&#41;](#Lesson21)
    22. [Robustness With Timeouts &#40;03:13&#41;](#Lesson22)
    23. [Timeout Exception Handling &#40;01:33&#41;](#Lesson23)
    24. [Asynchronous JAX-RS &#40;05:39&#41;](#Lesson24)
    25. [Combining Asynchronous JAX-RS With CompletableFuture &#40;03:29&#41;](#Lesson25)
    26. [ManagedExecutorService Configuration &#40;02:06&#41;](#Lesson26)
    27. [Handling Thread Pool Overload &#40;04:00&#41;](#Lesson27)
    28. [Serverside Service Orchestration &#40;04:39&#41;](#Lesson28)
    29. [Dry Pools And Service Stability &#40;03:10&#41;](#Lesson29)
    30. [Bulkheads - What's The Problem? &#40;03:10&#41;](#Lesson30)
    31. [Bulkheads With ManagedExecutorService &#40;03:41&#41;](#Lesson31)
    32. [Concurrency Utilities And Rejection Policies &#40;02:02&#41;](#Lesson32)
    33. [Managed ThreadFactories And Porcupine &#40;03:23&#41;](#Lesson33)
    34. [Backpressure With Porcupine &#40;02:56&#41;](#Lesson34)
    35. [Emitting ThreadPool Statistics &#40;02:12&#41;](#Lesson35)
    36. [Sending Overload Notifications &#40;10:41&#41;](#Lesson36)
    37. [Timeouts And Notifications &#40;04:09&#41;](#Lesson37)
    38. [Managed vs. Unmanaged Threads &#40;04:11&#41;](#Lesson38)
    39. [The Rejected Execution Handler In Detail &#40;05:27&#41;](#Lesson39)
    40. [Appserver Monitoring &#40;04:35&#41;](#Lesson40)
    41. [HTTP Queue Monitoring &#40;03:04&#41;](#Lesson41)
    42. [JDBC Pool Bulkheads &#40;04:52&#41;](#Lesson42)
    43. [HTTP Thread Pool Bulkheads &#40;02:26&#41;](#Lesson43)
    44. [Recap: Bulkheads and Stability &#40;07:22&#41;](#Lesson44)
    45. [Service Consumer Protection &#40;04:13&#41;](#Lesson45)
    46. [Built-In Application Monitoring &#40;05:17&#41;](#Lesson46)
    47. [Ping -- The Smoke Test &#40;04:00&#41;](#Lesson47)
    48. [Business Monitoring &#40;11:07&#41;](#Lesson48)
    49. [Exception Monitoring With Interceptors &#40;10:08&#41;](#Lesson49)
    50. [Protecting Clients With The Circuit Breaker &#40;10:07&#41;](#Lesson50)
    51. [Slow Motion With Snail &#40;02:59&#41;](#Lesson51)
    52. [Microservices--The Definition &#40;06:33&#41;](#Lesson52)
    53. [Java EE -- The "Microservice" Deployment Model &#40;05:45&#41;](#Lesson53)
    54. [What Is The Application Server Overhead? &#40;09:39&#41;](#Lesson54)
    55. [Docker Intro &#40;10:00&#41;](#Lesson55)
    56. [Java EE and Docker &#40;04:57&#41;](#Lesson56)
    57. [Java EE WARs--The Docker App Images &#40;05:13&#41;](#Lesson57)
    58. [The Docker + Java EE Synergy &#40;04:47&#41;](#Lesson58)
    59. [Docker Registry--The Interface &#40;04:51&#41;](#Lesson59)
    60. [Real World Docker &#40;05:31&#41;](#Lesson60)
    61. [Linking Containers With Legacy Links &#40;05:16&#41;](#Lesson61)
    62. [Dynamic Linking With User Defined Networks &#40;04:31&#41;](#Lesson62)
    63. [docker-compose Intro &#40;02:11&#41;](#Lesson63)
    64. [Legacy Links And Java EE &#40;10:46&#41;](#Lesson64)
    65. [Docker Legacy Links With ServiceLink &#40;04:31&#41;](#Lesson65)
    66. [Docker User Defined Networks and ServiceLink &#40;03:42&#41;](#Lesson66)
    67. [Service Configuration With Environment Entries And Docker &#40;06:08&#41;](#Lesson67)
    68. [Dynamic Configuration With In-Memory Grids and Docker &#40;09:23&#41;](#Lesson68)
    69. [Remote Configuration Via JAX-RS &#40;06:49&#41;](#Lesson69)
    70. [Big Thanks !!! &#40;01:09&#41;](#Lesson70)
* [Summary from the lessons](#SummaryLessons)
* [Contact](#Contact)



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
Lessons<a name="Lessons" />
---  



<br />
##### 1. Java 8 Basics - Method References &#40;02:29&#41;<a name="Lesson1" />


<br />
##### 2. How Expensive Is A Thread? &#40;03:16&#41;<a name="Lesson2" />


<br />
##### 3. Thread Pools For Robustness &#40;02:58&#41;<a name="Lesson3" />


<br />
##### 4. Introducing Callables &#40;03:39&#41;<a name="Lesson4" />


<br />
##### 5. Parallelization With Callable &#40;02:38&#41;<a name="Lesson5" />


<br />
##### 6. Backpressure And Thread Pools &#40;05:51&#41;<a name="Lesson6" />


<br />
##### 7. Built-In Task Rejection Policies &#40;01:55&#41;<a name="Lesson7" />


<br />
##### 8. Custom Overload Policies &#40;02:45&#41;<a name="Lesson8" />


<br />
##### 9. Building Pipelines With CompletableFutures &#40;02:54&#41;<a name="Lesson9" />


<br />
##### 10. Data Transformations &#40;01:40&#41;<a name="Lesson10" />


<br />
##### 11. Combining Pipelines &#40;03:23&#41;<a name="Lesson11" />


<br />
##### 12. Asynchronous Data Transformations &#40;02:26&#41;<a name="Lesson12" />


<br />
##### 13. Reuse With Pipeline Composition &#40;03:40&#41;<a name="Lesson13" />


<br />
##### 14. Transforming Exceptions Into Valid Results &#40;03:43&#41;<a name="Lesson14" />


<br />
##### 15. CompletableFuture And Exception Handling &#40;02:16&#41;<a name="Lesson15" />


<br />
##### 16. Configuring The CompletableFuture &#40;05:06&#41;<a name="Lesson16" />


<br />
##### 17. Custom Thread Pools and CompletableFuture &#40;01:32&#41;<a name="Lesson17" />


<br />
##### 18. Client-Server JAX-RS Programming &#40;03:38&#41;<a name="Lesson18" />


<br />
##### 19. JAX-RS Client And The CompletableFuture &#40;02:09&#41;<a name="Lesson19" />


<br />
##### 20. Sending Data To Server &#40;01:45&#41;<a name="Lesson20" />


<br />
##### 21. Transfomer -- The Introduction &#40;04:33&#41;<a name="Lesson21" />


<br />
##### 22. Robustness With Timeouts &#40;03:13&#41;<a name="Lesson22" />


<br />
##### 23. Timeout Exception Handling &#40;01:33&#41;<a name="Lesson23" />


<br />
##### 24. Asynchronous JAX-RS &#40;05:39&#41;<a name="Lesson24" />


<br />
##### 25. Combining Asynchronous JAX-RS With CompletableFuture &#40;03:29&#41;<a name="Lesson25" />


<br />
##### 26. ManagedExecutorService Configuration &#40;02:06&#41;<a name="Lesson26" />


<br />
##### 27. Handling Thread Pool Overload &#40;04:00&#41;<a name="Lesson27" />


<br />
##### 28. Serverside Service Orchestration &#40;04:39&#41;<a name="Lesson28" />


<br />
##### 29. Dry Pools And Service Stability &#40;03:10&#41;<a name="Lesson29" />


<br />
##### 30. Bulkheads - What's The Problem? &#40;03:10&#41;<a name="Lesson30" />


<br />
##### 31. Bulkheads With ManagedExecutorService &#40;03:41&#41;<a name="Lesson31" />


<br />
##### 32. Concurrency Utilities And Rejection Policies &#40;02:02&#41;<a name="Lesson32" />


<br />
##### 33. Managed ThreadFactories And Porcupine &#40;03:23&#41;<a name="Lesson33" />


<br />
##### 34. Backpressure With Porcupine &#40;02:56&#41;<a name="Lesson34" />


<br />
##### 35. Emitting ThreadPool Statistics &#40;02:12&#41;<a name="Lesson35" />


<br />
##### 36. Sending Overload Notifications &#40;10:41&#41;<a name="Lesson36" />


<br />
##### 37. Timeouts And Notifications &#40;04:09&#41;<a name="Lesson37" />


<br />
##### 38. Managed vs. Unmanaged Threads &#40;04:11&#41;<a name="Lesson38" />


<br />
##### 39. The Rejected Execution Handler In Detail &#40;05:27&#41;<a name="Lesson39" />


<br />
##### 40. Appserver Monitoring &#40;04:35&#41;<a name="Lesson40" />


<br />
##### 41. HTTP Queue Monitoring &#40;03:04&#41;<a name="Lesson41" />


<br />
##### 42. JDBC Pool Bulkheads &#40;04:52&#41;<a name="Lesson42" />


<br />
##### 43. HTTP Thread Pool Bulkheads &#40;02:26&#41;<a name="Lesson43" />


<br />
##### 44. Recap: Bulkheads and Stability &#40;07:22&#41;<a name="Lesson44" />


<br />
##### 45. Service Consumer Protection &#40;04:13&#41;<a name="Lesson45" />


<br />
##### 46. Built-In Application Monitoring &#40;05:17&#41;<a name="Lesson46" />


<br />
##### 47. Ping -- The Smoke Test &#40;04:00&#41;<a name="Lesson47" />


<br />
##### 48. Business Monitoring &#40;11:07&#41;<a name="Lesson48" />


<br />
##### 49. Exception Monitoring With Interceptors &#40;10:08&#41;<a name="Lesson49" />


<br />
##### 50. Protecting Clients With The Circuit Breaker &#40;10:07&#41;<a name="Lesson50" />


<br />
##### 51. Slow Motion With Snail &#40;02:59&#41;<a name="Lesson51" />


<br />
##### 52. Microservices--The Definition &#40;06:33&#41;<a name="Lesson52" />


<br />
##### 53. Java EE -- The "Microservice" Deployment Model &#40;05:45&#41;<a name="Lesson53" />


<br />
##### 54. What Is The Application Server Overhead? &#40;09:39&#41;<a name="Lesson54" />


<br />
##### 55. Docker Intro &#40;10:00&#41;<a name="Lesson55" />


<br />
##### 56. Java EE and Docker &#40;04:57&#41;<a name="Lesson56" />


<br />
##### 57. Java EE WARs--The Docker App Images &#40;05:13&#41;<a name="Lesson57" />


<br />
##### 58. The Docker + Java EE Synergy &#40;04:47&#41;<a name="Lesson58" />


<br />
##### 59. Docker Registry--The Interface &#40;04:51&#41;<a name="Lesson59" />


<br />
##### 60. Real World Docker &#40;05:31&#41;<a name="Lesson60" />


<br />
##### 61. Linking Containers With Legacy Links &#40;05:16&#41;<a name="Lesson61" />


<br />
##### 62. Dynamic Linking With User Defined Networks &#40;04:31&#41;<a name="Lesson62" />


<br />
##### 63. docker-compose Intro &#40;02:11&#41;<a name="Lesson63" />


<br />
##### 64. Legacy Links And Java EE &#40;10:46&#41;<a name="Lesson64" />


<br />
##### 65. Docker Legacy Links With ServiceLink &#40;04:31&#41;<a name="Lesson65" />


<br />
##### 66. Docker User Defined Networks and ServiceLink &#40;03:42&#41;<a name="Lesson66" />


<br />
##### 67. Service Configuration With Environment Entries And Docker &#40;06:08&#41;<a name="Lesson67" />


<br />
##### 68. Dynamic Configuration With In-Memory Grids and Docker &#40;09:23&#41;<a name="Lesson68" />


<br />
##### 69. Remote Configuration Via JAX-RS &#40;06:49&#41;<a name="Lesson69" />


<br />
##### 70. Big Thanks !!! &#40;01:09&#41;<a name="Lesson70" />



<br />
Summary from the lessons<a name="SummaryLessons" />
---



<br />
Contact<a name="Contact" />
---

Any question? Some helpful criticism?
* Please write an [Issue] or
* send me an `email` to <peter.rogge@yahoo.de>



[//]: # (Images)



[//]: # (Links)

[Adam Bien]:http://www.adam-bien.com/roller/abien/
[afterburner.fx]:https://github.com/AdamBien/afterburner.fx
[Afterburner.fx NetBeans Plugin Release]:http://www.adam-bien.com/roller/abien/entry/afterburner_fx_netbeans_plugin_release
[DI, IoC and MVP With Java FX -- afterburner.fx Deep Dive]:https://www.youtube.com/watch?v=WsV7kSSSOGs
[Geertjan Wielenga]:https://blogs.oracle.com/geertjan/entry/welcome_to_me
[GitHub]:https://github.com/
[H+D International Group]:https://www.hud.de/en/
[Help for Multilingual NetBeans Platform Applications]:https://dzone.com/articles/multilingual-netbeans-platform-applications
[Issue]:https://github.com/Naoghuman/articles/issues
[JavaFX]:http://docs.oracle.com/javase/8/javase-clienttechnologies.htm
[JavaFX 2.0]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_2.0
[JavaFX 8]:https://en.wikipedia.org/wiki/JavaFX#JavaFX_8
[NetBeans Platform 6.9 Developer's Guide]:https://www.packtpub.com/application-development/netbeans-platform-69-developers-guide
[NetBeans RCP]:https://netbeans.org/kb/trails/platform.html
[NetBeansIDE-AfterburnerFX-Plugin]:https://github.com/Naoghuman/NetBeansIDE-AfterburnerFX-Plugin