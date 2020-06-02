## Installation

* For [node (via npm)](https://www.npmjs.com/package/rita/v/2.0.0-beta.6) (1.2mb)
* For [the browser](https://github.com/dhowe/rita2js/releases/download/v2.0.0-beta.6/rita-web-full.js) (1.4mb)
* For [the browser (no lexicon)](https://github.com/dhowe/rita2js/releases/download/v2.0.0-beta.6/rita-web-nolex.js) (.5mb)


<div class="section">
  <div class="category">
    <a href=""><b>RiTa</b></a><br/>
    <a href="RiTa/VERSION/index.html">RiTa.VERSION</a><br/>
    <a href="RiTa/addTransform/index.html">RiTa.addTransform</a><br/>
    <a href="RiTa/alliterations/index.html">RiTa.alliterations</a><br/>
    <a href="RiTa/concordance/index.html">RiTa.concordance</a><br/>
    <a href="RiTa/conjugate/index.html">RiTa.conjugate</a><br/>
    <a href="RiTa/evaluate/index.html">RiTa.evaluate</a><br/>
    <a href="RiTa/hasWord/index.html">RiTa.hasWord</a><br/>
    <a href="RiTa/isAbbreviation/index.html">RiTa.isAbbreviation</a><br/>
    <a href="RiTa/isAdjective/index.html">RiTa.isAdjective</a><br/>
    <a href="RiTa/isAdverb/index.html">RiTa.isAdverb</a><br/>
    <a href="RiTa/isAlliteration/index.html">RiTa.isAlliteration</a><br/>
    <a href="RiTa/isNoun/index.html">RiTa.isNoun</a><br/>
    <a href="RiTa/isPunctuation/index.html">RiTa.isPunctuation</a><br/>
    <a href="RiTa/isQuestion/index.html">RiTa.isQuestion</a><br/>
    <a href="RiTa/isRhyme/index.html">RiTa.isRhyme</a><br/>
    <a href="RiTa/isVerb/index.html">RiTa.isVerb</a><br/>
    <a href="RiTa/kwic/index.html">RiTa.kwic</a><br/>
    <a href="RiTa/pastParticiple/index.html">RiTa.pastParticiple</a><br/>
  </div>
</div>

## RiTa v2 API

```
RiTa
------------
RiTa.VERSION
RiTa.addTransform()
RiTa.alliterations()
RiTa.concordance()
RiTa.conjugate()
RiTa.evaluate()
RiTa.hasWord()
RiTa.isAbbreviation()
RiTa.isAdjective()
RiTa.isAdverb()
RiTa.isAlliteration()
RiTa.isNoun()
RiTa.isPunctuation()
RiTa.isQuestion()
RiTa.isRhyme()
RiTa.isVerb()
RiTa.kwic()
RiTa.pastParticiple()
RiTa.phones()
RiTa.pos()
RiTa.posInline()
RiTa.presentParticiple()
RiTa.pluralize()
RiTa.randomOrdering()
RiTa.randomSeed()
RiTa.randomWord()
RiTa.rhymes()
RiTa.sentences()
RiTa.similars()
RiTa.singularize()
RiTa.soundsLike()
RiTa.stem()
RiTa.stresses() 
RiTa.syllables()
RiTa.tokenize()
RiTa.untokenize()
RiTa.words()
```

```
RiTa.Grammar
------------
addRule()
expand()
expandFrom()
loadRules()
removeRule()
toString()
```

```
RiTa.Markov
------------
addText()
addText() // ??
completions()
generate()
probability()
probabilities()
size()
toString()
toJSON()
RiMarkov.fromJSON()
```


## RiTaScript

RiTaScript can be used as part of any grammar (via RiGrammar) or can be run directly using RiTa.evaluate() 


### Choice

```
The weather was (sad | gloomy | depressed).  ->  The weather was gloomy. 
| I'm (very | super | really) glad to ((meet | know) you | learn about you).  ->  I'm very glad to know you. 
```

### Weighted Choice
```
The weather was (sad | gloomy [2] | depressed[4]).  ->  The weather was depressed. 
```

### Assignment
Basic assignments do not have output, they simply create or update a symbol

```
$desc=wet and cold
The weather was $desc  ->  The weather was wet and cold 
```

### Inline Assignment

Inline assignments create/modify a symbol _and_ output its contents

```
Jane was from [$place=(New York | Berlin | Shanghai)]. $place is cold and wet. 
     ->  Jane was from Berlin. Berlin is cold and wet.

$place=(New York | Berlin | Shanghai)`<br/>`$place is cold and wet in winter. 
     ->  Berlin is cold and wet in the winter.
    
In [$place=(New York | Berlin | Shanghai)] it is cold and wet in winter. 
     ->  In Berlin it is cold and wet in the winter.
```


### Transforms

```
The group of boys (to run).conjugate().
How many (tooth | menu | child).pluralize() do you have?
How many (tooth | menu | child).pluralize().toUpper() do you have?

// Resolves choice without repeating
How many (tooth | menu | child).norepeat() do you have?

// Resolves choice in sequence
How many (tooth | menu | child).seq() do you have?
```

<!--
### Choice

| | | 
|-|-|
| The weather was (sad &#124; gloomy &#124; depressed). | The weather was depressed. |
| I'm (very &#124; super &#124; really) glad to ((meet &#124; know) you &#124; learn about you). | I'm very glad to know you. |


### Weighted Choice
| | | 
|-|-|
| The weather was (sad &#124; gloomy [2] &#124; depressed[4]). | The weather was gloomy. |

### Assignment

Basic assignments do not have output, they simply create/update a symbol
| | | 
|-|-|
|$desc=wet and cold||
|The weather was $desc|The weather was wet and cold|

### Inline Assignment

Inline assignments create/modify a symbol _and_ output its contents

| | | 
|-|-|
| `Jane was from [$place=(New York | Berlin | Shanghai)]. $place is cold and wet.` | `Jane was from Berlin. Berlin is cold and wet.` |
| `$place=(New York | Berlin | Shanghai)`<br/>`$place is cold and wet in winter.` | `Berlin is cold and wet in the winter.` |
| `In [$place=(New York | Berlin | Shanghai)] it is cold and wet in winter.` | `In Berlin it is cold and wet in the winter.` |


```
Jane was from [$place=(New York | Berlin | Shanghai)]. 
$place is cold and wet in the winter.

$place=(New York | Berlin | Shanghai) 
$place is cold and wet in the winter.

$place=(New York | Berlin | Shanghai) is cold and wet in the winter.

In [$place=(New York | Berlin | Shanghai)], it is cold and wet in winter.

In [$place=(New York | Berlin | Shanghai) it is cold and wet in winter].

```
-->
### Symbols

```
$desc=dark and gloomy
The weather was $desc
```
&nbsp;&nbsp;&nbsp;&nbsp;or 
```
/* 'desc' defined in JS */
The weather was $desc
```

### Conditionals

```
// 'desc' can be defined in JS or RS */
{desc='party'} The party was happening
{desc='party', user=$john} The party was happening and John was wearing $John.color.
```
<!--
### Conditionals: If-else

```
{adj='positive'} The party was happening :: The party was not happening.
```
&nbsp;&nbsp;&nbsp;&nbsp;or 
```
{adj='positive'} The party was happening.
{adj!='positive'} The party was not happening.
```
<!--
### Labels
```
#Opening {
 The Fellow will be expected to teach one course. Apart from focusing on their own research and \
 teaching one course, the Fellow will be expected to give a presentation of their scholarship at the \
 Institute. The Fellow will also be expected to participate in the intellectual life of the community.
}

$Opening=(
 The Fellow will be expected to teach one course. Apart from focusing on their own research and \
 teaching one course, the Fellow will be expected to give a presentation of their scholarship at the \
 Institute. The Fellow will also be expected to participate in the intellectual life of the community.
)
```
-->

&nbsp;

## Developing
To build the library and run tests:
```
$ yarn install 
$ yarn compile
$ yarn test
```
&nbsp;
