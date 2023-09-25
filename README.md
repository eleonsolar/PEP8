# PEP 8 - Guía de estilo para código Python

La PEP8 es una guía que indica las convenciones estilísticas a seguir para escribir código Python. Se trata de un conjunto de recomendaciones cuyo objetivo es ayudar a escribir código más legible y abarca desde cómo nombrar variables, al número máximo de caracteres que una línea debe tener.

Guía oficial [PEP8](https://peps.python.org/pep-0008/) 

**Autor:** Guido van Rossum <guido at python.org>, Barry Warsaw <barry at python.org>, Nick Coghlan <ncoghlan at gmail.com>
**Estatus:** Active
**Tipo:** Process
**Creado:** 05-Jul-2001
**Historial del post:** 05-Jul-2001, 01-Aug-2013

**Tabla de contenido**

- [Introducción](#id1)
- [La insensata coherencia es el duende de las mentes pequeñas](#id2)
- [Disposición del código](#id3)
  - [Identación](#id4)
  - [¿Tabulaciones o espacios?](#id5)
  - [Longitud máxima de línea](#id6)
  - [¿Debe haber un salto de línea antes o después de un operador binario?](#id7)
  - [Líneas en blanco](#id8)
  - [Codificación del fichero fuente](#id9)
  - [Importaciones](#id10)
  - [Nombres de Dunder a nivel de módulo](#id11)
- [Comillas](#id12)
- [Espacios en blanco en expresiones y sentencias](#id13)
  - [Las manías](#id14)
  - [Otras recomendaciones](#id15)
- [Cuándo usar comas finales](#id16)
- [Comentarios](#id17)
  - [Comentarios en bloque](#id18)
  - [Comentarios en línea](#id19)
  - [Cadenas de documentación](#id20)
- [Convenciones de nomenclatura](#id21)
  - [Principio de anulación](#id22)
  - [Descriptivo: Estilos de denominación](#id23)
  - [Prescriptivo: Convenciones de denominación](#id24)
    - [Nombres que deben evitarse](#id25)
    - [Compatibilidad ASCII](#id26)
    - [Nombres de paquetes y módulos](#id27)
    - [Nombres de clases](#id28)
    - [Nombres de variables de tipo](#id29)
    - [Nombres de excepción](#id30)
    - [Nombres de variables globales](#id31)
    - [Nombres de funciones y variables](#id32)
    - [Argumentos de funciones y métodos](#id33)
    - [Nombres de métodos y variables de instancia](#id34)
    - [Constantes](#id35)
    - [Diseño para la Herencia](#id36)
  - [Interfaces públicas e internas](#id37)
- [Recomendaciones de programación](#id38)
  - [Anotaciones de funciones](#id39)
  - [Anotaciones de variables](#id40)
- [Referencias](#id41)
- [Copyright](#id42)
  
  
## Introducción<a name="id1"></a>  
  
Este documento proporciona convenciones de codificación para el código Python que comprende la biblioteca estándar en la distribución principal de Python. Por favor, consulta el PEP informativo complementario que describe las directrices de estilo para el código C en la implementación C de Python.

Este documento y el PEP 257 (Convenciones Docstring) fueron adaptados del ensayo original de Guido sobre la Guía de Estilo de Python, con algunas adiciones de la guía de estilo de Barry [2].

Esta guía de estilo evoluciona con el tiempo a medida que se identifican convenciones adicionales y las convenciones anteriores quedan obsoletas por los cambios en el propio lenguaje.

Muchos proyectos tienen sus propias guías de estilo de codificación. En caso de conflicto, estas guías específicas del proyecto tienen prioridad para ese proyecto.

## La insensata coherencia es el duende de las mentes pequeñas<a name="id2"></a>

Una de las ideas clave de Guido es que el código se lee mucho más a menudo de lo que se escribe. Las directrices proporcionadas aquí pretenden mejorar la legibilidad del código y hacerlo consistente en todo el amplio espectro de código Python. Como dice PEP 20, "La legibilidad cuenta".

Una guía de estilo trata de la consistencia. La consistencia con esta guía de estilo es importante. La consistencia dentro de un proyecto es más importante. La consistencia dentro de un módulo o función es lo más importante.

Sin embargo, hay que saber cuándo ser incoherente: a veces, las recomendaciones de la guía de estilo no son aplicables. En caso de duda, utilice su buen juicio. Mire otros ejemplos y decida qué le parece mejor. Y no dude en preguntar.

En particular: ¡no rompas la compatibilidad con versiones anteriores sólo para cumplir con este PEP!

Otras buenas razones para ignorar una directriz concreta:

  1. Cuando aplicar la directriz haría el código menos legible, incluso para alguien acostumbrado a leer código que sigue esta PEP.
  2. Para ser consistente con el código circundante que también la rompe (tal vez por razones históricas) - aunque esta es también una oportunidad para limpiar el desorden de alguien más (en el verdadero estilo XP).
  3. Porque el código en cuestión es anterior a la introducción de la directriz y no hay ninguna otra razón para modificar ese código.
  4. Cuando el código necesita seguir siendo compatible con versiones antiguas de Python que no soportan la característica recomendada por la guía de estilo.
  
## Disposición del código<a name="id3"></a>

### Identación<a name="id4"></a>

Usa 4 espacios por nivel de identación.

Las líneas de continuación deben alinear los elementos envueltos verticalmente usando la unión de líneas implícita de Python dentro de paréntesis, corchetes y llaves, o usando una hanging indent [1]. Cuando se utiliza una hanging indent se debe tener en cuenta lo siguiente; no debe haber argumentos en la primera línea y se debe utilizar una identación adicional para distinguirse claramente como línea de continuación:

```
# Correct:

# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# Add 4 spaces (an extra level of indentation) to distinguish arguments from the rest.
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# Hanging indents should add a level.
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
    

# Wrong:

# Arguments on first line forbidden when not using vertical alignment.
foo = long_function_name(var_one, var_two,
    var_three, var_four)

# Further indentation required as indentation is not distinguishable.
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
```

La regla de los 4 espacios es opcional para las líneas de continuación.

Opcional:

```
# Hanging indents *may* be indented to other than 4 spaces.
foo = long_function_name(
  var_one, var_two,
  var_three, var_four)
```

Cuando la parte condicional de una sentencia if es lo suficientemente larga como para requerir que se escriba en varias líneas, vale la pena señalar que la combinación de una palabra clave de dos caracteres (es decir, if), más un solo espacio, más un paréntesis de apertura crea una identación natural de 4 espacios para las líneas siguientes de la condicional multilínea. Esto puede producir un conflicto visual con el conjunto de código sangrado anidado dentro de la declaración if, que también estaría identado naturalmente a 4 espacios. Este PEP no toma una posición explícita sobre cómo (o si) distinguir visualmente tales líneas condicionales del conjunto anidado dentro de la declaración if. Las opciones aceptables en esta situación incluyen, pero no se limitan a:

```
# No extra indentation.
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# Add a comment, which will provide some distinction in editors
# supporting syntax highlighting.
if (this_is_one_thing and
    that_is_another_thing):
    # Since both conditions are true, we can frobnicate.
    do_something()

# Add some extra indentation on the conditional continuation line.
if (this_is_one_thing
        and that_is_another_thing):
    do_something()
```

(Véase también más adelante la discusión sobre si romper antes o después de los operadores binarios).

El llaves/corchete/paréntesis de cierre en sentencias multilínea puede alinearse bajo el primer carácter no espacio en blanco de la última línea de la lista, como en:

```
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )
```

o puede alinearse bajo el primer carácter de la línea que inicia la construcción multilínea, como en:

```
my_list = [
    1, 2, 3,
    4, 5, 6,
]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
)
```

### ¿Tabulaciones o espacios?<a name="id5"></a>

Los espacios son el método de sangría preferido.

Los tabuladores deben usarse únicamente para mantener la coherencia con el código que ya está sangrado con tabuladores.

Python no permite mezclar tabuladores y espacios para la sangría.

### Longitud máxima de línea<a name="id6"></a>

Limite todas las líneas a un máximo de 79 caracteres.

Para bloques de texto largos y fluidos con menos restricciones estructurales (docstrings o comentarios), la longitud de línea debe limitarse a 72 caracteres.

Limitar la anchura de la ventana del editor hace posible tener varios archivos abiertos uno al lado del otro, y funciona bien cuando se utilizan herramientas de revisión de código que presentan las dos versiones en columnas adyacentes.

El envoltorio por defecto en la mayoría de las herramientas interrumpe la estructura visual del código, haciéndolo más difícil de entender. Los límites se eligen para evitar el ajuste en editores con un ancho de ventana de 80, incluso si la herramienta coloca un glifo marcador en la columna final al ajustar las líneas. Es posible que algunas herramientas web no ofrezcan ningún ajuste de línea dinámico.

Algunos equipos prefieren una longitud de línea mayor. Para el código mantenido exclusiva o principalmente por un equipo que puede llegar a un acuerdo sobre este tema, está bien aumentar el límite de longitud de línea hasta 99 caracteres, siempre que los comentarios y docstrings se sigan ajustando a 72 caracteres.

La biblioteca estándar de Python es conservadora y exige limitar las líneas a 79 caracteres (y los docstrings/comentarios a 72).

La forma preferida de envolver líneas largas es usar la continuación de línea implícita de Python dentro de paréntesis, corchetes y llaves. Las líneas largas pueden dividirse en varias líneas encerrando las expresiones entre paréntesis. Éstos deben usarse preferentemente a las barras invertidas para la continuación de línea.

No obstante, la barra invertida puede ser adecuada en algunos casos. Por ejemplo, antes de Python 3.10, las expresiones largas y múltiples con no podían usar la continuación implícita, por lo que las barras invertidas eran aceptables para ese caso:

```
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())
```

(Véase la discusión anterior sobre las sentencias if multilínea para más información sobre la sangría de dichas sentencias with multilínea).

Otro caso es el de las sentencias assert.

Asegúrese de aplicar la sangría adecuada a la línea de continuación. 

### ¿Debe haber un salto de línea antes o después de un operador binario?<a name="id7"></a>

Durante décadas, el estilo recomendado era hacer una pausa después de los operadores binarios. Pero esto puede perjudicar la legibilidad de dos maneras: los operadores tienden a dispersarse por diferentes columnas de la pantalla, y cada operador se aleja de su operando y se sitúa en la línea anterior. En este caso, el ojo tiene que hacer un trabajo extra para saber qué elementos se suman y cuáles se restan:

```
# Wrong:
# operators sit far away from their operands
income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction -
          student_loan_interest)
```

Para resolver este problema de legibilidad, los matemáticos y sus editores siguen la convención contraria. Donald Knuth explica la regla tradicional en su serie Computers and Typesetting: "Aunque las fórmulas dentro de un párrafo siempre se rompen después de las operaciones y relaciones binarias, las fórmulas mostradas siempre se rompen antes de las operaciones binarias" [3].

Seguir la tradición de las matemáticas suele dar como resultado un código más legible:

```
# Correct:
# easy to match operators with operands
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```

En código Python, es permisible romper antes o después de un operador binario, siempre que la convención sea consistente localmente. Para código nuevo se sugiere el estilo de Knuth.

### Líneas en blanco<a name="id8"></a>

Rodee las definiciones de funciones y clases de nivel superior con dos líneas en blanco.

Las definiciones de métodos dentro de una clase se rodean de una sola línea en blanco.

Pueden utilizarse líneas en blanco adicionales (con moderación) para separar grupos de funciones relacionadas. Pueden omitirse las líneas en blanco entre un grupo de funciones relacionadas (por ejemplo, un conjunto de implementaciones ficticias).

Use líneas en blanco en funciones, con moderación, para indicar secciones lógicas.

Python acepta el carácter de avance de página control-L (es decir, ^L) como espacio en blanco; muchas herramientas tratan estos caracteres como separadores de página, por lo que puede utilizarlos para separar páginas de secciones relacionadas de su archivo. Tenga en cuenta que algunos editores y visualizadores de código basados en web pueden no reconocer control-L como un carácter de alimentación de formulario y mostrarán otro glifo en su lugar.

### Codificación del archivo fuente<a name="id9"></a>

El código en el núcleo de la distribución de Python debería usar siempre UTF-8, y no debería tener una declaración de codificación.

En la biblioteca estándar, las codificaciones que no sean UTF-8 deben usarse sólo con fines de prueba. Use caracteres no ASCII con moderación, preferiblemente sólo para denotar lugares y nombres humanos. Si utiliza caracteres no ASCII como datos, evite los caracteres Unicode ruidosos como z̯̯͡a̧͎̺l̡͓̫g̹̲o̡̼̘ y las marcas de orden de bytes.

Todos los identificadores en la biblioteca estándar de Python DEBEN usar identificadores sólo ASCII, y DEBERÍAN usar palabras en inglés siempre que sea factible (en muchos casos, se usan abreviaturas y términos técnicos que no están en inglés).

Se anima a los proyectos de código abierto con una audiencia global a adoptar una política similar.

### Importaciones<a name="id10"></a>

- Por lo general, las importaciones deben ir en líneas separadas:

```
# Correct:
import os
import sys
```
```
# Wrong:
import sys, os
```
Sin embargo, está bien decir esto:

```
# Correct:
from subprocess import Popen, PIPE
```

- Las importaciones se colocan siempre al principio del fichero, justo después de los comentarios y docstrings del módulo, y antes de las constantes y globales del módulo.

Las importaciones deben agruparse en el siguiente orden:

  - Importaciones de la biblioteca estándar.
  - Importaciones de terceros relacionadas.
  - Importaciones específicas de la aplicación/biblioteca local.
  
Debe poner una línea en blanco entre cada grupo de importaciones.

- Se recomiendan las importaciones absolutas, ya que suelen ser más legibles y tienden a comportarse mejor (o al menos dan mejores mensajes de error) si el sistema de importación está mal configurado (como cuando un directorio dentro de un paquete acaba en sys.path):

```
import mypkg.sibling
from mypkg import sibling
from mypkg.sibling import example
```

Sin embargo, las importaciones relativas explícitas son una alternativa aceptable a las importaciones absolutas, especialmente cuando se trata de diseños de paquetes complejos en los que el uso de importaciones absolutas sería innecesariamente rebuscada:

```
from . import sibling
from .sibling import example
```

El código de la biblioteca estándar debe evitar las disposiciones complejas de paquetes y utilizar siempre importaciones absolutas.

- Cuando se importa una clase de un módulo que contiene clases, normalmente está bien deletrear esto:

```
from myclass import MyClass
from foo.bar.yourclass import YourClass
```

Si esta ortografía provoca conflictos de nombres locales, escríbalos explícitamente:

```
import myclass
import foo.bar.yourclass
```

y usar “myclass.MyClass” y “foo.bar.yourclass.YourClass”.

- Deben evitarse las importaciones comodín (from <module> import *), ya que no dejan claro qué nombres están presentes en el espacio de nombres, confundiendo tanto a los lectores como a muchas herramientas automatizadas. Hay un caso de uso defendible para una importación comodín, que es volver a publicar una interfaz interna como parte de una API pública (por ejemplo, sobrescribir una implementación pura de Python de una interfaz con las definiciones de un módulo acelerador opcional y no se sabe de antemano exactamente qué definiciones se sobrescribirán).

Cuando se republican nombres de esta forma, se siguen aplicando las directrices que se indican a continuación en relación con las interfaces públicas e internas.


### Nombres de "Dunder" a nivel de módulo<a name="id11"></a>

Los "dunders" a nivel de módulo (es decir, nombres con dos guiones bajos iniciales y dos finales) como __all__, __author__, __version__, etc. deben colocarse después del docstring del módulo pero antes de cualquier sentencia import excepto de las importaciones __future__. Python obliga a que las importaciones futuras aparezcan en el módulo antes que cualquier otro código excepto las cadenas de documentación:

```
"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```

## Comillas<a name="id12"></a>

En Python, las cadenas entre comillas simples y las cadenas entre comillas dobles son iguales. Este PEP no hace ninguna recomendación al respecto. Elige una regla y cíñete a ella. Sin embargo, cuando una cadena contiene caracteres de comillas simples o dobles, use la otra para evitar barras invertidas en la cadena. Mejora la legibilidad.

Para cadenas con comillas triples, use siempre comillas dobles para ser consistente con la convención docstring en PEP 257.}

## Espacios en blanco en expresiones y sentencias<a name="id13"></a>

### Las manías<a name="id14"></a>

Evite los espacios en blanco en las siguientes situaciones:

- Inmediatamente dentro de paréntesis, corchetes o llaves:

```
# Correct:
spam(ham[1], {eggs: 2})
```
```
# Wrong:
spam( ham[ 1 ], { eggs: 2 } )
```

- Between a trailing comma and a following close parenthesis:

```
# Correct:
foo = (0,)
```
```
# Wrong:
bar = (0, )
```

- Immediately before a comma, semicolon, or colon:

```
# Correct:
if x == 4: print(x, y); x, y = y, x
```
```
# Wrong:
if x == 4 : print(x , y) ; x , y = y , x
```

- Sin embargo, en un slice los dos puntos actúan como un operador binario, y deben tener cantidades iguales a ambos lados (tratándolo como el operador de menor prioridad). En un slice extendido, ambos dos puntos deben tener la misma cantidad de espacio aplicada. Excepción: cuando se omite un parámetro de rebanada, se omite el espacio:

```
# Correct:
ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
ham[lower + offset : upper + offset]
```
```
# Wrong:
ham[lower + offset:upper + offset]
ham[1: 9], ham[1 :9], ham[1:9 :3]
ham[lower : : step]
ham[ : upper]
```

- Inmediatamente antes del paréntesis abierto que inicia la lista de argumentos de una llamada a función:

```
# Correct:
spam(1)
```
```
# Wrong:
spam (1)
```

- Inmediatamente antes del paréntesis abierto que inicia una indexación o un corte:

```
# Correct:
dct['key'] = lst[index]
```
```
# Wrong:
dct ['key'] = lst [index]
```

- Más de un espacio alrededor de un operador de asignación (u otro) para alinearlo con otro:

```
# Correct:
x = 1
y = 2
long_variable = 3
```
```
# Wrong:
x             = 1
y             = 2
long_variable = 3
```

### Otras recomendaciones:<a name="id15"></a>

- Evite los espacios en blanco al final del texto. Como suele ser invisible, puede ser confuso: por ejemplo, una barra invertida seguida de un espacio y una nueva línea no cuenta como marcador de continuación de línea. Algunos editores no lo preservan y muchos proyectos (como el propio CPython) tienen ganchos pre-commit que lo rechazan.

- Rodee siempre estos operadores binarios con un espacio a cada lado: asignación (=), asignación aumentada (+=, -= etc.), comparaciones (==, <, >, !=, <>, <=, >=, in, not in, is, is not), booleanos (and, or, not).

- Si se utilizan operadores con distintas prioridades, considere la posibilidad de añadir espacios en blanco alrededor de los operadores de menor prioridad. Siga su propio criterio; no obstante, no utilice nunca más de un espacio y deje siempre la misma cantidad de espacio en blanco a ambos lados de un operador binario:

```
# Correct:
i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)
```
```
# Wrong:
i=i+1
submitted +=1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)
```

- Las anotaciones de función deben usar las reglas normales para los dos puntos y siempre deben tener espacios alrededor de la flecha -> si está presente. (Para más información sobre anotaciones de funciones, véase Anotaciones de funciones):

```
# Correct:
def munge(input: AnyStr): ...
def munge() -> PosInt: ...
```
```
# Wrong:
def munge(input:AnyStr): ...
def munge()->PosInt: ...
```

- No utilice espacios alrededor del signo = cuando se utilice para indicar un argumento de palabra clave, o cuando se utilice para indicar un valor por defecto para un parámetro de función no anotado:

```
# Correct:
def complex(real, imag=0.0):
    return magic(r=real, i=imag)
```
```    
# Wrong:
def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```

Sin embargo, al combinar una anotación de argumento con un valor por defecto, utilice espacios alrededor del signo = :

```
# Correct:
def munge(sep: AnyStr = None): ...
def munge(input: AnyStr, sep: AnyStr = None, limit=1000): ...   
```
```
# Wrong:
def munge(input: AnyStr=None): ...
def munge(input: AnyStr, limit = 1000): ...
```

- En general, se desaconsejan las sentencias compuestas (varias sentencias en la misma línea):

```
# Correct:
if foo == 'blah':
    do_blah_thing()
do_one()
do_two()
do_three()
```

Mejor no:

```
# Wrong:
if foo == 'blah': do_blah_thing()
do_one(); do_two(); do_three()
```

- Aunque a veces está bien poner un if/for/while con un pequeño cuerpo en la misma línea, nunca lo hagas para sentencias con varias cláusulas. Evite también doblar líneas tan largas.

Mejor no:
```
# Wrong:
if foo == 'blah': do_blah_thing()
for x in lst: total += x
while t < 10: t = delay()
```

Definitivamente no:

```
# Wrong:
if foo == 'blah': do_blah_thing()
else: do_non_blah_thing()

try: something()
finally: cleanup()

do_one(); do_two(); do_three(long, argument,
                             list, like, this)

if foo == 'blah': one(); two(); three()
```

## Cuándo usar comas finales<a name="id16"></a>

Las comas finales suelen ser opcionales, pero son obligatorias cuando se trata de una tupla de un solo elemento. Para mayor claridad, se recomienda rodear estas últimas de paréntesis (técnicamente redundantes):

```
# Correct:
FILES = ('setup.cfg',)
```
```
# Wrong:
FILES = 'setup.cfg',
```

Cuando las comas finales son redundantes, suelen ser útiles cuando se utiliza un sistema de control de versiones, cuando se espera que una lista de valores, argumentos o elementos importados se amplíe con el tiempo. El patrón es poner cada valor (etc.) en una línea por sí mismo, añadiendo siempre una coma al final, y añadir el paréntesis/corche/corchete de cierre en la línea siguiente. Sin embargo, no tiene sentido poner una coma final en la misma línea que el delimitador de cierre (excepto en el caso anterior de las tuplas singleton):

```
# Correct:
FILES = [
    'setup.cfg',
    'tox.ini',
    ]
initialize(FILES,
           error=True,
           )
```
```
# Wrong:
FILES = ['setup.cfg', 'tox.ini',]
initialize(FILES, error=True,)
```

## Comentarios<a name="id17"></a>

Los comentarios que contradicen el código son peores que la ausencia de comentarios. Es prioritario mantener los comentarios actualizados cuando cambie el código.

Los comentarios deben ser frases completas. La primera palabra debe ir en mayúscula, a menos que se trate de un identificador que empiece por minúscula (¡nunca cambies las mayúsculas de los identificadores!).

Los comentarios en bloque suelen consistir en uno o varios párrafos formados por frases completas, cada una de las cuales termina en un punto.

Debe utilizar uno o dos espacios después del punto final en los comentarios de varias frases, excepto después de la frase final.

Asegúrate de que tus comentarios sean claros y fácilmente comprensibles para otros hablantes de la lengua en la que escribes.

Codificadores de Python de países de habla no inglesa: por favor, escriba sus comentarios en inglés, a menos que esté 120% seguro de que el código nunca será leído por personas que no hablen su idioma.	

### Comentarios en bloque<a name="id18"></a>
  
Por lo general, los comentarios de bloque se aplican a parte (o a todo) el código que les sigue, y están sangrados al mismo nivel que ese código. Cada línea de un comentario de bloque comienza con un # y un espacio (a menos que se trate de texto sangrado dentro del comentario).

Los párrafos dentro de un comentario de bloque están separados por una línea que contiene un solo #.

### Comentarios en línea<a name="id19"></a>

Utilice los comentarios en línea con moderación.

Un comentario en línea es un comentario en la misma línea que una sentencia. Los comentarios en línea deben estar separados de la sentencia por al menos dos espacios. Deben comenzar con # y un espacio.

Los comentarios en línea son innecesarios y, de hecho, distraen la atención si afirman lo obvio. No lo haga:

```
x = x + 1                 # Increment x
```

Pero a veces, esto es útil:

```
x = x + 1                 # Compensate for border
```

### Cadenas de documentación<a name="id20"></a>

Las convenciones para escribir buenas cadenas de documentación (también conocidas como "docstrings") están inmortalizadas en PEP 257.

- Escribe docstrings para todos los módulos, funciones, clases y métodos públicos. Los docstrings no son necesarios para los métodos no públicos, pero deberías tener un comentario que describa lo que hace el método. Este comentario debe aparecer después de la línea def.
- PEP 257 describe buenas convenciones de docstrings. Tenga en cuenta que lo más importante es que el """ que termina un docstring multilínea debe estar en una línea por sí mismo:

```
"""Return a foobang

Optional plotz says to frobnicate the bizbaz first.
"""
```

- En los documentos de una línea, mantenga el """ de cierre en la misma línea:

```
"""Return an ex-parrot."""
```

## Convenciones de nomenclatura<a name="id21"></a>

Las convenciones de nomenclatura de las bibliotecas de Python son un poco confusas, así que nunca conseguiremos que esto sea completamente consistente - no obstante, aquí están los estándares de nomenclatura actualmente recomendados. Los nuevos módulos y paquetes (incluyendo frameworks de terceros) deberían escribirse siguiendo estos estándares, pero cuando una biblioteca existente tiene un estilo diferente, se prefiere la consistencia interna.

### Principio de anulación<a name="id22"></a>

Los nombres que son visibles para el usuario como partes públicas de la API deben seguir convenciones que reflejen el uso más que la implementación.

### Descriptivo: Estilos de denominación<a name="id23"></a>

Hay muchos estilos de nomenclatura diferentes. Es útil poder reconocer qué estilo de denominación se está utilizando, independientemente de para qué se utilicen.

Se suelen distinguir los siguientes estilos de denominación:

- b (una sola letra minúscula)
- B (una sola letra mayúscula)
- lowercase
- lower_case_with_underscores
- UPPERCASE
- UPPER_CASE_WITH_UNDERSCORES
- CapitalizedWords (o CapWords, o CamelCase - llamada así por el aspecto desigual de sus letras [4]). También se conoce como StudlyCaps.

Nota: Cuando utilice acrónimos en CapWords, ponga en mayúsculas todas las letras del acrónimo. Así, HTTPServerError es mejor que HttpServerError.

- mixedCase (¡se diferencia de CapitalizedWords por el carácter inicial en minúscula!)
- Capitalized_Words_With_Underscores (¡feo!)

También existe el estilo de usar un prefijo único corto para agrupar nombres relacionados. Esto no se usa mucho en Python, pero se menciona para completar. Por ejemplo, la función os.stat() devuelve una tupla cuyos elementos tradicionalmente tienen nombres como st_mode, st_size, st_mtime y así sucesivamente. (Esto se hace para enfatizar la correspondencia con los campos de la estructura de llamada al sistema POSIX, lo que ayuda a los programadores familiarizados con ella).

La biblioteca X11 utiliza una X inicial para todas sus funciones públicas. En Python, este estilo se considera generalmente innecesario porque los nombres de atributos y métodos se prefijan con un objeto, y los nombres de funciones se prefijan con un nombre de módulo.

Además, se reconocen las siguientes formas especiales que utilizan guiones bajos iniciales o finales (generalmente pueden combinarse con cualquier convención de mayúsculas y minúsculas):

- _single_leading_underscore: indicador débil de "uso interno". Por ejemplo, from M import * no importa objetos cuyos nombres empiecen por guión bajo.
- single_trailing_underscore_: utilizado por convención para evitar conflictos con palabras clave de Python, p.ej.
```
tkinter.Toplevel(master, class_='ClassName')
```
- __double_leading_underscore: al nombrar un atributo de clase, invoca la manipulación de nombres (dentro de la clase FooBar, __boo se convierte en _FooBar__boo; ver más abajo).

- __double_leading_and_trailing_underscore__: Objetos o atributos "mágicos" que viven en espacios de nombres controlados por el usuario. Por ejemplo, __init__, __import__ o __file__. No invente nunca estos nombres; utilícelos sólo como están documentados.

### Prescriptivo: Convenciones de denominación<a name="id24"></a>

#### Nombres que deben evitarse<a name="id25"></a>

No utilice nunca los caracteres "l" (letra minúscula el), "O" (letra mayúscula oh) o "I" (letra mayúscula eye) como nombres de variables de un solo carácter.

En algunos tipos de letra, estos caracteres no se distinguen de los números uno y cero. Si tiene la tentación de utilizar "l", utilice "L" en su lugar.

#### Compatibilidad ASCII<a name="id26"></a>

Los identificadores utilizados en la biblioteca estándar deben ser compatibles con ASCII, tal y como se describe en la sección de política del PEP 3131.

#### Nombres de paquetes y módulos<a name="id27"></a>

Los módulos deben tener nombres cortos, todo en minúsculas. Se pueden utilizar guiones bajos en el nombre del módulo si mejora la legibilidad. Los paquetes de Python también deben tener nombres cortos, todo en minúsculas, aunque se desaconseja el uso de guiones bajos.

Cuando un módulo de extensión escrito en C o C++ va acompañado de un módulo Python que proporciona una interfaz de nivel superior (por ejemplo, más orientada a objetos), el módulo C/C++ lleva un guión bajo inicial (por ejemplo, _socket).

#### Nombres de clases<a name="id28"></a>

Los nombres de las clases deben utilizar normalmente la convención CapWords.

La convención de nomenclatura de funciones puede utilizarse en los casos en los que la interfaz esté documentada y se utilice principalmente como una llamada.

Tenga en cuenta que existe una convención distinta para los nombres de los componentes: la mayoría de los nombres de los componentes son palabras sueltas (o dos palabras juntas), y la convención CapWords sólo se utiliza para los nombres de las excepciones y las constantes de los componentes.

#### Nombres de variables de tipo<a name="id29"></a>

Los nombres de las variables de tipo introducidas en PEP 484 normalmente deberían usar CapWords prefiriendo nombres cortos: T, AnyStr, Num. Se recomienda añadir los sufijos _co o _contra a las variables utilizadas para declarar el comportamiento covariante o contravariante correspondientemente:

```
from typing import TypeVar

VT_co = TypeVar('VT_co', covariant=True)
KT_contra = TypeVar('KT_contra', contravariant=True)
```

#### Nombres de excepción<a name="id30"></a>

Dado que las excepciones deben ser clases, aquí se aplica la convención de nomenclatura de clases. Sin embargo, debe utilizar el sufijo "Error" en los nombres de las excepciones (si la excepción es realmente un error).

#### Nombres de variables globales<a name="id31"></a>

(Las convenciones son más o menos las mismas que para las funciones.

Los módulos que están diseñados para su uso a través de from M import * deben utilizar el mecanismo __all__ para evitar la exportación de globales, o utilizar la antigua convención de prefijar tales globales con un guión bajo (que es posible que desee hacer para indicar que estos globales son "no públicos del módulo").

#### Nombres de funciones y variables<a name="id32"></a>

Los nombres de las funciones deben escribirse en minúsculas, con las palabras separadas por guiones bajos si es necesario para mejorar la legibilidad.

Los nombres de las variables siguen la misma convención que los nombres de las funciones.

Sólo se permite mixedCase en contextos en los que ya es el estilo predominante (por ejemplo, threading.py), para mantener la compatibilidad con versiones anteriores.

#### Argumentos de funciones y métodos<a name="id33"></a>

Utilice siempre self como primer argumento en los métodos de instancia.

Utilice siempre cls para el primer argumento de los métodos de clase.

Si el nombre de un argumento de función coincide con una palabra clave reservada, suele ser mejor añadir un guión bajo al final en lugar de utilizar una abreviatura o un error ortográfico. Así, class_ es mejor que clss. (Tal vez sea mejor evitar tales choques utilizando un sinónimo).

#### Nombres de métodos y variables de instancia<a name="id34"></a>

Utilice las reglas de nomenclatura de funciones: minúsculas con palabras separadas por guiones bajos según sea necesario para mejorar la legibilidad.

Utilice un guión bajo inicial sólo para los métodos no públicos y las variables de instancia.

Para evitar conflictos de nombres con subclases, utilice dos guiones bajos iniciales para invocar las reglas de Python de manipulación de nombres.

Python mezcla estos nombres con el nombre de la clase: si la clase Foo tiene un atributo llamado __a, no puede ser accedido por Foo.__a. (Un usuario insistente aún podría acceder llamando a Foo._Foo__a.) Generalmente, los guiones bajos dobles sólo deberían usarse para evitar conflictos de nombres con atributos en clases diseñadas para ser subclasificadas.

Nota: existe cierta controversia sobre el uso de __names (véase más adelante).

#### Constantes<a name="id35"></a>

Las constantes suelen definirse a nivel de módulo y se escriben en mayúsculas con guiones bajos separando las palabras. Algunos ejemplos son MAX_OVERFLOW y TOTAL.

#### Diseño para la Herencia<a name="id36"></a>

Decide siempre si los métodos y variables de instancia de una clase (colectivamente: "atributos") deben ser públicos o no públicos. En caso de duda, elige no público; es más fácil hacerlo público después que hacer no público un atributo público.

Los atributos públicos son aquellos que esperas que utilicen los clientes no relacionados de tu clase, con tu compromiso de evitar cambios incompatibles hacia atrás. Los atributos no públicos son aquellos que no se pretende que sean utilizados por terceros; no garantizas que los atributos no públicos no cambien o incluso sean eliminados.

No usamos el término "privado" aquí, ya que ningún atributo es realmente privado en Python (sin una cantidad de trabajo generalmente innecesaria).

Otra categoría de atributos son aquellos que forman parte de la "API de subclase" (a menudo llamada "protegida" en otros lenguajes). Algunas clases están diseñadas para ser heredadas, ya sea para extender o modificar aspectos del comportamiento de la clase. Cuando diseñe una clase de este tipo, tenga cuidado de tomar decisiones explícitas sobre qué atributos son públicos, cuáles forman parte de la API de la subclase y cuáles son realmente sólo para ser utilizados por su clase base.

Con esto en mente, aquí están las directrices Pythonic:

- Los atributos públicos no deben llevar guión bajo.
- Si el nombre de tu atributo público colisiona con una palabra clave reservada, añade un guión bajo al final del nombre del atributo. Esto es preferible a una abreviatura o a una ortografía incorrecta. (Sin embargo, a pesar de esta regla, 'cls' es la ortografía preferida para cualquier variable o argumento que se sabe que es una clase, especialmente el primer argumento de un método de clase).

Nota 1: Véase la recomendación anterior sobre el nombre de los argumentos para los métodos de clase.

- Para atributos de datos públicos simples, es mejor exponer sólo el nombre del atributo, sin métodos accessor/mutator complicados. Ten en cuenta que Python proporciona un camino fácil para futuras mejoras, si encuentras que un simple atributo de datos necesita crecer en comportamiento funcional. En ese caso, usa propiedades para ocultar la implementación funcional detrás de una sintaxis simple de acceso a atributos de datos.
Nota 1: Trate de mantener el comportamiento funcional libre de efectos secundarios, aunque los efectos secundarios como el almacenamiento en caché están generalmente bien.

Nota 2: Evite usar propiedades para operaciones computacionalmente costosas; la notación de atributo hace creer a quien llama que el acceso es (relativamente) barato.

- Si su clase está destinada a ser subclasificada, y tiene atributos que no desea que las subclases utilicen, considere nombrarlos con doble guión bajo inicial y sin guión bajo final. Esto invoca el algoritmo de manipulación de nombres de Python, donde el nombre de la clase se transforma en el nombre del atributo. Esto ayuda a evitar colisiones de nombres de atributos si las subclases contienen inadvertidamente atributos con el mismo nombre.
Nota 1: Ten en cuenta que sólo se utiliza el nombre simple de la clase en el nombre mezclado, por lo que si una subclase elige tanto el mismo nombre de clase como el mismo nombre de atributo, pueden producirse colisiones de nombres.

Nota 2: La manipulación de nombres puede hacer que ciertos usos, como la depuración y __getattr__(), sean menos convenientes. Sin embargo, el algoritmo de manipulación de nombres está bien documentado y es fácil de realizar manualmente.

Nota 3: No a todo el mundo le gusta el name mangling. Intente equilibrar la necesidad de evitar conflictos accidentales de nombres con el uso potencial por parte de usuarios avanzados.

### Interfaces públicas e internas<a name="id37"></a>

Las garantías de compatibilidad con versiones anteriores sólo se aplican a las interfaces públicas. Por ello, es importante que los usuarios puedan distinguir claramente entre interfaces públicas e internas.

Las interfaces documentadas se consideran públicas, a menos que la documentación declare explícitamente que son provisionales o interfaces internas exentas de las garantías habituales de retrocompatibilidad. Todas las interfaces no documentadas deben considerarse internas.

Para soportar mejor la introspección, los módulos deberían declarar explícitamente los nombres en su API pública utilizando el atributo __all__. Establecer __all__ a una lista vacía indica que el módulo no tiene API pública.

Incluso con __all__ configurado adecuadamente, las interfaces internas (paquetes, módulos, clases, funciones, atributos u otros nombres) deben ir precedidas de un guión bajo inicial.

Una interfaz también se considera interna si cualquier espacio de nombres que la contenga (paquete, módulo o clase) se considera interno.

Los nombres importados deben considerarse siempre detalles de implementación. Otros módulos no deben confiar en el acceso indirecto a dichos nombres importados a menos que sean una parte explícitamente documentada de la API del módulo que los contiene, como os.path o el módulo __init__ de un paquete que expone funcionalidad de submódulos.

## Recomendaciones de programación<a name="id38"></a>

- El código debe escribirse de forma que no perjudique a otras implementaciones de Python (PyPy, Jython, IronPython, Cython, Psyco, etc.).
Por ejemplo, no confíe en la eficiente implementación de CPython de la concatenación de cadenas en el lugar para sentencias de la forma a += b o a = a + b. Esta optimización es frágil incluso en CPython (sólo funciona para algunos tipos) y no está presente en absoluto en implementaciones que no usan refcounting. En partes de la librería sensibles al rendimiento, debería usarse en su lugar la forma ''.join(). Esto asegurará que la concatenación ocurra en tiempo lineal a través de varias implementaciones.

- Las comparaciones a singletons como None deben hacerse siempre con is o is not, nunca con los operadores de igualdad.
Además, tenga cuidado al escribir if x cuando lo que realmente quiere decir es if x is not None (si x no es None), por ejemplo, al comprobar si una variable o argumento que por defecto es None se ha establecido con otro valor. El otro valor podría tener un tipo (como un contenedor) que podría ser falso en un contexto booleano.

- Utilice el operador is not en lugar de not ... is. Aunque ambas expresiones son funcionalmente idénticas, la primera es más legible y preferible:

```
# Correct:
if foo is not None:
```
```
# Wrong:
if not foo is None:
```

- Cuando se implementan operaciones de ordenación con comparaciones enriquecidas, es mejor implementar las seis operaciones (__eq__, __ne__, __lt__, __le__, __gt__, __ge__) en lugar de confiar en que otro código sólo ejercite una comparación en particular.
Para minimizar el esfuerzo, el decorador functools.total_ordering() proporciona una herramienta para generar los métodos de comparación que faltan.

PEP 207 indica que las reglas de reflexividad son asumidas por Python. Así, el intérprete puede intercambiar y > x con x < y, y >= x con x <= y, y puede intercambiar los argumentos de x == y y x != y. Se garantiza que las operaciones sort() y min() utilizan el operador < y la función max() utiliza el operador >. Sin embargo, es mejor implementar las seis operaciones para que no surjan confusiones en otros contextos.

- Utilice siempre una sentencia def en lugar de una sentencia de asignación que vincule una expresión lambda directamente a un identificador:

```
# Correct:
def f(x): return 2*x
```
```
# Wrong:
f = lambda x: 2*x
```

La primera forma significa que el nombre del objeto función resultante es específicamente 'f' en lugar del genérico '<lambda>'. Esto es más útil para las trazas y las representaciones de cadenas en general. El uso de la sentencia de asignación elimina la única ventaja que puede ofrecer una expresión lambda frente a una sentencia def explícita (es decir, que puede incrustarse dentro de una expresión mayor)

- Derivar las excepciones de Exception en lugar de BaseException. La herencia directa de BaseException está reservada para las excepciones cuya captura es casi siempre un error.
Diseñe jerarquías de excepciones basadas en las distinciones que el código que atrapa las excepciones probablemente necesite, en lugar de las ubicaciones donde se plantean las excepciones. Intenta responder a la pregunta "¿Qué ha ido mal?" programáticamente, en lugar de sólo declarar que "Ha ocurrido un problema" (ver PEP 3151 para un ejemplo de esta lección aprendida para la jerarquía de excepciones incorporada).

Aquí se aplican las convenciones de nomenclatura de clases, aunque debería añadir el sufijo "Error" a sus clases de excepción si la excepción es un error. Las excepciones que no son de error y que se utilizan para el control de flujo no local u otras formas de señalización no necesitan un sufijo especial.

- Utilice el encadenamiento de excepciones de forma apropiada. raise X from Y debe utilizarse para indicar un reemplazo explícito sin perder la traza original.
Al reemplazar deliberadamente una excepción interna (utilizando raise X from None), asegúrese de que los detalles relevantes se transfieren a la nueva excepción (como preservar el nombre del atributo al convertir KeyError a AttributeError, o incrustar el texto de la excepción original en el nuevo mensaje de excepción).

- Al capturar excepciones, mencione excepciones específicas siempre que sea posible en lugar de utilizar una cláusula except:

```
try:
    import platform_specific_module
except ImportError:
    platform_specific_module = None
```

Una cláusula except: desnuda atrapará las excepciones SystemExit y KeyboardInterrupt, haciendo más difícil interrumpir un programa con Control-C, y puede disfrazar otros problemas. Si desea capturar todas las excepciones que indican errores del programa, utilice except Exception: (bare except es equivalente a except BaseException:).

Una buena regla general es limitar el uso de cláusulas 'except' a dos casos:

1. Si el manejador de excepciones va a imprimir o registrar el rastreo; al menos el usuario será consciente de que se ha producido un error.
2. Si el código necesita hacer algún trabajo de limpieza, pero luego deja que la excepción se propague hacia arriba con raise. try...finally puede ser una mejor manera de manejar este caso.

- Al capturar errores del sistema operativo, prefiera la jerarquía de excepción explícita introducida en Python 3.3 sobre la introspección de los valores errno.

- Además, para todas las cláusulas try/except, limite la cláusula try a la cantidad mínima absoluta de código necesario. De nuevo, esto evita enmascarar errores:

```
# Correct:
try:
    value = collection[key]
except KeyError:
    return key_not_found(key)
else:
    return handle_value(value)
```
```
# Wrong:
try:
    # Too broad!
    return handle_value(collection[key])
except KeyError:
    # Will also catch KeyError raised by handle_value()
    return key_not_found(key)
```

Cuando un recurso es local a una sección concreta de código, utilice una sentencia with para asegurarse de que se limpia de forma rápida y fiable después de su uso. También es aceptable una sentencia try/finally.
Los gestores de contexto deben invocarse a través de funciones o métodos independientes siempre que hagan algo distinto de adquirir y liberar recursos:

```
# Correct:
with conn.begin_transaction():
    do_stuff_in_transaction(conn)
```
```
# Wrong:
with conn:
    do_stuff_in_transaction(conn)
```
   
El último ejemplo no proporciona ninguna información que indique que los métodos __enter__ y __exit__ están haciendo algo más que cerrar la conexión después de una transacción. Ser explícito es importante en este caso.

- Sea coherente con las sentencias return. Todas las sentencias return de una función deben devolver una expresión o ninguna de ellas debe hacerlo. Si alguna sentencia return devuelve una expresión, las sentencias return en las que no se devuelva ningún valor deben indicarlo explícitamente como return None, y debe haber una sentencia return explícita al final de la función (si es posible):

```
# Correct:

def foo(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return None

def bar(x):
    if x < 0:
        return None
    return math.sqrt(x)
```
```
# Wrong:

def foo(x):
    if x >= 0:
        return math.sqrt(x)

def bar(x):
    if x < 0:
        return
    return math.sqrt(x)
```

- Utilice ''.startswith() y ''.endswith() en lugar de trocear cadenas para buscar prefijos o sufijos.

startswith() y endswith() son más limpias y menos propensas a errores:

```
# Correct:
if foo.startswith('bar'):
```
```
# Wrong:
if foo[:3] == 'bar':
```

- Las comparaciones de tipos de objetos deben utilizar siempre isinstance() en lugar de comparar tipos directamente:

```
# Correct:
if isinstance(obj, int):
```
```
# Wrong:
if type(obj) is type(1):
```

- Para secuencias (cadenas, listas, tuplas), utilice el hecho de que las secuencias vacías son falsas:

```
# Correct:
if not seq:
if seq:
```
```
# Wrong:
if len(seq):
if not len(seq):
```

- No escriba literales de cadena que dependan de un espacio en blanco final significativo. Estos espacios son visualmente indistinguibles y algunos editores (o más recientemente, reindent.py) los recortan.

- No compare valores booleanos a Verdadero o Falso usando ==:

```
# Correct:
if greeting:
```
```
# Wrong:
if greeting == True:
```

Peor:

```
# Wrong:
if greeting is True:
```

- Se desaconseja el uso de las sentencias de control de flujo return/break/continue dentro del conjunto finally de un try...finally, donde la sentencia de control de flujo saltaría fuera del conjunto finally. Esto se debe a que dichas sentencias cancelarán implícitamente cualquier excepción activa que se esté propagando a través del conjunto finally:

```
# Wrong:
def foo():
    try:
        1 / 0
    finally:
        return 42
```

### Anotaciones de funciones<a name="id39"></a>

Con la aceptación de PEP 484, las reglas de estilo para las anotaciones de funciones han cambiado.

- Las anotaciones de funciones deben usar la sintaxis PEP 484 (hay algunas recomendaciones de formato para anotaciones en la sección anterior).
- Ya no se fomenta la experimentación con estilos de anotación que se recomendaba anteriormente en este PEP.
- Sin embargo, fuera de la stdlib, ahora se fomentan los experimentos dentro de las reglas de PEP 484. Por ejemplo, marcar una gran librería o aplicación de terceros con anotaciones de tipo estilo PEP 484, revisar lo fácil que fue añadir esas anotaciones, y observar si su presencia aumenta la comprensibilidad del código.
- La biblioteca estándar de Python debería ser conservadora en la adopción de tales anotaciones, pero su uso está permitido para código nuevo y para grandes refactorizaciones.
- Para el código que quiera hacer un uso diferente de las anotaciones de función se recomienda poner un comentario de la forma:
```
# type: ignore
```
cerca de la parte superior del archivo; esto indica a los comprobadores de tipo que ignoren todas las anotaciones. (En PEP 484 se pueden encontrar formas más precisas de desactivar las quejas de los comprobadores de tipos).

- Como los linters, los comprobadores de tipos son herramientas opcionales e independientes. Los intérpretes de Python por defecto no deberían emitir ningún mensaje debido a la comprobación de tipos y no deberían alterar su comportamiento basándose en las anotaciones.
- Los usuarios que no quieran usar comprobadores de tipos son libres de ignorarlos. Sin embargo, se espera que los usuarios de paquetes de librerias de terceros puedan querer ejecutar comprobadores de tipos sobre esos paquetes. Para este propósito PEP 484 recomienda el uso de ficheros stub: ficheros .pyi que son leídos por el comprobador de tipos con preferencia a los correspondientes ficheros .py. Los archivos stub pueden distribuirse con una biblioteca, o por separado (con el permiso del autor de la biblioteca) a través del repositorio typeshed [5].

### Anotaciones de variables<a name="id40"></a>

PEP 526 introdujo las anotaciones de variables. Las recomendaciones de estilo para ellas son similares a las de las anotaciones de funciones descritas anteriormente:

- Las anotaciones para variables de nivel de módulo, variables de clase e instancia, y variables locales deben tener un solo espacio después de los dos puntos.
- No debe haber ningún espacio antes de los dos puntos.
- Si una asignación tiene un lado derecho, entonces el signo de igualdad debe tener exactamente un espacio en ambos lados:
```
# Correct:

code: int

class Point:
    coords: Tuple[int, int]
    label: str = '<unknown>'
```
```
# Wrong:

code:int  # No space after colon
code : int  # Space before colon

class Test:
    result: int=0  # No spaces around equality sign
```

- Aunque la PEP 526 está aceptada para Python 3.6, la sintaxis de anotación de variables es la preferida para ficheros stub en todas las versiones de Python (ver PEP 484 para más detalles).

Notas a pie de página

[1] La sangría colgante es un estilo tipográfico en el que todas las líneas de un párrafo están sangradas excepto la primera. En el contexto de Python, el término se usa para describir un estilo donde el paréntesis de apertura de una sentencia entre paréntesis es el último carácter no espacio en blanco de la línea, con las líneas subsiguientes sangradas hasta el paréntesis de cierre.

## Referencias<a name="id41"></a>

[2] Barry’s GNU Mailman style guide http://barry.warsaw.us/software/STYLEGUIDE.txt
[3] Donald Knuth’s The TeXBook, pages 195 and 196.
[4] http://www.wikipedia.com/wiki/CamelCase
[5] Typeshed repo https://github.com/python/typeshed

## Copyright<a name="id42"></a>

Este documento es de dominio público.

Fuente: https://github.com/python/peps/blob/main/peps/pep-0008.rst

Última modificación 2023-09-09 17:39:29 GMT

