
# R Markdown

## Introduction
## Introducci�n


R Markdown provides an unified authoring framework for data science, combining your code, its results, and your prose commentary. R Markdown documents are fully reproducible and support dozens of output formats, like PDFs, Word files, slideshows, and more. 

R Markdown provee  un marco de referencia para la ciencia de datos, combinando tu c�digo, sus resultados, y tus comentarios en prosa. Los documentos de R Markdown son completamente reproducibles y soportan docenas de formatos de salida tales como PDFs, archivos de Word, presentaciones y m�s.

R Markdown files are designed to be used in three ways:
Los archivos R Markdown est�n dise�ados para ser usados de tres maneras:

1.  For communicating to decision makers, who want to focus on the conclusions,
    not the code behind the analysis.
    
1.  Para comunicarse con los tomadores de decisiones, quienes desean enfocarse en las     conclusiones, no en el c�digo que subyace al an�lisis.

1.  For collaborating with other data scientists (including future you!), who
    are interested in both your conclusions, and how you reached them (i.e.
    the code).
    
1. Para colaborar con otros cient�ficos de datos (incluyendo a tu yo futuro !!),         quienes est�n interesados tanto en tus conclusiones como en el modo en el que         llegaste a ellas (es decir, el c�digo).

    
1.  As an environment in which to _do_ data science, as a modern day lab 
    notebook where you can capture not only what you did, but also what you
    were thinking.
    
1.  Como un ambiente en el cual _hacer_ ciencia de datos, como un *notebook* de           laboratorio moderno donde puedes capturar no s�lo que hiciste, sino tambi�n           estabas pensando cuando lo hac�as.    

R Markdown integrates a number of R packages and external tools. This means that help is, by-and-large, not available through `?`. Instead, as you work through this chapter, and use R Markdown in the future, keep these resources close to hand:

R Markdown integra una cantidad de paquetes de R y herramientas externas. Esto implica que la ayuda ,en general, no est� disponible a trav�s de ` ?`. En su lugar, mientras trabajas a lo largo de este capitulo, y utilizas R Markdown en el futuro, mant�n estos recursos cerca:

*   R Markdown Cheat Sheet: _Help > Cheatsheets > R Markdown Cheat Sheet_,

*   R Markdown Reference Guide: _Help > Cheatsheets > R Markdown Reference 
    Guide_.
    
*   Hoja de referencia de R Markdown : _Help > Cheatsheets > R Markdown Cheat Sheet_

*   Gu�a de referencia R Markdown  : _Help > Cheatsheets > R Markdown Reference 
    Guide_

Both cheatsheets are also available at <http://rstudio.com/cheatsheets>.
Ambas hojas tambi�n se encuentran disponibles en http://rstudio.com/cheatsheets>.


### Prerequisites
### Prerequisitos

You need the __rmarkdown__ package, but you don't need to explicitly install it or load it, as RStudio automatically does both when needed.

Necesitas el paquete __rmarkdown__, pero no necesitas cargarlo o instalarlo expl�citamente ya que RStudio hace ambas acciones automaticamente cuando es necesario.




## R Markdown basics
## R Markdown b�sico

This is an R Markdown file, a plain text file that has the extension `.Rmd`:

Este es un archivo R Markdown, un archivo de texto plano que tiene la extensi�n `.Rmd`:

````
---
title: "Diamond sizes"
date: 2016-08-25
output: html_document
---

```{r setup, include = FALSE}
library(ggplot2)
library(dplyr)

smaller <- diamonds %>% 
  filter(carat <= 2.5)
```

We have data about `r nrow(diamonds)` diamonds. Only 
`r nrow(diamonds) - nrow(smaller)` are larger than
2.5 carats. The distribution of the remainder is shown
below:

```{r, echo = FALSE}
smaller %>% 
  ggplot(aes(carat)) + 
  geom_freqpoly(binwidth = 0.01)
```
````

It contains three important types of content:

