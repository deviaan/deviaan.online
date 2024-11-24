---
date: 2024-11-23
draft: false
title: 'Improving_workflow'
summary: 'Getting up and running is only part of the problem. I found my workflow very cumbersome which made writing feel more like a chore than something fun. Here I talk about the changes I made to make updating the website painless.'
---
# Improving Workflow

I knew that as much fun as I was having making this website in hard coded HTML, it wasn't going to scale and eventually writing a post would be frustrating and tedious. It was a great way to start--I built something instead of spending all my time learning about tools--but, if I wanted this project to continue, there were a few key pain points that I needed to tackle.

## A better way

I spent a lot of the last month researching website making tools. I knew I wanted something flexible and simple. Content Management Systems, like WordPress, and site builders are great, but were more than I needed. I tried writing some scripts myself to build the website, though I found that my time was then spent on making a tool rather than making a site.

Static Site Generators were exactly what I as looking for and I decided to go with [Hugo](https://gohugo.io/). It's just a single binary making it very easy to install and use. The [documentation](https://gohugo.io/documentation/) is great and the [template language](https://gohugo.io/templates/) made a lot of sense to me. There are also a lot of [themes](https://themes.gohugo.io/) to get started quickly, or to mine for inspiration.

The other SSGs I looked at were [Jekyll](https://jekyllrb.com/) and [Statiq](https://www.statiq.dev/). Jekyll feels very similar to Hugo. The templating language, [liquid](https://shopify.github.io/liquid/tags/variable/), reminds me of [Jinja](https://jinja.palletsprojects.com/en/stable/), which is something I've used before. In fact, if I had found Jekyll before Hugo I probably would have gone with it instead.

Statiq, on the other hand, _can_ be used as a simple binary the same way Hugo is, but what made it look interesting to me was the that you could define your entire pipeline for converting your Markdown files into a website. While I don't really need that much flexibility right now, I'm glad it's there if I ever do.

### Converting the website to Hugo

The easiest way to get started with Hugo is to use a [theme](https://themes.gohugo.io/). This will give you a website that looks professional and is trivial to set up. I wanted to keep my site looking similar to what I already have so instead I decided to recreate my site using a layout.

I started by grouping the parts of my website into three key categories:

1. Things that go on every page
2. Individual parts of a page that I want to reuse
3. The homepage

The first part is easy enough. Every page had to have the same header, navigation bar, banner, and (eventually) footer. I just took all this and put it into a file called `baseof.html`. Hugo takes this file and uses it construct every other page on your site. The `main` section is defined by each individual templates.


```html
<!DOCTYPE html>
<html lang="en">
    {{ partial "head/head.html" }}
    <body>
        <div class="page">
            {{ partial "header/site-header.html" }}
            {{ partial "menu/menu.html" }}
            <main>
                {{ block "main" . }}{{ end }}
            </main>
            {{ partial "footer/site-footer.html" }}
        </div>
    </body>
</html>
```


The components are known as `partials` and refer to the second category: parts of a page that I want to reuse. Each one goes into its own file that contains only the HTML elements required for that component. This makes it easy to reason about a particular part of a webpage, and keeps your layout organized so whenever you want to change something, you know exactly where to go. The partial for my `head` element, for example, only has the content that needs to go in the `<head>` section, and updating it here updates it site-wide.

```html
<head>
    <title>deviaan - Online
        {{ if .Title }}
            | {{ .Title }}
        {{ end }}
    </title>
    <link rel="stylesheet" type="text/css" href="/css/styles.css"/>
    <meta charset="UTf-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
    <meta name="description" content="deviaan's personal homepage"/>
    <link rel="icon" href="/images/icon.png" type="image/png"/>
</head>
```


The last thing that needed special attention was the homepage. This gets a special file called `index.html`. You can make a specific layout for any page you like, but in my case only the homepage needed it. For the other pages, there's two options: `single.html`, which renders any single page like this post or the [about page](/about) and `list.html`, which handles pages that have a group of things such as the [posts page](/posts) page. For both, I just used the example from the Hugo documentation.

I decided to change the layout of my home page into two simple two columns with posts on one side and updates on the other. The [example](https://www.w3schools.com/css/css_website_layout.asp) that W3Schools had in their tutorial seemed good to me, so I used that with a small variation to limit the horizontal width of the content.


```html
{{ define "main" }}
<div class="homepage">
    <div class="posts">
        {{ range first 5 (where .Site.RegularPages "Section" "posts").ByDate.Reverse }}
            {{ partial "cards/posts.html" .}}
        {{ end }}
    </div>
    <div class="updates">
        <h3>Latest Changes</h3>
        {{ range first 5 (where .Site.RegularPages "Section" "updates").ByDate.Reverse }}
            {{ partial "cards/updates.html" .}}
        {{ end }}
    </div>
</div>
{{ end }}
```

The CSS came from the W3 Schools example, combined with CSS I had already written for my site, and a [new Markdown style](https://github.com/simonlc/Markdown-CSS/blob/master/markdown.css) for the posts that I found online. To simplify porting over the CSS style for the posts, I created a new class called `article` and just copied the parts I wanted from the full Markdown style.

```css
.article {
	a {
		// Styles any links inside of a tag with the article class
	}
}
```

You can find the full website on [github](https://github.com/deviaan/deviaan.online). It's very basic, not as fancy as the themes, but if you can find something useful in there feel free to use it!


## Deploying made easy

I'm using [porkbun](https://porkbun.com/) for both domain registration and static hosting. They can link directly to a github repository and automatically publish your site changes, which works great when your final website is contained in repo. However, now that my repo is instructions on how to build the website and not the website itself, it doesn't work exactly how I want it to. I definitely don't want my entire repo on the static host. There is probably a way around this, but it seemed like a great opportunity to learn how to use [Github actions](https://docs.github.com/en/actions).

To deploy manually, I only needed to run `hugo` on my local machine, then zip the `public` folder, and upload it to Porkbun. It's only three steps, but it was very frustrating when I would realize that I forgot to run `hugo` or didn't re-zip the `public` folder.

Luckily, there's already a bunch of actions on Github that I can use. So, after setting up some [secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions) with my FTP credentials, I used [an action to build Hugo](https://github.com/marketplace/actions/build-hugo) and another to [ftp my files to Porkbun](https://github.com/marketplace/actions/ftp-deployment). This runs automatically when I commit and push any changes to my site. Since I'm building when I upload, this also means I no longer need to track changes to my `public` folder, which makes my repo just a bit cleaner.


```yaml
name: Deploy to Porkbun
run-name: ${{ github.actor }} deploying
on:
  push:
    branches: [main]
jobs:
  Deploy-Porkbun:
    runs-on: ubuntu-latest
    defaults:
      run:
        shell: bash
    steps:
    - name: Checkout latest
      uses: actions/checkout@v4

    - name: Build Hugo
      uses: lowply/build-hugo@v0.139.0
    
    - name: Publish changes
      uses: airvzxf/ftp-deployment-action@latest
      with:
        server: ${{ secrets.FTP_SERVER }}
        user: ${{ secrets.FTP_USERNAME }}
        password: ${{ secrets.FTP_PASSWORD }}
        local_dir: "./public"
```

## Writing should be fun

The last thing I needed to do was find a way of writing that felt natural and fun. I could use VS Code for this as well, though I prefer to use that only for coding and small changes. Having a dedicated tool for writing would help me have the write mindset whenever I sat down at my computer. This post was written using [Ghostwriter](https://ghostwriter.kde.org/)--a distraction free Markdown writing tool, which so far I really like!

The other tool I use is [Obsidian](https://obsidian.md/). It's designed for note taking and knowledge management with a ton of great features--including the ability to export your note vault as HTML. It uses Markdown for all its files so, besides using it for all my notes, I can use it to write more complex articles.

I use [Markor](https://github.com/gsantner/markor) whenever I need to write something on Android. While it's rare for me to do this on my phone, outside of making simple updates, I often do write on my tablet. Especially now that I don't carry around a laptop. Additionally, both Github and Obsidian are available on Android, which means I can have my notes and update my website from mobile if I ever need to.


# What's next?

In the immediate future, I'm looking forward to writing about something _other_ than the site itself. There are a few things I need to tweak, like the banner on the mobile version of the site, but none of those are really worth writing about outside of an update note.

At some point, I need to figure out how to handle images. The 2Gb of storage I'm using at Porkbun is more than enough for my site, but I don't want to saturate it with a bunch of images. For smaller, site-wide images, I don't mind dumping them in the static folder and referencing them as needed. For larger, page specific ones, I'm manually uploading to a public folder in my Google Drive and linking to them in the Markdown. There's clearly a better way to do this--especially when I'm exporting from Obsidian--but it hasn't become a big enough issue for me to worry about yet.