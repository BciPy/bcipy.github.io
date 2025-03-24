# BciPy Documentation

This website was created with the intention of hosting articles, documents, and research about BCI using BciPy!

## BciPy Code Documentation

If you are looking for CAMBI's BciPy source code, please visit [BciPy Github](https://github.com/CAMBI-tech/BciPy).

Most users will be add content to the `_posts` and `_faqs` directories. The `_posts` directory is for markdown blog posts and the `_faqs` directory is for FAQ markdown files. The blog posts and FAQ markdown files are written in markdown and contain front matter at the top of the file. The front matter contains metadata about the post or FAQ such as the title, date, author, tags.

Structure of the website:

- `_data` - Contains the main navigation and footer data in the form of yml files
- `_includes` - Contains the html snippets that are included in the layout
- `_layouts` - Contains the layout of the website
- `_posts` - Contains the blog posts. This is where new markdown files should be added.
- `_faqs` - Contains the FAQ markdown files. This is where new FAQ markdown files should be added.
- `_site` - Contains the generated site. This is where the website is built and these files are not to be committed to the repository.
- `_sass` - Contains the main styling for the website
- `_config.yml` - Contains the configuration for the website
- `assets` - Contains the css, images, and js files. Any new css, images, or js files should be added here and linked in the respective post or layout files.

## Installation

- Install Homebrew and/or update via `brew update`
- Follow the [Jekyll](https://jekyllrb.com/docs/installation/) installation instructions for your operating system. This will require Ruby to be installed (there are instructions on the Jekyll website for this and supported versions).
  - Alternatively, you can run `brew install ruby` to install Ruby
  - then run `gem install jekyll bundler` to install Jekyll and Bundler
- Run `bundle install` at the root of the project to install the required gems.

### Troubleshooting

- `bundler: failed to load command: jekyll` - This is likely due to the `bundler` gem not being installed correctly or it may need to be updated. Run `gem install bundler` to install or `bundle update` to update.
- `jekyll: command not found` - This is likely due to the `jekyll` gem not being installed correctly or it may need to be updated. Run `gem install jekyll`. See the [Jekyll Troubleshooting](https://jekyllrb.com/docs/troubleshooting/) page for more information on common issues.

### Running the website locally

- Run `bundle install`
- Run `bundle exec jekyll serve`

### Full theme documentation can be found here

- https://jekyllthemes.io/theme/desk-responsive-knowledge-base-and-faq-jekyll-theme

## Search

The search functionality is powered by [Simple-Jekyll-Search](https://www.npmjs.com/package/simple-jekyll-search). This is defined in the `_includes/navbar.html` file. The search functionality is configured by the `search.json` file. The search functionality is case-insensitive and will search for the following title, category, tags, url and date fields in the posts.
