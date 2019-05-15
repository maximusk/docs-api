---
title: "Structure"
date: "2018-10-01"
meta_title: "Ghost Handlebars Theme Structure - Documenation"
meta_description: "Discover the building blocks of a Handlebars theme in Ghost and start building a custom publication of your own! 👻"
next: 
  url: "/api/handlebars-themes/packagejson/"
  title: "Package.json"
sidebar: "handlebars"
keywords:
    - structure
    - handlebars
    - themes
    - templates
---
A Ghost theme contains static HTML templates that make use of helpers to output data from your site, and custom CSS for styling. 

## Structure

The recommended file structure for a Ghost theme is:

```bash:title=File structure
.
├── /assets
|   └── /css
|       ├── screen.css
|   ├── /fonts
|   ├── /images
|   ├── /js
├── default.hbs
├── index.hbs [required]
└── post.hbs [required]
└── package.json [required]
```

An optional `/partials` directory allows you to use partial templates across your site. This allows you to share blocks of HTML between multiple templates and reduce code duplication. 

```bash:title=File structure
.
├── /assets
    ├── /css
        ├── screen.css
    ├── /fonts
    ├── /images
    ├── /js
├── /partials
    ├── list-post.hbs
├── default.hbs
├── index.hbs [required]
└── post.hbs [required]
└── package.json [required]
```

### Templates

Two template files are required: `index.hbs` and `post.hbs`. All other templates are optional. We **highly** recommended using  a `default.hbs` file as a base layout for your theme. If you have significantly different layouts for different pages or content types, you can use the [dynamic routing](/concepts/routing/) configuration layer, or use partials to encapsulate common parts of your theme. 

Theme templates are hierarchical, so one template can extend another template. This prevents base HTML from being repeated. Here are some commonly used theme templates and their uses:

#### default.hbs
`default.hbs` is a base template that contains the boring bits of HTML that exist on every page such as `<html>`, `<head>` or `<body>` as well as the required `{{ghost_head}}` and `{{ghost_foot}}` and any HTML for the header and footer.

#### index.hbs
This is the standard required template for a list of posts. It is also used if your theme does not have a `tag.hbs`, `author.hbs` or `home.hbs` template. The `index.hbs` template usually extends `default.hbs` and is passed a list of posts using the `{{#foreach}}` helper.

#### home.hbs
An optional template to provide special content for the home page. This template will only be used to render `/`.

#### post.hbs
The required template for a single post which extends `default.hbs` and uses the `{{#post}}` helper to output the post details. Custom templates for individual posts can be created using `post-:slug.hbs`.

#### page.hbs
An optional template for static pages. If this is not specified then `post.hbs` will be used. Custom templates for individual pages can be created using `page-:slug.hbs`.

#### custom-{{template-name}}.hbs
An optional custom templates that can be selected in the admin interface on a per-post basis. They can be used for both posts and pages.

#### tag.hbs
An optional template for tag archive pages. If not specifed the `index.hbs` template is used. Custom templates for individual tags can be created using `tag-:slug`.

#### author.hbs
An optional template for author archive pages. If not specified the `index.hbs` template is used. Custom templates for individual authors can be created using `author{{slug}}`.

#### private.hbs
An optional template for the password form page on password protected publications.

#### error.hbs
An optional theme template for any 404 or 500 errors. If one is not specified Ghost will use the default.

#### amp.hbs
An optional theme template for  AMP ([Accelerated Mobile Pages](https://www.ampproject.org/docs/get_started/about-amp.html)). If your theme doesn't provide an `amp.hbs` file, Ghost will use its default.

#### robots.txt
Themes can include a robots.txt which overrides the default robots.txt provided by Ghost.

The development version of the default theme [Casper](https://github.com/TryGhost/Casper) can be used to explore how Ghost themes work, or you can customise Casper and make it your own!

### Helpers

Ghost templates are constructed from HTML and handlebars helpers. There are a few requirements:

In order for a Ghost theme to work, you must make use of the required helpers: `{{asset}}`, `{{body_class}}`, `{{post_class}}`, `{{ghost_head}}`, `{{ghost_foot}}`.

See the [full list of helpers](/api/handlebars-themes/helpers/)  for more detailed information about specific Handlebars helpers.

### Contexts

Each page in a Ghost theme belongs to a [context](/api/handlebars-themes/context/) which is determined by the URL. The context will decide what template will be used, what data is available and what is output by the `{{body_class}}` helper. 

### Styling

When building themes it is important to consider the scope of classes and IDs to avoid clashes between your main styling and your post styling. IDs are automatically generated for headings and used inside a post, so it's best practice to scope things to a particular part of the page. For example: #themename-my-id is preferrable to #my-id.

### Development mode
It is recommended to use a local install to build a custom theme using development mode – review the [local install guide](/install/local/) to get started with your own local install for development.

In production mode, template files are loaded and cached by the server. For any changes in a `hbs` file to be reflected, use the `ghost restart` command.

Ghost will automatically check for fatal errors when you upload your theme into Ghost admin. For a full validation report during development, use the [GScan tool](https://gscan.ghost.org/).


## Summary

You now have a solid understanding of how a Ghost theme is structured and an overview of some of the most common templates. Before diving into the specifics of contexts, helpers and additional features, the next step is to get an overview of the `package.json` file.
