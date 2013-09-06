# mySociety Developer Information

This site holds information for mySociety developers and volunteers, to help them produce better code, open better issues, and create pull requests more likely to be accepted.

## This Site

This site is mostly compiled by magic (specifically [Jekyll](http://jekyllrb.com/) and [Compass](http://compass-style.org/), using the [Foundation](http://foundation.zurb.com/) framework), which will have to be installed before you can do anything. The following commands will install the necessary software:

* `sudo gem install github-pages` for preference, or (if you have an older version of Ruby) `sudo gem install jekyll`
* `sudo gem install zurb-foundation`
* `sudo gem install compass`

You may find the following commands useful:

* `jekyll serve --watch` - Starts a web server on `localhost:4000` with the latest compiled copy of the site. Recompiles when files change.
* `compass watch` - Monitors static asset folders (most usefully the `sass` folder) for changes, and recompiles when necessary.