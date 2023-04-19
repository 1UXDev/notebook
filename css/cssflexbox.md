#flexbox notes
*hier stehen nur Dinge ddie ich mir in bezug auf flexbox merken will, das ist keine Abhandlung die Flexbox von grundauf erklärt*

## Parent Properties
| Property | Value | Descr |
|:-----|:-----|:-----|
|justify-content|`flex-start, flex-end, center , space-between, space-evenly, space-around`|positioning along the **main** axis, space between means there is only flex space *between* the items, flex around means there is flex space *around* the items|
|align-items|`flex-start, flex-end, center`|entlang der querachse positionieren|
|flex flow|´column wrap´| kombiniert flex-direction mit flex-wrap|
|align-items|`stretch flex-start/end, center, baseline` und weitere|wie sind die Children aneinander aligned? baseline= alle Texte sind aligned, stretch = alle heights orientieren sich am parent-container|
|align-content|'flex-start/end, stretch, center, space-between/around'|Wie sind die child-rows bei flexwrap gespaced?|


## Child Properties
| Property | Value | Descr |
|:-----|:-----|:-----|
|order| 3 | Ähnlich z-index, höhere Zahl = Weiter vorn, auch negativwerte möglich|
|flex-grow| 4 | verbreitert das Element n-fach im Vergleich zu den Anderen flex-children. Wenn alle "1" = gleichmäßig veteilt (hier ist keine Einheit wie "px" o.ä. notwendig)
|flex-shrink | 2 | Fall notwendig, kann das Element n-mal kleiner werden als die Anderen|
align-self|`auto | flex-start | flex-end | center | baseline | stretch`|Wie soll sich das Element im Container ausrichten?|






![link to Spiced Dokument](https://github.com/spiced-academy/chicory-web-dev/tree/main/sessions/css-flexbox)
![CSS TRcisk Cheatsheet](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
