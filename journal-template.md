# {DRAFT} Decred Journal – {month} {year}

{

- _Only remove DRAFT from the title when all other todos are solved, at the very end. Search for `{` to see what's left._
- _Hint: Hints just add context. If it doesn't start with "Hint: ", it is a task. This was a hint._
- _Hint: Read the Guidelines on how to make DJ great: https://github.com/xaur/decred-news/blob/docs/guidelines.md_

}

{ _upload title image xxxxxx.1_ }

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
- [Markets](#markets)
- [Relevant External](#relevant-external)


<a id="{some-announcement}" />

## { Some Announcement }

{ _Add individual sections for high-impact announcements, such as consensus votes, software releases, milestones, major bugs, etc._ }


<a id="development" />

## Development

The work reported below has the "merged to master" status unless noted otherwise. It means that the work is completed, reviewed, and integrated into the source code that advanced users can [build and run](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c), but is not yet available in release binaries for regular users.

{

- _For each project, cover its most notable dev work._
- _For each project, the order of reporting is "OLDEST FIRST", or "most released first": changes released to end users, merged to master, in progress (work started), discussions and future plans._
- _Add sections for any other project with notable activity._
- _Drop sections without notable updates._

- _For each project:_
  - _Step 1: Add every commit in chronological order_
  - _Step 2: Organize:_
    - _released, master, progress, future_
    - _user-facing up top, dev stuff down below_
  - _Step 3: Group further and tidy_

}


### dcrd

_[dcrd](https://github.com/decred/dcrd) is a full node implementation that powers Decred's peer-to-peer network around the world._

{ _Sources:_

- https://github.com/decred/dcrd/commits/master
- release branch

}

- {}


### dcrwallet

_[dcrwallet](https://github.com/decred/dcrwallet) is a wallet server used by command-line and graphical wallet apps._

{ _Sources:_

- https://github.com/decred/dcrwallet/commits/master
- release branch

}

- {}


### dcrctl

_[dcrctl](https://github.com/decred/dcrctl) is a command-line client for dcrd and dcrwallet._

{ _Hint: dcrctl is pulling most of the code from dcrd and dcrwallet. Often there is not much to report and this section can be removed._

_Sources:_ https://github.com/decred/dcrctl/commits/master }

- {}


### Decrediton

_[Decrediton](https://github.com/decred/decrediton) is a full-featured desktop wallet app with integrated voting, StakeShuffle mixing, Lightning Network, DEX trading, and more. It runs with or without a full blockchain (SPV mode)._

{ _Sources:_

- https://github.com/decred/decrediton/commits/master
- release branch
- #decrediton
- #hw-wallets

}

- {}


### Politeia

_[Politeia](https://github.com/decred/politeia) is Decred's proposal system. It is used to request funding from the Decred treasury._

{ _Sources:_

- https://github.com/decred/politeia/commits/master
- https://github.com/decred/politeiagui/commits/master
- https://github.com/decred/pi-ui/commits/master
- #politeia

}

- {}


### vspd

_[vspd](https://github.com/decred/vspd) is server software used by Voting Service Providers. A VSP votes on behalf of its users 24/7 and cannot steal funds._

{ _Sources:_

- https://github.com/decred/vspd/commits/master
- release branch

}

- {}


### dcrpool

_[dcrpool](https://github.com/decred/dcrpool) is server software for running a mining pool._

{ _Sources:_ https://github.com/decred/dcrpool/commits/master }

- {}


### Lightning Network

_[dcrlnd](https://github.com/decred/dcrlnd) is Decred's Lightning Network node software. LN enables instant and low-cost transactions._

{ _Sources:_

- https://github.com/decred/dcrlnd/commits/master
- Watch for fast-forward merges! `is:pr merged:2023-08-01..2023-08-31`
- https://github.com/decred/dcrlnlpd/commits/master
- #lndev

}

- {}


### cspp

_[cspp](https://github.com/decred/cspp) is a server for coordinating coin mixes using the CoinShuffle++ protocol. It is non-custodial, i.e. never holds any funds. CSPP is part of StakeShuffle, Decreds privacy system._

{ _Sources:_ https://github.com/decred/cspp/commits/master }

- {}


### DCRDEX

_[DCRDEX](https://github.com/decred/dcrdex) is a non-custodial, privacy-respecting exchange for trustless trading, powered by atomic swaps._

{ _Sources:_

- https://github.com/decred/dcrdex/releases
- release branch
- https://github.com/decred/dcrdex/commits/master
- https://github.com/decred/dexweb/commits/master
- updated PRs `is:pr sort:updated-desc updated:>=2023-07-01 created:<2023-08-01 -merged:<2023-08-01`
- #dexdev
- #dex

}

- {}


### Cryptopower

_[Cryptopower](https://github.com/crypto-power/cryptopower) is a multi-coin desktop GUI wallet for DCR, BTC, and LTC. It runs in a privacy-preserving light SPV mode without needing full blockchains, supports Decred staking, mixing, voting, and other unique features._

{ _Sources:_

- https://github.com/crypto-power/cryptopower
- https://github.com/crypto-power
- #cryptopower-dev
- #cryptopower

}


### dcrdata

_[dcrdata](https://github.com/decred/dcrdata) is an explorer for Decred blockchain and off-chain data like Politeia proposals, markets, and more._

{ _Sources:_

- https://github.com/decred/dcrdata/commits/master
- #dcrdata

}

- {}


### Timestamply

_[Timestamply](https://github.com/decred/dcrtimegui) is a free service for timestamping files powered by Decred blockchain. A timestamp proves that a certain file has existed at a certain moment of time. This has a range of applications in protecting data integrity._

{ _Sources:_

- https://github.com/decred/dcrtime
- https://github.com/decred/dcrtimegui
- https://github.com/decred/dcrtimejs
- #timestamp

}


### Documentation

_[dcrdocs](https://github.com/decred/dcrdocs) is the source code for Decred [user documentation](https://docs.decred.org/)._

{ _Sources:_

- https://github.com/decred/dcrdocs/commits/master
- #documentation

}

- {}


### Dev Docs

_[dcrdevdocs](https://github.com/decred/dcrdevdocs) is the source code for Decred [developer documentation](https://devdocs.decred.org/)._

{ _Sources:_

- https://github.com/decred/dcrdevdocs/commits/master
- #documentation

}

- {}


### decred.org

_[dcrweb](https://github.com/decred/dcrweb) is the source code for the [decred.org](https://decred.org/) website._

{ _Sources:_ https://github.com/decred/dcrweb/commits/master }

- {}


### Bison Relay

_[Bison Relay](https://github.com/companyzero/bisonrelay) is a new social media platform with strong protections against censorship, surveillance, and advertising, powered by Decred Lightning Network._

{ _Sources:_

- https://github.com/companyzero/bisonrelay
- https://github.com/companyzero/bisonrelay-web
- https://github.com/companyzero/sntrup4591761
- #br

}


### Other

- { _Smaller/common things go here._ }

{ _Sources:_

- https://github.com/orgs/decred/repositories
- #dev
- #research
- https://github.com/orgs/companyzero/repositories
- https://github.com/orgs/planetdecred/repositories
- https://github.com/orgs/raedahgroup/repositories
- https://github.com/xaur/decred-news/blob/docs/sources.md#development (more exotic dev sources)

}


<a id="people" />

## People

{ _Discover and greet new first-time contributors. For devs, list people who got their first non-trivial commits merged in master branches. For writers, list authors who published notable Decred content for the first time. Sort by type (dev/writing/etc.), then alphabetically._ }

Welcome the new first-time contributors:

- {@handle} ([{Project}]({ link to user's commits, CT profile, etc. }))

{ _Check CMS, remove if none._ } Congratulations to new contractors granted the Decred Contractor Clearance (DCC): [{@handle}]({ link to most relevant account }).

{

- _Welcome new corporate contractors with short intros._
- _Status updates from existing contractors._
- _Interviews with contributors. Link the interview and add a fun/strong quote._

}

Community stats as of {date} (compared to {date}):

- [Twitter](https://twitter.com/decredproject) followers: {} (+{})
- [Reddit](https://www.reddit.com/r/decred/) subscribers: {} (+{})
- [Matrix](https://chat.decred.org/) #general users: {} (+{})
- [Discord](https://discord.gg/GJ2GXfz) users: {} (+{}), verified to post: {} (+{})
- [Telegram](https://t.me/Decred) users: {} (+{})
- [YouTube](https://www.youtube.com/decredchannel) subscribers: {} (+{}), views: {} (+{})

{ _Optional: List/link notable SM dynamics._ }


<a id="governance" />

## Governance

{ _Hint: Currently this is a mix of finances and governance. We may add the separate Finances section in the future._

_Sources:_

- https://proposals.decred.org/
- https://proposals.decred.org/ - updates on approved props
- https://dcrdata.decred.org/proposals
- https://blockcommons.red/politeia-digest/
- https://github.com/decredcommunity/proposals/commits/master
- #proposals

}

In {month} the new [treasury](https://dcrdata.decred.org/treasury) received {n} DCR worth ${} at {month}'s average rate of ${}. {} DCR was spent to pay contractors, worth ${} at same rate.

A [treasury spend tx]({}) was approved with {} Yes votes and {}% turnout, and mined on {date}. It had {} outputs making payments to contractors, ranging from {} DCR to {} DCR. Most of this DCR was likely paid for {billing month} work, at its billing exchange rate of ${} the TSpend is worth around ${}.

{ _Other interesting facts/stories about the legacy or new treasury._ }

As of {date}, combined balance of [legacy](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) and [new treasury](https://dcrdata.decred.org/treasury) is {n} DCR ({n} million USD at ${n.nn}).

{ _High-level recap of decision-making activity and most important events._ }

- {}

See Politeia Digest [issue {}]({}) for more details on the month's proposals.


<a id="network" />

## Network

{ _Hint: "Network" tracks key "health" metrics of the fundamental infrastructure._

_Sources:_

- https://github.com/bochinchero/dcrsnapcsv
- https://github.com/bochinchero/dcrsnapshots
- #pow-mining
- #pos-voting

}

**Hashrate**: {month}'s [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&scale=linear&bin=day&axis=time) opened at ~{n} PH/s and closed ~{n} PH/s, bottoming at {n} PH/s and peaking at {n} PH/s throughout the month.

Distribution of {} PH/s hashrate [reported](https://miningpoolstats.stream/decred) by the pools on {date}: {PoolName n%, ...}.

{ _Hint: Fallback links for pool distribution: https://poolbay.io/crypto/54/decred , https://dcrstats.com/pow ._ }

Distribution of 1,000 blocks actually [mined](https://miningpoolstats.stream/decred) by {date}: {PoolName n%, ...}.

**Staking**: [Ticket price](https://dcrdata.decred.org/charts?chart=ticket-price&axis=time&visibility=true-true&mode=stepped) varied between {n}-{n} DCR.

The [locked amount](https://dcrdata.decred.org/charts?chart=ticket-pool-value&scale=linear&bin=day&axis=time) was {n.nn}-{n.nn} million DCR, meaning that {n.n}-{n.n}% of the circulating supply [participated](https://dcrdata.decred.org/charts?chart=stake-participation&scale=linear&bin=day&axis=time) in proof of stake.

{ _Add a recap of ticket price action if it was interesting._ }

**VSP**: The [{} listed VSPs](https://decred.org/vsp/) collectively managed ~{n} (+{n}) live tickets, which was {n.n}% of the ticket pool (+{n.n}%) as of {date}.

{ _Optional: mention biggest gainers_ }

**Nodes**: [Decred Mapper](https://nodes.jholdstock.uk/user_agents) observed between {} and {} dcrd nodes throughout the month. Versions of {} nodes seen on {date}: v{} - {n}%, ...

{ _Optional_ } The share of [mixed coins](https://dcrdata.decred.org/charts?chart=coin-supply&zoom=jz3q237o-la8vk000&scale=linear&bin=day&axis=time&visibility=true-true-true) varied between {n.n}-{n.n}%. Daily [mixed volume](https://dcrdata.decred.org/charts?chart=privacy-participation&bin=day&axis=time) varied between {n}-{n}K DCR.

{ _Optional_ } Decred's [Lightning Network](https://ln-map.jholdstock.uk/) explorer has seen {} nodes (+{}), {} channels (+{}) with a total capacity of {n.n} DCR (+{n.n}), as of {date}. These stats are different for each node. For example, @karamble's node reported {} nodes (+{}), {} channels (+{}) and {} DCR (+{}) capacity on same day {}.

{ _Add any interesting analysis or events in the network._ }


<a id="ecosystem" />

## Ecosystem

{ _Hint: "Ecosystem" is about new units of infrastructure or updates from existing: VSPs, exchanges, wallets, OTC desks, payment processors, investors. It is more about user-facing services, businesses, and wider adoption, while Network is more about the backbone. Use bullets or paragraphs, whatever looks best._

_Sources:_

- #ecosystem (should have updates from all sources below)
- https://github.com/decred/dcrwebapi/commits/master (changes to the VSP list)
- https://github.com/decred/dcrwebapi/pulls (new VSPs under review)
- https://github.com/decred/dcrweb/commits/master (for added/removed services)
- #general
- #hw-wallets
- #trading (exchange listings/elistings/incidents)

_Group as below. Alternatively, group as: Voting Service Providers, Wallets, Exchanges, Communication systems, Other news_

}

New services:

- {}

Services lost:

- {}

Other news:

- {}

New services discovered but not tested by the community yet:

- {}

Join our [#ecosystem](https://chat.decred.org/#/room/#ecosystem:decred.org) chat to get more news about Decred services.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.


<a id="outreach" />

## Outreach

{ _Summarize outreach/communications/marketing/PR activity for past month and any short-term plans. "Outreach" is anything about "sending our message out". Here is the "big picture" stuff while Events and Media go into the details._

_Sources:_

- updates for active marketing proposals
- updates for Cypherpunk Times engagement and recruiting
- Decred Vanguard
- Monde PR
- #marketing
- #writers

}


<a id="events" />

## Events

{ _Hint: Summarize any important or interesting facts about each event. Link to detailed reports when available._

_Sources:_:

- https://decredcommunity.github.io/events/index/
- #events

}

**Attended:**

- {}

**Upcoming:**

- {dates} - [{title}]({event link}) - {city}, {country}. {info}

{ _Announcements from events ppl._ }


<a id="media" />

## Media

{

- _Put notable community content efforts or new projects at the beginning. e.g. a new website, new podcast series, or an important guide how to make the network more robust._
- _For bullet lists, use the following format: `[Sentence case title]({link}) by @author - optional comment`._

_Sources:_

- https://twitter.com/decredproject
- https://www.reddit.com/r/decred/new/
- https://www.youtube.com/channel/UCJ2bYDaPYHpSmJPh_M5dNSg/videos
- https://www.youtube.com/results?search_query=decred&sp=CAI%253D
- https://www.tiktok.com/@decred_crypto
- https://anchor.fm/decred-magazine
- https://www.cypherpunktimes.com/page/2/
- https://decred.org/news/
- https://twitter.com/BisonDigest
- Monde PR placements
- Matrix #media
- Matrix #marketing
- Matrix #general
- https://github.com/decredcommunity/translations/blob/master/index.md

}

**Selected articles:**

- {}

**Videos:**

{ _If the video has a useful companion text post on CT, link it to._ }

- {}

**Audio:**

- {}

**Translations:**

- {}

**Non-English content:**

- {}

**Discussions:**

- { _Interesting convos on Matrix/Reddit/Twitter/BR/etc. that generated new ideas or perspectives_ }

**Other:**

- { _e.g. educational posts or anything that does not fit in other categories_ }

**Art and fun:**

- {}


<a id="markets" />

## Markets

In {month} DCR was trading between USDT {n.nn}-{n.nn} and BTC { five decimals }-{ five decimals }. The average daily rate was ${n.nn}.

{ _Optional: Markets overview, USD and BTC price trends, highs and lows, interesting events, interesting analysis. Sources:_

- https://twitter.com/applesaucesome1
- https://www.cypherpunktimes.com/tag/research-and-analytics/
- #trading

}

{ _DCRDEX updates, esp. trading volume dynamics._ }


<a id="relevant-external" />

## Relevant External

{ _Story ideas:_

- ...

}


{ _Hints (all optional):_

_1. Besides dramatic "epic fails", try to also report "epic wins" in areas relevant to Decred. Balance is good and we can learn from both._

_2. Order the stories as follows:_

- _Crypto L1 tech: PoW, ASIC resistance, full nodes, network security, etc._
- _Crypto L2+ tech: "Smart" contracts, DEX projects_
- _Crypto governance, finances, transparency, funding, chain forks, community splits_
- _Relevant exchanges and websites_
- _Regulations, privacy, security_
- _Fun stuff_

}

That's all for {month}. Suggest news for the next issue in our [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat room.


## About

This is issue {number} of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from the source after a minimal sanity check. The authors of the Decred Journal cannot verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing, editing, publishing: {}
- reviews and feedback: {}
- title image: {}
- funding: Decred stakeholders
