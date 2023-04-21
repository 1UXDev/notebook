# Grid Basics

* Flexbox for linear layouts, where content dictates the layout flow
* Grid is great for more complex, less linear layouts

<br>

-----------------------

<br>

Main { 
display:grid; gap: 12px; grid-template-columns:200px 200px 200px;
}

*you can also use 1fr, which means one fraction
*you can also use repeat(3, 1fr)

Repeat funktion repeat(8, 12.5%)
repeat (auto-fit, minmax(min-content, auto)) 
* auto-fill FILLS the row with as many columns as it can fit.
* auto-fit FITS the CURRENTLY AVAILABLE columns into the space by expanding them so that they take up any available space.


grid-template-columns // grid template-rows
-> grid-template: 20px 1fr 10% / repeat (3, 1fr);

grid-row: 3 / 4;
grid-column: 1 / 5;

grid-area: 1 / 1 / 3 / 5

minmax(minvalue, maxvalue)

grid-auto-flow: row // column // dense (dense packt das grid möglichst dicht ohne "löcher" column füllt vorrangig die columns auf)

--------------------
es gibt ein implicit grid (wenn Dinge im Grid existieren aber keine spalten / Zeilen da sind um sie zu halten (?))
grid-auto-columns oder grid-auto-rows werden genutzt um diese zu definieren,
wenn es ein grid gibt wird die neue Auto-Zeile/Spalte einfach dran gehangen 

------------
align-items // justify-items  => place-items: <align> <justify>     --> wichtiges Argument ist **end**

Items können sich mit justify-self oder align-self auch selbst platzieren. --> place-self (start, end, left, center, ...)

--------------

justify content platziert inhalte des grids an Anfang (start), ende (end) odr andere stellen (space-around, stretch, center, space-between, space-evenly...)
