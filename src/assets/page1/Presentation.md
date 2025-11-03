## Svelte Presentation

React is one of many frameworks which could be used for web app development, here is a brief introduction to an alternative which is popular with developers.

Most of the information here is drawn from the [Svelte Website](https://svelte.dev/) and if this taster is appealing you should follow up by going through the full tutorial sequence on that site.

![Slide1](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide1.PNG)

Presentation front page with presenter names and appropriate theme.

![Slide2](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide2.PNG)

React initially seems like a single framework so it may initially look as though Svelte is a framework and SvelteKit is some kind of development environment.

However, Svelte is actually a compliler to javascript modules which produces a very small code footprint.  SvelteKit is the framework.

Come to think of it React is not sufficient on its own you customarily include React Dom and may need other elements such as React Router.

### Svelte

![Slide3](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide3.PNG)

The Svelte website has a good sequence of tutorials presented within an interactive online editor.

The four sections discuss basic and advanced Svelte and then basic and advanced SvelteKit framework.

I hope that by following quickly through the first few sections of the svelte tutorial and the first few of the basic SvelteKit we can gain enough awareness of the syntax to follow through the operation of the svelte demo application.

![Slide4](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide4.PNG)

First the svelte syntax.  The page has a script section and an html like section.

A script variable, name, can be passed as a property into the presentation section.  Since it is a string, string functions can be applied to it.

![Slide5](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide5.PNG)

Variables can also be included as properties in the attributes of an html element.

Where the variable name is chosen to match the attribute name a short form syntax can be used.

![Slide6](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide6.PNG)

Style tags placed in a file apply their style to the scope of the file.

![Slide7](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide7.PNG)

If a paragraph is imported into the page from a separate file, it does not pick up the style from the importing files style tags.

![Slide8](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide8.PNG)

Whilst React would try to interpret `<strong/>` as JSX, svelte does not interpret this by default so the result of line 5 is to print the text literally.

The inclusion on line 6 of @html causes the html to be interpreted and produce bold text.

![Slide9](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide9.PNG)

This script provides a counter defined outside a function which increments it.   No need to use hooks at this point.

The button element has an on attribute for mouse click which will call the increment function when the mouse is clicked.

Line 11 is a standard javascript short format if then else structure which ensures that if the count is exactly 1 the button will display the singular term of 'time'.

![Slide10](/IT_Coursework1_OnlineTutorial/src/assets/page1/images/Slide10.PNG)

The $: syntax introduces a reactive variable which will result in an update of the display when it is changed.  This maintains the value of doubled as count * 2.  Note that the $: syntax is not needed in the display line 15.