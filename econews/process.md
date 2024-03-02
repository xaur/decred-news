# Decred Ecosystem News Workflow

*Anything is subject to feedback and revision!*

On a high level we have three stages:

- **Discovery**: scan sources, collect links and notes, map stories in draft files.

- **Research and writing**: follow links and notes found in the Scanning stage and write up each story. Do older stories first so we'll publish them in a chronological order (when possible).

- **Publishing**: Review/polish the story and publish it in the publication *targets* we maintain (currently Matrix and Discord, to be extended).


## Discovery


### What is notable

First let's establish **what is notable** for reporting in #econews and what do we hunt for:

- New releases of Decred software
- Network upgrades
- Network services added/lost/upgraded/changed/incidents
  - APIs, VSPs, mining pools, LN hubs, Politeia, etc.
- 3rd party financial services listing or delisting DCR
  - exchanges, wallets, payment processors
- Notable news about 3rd party exchanges or wallets that support DCR
  - security incidents, services added/removed/changed, regulation stuff
- Gained/lost merchants accepting DCR
- Notable users of Decred services
  - e.g. timestamping adoption
- Gained/lost investors
- Community effots to integrate Decred (monthly)

Read ~2 recent months of #ecosystem chat room to see real examples of what is being reported on.


### Sources

All sources will be listed in the `Econews Sources` chat room in Matrix. Please react to those messages with your emoji to share your scanning progress with the others.

Current list of sources:

