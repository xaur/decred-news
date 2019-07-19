# Decred Journal Production Guidelines

## Goals

1. Keep Decred community updated
2. Attract more builders to the project
3. Expose the quality and depth of Decred
4. Convey Decred culture and values

The target audiences can be grouped by the level of engagement (the Decred community, potential builders and everyone else) and by the technical level (high and low).

As a general rule, use less technical language whenever possible. Try to explain complex things in simple terms. At the same time, carefully inject technical goodness for developers, designers and experts in other fields.

Decred is advanced and sophisticated on all levels. Expose this and give a sense of how much is happening.

Community is the greatest asset. Highlight community initiatives (projects, articles) and intelligence (discussions).

## Workflow

On a high level, DJ uses GitHub to coordinate incremental creation of documents.

Lifecycle of a new DJ issue starts with creating a "draft" Git branch named like `draft07`, where `07` stands for July.

In this draft branch, a Markdown file for the new issue is created from a [template](journal-template.md).

Throughout the month DJ authors add notes of the stories that must be covered to the draft file.

Main writing work starts around the last week of the month.

As soon as individual sections are ready, they are submitted for review to people with proper project and domain knowledge:

* Development and People are posted in #dev with notifying people deeply engaged in each project (most commonly project leads)
* Events is posted in #event\_planning
* Outreach, Events and Media are posted in #marketing

Once all sections are finished the whole issue is posted for final review in #writers\_room.

All feedback received is incorporated in the draft.

Finally, the issue is polished and released on Medium, GitHub and other places, and the links are disseminated through various social media channels.

Release steps are captured in greater detail in the [release checklist template](release-checklist-template.md) that is used to generate a checklist for each issue.

