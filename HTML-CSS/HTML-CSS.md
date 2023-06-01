 # HTML and CSS

 ## HTML

Hypertext Markup Language. It is a standard markup langauage for creating web pages. We use HTML to structure a webpage and its content. 
While HTML is a language, it is not considered a programming langauge, because it is used for the structure of a webpage and doesn't involve the process of doing something. HTML files end with the `.html` or `.htm` extension. 

How does it work: a web browser reads the HTML file and renders its content so that users may view the page. 

*Markup language: a text-encoding system, consisting of a set of symbols inserted in a text document to control its structure, formatting, or the relationship between its parts. Examples of commonly used markup languages are: HTMl, XML (eXtensible markup language), SGML (standard generalized markup language)

## HTML Elements and Tags

HTML documents are comprised of a series of elements, which are represented by opening and closing tags. An element is everything from teh starg tag to the end tag, including the content, attributes, and even other elements contained inside those tags. 
A tag is the opening or closing entity. for example `<p>` and `</p>` are tags while `<p> This is a paragraph</p>` is an element.

Block elements: 
Always starts on a new line, and the browser automatically adds some space (margin) before and after the element - always takes up the full width available. For example `<div>` and `<p>` are block elements.

Inline elements: 
Does not start on a new line - takes up only as much width as necessary. For example, `<span>` is an inline element used for grouping text or elements.

Some examples of commonly used tags are: 
- `<div>`: used to block part of the webpage, takes up the width of the avaiable screen, can be used to separate page into blocks or sections
- `<p>`: for creating paragraphs
- `<img>`: for images
- `<html>`: the root element that defines the whole HTML document

## Attributes

All HTML elements can have attributes. They provide additional information about the element and are always specified in the start tag. They usually come in name/value pairs like `name=value`.
They can set the style, layout, other information of the HTML element. 

Common attributes: 
- href: specifies the URL for a hyperlink `<a>` tag
- src: specifies the path for an image
- width: specified width for an image
- height: specifies height for an image
- class: specifies a class name for an HTML element
- style: used to add inline CSS to a specific element
- id: specifies an id for an HTML element

 ## CSS

 Cascading Stule Sheets. A language for styling HTML documents by specufying certain rules for layout and display in key/value pairs.
 Style Sheets are a simple and powerful method of allowing attachment of rendering information to HTML documents. 
 It used to style the webpages by setting background-color, font color, font size, font family, etc.

 CSS Box Model: a box that wraps around every HTML element that consists of margins, borders, padding, and the content itself.

 ![image](https://th.bing.com/th/id/R.c4c5be4231646aa2336d946629c08f09?rik=1l%2ft6R0CgxXcpg&riu=http%3a%2f%2fhelicaltech.com%2fwp-content%2fuploads%2f2016%2f04%2fbox-model.jpg&ehk=82%2bWQeHPqqhDpJvTBfQWrg5oul8iS88jYHHer0grDjw%3d&risl=&pid=ImgRaw&r=0)

- Content: the content of the box, where text and images appear
- Padding: clears an area around the content
- Border: a border that goes around the padding and content
- Margin: clears the area outside the border

There are 3 ways to inject CSS into our HTML pages: 
- External: using an external style sheet with the .css file extension using the `<link>` element. Add this link i the `<head>` section of the HTML doc
- Internal (embedded): added using `<style>` element
- Inline: use to apply a unique style for a single element. Add the style attribute to any relevant element. For example: `<h1 style="color:blue;text-align:center;">This is a heading</h1>`

Inline style has the highest priority, wand will override internal and external styles.

 ## CSS Selectors

A pattern used to select and taeget specific HTML elements within a document. We use it to apply style and formatting to those selected elements.
CSS selectors are based on the elements' tag name, class ID< attributes, and its relationship with other elements.

Commonly used CSS selectors: 

- `#id` 
- `.class`
- `element` 
- `[attribute="value"]`
- `element > element`: Child selector - selects all the elements that are the children of a specified element


