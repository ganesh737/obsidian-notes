# HTML

TOC

## Syntax

### Sections of code

HTML5 allows for below tags to facilitate a more descriptive page and makes the page easier for Search Engine Optimizations(SEO) and accessibility -

main, header, footer, nav, video, article, section

### Doctype

You tell the browser this information by adding the ```<!DOCTYPE ...>``` tag on the first line, where the ```...``` part is the version of HTML. For HTML5, you use ```<!DOCTYPE html>```.

```html
<!DOCTYPE html>
```

### Head


### Body

#### Heading

```html
<h1></h1>
<h2></h2>
<h3></h3>
<h4></h4>
<h5></h5>
<h6></h6>
```

#### Paragraphs

```html
<p> adasfdasf </p>
```

#### Commenting

```html
<!-- sahfdaskjfhsd -->
```

#### Images with Alternative Text

```html
<img src="https://www.freecatphotoapp.com/your-image.jpg" alt="A business cat wearing a necktie.">
```

#### Links

##### External Pages with Anchor Element

```html
<a href="https://freecodecamp.org">this links to freecodecamp.org</a>
```

##### Internal Sections with Anchor Element

```html
<a href="#contacts-header">Contacts</a>
...
<h2 id="contacts-header">Contacts</h2>
```

##### Dead Links 

```html
<p>Click here to view more <a href="#" target="_blank">cat photos</a>.</p>
```

#### Lists

##### Unordered List

```html
<ul>
  <li>milk</li>
  <li>cheese</li>
</ul>
```

##### Ordered List

```html
<ol>
  <li>milk</li>
  <li>cheese</li>
</ol>
```


#### Inputs

##### Text

```html
<input type="text" placeholder="this is placeholder text">
```

#### Forms

##### Form Section

```html
<form action="https://freecatphotoapp.com/submit-cat-photo">
    <input type="text" placeholder="cat photo URL">
</form>
```

##### Submit Button

```html
<form action="https://freecatphotoapp.com/submit-cat-photo">
    <input type="text" placeholder="cat photo URL">
    <button type="submit">Submit</button>
</form>
```

##### Required Fields

```html
<form action="https://freecatphotoapp.com/submit-cat-photo">
    <input type="text" placeholder="cat photo URL" required>
    <button type="submit">Submit</button>
</form>
```

##### Radio Buttons

```html
<label for="indoor"> 
  <input id="indoor" type="radio" name="indoor-outdoor">Indoor 
</label>

```

##### Checkboxes

```html
<label for="loving">
	<input id="loving" type="checkbox" name="personality">Loving
</label>
```

##### Value Attribute

When a form gets submitted, the data is sent to the server and includes entries for the options selected. Inputs of type radio and checkbox report their values from the value attribute.

```html
<label for="indoor">
    <input id="indoor" value="indoor" type="radio" name="indoor-outdoor">Indoor
</label>
<label for="outdoor">
    <input id="outdoor" value="outdoor" type="radio" name="indoor-outdoor">Outdoor
</label>
```
Here, you have two radio inputs. When the user submits the form with the indoor option selected, the form data will include the line: indoor-outdoor=indoor. This is from the name and value attributes of the "indoor" input.


##### Checked Attribute

You can set a checkbox or radio button to be checked by default using the checked attribute.
```html
<input type="radio" name="test-name" checked>
```

#### division or div

The div element, also known as a division element, is a general purpose container for other elements.

It is useful for placing parts under same class and formatting.

#### Attributes

##### ID

Can be added to any element to provide internal link

# Nuances

## Force Open in new tab with target

```html
<a href="https://freecatphotoapp.com" target="_blank">Jump to Bottom</a>
```