# Decred Journal Production Guidelines

## Goals

1. Keep Decred community updated
2. Attract more builders to the project
3. Expose the quality and depth of Decred
4. Convey Decred culture and values

The target audiences can be grouped by the level of engagement (the Decred community, potential builders, everyone else) and by the technical level (high, low).

As a general rule, use less technical language whenever possible. Try to explain complex things in simple terms. At the same time, carefully inject technical goodness for developers, designers and experts in other fields.

Decred is advanced and sophisticated on all levels. Expose this and give a sense of how much is happening.

Community is the greatest asset. Highlight community initiatives (projects, articles) and intelligence (discussions).

For direct voting system like Decred, accurate information is critical for making good decisions.

## Workflow

On a high level, DJ uses Git and GitHub to coordinate the creation of documents.

Life cycle of a new DJ issue starts with creating a draft file from a [template](journal-template.md).

To keep everyone updated on release progress, a GitHub pull request is created from a [template](release-checklist-template.md) with a detailed checklist ([example](https://github.com/xaur/decred-news/pull/165)).

Throughout the month DJ authors add notes of the stories that must be covered to the draft file.

Main writing work starts around the last week of the month.

As soon as individual sections are ready, they are submitted for review to people with relevant project and domain knowledge:

- Development and People are posted in #dev with notifying people deeply engaged in each project (most commonly project leads)
- Events is posted in #events
- Outreach, Events and Media are posted in #marketing

Once all sections are finished the whole issue is posted for final review in the #writers room.

All feedback received is incorporated in the draft.

Finally, the issue is polished and released on Medium, GitHub and other places, and the links are disseminated through various social media channels.

See [here](https://github.com/xaur/decred-news/issues/65) for a list of sections and their owners.

### Git workflow

Summary: Each document is developed in its own "draft branch". When finished, only a single commit is added to `master`. Draft history is then archived in a special location.

Design goals of this workflows:

1. Remove drafting churn from the `master` branch.

   - Most users of the repo won't need draft commits after the doc has been published.
   - Keeping draft commits separately also allows archivists to fetch only the `master` branch to save time and space.

2. Save draft history _somewhere_.

   - May be useful for billing or analyzing person's track record of contributing.

3. Allow flexible editing.

   - The draft branch can be rather "dirty" in terms of both the document contents and its Git history. This gives more flexibility to editors and allows to grant them direct write access to this branch to save them from the pains of the pull request workflow.

The workflow is as follows:

- Create draft branch named like `draft202107`, where `202107` denotes July 2021.
- In the draft branch, create a Markdown file from a [template](journal-template.md) and name it like `202107.md`.
- Make edits to the doc.
- Do not add merge commits, they make history hard to read. If the branch was updated by others since your last sync, use `git rebase` to apply your changes on top.
- Add any images embedded in the doc. In general, avoid adding large binary files. See [Title image](#title-image) section.
- When the doc is finished, publish it on GitHub Pages (see example below).
- If all looks proper, fast-forward `master` to `gh-pages`.
- If bugs are found after the release, add more commits to `gh-pages` branch. Then again fast-forward `master` to `gh-pages`. All published versions must have matching commits in `master` and `gh-pages`.
- In general, avoid editing the doc after release, unless there is a very good reason to do so.
- [Update the index](#updating-index).
- Archive draft history in a special `drafts` branch
  - create `tmp` off latest master
  - merge both `drafts` and `draft202107` into `tmp` with a single commit, e.g. `gitm merge drafts draft202107` (order matters!) with a message like `Archive draft 202107`
  - fast-forward `drafts` to `tmp`
  - delete `tmp`
- Delete the draft branch locally and on GitHub.

Steps to publish the doc:

```
git checkout gh-pages
git checkout draft202107 journal/201906.md
git checkout draft202107 img/202107.1.github.png
git commit -a -m "202107: Add Decred Journal - July 2019"
git push origin gh-pages
```

### Updating index

There are two files that track all DJ issues and their translations. `index.md` contains _primary_ locations of documents, while `mirrors.md` tracks _all_ known locations where the issues or their translations are mirrored.

To avoid commit churn on `master`, these files are updated in batches once a month, after the release.

### Setup tips

- A lot of work can be done with just a browser, thanks to GitHub UI.
- For advanced text editing, comparison and Git operations you will need to setup local software. Get a comfortable text editor with Markdown support, ideally also with Markdown preview and Git support. Some options to try are Atom, Sublime Text, WebStorm. We are still looking for a solid combo, if you find one, please [share](https://github.com/decredcommunity/issues/issues/114) with other writers.
- For comparing revisions use GitHub UI [features](https://help.github.com/en/articles/about-comparing-branches-in-pull-requests), diff tool bundled in your text editor or a standalone tool like [Meld](http://meldmerge.org/).
- By default your email address will be inserted in Git commits and become public. Learn about email privacy [here](https://help.github.com/en/articles/setting-your-commit-email-address) and [here](https://help.github.com/en/articles/blocking-command-line-pushes-that-expose-your-personal-email-address). For the advanced - Git also leaks your machine time zone.

### Workflow tips

- Keep the draft file open. As soon as you see something notable, throw a raw link into the draft. If you are comfortable to write up the story immediately, go for it. Otherwise, add any notes, directions or questions that will help to expand the story later, possibly by other writers. See [TODO](#todos) syntax.
- Push the draft changes daily to stay in sync with other authors.
- Before making changes, make sure you're on the latest version.
- Before making large changes check with others to avoid conflicts.
- Before pushing changes, make sure you based them on the latest version. Use Git [rebase](https://git-scm.com/book/en/v2/Git-Branching-Rebasing) otherwise.
- Write up stories sooner to prevent the work piling up.
- Avoid sending too unfinished content for review, this leads to more roundtrips.
- Try to give 2 full days for final review.
- The sooner the DJ issue is released [the better](https://github.com/xaur/decred-news/issues/34).
- If you get stuck with Git, check the [Git Book](https://git-scm.com/book) or ask in #git\_help (ask for invite).

## Collecting content

### General

- All claims must reference sources.
- Stick to facts, minimize opinions and assumptions.
- Focus on what was **done**. Announcements and plans are good too - just be specific and minimize hype.
- All work is important, the challenge is to not overwhelm the reader and balance between bird's eye and the details, which are often interesting.
- Linked pages must be in English in most cases.
- Non-English links are allowed but they must be significant in some way, e.g. original research or ratings.
- Archive all linked pages in [web.archive.org](https://web.archive.org/) or [archive.today](https://archive.today/).
- To check if something was reported in previous issues, search the .md files
  - e.g. `grep -ir dcrwallet/pull/1330` shows that this PR was covered in Nov 2018
  - another way is to use the search box [on GitHub](https://github.com/xaur/decred-news)
- DJ issues are huge and writing many stories require understanding a fair bit of historical context and domain expertise. It comes with time.

### TODOs

TODOs are small tasks and notes embedded in the draft document.

Two types of TODOs are used in DJ.

First type is anything `{inside curly braces}`. It can be a task, a placeholder, a question or a note. Tasks need to be done while notes can be just removed when they are no longer needed. Examples:

Task:

> UTXO set optimization was merged {explain in plain English}

Question:

> 3 typos have been fixed {do we need this?}

Placeholders that must be filled:

> In {month} the treasury received {n} DCR and spent {n} DCR.

Special case of placeholder is an empty TODO, it must be obvious from the context what it should be replaced with:

> Reddit subscribers: {} (+{})

Second type of TODOs are "hanging" URLs not wrapped in Markdown links. For example, a hanging URL in Relevant External simply means "write up this story".

Final release must have all TODOs resolved, i.e. contain no curly braces and no URLs outside of Markdown links.

### Intro

Give a short and high level recap of month's highlights.

Don't add too much detail. Don't add any links, links will appear later in the text.

### Important Notice

If there is an important notice to deliver, place it immediately after the Intro. Some examples:

- prepare for upcoming consensus vote ([example](https://xaur.github.io/decred-news/journal/201910.html))
- reminder to vote in ongoing consensus vote
- reminder to vote in proposals with high impact
- upgrade software
- updates on incidents

The idea of first three items is to stimulate higher voter participation which is extremely important for project's success.

Fourth item reminds readers to upgrade to have good stuff deployed sooner.

### Major Release Coverage

If there is a major software release or feature release, place it after the Important Notice (if any). Examples:

- [v1.4.0 Upgrade and Consensus Vote](https://xaur.github.io/decred-news/journal/201901.html#v140-upgrade-and-consensus-vote)
- [Privacy release](https://xaur.github.io/decred-news/journal/201908.html#privacy)
- [v1.5 Release Candidates](https://xaur.github.io/decred-news/journal/201910.html#v15-release-candidates)

Release coverage is more focused on _users_ because it talks about features they can get by downloading new binaries (i.e. no need to build from source) or just visiting a website (Politeia, dcrdata). Development also tries to translate tech speak for users, but often includes tech goodies for _developers_ as noted below.

Whenever software downloads are mentioned, remind people to [verify](https://docs.decred.org/advanced/verifying-binaries/) them.

### Development

Per the [Goals](#goals), this section aims to update technical and less technical community members, attract more builders and expose the solid progress to everyone else. Development is perhaps the most challenging in this regard because of the constant need to balance between these audiences and switch between zooming in and zooming out.

A side goal is to educate people about the real effort needed to build robust cryptocurrency software.

There are two target subgroups of devs:

1. devs that already work for Decred - to them we give the big picture so if they see something interesting they can follow and discover new opportunities (interest often makes for the best performance)
2. devs who do not yet work on Decred - for them we show why Decred is a good place. For example, any effort to cut bloat, keep the stack up to date (no [horrific](http://catb.org/jargon/html/C/cthulhic.html) legacy tentacles), to improve privacy or in general do something elegantly would attract me personally (@bee).

All updates must be **notable** in some way.

The most notable event is the release of new software version. These don't happen every month, so most of the time we report changes in source code that happen in pull requests (PRs) or commits.

Signs of a _not_ notable pull request or commit: few lines changed, no description, no discussion, not many people involved, no references from or to this PR, short time span, few commits, not much happened during the month.

Some maintenance work sounds less "exciting": small bugfixes, increased test coverage, code refactoring, dependency upgrades, code cleanup, etc. Normally, such items are not reported on their own but are grouped in a general statement like "increased test coverage", unless the total amount is so small that can be omitted. Maintenance item does get a standalone mention when it is big (thousands of lines affected in non trivial way), took a ton of effort (e.g. hunting down a super tricky bug), has huge impact (e.g. vulnerability fix) or is otherwise interesting (e.g. someone went on a crusade to [remove jQuery](https://github.com/decred/dcrdata/pull/915) or remove a bad practice like [inline JS](https://github.com/decred/dcrdata/pull/873)). Automation upgrades like linters, CI, vulnerability detection, etc, are often notable.

Try to be specific when using catch-all phrases, e.g. "refactoring to increase separation of concerns" instead of just "refactoring".

While these things like may sound too generic, we often mention them to give a general sense that maintenance and infra work never stops and takes a lot of effort. Indirectly, it shows that our devs are experienced and know "the price" of a large codebase - if you don't consistently take care of it and just keep adding features it may blow up.

Special category we try to mention is changes backported from other Go codebases like btcd or lnd. Indirectly, it shows returns from past contributions in the space - seeds planted years ago by C0 by investing into btcsuite.

In each project sub-section, order work items from "most released" to "least released". Stages of work life cycle considered for reporting:

- work released in binaries or deployed to production sites
- work released in source code (merged in master branches)
- work finished but still in review
- work in progress (new work done this month)
- work started
- discussion started
- planned work, from near to long term

The same effort may be reported multiple times in multiple DJ issues as it moves to next stages. For example, reporting merged work tells developers and enthusiasts that new feature is available on master so they can build from source. Reporting after release tells everybody else the new feature is available in the binaries.

For each update, make it clear if and how it is **tangible** by users or by developers. Put user tangible updates first.

Don't worry if a project is short on updates. There are many projects and sometimes devs move their focus.

Where do we look for updates:

- [Decred project](https://github.com/decred) repos
- corporate contractors repos, e.g. [Raedah Group](https://github.com/raedahgroup)
- individual developers repos, e.g. [matheusd](https://github.com/matheusd)
- scan dev chats (optional)
- ask the devs. The more updates we get directly from devs, the better.

What do we look for:

- release notes
- pull requests
- commits
- interesting conversations

To find **merged pull requests** for the month:

- Use GitHub search features, notably the `merged:2019-06-01..2019-06-31` query to find pull requests that were [merged](https://help.github.com/en/articles/searching-issues-and-pull-requests#search-by-when-a-pull-request-was-merged) in a given month ([example](https://github.com/decred/politeia/pulls?q=is%3Apr+is%3Aclosed+merged%3A2019-06-01..2019-06-30)).

To find **open PRs** with activity:

- Check two queries, `is:open updated:2019-06-01..2019-06-31` and `is:open created:2019-06-01..2019-06-31`. Checking the `created` one separately is necessary because GitHub search does not list PRs which were created but not updated in the `updated` query. And unfortunately it does not support a logical `OR` so we have to check both. For each PR in the merged list, check that some notable activity happened in that month. There are false positives. Some activity may mark the PR as updated while nothing of interest happened. Example: [politeia#833](https://github.com/decred/politeia/pull/833) - work was merged on May 1, branch deleted on Jun 20 and the PR shows up as updated in the June search query above.

Some projects have commits that don't go the pull request route. For these, we scan **commits** on the `master` branches:

1. Open the `master` branch (e.g. [politeia](https://github.com/decred/politeia/commits/master)).
2. Find notable commits for the month.
3. If a commit links to its corresponding pull request, check that PR too for more context.

**Chats** may provide additional context for changes and interesting (sometimes notable) discussions. Scanning chats is optional because it can take a lot of time. Dev chat rooms: #dev, #politeia, #dcrdata, #lndev, #documentation, #design, and others.

For dev **stats**, there is a nice GitHub filter for calculating developers per repository ([example](https://github.com/decred/dcrd/graphs/contributors?from=2019-06-01&to=2019-07-01&type=c)). 

GitHub can be used to calculate the count of commits, added/deleted lines, and the count of contributors for a _single repo_ during the month:

- find IDs of last commit in previous month and last commit in current month
- construct GitHub compare link
  - e.g.: https://github.com/decred/dcrd/compare/70c14042...5048959f
  - 8 first characters of commit IDs would do, also mind the 3 dots `...`
- look at the contributors count

One more way to get the stats is Insights tab -> Pulse tab ([example](https://github.com/decred/dcrd/pulse)). The advantage is that it includes the count of "Active PRs" (whatever GitHub's definition of "active" is). A disadvantage is it's impossible to specify start and end of the period, which requires to take numbers from this page on 1st day of the month (ideally at UTC midnight).

Pay attention to very large changes (thousands of lines) and try to exclude automated changes that heavily skew the stats, such as regenerating code from ProtoBuf definitions ([example](https://github.com/decred/decrediton/pull/2565)) or mass reformatting ([example](https://github.com/decred/decrediton/pull/2481)).

See [Development](sources.md#development) in the sources cheat sheet.

### People

Main goals of People are:

1. Greet new contributors, both individuals and organizations
2. Make the community more familiar with people building Decred
3. Track community growth

**1. Greet new contributors**

- cheer people whose code got merged to master branches for the first time
- congratulate people who were granted a Decred Contractor Clearance (DCC)

Ways to detect new contributors:

- use the [contributor tracker](https://github.com/degeri/decred_contributor_track)
- watch for changes to [contributors](https://decred.org/contributors/) page in [commits](https://github.com/decred/dcrweb/commits/master) to dcrweb (this is not a perfect source as described below, but it may help not miss new people)
- when lurking GitHub, click the username on the commit to show all commits by that user and see if they started recently (for [example](https://github.com/decred/politeia/commits?author=martonp), martonp started in June)

**2. Make the community more familiar with people making Decred**

- tell about active contributors via personal stories and interviews. If an interview was released, add it to People if it has something about personalities (e.g. personal background, motivation, aspirations, stories, etc). Don't add purely technical interviews.

**3. Track community growth**

- keep an eye on user and follower counts in relevant social media accounts

Sources: [People](sources.md#people).

#### Why new contributors at decred.org are not reported

Following the [decision](#reporting-departures) to stop reporting removals from decred.org [Contributors](https://decred.org/contributors/) page, in [April 2020](https://xaur.github.io/decred-news/journal/202004.html#people) issue we have decided to also not report additions, for the same reasons.

Originally, we reported changes to the Contributors page assuming that it reflects the list of active Decred contributors. But later we realized that it does not and there is [no intention](https://github.com/decred/dcrweb/issues/781#issuecomment-594903664) to do so.

#### Why departures are not reported

In [January 2020](https://xaur.github.io/decred-news/journal/202001.html#people) issue the People section covered removals from the [Contributors](https://decred.org/contributors/) page at decred.org. @bee [argued](https://matrix.to/#/!psRvVbtljHXLzCBrjf:decred.org/$vhrC9Ak1Nc3UR4cgIXznoBC1Ci6wbO7dfpZuW57zsaI) that the Contributors page shall be treated as a list of _active_ contributors and that we should not fear talking about departures. However, after [more discussion](https://matrix.to/#/!RwcqjIOMNizkPzGnLr:decred.org/$158375819434036swOfM:decred.org) it was decided to stop mentioning removals in DJ based on the following points from @richardred:

- what that page actually represents is probably quite different to how most people will interpret it
- goes also for the converse, if we mention every removal from contributors page people may assume it can be used as list of current contractors, which afaik it is not good for. it's not a formal process and I don't know what the criteria are for determining when someone is removed from the page, it reflects maintenance of decred.org as well as Decred's staffing
- devoting too much attention to the changes to a page of decred.org, in the absence of any other public source, may give people a misleading impression about how useful or comprehensive that page is
- in many cases people may remain on that page for a considerable period after they have stopped contributing, which decreases its reliability further
- there are contractors who aren't listed at all

#### Reporting departures

In case we decide to report removals from the Contributors page again, or report other kinds of "departures", below are guidelines for presenting that.

"Goodbye" must be done in a decent way to people who were removed from decred.org/contributors or got their DCC revoked. Decent means:

1. Make it clear where they were removed from.
   - People are removed from decred.org/contributors to keep that list up-to-date. It is not an excommunication or anything like that, rather reflecting a status change.
   - DCC revocation is a bit more "severe" but is also not an eternal mark of shame. People are welcome to improve and try again.
2. Thank them for all the good work done to improve Decred.
3. Invite for collaborating again in the future and hint that there's always a lot of work to do.
4. Don't be afraid to talk about people leaving. People join and leave all the time, there are many reasons for both events and this is normal. When presented decently, it is actually a "power move", compared to organizations that try to amplify the "good news" of people joined and suppress the "bad news" of people leaving.

### Governance

Goal: provide a digest of decision-making activity and finances.

Finances overview includes treasury income and expenses in DCR and USD. When more finance info is available for reporting we may split this into a separate Treasury or Finances section per the [content plan](content.md).

Decision-making activity overview covers proposal activity on Politeia, pre-proposals posted in other places, as well as (meta) discussions about how Politeia and other governance processes should work.

For proposals with voting in progress or finished, mention ticket participation (turnout) in addition to Yes/No percentages. The idea here is to constantly bring turnout numbers to public attention. The higher the turnout, the more engaged are the stakeholders and the healthier is the network.

Since Politeia Digest provides more frequent and more detailed coverage of Politeia activity, limit Governance to higher level overview and link to Politeia Digest issues for more details and analysis.

Sources: [Governance](sources.md#governance).

### Network

The main goal of Network is to keep people's eyes on metrics with high impact on network security, such as hashrate, rate of missed tickets, locked DCR amount and percentage, count of nodes, node version distribution, etc.

This section also covers any notable dynamics like:

- sharp hashrate drop or increase
- incidents
- consensus change deployment progress
- migration of tickets to/from VSPs

Network, Mining and Integrations can be logically grouped in "infrastructure".

Sources: [Network](sources.md#network).

### Ecosystem

Ecosystem covers three distinct areas: Mining, Integrations, and Adoption.

Originally each had its own section, but more recently it is all covered in a single section called Ecosystem.

Sources: [Ecosystem](sources.md#ecosystem).

#### Mining

Mining used to cover the mining scene: new miner units and their stats, new PoW pools and updates from existing ones, relevant news about colocation, sellers, energy, cooling, etc.

Recent issues of DJ have omitted Mining since there is no big news here, and also because we don't have people tracking this space closely. [Contributions](contributing.md) are welcome.

#### Integrations

In contrast with Network, which is about fundamental infrastructure and health indicators, Integrations is about services expanding Decred infrastructure, most commonly _businesses_.

Besides announcements from VSPs, exchanges, wallets and payment processors, try to add interesting facts about them.

For example,

> Decred [is live](https://twitter.com/roomofsatoshi/status/1052879109099991041) on [Living Room of Satoshi](https://www.livingroomofsatoshi.com/). It allows one to pay any bill or to pay money into any Australian bank account with Decred. Established in 2014, the service helped to pay over 140,000 bills.

or

> [BitPro](https://bitpro.cc/) payment gateway added Decred and [posted](https://www.reddit.com/r/decred/comments/8og4he/bitpro_payment_gateway_adds_decred/) on Reddit. Notably, it is fully functional without javascript or cookies and does not ask for name or email, among other [features](https://bitpro.cc/start).

Updates about communications infrastructure (e.g. Matrix, Discord, Telegram, etc) also go here.

#### Adoption

There is no strict distinction between Integrations and Adoption. The guiding rule is: Integrations is about _building_ out the Decred infrastructure, while Adoption is about _using_ it by businesses and individuals. In other words, Adoption is about DCR being _adopted_ as store of value or medium of exchange, and building new products and services around it.

Stories must have something to do with Decred blockchain, for example:

- a new fund added DCR to its portfolio
- a new merchant started accepting DCR
- project or organization adopted dcrtime or Politeia
- something has been built on top of DCRDEX or atomicswap

Similar to Integrations, try to add interesting facts about each organization, in addition to a "dry" summary of what happened.

### Outreach

Provide overview of outreach/communications/marketing activity for past month and any future plans.

Logically, Events and Media are sub-sections of Outreach, but they have their own level 2 headers to keep the document flat.

Sources: [Outreach](sources.md#outreach).

### Events

Cover past and upcoming physical and web events where Decred had presence.

For each past event, add some basic info following the standard format in the template. On top of that, try to add the most interesting highlights (1-3 sentence per event). Same for upcoming events.

If the DJ release is close but some events still lack info, actively post a list of such events in #event and ask for comments.

Look at events from Decred's perspective, look for experience to learn from. Some hints: how it went, how many visitors, what they know, what they don't know, what they ask, what they think about Decred, any interesting trends that could shape our events activity.

Sources:

- some events have reports written up in the [events repo](https://github.com/decredcommunity/events) - you can subscribe and watch for updates
- follow Twitter accounts that often tweet about events, e.g. [Decred_ES](https://twitter.com/Decred_ES)
- more sources: [Events](sources.md#events).

### Media

Cover the best Decred-related content posted in the media. Ratings go here too.

Criteria for "Selected articles" is an [open question](https://github.com/xaur/decred-news/issues/21).

Signs of a good candidate article: something you would recommend reading to a wide audience, something we don't know or a fresh look at something we know, any original research, content from community members, something that took more than 2 hours to write.

For each selected article, optionally add a small note about why it is great.

Sources: [Media](sources.md#media).

### Discussions

Goal: Track interesting conversations on social media

Sources:

- scan [r/decred](https://www.reddit.com/r/decred/new/)
- use Reddit's follow/friend features to follow prominent posters
- [Discussions](sources.md#community-discussions)

### Markets

Report any interesting market movements. Ideally, cover the action in markets not frequently covered by the media - OTC and DEX.

Mention both USD and BTC price:

- USD price shows how Decred competes against fiat and the collective purchasing power of DCR holders (including the treasury - important health indicator)
- BTC price shows how Decred competes against Bitcoin, since they both are sovereign SoV+MoE focused cryptocurrencies with similar properties

Do not speculate about the price.

Sources: [Markets](sources.md#markets).

### Relevant External

The ideas behind this section:

1. Show that many good decisions were put into the foundation of Decred, that many problems were predicted and prevented years ago
2. Learn from experience of other projects
3. Track interesting trends, detect risks
4. Educate the audience about things that have big influence on Decred: cryptocurrency tech, governance, computer security, regulations.

Topics commonly covered here:

- PoW, ASIC resistance
- Full nodes
- Security of cryptocurrency networks (double spends and other attacks)
- Cryptocurrency tech
- Governance, funding, chain forks, community forks, and the controversy that often surrounds these
- DEX
- Exchanges and other services
- Regulations
- Computer security
- Fun stuff

Sources: [Relevant External](sources.md#relevant-external).

### Missed content

Some notable stories are discovered after the release. Add them in the next issue, optionally with a comment tag in italics e.g. `_(missed in March issue)_`.

### Title image

Title image used on GitHub Pages must be 768x384 pixels.

Try to fit it into 100-200 KiB to save space, e.g. by saving as JPEG with 98% quality. Motivation: Git repositories store all versions of all files ever committed, therefore they quickly grow in size when adding binary files like images.

For artwork caption, at the minimum add the title of the work and its author, e.g. `Image: Anomaly by @saneder`.

So far DJ images have been abstract art. If possible, add extra text hinting at what is expressed. The text must either make sense or be abstract enough to not need it, but not something in between. See [this discussion](https://github.com/xaur/decred-news/issues/76).

For photos, the caption must be a brief description of what is pictured.

## Style, Editing

### General

Principles:

- Save reader's time: keep the most important bits for each story and a link to follow.
- Avoid hype and fake excitement.
- Attitude: check that nothing damages Decred's public image (this does not mean hiding inconvenient facts, see [Neutrality](#neutrality)).

Areas of improvement:

- No factual errors.
- Grammar, punctuation, wording, tense consistency, sentence and paragraph composition.
- Make the language less boring.
- Proportion: check that more important stories get more space.
- Order of content.
- Remove empty sections (e.g. when no news for Mining).

### Neutrality

One of the goals of DJ is to assist Decred stakeholders in making good decisions. For this reason DJ strives to present facts accurately, avoid opinions and assumptions, put reasonable effort in verifying claims, and always link to sources.

At the same time, DJ arguably cannot be called "neutral" because it is produced by Decred enthusiasts who believe in certain values and have a certain sense of humor.

DJ shall put best effort to maintain a good public image of Decred, but not by the means of omitting inconvenient facts. Instead, any such facts must be presented as clearly as possible.

If there is a need to add an opinion, it must be inside a [quote block](#quotes).

See [this discussion](https://github.com/xaur/decred-news/issues/93).

### Order of reporting work

For any work reported, order the items from "most released" to "least released". See [Development](#development) for an example.

### How to identify people

This is an [open question](https://github.com/xaur/decred-news/issues/20).

The current approach is subjective and informal: use the most well known handle to identify Decred community members, use full names or handles for everyone else.

### How to give credit

When to credit someone for an accomplishment is an [open question](https://github.com/xaur/decred-news/issues/26).

There is no formal criteria at the moment. A lot of work is done each month. Adding credit to everything would overwhelm the reader. On the other hand, sometimes it feels right to give someone a shoutout, especially newcomers. Use your best judgement.

When giving credit to multiple people sort the names alphabetically:

> Thing X is released, credits to @alex, @maria and @sam

Speaking of the credits for DJ production at the end of the issue, make sure to add everyone who contributed. There is no formal criteria at the moment. The informal criteria is: add people who _actively_ brought us something, opposed to content just picked up by DJ authors.

### Quotes

Follow the standard format: `quoted text (source)`.

Example formats:

```
> Quoted tweet ([@handle](tweet link))

> Quoted chat message (@handle in [chat](matrix link))

> Quoted chat message with room specified, where it matters (@handle in [#room](matrix link))

> Quoted article (@handle in [article title](article link))

> Quoted text where type of source does not matter ([@handle](arbitrary link))
```

### Link text

Links should span 1-3 words. Avoid too short and too long link text. Examples:

- "feature X [is](link) now available": bad, too short, hard to click
- "[feature X is now available](link)": bad, too long, visual noise
- "[feature X](link) is now available": good balance

### Use canonical links without tracking

First, remove any tracking parameters like Medium's `gi=...`, Google Analytics `utm_...`, etc. As a general rule, remove any URL parameters that don't break the link. "URL parameters" is the stuff that comes after `?` in the URL.

Second, ensure URLs are [canonical](https://en.wikipedia.org/wiki/Canonical_link_element). This means using `www.reddit.com` over `old.reddit.com`, `www.youtube.com` over `youtu.be`, and so on. On most pages canonical link can be found in `<link rel="canonical" href="..."/>` in the page source. Use of canonical links improves linking of content together (e.g. on Reddit).

**Examples**

Bad: junk parameters: https://www.youtube.com/watch?v=3RGoUQK0g24&feature=share

Bad: non canonical domain: https://youtu.be/3RGoUQK0g24

Good: https://www.youtube.com/watch?v=3RGoUQK0g24

Bad: Forbes tracking (remove the `#425f36a11067`):

https://www.forbes.com/sites/kenrapoza/2019/06/20/facebooks-libra-coin-is-both-vampire-project-and-regulatory-nightmare/#425f36a11067

Bad: Medium tracking (remove the `?gi=68a95d076f04`):

https://hackernoon.com/decred-wants-you-be-one-of-the-first-to-test-the-dcr-lightning-network-dd9ecf14d95e?gi=68a95d076f04

### Chat links

For links to chat messages always use Matrix links over Discord or Telegram links.

Currently, we use links that open target messages in a web client hosted at `chat.decred.org`:

> Share your updates for the next issue in our [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat room.

In the future we should start using `matrix.to` links or even `mxc://` links, when they become easy to use.

For links to files that were uploaded to Matrix, don't link to file directly. Instead, link to (relevant) message that uploaded it. It is trivial to open the message and download the file, but it is not trivial to find the message by the direct file link.

### Markdown

- Use backslash `\` to escape underscore `_` so it won't be treated as italics. Example: `under\_score`.
- Always use hyphen `-` for bullet lists.
- Always use `_underscore_` for italics and `**double asterisk**` for bold.

See this excellent [cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) of Markdown features.

Medium/Odysee/etc versions may require additional processing to look nice. It is recommended that the "Git/Markdown maintainer" role does as much Markdown preparation as possible, and places the final files in a well-known location (e.g. [decred-journal-extra](https://github.com/xaur/decred-journal-extra)) so that Medium/Odysee admins can just copy-paste it without torture (be nice with them, we don't have many).

**Medium specifics**

1\. Avoid Markdown features that cause trouble when pasting into Medium:

- Paragraph breaks and blockquotes inside list items.
- Nested lists.
- In general, avoid combining _any_ two structural formatting features to be extra safe.

If you really want to use advanced Markdown features that "just work" on GitHub, please prepare a separate, simplified Markdown file for Medium that work-arounds all Medium's formatting issues.

2\. Table of Contents must be recreated manually.

**Odysee specifics**

1\. Replace all "simple" usages of the `@` character with its HTML escape sequence `&#64;`.

  - "Simple" usages are the ones NOT inside link text (e.g. `[@HotUser](url...)`), NOT coming after a square bracket (e.g. `\[@HotUser, bla bla\]` seems to work), and NOT inside link URLs (e.g. `[bla bla](https://medium.com/@username/...)`).

  - Why: Odysee Markdown renderer tries to automatically create links on `@username`-s. Problems - it may tag or even notify an unintended person, and it adds ugly paragraph breaks.

### Typography

This applies to English texts only.

[Translations](translating.md) are encouraged to follow the spirit of simplicity and consistency of this style guide, but are free to adapt to standards of their language.

#### Spelling

1\. Use US English consistently, see common spelling [differences](https://www.tysto.com/uk-us-spelling-list.html) with British English.

2\. Use simple word forms when possible.

#### Numbers

1\. For _large numbers_ always use either uppercase `K/M/B/T` or full `thousand/millions/billions/trillions`, e.g.:

- `$53K`
- `$7 million`

2\. For _small numbers_ use as few decimal places as necessary to reduce noise, but enough to retain context. Examples:

- for the locked DCR (absolute DCR and percentage of the circulating supply) we use two decimal places because the fluctuations are small and because a lot of money is behind this number: `Locked amount was 4.83-5.06 million DCR, which corresponded to 48.3-49.8% of the available supply.`

- for double-digit pool's hashrate share no decimals are necessary, but are needed for smaller numbes: `F2Pool 21%, UUPool 19%, AntPool 17%, Poolin 10%, BTC.com 7.3%, Luxor 2.2%, BeePool 0.14%, Coinmine 0.12%, suprnova 0.08%`

- same for node versions: `Roughly 78% run dcrd v1.4.0, 5.7% are dcrwallet v1.4.0 and 6.2% are v1.5.0(pre) dev builds.`

#### Dates

1\. For dates use short month format and no `th` after day number: `Jan 7`, `Feb 15` and so on.

In dev speak, the format is `MMM D`. Add year if necessary: `Oct 15, 2018`.

#### Characters

1\. Stick to ASCII character set, except the main heading (first line in the file) and names. Modern renderers like GitHub Pages or Medium take care of it and properly render quotes, dashes, etc.

- Use ` - ` (space, hyphen, space) to separate parts of sentences where you would use emdash.
- Use hyphen `-` for number ranges where you would use endash, e.g. `Jan 15-20`.
- Use `'` for single and `"` for double quotes.
- Non-ASCII is ok in names, e.g. `Permabull Niño`.

#### Capitalization

1\. Capitalize `Treasury` when used as a proper noun or formal entity, e.g. `The (Decred) Treasury`. Other uses must be lowercase, e.g. `The Decred project has a treasury`, `treasury funds`, `treasury payouts`, etc. ([discussion](https://matrix.to/#/!TbVdEHFJcNnQyCJpZI:decred.org/$K43TEh3otkfjYZBWJ9WeM7fSrFDRzHu5vk4LjHRDVF0))

2\. Use "Sentence case" for titles of articles/videos/podcasts.

> In sentence case, the title is written as if it were a sentence. This is considered a more casual style and is commonly used in newspapers and on the web for headline capitalization. There are a couple reasons why writers choose sentence case over title case:
> 
> - One could argue that capitalized words slow down a reader's ability to scan, while a title written in sentence case could be perceived as having an uninterrupted flow.
> - Some publications prefer this style simply because it's more likely to preserve consistency. With sentence case, there's no nitpicking over the capitalization of a three-letter preposition. ([grammar.yourdictionary.com](https://grammar.yourdictionary.com/capitalization/rules-for-capitalization-in-titles.html))

#### Punctuation

1\. Simple list items are lowercase without period at the end:

> - added feature 1
> - feature 2 made easier to use

To have more sentences in the list item, add a period and the sentence, this time it must end with a period

> - added feature 1. It makes your 30% happier.

2\. Do not insert punctuation into the quote that was originally _not part of the quote_:

> "To protect your privacy we will further reduce your privacy", the official said.

Note the `privacy", the` and not `privacy," the`

> The report added that "Versions prior to 5 are vulnerable. Versions 5-6 are not vulnerable but users are still advised to upgrade to version 7.". As of October 2021, 70% of clients are version 7.

Note the `version 7.". As` and not `version 7." As`.

While this goes [against](https://grammar.yourdictionary.com/grammar/punctuation/does-punctuation-go-inside-quotation-marks.html) many style guides, it is consistent and does not distort the quoted message.

### Linting

Just before the release:

- Remove non-ASCII characters (except the main heading and the names).
- Remove double space, trailing space, more than 2 subsequent newlines.
- Add any missing newlines around headings and bullet lists.
- Remove `?via` from matrix.to links.
- Remove tracking parameters from URLs.

## Reviewing

Take a note of the Git revision you review. If the file changes after your review, only the difference needs to be re-reviewed. This difference can be shown by constructing a diff link, e.g.:

https://github.com/xaur/decred-news/compare/5df8b0f2...draft06

where `5df8b0f2` is a 8-character Git revision and `draft06` is the name of the branch. Reads like "show me the changes since 5df8b0f2 until the latest draft06".

## Translations

See [Translating DJ](translating.md).

## Why Git?

Pros of the Git/GitHub workflow:

- all content can be easily downloaded and synced (semi-decentralized storage)
  - protects from knowledge loss from censorship by centralized platforms like Medium
- cloning is permissionless and does not require an account
  - no need to visit Google Docs
- all changes are recorded
- integrity protection
- allows more people to contribute in a proven workflow
  - devs can seamlessly engage/contribute since the workflow is similar to theirs
- you can use your favorite text editor and work offline
- show off: one of the most advanced productions in the space
- possible authenticity protection via digital signatures (requires extra setup)
- Git software is widespread

Cons:

- higher learning curve, except most trivial usage via GitHub web UI
- conflict resolution is not automatic and is error prone
- requires experienced Git maintainer to have a pretty repository

## Why curly braces for TODOs?

- They do not conflict with Markdown syntax that uses square brackets and parens for links: `[click here](http://example.com)`.
- They do not conflict with HTML syntax that uses angle brackets for tags: `<img>`. Markdown allows embedding HTML.
- They can be easily found and counted to estimate how much work remains.
- They can be highlighted in text editors.
- They can sit between words (aka "inline"). In contrast with typical TODO syntax in programming languages, where a TODO must take its own separate line.

## Contributing

See [here](contributing.md).
