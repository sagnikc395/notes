## landing page using HTML and CSS

- Making the zerodha landing page using HTML and CSS.
- Add styles , spacing and to make different shadows and box imaging and cleaner text and a button that has the given color.
- part3 -> add some js, create something new,create a returns calculator where the person has 3 calculator and the number of years they are going to put in and the expected outcome. i.e portfolio returns calculator.

### Browser

- Render webpages i.e HTML/CSS and JS.

- goal of a website is to allow a person to talk from one website to another website.

- Industry uses:

  - html -> very minimal
  - css -> minimal
  - js -> heavy

- HTML/CSS and JS files gets rendered -> goal of the browser is to get hit on a specific server, hit on the server and render it back on the screen.

- anyone can build a browser , they just need to follow a given specification.
- if our browser gets some HTML -> it should render the website inside the window of the browser.

### what purpose do HTML/CSS/JS Serve ?

- for most basic purposes, browser only understand HTML/CSS and JS to provide all the funcitonality to provide services.
- and these 3 services are all they need to render the websites(99%+)
- some may require webassembly (out of scope for now!)

## HTML jargon

- defines the structure of the website.
- what should be places after what, before what etc.
- jargon that we need to know of:

  - tags
  - attributes

- popular HTML tags:

  - \<html>
  - \<head>
  - \<title>
  - \<body>
  - \<div> / \<span>
  - \<h1> ... \<h6>
  - \<p>
  - \<img>
  - \<a>
  - input
  - \<button>
  - \<b> /<i>
  - \<center >

- even without any html tag we can write the content, but with tags we can create structure.

- \<div> is the most popular tag -> take 1 full width of your page. It more , then it will just overflow into the next line.

- \<html> , \<head> \<body> etc. are high level tags that are good to know for structuring the body and the actual content goes into body and head has metadata and import external scripts.

- div takes up all the space in the given line.
- to structure this between structurally and on the same line, we can use the span tag i.e in the inner children
- p and div are alsmost same .
- can change the default style of a tag via css.

- for making navigation use a tag , target= \_blank makes the blank search.
- b is for making your content as bold, i is for italic text.

- button tag lets us create a button, the pointer and color changes -> natively they look pretty ugly in HTML.

- buttons need some functionality associated with them , when user do onclick, onhover etc.

- input tag is to get user input

- any website is just made up of a bunch of tags and has recursive patterns of tags and items inside.
- no end of the amount of tags we can learn, can learn them over time

### Attributes:

- src, href ,onclick ,id etc are called attributes of a tag.
- extra things that we can pass onto the tags.
- some common ones:
  \<img src="">
  \<a href=" "></a>
  \<button onclick="">
  \<input id="username">

-

## CSS Basics

- made for styling a webpage -> colors,font-sizes,bg colors,
- used for positioning things on the page.
- how to add styles ?

  - add a style attribute to the tag.

- common styling attributes(CSS is huge, these are what are most frequently used):

  - color
  - background
  - border-radius
  - border
  - padding / margin
  - box-shadow

- padding -> to pad the div with some extra space.
- border,border-radius -> to add border and colors
- background -> to add background colors
- color -> text color
- margins and padding have a very subtle difference between them.

  - to add space within the div it is padding ,
  - to add space outside the div it is margin

- box-shadow -> very similar to a div, and allows us to add a shadow to a box.

  - requires 3 pixels gradient color and one color.
  - shadows are tweakedable via changing the parameters.
  - First Parameter -> direction towards which the shadow should go towards.(left or right)
  - generally as a developer, we get a figma file and need to copy the css on our website.

- generally enought to build basic loading page.

### how to add spaces ?

- divs always take up all the space available horizontally, spans only take up as much space as needed.
- how to make divs that only take the space they need ?

- Dumb Way:

  - use the float property -> the span we want floated to the right , add float:right, puts it to the right of the specific div.

- Ideal way of Doing this i.e to position element is to use Flexbox properties:
  - display:flex , tells that we are going to use flexbox and the children dont need to use all the width they need, but they need to be right next to each other.
  - justify-content -> to place where to keep the items flow, default value is start, can do end,center etc.
  - can also position equally by controlling the space -> space-between
- flexbox is the best way to position elements, other ways include absolute, floating etc.

- space-between -> all the children are equally spaced.
- flexbox only works for the immediate children.

  - so for applying in the components near to us , rather than on the parent one.

- gap to add gap between children components.
