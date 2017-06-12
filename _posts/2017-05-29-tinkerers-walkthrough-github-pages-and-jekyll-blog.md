---
title: Tinkerers Walkthrough Github Pages and Jekyll blog
date: 2017-05-29
description: A summary of codebase of the template, and  survey of required tasks
categories:
    - technology
image: https://source.unsplash.com/LUgHXvLe_kM/2000x1322?a=.png
---
_If you asked me two months ago whether I would ever develop a website, I would have scoffed at that question. From the looks of my blog, it has changed a lot. What changed?_

Github Pages happened, honestly. It allowed a fairly quick way to get the blog in production because of Jekyll. The issue was now that the more I spent the time tweaking or online, the more I wanted to change the code. The way I felt empowered to stab at the code with new features was through a thorough reading and understanding of what I was dealing with.

It is a skill that is very essential, I believe. And today, I want us to work through our template together with the aim of getting a lay of the Jekyll basics. 

Before we dive in, let's install one of my favorite utilities, `tree`. It allows us to do something like this,
```bash
tree
.
├── 404.html
├── about.html
├── apple-touch-icon.png
├── blog
│   └── index.html
├── _config.yml
├── contact.html
├── contact-success.html
├── css
│   └── screen.scss
├── _data
│   ├── footer.yml
│   └── navigation.yml
├── Gemfile
├── Gemfile.lock
├── images
│   ├── favicon.png
│   ├── logo
│   │   ├── dark.svg
│   │   └── light.svg
│   ├── screenshot-buttons.svg
│   └── _screenshot.jpg
├── _includes
│   ├── list-posts.html
│   ├── navigation.html
│   ├── post-title.html
│   ├── relative-src.html
│   └── social-icon.html
├── index.html
├── js
│   └── main.js
├── _layouts
│   ├── archive.html
│   ├── default.html
│   ├── page.html
│   └── post.html
├── LICENSE
├── _posts
│   ├── 2016-07-20-what-is-a-friend.md
│   ├── 2016-07-28-psychology-of-friendship.md
│   ├── 2016-08-02-life-cycle.md
│   ├── 2016-08-06-development-issues.md
│   ├── 2016-08-12-health.md
│   └── _defaults.md
├── README.md
├── robots.txt
├── _sass
│   ├── blog.scss
│   ├── contact.scss
│   ├── elements.scss
│   ├── footer.scss
│   ├── forms.scss
│   ├── landing-page.scss
│   ├── layout.scss
│   ├── mixins
│   │   ├── columns.scss
│   │   └── flexbox.scss
│   ├── navigation.scss
│   ├── staff.scss
│   └── variables.scss
├── siteicon.png
├── _staff_members
│   ├── anna.md
│   ├── betty.md
│   ├── _defaults.md
│   ├── gerald.md
│   ├── james.md
│   ├── robin.md
│   └── tom.md
└── touch-icon.png

12 directories, 58 files
```

This is, indeed, our directory, jekyllblogger.github.io. It would be helpful if you open the files along side, although, I will attaching more important snippets wherever required.

## 404.html
This is, undoubtedly, our error page. 404 is the error code for http page query to be not found. So, this is the page that people get if they have a broken link.
```
---
title: Not Found
description: This page doesnt exist!
image: https://source.unsplash.com/BcoGknSqlDc/2000x1322?a=.png
permalink: /404.html
layout: page
---
```

Now, the syntax is pretty straight-forward. The issues I find here though, are:
1. `title` seems a little dull. That's good for a professional website but I want every bit of the site to express me. I try to be corny with stuff and, that's what I would like this 404 page to be.
2. The image is so out of place. But it is a template. They could not have overdone this image.

Few things to notice are:
1. `permalink`: i.e., permanent link. So, Jekyll defaults to find this 404.html page in case of broken links.
2. `layout`: as we will encounter later, `layout` is the structure of different types of pages you might have. Jekyll is basically storing html in a rigid structure, then, when built, it finds these chunks of html and puts them together with css; voila! Your website is served.
3. `unsplash`: [Unsplash](https://unsplash.com) is a photo sharing site with original photos. The best part is that they are very free to use. These photos are professionally taken shots that are being uploaded by photographers, and curated by moderators. It is a beautiful website, don't blame me for your addiction.

## about.html
This is, again, an obvious page. This is the page where we introduce the website, and ourselves.

The structure is similar to `404.html` but it has a number of lines of html after the `---`.
Talking about `---`, the code between two of those is the YAML front matter. It allows for assigning various values here. 
On comparing this with the previous page, we are missing `layout`.

Let's open the website alongside too. We can relate that whatever that within the first `<section>` tag is only the background picture and, the page title and description.

Everything within the other section is the content on white. Amazingly, it lists staff members. It is good idea for a blog that is maintained by multiple people or even product sites with team profiles, maybe.

## apple-touch-icon.png, touch-icon.png and, siteicon.png
These are almost all the same. These could be the icon on the top left corner. A practice to find where they fit in is to either change them or remove them temporarily to gauge from errors or changes, what is their function?

## blog
The `blog` folder is the essentially a placeholder for the permalink `jekyllblogger.github.io/blog`. It has an `index.html` to be loaded when someone goes to that link. 

`index.html` itself is similar to the `about.html`, in terms of two sections; one for the banner with the title, the other for the content.

Content itself is similar through the use of similar `{% include ... %}` and `{% if ... %}`. 
Discussing them, they are sort of text manipulators. Jekyll has two text manipulation agents, syntactically, they are `{{ ... }}` and `{% ... %}`. Now, the double braces are basically placeholders. They are an indication of what actual text will be there. Remember, Jekyll actually creates html files by putting together chunks of code.
`{% .. %}` is the real manipulator that allows for various activities to be performed on text through the means of `if` or `for` statements.

Another thing to notice is are the `<div>` tag classes. These will be useful when creating a new page.

## \_config.yml
`_config.yml` is the configuration for the Jekyll site. It is an instruction set as to how to go about developing the website. It has a list of variables with values and, keywords. If you see code lines 7 through 9, those are your variables.

Line 12 explains to us that `siteicon.png` is the logo. Where is it used? We might gain that knowledge at a later stage.

Now, `gems` are `ruby` packages; the ones in our `_config.yml` are those plugins we are using.

Because we are usign a template built for Jekyll not Github Pages specifically, we will have issues with some plugins.

There are default values set, too. A quick inspection tells us, that for all paths (`path:""`) the pages have default layout, but under specific paths or type, the layout may differ. It is like saying, one loves vanilla ice cream but if there is a chocolate one available, that's what they will go for. Additionally, when they are on the beach, they want butterscotch ice cream. 