1.  An (optional) __YAML header__ surrounded by `---`s.
1.  __Chunks__ of R code surrounded by ```` ``` ````.
1.  Text mixed with simple text formatting like `# heading` and `_italics_`.

Contiene tres tipos importantes de contenido:
  1. Un encabezado YAML (opcional) rodeado de `---` 
  1. __Bloques__ de c�digo de R rodeado de ```` ``` ````.
  1. Texto mezclado con texto simple formateado con `# Encabezado` e `_it�licas_`.

When you open an `.Rmd`, you get a notebook interface where code and output are interleaved. You can run each code chunk by clicking the Run icon (it looks like a play button at the top of the chunk), or by pressing Cmd/Ctrl + Shift + Enter. RStudio executes the code and displays the results inline with the code:

Cuando abres un archivo `.Rmd`, obtienes una interfaz de *notebook* donde el c�digo y el *output* est�n intercalados. Puedes ejecutar cada bloque de c�digo haciendo clic el �cono ejecutar ( se parece a un bot�n de reproducir en la parte superior del bloque de c�digo), o presionando Cmd/Ctrl + Shift + Enter. RStudio ejecuta el c�digo y muestra los resultados incustrados en el c�digo:
  

<img src="rmarkdown/diamond-sizes-notebook.png" width="75%" style="display: block; margin: auto;" />

To produce a complete report containing all text, code, and results, click "Knit" or press Cmd/Ctrl + Shift + K.  You can also do this programmatically with `rmarkdown::render("1-example.Rmd")`. This will display the report in the viewer pane, and create a self-contained HTML file that you can share with others.

Para producir un reporte completo que contenga todo el texto, c�digo y resultados, hacerclic en "Knit" o presionar Cmd/Ctrl + Shift + K. Puede hacerse tambien de manera program�tica con `rmarkdown::render("1-example.Rmd")`. Esto mostrar� el reporte en el panel  *viewer* y crea un archivo HTML independiente que puedes compartir con otros.

<img src="rmarkdown/diamond-sizes-report.png" width="75%" style="display: block; margin: auto;" />

When you __knit__ the document, R Markdown sends the .Rmd file to __knitr__, http://yihui.name/knitr/, which executes all of the code chunks and creates a new markdown (.md) document which includes the code and its output. The markdown file generated by knitr is then processed by __pandoc__, <http://pandoc.org/>, which is responsible for creating the finished file. The advantage of this two step workflow is that you can create a very wide range of output formats, as you'll learn about in [R markdown formats].

Cuando haces *knit* el documento (knit en espa�ol significa tejer), R Markdown env�a el .Rmd a _knitr_, http://yihui.name/knitr/, que ejecuta todos los bloques de c�digo y crea un nuevo documento markdown (.md) que incluye el c�digo y su output. El archivo markdown generado por _knitr_ es procesado entonces por pandoc, http://pandoc.org/, que es el responsable de crear el archivo terminado. La ventaja de este flujo de trabajo en dos pasos es que puedes crear un muy amplio rango de formatos de salida, como aprender�s en [Formatos de R markdown ].

<img src="images/RMarkdownFlow.png" width="75%" style="display: block; margin: auto;" />

To get started with your own `.Rmd` file, select *File > New File > R Markdown...* in the menubar. RStudio will launch a wizard that you can use to pre-populate your file with useful content that reminds you how the key features of R Markdown work. 

Para comenzar con tu propio archivo `.Rmd`, selecciona *File > New File > R Markdown...* en la barra de men�. Rstudio iniciar� un asistente que puedes usar para pre-rellenar tu archivo con contenido �til que te recuerde como funcionan las principales caracter�sticas de R Markdown.



The following sections dive into the three components of an R Markdown document in more details: the markdown text, the code chunks, and the YAML header.

Las siguientes secciones profundizan en los tres componentes de un documento de R Markdown en m�s detalle: el texto markdown, los bloques de c�digo y el encabezado YAML.

### Exercises

