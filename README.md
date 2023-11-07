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

Create a new file at `src/layouts/MarkdownPostLayout.astro`
Add some code to our new layout file:

```js
---
const { frontmatter } = Astro.props;
---
<h1>{frontmatter.title}</h1>
<p style="color:red">Written by {frontmatter.author}</p>
<p>Published on: {frontmatter.pubDate.slice(0, 10)}</p>
<slot />
```

Include the new layout in our `.md` file:
```js
---
layout: ../../layouts/MarkdownPostLayout.astro

---
```

## Combine layouts to get the best of both worlds

We've added a layout for our blog posts. Now we can make our posts look like the rest of our site.

### Nest our two layouts

Our `Baselayout.astro` layout defines the overall layout of our pages.

We can match the look or our blog posts to the rest of our site by **nesting layouts**.

In our `MarkdownPost.astro` file, import `BaseLayout.astro` and use it to wrap the entire template content:

```js
---
// MarkdownPost.asto

import BaseLayout from './BaseLayout.astro';
const { frontmatter } = Astro.props;
---
<BaseLayout pageTitle={frontmatter.title}>
  <!-- <h1>{frontmatter.title}</h1> -->
  <p>{frontmatter.pubDate.slice(0,10)}</p>
  <p><em>{frontmatter.description}</em></p>
  <p>Written by: {frontmatter.author}</p>
  <img src={frontmatter.image.url} width="300" alt={frontmatter.image.alt} />
  <slot />
</BaseLayout>
```

## Unit 5 Astro API

With Astro API's we can add to our blog:

- index page
- tag pages
- RSS feed

And we will learn how to use:

- `Astro.glob()` to access data from files in our project
- `getStaticPaths()` to create multiple pages (routes) at once
- The Astro RSS package to create an RSS feed

### Create a blog post archive

Here we can configure the Blog page to create a list of links to our posts automatically.

We will:

- Access data from all our posts at once using `Astro.glob()`
- Display a dynamically generated list of posts on our Blog page
- Refactor to use a `<BlogPost />` component for each list item

#### Dynamically display a list of posts

In our `blog.asto` file, we can use `Astro.glob()` to return an array of objects, one for each blog post in `/src/pages/posts`:

```js
---
import "../styles/global.css";
import BaseLayout from "../layouts/BaseLayout.astro";

// Get an array of data providing information on each of our markdown files.
const allPosts = await Astro.glob('../pages/posts/*.md')

const pageTitle = "Blog Page";
---

<BaseLayout pageTitle={pageTitle}>
	<style>

	</style>
	<!-- <ul>
		<li><a href="/posts/post-1">Post 1</a></li>
		<li><a href="/posts/post-2">Post 2</a></li>
		<li><a href="/posts/post-3">Post 3</a></li>
	</ul> -->

  <!-- Render the links to our markdown files. -->
	<ul>
		{
			allPosts.map((post) => <li><a href={post.url}>{post.frontmatter.title}</a></li>)
		}
	</ul>

</BaseLayout>
```

### Generate tag pages

Here we will:

- Create a page to generate multiple pages
- Specify which page routes to build, and pass each page its own props

#### Dynamic page routing

We can create entire sets of pages dynamically using `.astro` files that export a `getStaticPaths()` function.

#### Create pages dynamically

Create a new file at `src/pages/tags/[tag].astro`:

```js
---
import BaseLayout from "../../layouts/BaseLayout.astro";
import BlogPost from "../../components/BlogPost.astro";

export async function getStaticPaths() {
    const allPosts = await Astro.glob("../posts/*.md");
    return [
        { params: { tag: "astro" }, props: { posts: allPosts } },
        { params: { tag: "successes" }, props: { posts: allPosts } },
        { params: { tag: "community" }, props: { posts: allPosts } },
        { params: { tag: "blogging" }, props: { posts: allPosts } },
        { params: { tag: "setbacks" }, props: { posts: allPosts } },
        { params: { tag: "learning in public" }, props: { posts: allPosts } },
    ];
}

const { tag } = Astro.params;
const { posts } = Astro.props;
const filteredPosts = posts.filter((post) =>
    post.frontmatter.tags?.includes(tag),
);
---

<BaseLayout pageTitle={tag}>
    <style>
        span {
            font-style: italic;
        }
    </style>
    <p>Posts tagged with <span>{tag}</span></p>

    <ul>
        {
            filteredPosts.map(
                // (post) => <li><a href={post.url}>{post.frontmatter.title}</a></li>
                (post) => <BlogPost url={post.url} title={post.frontmatter.title} />

            )
        }
    </ul>
</BaseLayout>
```

The `getStaticPaths()` function returns an array of page routes, and all of the pages at those routes will use the same template defined in the file.

*Make sure that every blog post contains at least on tag.*

We make our `props` and `tags` available outside our `getStaticPaths()` function like this:

