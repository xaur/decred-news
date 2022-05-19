# {DRAFT} Decred Journal – {month} {year}

{ _Only remove DRAFT from the title when all other todos are solved, at the very end. Search for `{` to see what's left._ }

{ _Hint: Hints just add context. If it doesn't start with "Hint: ", it is a task. This was a hint._ }

{ _Hint: Read the Guidelines on how to make DJ great: https://github.com/xaur/decred-news/blob/docs/guidelines.md ._}

![{alt text}](../img/{file.ext} "{hover tooltip text}")

_Image: { "Title by @author. Description..." OR just "Description..." }_

{ _Month's highlights, no links here, 5-7 bullets max._

- 
- 
- 
- 
- 

}

Contents: { _Sync ToC at the very end, when all text is finished_ }

- [Development](#development)
- [People](#people)
- [Governance](#governance)
- [Network](#network)
- [Ecosystem](#ecosystem)
- [Outreach](#outreach)
- [Events](#events)
- [Media](#media)
- [Discussions](#discussions)
- [Markets](#markets)
- [Relevant External](#relevant-external)

{ _Add individual sections for high-impact announcements before Development, such as consensus votes, software releases, milestones, major bugs, etc._ }

## Development

The work reported below has the "merged to master" status unless noted otherwise. It means that the work is completed, reviewed, and integrated into the source code that advanced users can [build and run](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c), but is not yet available in release binaries for regular users.

{

- _For each project, cover its most notable dev work._
- _For each project, the order of reporting is "most released first": changes released to end users, merged to master, in progress (work started), discussions and future plans._
- _Add sections for any other project with notable activity._
- _Drop sections without notable updates._

}

<a id="dcrd" />

**[dcrd](https://github.com/decred/dcrd)**

_dcrd is a full node implementation that powers Decred's peer-to-peer network around the world._

{ _Check https://github.com/decred/dcrd/commits/master ._}

- {}

<a id="dcrwallet" />

**[dcrwallet](https://github.com/decred/dcrwallet)**

_dcrwallet is a wallet server used by command-line and graphical wallet applications._

{ _Check https://github.com/decred/dcrwallet/commits/master ._}

- {}

<a id="dcrctl" />

**[dcrctl](https://github.com/decred/dcrctl)**

_dcrctl is a command-line client for dcrd and dcrwallet._

{ _Hint: dcrctl is pulling most of the code from dcrd and dcrwallet. Often there is not much to report and this section can be removed._ }

{ _Check https://github.com/decred/dcrctl/commits/master ._}

- {}

<a id="decrediton" />

**[Decrediton](https://github.com/decred/decrediton)**

_Decrediton is a full-featured desktop wallet app with integrated voting, StakeShuffle mixing, Lightning Network, DEX trading, and more. It runs with or without a full blockchain (SPV mode)._

{ _Check https://github.com/decred/decrediton/commits/master ._}

- {}

<a id="politeia" />

**[Politeia](https://github.com/decred/politeia)**

_Politeia is Decred's proposal system. It is used to request funding from the Decred treasury._

{ _Check Check these repos:_

- _. https://github.com/decred/politeia/commits/master ._
- _. https://github.com/decred/politeiagui/commits/master ._
- _. https://github.com/decred/pi-ui/commits/master ._

}

- {}

<a id="vspd" />

**[vspd](https://github.com/decred/vspd)**

_vspd is server software for running a Voting Service Provider. A VSP votes on behalf of its users 24/7 and cannot steal funds._

{ _Check https://github.com/decred/vspd/commits/master ._}

- {}

<a id="dcrstakepool" />

**[dcrstakepool](https://github.com/decred/dcrstakepool)**

_dcrstakepool is server software for running a Voting Service Provider. This was used before vspd and is now referred to as "legacy VSP"._

{ _Hint: Not maintained anymore, check just in case for now but will remove from template soon._ }

{ _Check https://github.com/decred/dcrstakepool/commits/master ._}

- {}

<a id="dcrpool" />

**[dcrpool](https://github.com/decred/dcrpool)**

_dcrpool is server software for running a mining pool._

{ _Check https://github.com/decred/dcrpool/commits/master ._}

- {}

<a id="dcrlnd" />

**[dcrlnd](https://github.com/decred/dcrlnd)**

_dcrlnd is Decred's Lightning Network node software. LN enables instant and low-cost transactions._

{ _Check https://github.com/decred/dcrlnd/commits/master ._}

- {}

<a id="cspp" />

**[cspp](https://github.com/decred/cspp)**

_cspp is a server for coordinating coin mixes using the CoinShuffle++ protocol. It is non-custodial, i.e. does not hold any funds._

{ _Check https://github.com/decred/cspp/commits/master ._}

- {}

<a id="dcrdex" />

**[DCRDEX](https://github.com/decred/dcrdex)**

_DCRDEX is a non-custodial exchange for trustless trading, powered by atomic swaps._

{ _Check https://github.com/decred/dcrdex/commits/master ._}

- {}

<a id="dcrandroid" />

**[Decred Wallet (Android)](https://github.com/planetdecred/dcrandroid)**

{ _Check https://github.com/planetdecred/dcrandroid/commits ._}

- {}

{ _Also check the common wallet library and report its (notable) changes in the most relevant section (Android, iOS, or GoDCR): https://github.com/planetdecred/dcrlibwallet/commits/master ._}

<a id="dcrios" />

**[Decred Wallet (iOS)](https://github.com/planetdecred/dcrios)**

{ _Check https://github.com/planetdecred/dcrios/commits/master ._}

- {}

<a id="godcr" />

**[GoDCR](https://github.com/planetdecred/godcr)**

_GoDCR is a lightweight desktop wallet app with integrated staking, privacy, and Politeia browsing._

{ _Check https://github.com/planetdecred/godcr/commits/master ._}

- {}

<a id="dcrdata" />

**[dcrdata](https://github.com/decred/dcrdata)**

_dcrdata is an explorer for Decred blockchain and off-chain data like Politeia proposals, markets, and more._

{ _Check https://github.com/decred/dcrdata/commits/master ._}

- {}

<a id="tinydecred" />

**[TinyDecred](https://github.com/decred/tinydecred)**

_TinyDecred is a toolkit for integrating Decred into Python projects. It includes an experimental light GUI wallet based on PyQt5._

{ _Check https://github.com/decred/tinydecred/commits/master ._ }

- {}

<a id="dcrros" />

**[dcrros](https://github.com/decred/dcrros)**

_dcrros is a middleware service that provides access to the Decred network via Rosetta API._

{ _Check https://github.com/decred/dcrros/commits/master ._}

- {}

<a id="dcrdocs" />

**[dcrdocs](https://github.com/decred/dcrdocs)**

_dcrdocs is the source code for Decred [user documentation](https://docs.decred.org/)._

{ _Check https://github.com/decred/dcrdocs/commits/master ._}

- {}

<a id="dcrdevdocs" />

**[dcrdevdocs](https://github.com/decred/dcrdevdocs)**

_dcrdevdocs is the source code for Decred [developer documentation](https://devdocs.decred.org/)._

{ _Check https://github.com/decred/dcrdevdocs/commits/master ._ }

- {}

<a id="dcrweb" />

**[decred.org](https://github.com/decred/dcrweb)**

_dcrweb is the source code for the decred.org website._

{ _Check https://github.com/decred/dcrweb/commits/master ._}

- {}

{ _Check for other new/updated repos in:_

- _. https://github.com/decred ._
- _. https://github.com/planetdecred ._
- _. https://github.com/raedahgroup ._

}

**Other**

- { _Smaller/common things go here._ }


## People

{ _List people who got their first non-trivial commits merged in master branches, in alphabetical order._ }

Welcome to new first-time contributors with code merged to master: {@handle} ([{repo}]({link to user's commits})), ... !

{ _Check CMS, remove if none._ }

Congratulations to new contractors granted the Decred Contractor Clearance (DCC): [{@handle}]({link to most relevant account}).

{ _Welcome new corporate contractors with short intros._ }

{ _Status updates from existing contractors._ }

{ _Interviews with contributors. Link to #media for generic references (e.g. "Check the 3 interviews with devs") or link directly when referencing a specific interview._ }

Community stats as of {date}:

- Politeia users: {} (+{})
- [Twitter](https://twitter.com/decredproject) followers: {} (+{})
- [Reddit](https://www.reddit.com/r/decred/) subscribers: {} (+{})
- [Matrix](https://chat.decred.org/) #general users: {} (+{})
- [Discord](https://discord.gg/GJ2GXfz) users: {} (+{})
- [Telegram](https://t.me/Decred) users: {} (+{})
- [YouTube](https://www.youtube.com/decredchannel) subscribers: {} (+{}), views: {} (+{})

{ _Optional: List/link notable SM dynamics._ }


## Governance

{ _Hint: Currently this is a mix of finances and governance. We may add the separate Finances section in the future._ }

In {month} the new [treasury](https://dcrdata.decred.org/treasury) received {n} DCR worth ${} at month's average rate of ${}. {} DCR was spent to pay contractors, worth ${} at {month}'s rate, or ${} at {prev month}'s billing rate of ${}.

As of {date}, combined balance of [legacy](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) and [new treasury](https://dcrdata.decred.org/treasury) is {n} DCR ({n} million USD at ${n.nn}).

{ _Report any other activity with the legacy or new treasury._ }

{ _High-level recap of decision-making activity and most important events._ }

- {}

{ _Check https://github.com/decredcommunity/proposals/commits/master for updates._ }

See Politeia Digest [issue {}]({}) and [issue {}]({}) for more details on the month's proposals.


## Network

{ _Hint: "Network" tracks key "health" metrics of the fundamental infrastructure._ }

{ _Hint: n, n.n, and n.nn tell how many decimals to keep, e.g. 100, 16.5, 8.63_ }

**Hashrate**: {month}'s [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&scale=linear&bin=block&axis=time) {_set zoom to show the month_} opened at ~{n} Ph/s and closed ~{n} Ph/s, bottoming at {n} Ph/s and peaking at {n} Ph/s throughout the month.

Distribution of hashrate [reported](https://miningpoolstats.stream/decred) by the pools on {date}: {PoolName n%, ...}.

{ _Hint: Fallback link for pool distribution: https://dcrstats.com/pow ._ }

Distribution of 1,000 blocks actually [mined](https://miningpoolstats.stream/decred) before {date}: {PoolName n%, ...}.

**Staking**: [Ticket price](https://dcrdata.decred.org/charts?chart=ticket-price&axis=time&visibility=true-true&mode=stepped) {_monthly zoom_} varied between {n}-{n} DCR, with 30-day [average](https://dcrstats.com/) at {n.n} DCR (+{n.n}). { use same t1-t2 for zoom }

The [locked amount](https://dcrdata.decred.org/charts?chart=ticket-pool-value&scale=linear&bin=block&axis=time) {_monthly zoom_} was {n.nn}-{n.nn} million DCR, meaning that {n.n}-{n.n}% of the circulating supply [participated](https://dcrdata.decred.org/charts?chart=stake-participation&scale=linear&bin=block&axis=time) {_monthly zoom_} in Proof of Stake.

{ _Add a recap of ticket price action if it was interesting._ }

**VSP**: On {date}, ~{n} (+{n}) live tickets were managed by [listed](https://decred.org/vsp/) vspd servers. Collectively the {n} VSPs managed {n.n}% of the ticket pool (+{n.n}%).

**Nodes**: Throughout {month} there were around {n} reachable nodes according to [PD Analytics](https://analytics.planetdecred.org/nodes).

Node versions as of {date} [snapshot](https://nodes.jholdstock.uk/user_agents) ({n} total, dcrd only): { vX.Y.Z - n%, ... }

{ _Optional_ } The share of [mixed coins](https://dcrdata.decred.org/charts?chart=coin-supply&zoom=jz3q237o-la8vk000&scale=linear&bin=day&axis=time&visibility=true-true-true) varied between {n.n}-{n.n}%. Daily [mixed amount](https://dcrdata.decred.org/charts?chart=privacy-participation&bin=day&axis=time) {_monthly zoom_} varied between {n}-{n}K DCR.

{ _Optional_ } Decred's [Lightning Network](https://ln-map.jholdstock.uk/) has seen {} nodes (+{}), {} channels (+{}) with a total capacity of {n.n} DCR (+{n.n}), as of {date}.

{ _Add any interesting analysis or events in the network._ }


## Ecosystem

{ _Hint: "Ecosystem" is about new units of infrastructure or updates from existing: VSPs, exchanges, wallets, OTC desks, payment processors, investors. It is more about user-facing services, businesses, and wider adoption, while Network is more about the backbone. Use bullets or paragraphs, whatever looks best._ }

{ _Check https://github.com/decred/dcrwebapi/commits/master for changes to the VSP list._ }

{ _Check https://github.com/decred/dcrwebapi/pulls for new VSPs under review._ }

{ _Check #services room for news._ }

{ _Check https://github.com/decred/dcrweb/commits/master to detect added/removed services._ }

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.


## Outreach

{ _Summarize outreach/communications/marketing/PR activity for past month and any short-term plans. "Outreach" is anything about "sending our message out". Here is the "big picture" stuff while Events and Media go into the details._ }


## Events

{ _Hint: Summarize any important or interesting facts about each event. Link to https://github.com/decredcommunity/events for detailed reports._ }

**Attended:**

- {}

**Upcoming:**

- {dates} - [{title}]({event link}) - {city}, {country}. {info}

{ _Announcements from events ppl._ }


## Media

{ _Put notable community content efforts or new projects at the beginning. e.g. a new website, new podcast series, or an important guide how to make the network more robust._ }

{ _Hint: For bullet lists below, use the following format: [Sentence case title]({link}) by @author - optional comment._ }

**Selected articles:**

- {}

**Videos:**

- {}

**Audio:**

- {}

**Art and fun:**

- {}

**Translations:**

- {}

**Non-English content:**

- {}


## Discussions

Comm systems news:

- { _e.g. added/removed chant channels, changes how comms work, etc_ }

{ _Hint: Interesting discussions that generated new ideas or perspectives._ }

Selected Reddit posts:

- {}

Selected Twitter discussions:

- {}


## Markets

In {month} DCR was trading between USD {n.nn}-{n.nn} / BTC {n.nnnnn}-{n.nnnnn}. The average daily rate was ${n.nn}.

{ _Optional: Markets overview, USD and BTC price trends, highs and lows, interesting events, interesting analysis._ }

{ _DCRDEX updates, esp. trading volume dynamics._ }


## Relevant External

{ _Hint: Besides dramatic "epic fails", try to also report some "epic wins" in areas relevant to Decred. We can learn from both._ }

{ _Hint: Follow or not follow the suggested grouping of stories below._ }

{ _Cryptocurrency L1 tech: PoW, ASIC resistance, full nodes, network security, etc._ }

{ _L2+ tech: "Smart" contracts, DEX projects._ }

{ _Governance, finances, funding, chain forks, community splits._ }

{ _Relevant exchanges and websites._ }

{ _Other: Regulations, privacy, security, fun._ }

That's all for {month}. Share your updates for the next issue in our [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat room.


## About

This is issue {number} of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from the source after a minimal sanity check. The authors of the Decred Journal cannot verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing and editing: {}
- reviews and feedback: {}
- title image: {}
- funding: Decred stakeholders