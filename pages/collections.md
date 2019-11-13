## Collections

* Pas d'import nécessaire
* Ajout de fonctions par rapport au Java
* Instanciation via des fonctions
    * arrayOf, mutableArrayOf
    * listOf, mutableListOf
    * mapOf, mutableMapOf
    * setOf, mutableSetOf


### Analogie avec les Stream Java8

* Pas d'appel au .stream()
* applicable sur tout type itérable <!-- .element: class="fragment" -->
* Ré-utilisable <!-- .element: class="fragment" -->
* Eager (Lazy pour Java)  <!-- .element: class="fragment" -->
* flatMap ne nécessite pas de renvoyer un stream <!-- .element: class="fragment" -->


### Lazy vs Eager

Eager - 5 map, 5 filter <!-- .element: style="color: #238500"-->
```kotlin
val result = listOf(1, 2, 3, 4, 5) 
  .map { n -> n * n } 
  .filter { n -> n < 10 } 
  .first()
```

Lazy - 1 map, 1 filter <!-- .element: style="color: #238500"-->
```kotlin
val result = listOf(1, 2, 3, 4, 5).asSequence()
  .map { n -> n * n } 
  .filter { n -> n < 10 } 
  .first()
```  