```js
const { tag } = Astro.params;
const { posts } = Astro.props;
```

We filter our list of posts to only include posts that contain the page's own tag:

```js
const filteredPosts = posts.filter((post) =>
    post.frontmatter.tags?.includes(tag),
);
```

If we need to construct the page routes, we write it **inside** `getStaticPaths()`.

To receive information in the HTML template of a page route, we write it **outside** `getStaticPaths()`.

#### Generate pages from existing tags

Here we are going to replace the above code with code that will automatically look for, and generate pages for, each tag used on our blog pages.

All of our blog posts should contain at least one tag: `tags: ['blogging']`

Now we can create an array of all of our existing tags:

```js
// src/pages/tags/[tag].astro
---
import BaseLayout from '../../layouts/BaseLayout.astro';

export async function getStaticPaths() {
  const allPosts = await Astro.glob('../posts/*.md');

  const uniqueTags = [...new Set(allPosts.map((post) => post.frontmatter.tags).flat())];
```

Replace the `return` value of the `getStaticPaths()` function:

```js
// src/pages/tags/[tag].astro

// return [
//     { params: { tag: "astro" }, props: { posts: allPosts } },
//     { params: { tag: "successes" }, props: { posts: allPosts } },
//     { params: { tag: "community" }, props: { posts: allPosts } },
//     { params: { tag: "blogging" }, props: { posts: allPosts } },
//     { params: { tag: "setbacks" }, props: { posts: allPosts } },
//     { params: { tag: "learning in public" }, props: { posts: allPosts } },
// ];

return uniqueTags.map((tag) => {
    const filteredPosts = allPosts.filter((post) =>
        post.frontmatter.tags.includes(tag),
    );
    return {
        params: { tag },
        props: { posts: filteredPosts },
    };
});
```

The `getStaticPaths()` function should always return a list of objects containing `params` (what to call each page route) and optionally any `props` (data that we want to pass to those pages). 

Now, we generate our list of objects automatically using our `uniqueTags` array to define each parameter.

Now our list of all blog posts is filtered **before** it is sent to each page as props. 

Here is the final code sample:

```js
---
import BaseLayout from '../../layouts/BaseLayout.astro';
import BlogPost from '../../components/BlogPost.astro';

export async function getStaticPaths() {
  const allPosts = await Astro.glob('../posts/*.md');

  const uniqueTags = [...new Set(allPosts.map((post) => post.frontmatter.tags).flat())];

  return uniqueTags.map((tag) => {
    const filteredPosts = allPosts.filter((post) => post.frontmatter.tags.includes(tag));
    return {
      params: { tag },
      props: { posts: filteredPosts },
    };
  });
}

const { tag } = Astro.params;
const { posts } = Astro.props;
---
<BaseLayout pageTitle={tag}>
  <p>Posts tagged with {tag}</p>
  <ul>
    {posts.map((post) => <BlogPost url={post.url} title={post.frontmatter.title}/>)}
  </ul>
</BaseLayout>
```

## Build a tag index page

Here we are going to:

- Add a new page using the `/pages/folder/index.astro` routing pattern
- Display a list of all our unique tags, linking to each tag page
- Update our site with navigation links to this new Tags page


### Use the `/pages/folder/index.astro` routing pattern

We are going to use our `/tags/` directory to store our `index.astro` file. This way we keep all our files relating to tags in the same directory.

### Make a Tag Index page

Create a new file at `src/pages/tags/index.astro`.

Import our `<BaseLayout>` layout.

Import a page title, and pass it to our layout as a component attribute.

Here's the code:

```js
---
import BaseLayout from '../../layouts/BaseLayout.astro';
const pageTitle = "Tag Index";
---
<BaseLayout pageTitle={pageTitle}></BaseLayout>
```

### Create an array of tags

Gather all the frontmatter data from each blog post in our `.md` files. We store them in `allPosts`.

Next we can store an array of unique tag names in `tags`.

```js
// src/pages/tags/index.astro
---
import BaseLayout from '../../layouts/BaseLayout.astro';
const allPosts = await Astro.glob('../posts/*.md');
const tags = [...new Set(allPosts.map((post) => post.frontmatter.tags).flat())];
const pageTitle = "Tag Index";
---
```

Now we can update our template in `index.astro`.

```js
<BaseLayout pageTitle={pageTitle}>
  <div>{tags.map((tag) => <p>{tag}</p>)}</div>
</BaseLayout>
```

Now we can turn these tags into links:

```js
<BaseLayout pageTitle={pageTitle}>
  <div>
    {tags.map((tag) => (
      <p><a href={`/tags/${tag}`}>{tag}</a></p>
    ))}
  </div>
</BaseLayout>
```

Here is the final code for `src/pages/tags/index.astro` with some styling:

