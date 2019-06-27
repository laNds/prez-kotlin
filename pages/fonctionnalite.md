# Fonctionnalité


### val & var

```kotlin
var mutable = 1
mutable = 2

val nonmutable = 1
nonmutable = 0 // compilation error
```

Note: - type non explicite 
- type déclaré après le nom de la variable


### Data class
Java : 
```java
class MonObject {
    private int id;
    private String nom;
    
    // Setter ... 
    // Getter
    // toString(), hashcode(), equals
}
```
kt
```kotlin
data class MonObjet(var id: Int, var nom: String)
```

Note: - Obtention presque similaire avec lombok mais avec un coût supplémentaire


### Data class
