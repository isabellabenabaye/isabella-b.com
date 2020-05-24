---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "7 Ways You Can Further Customize the Hugo Academic Theme"
slug: hugo-academic-customization
summary: "Sharing some of the ways I customized this site for anyone that would like to make similar adjustments to theirs ✨"
authors: []
tags: [hugo academic, academic theme, hugo, tutorial, customization]
categories: [tutorial,hugo,academic theme]
date: '2020-05-05'
reading_time: true

external_link: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: true

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter
links:
- name: 
  url: https://medium.com/@isabellabenabaye/7-ways-you-can-further-customize-the-hugo-academic-theme-393da277a04e?source=friends_link&sk=93ae6ba604cac1ac03f9009dfc894abf
  icon_pack: fab
  icon: medium-m

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
toc: true
# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---


Out of the box, the [Academic theme/framework](https://sourcethemes.com/academic/) is already *highly* customizable and just by adjusting the basic settings in `params.toml`, organizing and filling out your homepage widgets/about, and the assigning your fonts and theme colors of choice, you can already get it to look much more like your own, all without editing any code. Academic's [documentation](https://sourcethemes.com/academic/docs/get-started/) is very thorough and helpful, especially when starting out and if you're new to Hugo like I was. I could make a whole other blog post about why I love the Hugo Academic framework and why I'd recommend it to anyone wanting to create a website (because why not? It's free!). 

But if you're like me and particular about how you want it to look, there may be more things you'd like to adjust that aren't in the out-of-the-box settings. As I started to customize these things, I found that some were not that easy to find or figure out, so I thought I'd compile and share these settings in case anyone else would like to customize them as well.

{{% alert note %}}
An important thing to know before we begin is how Hugo uses [template lookup](https://gohugo.io/templates/lookup-order/). Basically, the theme files in `/themes/hugo-academic` tell Hugo how to build the site, but you can override this by placing folders and files of the same structure in your `root` folder. Here is an example from the [Academic documentation](https://sourcethemes.com/academic/docs/customization/#override-a-template):
 >For example, say we wish to add some HTML code to the navigation bar. Let’s copy the relevant file `themes/academic/layouts/partials/navbar.html` to `layouts/partials/navbar.html` (at the root of your site, not in `themes/academic/`), creating the `layouts/partials/` folders if they do not already exist. Now you can add the HTML code you want to your copy of the file, which will override Academic’s version.

**At the time of this post, Academic's latest release is v4.8.0.**
{{% /alert %}}   
<br /> 

**What I'll be covering:**
- [Full list of theme colors you can customize](#full-list-of-theme-colors-you-can-customize)
- [About widget without a summary](#about-widget-without-a-summary)
    - [Using my `about.html`](#using-my-abouthtml)
    - [Adjusting the `html` yourself](#adjusting-the-html-yourself)
- [Removing box-shadows](#removing-box-shadows)
- [From 'posts' to 'blog'](#from-posts-to-blog)
- [Changing displayed post dates](#changing-displayed-post-dates)
- [Adjusting post font size & page width](#adjusting-post-font-size--page-width)
- [Customizing the alert notes/warnings](#customizing-the-alert-noteswarnings)
- [That's all for now!](#thats-all-for-now)
  
<br />


## Full list of theme colors you can customize
If you won't be using one of the [themes](https://sourcethemes.com/academic/themes/) provided by Academic, the documentation shows you how you can [create your own theme](https://sourcethemes.com/academic/docs/customization/#custom-theme) and set the colors yourself. If you're creating your own `data/themes/my_theme.toml` here is a list of parameters you can specify, just put in your preferred colors. [Coolors](https://coolors.co/palettes/trending) is a great color palettes resource.
```markdown
# Theme metadata
name = "my_theme"

# Is theme light or dark?
light = true

# Primary
primary = "#EF476F"

# Menu
menu_primary = "#F7F7F7"
menu_text = "#FCA311"
menu_text_active = "#0EAD69"
menu_title = "#118AB2"

# Backgrounds
background = "#F7F7F7"
home_section_odd = "#F7F7F7"
home_section_even = "#F7F7F7"

dark_background = ""
dark_home_section_odd = ""
dark_home_section_even = ""

link = "#D90429"
link_hover = "#118AB2"
```

<br />

## About widget without a summary
If you only want to show your photo and social links in your `about` widget like I did, you'll need to override Academic's `about.html` located in `hugo-academic/layouts/partials/widgets` by putting in an html layout in your root `layouts/partials/widgets/`.    
There are two ways you can approach this, by    
(1 - **recommended**) using my `about.html` if you want it to be formatted exactly like [mine](https://isabella-b.com) is (centered, avatar & links only),    
(2) adjusting the `html` yourself.    

Here are the steps for each:

#### Using my `about.html`
You can find my `about.html` [here](https://gist.github.com/isabellabenabaye/cd018cb26027657ae9f9c6900f4fc3cd). 
- Create your `about.html` (keep that file name so that you don't have to adjust `about.md`) in your root `layouts/partials/widgets/`
- Copy-paste the contents of mine into your blank `about.html`    
That's it, your widget should update the next time that you `serve` it!

#### Adjusting the `html` yourself
  - Copy-paste the `about.html` located in `hugo-academic/layouts/partials/widgets` into your root `layouts/partials/widgets/`
  - Remove the entire summary section, from `<div class="col-12 col-lg-8">`, everything in between, til its matching `</div>`
  - Change `<div class="col-12 col-lg-4">` to `<div class="container centered">` as seen below:   

{{< figure src="about-widget.png" title="Before & after" lightbox="true" >}}
<br />

## Removing box-shadows
{{< figure src="box-shadow.png" title="With & without a box shadow" lightbox="true" >}}
**Removing the navigation bar's box-shadows**   
Create `assets/scss/custom.scss` in your root if it doesn't already exist. Paste the following into the file.
```css
 .navbar {
  height: 70px;
  background: $sta-menu-primary;
/* this is the part that takes out the shadow & the only edit */
  box-shadow: none;  
  font-size: 18px;
  font-weight: 900 !important;
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  z-index: 1030;
  padding: 0 1rem;
```   

**Removing the card component's box-shadows**   
Create `assets/scss/custom.scss` in your root if it doesn't already exist. Paste the following into the file.
```css
 .card-simple {
  background: #fff;
/* this is the part that takes out the shadow */
  box-shadow: none;
  border: 1px solid rgba(0,0,0,.09);
  border-radius: 3px;
  margin-top: 20px;
  padding: 15px 20px 15px 20px;
}

.card {
  margin-bottom: 1.5rem;
  overflow: hidden;
  text-overflow: ellipsis;
  background: #fff;
/* this is the part that takes out the shadow */
  box-shadow: none;
  transition: all 0.2s ease-out;
}
```   
<br />

## From 'posts' to 'blog'
{{% alert note %}}
**UPDATE**   
Since the writing of this post, I discovered a section in the Academic theme docs that shows another (easier) way to do this using permalinks. You can find it [here](https://sourcethemes.com/academic/docs/customization/#permalinks) under **Example 2**.
{{% /alert %}}
Instead of your posts having the default slug `your-site.com/posts/your-post`, you can change it to `your-site.com/blog/your-post` by doing the following:
- Rename the `posts` folder in your root `content/` to `blog`, or create a folder in `content/` called `blog`
- Copy `themes/hugo-academic/layouts/section/post.html` to your root `layouts/section/`
- Rename the new file located at `layouts/section/post.html` to `blog.html`   
<br />

## Changing displayed post dates
You'll need to override Academic's `page_metadata.html` located in `hugo-academic/layouts/partials/` by putting in an html layout in your root `layouts/partials/`. Copy the one in Academic's and paste it to yours so that this is its path: `layouts/partials/page_metadata.html`.  

We'll be editing your copy. This is a snippet from the original (in your text editor, find "`article-date`"):
```
  {{ if not (in (slice "talk" "page") $page.Type) }}
  <span class="article-date">
    {{ $date := $page.Lastmod.Format site.Params.date_format }}
    {{ if eq $page.Type "publication" }}
      {{ $date = $page.Date.Format (site.Params.publications.date_format | default "January, 2006") }}
    {{ else }}
      {{ if ne $page.Params.Lastmod $page.Params.Date }}
          {{ i18n "last_updated" }}
      {{ end }}
    {{ end }}
    {{ $date }}
  </span>
  {{ end }}
```
We'll replace that with:
```
  {{ if not (in (slice "talk" "page") $page.Type) }}
  <span class="article-date">
    {{ $date := $page.Date.Format site.Params.date_format }}
    {{ if eq $page.Type "publication" }}
      {{ $date = $page.Date.Format (site.Params.publications.date_format | default "January, 2006") }}
    {{ end }}
    {{ $date }}
  </span>
  {{ end }}
```
**Explanation:** The new code uses the `Date` instead of `Lastmod` & removes the else argument in the if statement that uses `last_updated`.   
<br />

## Adjusting post font size & page width
Create `assets/scss/custom.scss` in your root if it doesn't already exist. Paste the following into the file & adjust the `max-width` and `font-size` to your liking.
```
.article-container {
  max-width: 850px;
  padding: 0 20px 0 20px;
  margin: 0 auto 0 auto;
  font-size: 20px;
}
```   
<br />

## Customizing the alert notes/warnings
All of the options to edit the formatting of the alert notes and warnings can be found in `themes\hugo-academic\assets\scss\academic\_root.scss` under this heading, which you can use your text editor to find:
```
/*************************************************
 *  Article Alerts (Shortcode) and Asides (Mmark)
 **************************************************/
```
Create `assets/scss/custom.scss` in your root if it doesn't already exist and copy from that code snipped above until the end of the file; these are all of the style settings for the alert boxes.

Choose which parts to edit to your liking. For example, these are the parts I edited to make the alert box above:
```
.article-style aside p,
div.alert > div {
  position: relative;
  display: block;
  /* I made the font size smaller & adjusted the margin-left */
  font-size: 0.8rem;
  margin-left: 1.7rem;
  margin-top: 0;
  margin-bottom: 0;
}

/* I also changed the color of the icon & its top & left positions */ 
.article-style aside p::before,
div.alert > div:first-child::before {
  position: absolute;
  top: -0.3rem;
  left: -2rem;
  font-size: 1.4rem;
  color: #0EAD69;
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  content: '\f05a';
  width: 1rem;
  text-align: left;
}

/* You can edit the borders and backgrounds here */
.article-style aside,
.alert-note {
  color: #26547C;
  background-color: #F7F7F7;
  border-color: #0EAD69;
}

.alert-warning {
  color: #cd0930;
  background-color: #fff5f7;
  border-color: #ff3860;
}
```   
<br />

## That's all for now!
I know that this tutorial involves a lot of file and code creating and copying and can be confusing, especially if you're not familiar with how Hugo works, so if you have any questions don't hesitate to [DM/tweet me](https://twitter.com/_isabellamb) or comment below 😊 if there are any other customizations you noticed I did on this site that you're interested in trying but I didn't cover it, I'll be happy to tell you how I did that as well. You can find the source code for this site [here](https://github.com/isabellabenabaye/isabella-b.com).
 
If you want to see more of what Academic is capable of, check out [Alison Hill](https://alison.rbind.io)'s personal site. Before seeing hers I didn't know that it was possible to do so much with Academic & it's what inspired me to try it out myself (thank you Alison!). As I was building this I also referred to her code to figure out how to adjust things. She has several blog posts about how to set up a Hugo site using RStudio (which is what I did) and how to use and customize it as well! They're great resources that you should check out if you haven't already, especially if you're using RStudio.