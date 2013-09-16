---
layout: page
title: Coding Standards
---

*Readability is more important than cleverness.*

### Project design/ technology choices

* Choose the best technology stack for the combination of the needs of the
  project and our knowledge/sysadmin/support capabilities - if you're going for
  something new, we as a team will need to ensure we can deploy it, back it up
  etc by the time it goes live. Be proactive in starting comunication/planning
  around this early and be prepared to muck in.
* e.g. Database choice
* Progressive enhancement is the Right Thing to do. See e.g. [this
  article](http://jakearchibald.com/2013/progressive-enhancement-still-important/)
* URLs

### Coding

#### Indentation and whitespace

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

#### Control structures

* Braces should be on the *same line* as the if/elseif/else/etc. statement they
  are attached to. They should have space aside them, not touching a bracket or
  text.
* *Never* omit braces on single line statements on a separate line. It only
  leads to disaster in future. You may get away with `if ( foo ) { return; }`
  but only if it is doing something extremely obvious and clear (e.g. returning
  from a function early).
* If you have a multi line array definition or similar, put the closing `)` on
  its own line aligned with the start of the definition.

#### Functions and classes

* Be clear what a function is doing, in terms of returning data. Have a default
  return value.
* In general, classes have a capital letter.
* Use underscores or camelCase dependent upon the language's preference, but be
  consistent.

#### Strings and constants

* PHP - use single quotes if you don't need variable interpolation.
* SQL - put keywords such as `SELECT`, `UPDATE`, etc. in all caps to make them
  easy to find and distinguish.
* If you have a site wide constant, try and put it in ALLCAPS.

#### Tests

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

### Committing code and working with repositories

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

### Documentation and maintainability

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

### Browser testing

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

### Helpful tools

* Django-based: we have a [django-jumpstart
  repository](https://github.com/mysociety/django-jumpstart) to start the setup
  of a Django project.
* Django-based: DjDT (Django Debug Toolbar) is very useful for local
  development.