See [this issue](https://github.com/xaur/decred-news/issues/65) for a list of areas and their owners.

Setup tips:

* A lot of work can be done with just a browser, thanks to GitHub UI.
* For advanced text editing, comparison and Git operations you will need to setup local software. Get a comfortable text editor with Markdown syntax support, ideally also with Markdown preview and Git support. Some options to try are Atom, Sublime Text, WebStorm. If you find a strong setup please [share](https://github.com/decredcommunity/issues/issues/114) with other writers.
* For comparing revisions use GitHub UI [features](https://help.github.com/en/articles/about-comparing-branches-in-pull-requests), diff tool bundled in your text editor or a standalone tool like [Meld](http://meldmerge.org/).
* By default your email address will be inserted in Git commits and become public. Learn about email privacy [here](https://help.github.com/en/articles/setting-your-commit-email-address) and [here](https://help.github.com/en/articles/blocking-command-line-pushes-that-expose-your-personal-email-address). For the advanced - Git also leaks your machine time zone.

Workflow tips:

* Keep the draft file open. As soon as you see something notable, throw a raw link into the draft. If you are comfortable to write up the story immediately, go for it. Otherwise, add any notes, directions or questions that will help to expand the story later, possibly by other writers. See [TODO](#todos) syntax.
* Push draft notes daily to stay in sync with other authors.
* Before making changes, make sure you're on the latest version.
* Before pushing changes, make sure you based them on the latest version. Use Git rebase otherwise.
* Before doing large changes check with others to avoid conflicts.
* Write up stories sooner when possible to prevent the work piling up.
* Avoid sending too unfinished content for review, this leads to more roundtrips.
* Try to give 2 full days for final review.
* The sooner the DJ issue is released [the better](https://github.com/xaur/decred-news/issues/34).
* Do not edit the issue after it was released, unless there is a very good reason. If that happens, add commits to `master` branch (not the draft branch). Each released version must have a corresponding `master` commit.
* If you get stuck with Git, check the [Git Book](https://git-scm.com/book) or ask in #git\_help (ask for invite).

### Updating index

There are two files that track all DJ issues and their translations. `index.md` contains _primary_ locations of documents, while `mirrors.md` tracks _all_ known locations where the issues or their translations are mirrored.

To avoid commit churn on `master`, changes to these files are merged in batches around 1-3 times a month:

* create new branch e.g. `index07` (`07` for July)
* for the initial English version:
  * add GitHub Pages link to `index.md`
  * add GitHub Pages, Medium and decredcommunity links to `mirros.md`
* add all new known translations to `index.md` and `mirrors.md` accordingly
* push the branch, open a PR against `master`
* share the links to previews of index and mirrors in #writers\_room, ask translators to submit any missed translations
* collect submissions for several days
* add a single combined commit to `master` and `gh-pages`

## Collecting content

### General

* Linked pages must be in English in most cases.
* Non-English links are allowed but they must be significant in some way, e.g. original research or ratings.
* Archive all linked pages in [web.archive.org](https://web.archive.org/) or [archive.today](https://archive.today/).
* To check if something was reported in previous issues, search the .md files, e.g. `grep -ir dcrwallet/pull/1330` shows that this pull request was covered in Nov 2018. Another way is to use the search box [on GitHub](https://github.com/xaur/decred-news).
* All claims must reference sources.
* Stick to facts, minimize opinions and assumptions.
* Focus on what was **done**. Announcements and plans are good too - just be specific and minimize hype.
* All work is important, the challenge is how to not kill the reader and balance between bird's eye and the details, which are often interesting.
* DJ issues are huge and many stories require understanding a fair bit of historical context and domain expertise. It comes with time.

### TODOs

"TODOs" or "FIXMEs" are small tasks and notes embedded in the draft document.

Two types of TODOs are used in DJ.

First type is anything `{inside curly braces}`. It can be a task, a placeholder, a question or a note. Tasks need to be done while notes can be just removed when they are no longer needed. Examples:

Task:

> UTXO set optimization was merged {explain in plain English}

Question:

> 3 typos have been fixed {do we need this?}

Placeholders that must be filled:

> In {month} the Treasury received {n} DCR and spent {n} DCR.

Special case of placeholder is an empty TODO, it must be obvious from the context what it should be replaced with:

> Reddit subscribers: {} (+{})

Second type of TODOs are "hanging" URLs not wrapped in Markdown links. For example, a hanging URL in Relevant External simply means "write up this story".

Final release must have all TODOs resolved, i.e. contain no curly braces and no URLs outside of Markdown links.

### Development

Per the [Goals](#goals), this section aims to update technical and less technical community members, attract more builders and expose the solid progress to everyone else. Development is perhaps the most challenging in this regard for the constant need to balance between these audiences and switch between zooming in and zooming out.

A side goal is to educate people about the real effort needed to build robust cryptocurrency software.

There are two target subgroups of devs:

1. devs that already work for Decred - to them we give the big picture so if they see something interesting they can follow and discover new opportunities (interest often makes for the best performance)
2. devs who do not yet work on Decred - for them we show why Decred is a good place. For example, any effort to cut bloat, keep the stack up to date (no [horrific](http://catb.org/jargon/html/C/cthulhic.html) legacy tentacles), to improve privacy or in general do something elegantly would attract me personally (@bee).

Where do we look for updates:

* [Decred project](https://github.com/decred) repos
* corporate contractors repos, e.g. [Raedah Group](https://github.com/raedahgroup)
* individual developers repos, e.g. [matheusd](https://github.com/matheusd)
* scan dev chats (optional)
* ask the devs. The more updates we get directly from them, the better.

What do we look for:

* release notes
* pull requests
* commits
* interesting conversations

Stages of work lifecycle considered for reporting:

* work released in binaries or deployed to production sites
* work released in source code (merged in master branches)
* work finished but still in review
* work in progress (new work done this month)
* work started
* discussion started
* planned work, from near to long term

In each project section, order work items from "most released" to "least released".

The same effort may be reported multiple times in multiple DJ issues as it moves to next stage. Reporting after merge tells developers and enthusiasts new feature is available on master so they can build from source. Reporting after release tells everybody else the new feature is available in the binaries.

All updates must be **notable** in some way.

The most notable event is the release of new software version. These don't happen every month, so most of the time we report changes in source code that happen in pull requests (PRs) or commits.

Signs of a _not_ notable pull request or commit: few lines changed, no description, no discussion, not many people involved, no references from or to this PR, short time span, few commits, not much happened during the month.

Some work sounds less "exciting": small bugfixes, increased test coverage, code refactoring, dependency upgrades, code cleanup, etc. Normally, such items are not reported on their own but grouped in a general statement like "increased test coverage", unless the total amount is so small that can be omitted. These items do get a standalone mention when they are big (thousands of lines affected in non trivial way), took a ton of effort (e.g. hunting down a super tricky bug), have huge impact (e.g. vulnerability fix) or are otherwise interesting (e.g. someone went on a crusade to [remove jQuery](https://github.com/decred/dcrdata/pull/915) or remove a bad practice like [inline JS](https://github.com/decred/dcrdata/pull/873)). Infrastructure upgrades like linters, CI, vulnerability detection, etc, are often notable.

Try to be specific when using catch-all phrases, e.g. "refactoring to increase separation of concerns" instead of just "refactoring".

While things like "tests added" may sound too generic, they are often mentioned to give a general sense that infra work never stops and that takes a lot of effort. Indirectly, it shows that our devs are experienced and know "the price" of a large codebase - if you don't consistently take care of it and just keep adding features it may blow up.

Special category we try to mention is changes backported from other Go codebases like btcd or lnd. Indirectly, it shows returns from past contributions in the space - seeds planted years ago by C0 by investing into btcsuite.

Don't worry if a project is short on updates. There are many projects and sometimes devs move their focus.

To find **pull requests** for the month:

1. Use GitHub search features, notably the `updated:2019-06-01..2019-06-30` query to find pull requests that were active in a given month ([example](https://github.com/decred/politeia/pulls?q=is%3Apr+is%3Aclosed+updated%3A2019-06-01..2019-06-30)). Merged ones are in the Closed tab with a purple icon. In progress ones are in the Open tab.
2. For each PR in that "updated" list, check that some notable activity happened in a given month. The are false positives. Some activity like deletion of feature branches may paint the PR as updated while nothing of interest happened. Example: [politeia#833](https://github.com/decred/politeia/pull/833) - work was merged on May 1, branch deleted on Jun 20 and the PR shows up as updated in the June search query above.

Some projects may have commits that don't go the pull request route. For these, we scan **commits** on the `master` branches.

To find commits:

1. Open the master branch (e.g. [politeia](https://github.com/decred/politeia/commits/master)).
2. Scan month's commits.
3. If a commit links to its corresponding pull request, check that PR too for more context.

**Chats** may provide additional context for changes and interesting (sometimes notable) discussions. Scanning chats is optional because it may take a lot of time. Dev chat rooms: #dev, #politeia, #dcrdata, #lndev, #documentation, #design.

For dev **stats**, there is a convenient GitHub filter for calculating developers per repository ([example](https://github.com/decred/dcrd/graphs/contributors?from=2019-06-01&to=2019-07-01&type=c)).

GitHub can be used to calculate how many people contributed to the repo during the month:

* Find IDs of last commit in previous month and last commit in current month
* Construct GitHub compare link, e.g.: https://github.com/decred/dcrd/compare/70c14042...5048959f (8 first characters of commit IDs would do, also mind the 3 dots `...`)
* Look at the contributors count

### People

Main goals of People are:

1. Greet new contributors, both individuals and organizations
2. Make the community more familiar with people making Decred

The latter includes interviews and staff changes.

### Governance

Goal: provide a digest of decision-making activity and finances.

Finances include income and expenses in DCR and USD. When more finance info is available for reporting we may split this into a separate Treasury section, per the [content plan](content.md).

Sources:

* [Politeia](https://proposals.decred.org/) activity, [@pi_crumbs](https://twitter.com/pi_crumbs), [@slices_of_pi](https://twitter.com/slices_of_pi)
* [Politeia Digest](https://medium.com/politeia-digest)
* some [r/decred](https://www.reddit.com/r/decred/) discussions
* chats: #governance, #proposals

### Network

The main goal of Network is to keep people's eyes on network health indicators such as hashrate, locked DCR amount and percentage, count of nodes, node version distribution. Any notable incidents go here too.

Network, Mining and Integrations together cover the infrastructure area.

Stats and metrics websites:

* [dcrdata.org](https://explorer.dcrdata.org/)
* [charts.dcr.farm](https://charts.dcr.farm/)
* [dcrstats.com](https://dcrstats.com/)
* [dcr-data.netlify.com](https://dcr-data.netlify.com/)

Chats: #pow-mining, #pos-voting

### Mining

Mining used to cover the mining space: new miner units and their stats, new PoW pools and updates from existing ones, relevant news about colocation, sellers, energy, cooling, etc.

Recent issues of DJ have this section omitted because the first phase of Blake mining arms race is over, there are no big news and we simply don't have journalists tracking this space. [Contributions](contribute.md) are welcome.

### Integrations

In contrast with Network that is about "raw" infrastructure and health indicators, Integrations is about services expanding Decred infrastructure, most commonly businesses.

Besides just listing new exchanges, wallets and payment processors, dig key/interesting features and events about them.

For example,

> Decred [is live](https://twitter.com/roomofsatoshi/status/1052879109099991041) on [Living Room of Satoshi](https://www.livingroomofsatoshi.com/). It allows one to pay any bill or to pay money into any Australian bank account with Decred. Established in 2014, the service helped to pay over 140,000 bills.

or

> [BitPro](https://bitpro.cc/) payment gateway added Decred and [posted](https://www.reddit.com/r/decred/comments/8og4he/bitpro_payment_gateway_adds_decred/) on Reddit. Notably, it is fully functional without javascript or cookies and does not ask for name or email, among other [features](https://bitpro.cc/start).

### Adoption

The line between Integrations and Adoption is blurry, but the guiding rule is: Integrations is aboud _building_ out Decred infrastructure, while Adoption is about _using_ Decred infrastructure. In other words, Adoption is about simply using DCR and building new products and services on top of Decred infrastructure.

Stories must have something to do with Decred blockchain, for example:

* new merchants accept DCR
* project or organization uses dcrtime or Politeia

Dig interesting facts similar to Integrations.

### Outreach

Provide overview of outreach/communications/marketing activity for past month and any plans.

Logically, Events and Media sections belong to Outreach.

Chats: #marketing, #event\_planning, #social\_media

### Events

Cover past and upcoming physical and web events where Decred had presence.

For each past event, add some basic info following the standard format in the template. On top of that, try to add the most interesting highlights (1-3 sentence per event). Same for upcoming events.

If info is missing for some events closer to the release, actively post a list of such events in #event\_planning and ask for info.

Look at the events from Decred's perspective, look for experience to learn from. Some hints: how it went, how many people, what they know, what they don't know, what they think about Decred, any interesting trends that could shape our events activity.

Sources:

* Some events have reports written up in the [events repo](https://github.com/decredcommunity/events) - you can subscribe to it to watch for updates.
* Chats: #event\_planning
* Follow Twitter accounts that often tweet about events, e.g. [Decred_ES](https://twitter.com/Decred_ES).

### Media

Cover the best Decred-related content posted in the media.

Ratings go here too.

Criteria for "Selected articles" is an [open question](https://github.com/xaur/decred-news/issues/21).

Current informal criteria: something you would recommend reading to a wide audience, something we don't know or a fresh look at something we know, any original research, content from community members, something that took more than 2 hours to write.

For each selected article, optionally add a small note why it is great.

### Community Discussions

Goals:

1. Track community growth
2. Update about communications infrastructure (critical for online communities)
3. Track interesting conversations on social media

Sources:

* Reddit
  * watch [r/decred](https://www.reddit.com/r/decred/)
  * use Reddit's follow/friend features to follow prominent posters
* Twitter
  * [@decredproject](https://twitter.com/decredproject)
  * prominent users, e.g. [@lukebp_](https://twitter.com/lukebp_), [NoahPierau](https://twitter.com/NoahPierau), [RichardRed0x](https://twitter.com/RichardRed0x), etc
  * mentions of [@decredproject](https://twitter.com/search?q=%40decredproject), [$DCR](https://twitter.com/search?q=%24DCR), etc
  * hashtags [#Decred](https://twitter.com/hashtag/Decred), [#DecredChallenge](https://twitter.com/hashtag/DecredChallenge), etc

### Markets

Report any interesting market movements, and ideally, action in markets not frequently covered by the media - OTC and DEX.

Mention both USD and BTC price:

* USD price shows how Decred competes against fiat and the collective purchasing power of DCR holders (including the Treasury)
* BTC price shows how Decred competes against Bitcoin, another SoV+MoE focused cryptocurrency with similar properties

Do not speculate about the price.

Chats: #trading.

### Relevant External

The ideas behind this section:

1. Show that many good decisions were put into the foundation of Decred, that many problems were predicted and prevented years ago
2. Learn from experience of other projects
3. Track interesting trends, detect risks
4. Educate the audience about things that have big influence on Decred: cryptocurrency tech, governance, computer security, regulations.

Topics commonly covered here:

* PoW, ASIC resistance
* Security of cryptocurrency networks (double spends and other attacks)
* Cryptocurrency tech
* Governance, funding, chain forks, community forks, and the controversy that often surrounds these
* DEX
* Exchanges and other services
* Regulations
* Computer security
* Fun stuff

### Missed content

Some notable stories are discovered in later months. Add them, followed by a tag in italics: `_(missed in March issue)_`.

### Title image

Title image used on GitHub Pages must be 768x384 pixels.

Try to fit it into 100-200 KiB to save space, e.g. by saving as JPEG with 98% quality. Motivation: Git repositories keep all versions of all files ever committed, therefore they quickly grow in size when adding binary files like images.

For caption, at the minimum add the title of the work and its author, e.g. `Image: Anomaly by @saneder`.

So far DJ images are abstract art. If possible, add extra text hinting at what is pictured. The text must either make sense or be abstract enough to not need it, but not something in between.

## Style, Editing

### General

Look into these:

* Save reader's time: keep the most important bits for each story and a link to follow.
* Avoid hype and fake excitement.
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

### How to give credit

When to add credit to an accomplishment is an [open question](https://github.com/xaur/decred-news/issues/26).

There is no formal criteria at the moment. A lot of work is done each month. Adding credit to everything would overwhelm the reader. On the other hand, sometimes it feels right to give someone a shoutout. Use your best judgement.

When giving credit to multiple people sort the names alphabetically:

> Thing X is released, credits to @alex, @maria and @sam

Speaking of the credits for DJ production at the end of the issue, make sure to add everyone who contributed. There is no formal criteria at the moment. The informal criteria is: add people who _actively_ brought us something, opposed to content that DJ authors find and incorporate.

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
* For small numbers use as few decimal places as necessary to reduce noise, but enough to retain context. Example: for the percentage of locked DCR we use two decimal places because the fluctuations are small and because a lot of money is behind this number.
* Stick to ASCII character set, except the title and names. Modern renderers like GitHub Pages or Medium take care of it and properly render dashes, quotes, etc.
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

* all content can be easily downloaded and synced (nearly decentralized storage)
* all changes recorded
* get more contributions in a proven workflow
* integrity protection
* devs can seamlessly engage/contribute since the workflow is similar to theirs
* show off: one of the most advanced productions in the space
* possible authenticity protection via PGP signatures (requires extra setup)
* Git software is widespread
* Cloning is permissionless and does not require an account

Cons:

* higher learning curve, except most trivial usage
* conflict resolution is not automatic and is error prone
* requires experienced Git maintainer to have a pretty repository

## Why curly braces?

* They do not conflict with Markdown syntax that uses square brackets and parens for links: `[click here](http://example.com)`.
* They do not conflict with HTML syntax that uses angle brackets for tags: `<img>`. Markdown allows embedding HTML.
* They can be easily found and counted to estimate how much work is left.
* They can be highlighted in various text editors.
* They can sit between words (aka "inline"). In contrast with typical TODO syntax in programming languages, where a TODO must be on its own separate line.
