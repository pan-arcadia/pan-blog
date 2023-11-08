# astro content collections

Let's extend our [astro-blog-tutorial](https://github.com/pan-arcadia/astro-blog-tutorial) with **Content Collections**.

Content collections are a way to manage groups of similar content, such a blog posts. Collections help to organize our documents, validate YAML frontmatter, and provide automatic TypeScript type-safety for all of our content.

Here we will:

- Move our directory of blog posts into `src/content`
- Create a schema to define our post frontmatter
- Use `getCollection()` to get blog post content and metadata

By moving our blog posts to the special `src/content` directory, we can use performant APIs to generate our blog post index and display our individual posts.

We will also use a schema to define a common structure for each post that Astro will help us enforce. We use a schema to specify when frontmatter properties are required, and which data type each property must be. 