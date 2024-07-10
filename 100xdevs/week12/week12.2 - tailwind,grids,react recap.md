- hands on learning React + Next.js 
- building a yt clone in React from scratch using Tailwind.
- things to know in a frontend framework:
	- flex 
	- grids
	- responsiveness
	- background color, text color, hover
- usually enough to build the clone of any other framework.
- flex:
	- want div to appear right next to each other , need to use flex , as by default flex takes full width.
	- adding display: flex , appear side by side.
- justify-content tells that given the children are in the same line and we are using flex, how should we position them.
- flex-start, flex-end will start and end of the line.
	- only take as much space needed.
	- ![[Screenshot 2024-04-03 at 6.07.36 AM.png]]
- most of the times used in space-between or center with flex. flex-start is the default.

- With Tailwind:
	- basically CSS Framework that we import in our js.
	- put className as flex and add justify-between.
	- bg-red-800, p-2 etc is how we write the code with tailwind.
	- space-between -> justify-between ; to do flex-end -> justify-end 

### Grids in TW:
- another way to put 3 elements in the same row.
- grid grid-cols-3 ; to make a grid of 3 cols and all equally distributed.
- can also create grid's with different widths.
- In TW (with unequal width):
	- assuming the viewport split into 16 parts, how much should each part take.
	- col-span-5 , cols-span-5, col-span-2 , to create unequal widths for the grids.

### Responsiveness:
- very important in most websites.
- change the number of grid children that we see as the windows increase/decrease.
- 5 breakpoints have been defined:
	- <= 640px, user in sm breakpoint
	- <= 768px, user in md breakpoint
	- <= 1024px, used in ls breakpoint 
	- <= 1280px, used in xl breakpoint
	- <= 1530px, used for 2xl breakpoint
- need to conditionally render the site as per size.

### Working Mobile First:
- by default , tailwind works in a mobile first approach, and unprefixed utilities take effect on all screens, while prefixed utilities takes place on specified utilites and above.
- CSS: text-center , sm:text-left
	- implies that by default the text will be center and text-left will take effect when it crosses the sm breakpoint, else  the text-center will be used.

### color system:
- they have an inbuilt color system , can also define these ourselves and people use them for their use.
- every color has a 50 the shade to a 950th shade.


### font-size , bg-color and font-color:
- font-sm,font-xl, have predefined sizes, to change these change in the tailwind.config.js 
- border-radius -> adding radius to the div / containing element. rounded-sm, rounded-lg etc.
- bg-color -> to add background color 

### yt-clone:
- make individual components first and then glue them together.
- appbar, card, buttons and then created left sidebar and then glue them together.
- 