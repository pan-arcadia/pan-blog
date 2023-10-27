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