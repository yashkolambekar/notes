## Installation

To install Tailwindcss in your react Project, go to Tailwindcss.com and go to installation page, there we can select the 'Vite' from Framework guides.


## Philosophy

Tailwind css uses the concept of Utility classes, which means, all the css is given using classes. Basically you are writing css but not in a css file, we are using classnames. 

## Colors

In tailwind, we have some default colors, with various shades of them which have unique name, the shades are named like `green-50`, `green-100`, `green-200`, - , `green-900`, `green-950`. 50 being closer to white and 950 being closer to black.

To add our custom colors inside the tailwind css project, we can either edit the tailwind config and add a `colors` object to the `extend` object with all our necessary colors inside it like this

```js
theme: {
    extend: {
      colors :{
        saffron : {
          100: "#FF6714",
          200: "#FF6700"
        }
      }
    },
  },
```

or we can write a custom class in the classnames like `border-[#FF6714]` These are called arbitary values


## Custom Classes and CSS

```CSS
/* index.css */

@layer base {
    div{
        @apply bg-red-400;
        max-width: 50%;
    }
}
```

In the above example, we are applying one tailwind class (bg-red-400) and one custom css property (max-width) to the div tag, it will be applied to all the divs.

## Typography

Font-size: `text-xs`, `text-sm`, `text-base`, . . .


## Flex

