# Editing this Site
This site is built using Jekyll and Liquid, which rely on Ruby, JavaScript, HTML, and CSS. Despite the veritable soup that makes up the code, the site is relatively easy to edit if you know what you're looking for. For most issues, please see the CollectionBuilder documentation. However, since I've added some includes, it's best to explain things here as well.

Note that in adding UI elements to the site, I've tried my best to stay within the Jekyll and Liquid framework CollectionBuilder already uses, so that it's easy to edit things from the non-dev side. If you would like to make changes, please feel free; a local copy is stored as a backup in case any breaking changes occur.

## Site Components
The following components make up the core of what you will be editing on the site:
* config.yml file (not in a folder)
* template.yml file (in the _data folder)
* pages (.md files in the pages folder)
* objects (.jpg files in the objects folder)
* your metadata file (in the _data folder)
* config files (.csv files in the _data folder)

You may also want to browse the _includes folder to see what plug-and-play features are available to be added to pages on your site. We'll talk about what includes do later.

## Syntax: Front Matter
There are several things to note about syntax before you start editing, mainly that Jekyll relies on configuration files in YAML to manage the way the site is put together on a broad level. Think of the YAML as a set of instructions that tell Jekyll how and what to load from different files within your larger site folder. These files include the config.yml file, the theme.yml file, and the YAML front matter, or code at the top of the file, at the top of each page in the pages folder and some layouts in the layouts folder.

You won't actually need to change any of the underlying structure of the YAML in the config.yml and template.yml files, so feel free to edity those according to the green comments without fear! But you'll need to add YAML front matter at the top of each page you create. As such, it's important to know how it works.

### Editing YAML on a page
Let's take the about page (about.md) in the pages folder as an example. If you open the file, you'll see that there are three dashes --- at the top of the page, followed by a bunch of information, and then three dashes at the end. **Thess three dashes distinguish the YAML front matter from the rest of the code**. Everything inside of the pair of three dashes is the YAML front matter. You'll see that this front matter includes fields, like title, layour, permalink, credits, etc., followed by a colon : and a value (About, about, /about.html, true, etc.). This front matter lets you set perameters for which layout you want the page to use, what title you want the page to display, and what you want the link to that page to be on the site. You can also set other perameters, such as what featured image from your collection objects you want to appear on the page, and whether you want a heading to appear at the top of the page. The most important fields here, however, are **layout** and **permalink**.

#### Layouts
Layouts are pre-built HTML templates that you can call onto your page to arrange your content. They are stored in the _layouts folder. You'll see that most layouts include a section {{ content }}. This is where any text or images you enter in the page markdown file will load within the template. For example, in the about.html template, the {{ content }} section is located before the credits, and after a bunch of other code. When you add the about template to the about.md page in the pages folder, it will load everything in the about.html template before the {{ content }} section, then load anything you typed in the about.md page in the {{ content }} section, and then load the credits. If I put "Kiran is cool" into the about.md file, and have the layout in the about.md file set to "about," the About page will display everything in the about.html file, then replace {{ content }} with "Kiran is cool," and then display the credits.

Layouts are great because they allow you to reuse different fixed content and arrangements across pages without having to reduplicate your code. You'll notice that the majority of pages on the site use the basic page layout, which loads the header, footer, nav bar, and other static features.

#### Includes
One of the other things you will probably see within a layout file are includes, indicated by this snippet of code: {% include FOLDER/FILENAME %}. Includes are packages of JavaScript and HTML that can be slotted into pages and layouts to create cool features that can be resued across the site whenever you want. For example, there's an include called "card-gallery" that I created, which includes a bunch of HTML to create a gallery of cards that each have a little label and a photo. To add that to a page, I would simply type "{% include card-gallery %}" in the space on my page where I want the card gallery to appear. If I wanted to add a word cloud of all of the subjects represented in my data, I would go into the js subfolder and find the include name: cloud-js.html. I would then find the space on my page where I want to add the include and add the following code: {% include js/cloud-js.html %}. Simple as that.

#### Front Matter as Data
One of the other reasons why front matter is so important is because it serves as data for your includes to use to automatically decide what information to populate on the page. The cloud layout is a great example of this: it checks whether you have a field in your YAML front matter "cloud-fields" and checks the value of that field to decide what information to collect from your metadata spreadsheet. If you set cloud-fields to "subjects," for example, it will show all of your subjects. If you set it to "location," it will instead pull all of the values from the location field of your metadata spreadsheet. You can see this in action if you open the cloud.html layout and the subjects.md page.

## Configuring Big Things: Configs, Config.yml, and Template.yml
You have two major points of configuration for the site's functions: config.yml, which is a file not in any folder; and the config files located in the _data folder. The config files in the _data folder are simple tables that let you change what fields are shown on various pages. This will be where you edit what appears on the navbar, the browse page under each object, the map settings, and what the search bar includes and is labelled as.

### Utility Setup: Config.yml
The config.yml file controls large-scale things like your site's title (which appears on the tab label in your browser), a tagline, description, and keywords for search engines, **which metadata file you want to use**, and other settings that won't affect how the site looks, but will affect how it functions overall on the web.

### Aesthetics Setup: Config.yml
The theme.yml file controls how things appear on different pages, such as the featured image that shows up on in the banner on the home page, whether you want advanced and faceted search on the browse page, larger map settings like zoom level, increments for the timeline, compound object settings, the navbar color, the fonts available for use on the site, and more aesthetic choices that will affect the whole site or a whole set of pages on a general level.

## Things You Should Ask a Dev to Do
I encourage you to experiment with code, but just in case you're anxious about breaking things, here is a list of things you should probably ask a dev to do:
* Edit styles that aren't available in the template.yml file.
* Edit any of the JavaScript or HTML for _includes or _layouts.
* Add includes or features that you'd like to reuse across the site.
* Anything else you can think of that's not covered by the CB documentation.

| Element      | File to Edit |
| ----------- | ----------- |
| Aesthetics      | _data/template.yml       |
| Pages & content   | files in pages folder        |
| Metadata settings | config.yml |
| Colors | _data/config-theme-colors.csv |
| Search settings | _data/config-search.csv AND config.yml |
| Navbar | _data/config-nav.csv |
| Map settings | config-map.csv |