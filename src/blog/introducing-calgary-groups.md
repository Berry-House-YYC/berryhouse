---
layout: layouts/post.njk
title: Introducing CalgaryGroups.ca
subtitle: A searchable directory of grassroots organizations in Calgary
author: Brennan Kenneth Brown
date: 2025-12-26
description: How do you find your people, and your community within your local city? Calgary Groups is a searchable directory of grassroots organizations in Calgary.
tags: [projects, directory, grassroots, Calgary]
category: projects
featuredImage: https://raw.githubusercontent.com/Berry-House-YYC/calgarygroups/refs/heads/main/src/assets/screenshot.png
---

I've lived in Calgary nearly my entire life. For twenty years I’ve personally been trying to figure out where I belong in this city. And I mean that literally. What groups exist and who’s organizing around the things I care about? 

The ideal would be to be able to easily find places and groups where I could volunteer, learn, protest, create, or really just sit in a room of people who get it. You know?

Anytime I *was* lucky enough to find something, like a book club or community garden, it felt as though I stumbled onto something secret. Menionted in passing at a party. A sun-bleached poster at a coffee shop. Tagged haphazardly on an Instagram post. A Reddit thread from three years ago with broken links. This shouldn’t be so difficult, should it?

Calgary, for all it's faults, is an incredibly kind city. It has community, the city has people organizing and building. People creating and show up for each other. But information lives scattered across bios and pages and newsletters, or just word-of-mouth. 

If you’re not already connected, and especially if you’re new to the city, finding your people requires a lot of labour on your end. We got tired of drawing a map, so we built something a little more robust. 

# Introducing Calgary Groups

**[Calgary Groups](https://calgarygroups.ca/)** is a free, searchable directory of over +150 grassroots organizations, clubs, activist groups, and community initiatives in Calgary.
We didn't make this trying to be a flashy social network. It's just a simple, durable index. A public resource helping people find where they belong.

You can search and filter by:
* **Organization type** (Nonprofit, Grassroots, Social Club, Chapter, Cooperative, Small Business)
* **Interests** (Environment, LGBTQ2S+, Indigenous, Anti-Racism, Tech, Urban Issues, Arts & Culture, Health & Wellness, and more)
* **Meeting format** (In-person, Online, Hybrid)
* **Location** (by quadrant or city-wide)

Every listing includes contact information, a description, and links to websites and social media. It's built to be fast, accessible, and usable on any device. And because the entire directory lives as plain text files in a [public GitHub repository](https://github.com/berryhouse-ca/calgary-groups), it's transparent and editable. Not locked inside any platform.

## Why This Matters

When I tried to start my own community, [Write Club](https://writeclub.ca/) at Mount Royal University three years ago, one of the hardest parts was being *findable*. We'd post on Instagram, put up posters, send emails. But unless you were already in our network or someone told you directly, how would you know we existed? The same goes for so many groups I've encountered:

* The **Lavender Club YYC**, creating sober social spaces for lesbian and sapphic women
* **Street Cats YYC**, doing harm reduction outreach with compassion and dignity
* **Hollow Bone Healing Lodge**, supporting Indigenous cultural resurgence through land-based learning
* **T7 Mask Bloc**, distributing free N95 masks and advocating for community care
* **More Neighbours Calgary**, fighting for affordable housing and zoning reform
* **The Living Room YYC**, creating low-pressure social spaces for autistic and neurodivergent adults

These groups are invisible because the infrastructure to make community visible only exists in fragments, in dozens of disconnected places that you have to already know about to find. Calgary Groups is an attempt to change that.

## How It Works (And Why It's Built This Way)

We built this as a static website using [Eleventy](https://www.11ty.dev/), [Tailwind CSS](https://tailwindcss.com/), and [Alpine.js](https://alpinejs.dev/). It's hosted on [Netlify](https://www.netlify.com/), costs effectively nothing to run, and loads fast.

There's no database, no login system, no tracking, no ads.
Each organization is a simple Markdown file stored in the repository. 

When someone submits a new group or updates an existing one, it's added as a file. The site regenerates, and the directory updates. Simple, transparent, and maintainable. This design is deliberate:
* **No platform lock-in.** The data isn't trapped in a proprietary system. It's just text files that anyone can read, fork, or download.
* **Low maintenance burden.** Static sites don't break when dependencies update or servers crash. They just work.
* **Community-editable.** Anyone can submit a group, flag an error, or propose changes via GitHub.
* **Accessible and fast.** The site loads instantly, works on any device, and follows web standards for accessibility.

## What's Included

Right now, the directory includes **155 organizations** across Calgary:
* **61 Nonprofits** (from large organizations like the Calgary Climate Hub to smaller groups like Calgary Vegan Society)
* **49 Grassroots groups** (such as the Calgary Student Movement, Walls Down Collective, and Muslim Voices for Palestine)
* **37 Social Clubs** (book clubs, sports leagues, hobby groups, etc.)
* **8 Chapters** of national/international organizations (Data for Good, Strong Towns, Revolutionary Communist Party, etc.)

We've prioritized groups that:
* Are community-led or grassroots-organized
* Center marginalized voices (LGBTQ2S+, Indigenous, disability, anti-racist, low-income)
* Focus on local organizing, mutual aid, and solidarity work
* Might be harder to find through mainstream directories

This is a starting point.

## Two Asks / Call-to-Actions

**1. Explore the directory.** Browse [calgarygroups.ca](https://calgarygroups.ca/) and find something that speaks to you. Maybe it's a book club you didn't know existed. Maybe it's an activist group working on something you care about. Maybe it's a social club that sounds exactly like what you've been looking for.

**2. Help us grow it.** If you know a group that should be listed, [submit it through our form](https://calgarygroups.ca/submit/). If you see outdated information, let us know. If your own organization isn't listed, add it. This only works if it's actually used and maintained by the community.

## About Berry House

Calgary Groups is a project by **[Berry House](https://berryhouse.ca/)**, the small studio I run focused on building fast, accessible websites and thoughtful, effective writing.

Berry House exists to help independent creators, nonprofits, and community organizations own their platform. We build websites with [Eleventy](https://www.11ty.dev/) and the [JAMstack](https://jamstack.org/), write clear and compelling copy, and advocate for accessible, sustainable web practices.

We operate on a dual mission: standard rates for corporate clients fund pro-bono and pay-what-you-can work for marginalized communities, vulnerable individuals, and low-income nonprofits. Every paid project helps us continue supporting those who need it most.

If you need a website, help with content strategy, or just want to talk about the future of the independent web, [reach out](mailto:hi@berryhouse.ca). I'd love to hear from you.

# A Note of Thanks

This project wouldn't exist without **Yvonne Berger**, who did the incredible, painstaking work of curating and organizing these 155 listings. Building the directory was the easy part. Finding, researching, and categorizing every group? That's the real work. Thank you, Yvonne.

## What's Next

This is version 1.0. It's functional, usable, and ready to be tested by real people. But there's more we want to build:
* Enhanced filtering (by accessibility features, languages served, cost/free status)
* A way to mark groups as "verified" or "last updated"
* Better mobile UX
* RSS feeds for new/updated listings
* An API for other tools to pull from this data

But first, we need to know if this is useful. We need people to use it, share it, and help us fill in the gaps.