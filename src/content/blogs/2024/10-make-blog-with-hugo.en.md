---
title: I Finally Decided to Properly Build My Blog Using Hugo
date: 2024-10-12
slug: rebuild-blog-using-hugo
kind: page
draft: false
---

After leaving [temama.soy](https://temama.soy) neglected for so long, I finally decided to rewrite it into something that I can show people.

Mainly, I want to loosely document:

- My background (About)
- Descriptions and updates of the OSS I've built (Tools)
- Random thoughts and notes (Blogs)

## Structure

I came across [Hugo](https://gohugo.io/) by chance and decided to give it a try.  
Since my update frequency isn't going to be high, I remembered coming across Hugo when I was searching for a static site generator (apparently they call it SSG) CMS.

### Choosing a Theme

I browsed through the Blog tag on [Hugo Themes](https://themes.gohugo.io/), and these four caught my eye:

- [adityatelange/hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) ([demo](https://adityatelange.github.io/hugo-PaperMod/))
    - Simple, minimal movement
    - The way it assumes the top page text is specified in the config didn’t quite fit what I had in mind
- [humrochagf/colordrop](https://github.com/humrochagf/colordrop) ([demo](https://humberto.io/))
    - You can set a theme color that spreads across the whole site, leaving a strong impression
    - Since I've already decided my theme color will be [Nakakobai-iro](https://irocore.com/kobai-iro/) (a deep pink), it seemed like a good fit
- [Fastbyte01/KeepIt](https://github.com/Fastbyte01/KeepIt) ([demo](https://suspicious-archimedes-ab369d.netlify.app/))
    - Suitable for simple blogs
- [g1eny0ung/hugo-theme-dream](https://github.com/g1eny0ung/hugo-theme-dream) ([demo](https://g1en.site/))
    - It looks nice when images are lined up in the post list
    - But the motion when clicking the icon to switch to the portfolio page didn’t quite sit right with me

After trying out a few, I settled on PaperMod. The reasons are:

- After writing and placing a few posts, it turned out just the way I imagined
    - Hugo themes can be a bit tricky depending on the theme, especially when it comes to how lists are displayed, so I couldn't just pick one based on design alone
- Since my focus is more on blogging than building a portfolio, I liked how it could show a list of blog posts on the home page
    - I ran into an issue where only Blogs or Tools were showing up in the list, but after a closer look, I found a [small note in the documentation](https://github.com/adityatelange/hugo-PaperMod/wiki/FAQs#posts-from-only-one-foldersection-visible-on-home-page) that explained the issue:
    - If you don’t specify `params.mainSections`, Hugo defaults to `sites.mainSection`, which limits what gets displayed.

### Deployment

I set up Nginx on GCE and just dropped the `hugo`-generated files directly.  
Soon, I'll make it so I can deploy with GitHub Actions (feeling motivated).

### Bilingual Support

I'm feeding the articles I write in Japanese into ChatGPT to get an English version and will put it up as well.  
I’ll review and fix any parts where the nuance seems off, at least.  
By placing both `article-name.ja.md` and `article-name.en.md`, PaperMod conveniently provides links between the two versions.

---

Hugo is great! Someday I’d like to write my own theme too.  
I want to incorporate Nakakobai-iro somewhere.
