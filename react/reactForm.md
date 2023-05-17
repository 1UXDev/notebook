# States & Forms in React

## Controlled Component 
We changed component to a **controlled component** by adding value that we also have in search term, then we added value prop & onChange Handler, that calls setter setSearchTerm with the event-targets-value as Argument

```jsx
connect value attribute to whatever state of search term
input value = {searchTerm}
onChange={(event)=>{		// call setter-function from state
	setSearchTerm(even.target.value)
}}  // onChange is similar to onClick, updates search term in State
```
--> (now input field is also editable)

* **Problem:** 
<br> Components (SearchForm, SearchResult) are siblings and not one children of another, thus we need to „lift up“ Props into the common parent component 


„SearchTerm“_____->_____on Change_____->_____"Search Term"_____->_____"Search Term" 
from SearchForm____________________________over App (parent)______to SearchResult (sibling of SearchForm)
                                                            
<br>