1.  Create a new notebook using _File > New File > R Notebook_. Read the 
    instructions. Practice running the chunks. Verify that you can modify
    the code, re-run it, and see modified output.
    
1.  Crea un nuevo *notebook* usando _File > New File > R Notebook_. Lee las               instrucciones. Practica ejecutando los bloques. Verifica que puedes modificar el       c�digo,re-ejec�talo, y observa la salida modificada.
        
    
1.  Create a new R Markdown document with _File > New File > R Markdown..._
    Knit it by clicking the appropriate button. Knit it by using the 
    appropriate keyboard short cut. Verify that you can modify the
    input and see the output update.
    
1.  Crea un nuevo documento R Markdown con _File > New File > R Markdown..._
    Haz clic en el icono apropiado de *Knit*. Haz *Knit* usando  el atajo de teclado      apropiado. Verifica que puedes modificar el *input*  y  la actualizacion del         *output*.
    
1.  Compare and contrast the R notebook and R markdown files you created
    above. How are the outputs similar? How are they different? How are
    the inputs similar? How are they different? What happens if you
    copy the YAML header from one to the other?

1.  Compara y contrasta el *notebook* de R con los archivos de R markdown que has         creado antes. �C�mo son similares los outputs? �C�mo son diferentes? �C�mo son        similares los inputs? �En qu� se diferencian? �Qu� ocurre si copias el encabezado     YAML de uno al otro?

1.  Create one new R Markdown document for each of the three built-in
    formats: HTML, PDF and Word. Knit each of the three documents.
    How does the output differ? How does the input differ? (You may need
    to install LaTeX in order to build the PDF output --- RStudio will
    prompt you if this is necessary.)
    
1.  Crea un nuevo documento R Markdown para cada uno de los tres formatos                 incorporados: HTML, PDF and Word. Haz *knit* en cada uno de estos tres documentos.     �Como difiere el output? �C�mo difiere el input? (Puedes necesitar instalar LaTeX     para poder compilar el output en PDF--- RStudio preguntar� si esto es necesario).    

## Text formatting with Markdown
## Formateo de texto con Markdown

Prose in `.Rmd` files is written in Markdown, a lightweight set of conventions for formatting plain text files. Markdown is designed to be easy to read and easy to write. It is also very easy to learn. The guide below shows how to use Pandoc's Markdown, a slightly extended version of Markdown that R Markdown understands.

La prosa en los archivos `.Rmd` est� escrita en Markdown, un set liviano de convenciones para dar formato a archivos de texto plano. Markdown est� dise�ado para ser f�cil de leer y f�cil de escribir. Es tambien muy f�cil de aprender. La gu�a abajo muestra como usar el Markdown de Pandoc, una version ligeramente extendida de markdown que R Markdown comprende.


```
Text formatting 
------------------------------------------------------------

*italic*  or _italic_
**bold**   __bold__
`code`
superscript^2^ and subscript~2~

Headings
------------------------------------------------------------

# 1st Level Header

## 2nd Level Header

### 3rd Level Header

Lists
------------------------------------------------------------

*   Bulleted list item 1

*   Item 2

    * Item 2a

    * Item 2b

1.  Numbered list item 1

1.  Item 2. The numbers are incremented automatically in the output.

Links and images
------------------------------------------------------------

<http://example.com>

[linked phrase](http://example.com)

![optional caption text](path/to/img.png)

Tables 
------------------------------------------------------------

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell
```

The best way to learn these is simply to try them out. It will take a few days, but soon they will become second nature, and you won't need to think about them. If you forget, you can get to a handy reference sheet with *Help > Markdown Quick Reference*.

La mejor manera de aprender es simplemente probar. Tomar� unos d�as, pero pronto se convertir� en algo natural, y no necesitar�s pensar en ellas. Si te olvidas, puedes tener una �til hoja de referencia con *Help > Markdown Quick Reference*.

### Exercises
### Ejercicios


