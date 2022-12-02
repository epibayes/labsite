# Epibayes Lab
*built with Hugo Wowchemy, on the [Research Group Template](https://github.com/wowchemy/starter-hugo-research-group)*
- - - -
## WORKFLOW
Built with Hugo, so please take a look at [Hugo documentation](HUGOREADME.md)
### Downloading and Running:
- `git clone` this repo and follow the instructions in the [Wowchemy Hugo documentation for starting up the server](https://wowchemy.com/docs/getting-started/install-hugo-extended/)
- You can run a local version by using `hugo server` and opening `localhost:1313` on your internet browser of choice.
  - Make sure you have `hugo` installed to do this!!
### Pushing Changes:
- **DO NOT PUSH TO MASTER BRANCH DIRECTLY!**
- Push changes that ***won't break the site*** to the development branch
    - Make sure you're checked out onto the DEVELOPMENT branch: `git checkout development`
- For any potentially breaking changes, create a NEW branch: `git checkout -b <name of new branch>`
    - Send pull requests (PRs) to development
- **ONLY** development should ever be PR merged into master. Other branches should **ALWAYS** PR merge into development.
### Hugo Updates:
- Follow the update instructions in the [Wowchemy Hugo documentation for updating Hugo](https://wowchemy.com/docs/hugo-tutorials/update/)
### Web Deploy Details:
- Hugo sites are hosted by default on [Netlify](https://www.netlify.com/)
  - This site is currently associated with Stephanie's github account
  - There are two active deploys: one for the [development branch](https://labdev.netlify.app/) and one for the [master branch](https://epibayes.io/)
- - - -
## REPO CONTENTS
Only listing files **that have been interacted with**. Compare with the repo at [starter-hugo-research-group](https://github.com/wowchemy/starter-hugo-research-group).
### CONFIGURATION (config)
- `menu.yaml` - used to update what order each of the sections appears in the navigation bar
  - higher weight pushes content further rightwards
- `config.yaml` - *only title and baseURL were updated*
- `params.yaml` - *SEO was updated, footer was updated*
### CONTENT
Also reference [Wowchemy's widget documentation](https://wowchemy.com/docs/widget/) for more options and details.
#### The `authors/` folder holds each lab member's profile in its own folder
- `<first name> - <last name>/` - the folder (MINUS `admin/` folder) follows the same naming scheme of first name hyphen last name.
- `_index.md` - the profile itself.
  - **IMPORTANT LINES:**
    - The line for `user_groups` (approximately between lines 60 and 70) is used to determine if the lab member is a regular member, Jon (principal investigator), or former member. This will change under which category the lab member shows up in on the main lab page. 
    - Nov. 2022 EDIT: Former Member category has been removed from view, but people can still access former lab members' profiles by navigating to `/author/firstname-lastname`
      - Former members can keep their folders in the `authors/` directory but **should not** receive a corresponding file in the `people/` folder.
- `avatar.png` - the headshot
#### The `careers/` folder holds potential open positions at the Epibayes Lab
- `_index.md` - tells Hugo what kind of page it is (it's a "page"-type page).
- The `postdoc/` folder has the actual content for the careers page. Each non- `_index.md` markdown file in this folder will be a different career posting. Currently, there's an example, `postdoc.md`.
  - `_index.md` - this file determines what shows up when navigating to the careers page.
    - **Lines 12 - 14** (`## Work with the Epibayes Research Group`) should be removed or changed if an active posting needs to be added.
  - `postdoc.md` - This is the posting for a postdoc position.
    - **Line 6** (`draft: true`) prevents this page from showing up! Any inactive listings can be "turned off/hidden" by switching `draft: false` to `draft: true`.
    - **Lines 7 - 10** (`menu:`) show how the menu is structured: `All-Remote Post-Doctoral Fellow` is a menu item in `Open Positions`, which is a menu item under `Careers`.
    - **Use Headings!** These will auto-generate a table of contents.
#### The `contact/` folder has two files that determine how the contacts page shows up
- `index.md` -  tells Hugo what kind of page it is (it's a widget-type page).
- `contact.md` - has the details for the contact widget. Update lines under line 15 (the "content" line) to udpate information.
#### The `home/` folder has the different content that shows up directly on the home page
- `grants.md` - the different grants/funding Epibayes Lab is supported by
  - **Images** are located under `static/img/`.
  - **Line 8** (`weight: 20`) determines how "high up" on the home page this section shows up (currently is the second element).
- `image.md` - *switched active from `true` to `false`, left here for reference just in case the widget needs to be used*
- `index.md` - tells Hugo what kind of page it is (it's a widget-type page, specifically a `headless` one because it's used to make the home page)
- `people.md` - creates the "Meet the Team" section using the profiles in the `authors/` folder
  - **Line 4** (`weight: 60`) determines how "high up" on the home page this section shows up (currently is the sixth element).
  - **Lines 11 - 14** (`user_groups:`) show which user groups are going to show up, so make sure to tag each person in the `authors/` folder with the correct user group.
  - **Lines 15 - 23** (`design:`) ask which details should show up for each person. Currently, most of these options are turned to `false` because not everyone in the lab has provided these details.
- `posts.md` - shows recent posts; posts here refer to the blog posts that are in the `post/` folder
  - **Line 5** (`weight: 50`) determines how "high up" on the home page this section shows up (currently is the fifth element).
  - **Line 11** (`count: 3`) determines the number of posts that appear on the home page. Currently, 3 posts show up.
  - **Line 20** (`page_type: post`) determines the type of content that will show up (`post/` folder content).
  - **Line 22** (`view: 3`) can be adjusted to be one of the following:
    - 1 = List
    - 2 = Compact
    - 3 = Card (*the current setting*)
    - 4 = Citation (publication only)
- `publications.md` - shows a couple of recent publications; publications are found in the `publication/` folder
  - **Line 5** (`weight: 30`) determines how "high up" on the home page this section shows up (currently is the third element).
  - **Line 11** (`count: 3`) determines the number of publications that appear on the home page. Currently, 3 posts show up.
  - **Line 20** (`page_type: publication`) determines the type of content that will show up (`publication/` folder content).
  - **Line 22** (`view: 2`) can be adjusted to be one of the following:
    - 1 = List
    - 2 = Compact (*the current setting*)
    - 3 = Card
    - 4 = Citation (publication only)
- `recent_news.md` - shows a brief preview of recent news and media appearances from our lab members
  - This page (as well as `news.md`, `newslist.dat`, and `readfromfile.html`) directly borrow the news section [code and structure created by user apetros](https://github.com/wowchemy/wowchemy-hugo-themes/issues/1677).
  - **Line 7** (`subtitle:`) sets a redirect to the `\news` page. This is the content found in the `news.md` file.
  - **Line 8** (`weight: 40`) determines how "high up" on the home page this section shows up (currently is the fourth element).
  - **Line 14** (`{{< readfromfile "/content/newslist.dat" 10 >}}`) specifies that the top 10-ish lines from `newslist.dat` should appear.
- `welcome.md` - the very top-most element on the home page is a summary of what the lab does as well as a pic of the Epibayes logo
  - **Line 8** (`weight: 10`) determines how "high up" on the home page this section shows up (currently is the first element). **All other pages must have a weight greater than 10.**
  - **Line 16** shows the logo being imported as a "figure": I found that importing images as "figures" allows them to be placed with `float`-based positions.
    - `figure` images are in the `assets/media` folder
#### The `learning/` folder compiles a brief list of publications, projects, and talks/tutorials created by lab members
- `_index.md` - tells Hugo what kind of page it is (it's a "page"-type page).
- The `projectpublication/` folder contains projects and publications:
  - `_index.md` - this file determines what shows up when navigating to the learning page.
    - **Lines 8 - 11** (`menu:`) show how the menu is set up: "Projects and Publications" will show up as a sub-menu of the "Learning" menu, in the first position (`weight: 1`).
  - `covidmapping.md` - information about covidmapping.org. 
    - **Line 13** (`weight: 1`) makes this the first result under the "Projects and Publications" menu.
  - `covidmodules.md` - information about COVID-19 learning modules.
    - **Line 13** (`weight: 2`) makes this the second result under the "Projects and Publications" menu.
  - `publications.md` - a brief list of publications starting from 2019 and extending up to the present.
    - **Line 13** (`weight: 3`) makes this the third result under the "Projects and Publications" menu.
- The `talkstutorials/` folder contains talks and tutorials:
  - `_index.md` - this file determines what shows up when navigating to the learning page.
    - **Lines 8 - 11** (`menu:`) show how the menu is set up: "Projects and Publications" will show up as a sub-menu of the "Learning" menu, in the first position (`weight: 1`).
  - `zelner_cscs_seminar.pdf` - the slides for `zelner2021cscs.md`.
  - `zelner2020estimating.md` - information about the shiny app built for diff-in-diff.
    - **Line 15** (`weight: 1`): all talks and tutorials are not ordered so they are given `weight: 1`.
  - `zelner2020usingsimulation.md` - information about the shiny app built for simulation inference.
    - **Line 17** (`weight: 1`): all talks and tutorials are not ordered so they are given `weight: 1`.
  - `zelner2021cscs.md` - information about the talk on epidemiological models and infection inequality.
    - **Line 18** (`weight: 1`): all talks and tutorials are not ordered so they are given `weight: 1`.
  - `zelner2021likelihood.md` - information about the shiny app built for model fit.
    - **Line 16** (`weight: 1`): all talks and tutorials are not ordered so they are given `weight: 1`.
  - `zelner2021residential.md` - information about the shiny app built for segregation transmission.
    - **Line 16** (`weight: 1`): all talks and tutorials are not ordered so they are given `weight: 1`.
  - `zelner2021smoothing.md` - information about the shiny app built for smoothing.
    - **Line 16** (`weight: 1`): all talks and tutorials are not ordered so they are given `weight: 1`.
#### The `people/` folder takes profiles from `authors/` and makes them into widgets to be displayed on the homepage
- `index.md` - tells Hugo what kind of page it is (it's a widget-type page).
- `<firstname>.md` - each lab member is given their own widget.
  - `weight: 1` - current lab members
  - `weight: 3` - former lab members
    - Nov. 2022 EDIT: Former Member category has been removed from view.
- `Former.md` - used as a "header" between current and former members. Has `weight: 2` so it comes before former members and after currentmembers.
  - Nov. 2022 EDIT: Former Member category has been removed.
#### The `post/` folder contains different blog posts made by lab members
- `_index.md` - this file determines what shows up when navigating to the post page.
- Each `<post name>/` folder contains at least an `index.md` file with the blog post.
  - If there are images associated with the blog post, they also are inside the respective `<post name>/` folder.
#### The `publication/` folder contains different publications (journal articles, preprints, etc.) made by lab members
- `_index.md` - this file determines what shows up when navigating to the publication page.
- Each `<publication name>/` folder contains an `index.md` file with details about the publication.
  - **Line 3** (`authors`) credits the authors of the publication.
    - For lab members, their `author/` folder name (i.e. "Stephanie-Choi") should be added with quotes around it.
      - Except for Jon, who can just be added as `- admin`.
    - For non-lab members, their name should be added in quotes but without the hyphen. (i.e. "Emily Martin").
  - **Troubleshooting:** Make it a habit to put things in quotes. Colons (`:`) and double quotes (`"`) inside text sections can throw off the render. Use escapes (`\`) within text blocks (like `abstract` and `summary` sections) to keep special characters inside them.

#### `news.md` and `newslist.dat` are used to build the recent news articles pages
- In `news.md`, line 16 allows `newslist.dat` information to be read in and turned into a "widget"
- `newslist.dat` is a markdown-format file that lists out news appearances and links to the articles.
### LAYOUTS/SHORTCODES
Only one relevant file here, called `readfromfile.html`. This allows the `news` pages to be created given the `newslist.dat` file.
### STATIC
The subfolders `files/` and `img/` have content.
- `files/` currently holds CV/Resume PDFs that are linked in `author/` lab member profiles.
- `img/` has the images used in `grant.md` as well as all images called using the `figure` call: currently, some blog posts in `posts/` and the `welcome.md` page use `figure` calls.