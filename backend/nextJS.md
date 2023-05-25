# NEXT JS
* helps with routing, react is a SPA, with next we can use different pages
* **Serverside renders everything** and sends only html css to the user (+ additional things if necessary)

Filesystem Routing
* whenever in the "pages-folder" (e.g. about.js) will be localhost:3000/about by default 
* instead of using single img, you use a component that will do optimization on image 

npx create-next-app@latest myApp

in `_app.js import globals.css to pass it to the whole app
Home.module.css is for the homepage

## create new page
* simply create new page, e.g. about.js
* localhost:3000/about will now show the page
* React route is not necessary here

<br>

## Components

### Link component
* Links items without having to reload
* "Link" has to be imported as default from next
* if you want to style it, you can address it in CSS as a-tag

### img component
* will compress images and optimize to user device
* "Image" has to be imported as default from next
* if you define width or height in the "html", you have to define both
* if we use images from "outside", in nextconfig.js we have to add the external source to "allowed" sources in domains{images:[a.com, b.com, ...]}

<br>

### Additional Notes
* if babel error after project setup, replace eslintrc.json content with 
```jsx
{
  "extends": ["next/babel","next/core-web-vitals"]
}
```
* pages folder needs to be named "pages", otherwise next-routing will not work
* API-Folder is basically the backend (e.g. /api/hello returns a json)

<br>

<br>

--------------

<br>

