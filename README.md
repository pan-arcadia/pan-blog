# astro-blog tutorial notes

## Node.js

We'll need Node.js version `v18.14.1` or later.

## Launch Astro setup wizard

```shell
npm create astro@latest
```

Once the setup is running:

- Choose a project name.
- Choose "empty" template.
- Install dependencies.
- No TypeScript.
- Create repository.

## Create astro pages

Create an `about.astro` and `blog.astro` page in the `pages` directory. Copy the contents of `index.astro` to these pages.

## Add navigation links

Add navigation links to all three pages:

```html
<a href="/">Home</a>
<a href="/about/">About</a>
<a href="/blog/">Blog</a>
```

## Create posts

In `/pages/posts/`, create three files: `post-1.md`, `post-2.md`, and `post-3.md`.

In the `/pages/blog.asto`, create some links to these posts:

```html
<ul>
    <li>
        <a href="/posts/post-1">Post 1</a>
        <a href="/posts/post-2">Post 2</a>
        <a href="/posts/post-3">Post 3</a>
    </li>
</ul>
```

## Add dynamic content

### Define and use a variable.

We can add JavaScript to our Frontmatter section of the page and then refer to variables using curly braces `{}` in our code.

```js
// Frontmatter section of our Astro page.
---
const pageTitle = 'Our page'
---
```

```html
<!-- html section of our astro page. -->
<h1>{pageTitle}</h1>
```

### Write JavaScript expressions in Astro

```js
// Frontmatter section of our Astro page.
---
const identity = {
	firstname: 'Adam',
	lastname: 'Stone',
	country: 'Germany',
	hobbies: ['sleeping', 'sitting', 'drinking']
}
---
```

```html
<!-- html section of our astro page. -->
<p>My name is {identity.firstname}</p>
<ul>
    {identity.hobbies.map((hobby) => <li>{hobby}</li>)}
</ul>
```

## Styling

Using Astro's own `<style>` tags, we can style items on our page. Adding **attributes** and **directives** to these tags gives us more ways to style.

We can add styles to the head of our documents.

```html
<head>
    <meta charset="utf-8" />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <meta name="viewport" content="width=device-width" />
    <meta name="generator" content={Astro.generator} />
    <title>{pageTitle}</title>
    <style>
        h1 {
            color: purple;
            font-size: 4rem;
        }

        .hobbies {
            color: green;
            font-weight: bold;
        }
    </style>
</head>
```

### Using CSS variables

Our `<style>` tag can also reference variables in our frontmatter script using the `define:vars={ {...} }` directive.

We can define variables inside our code fence, then use them as CSS variables in our style tag.

```js
// Frontmatter section of our Astro page.
---
const hobbyColor = 'blue'
---
```

```html
<!-- html section of our astro page. -->
<head>
    ...
    <title>{pageTitle}</title>
    <style define:vars={{hobbyColor}}>
        h1 {
            color: purple;
            font-size: 4rem;
        }

        .hobbies {
            color: var(--hobbyColor);
            font-weight: bold;
        }
    </style>
</head>
```

## Add site-wide styling

We can also add global styling to our site.

### Add a global stylesheet

There are a few ways to define styles **globally** in Astro. Here we will create and import a `global.css` file into each of our pages. This way we can control some styles site-wide and also apply some specific styles where we need them.

Create a new folder: `/src/styles/global.css`

Here's some code to drop in there:

```css
html {
  background-color: #f1f5f9;
  font-family: sans-serif;
}

body {
  margin: 0 auto;
  width: 100%;
  max-width: 80ch;
  padding: 1rem;
  line-height: 1.5;
}

* {
  box-sizing: border-box;
}

h1 {
  margin: 1rem 0;
  font-size: 2.5rem;
}
```

Now we can import `global.css` in the frontmatter script our page:

```js
import '../styles/global.css'
```

## Unit 3 Components

Let's make some components.

Create a `src/components/` directory.

Create a `src/components/Navigation.astro` file.

Populate our component with the code we want.

Now we can import our component into the frontmatter script on a page:

```js
import Navigation from '../components/Navigation.astro'
```

And insert our component as a tag in our markup:

```html
<Navigation />
```

The component renders the code in the file.