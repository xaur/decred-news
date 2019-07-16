# Decred Journal Production Guidelines

## Goals

1. Show the depth of Decred. Decred is advanced and sophisticated on all levels. Expose this, give a sense of how much is happening.
2. Community is greatest asset. Highlight community initiatives (projects, articles) and intelligence (discussions).

Target audience is twofold:

* less technical: current and potential Decred users, investors and the world - most of the text must read well for these
* more technical: developers, designers and experts in other domains - carefuly inject some goodness for these groups

## Workflow

Lifecycle of a new Decred Journal (DJ) issue starts from creating a "draft" Git branch named like `draft07`, where `07` stands for July.

In this draft branch, a Markdown file for the new issue is created from a [template](https://github.com/xaur/decred-news/blob/docs/journal-template.md).

Throughout the month DJ authors add notes to the draft file.

Main writing work starts somewhere in last week of the month.

Somewhere around 3rd-5th of the next month some sections are posted for review by their corresponding domains.

Soon after that the whole issue is posted for final review in #writers\_room.

Finally, the issues is polished and released on Medium, GitHub and other places, and the links are disseminated through various social media channels.

See [release checklist](https://github.com/xaur/decred-news/blob/docs/release-checklist-template.md).

Tips:

* Have the text file open, throw raw links into the draft as soon as you see something notable.
* Push draft notes daily to stay in sync with other authors.
* Before making changes, make sure you're on the latest version.
* Before pushing commits, make sure you're on the latest version. Rebase otherwise.
* Before doing large changes check with others to avoid conflicts.
* Avoid sending unfinished document for review, this leads to several roundtrips.
* Try to give 2 full days for final review.
* Do not edit the issue after it was released, unless there is a very good reason. If that happens, add commits to `master` branch. Each published version must have a corresponding `master` commit.

### Updating index

* create new branch e.g. `index07` (`07` means July)
* add GitHub Pages link to `index.md`
* add GitHub Pages, Medium and decredcommunity links to `mirros.md`
* push the branch, open a PR against `master`
* notify translators in #writers\_room to submit any missed translations, share a preview link and PR link
* collect submissions for a few days
* add a single combined commit to `master` and `gh-pages`

## Collecting content

### General

* Linked pages must be in English in most cases.
* Non-English links are allowed but they must be significant in some way, e.g. original research or ratings.
* Archive all linked pages in web.archive.org or archive.today.
* To check if something was reported in previous issues, do a full text search in .md files, e.g. `grep -ir dcrwallet/pull/1330` shows that this pull request was covered in Nov 2018.
* All claims must reference sources.
* Stick to facts, minimize opinion and assumptions.
* Highlight achievements of our community.
* Focus on what was **done**.
* Announcements and plans are good too - just be specific and minimize hype.

### Development

Where do we look for updates:

* [Decred project](https://github.com/decred) repos
* corporate contractors repos, e.g. [Raedah Group](https://github.com/raedahgroup)
* individual developers repos, e.g. [matheusd](https://github.com/matheusd)
* scan dev chats (optional)
* ask the devs

What do we look for:

* pull requests
* commits
* interesting conversations

Stages in work lifecycle considered for reporting:

* work released in binaries or deployed to production sites
* work released in source code (merged in master branches)
* work finished but still in review
* work in progress (some work happened this month)
* work started
* discussion started
* planned work, from near to long term

The same work may be reported multiple times in multiple DJ issues as it moves to next stage.

Reporting after merge tells developers and enthusiasts new feature is available on master so they can build from source. Reporting after release tells everybody else the new feature is available in the binaries.

Within each project section, order work items from "most released" to "least released".

All updates must be **notable**. Signs of a _not_ notable pull request or commit: few lines changed, no description, no discussion, not many people involved, no references from or to this PR, short time span, few commits, not much happened during the month.

The primary source of updates for most Decred projects are the **pull requests** (PRs), currently hosted on GitHub.

To find PRs for the month:

1. Use GitHub search features, notably the `updated:2019-06-01..2019-06-30` query to find pull requests that were active in a given month ([example](https://github.com/decred/politeia/pulls?q=is%3Apr+is%3Aclosed+updated%3A2019-06-01..2019-06-30)). Merged ones are in the Closed tab with a purple icon. In progress ones are in the Open tab.
2. For each PR in that "updated" list, check that some notable activity happened in a given month. The are false positives. Some activity like deletion of feature branches may paint the PR as updated while nothing of interest happened. Example: [politeia#833](https://github.com/decred/politeia/pull/833) - work was merged on May 1, branch deleted on Jun 20 and the PR shows up as updated in the June search query above.

Some projects may have commits that don't go the pull request route. For these, we scan **commits** on the `master` branches.

To find commits:

1. Open the master branch (e.g. [politeia](https://github.com/decred/politeia/commits/master)).
2. Scan month's commits.
3. If a commit links to its corresponding pull request, check that PR too for more context.

**Chats** may provide additional context for changes and interesting (sometimes notable) discussions. Scanning chats is optional because it may take a lot of time. Dev chat rooms: #dev, #politeia, #dcrdata, #lndev, #documentation, #design.

For dev **stats**, there is a convenient GitHub filter for calculating developers per repository ([example](https://github.com/decred/dcrd/graphs/contributors?from=2019-06-01&to=2019-07-01&type=c))

### Governance

Sources:

* [Politeia](https://proposals.decred.org/) activity, [@pi_crumbs](https://twitter.com/pi_crumbs), [@slices_of_pi](https://twitter.com/slices_of_pi)
* [Politeia Digest](https://medium.com/politeia-digest)
* some [r/decred](https://www.reddit.com/r/decred/) discussions
* chats: #governance, #proposals

### Network

Stats and metrics websites:

* [dcrdata.org](https://explorer.dcrdata.org/)
* [charts.dcr.farm](https://charts.dcr.farm/)
* [dcrstats.com](https://dcrstats.com/)
* [dcr-data.netlify.com](https://dcr-data.netlify.com/)

Chats: #pow-mining, #pos-voting

### Integrations

Besides just listing new exchanges, wallets and payment processors, try digging key/interesting features/events about them.

### Adoption

The line between Integrations and Adoption is blurry, but the guiding rule is: Integrations is aboud _building_ our Decred infrastructure, while Adoption is about _using_ Decred infrastructure. 

Stories must have something to do with Decred blockchain, for example:

* new merchants accept DCR
* project or organization uses dcrtime or Politeia

### Outreach

Chats: #marketing, #event\_planning, #social\_media

### Events

Chats: #event\_planning.

For each past event, add some basic info following the standard format in the template. On top of that, try to add the most interesting highlights (1-3 sentence per event). Same for upcoming events.

### Media

Criteria for "Selected articles" is an [open question](https://github.com/xaur/decred-news/issues/21).

Current informal criteria: something you would recommend reading to a wide audience, something we don't know or a fresh look at something we know, any original research, content from community members, something that took more than 2 hours to write.

### Community Discussions

Report any interesting conversations.

* Reddit
  * watch [r/decred](https://www.reddit.com/r/decred/)
  * use Reddit's follow/friend features to follow prominent posters
* Twitter
  * [@decredproject](https://twitter.com/decredproject)
  * prominent users, e.g. [@lukebp_](https://twitter.com/lukebp_), [NoahPierau](https://twitter.com/NoahPierau), [RichardRed0x](https://twitter.com/RichardRed0x), etc
  * mentions of [@decredproject](https://twitter.com/search?q=%40decredproject), [$DCR](https://twitter.com/search?q=%24DCR), etc
  * hashtags [#Decred](https://twitter.com/hashtag/Decred), [#DecredChallenge](https://twitter.com/hashtag/DecredChallenge), etc

### Missed content

Some notable stories are discovered in later months. Add them, followed by a tag in italics: `_(missed in March issue)_`.

## Style, Editing

### General

Verify:

* No factual errors
* Attitude: check that nothing damages Decred's public image
* Grammar, punctuation, wording, tense consistency, sentence and paragraph composition
* Make the language less boring
* Proportion: check that more important stories get more space, and the other way round
* Order of content
* Remove empty sections (e.g. no news for Mining)

### Order of reporting work

For any work reported, order the items from "most released" to "least released". See [Development](#development) for an example.

### How to identify people

This is an [open question](https://github.com/xaur/decred-news/issues/20).

The current approach is subjective and informal: use the most well known handle to identify Decred community members, full names or handles for everyone else.

### How to credit people

When to add credit to an accomplishment is an [open question](https://github.com/xaur/decred-news/issues/26).

There is no formal criteria at the moment. A lot of work is done each month. Adding credit to everything would overwhelm the reader. On the other hand, sometimes it feels right to give someone a shoutout. Use your best judgement.

When giving credit to multiple people sort the names alphabetically:

> Thing X is released, credits to @alex, @maria and @sam

Speaking of the Credits sections at the end of the issue, make sure to note everyone who contributed.

### Quotes

Try to follow the standard format: `quoted text (source)`.

Example formats:

```
> Quoted tweet ([@handle](tweet link))

> Quoted chat message (@handle in [chat](matrix link))

> Quoted chat message with room specified, where it matters (@handle in [#room](matrix link))

> Quoted article (@handle in [article title](article link))

> Quoted text where type of source does not matter ([@handle](arbitrary link))
```

### Link text

Put links on 1-3 words. Avoid too short link text (hard to click) and too long link text (visual noise). Examples:

* "feature X [is](link) now available": bad, too short, hard to click
* "[feature X is now available](link)": bad, too long, visual noise
* "[feature X](link) is now available": good balance

### Use canonical links without tracking

1. Ensure URLs are [canonical](https://en.wikipedia.org/wiki/Canonical_link_element). This implies using www.reddit.com over old.reddit.com. On most pages canonical link can be found in `<link rel="canonical" href="..."/>` in the page source.

2. Remove any tracking parameters like Medium's `gi=...`, Google Analytics `utm_...`, etc. As a general rule, remove any URL parameters that don't break the link.

**Examples**

Non-canonical URLs with junk parameters:

https://www.youtube.com/watch?v=3RGoUQK0g24&feature=share

https://youtu.be/3RGoUQK0g24

Good URL: https://www.youtube.com/watch?v=3RGoUQK0g24

Forbes tracking (remove the `#425f36a11067`):

https://www.forbes.com/sites/kenrapoza/2019/06/20/facebooks-libra-coin-is-both-vampire-project-and-regulatory-nightmare/#425f36a11067

Medium tracking (remove the `?gi=68a95d076f04`):

https://hackernoon.com/decred-wants-you-be-one-of-the-first-to-test-the-dcr-lightning-network-dd9ecf14d95e?gi=68a95d076f04

### Matrix links

For links to messages always use Matrix links, specifically matrix.to links (don't use riot.im links).

For links to files that were uploaded to Matrix, don't link to file directly. Instead, link to (relevant) message that uploaded it. It is trivial to open the message and download the file, but it is not trivial to find the message by the direct file link.

### Markdown

Use backslash `\` to escape underscore `_` so it won't be treated as italics. Example: `under\_score`.

Avoid Markdown features that are problematic in the Medium version:

* Paragraphs and blockquotes inside list items
* Nested lists

https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#lists

### Typography

This applies to English only:

* Use simple word forms when possible.
* For large numbers always use either uppercase `K/M/G` or full `thousand/millions/billions`, e.g. `$53K`.
* Stick to ASCII character set, except the title and names. Modern renderers like GitHub Pages or Medium take care of it, and properly render dashes, quotes, etc.
  * Use ` - ` (space, hyphen, space) to separate parts of sentences where you would use emdash.
  * Use hyphen for number ranges where you would use endash.
  * Use `'` for single and `"` for double quotes.
  * The exception is names, e.g. `Permabull Niño`
* For dates use short month format without `th`: `Jan 7`, `Feb 15` and so on. In dev speak, the format is `MMM D`.
* Use proper [title case](https://en.wikipedia.org/wiki/Letter_case) for Selected articles, even when original title is not in proper case.

### Linting

* Remove non-ASCII characters (except the main title and names).
* Remove double space, trailing space, more than 2 subsequent newlines
* Add any missing newlines around headings and bullet lists.
* Remove `?via` from matrix.to links
* Remove tracking parameters from URLs

## Reviewing

Take a note of the Git revision you review. If the file changes after your review, only the difference needs to be re-reviewed. This difference can be seen by constructing a diff link:

https://github.com/xaur/decred-news/compare/5df8b0f2...draft06

where `5df8b0f2` is a 8-character Git revision and `draft06` is the name of the branch. Reads like "show me the changes since 5df8b0f2 until the latest draft06".

## Translations

1\. Check the [index](https://xaur.github.io/decred-news/) to see if translation to your language already exists. If it does exist but you don't like it, feel free to submit improvements. If that fails somehow, nobody stops you from creating your own translation.

2\. Ideally, wait for the document you wish to translate to be fully finished and released.

3\. Before you start translating, make note of the Git branch and revision that you translate. It will be useful later to track changes to the source document.

4\. Add people who worked on the translation to the separate credits line at the bottom

> Credits (alphabetical order): a, b, c
> 
> Translated by: x, y, z

5\. Note whether the translation is full or partial. If partial, note what was covered or what was omitted. The best places for such note are start or end of the document.

6\. When finished, submit your translation for listing on the [index](https://xaur.github.io/decred-news/) and [mirrors](https://xaur.github.io/decred-news/mirrors.html) pages. Either create a [pull request](https://github.com/xaur/decred-news/pulls), or create an [issue](https://github.com/xaur/decred-news/issues) or let us know in [#writers\_room](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org).

7\. Consider mirroring your translations in a GitHub repository. This will allow easy replication, thus hardening censorship resistance. For example, see [Arabic](https://github.com/Insaf01/decred-journal-ar) or [Chinese](https://github.com/Guang168/DecredCNJournal) repos.

8\. Coordinate with writers and other translators in [#writers\_room](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org). Share your experiences: how long the translation took to make, how big is your audience, what do they find more or less valuable to translate.

## Why Git?

Pros of the Git/GitHub workflow:

* all content can be easily downloaded and synced
* all changes recorded
* get more contributions in a proven workflow
* integrity protection
* devs can seamlessly engage/contribute since the workflow is similar to theirs
* show off: one of the most advanced productions in the space
* possible authenticity protection via PGP signatures (requires extra setup)

Cons:

* higher learning curve, except most trivial usage
* conflict resolution is not automatic and is error prone
* requires experienced Git maintainer to have a pretty repository
