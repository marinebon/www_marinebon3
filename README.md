# www_marinebon3

* [Up & running with blogdown in 2021 | Alison Hill](https://alison.rbind.io/post/new-year-new-blogdown/)

## Create blogdown site

* [1.2 A quick example | blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/a-quick-example.html)

  - Create
    ![](https://bookdown.org/yihui/blogdown/images/new-project.png)
    Or:
    ```r
    blogdown::new_site()
    ```

  - Serve
    ![](https://bookdown.org/yihui/blogdown/images/addin-serve.png)
    Or:
    ```r
    blogdown:::serve_site()
    ```

## Add post

Addins > <span style="color:gray">BLOGDOWN:</span> New post

Or:

```r
blogdown:::new_post_addin()
```

## Check

- Check

```r
blogdown::check_site()
```

Attended to all TODOs:

```
― Running a series of automated checks for your blogdown website project...
----------------------------------------------
○ A successful check looks like this.
● [TODO] A check that needs your attention looks like this.
| Let's check out your blogdown site!
----------------------------------------------
― Checking config.yaml
| Checking "baseURL" setting for Hugo...
○ Found baseURL = ""; nothing to do here!
| Checking "ignoreFiles" setting for Hugo...
● [TODO] Add these items to the "ignoreFiles" setting: "\\.knit\\.md$", "\\.utf8\\.md$"
| Checking setting for Hugo's Markdown renderer...
○ All set! Found the "unsafe" setting for goldmark.
― Check complete: config.yaml

― Checking .gitignore
| Checking for items to remove...
○ Nothing to see here - found no items to remove.
| Checking for items to change...
○ Nothing to see here - found no items to change.
| Checking for items you can safely ignore...
● [TODO] You can safely add to .gitignore: .DS_Store, Thumbs.db
| Checking for items to ignore if you build the site on Netlify...
● [TODO] When Netlify builds your site, you can safely add to .gitignore: /public/, /resources/
| Checking for files required by blogdown but not committed...
● [TODO] Found 1 file that should be committed in GIT:

  layouts/shortcodes/blogdown/postref.html
― Check complete: .gitignore

― Checking Hugo
| Checking Hugo version...
○ Found 3 versions of Hugo. You are using Hugo 0.83.1.
| Checking .Rprofile for Hugo version used by blogdown...
| Hugo version not set in .Rprofile.
● [TODO] Use blogdown::config_Rprofile() to create .Rprofile for the current project.
● [TODO] Set options(blogdown.hugo.version = "0.83.1") in .Rprofile and restart R.
― Check complete: Hugo

― Checking netlify.toml...
○ Found HUGO_VERSION = 0.81.0 in [build] context of netlify.toml.
| Checking that Netlify & local Hugo versions match...
| Mismatch found:
  blogdown is using Hugo version (0.83.1) to build site locally.
  Netlify is using Hugo version (0.81.0) to build site.
● [TODO] Option 1: Change HUGO_VERSION = "0.83.1" in netlify.toml to match local version.
● [TODO] Option 2: Use blogdown::install_hugo("0.81.0") to match Netlify version, and set options(blogdown.hugo.version = "0.81.0") in .Rprofile to pin this Hugo version (also remember to restart R).
| Checking that Netlify & local Hugo publish directories match...
○ Good to go - blogdown and Netlify are using the same publish directory: public
― Check complete: netlify.toml

― Checking content files
| Checking for validity of YAML metadata in posts...
○ All YAML metadata appears to be syntactically valid.
| Checking for previewed content that will not be published...
● [TODO] Found 1 file with a future publish date:

  content/event/example/index.md

  If you want to publish today, change a file's YAML key to 'date: 2021-05-05'
● [TODO] Found 2 files marked as drafts. To un-draft, run the command:

  blogdown::edit_draft(c(
  "content/privacy.md",
  "content/terms.md"
  ))

  and change a file's YAML from 'draft: true' to 'draft: false' or delete it
| Checking your R Markdown content...
○ All R Markdown files have been knitted.
○ All R Markdown output files are up to date with their source files.
| Checking for .html/.md files to clean up...
○ Found 0 duplicate .html output files.
○ Found 0 incompatible .html files to clean up.
| Checking for the unnecessary 'content/' directory in theme...
○ Great! Your theme does not contain the content/ directory.
― Check complete: Content
```

Miscellaneous commands used fixing above TODOs:

```r
blogdown::config_Rprofile()

blogdown::edit_draft(c(
"content/privacy.md",
"content/terms.md"
))

blogdown::check_site()
```

## Add Github Action

- `blogdown` one of [r-lib/actions: /examples](https://github.com/r-lib/actions/tree/master/examples#example-workflows)

```r
usethis::use_github_action("blogdown")
```

```
✓ Setting active project to '/Users/bbest/github/marinebon/www_marinebon3'
✓ Creating '.github/'
✓ Adding '^\\.github$' to '.Rbuildignore'
✓ Adding '*.html' to '.github/.gitignore'
✓ Creating '.github/workflows/'
✓ Writing '.github/workflows/blogdown.yaml'
• Learn more at <https://github.com/r-lib/actions/blob/master/examples/README.md>
```

```r
usethis::use_github_action("blogdown")
blogdown:::serve_site()
```

## Github Action to Netlify

Followed:

* [Deploy your bookdown project to Netlify with Github Actions | Emil Hvitfeldt](https://www.hvitfeldt.me/blog/bookdown-netlify-github-actions/)

Netlify -> Github Secrets in repository:

- API ID -> `NETLIFY_SITE_ID`
- Personal Access Token -> `NETLIFY_AUTH_TOKEN`

Q: Why not just publish to Github Pages vs deploy additionally to Netlify?


```r
blogdown:::serve_site()
renv::snapshot()
```

```bash
git commit -m "init rstudio/blogdown site w/ Hugo wowchemy/academic-starter and GH Action to Netlify deploy"
git push
```