```js
---
import BaseLayout from '../../layouts/BaseLayout.astro';
const allPosts = await Astro.glob('../posts/*.md');
const tags = [...new Set(allPosts.map((post) => post.frontmatter.tags).flat())];
const pageTitle = "Tag Index";
---
<BaseLayout pageTitle={pageTitle}>
  <div class="tags">
    {tags.map((tag) => (
      <p class="tag"><a href={`/tags/${tag}`}>{tag}</a></p>
    ))}
  </div>
</BaseLayout>
<style>
  a {
    color: #00539F;
  }

  .tags {
    display: flex;
    flex-wrap: wrap;
  }

  .tag {
    margin: 0.25em;
    border: dotted 1px #a1a1a1;
    border-radius: .5em;
    padding: .5em 1em;
    font-size: 1.15em;
    background-color: #F8FCFD;
  }
</style>
```

## RSS feed

I skipped this section. Don't want to do this right now.


## Astro Islands

I skipped over the `Preact` part of the tutorial, but I did add the light/dark mode part.

### Add and style a theme toggle icon

Create a new file `src/components/ThemeIcon.astro` and add the following code:

```js
---
---
<button id="themeToggle">
  <svg width="30px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
    <path class="sun" fill-rule="evenodd" d="M12 17.5a5.5 5.5 0 1 0 0-11 5.5 5.5 0 0 0 0 11zm0 1.5a7 7 0 1 0 0-14 7 7 0 0 0 0 14zm12-7a.8.8 0 0 1-.8.8h-2.4a.8.8 0 0 1 0-1.6h2.4a.8.8 0 0 1 .8.8zM4 12a.8.8 0 0 1-.8.8H.8a.8.8 0 0 1 0-1.6h2.5a.8.8 0 0 1 .8.8zm16.5-8.5a.8.8 0 0 1 0 1l-1.8 1.8a.8.8 0 0 1-1-1l1.7-1.8a.8.8 0 0 1 1 0zM6.3 17.7a.8.8 0 0 1 0 1l-1.7 1.8a.8.8 0 1 1-1-1l1.7-1.8a.8.8 0 0 1 1 0zM12 0a.8.8 0 0 1 .8.8v2.5a.8.8 0 0 1-1.6 0V.8A.8.8 0 0 1 12 0zm0 20a.8.8 0 0 1 .8.8v2.4a.8.8 0 0 1-1.6 0v-2.4a.8.8 0 0 1 .8-.8zM3.5 3.5a.8.8 0 0 1 1 0l1.8 1.8a.8.8 0 1 1-1 1L3.5 4.6a.8.8 0 0 1 0-1zm14.2 14.2a.8.8 0 0 1 1 0l1.8 1.7a.8.8 0 0 1-1 1l-1.8-1.7a.8.8 0 0 1 0-1z"/>
    <path class="moon" fill-rule="evenodd" d="M16.5 6A10.5 10.5 0 0 1 4.7 16.4 8.5 8.5 0 1 0 16.4 4.7l.1 1.3zm-1.7-2a9 9 0 0 1 .2 2 9 9 0 0 1-11 8.8 9.4 9.4 0 0 1-.8-.3c-.4 0-.8.3-.7.7a10 10 0 0 0 .3.8 10 10 0 0 0 9.2 6 10 10 0 0 0 4-19.2 9.7 9.7 0 0 0-.9-.3c-.3-.1-.7.3-.6.7a9 9 0 0 1 .3.8z"/>
  </svg>
</button>

<style>
  #themeToggle {
    border: 0;
    background: none;
  }
  .sun { fill: black; }
  .moon { fill: transparent; }


  :global(.dark) .sun { fill: transparent; }
  :global(.dark) .moon { fill: white; }
</style>
```

Now we can add the icon to `Header.astro`:

```js
---
import Navigation from './Navigation.astro';
import ThemeIcon from './ThemeIcon.astro';
---
<header>
  <nav>
    <ThemeIcon />
    <Navigation />
  </nav>
</header>
```

Now let's add some styling to our `global.css`:

```css
html.dark {
  background-color: #0d0950;
  color: #fff;
}

.dark .nav-links a {
  color: #fff;
}
```

And finally we can add some client-side interactivity.

Add the following `<script>` tag in `src/components/ThemeIcon.astro` after our `<style>` tag:

```js
<script is:inline>
  const theme = (() => {
    if (typeof localStorage !== 'undefined' && localStorage.getItem('theme')) {
      return localStorage.getItem('theme');
    }
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      return 'dark';
    }
      return 'light';
  })();

  if (theme === 'light') {
    document.documentElement.classList.remove('dark');
  } else {
    document.documentElement.classList.add('dark');
  }

  window.localStorage.setItem('theme', theme);

  const handleToggleClick = () => {
    const element = document.documentElement;
    element.classList.toggle("dark");

    const isDark = element.classList.contains("dark");
    localStorage.setItem("theme", isDark ? "dark" : "light");
  }

  document.getElementById("themeToggle").addEventListener("click", handleToggleClick);
</script>
```
