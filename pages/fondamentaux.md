# Fondamentaux


### val & var

```kotlin
var mutable = 1 // équivaut à var mutable: Int = 1
mutable = 2

val nonmutable = 1
nonmutable = 0 // compilation error
```

Note: - type non explicite 
- type déclaré après le nom de la variable


### Instanciation de variable

```kotlin
val rectangle = Rectangle(5.0, 2.0) 
```
Note: Aucune nécessité du mot clef new


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

```kotlin
// Sur des collections

for (item in collection) print(item)

// Sur des Map 

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

```kotlin
// Expression donc le résultat peut être stocké

when (Math.random().toInt()) {
    0, 1 -> print("x == 0 or x == 1")
    else -> print("otherwise")
}

// Peut être utilisé comme un simple if else if

when {
    x.isOdd() -> print("x is odd")
    x.isEven() -> print("x is even")
    else -> print("x is funny")
}
```


### Ranges
  
```kotlin
// Utilisable pour itéré
for (x in 1..5) {
    print(x)
}

// Utilisable dans un if
if (x in 1..10) ...

// Utilisable dans un when
when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}

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
