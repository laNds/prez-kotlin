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


### Autres

- tailrec : Fonction ouverte a la recursion
- open: Fonction pouvant être overridé
- override: Fonction overridé