1.  Practice what you've learned by creating a brief CV. The title should be
    your name, and you should include headings for (at least) education or
    employment. Each of the sections should include a bulleted list of
    jobs/degrees. Highlight the year in bold.
    
1.  Practica lo que has aprendido crando un CV breve. El t�tulo deber�a ser tu nombre,     y  deber�as incluir encabezados para (por lo menos) educaci�n o empleo. Cada una      de las secciones deber�a incluir una lista punteada de trabajos/ t�tulos              obtenidos.  Resalta a�o en negrita.    
    
1.  Using the R Markdown quick reference, figure out how to:
1.  Usando  la referencia rapida de R Markdown, descubre como:

    1.  Add a footnote.
    1.  Add a horizontal rule.
    1.  Add a block quote.
    
    1.  Agregar una nota al pie.
    1.  Agregar una linea horizontal.
    1.  Agregar una cita en bloque.    
    
1.  Copy and paste the contents of `diamond-sizes.Rmd` from
    <https://github.com/hadley/r4ds/tree/master/rmarkdown> in to a local
    R markdown document. Check that you can run it, then add text after the 
    frequency polygon that describes its most striking features.
    
1.  Copia y pega los contenidos de `diamond-sizes.Rmd` desde                              <https://github.com/hadley/r4ds/tree/master/rmarkdown> a un documento local de R      Markdown. Revisa que puedes ejecutarlo,  agrega texto despues del poligono de         frecuencias que describa sus caracteristicas m�s llamativas.    

## Code chunks
## Bloques de c�digo

To run code inside an R Markdown document, you need to insert a chunk. There are three ways to do so:
Para ejecutar c�digo dentro de un documento R Markdown, necesitas insertar un bloque.
Hay tres maneras para hacerlo:

1. The keyboard shortcut Cmd/Ctrl + Alt + I

1. El atajo de teclado Cmd/Ctrl + Alt + I

1. The "Insert" button icon in the editor toolbar.

1. El icono "Insertar" en la barra de edici�n 

1. By manually typing the chunk delimiters ` ```{r} ` and ` ``` `.

1. Tipeando manualmente los delimitadores de bloque ` ```{r} ` y ` ``` `.


Obviously, I'd recommend you learn the keyboard shortcut. It will save you a lot of time in the long run!

Obviamente, recomendar�a que aprendieras a usar el atajo de teclado. A largo plazo, te ahorrar� mucho tiempo.

You can continue to run the code using the keyboard shortcut that by now (I hope!) you know and love: Cmd/Ctrl + Enter. However, chunks get a new keyboard shortcut: Cmd/Ctrl + Shift + Enter, which runs all the code in the chunk. Think of a chunk like a function. A chunk should be relatively self-contained, and focussed around a single task. 

Puedes continuar ejecutando el c�digo usando el atajo de teclado que para este momento (espero!) ya conoces y amas : Cmd/Ctrl + Enter. Sin embargo, los bloques de c�digo tienen otro atajo de teclado: Cmd/Ctrl + Shift + Enter, que ejecuta todo el c�digo en el bloque. Piensa el bloque como una funci�n. Un bloque deber�a ser relativamente aut�nomo,y enfocado alrededor de una sola tarea.


The following sections describe the chunk header which consists of ```` ```{r ````, followed by an optional chunk name, followed by comma separated options, followed by `}`. Next comes your R code and the chunk end is indicated by a final ```` ``` ````.

Las siguientes secciones decriben el encabezado de bloque que consiste en ```` ```{r ````, seguido por un nombre opcional para el bloque, seguido entonces por opciones separadas por comas, y concluyendo con `}`. Inmediatamente despu�s sigue tu c�digo de R el bloque y el fin del bloque se indica con un  ```` ``` ```` final.

### Chunk name
### Nombres en bloques

Chunks can be given an optional name: ```` ```{r by-name} ````. This has three advantages:
Los bloques puede tener opcionalmente nombres : ```` ```{r nombre} ````. Esto presenta tres ventajas:

