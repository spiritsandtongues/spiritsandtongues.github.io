# Spirits and Tongues Website

## Development

### Tech stack

This project is built with the following technologies:

- **[Jekyll](https://jekyllrb.com/)**, for generating static site content from HTML templates and Markdown files.
- **[AmplitudeJS](https://github.com/serversideup/amplitudejs)**, for implementing audio player controls.
- **[OCI Containers](https://opencontainers.org/)**, for running the project locally.
- **[EditorConfig](https://editorconfig.org/)**, for maintaining consistent code formatting between different editors.
- **[GitHub Pages](https://pages.github.com/)**, for free website hosting.
- **[CloudFlare](https://www.cloudflare.com/)**, for free CDN service and enabling HTTPS.

### Prerequisites

In order to run the project on your local machine, you'll need the following:

- **[Docker Desktop](https://www.docker.com/products/docker-desktop), or an equivalent tool that supports the Docker CLI:** This project is set up to run in development mode inside a container, to avoid having to manually install Ruby and Jekyll.
- **[EditorConfig](https://editorconfig.org/):** This is a tool for helping maintain consistent code formatting between different editors. Some editors/IDEs come with it preinstalled, but for others, you'll need to download it as an extension. When it's installed, it will automatically read the project's `.editorconfig` file and use the settings it specifies.

### Running locally

To run the project locally, open a command prompt to the project root and run `docker compose up`. Once this is running, you'll be able to view the website at [http://localhost:4000](http://localhost:4000). The website will also auto-reload as you edit the code.

### Updating dependencies

In order to update the Ruby dependencies to their latest versions, open a command prompt to the project root and run `docker compose -f docker-compose-update.yml up`. This will update the versions in the `Gemfile.lock` file.

### Deploying the website

Each time a new commit is pushed to the `master` branch, it will trigger the website to be built by Jekyll and then deployed to [https://spiritsandtongues.com/](https://spiritsandtongues.com/). To prevent changes from prematurely going live, all work should be done on the `develop` branch. Once it is ready to go live, it can then be merged into the `master` branch.

## Content

### Podcast episodes

New podcast episodes are automatically pulled in to the website. After the page loads, JavaScript retrieves the RSS feed from [Libsyn](https://libsyn.com/), parses it, and then displays each episode on the page.

### Blog posts

To create a new blog post, create a file in the `_posts` directory, following the guidelines below. It will automatically show up in the list of posts, ordered according to the date in its metadata.

#### Filename

A blog post's filename should follow the pattern `<year>-<month>-<day>-<resourceName>.md`.

`<year>` should be a four-digit number representing the year the post was published, `<month>` should be a two-digit number representing the month the post was published, and `<day>` should be a two-digit number representing the day of the month the post was published. The date that consists of these three elements does the following:

- It determines the date that shows up underneath the blog post's title on the website.
- It determines how the blog post is sorted in relation to other posts on the website.
- The date's year determines the year that shows up in the URL of the blog post.
- If the date is in the future, then the blog post doesn't show up on the website until the next time the site is deployed on or after that date.
- If a file is created in the `_posts` directory without a date (in the format `<resourceName>.md`), it will be a draft post, which doesn't show up on the website.

`<resourceName>` should be a string in kebab case that is similar to the name of the blog post. This controls the last section of the URL for the post. For example if `<resourceName>` is set to "example-blog-post", then its URL will be `https://spiritsandtongues.com/blog/<year>/example-blog-post`.

#### Metadata

Each file in the `_posts` directory needs to have a metadata section at the top, in this format:

```
---
layout: post
title: "<title>"
---
```

The `layout: post` line tells Jekyll it should render the blog post by inserting its content into `_layouts/post.html`.

The `title: "<title>"` line determines the blog post's title that will show up on the website, where `<title>` is the title. Note that the parentheses are required. If the blog post's title also contains parentheses, they need to be escaped. For example, if the title is 'A "New" Blog Post', then this metadata line should be written as `title: "A \"New\" Blog Post"`.

#### Preview

On the website's list of blog posts, a short preview of each post is shown underneath its title. This is controlled by the `<!--preview-cutoff-->` tag. All content above this tag (excluding the metadata) is included in the post's preview. Even if this content consists of multiple paragraphs, it will show up as a single paragraph in the preview.

#### Content

The content of each blog post should be written in [GitHub Flavored Markdown](https://github.github.com/gfm/). When building the website, Jekyll renders this as HTML and places it inside the specified layout HTML file.

Since a blog post's title comes from the metadata and is displayed on the website using an `<h1>` heading, any headings in the blog post content should start with `<h2>` (`##` in Markdown).

If a blog post contains any images, they can be placed in the `images` directory and then inserted into the post using Markdown. For instance, and image located at `images/example-blog-post/example-image.png` can be included using the Markdown `![<altText>](/images/example-blog-post/example-image.png)`, where `<altText>` is the alt text to use for the image.

Markdown can contain inline HTML, so if a blog post needs any special formatting that can't be done with Markdown's features, HTML can be used instead.
