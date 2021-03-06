# [Variables](@id variables)

Una variable en Julia es un nombre asociado a un valor. Esto es útil cuando pretendemos almacenar un valor (como el que obtenemos después de un cálculo) para un uso posterior. Por ejemplo:

```julia-repl
# Assign the value 10 to the variable x
julia> x = 10
10

# Doing math with x's value
julia> x + 1
11

# Reassign x's value
julia> x = 1 + 1
2

# You can assign values of other types, like strings of text
julia> x = "Hello World!"
"Hello World!"
```

Julia proporciona un sistema muy flexible para nombrar las variables. Los nombres de variable son sensibles a las mayúsculas, y no tienen significado semántico (es decir, que el lenguaje no trata de modo distinto  a las variables basándose en sus nombres).

```jldoctest
julia> x = 1.0
1.0

julia> y = -3
-3

julia> Z = "My string"
"My string"

julia> customary_phrase = "Hello world!"
"Hello world!"

julia> UniversalDeclarationOfHumanRightsStart = "人人生而自由，在尊严和权利上一律平等。"
"人人生而自由，在尊严和权利上一律平等。"
```

Los nombres Unicode (usando codificación UTF-8) están permitidos:

```jldoctest
julia> δ = 0.00001
1.0e-5

julia> 안녕하세요 = "Hello"
"Hello"
```

En el REPL y otros entornos de edición Julia se pueden introducir símbolos matemáticos Unicode usando la notación de *Latex* precedido de backslash y seguido de un tabulador. Por ejemplo, podemos crear el nombre de variable `δ` tecleando `\delta`-*tab*, o incluso el nombre `α̂₂` tecleando `\alpha`-*tab*-`\hat`- *tab*-`\_2`-*tab*. (Si encuentras un símbolo en algun sitio, como por ejemplo en el código de alguien, y no sabes como escribirlo, el REPL te ayudará: solamente teclea `?` y luego pega el símbolo.)

Julia también permite redefinir constantes predefinidas su fuera necesario:

```jldoctest
julia> pi
π = 3.1415926535897...

julia> pi = 3
WARNING: imported binding for pi overwritten in module Main
3

julia> pi
3

julia> sqrt(100)
10.0

julia> sqrt = 4
WARNING: imported binding for sqrt overwritten in module Main
4
```

Sin embargo, esto no se recomienta para evitar una potencial confusión.

## Nombres de Variables Permitidos

Los nombres de variable deben comenzar con una letra (`A`-`Z` o `a`-`z`), símblo de subrayado, o un subconjunto de puntos Unicode mayores que `00A0`. En particular, se permiten las [categorías de caracteres Unicode](http://www.fileformat.info/info/unicode/category/index.htm) Lu/Ll/Lt/Lm/Lo/Nl (letras), Sc/So (monedas y otros símbolos), y otros pocos caracteres (por ejemplo, un subconjunto de los símbolos matemáticos Sm). Entre los caracteres subsecuentes se pueden también incluir `!` y los dígitos (`0`-`9` y otros caracteres en las categorías Nd/No), así como otros puntos de código Unicode: diacríticas y otras marcas de modificación (categorías Mn/Mc/Me/Sk), algunos conectores de puntuación (category Pc), 
primos, y otros cuantos caracteres.

Los operadores como `+` son también identificadores válidos, pero son analizados sintácticamente de un modo especial. En algunos contextos, los operadores pueden ser usados justo como variables; por ejemplo `(+)` se refiere a la función de suma, y `(+) = f` la reasignará. La mayoría de los operadores infijos Unicode (en la categoría Sm), tal como `⊕`, son analizados como operadores infijos y están disponibles para métodos definidos por el usuario (por ejemplo, podemos usar `const ⊗ = kron` para definir `⊗` como un operador infijo producto de Kronecker).

Los únicos nombres específicamente prohibidos para nombres de variables son los nombres de las instrucciones predefinidas:

```julia-repl
julia> else = false
ERROR: syntax: unexpected "else"

julia> try = "No"
ERROR: syntax: unexpected "="
```

Algunos caracteres Unicode son considerados equivalentes en identificadores. Las distintas formas de introducir caracteres que combinan en Unicode (por ejemplo, acentos) son tratadas como equivalentes (específicamente los identificadores Julia son normalizados NFC). Los caracteres Unicode `ɛ` (U+025B: Latin small letter open e) y `µ` (U+00B5: micro sign) son tratados como las letras griegas correspondientes, debido que las primeras son más fácilmente accesibles via alguos métodos de entrada.

## Convenciones de Estilo

Aunque Julia impone pocas restricciones a los nombres válidos, se ha vuelto útil adoptar las 
siguientes convenciones:

* Los nombres de variable van en minúsculas.
* La separación enre palabras puede indicarse mediante el símbolo de guión bajo, aunque se desaconseja 
  su uso a menos que los símbolos sean difíciles de leer.
* Los nombres de tipos y módulos comienzan con mayúscula y la separación entre palabras se representa 
  con el formato *camel case*.
* Los nombres de funciones y macros van en minúscula, sin símbolos de guión bajo.
* Las funciones que escriben en sus argumentos tienen nombres que finalizan con el símbolo de admiración `!`.
  Estas suelen ser llamadas funciones "mutadoras" o funciones "*in-place*" debido a que pretenden producir 
  cambios en sus argumentos después de que la función sea invocada, no solo devolver un valor.
  
Para más información sobre convenciones de estilo, ver la [Guía de Estilo](@ref style-guide).
