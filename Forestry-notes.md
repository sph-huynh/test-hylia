## Forestry Notes Part 1

I'm developing my website with 11ty and Forestry. There are Forestry developer guides for Hugo, Jekyll and Gatsby but not 11ty. So I'll be going through the Hugo guide (as I am already familiar with it) and translating my notes to be used with Forestry.

You can see the [original Forestry guide for Hugo here](https://forestry.io/docs/guides/developing-with-hugo/).

# Developing with 11ty

## Introduction
Eleventy is a simpler static site generator.

[Choose 11ty if you want to](https://www.11ty.dev/docs/)
- incrementally change your website
- want the flexibility of using whatever template suits you

## Getting Started

To get started, I would recommend looking through one of the [starter projects](https://www.11ty.dev/docs/starter/) and exploring the structure before you pick a particular template language. Ofc if you already have something in mind, go for it.

[Hylia](https://github.com/DirtyF/hylia-forestry) is a template that the Forestry team already has a starter project in.

# Project Structure

In 11ty, you have a lot of flexibility around your content structure. 

An examples structure might look like this..

```
.
├── _includes/
├── css/
├── posts/
|   └── 2020/
├── .editorconfig
├── .eleventyignore
├── .gitignore
├── ABOUT.md
├── index.njk
├── package.json
├── package-lock.json
├── README.md
```


I'm going to move all contents into a `site` folder, so mine will look like this.

```
.
├── _11ty/
├── _posts/
|   └── careers/
├── dist/
├── site/
|   └── _data/
|   └── _includes_/
|       └── css/
|       └── layouts/
|           └── example.njk
|       └── partials/
|           └── components/
|           └── global/
|   └── admin/
|       └── config.yml
|       └── index.html
|   └── assets/
|       └── images/
|   └── content/
|       └── pages/
|           └── about.md
|       └── careers/
|       └── index.md
|   └── .eleventy.js
|   └── .eleventyignore
|   └── .gitignore
|   └── README.md
```

If you do change any of the file locations, you need to specify in your `.eleventy.js` file (in the root of your directory) where it should expect what, in which folder.

```
module.exports = function(eleventyConfig) {


// Layout aliases
	eleventyConfig.addLayoutAlias('example', 'layouts/example.njk');

// Tell 11ty to find these assets inside these folders
	eleventyConfig.addPassthroughCopy("site/assets");
	eleventyConfig.addPassthroughCopy('site/admin');
	eleventyConfig.addPassthroughCopy("site/content");

// Tell 11ty where is where
    return {
		pathPrefix: "/",
		dir: {
			includes: "_includes",
			data: "_data",
			input: "site",
			output: "dist"
		},
		passthroughFileCopy: true,
    templateFormats: [ "md", "njk"],
    markdownTemplateEngine: "njk",
    htmlTemplateEngine: "njk"
	};

};
```

Read more about the layout aliases [here](https://www.11ty.dev/docs/layouts/).

Read more about [the moving the asset files (passthrough copy)](https://www.11ty.dev/docs/copy/).

Read more about the `dir: ` part and defining where your output files are [here](https://www.11ty.dev/docs/config/).

## How Forestry Parses 11ty

