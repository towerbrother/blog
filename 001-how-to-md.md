# Quick and dirty intro to Markdown

A (definitely) non-comprehensive guide to Markdown that will get you off the couch and catapult you in a new dimension of possibilities... well at least at your keyboard to write the book you always wanted to write or start the University thesis you should have started months ago.

## TL;DR

Markdown is a _lightweight markup language used to add formatting elements to plaintext text documents_. It's free, portable, easy to learn and 100% future proof. Jump to the [Cheatsheet](#cheatsheet) below to get started.

## What is Markdown?

Markdown is a _lightweight markup language used to add formatting elements to plaintext text documents_. It is widely used in web development world for content creation, in fact it is also known as a _Text-to-HTML conversion tool_.

It differs from word processor and rich-text editors (i.e. Microsoft Word) as no shortcut and built-in tools are available. In addition, the formatting is not immediately visibile (unless you preview your markdown-formatted text - VS Code shortcut **Ctrl+Shift+V** or if you use online services like [Dillinger](https://dillinger.io/)).

Text formatting like headers, bolds, italics, bullet-points, tables, code blocks etc. are applied using simple characters. Sorry... no fancy buttons available here - only you, your brain and your keyboard. No distractions!

Markdown syntax nonetheless is designed to be readable and unobtrusive on its own and, after a while, can be easily read and understood even without being rendered.

## Why Markdown?

You may ask yourself then... why in the world should I give up my fancy tool and use such a weird-looking alternative? It may seem like giving up a penthouse suite at the Ritz for a furnished studio Airbnb with only a sofabed and an electric cooker... let me list a couple of possible reasons and then we will jump right into it.

- **it's free** - don't we all like free lunches!?

- **it's easy to learn** - really! a bit of practice and a comprehensive cheatsheet for brain-fart-moments.

- **it's portable** - markdown-formatted text can be opened using (basically) any application... try open a Microsoft Word document with another application... good luck mate!

- **it's platform independent** - any application on any device with any operating system.

- **it's forever** - even in the event your preferred markdown app cease to exist, you will always be able to maintain your content with another app.

## Let's get into it... enough chit-chatting

How to start then... I personally use Visual Studio Code as my one-stop-shop for programming and content creation, but really, for markdown, there are many more options. Below a bunch of options for you, in no particular order. I am not affiliate with any of those... I don't care witch one you end up using.

- download a software that supports markdown:
  - [Visual Studio Code](https://code.visualstudio.com/)
  - [Ghost Writer](https://wereturtle.github.io/ghostwriter/)
  - and many other fancy tools for a fee

- use an in-browser web application:
  - [Dillinger](https://dillinger.io/)
  - [Stack Edit](https://www.markdownguide.org/tools/stackedit/)

## Cheatsheet

### Emphasis

<pre>
*Emphasize* _emphasize_
**Strong** __Strong__
</pre>

This is an example of *emphasis* and of **boldness**.

### Inline Links

<pre>
A [link](http://example.com).
</pre>

A [link](http://example.com/).

### Referenced Links

<pre>
Some text with [a link][1] and
[another link][2].

[1]: http://example.com/
[2]: http://example.org/
</pre>

Some text with [a link][1] and
[another link][2].

[1]: http://example.com/
[2]: http://example.org/

### Bullet points

<pre>
* Item
or
- Item
</pre>

- Item

- Item

### Numbered Lists

<pre>
1\. Item
2\. Item
</pre>

1. Item
2. Item

### Mixed Lists

<pre>
1\. Item
2\. Item
   - Mixed
   - Mixed  
3\. Item
</pre>

1. Item
2. Item
    - Mixed
    - Mixed
3. Item

### Blockquotes

<pre>
> Quoted text.
>
> > Quoted quote.
> - Quoted
> - List
</pre>

> Quoted text.
>
> > Quoted quote.

> - Quoted
> - List

### Pre-formatting

<pre>
  Begin each line with
  two spaces or more to
  make text look
  e x a c t l y
  like  you  type i
  t.</pre>

### Code

<pre>
`This is code`
</pre>

`This is code`

### Code block

<pre>
~~~~
{
  "firstName": "Bruce",
  "lastName": "Wayne",
  "job": "Batman"
}
~~~~

or this way

```
.blue {
  color: blue;
}
```
</pre>

~~~~
{
  "firstName": "Bruce",
  "lastName": "Wayne",
  "job": "Batman"
}
~~~~

```
.blue {
  color: blue;
}
```

### Code block - specify language

<pre>
~~~~JSON
{
  "firstName": "Bruce",
  "lastName": "Wayne",
  "job": "Batman"
}
~~~~

or this way

```css
.blue {
  color: blue;
}
```
</pre>

~~~~JSON
{
  "firstName": "Bruce",
  "lastName": "Wayne",
  "job": "Batman"
}
~~~~

```css
.blue {
  color: blue;
}
```

### Headers

<pre>
# Header 1

## Header 2

### Header 3

#### Header 4

##### Header 5

###### Header 6
</pre>

# Header 1

## Header 2

### Header 3

#### Header 4

##### Header 5

###### Header 6

### Tables

<pre>
| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |
</pre>

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

You can format text in tables but you can’t use headings, blockquotes, lists, horizontal rules, images, or most HTML tags.

### Tables alignment

<pre>
| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |
</pre>

| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |

## Additional resources you can check

<https://code.visualstudio.com/docs/languages/markdown>

<https://www.markdownguide.org/getting-started/>
