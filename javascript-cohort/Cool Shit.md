# Tailwind CSS

basically an easier way of styling, has some downsides of it but good to know
follow the installation guide in the docs

**4 IMPORTANT THINGS IN ANY FRONTEND FRAME** - 
1. Flex
2. Grids
3. Responsiveness
4. Background & Text Color, *Hovers*

- Tailwind follows mobile-first, means what you code normally will appear on all screens that way, if you use a breakpoint then uss point ke upar wale ke liye likhte ho tum code
- you can refer to a tailwind cheat sheet instead of looking up on docs
- to get a color from a screenshot or image, upload image online and pick color
- if you are using figma, you can simply get all the properties
- you can use svgs in tailwind ( check the docs ), **HEROICONS** is cool af
## Flexbox

**in raw :**
```css
display : flex;
justify-content : space-between;
```
or
```jsx
<div style={{display : "flex", justifyContent:"space-between"}}
```

**in tailwind :** you just need to add classes to the elements
```jsx
<div className="flex justify-between">{content_here}</div>
```

you can get the classes from tailwind docs


## Grids

**in raw :**
```css
display: grid;
grid-template-columns: 1fr 2fr; /* Two columns, first column takes 1 part, second column takes 2 parts */

/*or we can do this*/
grid-template-columns: repeat(3, 100px); /* Three columns, each 100px wide */ 


grid-gap: 10px; /* Gap between grid items */
```


**in tailwind :**
for equal widths - 
```css
className="grid grid-cols-3"
```

for unequal widths -
```jsx
<div className="grid grid-cols-12">
	<div className="col-span-3"></div>
	<div className="col-span-5"></div>
	<div className="col-span-4"></div>
</div>
```

## Responsiveness
**in raw :**
```css
@media (min-width : 768px) {}
``` 
and then you define your css

**in tailwind :**
[you can read here](https://tailwindcss.com/docs/responsive-design)


## Colors
there are many shades of each color specified in tailwind
here's how to implement : 
```jsx
className="bg-green-500 text-red-500"
```



## Basic walkthrough to clone a frontend
1. create components first
2. then glue them together
3. add further styling


## Creating custom shit
in your tailwind config,
go in extend and type
```js
colors : {
	blue : {
		700 : "#146eb4"
	}
}
```




# Storybook.js
it is used to create components and test them without putting them in the main app
can be used to open source project components as well
the dev can then choose components and add them to the main app



# Material UI ( MUI )
- straight components out of the box to paste in your code
- issue : very hard to customize
- slowly dying
- great if you dont want to design and want a fast design for hackathons or sum' shit 

# More UIs
- Radix UI
- Shadcn UI
- Aceternity UI
- **Dub.sh**
- **GSAP FOR ANIMATORY TYPE STUFF**
