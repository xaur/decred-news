# Release checklist

Checklist currently in use. For unused ideas see [release-checklist-ideas.md](release-checklist-ideas.md).

Legend: `by: X` - execute step by date X, `ready by: X` - resource must be ready by date X, `PO` - product owner responsible for the overall quality.

Copy the raw Markdown below `---` into a new release GitHub issue or pull request.

---

**DRAFT**: {link}

**Usage**: This is a "soft" task list, some tasks may be skipped to save time. PO = Product Owner.

**Monthly snapshots**: Snapshot data that is hard to obtain later. Ideally, capture it at 1st day of the month at 00:00 UTC.

- [ ] Social media stats for People
- [ ] Mining stats
  - Absolute Ph/s and network share % values as _reported_ by pools and dashboards
  - Counts of blocks _actually mined_ in a certain timeframe
  - [miningpoolstats.stream](https://miningpoolstats.stream/decred)
  - or [poolbay.io](https://poolbay.io/crypto/54/decred)
  - or [dcrstats.com/pow](https://dcrstats.com/pow)
- [ ] Staking stats
  - Ticket price [30-day average](https://dcrstats.com)
- [ ] Node stats
  - [Decred Mapper](https://nodes.jholdstock.uk/user_agents)
- [ ] VSP stats
  - rendered: [decred.org/vsp](https://decred.org/vsp/)
  - API: [legacy](https://api.decred.org/?c=gsd), [current](https://api.decred.org/?c=vsp)
- [ ] [LN stats](https://ln-map.jholdstock.uk/)

**Writing**

- [ ] Request a PR update for Outreach in advance
- [ ] Harvest GitHub repos for dev updates
  - Make notes of new names for first-time contributors in People
- [ ] Complete Development
- [ ] Complete People
- [ ] PO review Development and People
- [ ] Ask in #dev to review Development and People
- [ ] Ask in #planetdecred to review Development
- [ ] Complete Governance
- [ ] Complete Network
- [ ] Scan Twitter for notable news
- [ ] Scan Reddit for notable news
- [ ] Complete Ecosystem
- [ ] Complete Events
- [ ] Ask #events to review Events
- [ ] Complete Media
- [ ] Complete Outreach
- [ ] Ask #marketing to review Outreach+Events+Media
- [ ] Complete Markets
- [ ] Complete Relevant External
- [ ] Offer quoted people to review their texts
- [ ] Complete Intro
- [ ] PO review of all sections
- [ ] Incorporate all feedback
- [ ] Ensure that all people who contributed or gave feedback are in [Credits](https://github.com/xaur/decred-news/blob/docs/guidelines.md#how-to-give-credit)
- [ ] Add draft image IDs and captions
- [ ] Resolve all [TODOs](https://github.com/xaur/decred-news/blob/docs/guidelines.md#todos)
- [ ] Review by first reviewer
- [ ] Add [title image](https://github.com/xaur/decred-news/blob/docs/guidelines.md#title-image)
- [ ] Add other images
- [ ] [Lint](https://github.com/xaur/decred-news/blob/docs/guidelines.md#linting)
- [ ] Remove `{DRAFT}` from title
- [ ] Final auto grammer check

**Publishing**

- [ ] Publish on xaur.github.io
- [ ] Add images of all sizes to the [files repo](https://github.com/xaur/decred-journal-files)
- [ ] Select "primary" mirror to broadcast (normally Decred Magazine)
- [ ] Publish on Decred Magazine
  - Check ToC, formatting, images, captions
- [ ] Publish on Medium
  - Upload the right images
  - Make ToC
  - Add to `/decred/journals`
  - Add relevant tags
  - Verify text previews on [Decred](https://medium.com/decred) and the [Journals](https://medium.com/decred/journals/home) list
  - Check for formatting issues
- [ ] Post on r/decred
- [ ] Tweet via decredproject
  - Add the right title image for Twitter
- [ ] Announce in Matrix #dcr room
  - Add links to all mirrors
- [ ] Announce on: t.me/DCRann, Blockfolio, CoinGecko, etc.
- [ ] Squash `gh-pages` to have a single commit for the new issue
- [ ] Fast-forward `master` to `gh-pages` (so that translators can get it from `master`)
- [ ] If changes are needed after the release, add new commits to `gh-pages` (test in `draftXX` if needed), `master` and update other places
- [ ] Add new issue to decred.org Press page
  - Submit a PR editing [coverage.yml](https://github.com/decred/dcrweb/blob/master/src/data/press/coverage.yml)
  - Verify deployment at decred.org
- [ ] [Update index](https://github.com/xaur/decred-news/blob/docs/guidelines.md#updating-index)

**Housekeeping**

- [ ] Archive draft history
  - create `tmp` at `master`, merge both `drafts` and the latest draft commit into `tmp`, fast-forward `drafts` to `tmp`, delete `tmp`
- [ ] Update `journal-template.md` in the `docs` branch
- [ ] Update `release-checklist-template.md` in the `docs` branch
- [ ] Start new cycle
- [ ] Delete the draft branch (will auto-close the PR)
