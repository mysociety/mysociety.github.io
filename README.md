# mySociety Developer Information

This site holds information for mySociety developers and volunteers, to help them produce better code, open better issues, and create pull requests more likely to be accepted.

## This Site

### Compiling

This site is mostly compiled by magic (specifically [Jekyll](http://jekyllrb.com/) and [Compass](http://compass-style.org/), using the [Foundation](http://foundation.zurb.com/) framework), which will have to be installed before you can do anything. The following commands will install the necessary software:

* `sudo gem install github-pages` for preference, or (if you have an older version of Ruby) `sudo gem install jekyll`
* `sudo gem install zurb-foundation`
* `sudo gem install compass`

You may find the following commands useful:

* `jekyll serve --watch` - Starts a web server on `localhost:4000` with the latest compiled copy of the site. Recompiles when files change.
* `compass watch` - Monitors static asset folders (most usefully the `sass` folder) for changes, and recompiles when necessary.

### Workflow

Since this site involves describing standards, changes should be properly controlled and discussed. This is achieved using the  [git flow](http://nvie.com/posts/a-successful-git-branching-model/) branching model, combined with pull requests. You might find this [git flow cheatsheet](http://danielkummer.github.io/git-flow-cheatsheet/) to be useful.

Sticking to this workflow makes sure that changes are properly discussed and managed, and that there are clear published versions of the standards.

#### Substantial Changes

To propose substantial changes, such as a change in an actual standard, here's what to do:

1. Start a new feature (`git flow feature start {name}`).
2. Open a GitHub pull request from your feature branch to `develop`. This is where debating the merits of changes will happen.
3. When everybody is happy with the changes, finish the feature (`git flow feature finish {name}`). When you push your changes the pull request will be closed automatically.

The `develop` branch contains the current 'working' state of the standards. After a significant set of changes have been approved and merged, you should:

1. Start a new release with a suitable [version number](http://semver.org/) (`git flow release start {version}`).
2. Give the content a final proof reading.
3. If necessary, make changes in the release branch.
4. When you're happy with everything, finish the release (`git flow release finish {version}`)

#### Minor Changes

If you are making a minor uncontentious change (such as updating a list of references or fixing a minor typo) then changes can be made directly on the `develop` branch.