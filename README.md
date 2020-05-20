# Notes

My Changelog:
* Use Markdown instead of text


Original Creator Notes are Below

## Notes [![Build Status](https://travis-ci.org/nickjj/notes.svg?branch=master)](http://travis-ci.org/nickjj/notes)

A zero dependency shell script that makes it really simple to manage your text
notes.

Instead of trying to impose a whole bunch of rules and syntax requirements,
this tool does its best to get out of your way.

It tries to do everything possible so that if you're working in a terminal, you
can save whatever text you want into a file. This could come from typing a
sentence out, pasting something from your clipboard or saving the output of a
program.

## Demo Video

[![Demo
video](https://nickjanetakis.com/assets/blog/cards/organize-your-text-based-notes-from-the-command-line-with-this-script-53667299e8d44dbc6091a80a477dc540e201da4aa47ba974f630da4690500444.jpg)](https://nickjanetakis.com/blog/organize-your-text-based-notes-from-the-command-line-with-this-script)

#### Updates to the notes script since this video

- `v0.2.0` scopes the notes files [per month instead of per
  day](https://github.com/nickjj/notes/commit/4693109f27dc15da6626e3afbba53730810df026).
  This differs from what's in the video at the 4:00 mark.
- `v0.1.0` matches exactly what's in this video.

## Design Goals and Philosophy

I've been keeping track of my notes in plain text files since 2001. I always
felt like when it comes to jotting down notes it was always best to do
everything possible to keep friction low.

That means not worrying about specific file types, formatting, tagging,
check boxes, syntax rules and a bunch of other things that delay you from
getting something out of your head and into a document.

### Text is amazing for notes because:

- You can use `grep` and friends to search through it later
- Even with notes dating back from 2001, I'm only using 1.5mb of disk space
- It's really easy to back up and sync to other devices using Drop Box or similar tools

Since it's unstructured text you can use this tool for whatever type of note
taking you want. You can keep track of general thoughts, create a diary or make
plan files similar to what John Carmack did [for a number of
years](https://github.com/ESWAT/john-carmack-plan-archive).

I personally use it as a scattered brain dump. Even with things being very
unstructured (and even untagged) I can usually `grep` out anything I want
within a few seconds.

### Your notes are organized by auto-dated files

Let's say it's December 25th, 2019. If you were to run `notes hello world` it
would create a `2019-12.txt` file in your `NOTES_DIRECTORY` (this is
something you can configure). It would then append `hello world` to the end of
the file.

If you run `notes something else` on the next day it will still append to the
same file and continue appending to that file until the next months hits. For
example, on January 1st 2020 any `notes` commands will append to a
`2020-01.txt` file.

There's other things you can do such as piping input to it, or running the
script without any arguments to open the file in your configured `EDITOR` but
let's first go over installing it before we get to that.

### What is this script not good for?

Depending on how you work, it's probably not ideal for grouping up a bunch of
extended thoughts about a specific topic.

For example, if you were planning to write a book and you spent 3 months
gathering info about what you're writing about then you would end up with a
bunch of isolated date formatted files that was mixed in with everything else.

In those cases, I recommend you make a new script called `book` which basically
does what this script does except it always dumps everything to 1 specific file
of your choosing which isn't dated. That's what I do to help plan my
[video courses](https://nickjanetakis.com/courses/).

## Installation

Copy / paste the line below, or if you don't like this pattern of installing
scripts then feel free to run things manually.

### 1 liner to get `notes` downloaded to `/usr/local/bin`:

```sh
sudo curl \
  -L https://raw.githubusercontent.com/nickjj/notes/master/notes \
  -o /usr/local/bin/notes && sudo chmod +x /usr/local/bin/notes
```

There's no fancy `git clone` instructions because you may end up modifying at
least 1 line of the script. Plus since the script is so simple, this repo is
likely not going to change and if it does you will be able to `diff` it without
any issues.

### Configuration

By default it will use `${HOME}/notes` as your notes directory and if that
directory doesn't exist beforehand, this script will allow you to create it
with a `y/n` prompt when you first run the program.

You can also customize your notes path in 1 of 2 ways:

1. Put `export NOTES_DIRECTORY="/tmp/foo"` in your `~/.profile` or equivalent
file (`/tmp/foo` would be your notes path)
2. Directly edit the `notes` script and replace `${HOME}/notes` with `/tmp/foo`
in the `NOTES_DIRECTORY` variable

Also, if you want this script to open your notes in your code editor you'll
want to make sure you have your `EDITOR` defined in your `~/.profile` too. This
is a Unix standard. For example, mine looks like `export EDITOR="vim"`.

*If you change your `~/.profile`, don't forget to log out / login.*

## Usage Examples

There's 3 ways of using this script:

- `notes something you want to jot down`
  - Appends whatever arguments you add as text into the dated file

- `xclip -o | notes`
  - Pipes and appends anything (in this case your clipboard's contents) into the dated file

- `notes`
  - Opens the dated file in your configured `EDITOR`

That's really all there is to it. With the above 3 ways of adding notes you'll
find yourself adding all sorts of different types of notes with very little
friction. I encourage you to check out [just how short the source
code](https://github.com/nickjj/notes/blob/master/notes) is.

If you wanted to go all out, you could even create custom key binds in your
code editor that would take the selected text and append it to your notes by
running one of the above commands. Since everything is text you have a lot of
flexibility!

Also, you have the power of the command line at your finger tips to manipulate
these files however you see fit. For example you can run `cat 2019-*.txt >
2019.txt` to create a yearly file.

## About the Author

I'm a self taught developer and have been freelancing for the last ~20 years.
You can read about everything I've learned along the way on my site at
[https://nickjanetakis.com](https://nickjanetakis.com/). There's hundreds of
[blog posts](https://nickjanetakis.com/blog/) and a couple of [video
courses](https://nickjanetakis.com/courses/) on web development and deployment
topics. I also have a [podcast](https://runninginproduction.com) where I talk
to folks about running web apps in production.
