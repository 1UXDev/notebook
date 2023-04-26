# HTML 

## Labels and Inputs
* <label> + <input> usually come in pairs
* "name=" is required, "value=" is what is handed over to the server

```HTML
<label for="myInputID">Here will be your Input</label>
<input type="text" id="myInputID" name="InputName"/> 
```

* labels always needs "for=", inputs always need "name=" and "id=" that can be addressed by the 

```HTML
<label for="favSeason>Your Favorite Season</label>
<select name="favSeason" id="fav-season">
  <option value="">Select Value</option>
  <option value="summer">Summer</option>
  <option value="winter>Winter</option>
</select>
```

* * The first option with empty value does not return anything to the server

## Fieldset and Legend
* since form-elements are inline, they need to be wrapped by a block-ish element: Fieldset
* <legend> is a dedicated descriptor element

##Further Notes
* <form aria-labeledby="heading"> --> h2 on top of page with id="heading" is linked for screenreaders
* <fieldset aria-describedby="descriptionElementID"> s.o.
