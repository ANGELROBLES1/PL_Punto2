# Implementación y pruebas del lenguaje (Punto 2)
## Descripción

En este punto se implementa la gramática diseñada previamente utilizando ANTLR, con el objetivo de construir un analizador capaz de validar instrucciones del lenguaje CRUD propuesto.

A diferencia de una validación básica, se incorpora un sistema de detección de errores que permite identificar fallos sintácticos indicando su ubicación (línea y columna), simulando el comportamiento de un compilador real.

## Archivos utilizados
- ANT.g4: Definición de la gramática
- main.py: Ejecución del parser y manejo de errores
- ejemplos.txt: Casos de prueba (correctos e incorrectos)

## Archivos generados automáticamente:

- ANTLexer.py
- ANTParser.py
- ANTListener.py
- 
## Proceso de implementación

1. Generación del parser
Se utilizó ANTLR para generar el analizador léxico y sintáctico:
``
antlr4 -Dlanguage=Python3 ANT.g4
``

2. Ejecución del programa
``
python3 main.py
``

Se diseñaron pruebas con dos enfoques:

Validación de instrucciones correctas
Pruebas de robustez introduciendo errores intencionales
Pruebas realizadas

1. Ejecución con entradas válidas

Entrada:

PUSH usuarios WITH [ nombre => "Angel", edad => 20 ]
PULL usuarios FILTER edad > 18

Salida:

Analizando linea 1: PUSH usuarios WITH [ nombre => "Agel", edad => 20 ]

Analizando linea 2: PULL usuarios FILTER edad > 18

Esto indica que el parser acepta correctamente la estructura del lenguaje.

2. Pruebas con errores sintácticos

Se introdujeron errores para evaluar la robustez del sistema.

Error 1: estructura inválida

Entrada:

PUSH usuarios WITH nombre => "Harry"

Salida esperada:

Linea X, Columna Y -> ERROR: mismatched input ...

Causa: falta de delimitadores [ ].

Error 2: operador no reconocido

Entrada:

PULL usuarios FILTER edad <> 20

Causa: el operador <> no está definido en la gramática.

Error 3: valor faltante

Entrada:

SHIFT usuarios REPLACE [ edad => ] FILTER nombre == "Angel"

Causa: ausencia de valor en la asignación.

Error 4: palabra clave incorrecta

Entrada:

PSUH usuarios WITH [ nombre => "Angel" ]

Causa: error léxico en la palabra reservada (PUSH mal escrita).

Error 5: cadena no cerrada

Entrada:

PUSH usuarios WITH [ nombre => "Harry ]

Causa: string sin cierre de comillas.

Error 6: instrucción incompleta

Entrada:

DROP usuarios FILTER

Causa: falta la condición.

Análisis de resultados

El sistema implementado permite:

Detectar errores léxicos y sintácticos
Identificar la posición exacta del error
Evaluar múltiples instrucciones en un solo archivo
Validar la robustez del lenguaje frente a entradas inválidas

<img width="817" height="394" alt="image" src="https://github.com/user-attachments/assets/64182854-a170-47bf-bc6f-a288884ad9f5" />
