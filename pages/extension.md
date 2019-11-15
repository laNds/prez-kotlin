## Extension


### Principe 

Etendre les fonctionnalités d'une classe
- sans héritage<!-- .element: class="fragment" -->
- sans usage du Decorator pattern<!-- .element: class="fragment" -->


### Extension function

```kotlin
fun MutableList<Int>.swap(index1: Int, index2: Int) {
    val tmp = this[index1] // this corresponds a la liste
    this[index1] = this[index2]
    this[index2] = tmp
}
//
val myList = mutableListOf(1,2,3,4,5,6)
myList.swap(1, 2)
```


### Extension properties

```kotlin
val <T> List<T>.lastIndex: Int 
    get() = size - 1
```


### Extension : résolution statique

```kotlin
open class Forme
class Rectangle: Forme()

fun Forme.getName() = "Forme"
fun Rectangle.getName() = "Rectangle"

fun printClassName(s: Forme) = println(s.getName())   

printClassName(Rectangle())
```

Forme <!-- .element: class="fragment" style="color: #238500"-->

Equivalent à la définition de méthodes statiques<!-- .element: class="fragment" -->

Note: Résolution statique donc pas au runtime


### Notation infix

```kotlin
infix fun Int.add(x: Int): Int = this + x

1 add 2
```

- Extension fonction ou une fonction membre <!-- .element: class="fragment"-->
- Un seul paramètre <!-- .element: class="fragment" -->
- Pas de varaargs <!-- .element: class="fragment"-->
- Pas de default value <!-- .element: class="fragment"-->

Note: On parle de notation Infix (possibilité d'ommettre le . et les parenthèse)
