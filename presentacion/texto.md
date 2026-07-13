¿Cuanto tiene qué pensar un LLM para responder nuestras preguntas?

1. Por qué está pregunta?
2. Qué es un LLM y cómo lo representamos?
3. Cómo medimos pensar?


# Motivación transformers

IA generativa \
uso y adopción

Attn is all you need \
transformers son el building block

introduzco acá la idea de CoT prompting? \
creo que informalmente es el lugar


# Explicación del modelo

1. modelo autoregresivo
2. dos cajas
3. abro las cajas
\
\
comentarios sobre:
- repr finita
- un transf para cada input size
- budget

doy la idea de normalización acá?

    Por qué estudiar CoT y qué otros parámetros se pueden estudiar

# Clases CoT[T(n), d(n)]

1. La def
2. Para estudiar cómo se comportan estas clases probamos que están cerradas bajo operaciones booleanas.
    - Construcción para el not (no tan importante)
    - Construcción para el or (un poco más importante)

Vale la pena decir algo sobre que para hacer esto y para hablar de normalización definimos un montón de primitivas?


# Dónde se para CoT[T(n), d(n)] con respecto a las clases conocidas

## Intro a circuitos
- Definición de circuitos
- Size(T(n))
- NC^0 y AC^0
- Majority?
- P
- P/poly
- uniformidad?

Decir que en AC^0 podes: (las cosas que necesitamos después)
- Indexar
- Sumar



## Upper bound deterministico
Creo que no es tan interesante pero me parece que estaría bueno comentar como es que cada una de las piezas de un trasnformer se modela en AC^0

A mi me gusta el resultado de que log(n) pasos de cot no te sacan de AC^0. Pienso explicar la demo porque además es algo que nos trajo cosas interesantes después


## Lower bound
En cada paso de CoT computas una compuerta del circuito.
Está bueno comentar el truco de que el position encoding hace toda la magia.
Ver cómo representar esto visualmente.


# Los transformers no son deterministicos

Acá me gusta lo de poner una screenshot de chatgpt respondiendo distinto al mismo prompt.

## Nuestra construcción

# Clases RCoT[T(n), d(n)]
- Def
- La construcción es buena
    - Puede simular deterministicos
        - Decir que los normalizo y ya samplear y tomar máximo es lo mismo
    - Tiene reducción de error
        - Decir que hago lo mismo que en la disjunción de deterministicos pero muchas veces y tomo voto majoritario
    - Cerrado por op booleanas
        - Por completitud hay que mencionarlo pero solo voy a decir que es igual al otro caso


# Dónde se para RCoT[T(n), d(n)] con respecto a las clases conocidas

## Intro a circuitos probabilisticos y BPP
- Definición de circuitos probabilisticos
- BPAC^0
- BPSIZE
- BPP
- BPP/poly
- Uniformidad?

- BPAC^0[log(n)] = AC^0
- Relaciones con deterministicos? (P/poly = BPP/poly)


# Upper bound
Lo unico que cambia con el caso deterministico es el token selector.
Mostramos que esa pieza también se puede hacer en AC^0.
Para eso mejor mostramos que lo hacemos en AC^0 con O(1) bits de azar.

Recall:
- AC^0 puede indexar
- AC^0 puede hacer cuentas 

Entonces mostramos como definimos los rangos y cómo indexamos con una seed aleatoria.
Cuántos bits tiene la seed? gg


Cómo replicamos lo de los log(n) pasos en el setting probabilistico?
El problema: ahora hay más de una run consistente. 
Puede haber runs consistentes que acepten y otras que rechacen.
Necesitamos tomar majority.
Pero tiene promesa!


# Lower bound
Not so interesting jajaaj


# Cómo se relacionan los probabilisticos y los deterministicos entre si?

## RCoT[poly] = CoT[poly]

Ya vimos que CoT[T(n), d(n)] está en RCoT[T(n), d(n)] (por la simulación)

Pero también vale la vuelta!

CoT[poly] = P/poly = BPP/poly = RCoT[poly]

O sea que no pareciera dar una ventaja el azar en los transformers.

Este primer resultado da la idea de que para hacer complejidad que no es fine grained (no sé como se llama) pareciera no hacer falta estudiar los transformers probabilisticos.



## Uniformidad
En el area de la complejidad en general surgen criticas a la no uniformidad porque trae consigo problemas no computables.

Qué ocurre al restringir las familias de transformers a que sean P-uniformes?

P = (Uniform)CoT[poly]\
BPP = (Uniform)RCoT[poly]


P = BPP? pregunta abierta sin consenso pero hay acuerdo en que el azar da una ventaja polinomial ---> tenemos algún ejemplo?

- Future work: los transformers son muy finitos, el azar que tienen se debe poder computar. Estaría bueno tener una simulación de probabilisticos por deterministicos y ver su overhead.

## URCoT[poly] in CoT[poly]

Como en el teo de adleman, BPP subseteq P/poly.
La no uniformidad da suficiente poder como para comerse al azar también en los transformers



# Cierre
No sé cómo cerrar








