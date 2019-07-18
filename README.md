# universe_background_cssGrid
A background simulating the univese for CSS grid 

### Motivation for creating this tiny universe
I couldn't find online, so I coded it. I took me a couple of hours, but hopefully this can help on your projects. 

## Steps:
- create a grid item with the id name "universeDisplay" (HTML)
-  create a svg item inside the grid 
```html
  <div id="universeDisplay">
                    <svg id="svgEL" >
                    <!-- cirles go here -->
                    </svg> 
  </div>
```
- copy and past the JS file 
```javascript
// set up 
/* Stars algorithm base on a size of the grids */

// 1- get the pixel size of your grid

var universeIdName = "universeDisplay";

//setting the size of the svg 
var svgCanvas = document.getElementById("svgEL");

svgCanvas.setAttribute("height", document.getElementById(universeIdName).offsetHeight);
svgCanvas.setAttribute("width", document.getElementById(universeIdName).offsetWidth);

function sizeChanged() {
  svgCanvas.setAttribute("height", document.getElementById(universeIdName).offsetHeight);
  svgCanvas.setAttribute("width", document.getElementById(universeIdName).offsetWidth);
}
window.onresize = sizeChanged;

/* inserting the stars into the empty univeser" */

var stars = new Array();
var nStars =  750;

//first 100 stars are huuuuugeeeeeeeeeeee
for (let i = 0; i < 100; i++) {
  stars[i] = document.createElementNS("http://www.w3.org/2000/svg", "circle");
  stars[i].setAttribute("cx", Math.floor(Math.random() * document.getElementById(universeIdName).offsetWidth) + 1);
  stars[i].setAttribute("cy", Math.floor(Math.random() * 2000) + 1);
  stars[i].setAttribute("r", 2);
  stars[i].setAttribute("fill", "white");

  svgCanvas.appendChild(stars[i]);
}

// the rest planets are white dots of size 1 
for (let i = 100; i < nStars; i++) {
  stars[i] = document.createElementNS("http://www.w3.org/2000/svg", "circle");
  stars[i].setAttribute("cx", Math.floor(Math.random() * document.getElementById(universeIdName).offsetWidth) + 1);
  stars[i].setAttribute("cy", Math.floor(Math.random() * 2000) + 1);
  stars[i].setAttribute("r", 1);
  stars[i].setAttribute("fill", "white");

  svgCanvas.appendChild(stars[i]);
}

//5 earth size 
nStars+=5;
for (let i = nStars -5; i < nStars ; i++) {
  stars[i] = document.createElementNS("http://www.w3.org/2000/svg", "circle");
  stars[i].setAttribute("cx", Math.floor(Math.random() * document.getElementById(universeIdName).offsetWidth) + 1);
  stars[i].setAttribute("cy", Math.floor(Math.random() * 2000) + 1);
  stars[i].setAttribute("r", 1);
  stars[i].setAttribute("fill", "rgb(48, 161, 226)");

  svgCanvas.appendChild(stars[i]);
}


// creating some suns to illuminate 
// the universe
nStars+=Math.floor((nStars * .05));
for (let i = 1 + nStars - Math.floor((nStars * .05)); i < nStars ; i++) {
  stars[i] = document.createElementNS("http://www.w3.org/2000/svg", "circle");
  stars[i].setAttribute("cx", Math.floor(Math.random() * document.getElementById(universeIdName).offsetWidth) + 1);
  stars[i].setAttribute("cy", Math.floor(Math.random() * 2000) + 1);
  //stars[i-1].r.baseVal.value == "1" ?  stars[i].setAttribute("r", 1) : stars[i].setAttribute("r", 2);
  i % 2 == 0 ?  stars[i].setAttribute("r", 1) :  stars[i].setAttribute("r", 2);
  stars[i].setAttribute("fill", "yellow");
  svgCanvas.appendChild(stars[i]);
}


console.log(nStars);
console.log(stars.length);

// random movement for the stars of the universe 

var poNe = Math.floor(Math.random() * 3) - 1;
var move = Math.floor(Math.random() * 5) + 0;
var iterate;
var steps = 2;
var slope = new Array();
slope[0] = Math.floor((Math.random() * 3) - 1);
slope[1] = Math.floor((Math.random() * 3) - 1);
slope[2] = Math.floor((Math.random() * 3) - 1);
slope[3] = Math.floor((Math.random() * 3) - 1); 



function movingStars() {
  let cx ;
  let cy;

  for (let i = 0; i < Math.ceil(stars.length / 5); i++) {

    slope[0] = Math.floor((Math.random() * 3) - 1);
    slope[1] = Math.floor((Math.random() * 3) - 1);


    move = Math.floor(Math.random() * steps) + 0; //move 0 to 2 spaces 
     cx = stars[i].cx.baseVal.value;
     cy = stars[i].cy.baseVal.value;
    stars[i].setAttribute("cx", cx + (move * slope[0]));
    stars[i].setAttribute("cy", cy + (move * slope[1]));
  } 

  // 1/5 of the stars move opposite to the previos one
  iterate = stars.length / 5 + stars.length / 5;
  for (let i = Math.ceil ( (stars.length / 5)) ; i < iterate; i++) {

    slope[2] = Math.floor((Math.random() * 3) - 1);
    slope[3] = Math.floor((Math.random() * 3) - 1); 

    move = Math.floor(Math.random() * steps) + 0; //move 0 to 5 spaces 
     cx = stars[i].cx.baseVal.value;
     cy = stars[i].cy.baseVal.value;
    stars[i].setAttribute("cx", cx + (move * slope[2]));
    stars[i].setAttribute("cy", cy + (move * slope[3]));
  }

}

var moveStars = setInterval(movingStars, 100);

/* Button */
function stop(){
  clearInterval(moveStars);
}

function reset(){

  for(let i = 0; i<stars.length;i++){
    stars[i].setAttribute("fill", "black");
  }
  
console.log(nStars);
console.log(stars.length);

  
}
```
