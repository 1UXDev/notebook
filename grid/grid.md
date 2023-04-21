# Grid Basics

* Flexbox for linear layouts, where content dictates the layout flow
* Grid is great for more complex, less linear layouts

<br>

-----------------------

<br>

## Parent container usually contains
display:grid; 
gap: N px;
grid-template: Nfr Npx N% / repeat(3,1fr) \[define rows / define columns\]
* you could also write it as grid-template-columns:; & grid-template-rows:; but thats just verbose.
align-items // justify-items  => place-items: <align> <justify>     --> wichtiges Argument ist **end**
*justify content platziert inhalte des grids an Anfang (start), ende (end) odr andere stellen (space-around, stretch, center, space-between, space-evenly...)


### Repeat can be quite elaborate
* with grid 1fr, which means one fraction
* you can also use repeat(3, 1fr) or could also be used like repeat(8, 12,5%) \[=100%\]
* repeat (auto-fit, minmax(min-content, auto)) 

### Auto-fill & Auto-fit 
* auto-fill FILLS the row with as many columns as it can fit.
* auto-fit FITS the CURRENTLY AVAILABLE columns into the space by expanding them so that they take up any available space.

## Child container usually contains

### grid area
grid-area: 1 / 1 / 3 / 5  \[row begin, column begin, row end, column end\]
<br> *one could also use trhe more verbose version which is grid-row: 3 / 4; grid-column: 1 / 5;*

### minmax
minmax(minvalue, maxvalue)
* --> can also be stacked with repeat, see above

### auto-flow
grid-auto-flow: row // column // dense (dense packt das grid möglichst dicht ohne "löcher" column füllt vorrangig die columns auf)

### align & justify items
Items können sich mit justify-self oder align-self auch selbst platzieren. --> place-self (start, end, left, center, ...)

--------------------
## Implicit grid
es gibt ein implicit grid (wenn Dinge im Grid existieren aber keine spalten / Zeilen da sind um sie zu halten (?))
grid-auto-columns oder grid-auto-rows werden genutzt um diese zu definieren,
wenn es ein grid gibt wird die neue Auto-Zeile/Spalte einfach dran gehangen 
