# Syntaxe


### Création d'instanc

  - pas de new
```kotlin
val rectangle = Rectangle(5.0, 2.0) //no 'new' keyword required
```

### Fonction avec retour

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}

//inline
fun sum(a: Int, b: Int) = a + b
```

- pas de ;
- Type déclaré après la variable
- Inférence du type de retour
- Paramètre obligatoirement immutable


### Fonction void

```kotlin
// Unit non obligatoire
fun sum(a: Int, b: Int): Unit {
    println(a + b)
}
```


### If
- Utilisable comme en Java
- Peut être considéré comme une expression

```kotlin
val i = if (a > b) a else b
```


### String template

```kotlin
var a = 1
val s1 = "a est $a" 

a = 2
val s2 = "${s1.replace("est", "était")}, et maintenant est $a"
```


### Vérification de type et cast automatique

```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj is String) {
        // Obj est un String dans ce scope
        return obj.length
    }

    // Obj est toujours de type Any
    return null
}
```


### for
- Parcours de collection

```kotlin
for (item in collection) print(item)
```
- Parcours de map

```kotlin
val s = HashMap<String, String>()
for ((k,v) in s) println("<$k, $v>")
```


### while

```kotlin
while (index < items.size) {
    println("item at $index is ${items[index]}")
    index++
}
```


### when
  - Expression donc le résultat peut être stocké 
```kotlin
when (Math.random().toInt()) {
    0, 1 -> print("x == 0 or x == 1")
    else -> print("otherwise")
}
```
  - Peut être utilisé comme un simple if else if
```kotlin
    when {
        x.isOdd() -> print("x is odd")
        x.isEven() -> print("x is even")
        else -> print("x is funny")
    }
```


### Ranges
  - Utilisable pour itéré
  
```kotlin
for (x in 1..5) {
    print(x)
}
```
  - Utilisable dans un if
  
```kotlin
if (x in 1..10) ...
```