- [@decredproject](https://twitter.com/decredproject) announcements
- [decred-binaries releases](https://github.com/decred/decred-binaries/releases)
- [Cryptopower releases](https://github.com/crypto-power/cryptopower/releases)
- [@cryptopowerWlt](https://twitter.com/cryptopowerWlt) announcements
- [DCRDEX releases](https://github.com/decred/dcrdex/releases)
- [Bison Relay releases](https://github.com/companyzero/bisonrelay/releases)
- [vspd releases](https://github.com/decred/vspd/releases)
- [gominer](https://github.com/decred/gominer/commits/master) and [dcrpool](https://github.com/decred/dcrpool/commits/master) `master` branches (\*1)
- [dcrweb commits](https://github.com/decred/dcrweb/commits/master)
- [dcrwebapi commits](https://github.com/decred/dcrwebapi/commits/master)
- [dcrwebapi pull requests](https://github.com/decred/dcrwebapi/pulls?q=is%3Apr)
- #hw-wallets chat
- #general chat
- #pow-mining chat
- #br chat
- #trading chat
- #ecochat
- [Cypherpunk Times](https://www.cypherpunktimes.com/page/2/) weekly/monthly digests

*(\*1) Normally we only check for releases that end users can consume ([example](https://github.com/decred/decred-binaries/releases)). gominer and dcrpool are exceptions because they are "consumed" by the miners who build from source, from the `master` branch, so we quickly check that too. But we only look for notable changes (important fixes or important features like).*


### Mapping stories

- Find the draft file corresponding to the month you are mapping, e.g. `202401.md` for January 2024. These files are hosted [here](https://github.com/xaur/econews/tree/drafts/econews) (for Git nerds - notice we keep it in a special `drafts` branch).
- Set up quick access to the draft file. Bookmark it or open in your local text editor and keep it open.
- Scan sources listed in the `Econews Sources` room one by one.
- If you see anything notable, first check if the story is already mapped in the draft file.
- If the story is not mapped, add a stub for it by copying from [this template](https://github.com/xaur/econews/blob/drafts/templates.md). Insert any links/notes "to be processed later" between the `{` and `}` marks.
- If the story is already mapped (i.e. a stub exists), add any *new* links or notes you've found, again between `{` and `}`. If you write a final paragraph of text immediately, place it *outside* of the `{` and `}`.
- After you map all stories from one source and *push your changes to the draft files* to GitHub, please react to the corresponding message to share your progress.

Draft and written up stories will be hosted in a [separate repo](https://github.com/xaur/econews) (i.e. not in this DJ repo) until the process is tested and polished.


## Writing stories

**NOTE: It is recommended to scan \*all sources\* a few days ahead of the story you are writing up**, so that we publish them in more or less chronological order. For example, if you are writing an event that happened on Jan 5th, it would be ideal to have all sources scanned and all stories mapped by Jan 10th. This way even if the story surfaces in the sources a few days later, we will detect it and report in the correct order.

See an example of the end result here: https://github.com/xaur/econews/blob/master/econews/202312.md

- All editing churn happens in the `drafts` branch. Unlike DJ we will have just one drafts branch for simplicitly. When a story is finished it is added to the `master` branch and posted in chats (and possibly other targets in the future).

- Stuff inside curly braces (`{` and `}`) are *tasks* - things that need to be done/researched/written up/otherwise processed (by any contributor). Completed story must have no curly braces in it.

- *Title and body combined* must take under **1,930 bytes** (which is 1,930 characters if's just ASCII) so it could published in Discord.

- Markdown body is made of bullets.

- First bullet must summarize the story and contain a key fact or two.

- Each remaining bullet must cover notable aspects of the story.

- Links to announcements (as `Announcements: ...` bullet), media coverage (as `Coverage: ...` bullet) and community discussions (as `Discussions: ...`) must be the last bullets.


## Publishing checklist

- [ ] Write item draft in the `drafts` branch
- [ ] Review by someone
- [ ] Add all contributors to `authors`
- [ ] Add relevant `tags`
- [ ] Publish in Git repo's release branch
  - Fill `published_utc`
- [ ] Publish in Matrix `#econews` room
  - Format for Matrix { to be clarified }
- [ ] Post the link in Matrix `#ecochat` room


## Metadata format

All stories begin with a metadata block that looks like this:

```
\`\`\`
event_id: 20240131.1
title: Cryptopower released for Android and iOS
author: alice, bob
published_utc: 2024-02-02
updated_utc: 2024-02-05
tags: wallets, Cryptopower
\`\`\`
```

Metadata is placed in this block to facilitate the generation of web pages.

- `event_id` is a unique identifier for a news *event*. It is based on event's date e.g. `20240115.1`. The numeric suffix (`.1`, `.2`, ...) is added to differentiate multiple events on the same date. The date must be a UTC date, i.e. if the event occurred on 2024-01-16 02:00 in the UTC+8 timezone, its UTC date is 2024-01-15. Because event's date is captured by this field we won't store it again in a human friendly format (`2024-01-15`) and instead derive it to avoid duplication. `event_id` will be used in the generated short links.

- `title` is a concise title of the event. If it containts a colon `:`, wrap the whole title in double quotes e.g. `"New DCR mining pool: dcr.gopool.cash"`. The title must be in "Sentence case".

- `author` is a comma-separated list of authors, co-authors, and editors who worked on the news entry. Authors who did more work must come first. Prefer authors' best known *usernames* e.g. `johnz`. These usernames will be used in the links to authors' pages. More information about the authors like their full display name (`John Zoo`) will be stored elsewhere.

- `published_utc` is the UTC date when the news entry was published in the "original release location" which is the Matrix chat room for entries before a Git repository was created, or the Git repository after it was created. { to be clarified }

- `updated_utc` is only added if the entry was updated after it was published.

- `tags` is a comma-separated list of tags. Tags must not contain spaces and use underscore `_` instead.

Valid tags:

- community\_efforts
- exchanges
- loans
- mining
- regulation
- releases
- security
- staking
- vsps
- wallets
- (any hardware/software product name)
- (any organization name)
- (any country name)


## File format

- `.md` file extension, can't use custom extension without breaking GitHub's Markdown rendering.
- `----` is a story separator.
- Metadata block above each story has triple backticks (\`\`\`) before and after it. We'd pick more disctinct syntax but this was chosen as a compromise with GitHub.
- Stories are sorted as "oldest `published_utc` first".
