# plantuml-petrinets

> *"You love PlantUML and Petri Nets, and you want to draw Petri Nets in PlantUML? This is for you :heart:"*

This is a small includable plantuml library for defining [Petri Nets](https://en.wikipedia.org/wiki/Petri_net) in [PlantUML](https://github.com/plantuml).
This library provides the following macros:

* `Place(name,as="",marking="",style="")`  
    creates a place with the given name and an optional alias, marking or style.
* `VTrans(name,as="",style="")`  
    creates a vertical transition with the given name and an optional alias or style
* `HTrans(name,as="",style="")`  
    creates a vertical transition with the given name and an optional alias or style
* `Arc(source,target,label="")`  
    creates a down/right arc from source to target with an optional label
* `ArcUp(source,target,label="")` or `UpArc(source,target,label="")`
    creates a up/left arc from source to target with an optional label
* `ArcSame(source,target,label="")` or `SameArc(source,target,label="")`  
    creates an arc from source to target with an optional label not influencing the ranking of places and transitions
* `ArcNoRank(source,target,label="")`  
    creates an arc from source to target with an optional label not influencing the ranking of places and transitions
* `ArcHidden(source,target)`  
    creates an invisible arc from source to target affecting the ranking and placement of nodes
* `Token(number)`  
    creates a string of black circles as tokens
* `Sub(string)`  
    creates a string replacing any number to its subscript version, e.g. Sub("t1") yields "t₁".
* `LeftToRight()`  
    changes the diagram direction from top down to left to right

It permits the simple definition of Petri Nets.

> **Note:** This library currently falls back to graphviz, hence all style options are provided via graphviz options rather than plantuml options.

# Possible Use

To use the library copy the library from this repository into your local folder. Then you can include it into a PlantUML file and use the commands to create your petri net. Please note, that in order for this to work, the macros must be placed within a `digraph` block.

Here is an example of a basic Petri Net:

```plantuml
@startuml
!include ../plantuml-petrinets.iuml

digraph PTnet {

  LeftToRight()

  VTrans(Sub("t0"),t0)
  Place(Sub("s0"),s0,_marking=Token(2))
  VTrans(Sub("t1"),t1,_style="fillcolor=red")
  Place(Sub("s1"),s1)

  Arc(t0,s0)
  Arc(s0,t1,"2")
  Arc(t1,s1)
  ArcHidden(s0,s1)

}

@enduml
```

This Petri Net can be compiled as usual with Plantuml `java -jar plantuml.jar basic-petrinet.puml`.

![Basic petri net](examples/basic-petrinet.png)

You will find more examples in the [examples](examples/) folder.

> **Hint:** In the future there will be a release of the library, which can be included via an URL.

# Limitations

* Uses PlantUML's fallback to Graphviz
* It is currently impossible to color tokens
* Places and transitions can be styled both globally and individually. Please refere to the [Graphviz reference](https://graphviz.org/doc/info/attrs.html) for style options.
* If you want to contribute please read details on how the [PlantUML's preprocessor](https://plantuml.com/en/preprocessing) works

# Version

0.1.2
