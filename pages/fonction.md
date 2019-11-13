## Fonction


### Déclaration
#### Avec retour

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}

//inline
fun sum(a: Int, b: Int) = a + b
```

#### Sans retour

```kotlin
// Unit non obligatoire
fun sum(a: Int, b: Int): Unit {
    println(a + b)
}
```

Note: - Type déclaré après la variable
- Inférence du type de retour
- Paramètre obligatoirement immutable


### Argument par défaut

```kotlin
fun sum(a: Int = 0, b: Int = 0): Int {
    return a + b
}
```


### Named Arguments

```kotlin
fun doSomething(str: String, wordSeparator: Char): Unit {}

doSomething("test", '_')
doSomething(str = "test", wordSeparator = '_')
doSomething(wordSeparator = '_', str = "test")
```


### Varargs

```kotlin
fun <T> asList(vararg ts: T): List<T>

asList(1,2,3,4,5,6)
```


### Surcharge d'opérateur
* Liste des opérateurs surchargeable limitée
```kotlin
data class Counter(val dayIndex: Int) {
    operator fun plus(increment: Int): Counter {
        return Counter(dayIndex + increment)
    }
}
val counter = Counter(1)
println(counter1 + 4)
```


### Lambda avec un seul argument

it, nom de l'élement parcouru
```kotlin
val result = listOf(1, 2, 3, 4, 5) 
  .map { it * it } 
  .filter { it < 10 }
  //filter(1) { it < 10 } 
  .first()
```


### Autres

- tailrec : Fonction ouverte a la recursion
- open: Fonction pouvant être overridé
- override: Fonction overridé

