# Coroutine


### Les coroutines, c'est quoi ?

* "Threads légers"<!-- .element: class="fragment" -->
    * concurrence gérée au niveau de Kotlin
    * utilisation de vrais threads au besoin
* Code élégant<!-- .element: class="fragment" -->
    * async / await
    * adieu les CompletableFuture !
* Programmation asynchrone<!-- .element: class="fragment" -->


### Ecriture d'une coroutine

* CoroutineScope<!-- .element: class="fragment" -->
    * Scope dans lequel on peut lancer des coroutines
* CoroutineContext<!-- .element: class="fragment" -->
    * Pools de threads
* async / await <!-- .element: class="fragment" -->

```kotlin
runBlocking(Dispatchers.Default /* CoroutineContext */) {
    // CorountineScope
    val one = async { maFonction1() }
    val two = async { maFonction2() }
    println(one.await() + two.await())
}
```
<!-- .element: class="fragment" -->


### Exemple dans la vraie vie

* Une API permet de récupérer l'horoscope pour un jour et un signe donnés
    ```sh
    GET /horoscopes/$date/$sign
    ```
    <!-- .element: class="fragment" -->
    ```JSON
    {
    "id": "5dc3a4db7c99a330508683d7",
    "sign": "Cancer",
    "description": "Une bonne surprise est possible, ...",
    "date": "2019-11-07",
    "periode": "du 22 juin au 22 juillet"
    }
    ```
<!-- .element: class="fragment" -->
* Objectif : Récupérer tous les horoscopes du jour en appelant l'API pour chaque signe avec la date du jour<!-- .element: class="fragment" style="color: #e73e01" -->


### Première étape...

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


### Solution séquentielle
```kotlin 
// pour chaque signe on fait l'appel à l'API
// on obtient une liste contenant tous les horoscopes du jour  
val results = signs.map { sign -> getHoroscope(today, sign) }
println(results)
```

<img data-src="/lib/img/synchrone_way.png" style="border: none"><!-- .element: class="fragment" -->

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
<img data-src="/lib/img/parallel_way.png" style="border: none"><!-- .element: class="fragment" -->


## Programmation asynchrone


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


<img data-src="/lib/img/asynchrone.png" style="border: none">

* Sur l'appel GET, la fonction est "suspendue" le temps d'avoir la réponse du serveur
* le thread principal est débloqué pour exécuter une autre fonction
* Le temps où le thread ne fait rien d'autre qu'attendre est réduit


### Asynchrone avec plusieurs Threads

```kotlin
newFixedThreadPoolContext(2, "my-context").use {
        runBlocking(it) { // utilisation d'un pool de 2 threads
            // appels async...      
        }
 }
```
<!-- .element: class="fragment" -->
<img data-src="/lib/img/asynchrone_pool.png" style="border: none"><!-- .element: class="fragment" -->


### Coroutines : ce qu'il faut retenir

* synthaxe simple et claire<!-- .element: class="fragment" -->
* outil puissant<!-- .element: class="fragment" -->
    * parallélisation de code bloquant
    * Programmation asynchrone
    * même synthaxe pour les 2