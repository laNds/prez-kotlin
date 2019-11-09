# Null-safety


### Principes généraux

- Intégré directement au langage grâce au "?"
- Porté par le type de l'objet manipulé
```kotlin
var a = "abc"
a = null // compile error
//
var b: String? = "abc"
println(b.length) // compile error car risque de NPE
b = null // Ok
```
- Peut être renvoyé par une fonction
```kotlin
fun length(b: String?): Int? =  b?.length
```


### Safe calls

- Opérateur ? permet de faire des appels sécurisé

```kotlin
var b: String? = "abc"
println(b?.length) // Ok, affichera la valeur sinon null
```


### Elvis operator

```kotlin
val l = if (b != null) b.length else -1
```
#### équivaut 
```kotlin
val a = b?.length ?: -1

```


### Not null assertions (!!)
- Force la non nullité de la variable
- Utile dans les cas d'utilisation d'une librairie Java pour assurer qu'une valeur est non null
- Risque de NPE si mal utilisé

```kotlin
val l = b!!.length // Peut throw une NPE si b était réelement nulle
```