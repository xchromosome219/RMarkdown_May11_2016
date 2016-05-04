# Creating Dynamic Documents with RMarkdown and Knitr
Marian L. Schmidt  
May 11th, 2016  




# Getting Started

# 1. Load Packages
The following packages are necessary for to

```r
#install.packges("knitr")
library(knitr)
#install.packages("dplyr")
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
#install.packages("ggplot2")
library(ggplot2)
```

***

# Dynamic Documents  

<a href="https://en.wikipedia.org/wiki/Literate_programming">Literate programming</a> is the basic idea behind dynamic documents and was proposed by Donald Knuth in 1984.  Originally, it was for mixing the source code and documentation of software development together.  Then we could:  

1. **Tangle**:  Extract the source code out of the document.  
2. **Weave**:  Execute the code to get the compiled results.  

In dynamic documents, program or analysis code is run to produce output (e.g. tables, plots, models, etc) and then are explained through narrative writing. 


***

***



# Markdown

To fully understand RMarkdown, we first need to cover <a href="https://daringfireball.net/projects/markdown/">Markdown</a>, which is a system for writing simple, readable text that is easily converted to html.  Markdown essentially is two things:  

1. A plain text formatting syntax  
2. A software tool written in Perl.  
    - Converts the plain text formatting into HTML.  
    
>**Main goal of Markdown:**  
> Make the syntax of the raw (pre-html) document as readable possible. 

Would you rather read this?  
```html
<body>
  <section>
    <h1>Rock Climbing Packing List</h1>
    <ul>
      <li>Climbing Shoes</li>
      <li>Harness</li>
      <li>Backpack</li>
      <li>Rope</li>
      <li>Belayer</li>
    </ul>
  </section>
</body>
```
The above code is html.

Or this?  
```markdown
# Rock Climbing Packing List

* Climbing Shoes
* Harness
* Backpack  
* Rope
* Belayer
```
The above code is Markdown and it is clear that this option is definitely much easier to read!

We will talk more about the syntax of Markdown after we introduce RMarkdown. 


# RMarkdown
<a href="http://rmarkdown.rstudio.com/">RMarkdown</a> is a variant of Markdown that makes it easy to create dynamic documents, presentations and reports from R.  It has embedded R code chunks to be used with `knitr` to make it easy to create reproducible (web-based) reports in the sense that they can be automatically regnerated when the underlying code it modified.    

- RMarkdown lets you combine **Markdown** with images, links, tables, LaTeX, and actual R code.
- **RStudio makes creating documents from RMarkdown easy** but you can use Pandoc (more on that later) instead.
- RStudio (like R) is free and runs on any operating system.


RMarkdown renders many different types of files including:  

- <a href="http://rmarkdown.rstudio.com/html_document_format.html">HTML</a>    
- <a href="http://rmarkdown.rstudio.com/pdf_document_format.html">PDF</a>  
- Markdown  
- <a href="http://rmarkdown.rstudio.com/word_document_format.html">Microsoft Word</a>   
- Presentations:  
    - Fancy HTML5 presentations:  
        - <a href="http://rmarkdown.rstudio.com/ioslides_presentation_format.html">ioslides</a>
        - <a href="http://rmarkdown.rstudio.com/slidy_presentation_format.html">Slidy</a>  
        - <a href="http://slidify.org/index.html">Slidify</a>
    - PDF Presentations:  
        - <a href="http://rmarkdown.rstudio.com/beamer_presentation_format.html">Beamer</a>  
    - Handouts:  
        - <a href="http://rmarkdown.rstudio.com/tufte_handout_format.html">Tufte Handouts</a> 
- <a href="http://rmarkdown.rstudio.com/package_vignette_format.html">HTML R Package Vignettes</a>  
- <a href="http://rmarkdown.rstudio.com/rmarkdown_websites.html">Even Entire Websites!</a>   

![](Images/Rmd_output.png)

While there are a lot of different types of rendered documents in RMarkdown, today we will focus primarily on HTML output files, as I have found these files to be the most useful and flexible for my research.

