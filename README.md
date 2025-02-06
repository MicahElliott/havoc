# Havoc

> Cry 'Havoc,' and let slip the dogs of war
> — _Mark Antony in Act 3, Scene 1 of Shakespeare's Julius Caesar_

This is a very simple set of scripts that create a release suited for
publishing; eg, to Github.

Havoc's `wardoc` discovers commits since your last release and categorizes and
auto-documents them into Markdown that's suitable as a pretty release page.

Havoc's `letslip` creates a release that is uploaded to Github (and others
maybe someday). This presently relies on having [gh](https://cli.github.com/) installed.

## Usage

Generate a "git tag" file, `git-tag-v2025.02.02`:

```
% wardoc
# [v2025.02.02](https://github.com/MicahElliott/captain/releases/tag/v2025.02.02)

**[Full Changelog](https://github.com/MicahElliott/captain/compare/v2025.01.09...v2025.02.02)**

## Fixes
- :bug: Be smarter when invoked in non-git dir (894434f)

## Features
- :sparkles: On failures print more helpful info (e729228)
- :sparkles: Timeout long commands, default 10s (ba03f64)

## Configuration
- :wrench: Improve install docs (ecbb3a6)

---
_This release was created by [havoc](https://github.com/MicahElliott/havoc)_
```

Then open it in `$EDITOR` if you like. You could add a release theme or
summary or whatever.

Create a tag and release, and push it to Github:

```
% letslip git-tag-v2025.02.02

```

## Anti-features

Havoc doesn't try to do anything smart with auto-creating versions according
to [SemVer](https://semver.org/). It presently is only
[CalVer](https://calver.org/) oriented for its simplicity.

## Background

I like the idea of [gitmoji](https://github.com/carloscuesta/gitmoji-cli) but
find it to be overkill (huge, slow, clunky, and too many categories). So Havoc
supports pretty close to a subset, which comprise my opinionated choosing. See
those supported `emojis` in [the source](./templatize) (not worth
re-documenting here).

Havoc also supports your standard categories from [Conventional
Commits](https://www.conventionalcommits.org/en/v1.0.0/#specification), and
from [Gommit](https://github.com/antham/gommit). IOW,
if you're using any semi-standard prefixed commit convention, Havoc aims to
work for you (or should soon enough).

## Other related/helpful tools

Now that you have an officially released project (YAY!), you want people to
easily install (and update!) it. These make that process a one-liner:

- [Pacrat](https://github.com/MicahElliott/pacrat) — A minimal yet flexible
  package manager for a variety of package types and OSs, geared toward
  installing CLI tools
- [Eget](https://github.com/zyedidia/eget) — Easily install prebuilt binaries from GitHub
