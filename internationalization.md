---
layout: page
title: Internationalization
---
-   [Introduction](#introduction)
-   [General Guidelines](#general-guidelines)
-   [Examples](#examples)
-   [Checklist](#checklist)

## Introduction

Marking up text for translation in a way that will actually make it
possible for people using languages with different grammars to translate
the text coherently involves doing things that are counterintuitive for
a programmer! e.g. you don't want to break sentences into smaller
fragments that can be combined. Some resources to read **before** you
start marking up application text for translation:

-   [http://www.gnu.org/software/gettext/manual/html\_node/Preparing-Strings.html](http://www.gnu.org/software/gettext/manual/html_node/Preparing-Strings.html)
-   [http://www.gnu.org/prep/standards/html\_node/Internationalization.html](http://www.gnu.org/prep/standards/html_node/Internationalization.html)

## General Guidelines

### Don't concatenate strings to "build" a sentence

Different languages put things in different orders in the sentence. A
trivial example would be `"the " + $colour + " house"` where many
languages would need to move the `$colour` after the word "house". This
applies even when putting something as simple as a number at the end of
a sentence: `"Number of tries: " + $tries` — don't do it. Some languages
will need to add something after the number. In all these cases,
**include a full *unit of meaning* within a single translatable
string**, using tokens to insert variables into it, so the translator
can render it with the variables in any order needed.

### Don't let identical strings be "grouped" in the translation file, if you can help it

If a string, say `_("Print")`, is used several times in your code, your
i18n engine may well group all the uses together in the translation
file, and present it to translators just once for translation. Problem
is, it may well need to be translated differently depending on the
context, e.g. whether it's a button label/menu option or a page title, a
noun or a verb, etc. There's often a way to force each string to be
considered unique, either by using a unique token in place of each
translatable string, or by optionally adding something to make
otherwise-identical strings unique one at a time, as required.

### Fill your code to bursting with comments that explain CONTEXT of a translatable string

...pretty much every one of them, even when it appears to be bloody
obvious to you. No, really. These comments need to be in a format that
will be copied over to the translation file. Your translators may or may
not have access to the source code; even if they do, they may well not
understand it, at all. On the other hand, their default translation
interface will include any comments contained in the translation file. I
once saw the phrase "Print Options" translated (quite reasonably) into
many languages as though it meant "Options for printing", but examining
the source code revealed that it actually meant "Print out the list of
options". That label will be unhelpful and meaningless in many of the
localised versions of that particular application. I regularly see
things like "%s by %s" for translation, but I need to know what each %s
represents to be able to do it properly. The clarifying comment should
definitely explain what any variables represent that will be inserted
into the string; can usefully include info on what page/screen/dialog
the string appears in; say what the words in it refer to; whether it's a
label on a button, a clickable link, a title, an instruction to the
user, or whatever.

### Consider plurals carefully

Definitely don't hard-code a singular/plural.
`n=1 ? _("page") : _("pages")` is all wrong. (See "concatenating
strings" above). Your i18n framework will have a specific format for
dealing with plurals. Please use it. Lots of languages use singulars and
plurals like English, but lots of others don't. Arabic and Slovene have
a "dual" form, used when you've got two of something. Russian has a form
for "2, 3, or 4" or something, and the "plural" only kicks in from 5
upwards. The i18n framework will handle that, as long as it's invoked
correctly by the coder.

### Consider what to leave out of the translation process

Not *every* string to be displayed necessarily needs including in the
translation file. If it's part of an admin interface that only appears
to coders, does it need translating? Possibly, possibly not, you decide,
but don't create unnecessary work. When we met with the clients for
FixMyBarangay (the Philippines FixMyStreet project) contrary to our
expectations it was made clear that the admin site (which is, for the
pilot, pretty much **all** of FMS) could and should be entirely in
English, and translation was not needed (even though the administrators
may well be manipulating data in another language). So don't guess:
check with the project manager if your translation is really necessary.

## Examples

### "not sent to council"

How to translate the string *"not sent to council"* into French? I need
to know *what* hasn't been sent (a message, a report, a letter, some
information); and whether it's a label on a single example of something
not sent, or the heading of a list of lots of them. Why? Because
*envoyé* ("sent") needs an extra *e* if the thing that's sent (or not
sent) happens to be a feminine noun; and it'll need an *s* too if we're
referring to more than one of them. The translator has to know all of
this information to give an adequate translation; otherwise you might as
well feed it through Babelfish and cross your fingers. If the same
phrase is used on both a single message and on a list of messages, it
*must* appear as two separate entries in the translation file (see
"grouping identical strings"). If the phrase appears once in the code,
but can refer to one or to many things not sent to the council, it will
actually require the coder to think beyond English and to allow for a
plural where English doesn't need one. This kind of thing is difficult
to cater for unless you're planning the software in numerous languages
before it's coded; and in fact, it's impossible to cover everything that
might be required, as there will always be some language that needs
something done differently. In some cases, you just have to wait for
patches (or just complaints) from individual translators.

### "(optional)"

As above, the translator needs to know (via a clarifying comment in the
translation file) *what* is optional — one thing? many things? what?
This is probably a label on a form field or something, but the
translator doesn't know that unless you inform them; if it were a label
on a button which will make something become optional, then the
translation may well be different, but without checking the source code,
there's no way of knowing. (Assume the translator doesn't have access to
the source code, is disinclined to look at it, or just incapable of
gleaning anything from it). To complete the example, if the thing that's
optional is *information* or *an address* or *hair colour*, then the
translation into French would be *facultative*. If it's a *message* or a
*phone number* or a *name* that's optional, then it's *facultatif*.
(French is weird like that, OK? But it's massively less weird than
Slovene, or Farsi, or Swahili, honest). If the same label is used for
several different things, then the translator needs to be able to
translate each case separately, and have a clarifying comment for each
to explain what is being labelled as "optional" so they can provide the
correct translation.

## Checklist

-   If your translation file contains single prepositions as
    translatable strings (e.g. "to", "by", "at", etc.) you've done it
    wrong. Your code is impossible to localise.
-   If your translation file contains single prepositions with a token
    or two (e.g. " at %s", "%d off", etc.) you're half way to doing it
    right. The strings *will* be translatable once the translator knows
    what "%s" represents, so add a comment (in the translation file),
    e.g. "%s is a date", or "string appears as ' at 10:00'").

## Working with .po files

### Manual process, ignoring Transifex

This can be partly project dependent, but in the general case, things
work as follows. If you have added new strings to the codebase, you run
a script like gettext-extract that will search the codebase for strings
and add them to the master .po file. You then run gettext-merge in order
to bring each of the language .po files up to date with these strings
(any strings now no longer used will be commented out and moved to the
bottom, nothing a translator has done should be lost). You then commit
these changes, and can then ask the translator(s) to work from their new
file with its new strings. If a translator sends you a file based upon
an older master .po file than the one now present (you can tell this by
looking at the POT-Creation-Date line near the top of the .po file
you've been sent compared with that in the repository), then you can run
gettext-merge immediately in order to bring it back in line (and hope
that they haven't bothered to translate something that's now no longer
there). Once you have some .po file you want to see on the site, you
need to run gettext-makemo which compiles the .po files to .mo files.
Apache will not notice changes to .mo files without a restart,
annoyingly.
