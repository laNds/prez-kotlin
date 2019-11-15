## Classe


### Instanciation des classes
```kotlin
class Chat(val nom: String, val race: String) {
    private var patte = 0
    constructor(nom: String): this(nom, "Européen") {
        println("Constructeur Auxiliaire")
    }
}
Chat("Minou") // Constructeur auxiliaire
val chat = Chat("Ronron", "Chartreux")
chat.nom = "RonRonRon" // impossible car val utilisé
```


### Object
Equivalence au Singleton
```kotlin
object Math {
    fun moyenne(valeurs: Array<Int>): Double {
        if (valeurs.isEmpty()) return 0.0
        return (valeurs.sum() / valeurs.size).toDouble()
    }
}
println(Math.moyenne(arrayOf(1,2,3,4))
```


### Companion object
Equivalent du static Java
```kotlin
class Chat(val nom: String, val race) {
    companion object {
        const val RACE_PAR_DEFAUT = "Européen" 
    }
    constructor(nom: String): this(nom, RACE_PAR_DEFAUT) {
        println("Constructeur Auxiliaire")
    }
}
```


### Implémentation d'interface
```kotlin
class Chat(val nom: String, val race: String): Serializable
```


### Héritage
```kotlin
open class Vehicule(nombreRoues : Int, nombrePlaces: Int)
class Velo : Vehicule(2,1)
class Automobile(nombreRoues: Int, nombrePlaces: Int) : 
            Vehicule(nombreRoues, nombrePlaces)
```


### Data class
#### Java
```java
class MonObject {
    private int id;
    private String nom;
    
    // Setter ... 
    // Getter
    // toString(), hashcode(), equals
}
```
#### Kotlin
```kotlin
data class MonObjet(var id: Int, var nom: String)
```

Note: - var implique setter 


### Surcharge d'opérateurs
Liste des opérateurs surchargeables limitée
```kotlin
data class Counter(val dayIndex: Int) {
    operator fun plus(increment: Int): Counter {
        return Counter(dayIndex + increment)
    }
}
val counter = Counter(1)
println(counter + 4)
```
