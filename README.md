# LiveCoMS content

This repository provides public-facing access to the content of the [author instruction/policy pages for the Living Journal of Computational Molecular Molecular Science (LiveCoMS)](https://livecomsjournal.github.io).

The journal itself is published via Scholastica at [livecomsjournal.org](http://livecomsjournal.org), but full author instructions and policy information are maintained at [livecomsjournal.github.io](https://livecomsjournal.github.io) and this repository provides access to edit the content of the latter site.

## Contacts

If you have questions or concerns, please use our issue tracker here, or contact the managing editors at [managing@livecomsjournal.org](mailto:managing@livecomsjournal.org).

## Generate navigation
The subpages of [livecomsjournal.github.io](https://livecomsjournal.github.io) have a navigation column on the left (see [livecomsjournal.github.io/authors/policies/](https://livecomsjournal.github.io/authors/policies/) for an example). This navigation is read from `_data/navigation.yml` and is static, meaning that it needs to be re-generated whenever changes to the structure of a document are done. Specifically, the navigation consists of links to all first and second title levels (`# Title` and `## Title` in Markdown), and if any of those are changed, the navigation needs to be updated.

There is a script named `generate_navigation.py` which generates the content of the navigation file. Calling
```
python3 generate_navigation.py > _data/navigation.yml
```
regenerates the navigation file with the current state of the Markdown-files. It does so by reading through all `.md` files (except `index.md`) in the `_about_livecoms`, `_author_instructions` and `_editorial_policies` and generating a menu item for every first-level or second-level title. It also read the frontmatter of each file and rewrites it in case no `permalink` or no `sidebar` tag is found.

The script is helpful, but probably not fool-proof - a visual inspection of the result via `git diff`, or even better a check of the result in a local jekyll installation is highly recommended before pushing the new navigation file to the `master` branch.

## Testing Locally

First you will need to install the gem for `github-pages`. Run the following command:

```
gem install github-pages
```

This will install the github-pages gem and all dependencies (including jekyll).

Later, to update the gem, type:

```
gem update github-pages
```

To build a local copy, go into the directory and type:

```
jekyll build
```

This will create (or modify) a _site/ directory, containing everything from assets/, and then the index.md and all pages/*.md files, converted to html. (So there’ll be _site/index.html and the various _site/pages/*.html.)

**Do not commit this directory in a Pull Request!! Github will compile this directory on its own.**

Type the following in order to “serve” the site. This will first run build, and so it does not need to be preceded by `jekyll build`.

```
jekyll serve
```

Now open your browser and go to http://localhost:4000
