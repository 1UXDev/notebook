# js & forms

## Access content in form fields
* Default Behaviour: submit => Browser tries to reload page with appended parameters: "? in Url for query string
* AddEventListener and **event.preventDefault()** so it is not submitted on buttonclick or enter in an input field 

### Step-by-Step Approach
1. get the target (the form): `const form = event.target`
2. get the elements in the form: `const elements = form.elements`
3. get the value: const values = `elements.firstName.value`
* or in one line: `event.target.elements.firstName.value`
* "event.target" => accesses the "target" of the eventlistener (form) & returns the form elements (but only returns the "natural" form elements like input, button, etc.)

### Data Object
* FormData() Object constructs Key-Value-Pairs(-Object) to represent everything in the form
1. `const form = event.target` // get the form element
2. `const formData = new FormData(form)` //get the data in a FormData-Object
<br>&emsp; *2.1 &emsp; console.log(FormData) // shows that this Object is not a "classic" Object*
<br>&emsp; *2.2 &emsp; formData.get("firstName") would get the Value from the Object*
3. **const data = Object.fromEntries(formData)** // transforms it to regular Object

## Other Methods
* Post-Requests - in the HTML it could also use GET ...

-------------------------------

## Handling user Inputs
* Data validation: check if data requirements apply (type, structure, range, etc.)
* Inpute Attributes like `minlength ="3"` => errormessage tells user the new requirement
* Data Vlaidation happens twice: in the front-end for the user and in the server later-on
* for input fields use event "input", for checkboxes and radios "change" may be better
