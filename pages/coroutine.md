# Coroutine


### Les coroutines, c'est quoi ?

* "Threads légers"<!-- .element: class="fragment" -->
    * concurrence gérée au niveau de Kotlin
    * utilisation de vrais threads au besoin
* Code élégant<!-- .element: class="fragment" -->
    * async / await
    * adieu les CompletableFuture !
* Programmation asynchrone<!-- .element: class="fragment" -->


### le vocabulaire

* CoroutineContext<!-- .element: class="fragment" -->
    * Contexte d'execution d'une coroutine
* CoroutineScope<!-- .element: class="fragment" -->
    * Scope dans lequel on peut lancer des coroutines
* Lancement de coroutine<!-- .element: class="fragment" -->
    * launch / async
    * await : attend le résultat d'une fonction lancée dans async


```kotlin
newSingleThreadContext("my-context").use { ctx ->
    runBlocking(ctx) { // CorountineScope
        val one = async {
            // coroutine
            delay(1000L);
            1
        }
        val two = async {
            // coroutine
            delay(2000L);
            2
        }
        println(one.await() + two.await())
    }
}
```


### Un peu de concret

```kotlin
// liste des 12 signes du zodiaque
val signs = arrayOf("Bélier", "Taureau", "Gémeaux", "Cancer" ...)
```

```kotlin
// Appel API /horoscopes/$date/$sign avec la lib Jersey
// récupere l'horoscope pour un jour et un signe donnés
fun getHoroscope(date: String, sign: String): Horoscope {
    val client = Client()
    val webResource = client.resource("$baseUrl/horoscopes/$date/$sign")
    val response = webResource
            .accept("application/json")
            .type("application/json")
            .get(ClientResponse::class.java)
    if (response.getStatus() != 200) {
        throw RuntimeException("Failed : HTTP error code : " + response.getStatus())
    }
    return response.getEntity(Horoscope::class.java)
}
```
* Objectif : récupérer tous les horoscopes du jour<!-- .element: class="fragment" style="color: #e73e01" -->


### Solution séquentielle
```kotlin 
// pour chaque signe on fait l'appel à l'API
// on obtient une liste contenant tous les horoscopes du jour  
val results = signs.map { sign -> getHoroscope(today, sign) }
println(results)
```
Temps d'exécution ≃ 1393ms<!-- .element: class="fragment" -->


### Parallélisation avec les coroutines

```kotlin
val horoscopes = arrayListOf<Horoscope>()
runBlocking(Dispatchers.IO) { // utilisation du pool de threads IO
    val horoscopesDeferred = signs.map { sign ->
        // appel async pour chaque signe
        async { getHoroscope(today, sign) }
    }
    horoscopesDeferred.forEach {
        // pour chaque resultat d'appel
        // on attend que le résultat soit arrivé
        horoscopes.add(it.await())
    }
}
println(horoscopes)
```
<!-- .element: class="fragment" -->
(Solution équivalente à CompletableFuture)<!-- .element: class="fragment" -->

Temps d'exécution ≃ 350ms<!-- .element: class="fragment" -->


### Programmation asynchrone


### Suspending functions

* Fonctions dont l'exécution peut être suspendue et reprise plus tard<!-- .element: class="fragment" -->
    * Ne bloque pas le thread
* Ne peut être lancée que par une autre "suspending function"<!-- .element: class="fragment" -->
* Programmation asynchrone<!-- .element: class="fragment" -->
    * conservation du paradigme imperatif
    * pas de callback grâce à l'async / await
* Exemples : delay, r2dbc, Ktor<!-- .element: class="fragment" -->


### Ktor : Appel http en suspending
```kotlin
// Initialisation de HttpClient de la lib Ktor
val httpClient = HttpClient(CIO) {
    install(JsonFeature) {
        serializer = GsonSerializer()
    }
}
```

```kotlin
// suspend : la fonction peut rendre la main au thread en court si elle ne fait qu'attendre
suspend fun getHoroscope(date: String, sign: String): Horoscope {

    // httpClient.get est une "suspend function"
    return httpClient
            .get<Horoscope>("$baseUrl/horoscopes/$date/$sign") {}
}
```


### Solution asynchrone
```kotlin
// Version asynchrone
val results = arrayListOf<List<Horoscope>>()
runBlocking { // plus qu'un thread utilisé, c'est suffisant ;)
    val horoscopesDeferred = signs.map { sign ->
        async { getHoroscope(today, sign) }
    }
    horoscopesDeferred.forEach {
        horoscopes.add(it.await())
    }
}
println(results)
```
Temps d'exécution ≃ 220ms<!-- .element: class="fragment" -->