## Structures de contrôles


### If
- Utilisable comme en Java
- Peut être considéré comme une expression

```kotlin
val i = if (a > b) a else b
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
