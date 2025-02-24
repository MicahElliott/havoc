# Havoc

> Cry 'Havoc,' and let slip the dogs of war
> — _Mark Antony in Act 3, Scene 1 of Shakespeare's Julius Caesar_

Check out Havoc's [Releases
page](https://github.com/MicahElliott/havoc/releases) (also on right sidebar)
for examples of what it does!

This is a very simple couple of scripts that create a documented "Release"
suited for publishing; eg, to Github. Any executable script(s)/binarie(s) can
become something that is a "releasable package" with documentation and a
predictable set of artifacts. Then your users can quickly discover, download,
and run your work with minimal effort.

One of Havoc's goals is to **make releases consistent**. If you browse across
various projects' _Release_ pages, you won't see two that are alike!

Havoc's `wardoc` (invoked implicitly) discovers commits since your last
release and categorizes and auto-documents them into Markdown that's suitable
as a pretty release page (that passes
[markdownlint](https://github.com/markdownlint/markdownlint) if you care).

Havoc's eponymous main script (which is all you need to invoke) creates a
release that is uploaded to Github (and others maybe someday).

## Dependencies

Havoc should run fine on **any Linux or Mac or WSL**.

- Uploading presently relies on having **[gh](https://cli.github.com/) (the
  Github CLI)** installed.

- [OPTIONAL] Generating a summary relies on **[llm cli](https://github.com/simonw/llm)**.

- [OPTIONAL] If you have [bat](https://github.com/sharkdp/bat) installed, you
  will see a nicer local display of the generated doc.

## Install

If you use [eget](https://github.com/zyedidia/eget) (highly recommended!),
simply run: `eget micahelliott/havoc`. Othewise, you can download `havoc` and
`wardoc` from [bin/](./bin) to somewhere on your `$PATH`.

## Usage

Havoc wants a little structure: releasable scripts and binaries in `bin/`, and
a directory `releases/` for it to create releases and docs. So if you haven't
already:

```
mkdir bin releases; mv MYRUNNABLES bin
```

You may want to add `releases/` to `.gitignore` since it will end up with a
bunch of tarballs. Which is kinda the point of having a separate dir for this.
Or something like [git-lfs](https://github.com/git-lfs/git-lfs) could be used.

Generate a "git release doc/tag" file, `releases/v2025.02.02.md`, and release
tarball:

```
% havoc
Creating artifact of runnable tools in bin dir: releases/havoc-v2025.02.06.tgz
./
./havoc
./wardoc

Will create and push git tag: v2025.02.06
Proceed? [y/n] y
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To github.com:MicahElliott/havoc.git
 * [new tag]         v2025.02.06 -> v2025.02.06
Created release doc ‘releases/v2025.02.06.md’
Edit? [y/n] n
Creating a new release on github
https://github.com/MicahElliott/havoc/releases/tag/v2025.02.06
```

The (editable) Markdown file looks something like this:

```
**[Full Changelog](https://github.com/MicahElliott/captain/compare/v2025.01.09...v2025.02.02)**

## Fixes

- :bug: Be smarter when invoked in non-git dir (894434f)

## Features

- :sparkles: On failures print more helpful info (e729228)
- :sparkles: Timeout long commands, default 10s (ba03f64)

## Configuration

- :wrench: Improve install docs (ecbb3a6)

---
_This release was created with [havoc](https://github.com/MicahElliott/havoc)._
```

## Advanced usage (optional)

### Frequent releases

If you need to release multiple times on a given day, you can pass an arg to
Havoc indicating an additional suffix. This is also useful for creating a
`-alpha` or `-beta` or some such label.

### LLM summaries

LLMs are well suited to the task of summarizing commits. Havoc supports such
automatic generation. It uses `llm`, so you have to configure it if you want
to use this feature. With this option, a "Summary" is added to the top of the
categorized commit listing. It is based on full commit bodies, not just
subject line.

### Generated SHA for verification

Along with the release archive tarball, a similarly named file with a
`.sha256` suffix is generated. This can be inspected manually, or can be used
automatically by `eget` (see below).

### Configuration

You can change the format of each commit that is shown in the bulleted lists
in the release doc. Eg, if you wanted to also see dates (`%aI`) and author
names (`%an`) use the env var:

```
% HAVOC_COMMIT_FORMAT='%aI %s (%h) <%an>' havoc
```

## Anti-features

Havoc doesn't try to do anything smart with auto-creating versions according
to [SemVer](https://semver.org/). It presently is only
[CalVer](https://calver.org/) oriented for its simplicity.

It also does not do a release for you. It's up to you to get binaries onto
machines, run migrations, etc.

## Background

I like the idea of [gitmoji](https://github.com/carloscuesta/gitmoji-cli) but
find its CLI to be overkill (huge, slow, clunky, and too many categories). So Havoc
supports pretty close to a subset, which comprise my opinionated choosing. See
those supported `emojis` in [the source](./bin/wardoc) (not worth re-documenting
here).

I realize that `gh` is able to do a lot of what Havoc does. But Havoc supports
a more flexible workflow, not requiring PRs for everything, and not requiring
SemVer.

Havoc also supports your standard categories from [Conventional
Commits](https://www.conventionalcommits.org/en/v1.0.0/#specification), and
from [Gommit](https://github.com/antham/gommit). IOW, if you're using any
semi-standard prefixed commit convention, Havoc aims to work for you (or
should soon enough).

## Other related/helpful tools

Now that you have an officially released project (YAY!), you want people to
easily install (and update!) it. These minimal tools play nice with Havoc and
make that process very simple:

- [Pacrat](https://github.com/MicahElliott/pacrat) — A minimal yet flexible
  package manager for a variety of package types and OSs, geared toward
  installing CLI tools
- [Eget](https://github.com/zyedidia/eget) — Easily install prebuilt binaries from GitHub

### Fancy alternatives

I considered using [git-cliff](https://github.com/orhun/git-cliff) but ...
