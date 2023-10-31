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

## Send our first script to the browser.

We can add client-side JavaScript using `<script>` tags to the *markup* section of the `.astro` file.

`<script>` tags by default are process by Astro.

- Any imports will be bundled, allowing us to import local files or Node modules.
- The processed script will be injected into our page's `<head>` with `type="module"`.
- TypeScript is fully supported.
- If our component is used more than once on a page, the script will be included once.

- Rendering is not blocked. The browser continues to process the rest of the HTML while the module script and its dependencies load.
- The browser waits for HTML to be processed before executing module scripts. 
- `async` and `defer` attributes are not necessary. Module scripts are always deferred.

## Unit 4 Layouts

In this unit we will:

- Create reusable layout components
- Pass content to our layouts with `<slot />`
- Pass data from Markdown frontmatter to our layouts
- Nest multiple layouts

### Build our first layout

- Refactor common layouts into a page layout
- Use an Astro `<slot />` element to place page contents withing a layout
- Pass page-specific as props to its layout

Create an new file at `src/layouts/Baselayout.astro`.

Copy the contents of `index.astro` into `BaseLayout.astro`.

Now we can replace the code in `index.astro` with:

```js
// index.astro
---
import BaseLayout from '../layouts/BaseLayout.astro'
const pageTitle = 'Home Page'
---

<BaseLayout>
    <h2>Blog subtitle text.</h2>
</BaseLayout>

```

Now we add a `<slot>` element to `BaseLayout.astro`:

```js
// BaseLayout.astro
---
import Header from '../components/Header.astro';
import Footer from '../components/Footer.astro';
import '../styles/global.css';
const pageTitle = "Home Page";
---
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <meta name="viewport" content="width=device-width" />
    <meta name="generator" content={Astro.generator} />
    <title>{pageTitle}</title>
  </head>
  <body>
    <Header />
    <h1>{pageTitle}</h1>

    <slot />

    <Footer />
    <script>
      import "../scripts/menu.js";
    </script>
  </body>
</html>
```

### Pass page-specific values as props

Pass the page title to our layout component from `index.astro` using a component attribute:

```js
---
import BaseLayout from '../layouts/BaseLayout.astro';
const pageTitle = "Home Page";
---
<BaseLayout pageTitle={pageTitle}>
  <h2>My awesome blog subtitle</h2>
</BaseLayout>
```

Change the script of our `BaseLayout` component to receive a page title via `Astro.props` instead of defining a constant.

```js
// BaseLayout.astro
---
import Header from '../components/Header.astro';
import Footer from '../components/Footer.astro';
import '../styles/global.css';
// const pageTitle = "Home Page";
const { pageTitle } = Astro.props;
---
```

## Create and pass data to a custom blog layout

Let's add a layout for our blog posts!

When we inclue the `layout` frontmatter property in an `.md` file, all of our frontmatter YAML values are available to the layout file.

1. Create a new file at `src/layouts/MarkdownPostLayout.astro`
2. Add some code to our new layout file:
  ```js
---
const { frontmatter } = Astro.props;
---
<h1>{frontmatter.title}</h1>
<p style="color:red">Written by {frontmatter.author}</p>
<p>Published on: {frontmatter.pubDate.slice(0, 10)}</p>
<slot />
```
3. Include the new layout in our `.md` file:
```js
---
layout: ../../layouts/MarkdownPostLayout.astro

---
```