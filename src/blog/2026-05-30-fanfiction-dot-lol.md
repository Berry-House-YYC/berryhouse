---
layout: layouts/post.njk
title: 'Announcing Fanfiction.lol: A Manifesto on Human Creativity and AO3'
author: Brennan Kenneth Brown
date: '2026-05-30'
description: >-
  I deployed my own AO3 fork called fanfiction.lol, an independent fanfiction
  archive with no invite queue, fandom-agnostic moderation, and expanded content
  warnings. A manifesto on why fan communities deserve free infrastructure, the
  history of transformative works from Virgil to AO3, and the challenges of
  running a volunteer-powered archive at scale.
tags:
  - indieweb
  - technical
  - self-hosting
  - fandom
  - community
  - open-source
category: projects
---

At Berry House, we believe in accessible, self-hosted infrastructure that supports real communities. **fanfiction.lol** is the latest experiment in that direction: an independent, open fanfiction archive running on a homelab server. This post walks through why it exists, how it was built, and what it means for the future of fan communities.

A few days ago, I wrote a [guide for setting up a cheap, accessible server](https://brennan.day/homelab-for-the-beginner-you-can-self-host-your-own-server-on-50-hardware/). In truth, after being a front-end developer for over a decade, I realized that the full-stack wasn't as scary as I thought it'd be. But with the server up and running, I needed a real project to sink my teeth into. Something that would force me to have skin in the game.

Being on the [IndieWeb](https://indieweb.org/) for half a year now, I've encountered a lot of impressive, talented web developers and webweavers—I went over a few of them in [my love letter post](https://brennan.day/a-love-letter-to-everything/). One of them is a sysadmin I know who runs [SuperLove](https://superlove.sayitditto.net/), a fork of the codebase [otwarchive](https://github.com/otwcode/otwarchive), the codebase powering the largest fanfiction archive in the world, [Archive of Our Own](https://archiveofourown.org/), or AO3.

I was told this is notoriously difficult to set up, and that there are only a handful of these AO3 forks in existence. [SquidgeWorld](https://squidgeworld.org/), run by Walter, published the foundational bare-metal setup guide at [squidgeworld.org/works/34491](https://squidgeworld.org/works/34491). Squideworld was the [very first AO3 fork](https://fanlore.org/wiki/Squidge.org), launched in November 2020. Since then, a small constellation of independents has followed. 

I decided to try my hand at initializing and deploying one of my own, specifically because of the challenge. I purchased the domain fanfiction.lol for two bucks, set up my CloudFlare tunnel, populated the database, wrote quite a bit of janky Ruby script, and to my surprise things didn't take that long to get up and running (mostly though with the help of [Melo's guide](https://superlove.sayitditto.net/works/171), of course).

Let me tell you, the stack is a bit of a beast. There's Ruby on Rails 8.1.0 running on Ruby 3.4.6, MySQL for the database, Redis, Elasticsearch (which takes 2GB of RAM alone), and Memcached. They're all containerized with Docker Compose. The otwarchive codebase is a full-featured archive with work search, kudos, comments, collections, and the well-known AO3 tagging system. I wrestled with database initialization, Elasticsearch indexing, site skins (the CSS is stored in the database, not files, which makes design work hell), and configuring SendGrid for SMTP email notifications.

I deployed it to the server currently living in my basement behind a Cloudflare Tunnel, handling SSL and routing without opening my home ports to the internet. The whole thing runs in Docker containers: the Rails app, a background job worker, a scheduler for recurring tasks, and all the supporting services. It's a lot of moving parts, but Docker makes it manageable thankfully.

So, after sitting at my IDE for 20 hours straight and looking at site surprisingly running, I asked myself: do I actually want to do this for real? Do I want to be a webmaster for a fandom writing community?

The answer was an unhesitating yes.

## The Fanfics of Virgil, Dante, and Shakespeare

I've been writing my entire life, and have written a lot already about how I believe writing is sacred, even going as far as to proclaim it [is literal magic](https://brennan.day/storytelling-part-two-the-literal-magic-of-writing/). Writing is how we process the world and relieve some of that constant flooding of our minds. It's how we figure out our identity until something fits. Writing is good medicine.

And [fandom](https://blog.brennanbrown.ca/fandom-is-awesome-furries-are-awesome-bronies-are-awesome-cringe-is-awesome-fuck-you-1c7b5558457b?sk=18dabe2ea92ddb5165fd718ce85960c4) in particular is where a lot of that writing lives. The history of [transformative works](https://fanlore.org/wiki/Fanworks) is much longer than most people assume. 

Virgil wrote *The Aeneid* as an expansion of Homer, Dante planted his self-insert and contemporaries in Hell, Shakespeare himself [recycled plots](https://www.thedailystar.net/daily-star-books/news/exploring-the-transformative-power-fanfiction-3371596) from Holinshed and Ovid with creative abandon. People have always extended or deconstructed stories. Always have yearned for a rewritten ending or to give a voice to a background character. You see, the practice of taking a story that matters to you and doing something new with it is as old as storytelling itself.

And the Internet liberated the practice! LiveJournal in the early 2000s. FanFiction.net. Even zines before that, the physical stapled things circulated at conventions, mailed between strangers who found each other through classified ads in the back of genre magazines. [Fan communities](https://learnaboutpod.com/ep-132/) gave historically marginalised people (women and Queer people especially) spaces to write stories that the mainstream wouldn't write, to explore identities that the mainstream wouldn't represent, and to say things the mainstream wouldn't print. The shame often attached to fanfiction, the social condescension of "oh, you write that kind of thing," has always been a shame aimed at the people who needed these spaces most.

There is an incredible outpouring of love and creative labour in fandom, often dismissed by the general population, as well as by the "more serious" writing circles I've moved through. Fanfiction communities produce extraordinary writers. They have produced communities that have held people through some of the hardest years of their lives. 

They deserve independent, free infrastructure. And yes, it is that serious.

## What AO3 Has Become

[Archive of Our Own](https://archiveofourown.org/) is important. The [Organization for Transformative Works](https://www.transformativeworks.org/) built a non-profit, volunteer-run, ad-free archive legally defending fanwork as transformative expression. That is nothing short of remarkable. AO3 currently hosts over 18 million works across more than 77,000+ fandoms, and recently crossed 10 million registered users. That's a staggering amount of human creative energy freely shared.

But AO3 has, inevitably, become a massive institution. And institutions calcify. The OTW is an all-volunteer organization, and the strains of that model are visible. Internal documents have long acknowledged an "existing burnout problem" and volunteer hiring freezes, leaving time as a scarce resource across many projects. One OTW Volunteers and Recruiting chair described an "epidemic" of volunteer burnout and turnover that has plagued the organization since at least the early 2010s. The scale of the archive has only grown since then. Feature development that the community has requested for years moves slowly, when it moves at all. Policy and Abuse received approximately 28,000 tickets in 2024 alone, processed by volunteers. The bureaucratic overhead of running something this large, this carefully, and this democratically is enormous—and it shows.

And then there's the invitation system. On Archive of Our Own, there are currently 144,235 people on the waiting list, and they send 4000 invitations every 12 hours. It would take over two weeks for you to get an invite if you're at the back of the line. The invitation system exists so that AO3 can grow in a controlled manner, but a project like mine doesn't have that problem.

## What Makes `fanfiction.lol` different?

**Anybody is free to register on [fanfiction.lol](https://fanfiction.lol).** Unlike AO3 and the other forks, there is no queue or invite system. On Archive of Our Own, there are currently 144,235 people on the waiting list, and they send 4000 invitations every 12 hours. It would take over two weeks for you to get an invite if you're at the back of the line. You want to post your story on fanfiction.lol, then sign up. That's it. 

The site runs on the same open-source [otwarchive codebase](https://github.com/otwcode/otwarchive), which means it has the same robust tagging system, the same work search, the same kudos and comments and collections infrastructure.

What does that mean in practice?

**fanfiction.lol is fandom/discourse agnostic.** I care about the writing of fans, not discussions about what writing is good or problematic. There is no interest in fandom's internal politics. Write whatever you want. Tag it honestly so readers can find what they're looking for and avoid what they'd rather avoid.

**I take content warnings seriously.** The archive warnings have been updated to include Systemic Oppression, Colonialism, Ableism, Homophobia/Transphobia, Racism, and Real Person Fiction. These are important signals for readers who need them. The relationship tags currently include Aromantic/Asexual Spectrum, QPR, Non-Binary/Genderqueer Focus, Poly/Ensemble, and more. A tagging system should reflect the full range of what people actually write. If you think I've missed something, let me know and I'll add it!

**All tags are canonical.** On AO3, only certain approved tags are "canonical", which means they're searchable and wrangled by volunteers into consistent forms. The rest are secondary and freeform. Here, everything you tag goes into the searchable record.

**It's small. It's personal. It's mine.** And yours, too, if you'd like.

## My Limitations

I have not been actively involved in fandom spaces since I was a teenager. I'm thirty years old now. I approach this with no existing allegiances, no current involvement in any fandom's internal debates, no stake in any ship war or discourse cycle. I understand that some people will read that as disqualifying. But there's a real benefit to bringing fresh eyes somewhere, I think.

But I have been chronically online since Windows 98, and [I've run a writing community before](https://writeclub.ca/about), for three years. I've learned a lot of lessons from that experience, and I understand the dynamics at play.

Something else important that I want to note is that multiple owners of AO3 forks have told me that this is a difficult, unforgiving role. That there are a lot of bad-faith entitled people they've had to deal with, and have gotten harassed and stalked simply for operating a fanfiction website. I am not ignorant or naïve to how the Internet and people on it can be, but I do know I can handle it. 

I know how to moderate a space, and I know how to hold a line, and I do not believe that the possibility of harassment is a reason to leave the commons ungoverned or un-built. The commons must not be destroyed. Someone has to tend the infrastructure.

## Joy-as-priority

As the name makes obvious, [fanfiction.lol](https://fanfiction.lol) is supposed to be fun and joy in fandom and creation. It is supposed to be a place where the writing is the point. I care deeply about fans and their work, not the discourse around the writing, not status hierarchies, nor the arbiters of legitimacy. Write whatever you want and celebrate the fact that you made something.

I am bringing the [same good-faith, big-tent philosophy](https://brennan.day/what-does-it-mean-to-be-a-good-editor/) I bring to the IndieWeb and my life in general.

## Break Things, Please

Right now the site has only a handful of users, and fanfiction.lol is very much in active development. Things may break, data may occasionally get obliterated, and I am one person running this alongside [a lot of other web projects](https://brennan.day/indieweb).

If you're someone who enjoys fandom, I'd love for you to [sign up](https://fanfiction.lol/signup) if only to poke around, try to break things! Tell me what you find. The source code lives at [source.tube/brennan/fanfiction.lol](https://source.tube/brennan/fanfiction.lol). You can find me at [brennan.day/accounts](https://brennan.day/accounts) across the web. Send an email to [mail@brennanbrown.ca](mailto:mail@brennanbrown.ca) or find me on Mastodon at [@brennan@social.lol](https://social.lol/@brennan).

Write whatever the hell you want!

---

*At Berry House, we help independent creators, communities, and small teams build fast, accessible, self-owned websites. If you're interested in a community platform, a homelab, or a website you actually control, [see our services](/services/) or [get in touch](/contact/).*
