# Release checklist

Checklist currently in use. For unused ideas see [release-checklist-ideas.md](release-checklist-ideas.md).

Legend: `(opt)` - optional steps, `by: X` - execute step by date X, `ready by: X` - resource must be ready by date X, `PO` - product owner responsible for the overall quality.

Copy the raw Markdown after ``` into a new release issue or pull request.

---

**DRAFT**: {link}

**Dependencies**: Send notice in advance so that people can plan their work.

- [ ] [title image](https://github.com/decred/dcrdesign/issues) (notify by: 20th, ready by: 3rd)
- [ ] first time contributors
- [ ] PR update (notify by: 28th, ready by: 3rd)

**Monthly snapshots**: Snapshot data that is hard to obtain later. Aim to capture it at 1st day of the month at 00:00 UTC.

- [ ] social media stats
  - accs reported in People ("key" list)
  - all accs in [social-media-stats](https://github.com/decredcommunity/social-media-stats)
  - untracked candidate accounts ("maybe" list)
  - see if any new accounts need to be tracked
- [ ] Medium and Publish0x post stats
- [ ] Reddit traffic stats
- [ ] mining
  - pool hashrate absolute Ph/s and share %  values
  - [miningpoolstats.stream](https://miningpoolstats.stream/decred)
  - [dcrstats.com/pow](https://dcrstats.com/pow)
  - luxor.tech API
  - save raw data where possible (JSON etc)
- [ ] staking
  - ticket price [30-day average](https://dcrstats.com)
- [ ] network stats
  - nodes at [Decred Mapper](https://nodes.jholdstock.uk/user_agents)
  - nodes at [dcrextdata](https://dcrextdata.planetdecred.org/nodes)
  - update the list of known [nodes and groups](https://github.com/decredcommunity/network-stats/tree/master/nodes)
- [ ] vspd and dcrstakepool instance stats
- [ ] [LN stats](https://ln-map.jholdstock.uk/)

**Writing**

- [ ] extract more dev updates from GitHub repos
- [ ] complete Development (by: 2nd)
- [ ] complete People (by: 2nd)
- [ ] PO review Development and People
- [ ] ask in #dev to review Development and People
- [ ] complete Events
- [ ] (opt) ask #events to review Events
- [ ] complete Outreach
- [ ] complete Media
- [ ] (opt) ask #marketing to review Outreach+Events+Media
- [ ] complete Governance
- [ ] complete Network
- [ ] complete Integrations, Adoption
- [ ] (opt) find interesting Reddit and Twitter threads
- [ ] complete Community Discussions
- [ ] complete Markets
- [ ] complete Relevant External
- [ ] (opt) ask quoted people to review their texts
- [ ] complete Intro
- [ ] PO review of all sections
- [ ] (opt) ask #writers to review (by: 3rd)
- [ ] incorporate all feedback
- [ ] resolve all [TODOs](https://github.com/xaur/decred-news/blob/docs/guidelines.md#todos)
- [ ] ensure that all people who contributed or gave feedback are in [credits](https://github.com/xaur/decred-news/blob/docs/guidelines.md#how-to-give-credit)
- [ ] [lint](https://github.com/xaur/decred-news/blob/docs/guidelines.md#linting)
- [ ] add [title image](https://github.com/xaur/decred-news/blob/docs/guidelines.md#title-image)
- [ ] remove `{DRAFT}` from title
- [ ] pre-release review: check spelling, grammar, test that links work

**Publishing**

- [ ] publish on GitHub with a single commit to `gh-pages`
- [ ] add all images to the [files repo](https://github.com/xaur/decred-journal-files)
- [ ] publish on Medium
  - upload images
  - make Table of Contents
  - add to /decred/journals
  - add relevant tags
  - verify text previews shown at /decred and /decred/journals
  - check for formatting issues
- [ ] publish on Publish0x
  - upload images
  - add relevant tags
  - check for formatting issues
- [ ] post on r/decred
- [ ] tweet via decredproject
  - add title image
- [ ] submit new issue to decred.org Press page ([example](https://github.com/decred/dcrweb/pull/898))
- [ ] if changes are necessary after the release, add commits to `gh-pages` (test in `draftXX` if needed) and update other places
- [ ] announce on: Matrix #dcr, t.me/DCRann, Blockfolio, CoinGecko, LinkedIn
- [ ] [update index](https://github.com/xaur/decred-news/blob/docs/guidelines.md#updating-index)
- [ ] fast-forward `master` to `gh-pages`

**Housekeeping**

- [ ] archive draft history
  - create `tmp` at `master`, merge both `drafts` and the latest draft commit, fast-forward `drafts` to `tmp`
- [ ] (opt) update `journal-template.md` in `docs` branch
- [ ] (opt) update this `release-checklist-template.md` in the `docs` branch
- [ ] start new cycle