## Why R Markdown?
A convenient tool for reproducible and dynamic reports with R!       

- Execute code with `knitr`.   
- Easy to learn syntax.  
- Include LaTeX equations.  
- Don't need to worry about page breaks or figure placement.  
- Consolidate your code and write up into a single file:  
    + Slideshows, pdfs, html documents, word files  
- It's **so easy** to use with version control with Git!   

### Simple Workflow  

1. Create `.Rmd` file that includes R code chunks and and markdown narratives.  
2. Give the `.Rmd` file to `knitr` to execute the R code chunks and create a new `.md` file.  
3. Give the `.md` file to pandoc, which will create the final rendered document (e.g. html, microsoft word, pdf, etc.).  

![](Images/Rmd_workflow.png)

While this may seem complicated, we can hit the "Knit" button at the top of the page
![](Images/knit_button.png)

or we can run the following code:  
```
rmarkdown::render("RMarkdown_Lesson.Rmd", "html_document")
```





## YAML Headers

### RMarkdown Appearance and Syle
Rmarkdown has several options that control the appearance of HTML documents.  Some aruments to choose from are:  

- **theme**  
- **highlight**  
- **smart**  


The HTML output themes are drawn from the <a href="http://bootswatch.com/">Bootswatch</a> library.  Valid **HTML themes** include the following:    

- `cerulean`, `cosmo`, `default`,`flatly`, `journal`, `lumen`, `paper`, `readable`, `sandstone`, `spacelab`, `simplex`, `united`, and `yeti`.  
    - For example, the theme of this page is `lumen`.
- Pass null for no theme (in this case you can use the css parameter to add your own styles).

**Highlight** specifies the syntax highlighting style. Supported styles include the following:  

- `default`, `espresso`, `haddock`, `kate`, `monochrome`, `pygments`, `tango`, `textmate`, and `zenburn`.   
- Pass null to prevent syntax highlighting.

**Smart** indicates whether to produce typographically correct output, converting straight quotes to curly quotes, --- to em-dashes, -- to en-dashes, and ... to ellipses. **Smart** is enabled by default.

For example:

```
---
output:
  html_document:
    theme: slate
    highlight: tango
---
```

If you felt inclined, you could also produce and use your own theme.  If you did so, the output section of your YAML header would like like:  
```
output:
  html_document:
    css: styles.css
```

If you wanted to go the extra mile and write your own theme in addition to highlight, the YAML header would look like: 
```
---
output:
  html_document:
    theme: null
    highlight: null
    css: styles.css
---
```



Here's a link to learn more about the <a href="http://rmarkdown.rstudio.com/html_document_format.html#appearance_and_style">Appearance and Style</a> in HTML output.

# Knitr Themes
The knitr syntax theme can be adjusted or completely customized.  If you do not prefer the default themes, use the object `knit_theme` to change it.  There are **80 themes** contained within `knitr` and we can view the names of them by `knit_theme$get()`.

What are the first 30 `knitr` themes?


```r
head(knit_theme$get(), 30)
```

```
##  [1] "acid"          "aiseered"      "andes"         "anotherdark"  
##  [5] "autumn"        "baycomb"       "bclear"        "biogoo"       
##  [9] "bipolar"       "blacknblue"    "bluegreen"     "breeze"       
## [13] "bright"        "camo"          "candy"         "clarity"      
## [17] "dante"         "darkblue"      "darkbone"      "darkness"     
## [21] "darkslategray" "darkspectrum"  "default"       "denim"        
## [25] "dusk"          "earendel"      "easter"        "edit-anjuta"  
## [29] "edit-eclipse"  "edit-emacs"
```

We can use `knit_theme$set()` to set the theme.  For example, to set the theme to *fruit* we could run the following code:


```r
knit_theme$set("fruit")
```

Here's the link to find your favorite theme of all the <a href="http://animation.r-forge.r-project.org/knitr/">80 knitr highlight themes</a>.


