# Release checklist ideas

This checklist has both what we do now and ideas of what we could do to in the future. For current working checklist see [release-checklist-template.md](release-checklist-template.md).

Optional steps are marked with `(opt)`.

**Dependencies**: Send notice in advance so people can plan their work.

- [ ] Request title image via an [issue in dcrdesign](https://github.com/decred/dcrdesign/issues)
  * GitHub version must be 768x384 px
  * ask for image title and theme to be used in the image caption (saender)
- [ ] Request month's first time contributors (degeri, s_ben or #research)
- [ ] Request dev activity stats (degeri, s_ben or #research)

**End of month snapshots**: Snapshot data that is hard to obtain later.

- [ ] snapshot social media stats
  * Politeia, Matrix, Discord, Slack, Telegram, Twitter, Reddit, YouTube, Facebook, LinkedIn, GitHub dcrd, Instagram
  * (opt) non-English platforms: Telegram (es pt zh it ru), Twitter (es), Instagram
- [ ] staking
  * 30-day average ticket price (https://dcrstats.com)
- [ ] nodes
  * node count, versions, etc (ask chappjc or #dev or dcr.farm)

**Release**

- [ ] (opt) Notify #writers_room few days in advance
  * call target review date, ask who will be available
- [ ] Try to extract more dev updates from master branches
- [ ] Complete Development
- [ ] Ask in #dev to review Development
- [ ] Complete Events
- [ ] (opt) Ask #event_planning to review Events
- [ ] Complete Outreach
- [ ] Complete Media
- [ ] (opt) Ask #marketing to review Outreach+Events+Media
- [ ] (opt) Ask #trading to review/improve Markets section
- [ ] (opt) Find interesting Reddit and Twitter threads
- [ ] (opt) Ask #general for awesome Decred-related pics and photos of the month
- [ ] (opt) Look for awesome pics and photos
- [ ] (opt) Add a few interesting pics up to 300 px height
- [ ] (opt) Ask quoted people to review their texts
- [ ] Pre-review read: check spelling, grammar, test that links work
- [ ] Ask #writers_room to review
- [ ] (opt) Wait for GitHub dev activity tweet (lustosa)
- [ ] Resolve all [TODOs](https://github.com/xaur/decred-news/blob/docs/guidelines.md#todos)
- [ ] Carefully check that all people who contributed or gave feedback are in [credits](https://github.com/xaur/decred-news/blob/docs/guidelines.md#how-to-give-credit)
- [ ] [Lint](https://github.com/xaur/decred-news/blob/docs/guidelines.md#linting)
- [ ] Add [title image](https://github.com/xaur/decred-news/blob/docs/guidelines.md#title-image)
- [ ] Remove `{DRAFT}` from title
- [ ] Final read
- [ ] Publish on GitHub with a single commit to `gh-pages`
- [ ] (opt) Ask karamble to add the post on decredcommunity.org
- [ ] Publish on Medium (richardred or Haon)
- [ ] (opt) Verify Medium version, check for formatting issues
- [ ] Choose the best link to disseminate: Medium vs GitHub Pages vs decredcommunity, etc
- [ ] Submit best link to r/decred
- [ ] Tweet best link via decredproject. Don't forget to add title image.
- [ ] If bugs are found in the published version quickly after the release, add commits to the draft branch and amend the commit on `gh-pages`
- [ ] Fast-forward `master` to `gh-pages`
- [ ] If changes are necessary after the release (>1 h), add extra commits to both `master` and `gh-pages`.
- [ ] [Update index](https://github.com/xaur/decred-news/blob/docs/guidelines.md#updating-index)
- [ ] Create Git tag from the draft branch, e.g. `archive/draft1901`
- [ ] Delete the draft branch
- [ ] (opt) Update `journal-template.md` in `docs` branch
- [ ] (opt) Update this release checklist template in the `docs` branch