1.  You can more easily navigate to specific chunks using the drop-down
    code navigator in the bottom-left of the script editor:
    
1.  Puedes navegar m�s f�cilmente a bloques espec�ficos usando el navegador de c�digo     desplegable abajo a la izquierda en el editor de *script*:
    <img src="screenshots/rmarkdown-chunk-nav.png" width="30%" style="display: block; margin: auto;" />

1.  Graphics produced by the chunks will have useful names that make
    them easier to use elsewhere. More on that in [other important options].
1.  Los gr�ficos producidos por los bloques tendr�n nombres �tiles que hace que sean      m�s f�ciles de utilizar en otra parte.  M�a sobre esto en [otras opciones             importantes].    
    
1.  You can set up networks of cached chunks to avoid re-performing expensive
    computations on every run. More on that below.
1.  Puedes crear redes de bloque cacheados para evitar re-ejecutar computos costosos      en cada ejecucion. M�s sobre esto mas adelante.     

There is one chunk name that imbues special behaviour: `setup`. When you're in a notebook mode, the chunk named setup will be run automatically once, before any other code is run.

Hay un nombre de bloque que tiene comportamiento especial: `setup`. Cuando te encuentras en modo *notebook*, el bloque llamado setup se ejecutar� autom�ticamente una vez, antes de ejecutar cualquier otro c�digo.


### Chunk options
### Opciones los bloques

Chunk output can be customised with __options__, arguments supplied to chunk header. Knitr provides almost 60 options that you can use to customize your code chunks. Here we'll cover the most important chunk options that you'll use frequently. You can see the full list at <http://yihui.name/knitr/options/>. 

La salida de los bloques puede personalizarse con __options__, argumentos suministrados al encabezado del bloque. Knitr provee casi 60 opciones para que puedas usar para personalizar tus bloques de c�digo. Aqui cubriremos las opciones de bloques mas imporantes que usaras m�s frecuentemente. Puedes ver la lista completa en <http://yihui.name/knitr/options/>. 

The most important set of options controls if your code block is executed and what results are inserted in the finished report:

El set de opciones m�s importantes  controla si tu bloque de c�digo es ejecutado y que resultados estar�n insertos en el reporte terminado: 
  
*   `eval = FALSE` prevents code from being evaluated. (And obviously if the
    code is not run, no results will be generated). This is useful for 
    displaying example code, or for disabling a large block of code without 
    commenting each line.
    
*   `eval = FALSE` evita que c�digo sea evaluado. (Y obviamente si el c�digo no es         ejecutado no se generaran resultados). Esto es �til para mostrar c�digos de           ejemplo,o para deshabilitar un gran bloque de c�digo sin comentar cada l�nea.   

*   `include = FALSE` runs the code, but doesn't show the code or results 
    in the final document. Use this for setup code that you don't want
    cluttering your report.
    
*   `include = FALSE` ejecuta el c�digo, pero no muestra el c�digo o los resultados       en el documento final. Usa esto para que c�digo de configuracion que no quieres       que abarrote tu reporte.    

*   `echo = FALSE` prevents code, but not the results from appearing in the 
    finished file. Use this when writing reports aimed at people who don't
    want to see the underlying R code.
    
*   `echo = FALSE` evita que se vea el c�digo, pero no los resultados en el archivo       final. Utiliza esto cuando quieres escribir reportes enfocados a personas que no      quieren ver el c�digo subyacente de R.    

    
*   `message = FALSE` or `warning = FALSE` prevents messages or warnings 
    from appearing in the finished file.

*   `message = FALSE` o `warning = FALSE` evita que aparezcan mensajes o advertencias      en el archivo final.

*   `results = 'hide'` hides printed output; `fig.show = 'hide'` hides
    plots.
    
*   `results = 'hide'` oculta el *output* impreso; `fig.show = 'hide'` oculta             graficos.    

