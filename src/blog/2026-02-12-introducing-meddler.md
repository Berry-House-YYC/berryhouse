---
layout: layouts/post.njk
title: Introducing Ⓜ️ Meddler
subtitle: A Medium export converter for the IndieWeb
author: Brennan Kenneth Brown
date: 2026-02-12
description: I created a Medium export converter for the IndieWeb that converts your Medium archive into clean Markdown for Jekyll, Hugo, Eleventy, or Astro.js. Available as both a command line tool, and a web interface.
tags: [indieweb, medium, open-source, static-site-generators, web-development]
category: projects
featuredImage: /assets/blog/meddler.jpg
---

Two of the best features of Medium are the fact you can [export your email subscribers list](https://medium.com/dancing-elephants-press/how-to-export-your-e-mail-subscribers-from-medium-f55c9f1ef6ab) and [export your entire account, including your writing](https://help.medium.com/hc/en-us/articles/115004745787-Export-your-account-data). Why are these two of the best features? Because this means that, at anytime, you can take both your work and audience to another platform.

What happens when platforms _don't_ offer this? When Vine shut down in 2017, creators lost years of work overnight. When Yahoo acquired and then killed Geocities, [an estimated 38 million user-built pages vanished](https://computerhistory.org/blog/a-tale-of-deleted-cities/). More recently, platforms like Cohost and Revue closed with limited or no export options. Even Substack's export gives you a basic CSV, which is not a simple plug-and-play for your new blog. Medium, to its credit, lets you take your data with you.

The problem is, though, the export of your work? **For anybody that's used the export feature, they know it has a few issues.** Medium provides a GDPR-compliant data export in the form of a `.zip` archive containing HTML files.

While this preserves content, the format is:

* **Not portable**: files are single-page HTML documents with inline CSS and Medium-specific class names.
* **Noisy**: includes Medium's presentation layer (`graf--`, `section--`, `markup--` CSS classes), making content reuse difficult.
* **Scattered**: metadata like publish date, canonical URL, subtitle, and author are embedded in the HTML footer and header, not structured as data.

And, most importantly for me, the files are not SSG-ready. No YAML, TOML, or JSON front matter, and no clean Markdown body.

At Berry House, we've been advocates of the [IndieWeb](http://indieweb.org/) for quite awhile now. So we decided to use our skills as developers to solve this issue ourselves.

So, we created [**Ⓜ️ Meddler**](https://meddler.fyi/), a command-line tool and website that will take the .ZIP of your export that Medium gives you and turn it into clean, portable Markdown formats for [Jekyll](https://jekyllrb.com/), [Hugo](https://gohugo.io/), [Eleventy](https://11ty.dev/), or [Astro.js](https://astro.build/).

What does this mean? That you can migrate your body of work to your own independent JAMstack blog anytime. You have your blog as a repository on GitHub, [GitLab](https://gitlab.com/), or [CodeBerg](https://codeberg.org/) and host it on a platform like [Netlify](https://www.netlify.com/) or [Vercel](https://vercel.com/) and wire to a domain from [Porkbun](https://porkbun.com/) or other provider. This means you're completely platform-independent. You own and control every aspect of your digital online presence.

Now, this blog post isn't a tutorial for getting your own static-site generator up online. There are plenty of other helpful resources for that. This is about how to use the tool we made to easily migrate and transfer your work from Medium _to_ your new independent blog.

## What is Ⓜ️ Meddler? How does it work?

We decided to create two different converters for this project: a command-line tool for power users, and a simple drag-and-drop website for everyone else.

The site, [https://meddler.fyi](https://meddler.fyi/), runs entirely in the browser. No server, no uploads to third parties, which makes it private and fast. We used our own Medium export (of over 300 stories, ranging from drafts to responses to full articles) to make sure it correctly handled and exported the wide variety of data that Medium gives you.

<img src="/assets/blog/preview-meddler.jpg" alt="Meddler web interface showing the preview of converted Medium posts">

When you successfully upload your export .ZIP, you'll see all the data it contains.

Next, the configuration screen gives granular control over how your export is converted. Here's a breakdown of what each section does:

<img src="/assets/blog/config-meddler.jpg" alt="Meddler configuration screen showing format options and settings">

**Format & Target** lets you choose your static site generator (Hugo, Eleventy, Jekyll, Astro, or Generic) and front matter format (YAML, TOML, or JSON). Selecting a target automatically applies sensible defaults. For example, choosing Hugo switches front matter to TOML and enables shortcodes for embeds. You can also choose output format: Markdown (the default), cleaned HTML, or structured JSON.

**Content Options** controls what gets included. You can toggle draft posts, responses (your short replies written to other people's articles), and whether drafts go into a separate folder. There's also an option to extract the featured image into front matter.

**Image Handling** is one of my favourite features. You can either keep the original Medium CDN URLs (faster, but they may break over time as Medium changes infrastructure) or download all images locally so they're bundled with your export. The web version fetches images directly from Medium's CDN in your browser. You can also organize images per-post into subdirectories like `images/my-post-slug/01.jpeg` instead of having everything messy in a flat folder.

**Embed Handling** determines how YouTube videos, GitHub Gists, Tweets, and other embedded content are converted. "Raw HTML" preserves the original iframes. "SSG shortcodes" auto-detects the embed type and converts them to native shortcodes (e.g., Hugo's {% raw %}`{{</* youtube */>}}`{% endraw %}). "Placeholder links" gives you the most portable option, plain Markdown links.

### Supplementary Data

Medium's export includes far more than just your posts. Meddler can extract and convert all of it:

* **Bookmarks**—your reading list, exported as structured data
* **Claps**—every post you've clapped for, with clap counts
* **Highlights**—quotes you've highlighted on other people's articles
* **Interests**—the tags, topics, publications, and writers you follow
* **Lists**—your curated reading collections
* **Earnings**—Partner Program revenue data per article
* **Social graph**—who you follow (users, publications, topics)
* **Profile**—your display name, bio, avatar URL, connected accounts

**Advanced** options include date format (ISO 8601 or date-only), section break style (horizontal rules, extra spacing, or none), and the ability to add arbitrary custom front matter fields, handy if your blog template expects fields like `layout`, `locale`, or `canonical_url`.

As you change settings, you can click "Show live preview" to see exactly what your converted Markdown will look like, front matter and all, updating in real time.

<img src="/assets/blog/export-meddler.jpg" alt="Meddler export screen showing download progress and conversion log">

You'll get a helpful log explaining what's going on as the converter runs. It shows you each phase: converting posts, downloading images (with a progress bar), processing supplementary data, and finally zipping everything up.

At the end, you get a summary report telling you exactly how many posts were converted, how many drafts and responses were included, how many images were downloaded (and if any failed), and how many supplementary data files were generated.

Once it's done, you download a single `.zip` file containing your entire converted blog, ready to drop into your static site generator's content directory.

## The Command-Line Tool

If you're comfortable with a terminal, the CLI version gives you even more power and reliability. Install it with a single command:

```bash    
npm install -g meddler-cli
```

Then convert your export:

```bash
meddler convert medium-export.zip --preset hugo
```

That's it. One command and your entire Medium archive is converted. But the CLI also supports fine-grained control:

```bash
meddler convert medium-export.zip \
 --target jekyll \
 --front-matter yaml \
 --images download \
 --include-drafts \
 --include-responses
```

You can target any supported SSG (`hugo`, `eleventy`, `jekyll`, `astro`, or `generic`), choose your front matter format, control image downloading, and toggle which content to include. There's also a `--dry-run` flag that shows you what _would_ be converted without writing any files—useful for previewing large exports.

For repeatable workflows, you can create a `.meddlerrc.json` configuration file:

{% raw %}
```json
{
 "frontMatter": "yaml",
 "target": "hugo",
 "includeDrafts": true,
 "imageMode": "download",
 "supplementary": ["profile", "earnings", "bookmarks"],
 "extraFields": {
 "author": "{{author.name}}",
 "canonical_url": "{{url}}"
 }
}
```
{% endraw %}

Notice the template variables, {% raw %}`{{author.name}}`{% endraw %}, {% raw %}`{{url}}`{% endraw %}, {% raw %}`{{date}}`{% endraw %}, etc. These let you inject dynamic metadata into custom front matter fields, which is incredibly useful for themes that expect specific fields.

The CLI also has better image downloading than the web version. Because it runs on your machine with Node.js, it doesn't have the browser's CORS restrictions, so it can reliably fetch every image from Medium's CDN. For large exports with hundreds of images, this makes a real difference.

## What does the output look like?

Here's an example of what a converted post looks like with YAML front matter:

```yaml
---
title: "My Article Title"
subtitle: "A deeper look at the topic"
date: "2023-06-15T14:30:00.000Z"
slug: "my-article-title"
canonical_url: "https://medium.com/@username/my-article-title-abc123"
author: "Your Name"
medium_id: "abc123def456"
draft: false
tags:
 - programming
 - web-development
image: "images/my-article-title/featured.jpeg"
---
## Heading

Your clean Markdown content here, with all of Medium's
presentation cruft stripped away...
```

The metadata that Medium embeds in the HTML such as title, subtitle, publish date, canonical URL, author, and tags all get extracted and structured into proper front matter. The body is clean Markdown with ATX-style headings, fenced code blocks, and proper link formatting.

## Under the Hood

Meddler is a TypeScript monorepo with three packages. The core library (`@berryhouse/core`) handles all the parsing and conversion logic. It uses [cheerio](https://cheerio.js.org/) to parse Medium's HTML and [Turndown](https://github.com/domchristie/turndown) to convert it to Markdown, with custom rules for Medium-specific elements like drop caps, section dividers, mixtape embeds (those linked article cards), and embedded content like YouTube videos and GitHub Gists.

The CLI (`@berryhouse/meddler`) wraps the core library with [Commander.js](https://github.com/tj/commander.js/) for argument parsing, [chalk](https://github.com/chalk/chalk) for coloured terminal output, and [ora](https://github.com/sindresorhus/ora) for progress spinners. The web app is built with React, Vite, and Tailwind CSS, and uses [JSZip](https://stuk.github.io/jszip/) for ZIP file handling, all running entirely client-side.

You can view the NPM package here: [https://www.npmjs.com/package/meddler-cli](https://www.npmjs.com/package/meddler-cli)

## Why I Built This

Over the years, I've accumulated over 300 stories of articles, drafts, and responses on Medium. When I've tried to move my writing to my own blog, I hit the same wall. Medium's export is HTML soup.

When I attempted to convert years ago, I remember having to initialize a WordPress account to use the Medium-to-Wordpress plug-in, followed by a CLI tool that would convert Wordpress posts to Jekyll markdown. The process was clunky and error-prone.

No tools handle the full picture and none of them offered a web interface for people who don't want to touch a terminal.

So I built the tool I wished existed. I tested it against my own massive export, fixed edge cases, and made sure it handled everything from a brand-new account with zero posts to a veteran writer with hundreds of articles and years of bookmarks, claps, and highlights.

## I Still Love Medium!

I've been a writer on Medium for over ten years now, my first article published at the end of 2015, titled ["The Best Time to Start a New Year's Resolution is Right Now"](https://blog.brennanbrown.ca/the-best-time-to-start-a-new-year-s-resolution-is-right-now-ffdd389fbf01).

Since then, we've seen many platforms rise and fall. We've stayed on Medium because we sincerely think it's a wonderful place to write, relative to many others. We earn a living with the Medium partner program. We think Medium is one of the few platforms that has ignored enshittification and promotes thoughtful, longform writing which the web desperately needs. We mentioned many of these points in ["Move to a Better Internet in 2026"](https://blog.brennanbrown.ca/move-to-a-better-internet-in-2026-8ab3d36bae20).

So, please don't get us wrong. We're not making this tool because we want to leave Medium, or we think you ought to leave. Rather, we're making it so you have the ability to have your own your work. [Publish on your own site](https://indieweb.org/POSSE), syndicate elsewhere.

We also now post our articles to our own site, [🔆 Brennan.Day](https://brennan.day/) (with the added benefit of not being paywalled), an independent publication built with [11ty](https://en.wikipedia.org/wiki/Eleventy_(software)), and we really think everyone should have their own website that they make from scratch.

The IndieWeb is becoming more accessible than ever, and gives you freedom and flexibility (and fun!) that no social media platform can. If you miss what the Internet used to be, this is how we reclaim it. The more of us that migrate away from corporate, privacy-hostile platforms and services, the less of a chokehold they'll have on the Internet as a whole. You can read ["The Absolute Beginner's Guide to the IndieWeb for Writers and Non-Coders"](https://blog.brennanbrown.ca/the-absolute-beginners-guide-to-the-indieweb-for-writers-and-non-coders-477ff43b9f3c) to see more about that.

## Try Meddler Out!

If you're thinking about migrating from Medium (or just want a backup of your content in a portable format) give Meddler a try:

* **Web**: [meddler.fyi](https://meddler.fyi/)—drag, drop, download. No installation required.
* **CLI**: `npm install -g meddler-cli` for power users and automation.
* **Source**: [github.com/brennanbrown/meddler](https://github.com/brennanbrown/meddler) The entire project is open source under the AGPL-3.0 license and contributions are welcome!

Your words are yours. They should live wherever you want them to.

_Meddler is not affiliated with Medium. It's an independent, open-source tool built for the IndieWeb community._