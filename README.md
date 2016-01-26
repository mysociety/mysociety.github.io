# mySociety Developer Information

This site holds information for mySociety developers and volunteers, to help
them produce better code, open better issues, and create pull requests more
likely to be accepted.

## This Site

### Installing

This site is mostly compiled by magic – specifically
[Jekyll](http://jekyllrb.com/) and [Sass](http://sass-lang.com/) which will
have to be installed before you can do anything.

Unless you have a good reason not to, you will probably want to use Bundler
to install the ruby dependencies. Just run this from the root directory of
this repo:

    bundle install --path vendor/bundle

Also, make sure to check out the latest version of the `theme` submodule:

    git submodule update --init

### Compiling

Compile the Sass styles from the theme, with:

    bundle exec sass --watch theme/sass:assets/css --style compressed

And run the Jekyll server with:

    buyndle exec jekyll serve

The website will be available at `http://localhost:4000` and will recompile
automatically when files are changed.

### Workflow

Since this site involves describing standards, changes should be properly
controlled and discussed. This should be done through GitHub pull requests.

#### Substantial Changes

To propose substantial changes, such as a change in an actual standard, here's
what to do:

1. Branch `master`, giving your new branch a sensible name.
2. Open a GitHub pull request from your feature branch to `master`. This is
   where debating the merits of changes should happen.
3. When everybody is happy with the changes, merge the branch into `master`.
   The pull request on GitHub will close itself, and the published site will
   recompile.

#### Minor Changes

If you are making a minor, uncontentious change (such as updating a list of
references or fixing a typo) then changes can be made directly on the `master`
branch. The published site will recompile once changes are pushed to GitHub.