*   `error = TRUE` causes the render to continue even if code returns an error.
    This is rarely something you'll want to include in the final version
    of your report, but can be very useful if you need to debug exactly
    what is going on inside your `.Rmd`. It's also useful if you're teaching R
    and want to deliberately include an error. The default, `error = FALSE` causes 
    knitting to fail if there is a single error in the document.
    
*   `error = TRUE`  causa que el *render* contin�e incluso si el c�digo devuelve un error. Esto es algo que raramente quieres incluir en la version final de tu reporte, pero puede ser muy �til si necesitas depurar exactamente que ocurre dentro de tu `.Rmd`. Es tambi�n �til si estas ense�ando R y quieres incluir deliberadamente un error. Por defecto, `error = FALSE` provoca que el *knitting* falle si hay incluso un error en el documento.    
    
The following table summarises which types of output each option supressess:
La siguiente tabla resume que tipos de *output*suprime cada opci�n:

Option             | Run code | Show code | Output | Plots | Messages | Warnings 
-------------------|----------|-----------|--------|-------|----------|---------
`eval = FALSE`     | -        |           | -      | -     | -        | -
`include = FALSE`  |          | -         | -      | -     | -        | -
`echo = FALSE`     |          | -         |        |       |          |
`results = "hide"` |          |           | -      |       |          | 
`fig.show = "hide"`|          |           |        | -     |          |
`message = FALSE`  |          |           |        |       | -        |
`warning = FALSE`  |          |           |        |       |          | -


Opci�n             | Ejecuta  | Muestra   | Output | Graficos | Mensajes |Advertencias                    | c�digo   | c�digo    |        |          |          |
-------------------|----------|-----------|--------|----------|----------|---------
`eval = FALSE`     | -        |           | -      | -        | -        | -
`include = FALSE`  |          | -         | -      | -        | -        | -
`echo = FALSE`     |          | -         |        |          |          |
`results = "hide"` |          |           | -      |          |          | 
`fig.show = "hide"`|          |           |        | -        |          |
`message = FALSE`  |          |           |        |          | -        |
`warning = FALSE`  |          |           |        |          |          | -

### Table
### Tablas
By default, R Markdown prints data frames and matrices as you'd see them in the console:
Por defecto, R Markdown imprime data frames y matrices tal como se ven en la consola:


```r
mtcars[1:5, ]
#>                    mpg cyl disp  hp drat   wt qsec vs am gear carb
#> Mazda RX4         21.0   6  160 110 3.90 2.62 16.5  0  1    4    4
#> Mazda RX4 Wag     21.0   6  160 110 3.90 2.88 17.0  0  1    4    4
#> Datsun 710        22.8   4  108  93 3.85 2.32 18.6  1  1    4    1
#> Hornet 4 Drive    21.4   6  258 110 3.08 3.21 19.4  1  0    3    1
#> Hornet Sportabout 18.7   8  360 175 3.15 3.44 17.0  0  0    3    2
```

If you prefer that data be displayed with additional formatting you can use the `knitr::kable` function. The code below generates Table \@ref(tab:kable).
Si prefieres que los datos tengan formato adicional puedes usar la funci�n `knitr::kable`. El siguente c�digo genera una Tabla \@ref(tab:kable).


```r
knitr::kable(
  mtcars[1:5, ], 
  caption = "Un kable de knitr."
)
```



Table: (\#tab:kable)Un kable de knitr.

                      mpg   cyl   disp    hp   drat     wt   qsec   vs   am   gear   carb
------------------  -----  ----  -----  ----  -----  -----  -----  ---  ---  -----  -----
Mazda RX4            21.0     6    160   110   3.90   2.62   16.5    0    1      4      4
Mazda RX4 Wag        21.0     6    160   110   3.90   2.88   17.0    0    1      4      4
Datsun 710           22.8     4    108    93   3.85   2.32   18.6    1    1      4      1
Hornet 4 Drive       21.4     6    258   110   3.08   3.21   19.4    1    0      3      1
Hornet Sportabout    18.7     8    360   175   3.15   3.44   17.0    0    0      3      2















