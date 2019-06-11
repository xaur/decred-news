# Release checklist

Optional steps are marked with `(opt)`.

## Dependencies

Send notice in advance so people can plan their work.

- [ ] Request title image via an [issue in dcrdesign](https://github.com/decred/dcrdesign/issues)
  * GitHub version must be 768x384 px
  * Ask for image title and theme to be used in the tooltip (@saender)
- [ ] Request new first time contributors from #research (@degeri, @s_ben)
- [ ] Request dev activity stats from #research (@degeri, @s_ben)

## End of month snapshots

Take snapshots of data that is hard to obtain later.

- [ ] social stats
  * Politeia, Matrix, Discord, Slack, Telegram, Twitter, Reddit, YouTube, Facebook, LinkedIn, GitHub dcrd, Instagram
  * (opt) non-English platforms: Telegram (es pt zh it ru), Twitter, Instagram
- [ ] staking
  * 30-day average ticket price (https://dcrstats.com)
- [ ] nodes
  * node count, versions, etc (ask @chappjc or #dev or dcr.farm)

## Release

- [ ] (opt) Notify #writers_room few days in advance
  * call target review date, ask who will be available
- [ ] Try to extract more dev updates from master branches
- [ ] Complete Development
- [ ] Ask in #dev to review Development
- [ ] Complete Events
- [ ] (opt) Ask #event_planning to review Events
- [ ] (opt) Find more selected articles
- [ ] Complete Outreach+Events+Media
- [ ] (opt) Ask #marketing to review Outreach+Events+Media
- [ ] (opt) Ask #trading to review/improve Markets section
- [ ] (opt) Find interesting Reddit threads
- [ ] (opt) Ask #general for awesome Decred-related pics and photos of the month
- [ ] (opt) Look for awesome pics and photos
- [ ] (opt) Add a few interesting pics up to 300 px height
- [ ] (opt) Ask quoted people to review their texts
- [ ] Pre-review read: check spelling, grammar, test that links work
- [ ] Ask #writers_room to review
- [ ] (opt) Wait for GitHub dev activity tweet (@lustosa)
- [ ] Resolve all todos: `{}`'s and any URLs outside of Markdown links
- [ ] Carefully check that all people who contributed or gave feedback are in credits
- [ ] Lint
- [ ] Add title image (compress into JPEG with 98% quality to save 2x vs PNG)
- [ ] Remove `{DRAFT}` from title
- [ ] Final read
- [ ] Publish on GitHub with a single commit to `gh-pages` branch
- [ ] Submit to r/decred
- [ ] Ask @karamble to add the post on decredcommunity.org
- [ ] Publish on Medium (@richardred or @Haon)
- [ ] (opt) Verify Medium version, check for formatting issues
- [ ] Tweet via @decredproject. Use either GitHub Pages, Medium or decredcommunity link. Don't forget to add title image.
- [ ] If bugs are found in the published version, quickly add commits to both `gh-pages` and the draft branch
- [ ] Update index and mirrors
- [ ] If extra commits were made to `gh-pages`, rebase and combine them into one
- [ ] Fast-forward master to `gh-pages`
- [ ] Create Git tag from the draft branch, e.g. `archive/draft1901`
- [ ] Delete the draft branch
- [ ] (opt) Update `journal-template.md` in `docs` branch
- [ ] (opt) Update this release checklist template
