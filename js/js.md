# js basics

## Primitive Datatypes
* undefined
* Null --> Empty value e.g. for variables to be filled later
* Boolean
* Number
* String
* BigInt --> avoid using this
* Symbol

() **Note**
Strings can be converted to numbers like this:
let a = "10"; // typeof = string
let b = +a; // typeof = number

an empty string returns a falsy value
arrays are also objects, thats why you check with isArray if something is an array

## Types of Variables
* var xyz => scopes to whole function it is in; 
<br> *also var can be hoisted (called before defined, because js puts it on top automatically, but it is bad practice because like this variables can be accidentally overwritten)*
* let xyz => scopes to immediate codeblock enclosed by {}
* const xyz

=> **whenever possible use const**

<details>
  <summary>Scoping difference var & let</summary>
  ```
        
        function run() {
        var foo = "Foo";
        let bar = "Bar";

        console.log(foo, bar); // Foo Bar

        {
          var moo = "Mooo"
          let baz = "Bazz";
          console.log(moo, baz); // Mooo Bazz
        }

        console.log(moo); // Mooo
        console.log(baz); // ReferenceError
      }

      run();
   ```
</details>`

´<script src="./js/index.js" defer></script>´

---------------------

Truthy: True, non zero numbers, non-empty strings
Falsy: 0, empty strings, Null, undefined



