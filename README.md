# Flip's Personal Website '21

Realized here: [particle.ucr.edu](https://particle.ucr.edu)

Flip Tanedo
June 2021 (Update 10 September; Updated 20 Aug 22)

See `Academic_README.md` for the README file for the Hugo Academic Resumé template. I periodically re-do my personal website from scratch using the latest Academic template.

Most of the material is copied from earlier websites. This `README.md` file is a personal reminder of how I edited the page. 

[2020 version](https://github.com/fliptanedo/flip-www-2020).



## Quick Edits

Notes: I'm not starting from scratch (Aug 22), but I notice that it has become harder and harder to start from scratch if one so wishes. The direct link to the GitHub repository with the basic Hugo academic theme is [here](https://github.com/wowchemy/starter-hugo-academic).

* Updating CV: place the new file in `./static/files/`
* Updating status: `./content/authors/admin/_index.md`
* **Updating research**
  * `researchslide.md`
  * Image goes in: `./assets/media/research/`
    * 1200x400 works
* Calendar: grab the code from the "share calendar" option on Google Calendar.



### New partial: Design

I was torn between using the premade **gallery** widget and the **projects** widget. 

* **Gallery**: compact, easy to fill. However, no room for discussion of the work. Usage is described [here](https://github.com/wowchemy/wowchemy-hugo-themes/issues/398). Doing this properly will take some time. Punt it for a future update. 
* **Projects**: perhaps overkill (tags, discussion, etc.).

I think the easiest thing for me would be to reuse my teaching widget. I copied the `./layouts/partials/widgets/teaching.html` to `...portfolio.html` and edited the image source folder. 

I am using the `.content/post/` folder for descriptions of each design. I may want to change this in the future.



### For Next Time

* I backed up some old sites in `./static/archived/`. These show up under `./archived/` when uploaded. I probably should link to them.

## Getting Started

### Download the Template

What was previous the Hugo Academic theme is now called [Wowchemy](https://wowchemy.com). The default method to build a page is to pick [a template](https://wowchemy.com/templates/) and deply through Netlify. This, in turn, will automatically link to GitHub to create a repository, which you can then fork with `git clone https://github...` where you fill in the appropriate URL for the GitHub repository.

### Run Hugo

Make sure you have Hugo e.g. through Homebrew. If it's been a while, you may want to update (up**grade**) hugo using `brew upgrade hugo` at the terminal. 

`hugo server -D` 

The output will include a URL: `Web Server is available at //localhost:1313/`, navigate your browser to this URL to view the page.

### If there's an error... 

I end up getting the following error: 

```
Error: failed to download modules: exec: "go": executable file not found in $PATH
```

This means we have to [install some Go dependences](https://wowchemy.com/docs/getting-started/install-hugo-extended/):

```
brew install git golang hugo
```

Then open `~/.zshrc` and add the following line

``` 
export PATH=$PATH:/usr/local/go/bin
```

You have to restart the Terminal app.

## What's New?

Since I last did this, the George Cushen's Academic theme has been renamed and expanded to Wowchemy. This new version has a content management server (CMS) that I find a bit cumbersome to navigate due to how I tend to bend the tempalte. The main references for modifying the template are here:

* https://wowchemy.com/docs/getting-started/customization/
* https://wowchemy.com/docs/getting-started/page-builder/

Hugo now uses modules, see [this discussion](https://zhauniarovich.com/post/2020/2020-09-hugo-modules/). 

## Transfer Assets from Previous Version

Wowchemy (Hugo Theme Academic) is a template. 

Hugo makes it easy to modify the template by searching for local template files ahead of the default template files. In theory, one can simply copy one of the default html template files and place the copy in the appropraite local directory to over-ride the default template.  Previously, the theme files were located in `.themes/academic`, now you can find them on the [wowchemy/wowchemy-hugo-modules](https://github.com/wowchemy/wowchemy-hugo-modules/tree/main/wowchemy) GitHub page. In principle, one should be able to place modified files in `./layouts/` relative to the root directory. *Unfortunately this doesn't quite work; more notes on this as we go.*

I suggest downloading that GitHub repository to make it easy to copy the html files. For more information, see: https://gohugo.io/getting-started/directory-structure/

All paths are relative to the project root. 

1. **Note: this didn't work for me (see below).** Create a `./layouts/` folder (or copy over the 2020 folder). Hugo will look here for templates and shortcodes first. This over-rides any files from the theme. Copy the contents of the 2020 webpage `./layouts/` folder. This should include three subfolders: 

   * `./layouts/partials/` templates for the home page.
   *  `./layouts/shortcodes/` these include a shortcode for twitter and a shortcode for e-mail hyperlinks that are robust against bots looking for e-mail addresses to spam.
   * `./layouts/_default/baseof.html` , the superstructure of the homepage, which we'll want to weak for the background and the footer.

   **Fix:** we'll have to ***make a local copy*** of the [wowchemy/wowchemy-hugo-modules](https://github.com/wowchemy/wowchemy-hugo-modules/tree/main/wowchemy) theme. Then go to `./go.mod` and add a line of the form:

   ```
   replace github.com/wowchemy/wowchemy-hugo-modules/wowchemy => /Users/flip/Documents/Website/wowchemy-hugo-modules-main/wowchemy
   ```

   See [Modifying modules.](https://gohugo.io/hugo-modules/use-modules/#make-and-test-changes-in-a-module) Then make the modifications directly to the local copy. You can skip this part for now; the other steps in this section modify meta-data rather than hacking the template. **Remark**: *it turns out that once I started using a local copy of wowchemy, Hugo started reading the local `./layouts` folder in my project directory.*

2. Copy the `./assets/scss` folder (containing `custom.css`) from the 2020 version. This includes:

   * "crypted email" to make it harder to skim email addresses
   * CSS styles for fonts
   * Google Calendar settings
   * CSS style adding a watermark
   * CSS style for a sidebar picture on the CV widget 
   * CSS style for footer
   * CSS style for the About Me section
   * CSS styles for various types of icon lists
   * CSS style hack for navigation bar opacity

3. Now set up the toml files for [custom fonts and color theme](https://wowchemy.com/docs/getting-started/customization/#custom-theme). The color theme is `./data/themes/fliptheme.toml`, the font theme is `.data/fonts/flipfont.toml`.

4. Now copy over the static files. Hugo still supports placing files and images in a `./static`  folder (e.g. see [this help page](https://discourse.gohugo.io/t/i-want-my-theme-to-use-images-as-backgrounds-i-know-how-to-use-css/27881/6)). See, e.g. this wowchemy [note on linking to files](https://wowchemy.com/docs/content/writing-markdown-latex/#link-to-a-file). Note, however, that [wowchemy looks](https://wowchemy.com/docs/content/page-features/#header-image) for images in `assets/media/`. For our purposes, let's start by copying over `./static`  from the old site and we can modify things as needed.

   * There's a bunch.
   * Move the research images to `assets/media/research` (not static; the research carousel will look here)

5. Favicon: this goes in `./assets/images` as a 512x512 image titled `icon.png`. If there is also a file names `logo.png` then this will be uesd in place of the site name on the menubar.

Check that the page compiles.

## Configuration 

Because there are significant structural changes in Hugo and Wowchemy/Academic

1. Let's start with `./config/_default/config.yaml`

   * Most of these are self-explanatory. Update the `title`, `baseurl`, and `copyright`. 

2. Go to `./config/_default/menus.yaml`; there's nothing to do here yet, but let's take a peek to see how it works. **Tip**: *edit this file as you write new sections in `content/home/`.* 

   * This sets the navigation of the homepage. 
   * Note that the list `menus.yaml` only controls the homepage menu items: name, link, and position on the navigation bar. It is independent of the weights in the `./content/home/...md`  widgets and their separate weights, which control the ordering of the sections on the page. 

3. Go to `./config/_default/params.yaml`

   * `theme: fliptheme`, assuming `./data/themes/fliptheme.toml`

   * `day_night: false` to turn off the day/night toggle

   * `font: 'flipfont'` , assuming `.data/fonts/flipfont.toml`

   * Copy the email fields from the previous `params.toml`. The `email1`,  `email2`, and  `email3` parameters are used by the cryptedemail css hack.

   * Turn off  `show_search` 

   * Set the `main_menu` alignment to `r`

   * Turn off `math` to enable the LaTeX markdown extension

   * At the bottom:

     ```
     ## ADDED BY FLIP
     # Feynman Diagram Footer
     footmark: 'layout/feynmanfooter.png'
     
     # Footer logos
     midlogo: 'logo/UCRPAlogo2.png'
     mylogo: 'logo/FlipAmbigram.png'
     
     # watermark on the about widget
     watermark: 'background/Bundle3.jpg'
     ## /FLIP
     ```

     

## Content

The `./content` folder contains subfolders for biographical data (`authors/admin`) and the homepage widgets `home/` . We won't use the other components. 

### authors/admin

Update `avatar.jpg` with your photo, update `_index.md`. This is where the `about` widget draws its information from.

In `content/authors/admin`:

- replace `avatar.jpg` with a profile photo
- Update the personal data in `_index.md`
  - We won't be using the `interests` or  `education` lists in `_index.md`
- Transfer over the long list of **social** icons. We'll eventually edit the template files so that they show up under the bio blurb, not the profile picture.

## Cleaning excess files

1. Delete `privacy.md` and `terms.md`; this may be something to explore in the future.

2. Delete the following folders in `./content/`: 

   * slides
   * publication
   * project
   * post
   * event

   In the future I may want to include these.

3. Delete (or set `active = false`) the following widgets (`.md` files) in `./content/home/`:

   * talks
   * tags
   * skills
   * publications
   * projects
   * posts
   * featured
   * experience
   * accomplishments
   * demo.md 

   So that's everything except `about.md`, `contact.md`, `index.md` . Note that there is no longer a `slider.md` default. It looks like [it's still available](https://wowchemy.com/docs/getting-started/page-builder/#slider), though.

We'll fill in the content later.

**Remark**: *at this stage, the site probably looks a bit sparse. It is a good check point to make sure everything is in place.*

## Background and Footer (hacking the template)

### Preliminaries

This is the annoying part. Make sure you have a local copy of the wowchemy theme; see the **transfering assets** section above. Go ahead and make sure that the following files are copied from the old site to the local copy of the wowchemy theme.

* `./layouts/partials/` templates for the home page.
*  `./layouts/shortcodes/` these include a shortcode for twitter and a shortcode for e-mail hyperlinks that are robust against bots looking for e-mail addresses to spam.
* `./layouts/_default/baseof.html`: keep the old version, we're going to modify it below. 

### Hack: I'm not sure how this works

**Remark**: *I'm very confused with how this is working or not working. What does work for me is to make sure that (1) there is a local copy of the wowchemy theme, (2) the `./go.mod` file in the project directory is pointing to that local copy using a `replace` command. Only then will hugo use the local `layouts` directory for templating.* I'm sure this is just a silly bug. 

**Reminder:** we'll have to ***make a local copy*** of the [wowchemy/wowchemy-hugo-modules](https://github.com/wowchemy/wowchemy-hugo-modules/tree/main/wowchemy) theme. Then go to `./go.mod` and add a line of the form:

```
replace github.com/wowchemy/wowchemy-hugo-modules/wowchemy => /Users/flip/Documents/Website/wowchemy-hugo-modules-main/wowchemy
```

See [Modifying modules.](https://gohugo.io/hugo-modules/use-modules/#make-and-test-changes-in-a-module) It seems like you do *not* have to modify the local copy of the template; you can place the modified files in `./layouts`. 

### baseof.html

There are two major design edits here. They're a bit of a pain to implement, but that's my hubris for you. Note: the copy of `./layouts/_default/baseof.html` that we put in here is now outdated. Let's start by placing the most updated version, which we will shortly edit.  

Make sure you have included `/layouts/_default/baseof.html` from the previous site. 

Here's what `baseof.html` looks like (you can grab this from the wowchemy template files on GitHub) after I modified it.  **Remark**: *make sure any updated layout files are modified from the latest template, not just copies of the previous version.*

```html
<!DOCTYPE html>
<!-- TEST -->
{{- $language_code := site.LanguageCode | default "en-us" -}}
<html lang="{{$language_code}}" {{ if in site.Data.i18n.rtl.rtl $language_code }}dir="rtl"{{end}}>

{{ partial "site_head" . }}

{{ $show_navbar := site.Params.main_menu.enable | default true }}
{{- $highlight_active_link := site.Params.main_menu.highlight_active_link | default true -}}
<body id="top" data-spy="scroll" {{ if $show_navbar }}data-offset="70"{{end}} data-target="{{ if or .IsHome (eq .Type "widget_page") | and $highlight_active_link }}#navbar-main{{else}}#TableOfContents{{end}}" class="page-wrapper {{with .Params.design.css_class}}{{.}}{{end}} {{ if not (.Scratch.Get "light") }}dark{{end}} {{ if not $show_navbar }}no-navbar{{end}}" {{with .File}}data-wc-page-id="{{.File.UniqueID}}"{{end}} {{with .Params.design.css_style}}style="{{. | safeCSS}}"{{end}}>

  {{/* Initialise Wowchemy. */}}
  {{ $js_license := printf "/*! Wowchemy v%s | https://wowchemy.com/ */\n" site.Data.wowchemy.version }}
  {{ $js_license := $js_license | printf "%s/*! Copyright 2016-present George Cushen (https://georgecushen.com/) */\n" }}
  {{ $js_license := $js_license | printf "%s/*! License: https://github.com/wowchemy/wowchemy-hugo-modules/blob/main/LICENSE.md */\n" }}
  {{ $js_bundle_head := $js_license | resources.FromString "js/bundle-head.js" }}
  {{ $wcDarkLightEnabled := site.Params.day_night | default false }}
  {{ $wcIsSiteThemeDark := not (.Scratch.Get "light") | default false }}
  {{ $js_params := dict "wcDarkLightEnabled" $wcDarkLightEnabled "wcIsSiteThemeDark" $wcIsSiteThemeDark }}
  {{ $js_bundle := resources.Get "js/wowchemy-init.js" | js.Build (dict "params" $js_params) }}
  {{- if hugo.IsProduction -}}
    {{- $js_bundle = $js_bundle | js.Build (dict "format" "iife") | minify -}}
  {{- else -}}
    {{- $js_bundle = $js_bundle | js.Build (dict "format" "iife" "sourceMap" "inline") -}}
  {{ end }}
  {{ $js_bundle := slice $js_bundle_head $js_bundle | resources.Concat "js/wowchemy-init.min.js" }}
  {{- if hugo.IsProduction -}}
    {{ $js_bundle = $js_bundle | fingerprint "md5" }}
  {{- end -}}
  <script src="{{ $js_bundle.RelPermalink }}"></script>

  {{ partial "search" . }}

<!-- FLIP: FOR WATERMARK -->
<div id="watermark" style="background-image:url('{{ $.Site.BaseURL }}/img/{{ .Site.Params.watermark }}');"></div>
<!-- /FLIP --> 

  <div class="page-header">
    {{ partial "navbar" . }}
  </div>

<!-- FLIP 2019 -->
<div id="THECONTENT"> <!-- closed below; see flip2019.css -->
<!-- /FLIP 2019 -->

  <div class="page-body">
    {{ block "main" . }}{{ end }}
  </div>

  <div class="page-footer">
    {{/* Docs and Updates layouts include the site footer in a different location. */}}
    {{ if not (in (slice "book" "docs" "updates") .Type) }}
    <!-- FLIP -->
    <div style="position: relative; width: 0; height: 0">
    <div id="feynmanfoot" style="background-image:url('{{ $.Site.BaseURL }}/img/{{ .Site.Params.footmark }}');"></div>
    </div>
    <div id="botbar1"></div>
    <!-- -- -->
    <div id="FOOTERBAR">
    <!-- /FLIP -->
    <div class="container">
      {{ partial "site_footer" . }}
    </div>
    <!-- FLIP -->
    </div> <!-- closes div FOOTERBAR -->
    <!-- /FLIP -->
    {{ end }}
  </div>

<!-- FLIP -->
</div> <!-- closes id="THECONTENT" -->
<!-- /FLIP -->

  {{ partial "citation" . }}

  {{ partial "site_js" . }}

</body>
</html>
```

My edits are highlighted with comments.

We can see where the navigation bar is called and where the footer is called. The stuff in between calls the sections of the home page. Here's what we want to do:

1. **We want the background of the `<body>` to be dark gray.** Aesthetically we want the background to be white. However, the navigation bar and footer will be dark gray. What this means is that if one over-scrolls (pulls above or below the main page by a little) then you get a bit of white pulling from under the footer or from above the navigation bar. This looks distracting, so we're going to jump through some hoops. This involves:

   a) setting the `<body>` background to be dark gray. If you've copied over the style files, this should already be active.

   b) creating a new `<div id="THECONTENT">` that has a white background. All of the sections will be inside this division. Over scrolling, however, will pull more space from *outside* this division, which will be dark gray.

2. **We want the fancy footer**. I have a neat Feynman diagram footer graphic that I like.  Observe that the `<div class="container">` that encloses the footer does not spread across the entire navigator width.  The `container` class is something inherited from Bootstrap, the responsive design grid system that *Academic* is built upon.

   We have to place additional `<div>`s just around and above the footer. 

Bonus: at this stage you can also put in the `baseof.html` code for a watermark.

In earlier steps we defined the locations of the graphics in `params.yaml`

```toml
## ADDED BY FLIP
# Feynman Diagram Footer
footmark: 'layout/feynmanfooter.png'

# Footer logos
midlogo: 'logo/UCRPAlogo2.png'
mylogo: 'logo/FlipAmbigram.png'

# watermark on the about widget
watermark: 'background/Bundle3.jpg'
## /FLIP
```

This is a good checkpoint: the website should look reasonable at this stage.

### navbar.html partial

We have this copied over from last time, but a better thing to do is to update it with the latest wowchemy template. 

The **breakpoint** of a navigation bar is the window width at which the bar collapses into the familiar "three horizontal bars" symbol for an expanding menu. Bootstrap 4 makes this easy. [Here's how it works](https://stackoverflow.com/a/36289507/4812646):

> Changing the navbar breakpoint is easier in Bootstrap 4 using the navbar-expand-* classes:

```html
<nav class="navbar fixed-top navbar-expand-sm">..</nav>
```

The options are

- `navbar-expand-sm`: mobile menu on xs screens <576px
- `navbar-expand-md`: mobile menu on sm screens <768px
- `navbar-expand-lg`: mobile menu on md screens <992px
- `navbar-expand-xl`: mobile menu on lg screens <1200px
- `navbar-expand`: never use mobile menu
- *(no expand class)* = always use mobile menu

The relevant line shows up at the top of `themes/academic/layouts/partials/navbar.html`. You know what that means: make a copy of that file in `/layouts/partials/` and change 

```html
<nav class="navbar navbar-light fixed-top navbar-expand-lg py-0 compensate-for-scrollbar" id="navbar-main">
```

to

```html
<nav class="navbar navbar-light fixed-top navbar-expand-md py-0 compensate-for-scrollbar" id="navbar-main">
```

You can use `navbar-expand-sm` if your menu is particularly brief. 

By the way, this is also *way* easier than it used to be in Bootstrap 3, remember to be grateful.

### 3 column footer

We have also copied over `themes/academic/layouts/partials/site_footer.html`. It's worth updating the base file to match the wowchemy template and then inserting the new text.

Here's my modification:

```html
<footer class="site-footer">
<!-- FLIP: commented out all the old stuff -->
<!-- 
  {{ if .IsTranslated | and site.Params.footer.show_translations }}
    <div class="powered-by d-flex flex-wrap pb-2 justify-content-center">
      <div class="p-2 font-weight-bold"><i class="fas fa-globe pr-1" aria-hidden="true"></i>{{ i18n "languages" }}:</div>
      <div class="p-2">{{ index site.Data.i18n.languages .Lang }}</div>
      {{ range .Translations }}
        <div class="p-2"><a href="{{ .Permalink }}">{{ index site.Data.i18n.languages .Lang }}</a></div>
      {{ end }}
    </div>
  {{ end }}

  {{ if or (site.GetPage "terms.md") (site.GetPage "privacy.md") }}
  <p class="powered-by">
    {{ with site.GetPage "privacy.md" }}
      {{ printf "<a href=\"%s\">%s</a>" .RelPermalink .Title | safeHTML }}
    {{ end }}
    {{ with site.GetPage "terms.md" }}
      {{ if site.GetPage "privacy.md" }} &middot; {{ end }}
      {{ printf "<a href=\"%s\">%s</a>" .RelPermalink .Title | safeHTML }}
    {{ end }}
  </p>
  {{ end }}

  {{ with site.Copyright }}
  <p class="powered-by">
    {{ replace . "{year}" now.Year | markdownify }}
  </p>
  {{ end }}

  {{/* Display copyright license. */}}
  {{ partial "site_footer_license" . }}

  <p class="powered-by">
    {{ $is_sponsor := site.Params.i_am_a_sponsor | default false }}
    {{ $hide_published_with_footer := site.Params.power_ups.hide_published_with | default true }}
    {{ if not (and $is_sponsor $hide_published_with_footer) }}
      {{ $default := "Published with {wowchemy} — the free, {repo_link}open source{/repo_link} website builder that empowers creators." }}
      {{ $i18n_published_with := i18n "published_with" | default $default }}
      {{ if not (findRE "{wowchemy}" $i18n_published_with) }}
        {{ warnf "Please attribute Wowchemy using `{wowchemy}` in the `published_with` text." }}
        {{ $i18n_published_with = $default }}
      {{ end }}
      {{ $i18n_published_with = replace $i18n_published_with "{wowchemy}" "<a href=\"https://wowchemy.com/?utm_campaign=poweredby\" target=\"_blank\" rel=\"noopener\">Wowchemy</a>" | safeHTML }}
      {{ $i18n_published_with = replace $i18n_published_with "{repo_link}" "<a href=\"https://github.com/wowchemy/wowchemy-hugo-modules\" target=\"_blank\" rel=\"noopener\">" | safeHTML }}
      {{ $i18n_published_with = replace $i18n_published_with "{/repo_link}" "</a>" | safeHTML }}
      {{ $i18n_published_with | markdownify | emojify }}
    {{ end }}
  </p> -->
  <!-- FLIP: new -->
<div class="row" id="footer-columns">
  <div class="col-md-4" id="footer-col-1">
    <img src="{{ $.Site.BaseURL }}img/{{ $.Site.Params.mylogo }}" class="center-me">
  </div>
  <div class="col-md-4" id="footer-col-1">
    <img src="{{ $.Site.BaseURL }}img/{{ $.Site.Params.midlogo }}" class="center-me">
  </div>
  <div class="col-md-4" id="footer-col-1">
    <p class="powered-by">
    {{ with site.Copyright }}{{ replace . "{year}" now.Year | markdownify}} &middot; {{ end }}

    Published with G. Cushen's
    <a href="https://github.com/wowchemy/wowchemy-hugo-modules" target="_blank" rel="noopener">wowchemy</a> for
    <a href="https://gohugo.io" target="_blank" rel="noopener">Hugo</a>.

    {{ if ne .Type "docs" }}
    <span class="float-right" aria-hidden="true">
      <a href="#" id="back_to_top">
        <span class="button_icon">
          <i class="fas fa-chevron-up fa-2x"></i>
        </span>
      </a>
    </span>
    {{ end }}
  </p>
  </div>
</div>
<!-- /FLIP -->
</footer>

```

### "About Widget" Watermark

**Note**: there's a new way to do this [within wowchemy]((https://wowchemy.com/docs/getting-started/page-builder/#background)), I may want to change to that instead in the future. For now we'll use the old method

One fancy thing to add in is a watermark. If you copied the watermark code in `baseof.html` and `params.toml` (as well as the relevant parts of `custom.css`, it should already be up and running. 

In `baseof.html`: the code:

```html
<!-- FLIP: FOR WATERMARK -->
<div id="watermark" style="background-image:url('{{ $.Site.BaseURL }}/img/{{ .Site.Params.watermark }}');"></div>
<!-- /FLIP -->	
  {{ partial "navbar.html" . }}
```

Note that I've tried to annotate my edits compared to the default file. This is helpful since the next time I make edits, the default file may have been upgraded and I need to remember where to put hacks.

## Content

Now we move on to filling out the widgets on the homepage. We've copied over the widget layouts from the previous version. However, these are modified on an old version of the theme. We want to copy the current theme widgets and apply the hacks from the previous version to make sure the widgets are compatible.

All of the following are in  `layouts/partials/widgets/`. I assume that you are starting from a clean version from the latest version of the theme. By marking all replacements and removals with comments (e.g. `<!-- FLIP -->`), it's easy to find where to insert new code in the clean version. In this file I'll just write a few general comments, you can refer to the previous files in `./layouts/partials/widgets`.

### about.html

* Comment out icon list, move it below. 
* Add a `{{ $page.Content }}` portion. Note that this is different from `{{ $person_page.Content }}`. The latter is filled in from `_index.md` in the `./config` folder. The former is used for the small comment. 
* Removed the interests/education; we'll put that in the CV
* Go ahead and edit `.content/home/about.md`

### CV

The next item on the website should be a mini-CV with links to a full CV. Copy the latest version of `/layouts/partials/widgets/blank.html` to the project directory, `./layouts/partials/widgets/blank.html` . Make another copy in the project directory rename it to `CV.html`. 

Actually, I think the CV widget is fine as is. I just copied from the previous version. Go ahead and copy `.content/home/CV.md` from the previous version.

Comments:

* Note also the minor tweak of `<h1>` to `<h2>` in the following line:

  ```html
  {{ with $st.Title }}<h2>{{ . | markdownify | emojify }}</h2>{{ end }}
  ```

  This is so that "Curriculum Vitae" fits on one line on large screens. 

* ##### Add a "download pdf" button

  In `CV.html` under `<div class="col-xs-12 col-md-4 section-heading">`:

  ```html
      <p>
      <a class="btn btn-outline-primary btn-xs" href="{{ $st.Params.cv_pdf }}">
        Download Complete CV
      </a>
      </p>
  ```

* In the header of `CV.md`:

  ```md
  # CV location
  cv_pdf = "./files/Tanedo.pdf"
  ```

  Note that this has to go between the `+++` in the header section, and above any list parameters (Defined with brackets: `[list]`). 

### Slider (Research Carousel)

I'm not sure what's going on here. The main reference is here: https://wowchemy.com/docs/getting-started/page-builder/#slider

* The png images with transparencies are not darkened. 

* Images aren't being rescaled. [Bug report from someone else](https://github.com/wowchemy/wowchemy-hugo-modules/issues/2158).

* Hack: based on [slider.html template](https://github.com/wowchemy/wowchemy-hugo-modules/blob/main/wowchemy/layouts/partials/widgets/slider.html)

  * Looks like I want to modify class `carousel-inner`

  * Suggestion is `ground-position:center; background-repeat: no-repeat; background-size: cover;` via [this thread](https://github.com/wowchemy/wowchemy-hugo-modules/issues/2158#issuecomment-803296060)

  * Propose: put this in `custom.css`

    ```
    .carousel-inner {
      ground-position:center; 
      background-repeat: no-repeat; 
      background-size: cover;
    }
    ```

  * Alternative that works in the markdown for `slider.md`: 

    ```
    height = "400px; background-position:center; background-repeat: no-repeat; background-size: cover"
    ```

    This works because the height is inserted right where the image is called.

  * Tried again: using the default template from wowchemy. Seems to work ok.  New problem: the dimmer will dim the entire carousel, not just the image. Problem is in the `slider.html` where a typical element looks like

    ```
    <div class="wg-hero dark carousel-item active" style=" height: 300px; background-color: #666;background-image: url(&#39;http://localhost:1313/flip/media/bubbles.jpg&#39;);filter: brightness(0.5);">
        <div class="container" style="text-align: center;">
            <h1 class="hero-title">
              Hello
            </h1>
    
            
            <p class="hero-lead" style="margin: 0 auto 0 auto;">
              I am center aligned 😄
            </p>
            
    
            <p>
              <a href="https://example.org" class="btn btn-light btn-lg"><i class="fas fa-graduation-cap" style="padding-right: 10px;"></i>Download my app</a>
            </p>
            
          </div>
      </div>
      
    ```

    The `filter:brightness(0.5)` is affecting the sub-divs. The issue is discussed [here](https://stackoverflow.com/a/21363446). Looks like no good solution. Better to just dim images by hand. 

### Teaching Widget

* Leaving this as-is for now. Note that we're still using TOML format, where most of the current files in the template use YAML.

### Team Widget

 In the future, it may be better to make a separate style for *only* this widget, which seems to be something allowed. (I'm not sure where to put the css file, though.)

### Twitter

This uses the blank widget with a twitter **shortcode** (Hugo's way of inserting bits of html). I had to adapt this since last year due to some updates on how Hugo does short codes. 

Should probably move press items to a separate file.

### Contact

We can hack the `contact.html` template to include a Google Calendar widget. Insert the following code: below `<div class="col-12 {{if eq $columns "2"}}col-lg-8{{end}}">`:

```
<div class="col-12 {{if eq $columns "2"}}col-lg-8{{end}}">
  {{ with $st.Content }}{{ . }}{{ end }}

<!-- FLIP 2019 -->
    {{ with $page.Params.calendar }}
      <iframe src="https://calendar.google.com/calendar/embed?height=200&amp;wkst=1&amp;bgcolor=%23ffffff&amp;ctz=America%2FLos_Angeles&amp;{{ range $index, $item := $page.Params.calendar }}src={{ with $item.src }}{{ . }}{{ end }}&amp;{{ end }}color=%23C0CA33&amp;color=%23F4511E&amp;color=%237986CB&amp;color=%23F6BF26&amp;mode=AGENDA&amp;showNav=0&amp;showPrint=0&amp;showTabs=0&amp;showCalendars=0&amp;showTitle=0" style="border:solid 1px #777" width="98%" height="200" frameborder="0" scrolling="no"></iframe>
    {{ end }}
    <!-- /FLIP 2019 -->
```

Next comment out the old email line. We want to replace it with the "crypted email" code which hides the full email address from the final html file. This is a super low-level way of making it harder to skim your email address. I think this was effective in the mid 2000s, and probably completely irrelevant today. Still, I've been using this on my personal website for over a decade, so I might as well keep up the tradition.

```
<!-- FLIP: comment out -->
    <!-- {{ if $data.email }}
    <li>
      <i class="fa-li fas fa-envelope fa-2x" aria-hidden="true"></i>
      <span id="person-email">
      {{- if $autolink }}<a href="mailto:{{ $data.email }}">{{ $data.email }}</a>{{ else }}{{ $data.email }}{{ end -}}
      </span>
    </li>
    {{ end }} -->
<!-- /FLIP -->
```

Replace it with:

```
<!-- FLIP 2019 -->
      <!-- from: https://stackoverflow.com/a/41566570 -->
      {{ with $.Site.Params.email1 }}
        <li>
          <i class="fa-li fas fa-envelope fa-2x" aria-hidden="true"></i>
          <span id="person-email" itemprop="email">
            <a data-name="{{ $.Site.Params.email1 }}" data-domain="{{ $.Site.Params.email2 }}" data-tld="{{ $.Site.Params.email3 }}" href="#" class="cryptedmail" onclick="window.location.href = 'mailto:' + this.dataset.name + '@' + this.dataset.domain + '.' + this.dataset.tld"></a>
          </span>
        </li>
      {{ end }}
<!-- /FLIP 2019 -->
```



## Other tweaks

### Headings

There was an issue with section headings on small screens. Section headings from widget layouts that I ported from the last version are all left-aligned on small screens. On the other hand, when the 2021 default wowchemy blank layout is used, they are center aligned on small screens.  

Issue seems to be in `widget_page.html` which calls the widgets: line 110

```
{{ $use_cols := in (slice "pages" "featured" "experience" "accomplishments" "contact" "blank" "tag_cloud" "portfolio") $widget }}
```

Has to do with whether or not you are using a custom layout or blank.html. This is called here:

```
{{if $use_cols}}
      <div class="row  {{if not $st.Title | or (eq $columns "1") }}justify-content-center{{end}}">
      {{ if $st.Title }}
        {{ if eq $columns "1" }}
          <div class="section-heading col-12 mb-3 text-center">
            {{ with $st.Title }}<h1 class="mb-0">{{ . | markdownify | emojify }}</h1>{{ end }}
            {{ with $st.Params.subtitle }}<p class="mt-1">{{ . | markdownify | emojify }}</p>{{ end }}
          </div>
        {{else}}
          <div class="section-heading col-12 col-lg-4 mb-3 mb-lg-0 d-flex flex-column align-items-center align-items-lg-start">
            {{ with $st.Title }}<h1 class="mb-0">{{ . | markdownify | emojify }}</h1>{{ end }}
            {{ with $st.Params.subtitle }}<p class="mt-1">{{ . | markdownify | emojify }}</p>{{ end }}
          </div>
        {{end}}
      {{end}}
    {{end}}
```



My solution: modify templates, but also modify `widget_page.html` line 110 to include my custom widget layouts:

```
  {{ $use_cols := in (slice "pages" "featured" "experience" "accomplishments" "contact" "blank" "tag_cloud" "portfolio" "teaching") $widget }}
```



Corresponding change to `teaching.html`:

```
{{ $st := .page }}
{{ $columns := $st.Params.design.columns | default "2" }}


{{ if ne $columns "1" }}
  <div class="col-12 col-lg-8">
    {{ $st.Content }}
    <div class="row">
    {{ with $st.Params.teaching }}
          {{ range .class }}
            <div class="col-3 teaching">
             <a href="{{ .website }}"><img class="teachingpic" src="{{ $.Site.BaseURL }}img/teaching/{{ .photo }}"></a>
             <a href="{{ .website }}">{{ .number }}, {{ .session }}</a> <br />
             <span class="smaller">{{ .name }}</span>
            </div>
         {{ end }}
        {{ end }}
    </div>
  </div>
{{ else }}
{{ end }}

```



Have to do this for each custom 2-column widget.

## Adding a separate page

I like to have some one-off pages that are not directly linked in the menu bar. For example, a page for letter of recommendation instructions for undergraduates. 

### New Method: set these up as "blog" posts

Rather than having one-off pages "on an island," I might as well use the `./content/post` folder for these. Each post has a subfolder.

Problem: for some screen sizes, the menu bar overlaps the page title.![Screen Shot 2021-09-10 at 4.02.16 PM](/Users/flip/Documents/Website/tanedo-website-2021/README.assets/Screen Shot 2021-09-10 at 4.02.16 PM.png)

### Old Method: doesn't work anymore

To do this, add a new folder `./content/recs/` with a markdown file `./content/recs/_index.md`

I used the sample site's `.content/post/_inxed.md` as a template. 

```
---
title: Letters of Rec

# View.
#   1 = List
#   2 = Compact
#   3 = Card
view: 2

# Optional header image (relative to `static/img/` folder).
header:
  caption: ""
  image: ""
---
Here are some instructions if you would like to ask me for a **letter of recommendation**. Key guidelines:
```

*Hmm! This doesn't seem to work!*

## Deploying

Note: UCR now uses 2-factor authentication. In order to ssh/sftp into the server, one needs to connect with a VPN in order to open up the port.

## Cheat Sheets

* [Emoji in Hugo](https://www.webfx.com/tools/emoji-cheat-sheet/)
* See 2020 Readme for some previous design notes.
* https://isabella-b.com/blog/hugo-academic-customization/



## Work in progress for next time

* There are some problems with intermediate screen sizes: the titl eof the page gets cut off by the menu bar and the bottom of the page has excess whitespace. 

![Screen Shot 2021-09-10 at 4.08.30 PM](/Users/flip/Documents/Website/tanedo-website-2021/README.assets/Screen Shot 2021-09-10 at 4.08.30 PM.png)

* Note that GitHub now requires [Personal Access Tokens]((https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)). Be sure to test this out.
