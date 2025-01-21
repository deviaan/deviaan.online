---
date: 2024-10-04
draft: false
title: 'Up and Running'
summary: My first post! I'm not sure if it's a tradition, but in this one I just talk about why I wanted to make this and how I made it. Not really a tutorial, but more just picking reasons to do X over Y, along with links to resources that helped me get started!
---
# Up and Running!

Well that wasn't so hard! After years--decades even--of wanting to set up a personal website, I've finally done it! It's easier than ever with the only hard part being _actually_ getting started. The whole thing is a bit wonky still, it'll probably take me a while to get it just right. That's the biggest thing I've learned--don't wait for it to be just right. It's much more important to get whatever it is you want out there and work on it, than it is to get it perfect. I've known that for years, I just could not internalize it. 

Take this post for example. In truth, I wasn't sure what to write about for my first post, so I just started putting words to the page and seeing what came out. Nothing amazing, to be sure, but still _something_. The most obvious thing to talk about here would be _why_ I did this and _how_ I did it. I have a feeling I won't have low hanging fruit for long, so I'm going to pick it while I can!

### Why not?

There's no real reason to make a personal website, especially in 2024, except that you just _want to_. For me, it's something I've wanted to do ever since I first used the internet at my public library. It's a fun hobby that let's you express yourself in a way that is easily shared with others and, while I don't think many people will read this, I do like the idea of some random person finding something useful or just neat on here. I know that some of my favorite places online are just random, small websites made by people I'll never meet.

That's not to say that I think you _should_ make one--only if you want to. There's a lot to learn, and it can be annoying at times to get things to look the way you want them. I haven't even started thinking about making this thing phone friendly. Still, if you are a curious person I think making a personal website is a fine hobby to have!

There's a fun spirit in the old-style web. Each site reflecting the personality and skills of the creator, crawling or surfing through them to find interesting things. It's harder to go viral, never mind to monetize, things like this--which is exactly the point. I wanted something that was just for fun, not a "potential source of income" or whatever. A true waste of time.

### Making this website

There's a million different ways to get started. If you want something more comprehensive, I recommend taking a look at the guide at [32 Bit Cafe](https://32bit.cafe/cyowebsite/). They cover a ton of different options for your skill, time, and money. What I go over here is just what I chose to do, and why I chose to do it. I found that hearing about why people went the direction they did helped me a lot in picking my path through the web.

#### Scope and hosting

At my day job, I'm a backend developer. To me, this meant that my hobby site needed to be as simple as possible. I don't want to write endpoints or deal with databases for fun, when I do that all day already. I also knew I wanted to use as little JavaScript as possible--just good old HTML and CSS. My primary goal is just to have a fun site where I can just drop whatever I want. The simplest option for this, of course, would be to use an existing service, but I wanted to have more control over the website then a lot of these services allow. Key among these is my desire to have my own custom domain--because I think it's really cool--and to be able to grow or shrink the website based on whatever I want to do.

Right away I had a few options:
1. A [static site generator](https://github.com/myles/awesome-static-generators)
2. Down and dirty, hand crafted HTML

A static site generator is better for larger sites, and makes updating them _much_ simpler. However, I didn't want to spend time learning a new tool when I didn't have a clear picture of what I wanted to make yet. I decided that to start, I'll just make some plain old HTML pages and link them together. This is quick and easy, though not very scalable. If I ever need an SSG, I'll spend some time looking at the options available or just make one that works specifically for my site.

For hosting, I went with [Porkbun's static webhosting](https://porkbun.com/). There's free options, of course, like [Github Pages](https://pages.github.com/) or [Neocities](https://neocities.org/), but I like being able to get support if I need it and Porkbun handles the SSL certs for me. I already use them as my domain registrar so everything was really easy, just click and go. I linked Porkbun to a Github repo so I don't even need to upload a zip of my website, as soon as I push the changes to the main branch they go live on the site.

#### Tools

Since I know I wanted to make a very simple website, the tools I needed would be equally simple.

- For text editing, good old [Notepad++](https://notepad-plus-plus.org/). The first text editor I ever used (well except notepad), and something that very much fits in with the spirit of what I'm trying to do here. I really hope I never need anything more advanced...though getting my `vimrc` up to date sounds fun too.
- [Gimp](https://www.gimp.org/) and [Inkscape](https://inkscape.org/) for image generation. I may not be much of an artist, but I want to do as much of this website on my own as I can.
- [Github Desktop](https://desktop.github.com/download/) for managing my repo. I normally use the CLI or the built in tools in my IDE for Github, but this is a good opportunity to try out the stand alone app. It's pretty friendly, and a good alternative if you don't want to bother with the command line.
- [Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/install) with [Python](https://www.python.org/) using [http.server](https://docs.python.org/3/library/http.server.html) for local testing. I use Python at work, so I don't want to write Python code if I can avoid it, but `python -m http.server` in my project folder is a _really, really_ easy way to test out the website. I don't think I strictly need it, but it's closer to what is actually happening on the live site. Take a look at the [differences](https://stackoverflow.com/questions/40204913/difference-between-localhost-and-opening-html-file) if you're interested.
- Google Drive to host images. If you have a publicly accessible folder, you can use it [host your images and other files](https://stackoverflow.com/questions/15557392/how-do-i-display-images-from-google-drive-on-a-website). Porkbun has a 2GB limit for the website at my current tier, which should be plenty especially if it's nearly all text.

#### Workflow

That's really all there is to it! When I work on the site I just follow a few steps: 
1. Open the terminal and navigating to my project folder then starting the server with `python -m http.server`. 
2. Open Firefox and browse to `http://localhost:8000/`
3. Open Notepad++

From there, it's just a matter of deciding what I want to do and making the changes! [32 bit cafe](https://32bit.cafe/) has great tutorials to get started, but you can also check out [MDN](https://developer.mozilla.org/en-US/) or [W3Schools](https://www.w3schools.com/) if you want documentation or how-to's.

For inspiration, I browse [Neocities](https://neocities.org/) websites or go to [Marginalia](https://search.marginalia.nu/explore/random) to see what I can find.

Only other thing I use is [Obsidian](https://obsidian.md/) for note taking, and to write my posts. As much as I like the old web, I don't want to keep what I write in just an HTML file. Obsidian is a great app that keeps everything in plain text, meaning you'll be able to access it even if you don't want to use Obsidian anymore.

### What's left to do?

The most important thing, to me, was to just get on the web. The second most important thing is to _not_ scope creep. If this thing becomes a job, I'll very quickly abandon it. I'd much rather just go slowly and add things as I need them, then try to come up with some whole grand plan.

For the near future, the only things I know I want to do are:
1. Finish setting up the other pages and tables
2. Coming up with a system for the more tedious parts of maintaining a website

For the second point, this will _probably_ mean using some kind of SSG or--more likely--just writing a simple one myself. After all, I just need it to read some posts to build a couple of tables with links to them. How hard could it be?

As far as content, I'll start out by just sharing my thoughts on whatever I happen to be into at the moment. The Log pages are just my best guess at what I'll like to write about, and I will add or remove them as needed. Long term, I'd like to showcase some projects on here but I'm not quite sure what yet. For now, though, I'm just glad to have put something out there!