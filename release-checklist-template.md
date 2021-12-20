# Release checklist

Checklist currently in use. For unused ideas see [release-checklist-ideas.md](release-checklist-ideas.md).

Legend: `by: X` - execute step by date X, `ready by: X` - resource must be ready by date X, `PO` - product owner responsible for the overall quality.

Copy the raw Markdown after `---` into a new release issue or pull request.

---

**DRAFT**: {link}

**Dependencies**: Send notice in advance so that people can plan their work.

- [ ] [title image](https://github.com/decred/dcrdesign/issues)
- [ ] first time contributors
- [ ] PR update

**Monthly snapshots**: Snapshot data that is hard to obtain later. Ideally, capture it at 1st day of the month at 00:00 UTC.

- [ ] social media stats
  - accs reported in People (the "key" list)
  - all accs in [social-media-stats](https://github.com/decredcommunity/social-media-stats)
  - untracked candidate accounts (the "maybe" list)
  - see if any new accounts need to be tracked
- [ ] Medium and Publish0x post stats
- [ ] Reddit traffic stats
- [ ] mining
  - pool hashrate absolute Ph/s and share % values
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

- [ ] scan GitHub repos for dev updates
- [ ] complete Development
- [ ] complete People
- [ ] PO review Development and People
- [ ] ask in #dev to review Development and People
- [ ] complete Governance
- [ ] complete Network
- [ ] scan Twitter for notable news
- [ ] scan Reddit for notable news
- [ ] complete Ecosystem
- [ ] complete Events
- [ ] ask #events to review Events
- [ ] complete Media
- [ ] complete Outreach
- [ ] ask #marketing to review Outreach+Events+Media
- [ ] complete Markets
- [ ] complete Relevant External
- [ ] offer quoted people to review their texts
- [ ] complete Intro
- [ ] PO review of all sections
- [ ] ask #writers to review
- [ ] incorporate all feedback
- [ ] resolve all [TODOs](https://github.com/xaur/decred-news/blob/docs/guidelines.md#todos)
- [ ] ensure that all people who contributed or gave feedback are in [credits](https://github.com/xaur/decred-news/blob/docs/guidelines.md#how-to-give-credit)
- [ ] add [title image](https://github.com/xaur/decred-news/blob/docs/guidelines.md#title-image)
- [ ] add other images with captions
- [ ] pre-release review: grammar, test that links work
- [ ] [lint](https://github.com/xaur/decred-news/blob/docs/guidelines.md#linting)
- [ ] remove `{DRAFT}` from title
- [ ] auto grammer check

**Publishing**

- [ ] publish on GitHub with a single commit to `gh-pages`
- [ ] add new issue to the index.md
- [ ] add all images to the [files repo](https://github.com/xaur/decred-journal-files)
- [ ] publish on Medium
  - upload images
  - make Table of Contents
  - add to `/decred/journals`
  - add relevant tags
  - verify text previews shown at `/decred` and `/decred/journals`
  - check for formatting issues
- [ ] publish on Publish0x
  - upload images
  - add relevant tags
  - check for formatting issues
- [ ] post on r/decred
- [ ] tweet via decredproject
  - add correct title image for Twitter
- [ ] announce on: Matrix #dcr, t.me/DCRann, Blockfolio, CoinGecko, LinkedIn
- [ ] announce on Instagram
- [ ] fast-forward `master` to `gh-pages` (translators consume `master`)
- [ ] if changes are needed after the release, add commits to `gh-pages` (test in `draftXX` if needed) and update other places
- [ ] [update index](https://github.com/xaur/decred-news/blob/docs/guidelines.md#updating-index)
- [ ] add new issue to decred.org Press page ([coverage.yml](https://github.com/decred/dcrweb/blob/master/src/data/press/coverage.yml))
  - verify deployment

**Housekeeping**

- [ ] archive draft history
  - create `tmp` at `master`, merge both `drafts` and the latest draft commit, fast-forward `drafts` to `tmp`
- [ ] update `journal-template.md` in the `docs` branch
- [ ] update `release-checklist-template.md` in the `docs` branch
- [ ] start new cycle
- [ ] delete the draft branch (will auto-close the PR)
