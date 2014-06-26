---
layout: page
title: Coding Standards
---

*Readability is more important than cleverness.*

## Project design/ technology choices

* Choose the best technology stack for the combination of the needs of the
  project and our knowledge/sysadmin/support capabilities - if you're going for
  something new, we as a team will need to ensure we can deploy it, back it up
  etc by the time it goes live. Be proactive in starting comunication/planning
  around this early and be prepared to muck in.
* e.g. Database choice
* Progressive enhancement is the Right Thing to do. See e.g. [this
  article](http://jakearchibald.com/2013/progressive-enhancement-still-important/)
* URLs

## Coding

### General style

* Try to be aware of the idioms of the language you're working in, and use them.

#### Python style resources:
* [PEP8](http://legacy.python.org/dev/peps/pep-0008/)
* [PEP257](http://legacy.python.org/dev/peps/pep-0257/)
* [Django Coding Style Guide](https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/coding-style/)
* [flake8](https://pypi.python.org/pypi/flake8)

#### Ruby style resources:
* [ruby-style-guide](https://github.com/bbatsov/ruby-style-guide)
* [rubocop](https://github.com/bbatsov/rubocop)
* [rails-style-guide](https://github.com/bbatsov/rails-style-guide)

### Indentation and whitespace

* If the language you're using has a clear convention (e.g. ruby 2 space
  indents), follow that. Otherwise, indents are spaces, in steps of 4.
* In nice templates (e.g. Catalyst, Django, etc), try indenting HTML 4, but IF
  statements and the like 2 (ie. inbetween the HTML indents). This can be quite
  a clear way to indent loops and conditional blocks, and yet keep it visually
  readable (e.g. if you have some items of a UL be conditional, some not).
* Don't have any trailing space at the end of lines (this can cause problems
  with e.g. JS continuations, or PHP end of files).
* Actually, with PHP, make sure you end your file *without* a final `?>` as
  then we don't have to worry about that particular problem.
* Files should be Unix encoded, not Windows encoded (`\n` not `\r\n`).
* In general, put spaces around operators.
* Whilst it may be slightly more readable to line up a group of e.g. variable
  assignments under the `=`, it makes it more confusing if that list is edited
  in future and the commit shows other lines have (needlessly) changed. So not
  recommended, but allowable.
* Try not to let line lengths exceed 80 characters.

### Control structures

* Braces should be on the *same line* as the if/elseif/else/etc. statement they
  are attached to. They should have space aside them, not touching a bracket or
  text.
* *Never* omit braces on single line statements on a separate line. It only
  leads to disaster in future. You may get away with `if ( foo ) { return; }`
  but only if it is doing something extremely obvious and clear (e.g. returning
  from a function early).
* If you have a multi line array definition or similar, put the closing `)` on
  its own line aligned with the start of the definition.

### Functions and classes

* Be clear what a function is doing, in terms of returning data. Have a default
  return value.
* In general, classes have a capital letter.
* Use underscores or camelCase dependent upon the language's preference, but be
  consistent.

### Strings and constants

* PHP - use single quotes if you don't need variable interpolation.
* SQL - put keywords such as `SELECT`, `UPDATE`, etc. in all caps to make them
  easy to find and distinguish.
* If you have a site wide constant, try and put it in ALLCAPS.

### Tests

* If fixing a bug, the best practice way to proceed is to write a test that
  fails due to the bug, fix the bug, then make sure the test passes.
* Different projects have different approaches to tests. Older projects have a
  monolithic test-run script which acts as a browser and visits parts of a test
  site. This is fine, but slow; nevertheless, please do add to and check it
  passes if working on those. Newer frameworked projects all have their own way
  of running tests; hopefully they all have tests already, so find them and add
  there. If starting a new project, adding tests is a requirement and
  considered as part and parcel of development time. As with commit messages,
  tests are for anyone ever working on the project ever in the future; they
  provide security that changes can be made. For a mature project the ideal is
  to have some unit tests and some functional tests for key scenarios.

## Committing code and working with repositories

* When committing, please commit individual changes in separate commits (not
  one "Fixes this and this and this and this" commit), unless for some reason
  that is impossible to do. In any case, please describe the change the commit
  makes as clearly as possible - you are documenting this change for anyone
  ever working on the project ever in the future, so please avoid "Update
  style" or "Improve flow".
* Ticketing - if you find a bug, ticket it. If you think of a feature request,
  ticket it. If you're asked to implement something and it isn't already
  ticketed, tell the person off who told you to do it, and ticket it. If you
  are working on something and have an update for others working on the
  project, leave an update on the ticket if appropriate. Refer to ticket
  numbers in commits, and basically do everything to ensure that things are
  linked together and documented automatically as much as possible. Basically,
  if you go on holiday for a year, it would be good if we can look at your
  tickets and see what you were working on and where you got to.
* Although there are some differences between projects, our standard
  workflow is that code that is merged into the deployable branch
  (typically `master`) should have been reviewed and approved by
  another developer before that merge happens, although you
  should use common sense to decide when a pull request and
  review is needed.  For more details on code reviews, see the
  next section.

## Commit messages

Good commit messages are very important for making our
repositories easy to work in.  Commit messages like "fix bug",
or "More changes" are of no use to anyone.  git makes it easy to
search for when a change was introduced, and good commit
messages provide invaluable context for that change to a
developer who might need to know about the code many years
after it was written.

A good commit message should explain *why* the change it
introduces was needed, and (particularly if the implementation
is non-obvious) a explanation of *what* was done.

Although it's helpful to reference GitHub issues in a commit
message (e.g. "Fixes #1234" so that the issue is closed
automatically) you shouldn't assume that the person reading the
commit message has access to that issue since it isn't in the
repository (and we might move to another bug tracker in the
future).  The commit message should still concisely explain the
bug that's being fixed.

In terms of formatting of the commit message it should have the
following structure:

    A summary of the change introduced in the commit, under 72 characters

    After a blank line, a fuller description of why the change
    was introduced, any necessary background, and a summary of
    the change made for more complex issues.  This summary
    should be hard-wrapped at under 72 characters.

    If in doubt, more discussion and context rather than less is
    preferred.

## Code reviews

For any project you're working on, you should know which other other
developers are expected to be able do code reviews for you.  If it's
not clear to you who those people are, please establish that by email.
When you make a pull request, it's a good idea to also explicitly ask
in IRC for one of those possible reviewers to look at it, since it's
easy to miss GitHub notifications given their volume.  As the reviewer
of a pull request, here is some guidance for what to do:

* Look at it as soon as you can, or let the author know when you can
  deal with it.  The shorter the feedback loop here the better: it's
  essentially the "fail fast" principle.
* Start by thinking about the intent of the pull request and the big
  picture before looking at the details of the implementation.
  Although pointing out typos or non-idiomatic language uses is
  helpful, and certainly part of the review process, it's not worth
  the author dealing with those if they're in sections of code
  that shouldn't even be there, for example.
* Anything that you'd like the author to fix, or take action on,
  should be left in a GitHub comment on the pull request rather
  than just mentioned to them in IRC.  (Of course, it's often
  helpful to check things with the author in IRC, but please
  bear in mind that if something wasn't clear to you, it might
  well be the case that the code should be clearer, have some
  comments added, or that the commit messages should be better.)
* As the reviewer, it's **not** your responsibility to make the
  changes - you shouldn't just add extra commits to the pull request,
  for example.  It's the original author's work and you are just
  suggesting changes that they should make, not do it for them.
* Remember to check that the pull request includes tests that cover
  any new code and would detect regressions.
* Leave a comment when you've finished the review - a simple
  `:+1:` is sufficient if there are no problems.  The original
  author can then go ahead to merge and push.  (Note that while
  in other organisations it's common for the reviewer to merge
  and deploy if they're happy with the code, our convention is
  that the author deals with this after getting a thumbs-up,
  since they are likely to be in a better position to deal with
  any conflicts on merging or problems on deploying.)
* Please be constructive and kind in your feedback.

(For more advice about doing good code reviews, [this article may be
useful](http://alexgaynor.net/2013/sep/26/effective-code-review/).)

As the coder:

* When making changes to pull requests following initial review, it
  makes the request easier to re-review if you make changes in
  subsequent commits rather than rewriting. Otherwise it takes more work
  for the reviewer to figure out/remember what's changed. The fixup
  commits can then be squashed or merged into other commits before
  merging into the main branch.

If no one who can do a review of your pull request is around, you need
to assess whether it's so urgent that you need to merge it
regardless.  If you're not clear about this do ask about it by
email or IRC.

## Documentation and maintainability

* At a minimum, there should be a list of steps required to install the
  project. As the project matures, and hopefully proves to be useful, consider
  making the codebase easier to install - see, for example our [installation
  standards]({{ site.baseurl }}installation-standards.html)
* Every project should have a README(.md, whatever) for its GitHub page, so
  aimed primarily at those who will know what GitHub is.
* As with code, wrap long lines. It makes it easier to read on GitHub and to
  compare diffs.
* In code: don't overcomment, but don't undercomment either. If your language
  provides a way to document functions nicely (python docstrings, perldoc), do
  use them to provide overview documentation of code.
* Think about *maintainability* - if someone comes new to work on the project,
  what do they need to know? If you are incapacitated for a long period of
  time, what information do you only hold inside your head? Please get it
  written somewhere.
* Outside code: There are many places for documentation; we will probably never
  settle on where is best. You can document in files in the repository, you can
  use the GitHub wiki, have a GitHub site even.

## Browser testing

* Many of our users are in government, or well outside the normal tech-savvy
  world we inhabit. They will have older browsers, and less knowledge of using
  computers. Our sites should still work in IE6, though of course functionality
  may differ, we are in no way a "pixel-perfect" house.
* You can get VMs of IE6-11 from
  [modern.ie](http://www.modern.ie/en-US/virtualization-tools#downloads). On
  Linux/OS X a tool called [ievms](https://github.com/xdissent/ievms) automates
  the installation process - see [these
  instructions](https://github.com/xdissent/ievms#installation). Or Robin has a
  browserstack account for quick testing.
* For info, IE7 was the oldest version to support position:fixed and
  min/max-width; IE8 was the oldest to support display:table and
  box-sizing:border-box; IE9 was the oldest to support media queries.
* Media queries - Various approaches possible. If going with a mobile-first
  approach (probably wise), FixMyStreet puts all the "desktop" type styles in a
  separate stylesheet and includes that both with a media query and with an IE
  conditional comment. Or you could use Respond.js if your IE usage is
  considered low enough (it can have an effect on IE browsing).
* Using new features - you are encouraged to use modern features that make CSS
  development easier, but not at the expense of old IE going horribly wrong
  (see first bullet point). So if you use display:table, or box-sizing, and
  these cause a large adverse effect, you must have workarounds. You may find
  [caniuse.com](http://caniuse.com/) helpful in determining what is safe to
  use.

## Language-based dependency managers

If your vhost wishes to use python packages from PyPi, ruby gems, or whatever,
please do not use a language specific way of installing something globally
(e.g. sudo gem install) as there is no record of what has been installed and
will cause issues when it comes to deployment. There are the following options:

* Install a Debian package for that code, and use that in your code (e.g. if
  you're happy with the Debian version of django, or sass) - a python
  virtualenv will need to have access to system site packages (see e.g. sayit's
  set up script for version-independent way of doing that);
* For python, use virtualenv to install packages locally for that vhost, and
  list them in a requirements.txt file;
* For ruby, if it's a whole app you probably want to investigate e.g. bundler.
  If you just need a gem for e.g. CSS compilation, then you should alter/setup
  your GEM_HOME to somewhere within your vhost to install the gems, add it to
  GEM_PATH, and add the bin directory to PATH. (You could theoretically use gem
  install --user-install, but this could lead to confusion as a developer if
  you have multiple developer sites on one server and need to keep version
  separation).

## Helpful tools

* Django-based: we have a [django-jumpstart
  repository](https://github.com/mysociety/django-jumpstart) to start the setup
  of a Django project.
* Django-based: DjDT (Django Debug Toolbar) is very useful for local
  development.
