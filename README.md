# Introduction to JavaScript

- Open your existing codespace (The one we used in the early part of the module) https://github.com/codespaces.
- In the terminal enter
```
git clone https://github.com/CHT2520-web-prog/javascript
```
- This will copy the contents of this repository into your codespace.

- Test you can view the page in a browser. It will be a simple HTML page, with some basic styling.

## Linking the HTML Page to the JavaScript File
- Paste the following `<script>` element into the page, just before the closing `<body>` tag to link the HTML page to the JavaScript file (app.js)

```html
<script src='js/app.js' defer></script>
```
- Refresh the page in the browser, right-click on the page and open the developer tools. You should see a `console.log` message saying 'Ready to do some JavaScript'. 
- Find the line of code in _app.js_ that is generating this message. It's inside the function `init()` which is called as soon as the JavaScript file has loaded.

## Working with Data
- Have a look at the top of the _app.js_. Note the two arrays of JavaScript objects, `filmsFrom2000s` and `filmsFrom2010s`.
- Inside the `init()` function, immediately after the first `console.log` message add code to display information about the first object in the `filmsFrom2000s` array:

```javascript
function init() {
   console.log("Ready to do some JavaScript");
   film = filmsFrom2000s[0];
   console.log(film);
   console.log(`The first film in the filmsFrom2000s array is ${film.title}`);
}
```
- View the page in the browser, the `console.log` message that should display 'The Incredibles'. 
- Next, still inside the `init()` function, add the following code to use a `forEach` loop to display the titles of all the films in the array

```javascript
   console.log("\nFilms from the 2000s:");
   filmsFrom2000s.forEach((film) => console.log(`${film.title}`));
```
- Again, test the page in the browser, make sure you understand what the `forEach` is doing. 
- Next, we'll filter this list of films, add the following code.

```javascript
filmsFrom2004 = filmsFrom2000s.filter((film) => {
    if(film.year===2004){
        return true;
    }
    return false;
});
    
console.log("\nFilms from 2004:");
filmsFrom2004.forEach((film) => console.log(`${film.title}`));
```

- Again, test the page.

### Test Your Understanding
How can you modify this block of code to:
- Change the first console.log message so it outputs 'The second film in the filmsFrom2000s array is Spirited Away. It was made in 2001'. Make sure you use the `title` and `year` properties of the object.
- Add an extra film to the array. Check you can output the film's details in the console 
- Modify the `filter` method so that all films made after 2002 are returned.

## Using the DOM
Instead of displaying the films in the console, let's display them in the HTML page. 

- Still inside the `init()` function, add the following code:

```javascript
//Grab hold of the <div> with the id of film-list-holder
const filmListHolder = document.querySelector("#film-list-holder");
//Delete the existing content of this element
filmListHolder.innerHTML = "";
//For each film create a <div> element
filmsFrom2000s.forEach((film) => {
    //Create a <div> element
    const filmDiv = document.createElement("div");
    //Populate the <div> with the film title
    filmDiv.textContent = film.title
    //Insert the <div> into the HTML page
    filmListHolder.appendChild(filmDiv);
});
```
- Test the page, you should find the films are now displayed in the HTML page. 

There is already a function in th epage `updateFilmList()` that does something very similar to this code. Comment out the code we have just added and call this function instead i.e.

```javascript
// //Grab hold of the <div> with the id of film-list-holder
// const filmListHolder = document.querySelector("#film-list-holder");
// //Delete the existing content of this element
// filmListHolder.innerHTML = "";
// filmsFrom2000s.forEach((film) => {
//     //Create a <div> element
//     const filmDiv = document.createElement("div");
//     //Populate the <div> with the film title
//     filmDiv.textContent = film.title
//     //Insert the <div> into the HTML page
//     filmListHolder.appendChild(filmDiv);
// });
updateFilmList(filmsFrom2000s);
```
Check this works, each film should be displayed as a hyperlink. 
Have a good look through the code in `updateFilmList()` to make sure you understand what it is doing. 

### Test Your Understanding 
- Can you display the film year alongside the title e.g. Finding Nemo (2001).


## Making Things Interactive

Add the following code in `init()` to select the decade hyperlinks.


```javascript
const decadeLinks = document.querySelectorAll(".decade-link");
decadeLinks.forEach((link) => {
        console.log(link)
    });
```
Check this works, you should be able to see the HTML elements displayed in the console. 

Note, how we used `querySelectorAll()` becuase there are multiple elements, and we use a `forEach` loop to display each element in turn. 

Next, we will make the links clickable by attaching an event listener.

Modify this block of code so it looks like the following:

```javascript
decadeLinks.forEach((link) => {
    link.addEventListener("click", ()=>{
      console.log(`Clicked a hyperlink`)
    });
});
```
Test this works. When the user clicks a hyperlink, a `console.log` message should be displayed. 

It might be nice to know which hyperlink was clicked, we can do this with the `event` object. Change the code to the following:

```javascript
decadeLinks.forEach((link) => {
    link.addEventListener("click", (event)=>{
      console.log(event.currentTarget.textContent)
    });
});
```

Test this works, the text of the hyperlink (either 2000 or 2010) should be displayed in the console.

Finally, let's call the `changeDecade()` function when one of the links is clicked. 

```javascript
decadeLinks.forEach((link) => {
    link.addEventListener("click", changeDecade);
});
```
Test this works, when the user clicks a hyperlink, the list of films should change.  
Have a good look at the `changeDecade()` function. The comments explain what each line is doing. 


### Test Your Understanding.

How can you update the `<h1>` element to display 'Here's a list of film from the 2000s' (or 2010s depending on which decade has been selected). You will need to: 

- Uncomment the line in `changeDecade()` that calls the function `updateFilmsHeading()`

```
//updateFilmsHeading(decade);
```
Create the function e.g. `updateFilmsHeading`. 

Inside this function:
- Select the `<h1>` element (use `queryselector`)
- Change the content of the `<h1>` element using the `decade` parameter. 
