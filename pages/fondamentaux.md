## Fondamentaux


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


### Tout est Objet

```kotlin
val cinq = 2.and(3)
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


### Déconstruction

```kotlin
val (validElements, nonValidElements) = 
            elements.partition { element.isValid }
```


### String template

```kotlin
var a = 1
val s1 = "a est $a" 

a = 2
val s2 = "${s1.replace("est", "était")}, et maintenant est $a"
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
