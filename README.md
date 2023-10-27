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