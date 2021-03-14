# Decred Journal – February 2021

![abstract art](../img/202102.1.github.png)

_Image: L2 by @saender_

February's highlights:

- v1.6.1 software was released, it adds bug fixes and UX improvements to the 1.6 release
- PoW and PoS upgrade thresholds were met, but not before a ticket voting policy which forces miners to upgrade was released
- PoS participation reached new heights, and the percentage of mixed DCR surged from 31% to 38%
- Kohola, a front-end for dcrwallet geared towards expert users, was introduced and released
- The Decred Journal and Open Source Research 2021 proposals were approved by stakeholder vote

Contents:

- [v1.6.1 Patch Release](#v161-patch-release)
- [Vote on the New Consensus!](#vote-on-the-new-consensus)
- [Development](#development)
- [People](#people)
- [Governance](#governance)
- [Network](#network)
- [Integrations](#integrations)
- [Outreach](#outreach)
- [Events](#events)
- [Media](#media)
- [Community Discussions](#community-discussions)
- [Markets](#markets)
- [Relevant External](#relevant-external)

## v1.6.1 Patch Release

The new [release](https://twitter.com/decredproject/status/1364636813168693252) includes bug fixes and UX improvements for dcrd, dcrwallet, Decrediton, and dcrdex. Most changes have been addressing issues with the new VSP staking and how it plays together with mixing. Importantly, it allows Decrediton users to set consensus vote choices with both legacy and new VSP.

Get the full release notes and downloads [here](https://github.com/decred/decred-binaries/releases/tag/v1.6.1), or read the compressed overview of changes in the sections below. As always, respect the signature [verification](https://docs.decred.org/advanced/verifying-binaries/) ritual to ensure you'll run exactly what was packaged by the devs.

There are still some rough edges in the new VSP + mixing combo, check this [post](https://www.reddit.com/r/decred/comments/m3k31o/161_things_ive_learned/) by u/mowmowbeans to learn about the workarounds.

To get up to speed with Decrediton updates check @Exitus' quick [mixing](https://www.youtube.com/watch?v=QC65PBNwAK4) and [staking](https://www.youtube.com/watch?v=olWfTqw16OQ) video tutorials.

## Vote on the New Consensus!

Voting to activate the new decentralized treasury has started on Mar 12 and will run until Apr 9.

To get informed, read the original [proposal](https://proposals.decred.org/proposals/c96290a), the technical [spec](https://github.com/decred/dcps/blob/master/dcp-0006/dcp-0006.mediawiki), or watch the [explanation](https://www.youtube.com/watch?v=BdTLKAassvc) by @matheusd (starts around 14 min).

If you haven't set your voting preferences yet, please [do so now](https://www.reddit.com/r/decred/comments/lu1af0/psa_upcoming_decentralized_treasury_consensus/) so your desired vote is cast when any of your tickets vote. The correct id for the new vote is `treasury`.

To watch how the voting unfolds see the voting [dashboard](https://voting.decred.org/) or the [visualization](https://explorer.dcrdata.org/agenda/treasury) at dcrdata.

## Development

The work reported below has the "merged to master" status unless noted otherwise. It means that the work is completed, reviewed, and integrated into the source code that advanced users can [build and run](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c), but is not yet available in release binaries for regular users.

**[dcrd](https://github.com/decred/dcrd)**

The v1.6.1 patch release shipped the following changes:

- notification logic [modified](https://github.com/decred/dcrd/pull/2597) to force proof-of-work miners to upgrade so that voting on the new consensus changes can commence
- fixed a rare [issue](https://github.com/decred/dcrd/pull/2582) where connections might not be reestablished after a network outage

In development towards the [next release](https://github.com/decred/dcrd/milestone/26), this month's highlight is the addition of a [UTXO cache](https://github.com/decred/dcrd/pull/2591) that cuts initial blockchain sync time by ~33% at the cost of some extra memory. It also significantly speeds up block processing during normal operation and reduces wear and tear on the storage medium by allowing entries that are created and spent between flushing intervals to avoid being written at all. UTXO cache is a required step towards [multi-peer](https://github.com/decred/dcrd/issues/1145) parallel block downloading.

Another highlight is the [introduction](https://github.com/decred/dcrd/pull/2579) of Age-Partitioned Bloom Filters. APBF is a lookup device that can quickly tell if it contains an element. It can track _a lot_ of data while using little memory, at the cost of a controlled rate of false positives. Unlike classic Bloom filters, it can handle an unbounded amount of data by aging and discarding old items. The motivation for adding APBFs to Decred is to replace the LRU (least recently used) cache used to continuously track what data other peers are known to have. For a concrete example, the memory to track addresses known by 125 peers is reduced from ~200 to ~5 MiB when using APBFs. Also, the package will be [useful](https://matrix.to/#/!zefvTnlxYHPKvJMThI:decred.org/$ulmCeMPuDSSmt3KTB09fJpypa4fpooFILTXKtQNWUCg) for other projects like wallet, DEX, mobile wallets, etc. Read the details in full glory in the [PR](https://github.com/decred/dcrd/pull/2579) and the [README](https://github.com/decred/dcrd/tree/master/container/apbf).

Other merged work:

- primary operations in `apbf` package made more than two times [faster](https://github.com/decred/dcrd/pull/2584) with smart bit-level math
- tracking of recently [confirmed](https://github.com/decred/dcrd/pull/2580) transactions and [addresses](https://github.com/decred/dcrd/pull/2583) known by peers switched to use APBFs
- tracking of recently [rejected](https://github.com/decred/dcrd/pull/2590) transactions also switched to APBFs, with extra benefits of lowering bandwidth usage in high rejection scenarios while simultaneously increasing robustness against malicious peers
- `reject` message [deprecated](https://github.com/decred/dcrd/pull/2586) towards its eventual removal in future versions (read [this](https://github.com/decred/dcrd/issues/2546) for a list of privacy and correctness issues with this message)

**[dcrwallet](https://github.com/decred/dcrwallet)**

Changes shipped with v1.6.1 patch:

- new gRPC method to set ticket [vote choice](https://github.com/decred/dcrwallet/pull/1981) at the associated VSP via the new vspd protocol (used by Decrediton)
- when the account only has a single output, create an extra transaction to make enough [outputs](https://github.com/decred/dcrwallet/pull/1980) for a VSP ticket purchase, and use the resulting [fee](https://github.com/decred/dcrwallet/pull/2005) output (fixes the "not enough utxos" [error](https://www.reddit.com/r/decred/comments/lebx71/error_when_trying_to_purchase_tickets_with/))
- skip [unpublished](https://github.com/decred/dcrwallet/pull/1985) transactions when selecting outputs and clear unpublished status when the tx is mined (fixes certain double spend cases)
- consider [tx fees](https://github.com/decred/dcrwallet/pull/1992) when mixing to avoid unmixable outputs
- fixed outputs from unpublished transactions being included in the [spendable](https://github.com/decred/dcrwallet/pull/2002) balance
- fixed a chance to pay a very [high fee](https://github.com/decred/dcrwallet/pull/2002) during mixing (this was a regression between v1.6.0 and v1.6.1, i.e. did not affect any release)
- updated salsa20 and blake2b [dependencies](https://github.com/decred/dcrwallet/pull/1998) to prevent possibility memory corruption
- return [error](https://github.com/decred/dcrwallet/pull/1990) from `signrawtransaction` if the transaction has no inputs
- save [mixed](https://github.com/decred/dcrwallet/pull/1989) output transactions and watch outputs

**[Decrediton](https://github.com/decred/decrediton)**

Changes shipped with v1.6.1 patch:

- setting consensus vote [choice](https://github.com/decred/decrediton/pull/3200) implemented for vspd tickets
- [disable](https://github.com/decred/decrediton/pull/3231) some buttons while mixer, auto-buyer or ticket purchases are running to avoid possible issues
- disable the [auto-buyer](https://github.com/decred/decrediton/pull/3182) when switching between legacy and vspd modes to prevent unexpected ticket purchases
- add [sanity](https://github.com/decred/decrediton/pull/3230) checks for ticket purchasing to prevent malformed legacy VSP tickets
- support for filtering transactions by multiple [criteria](https://github.com/decred/decrediton/pull/3194)
- improved layout of [staking stats](https://github.com/decred/decrediton/pull/3205) and [tx history](https://github.com/decred/decrediton/pull/3195) on small screens
- show different icons for mixed and unmixed [accounts](https://github.com/decred/decrediton/pull/3225)
- show a meaningful [message](https://github.com/decred/decrediton/pull/3252) explaining why sometimes fewer tickets are purchased than requested
- show a [timeout](https://github.com/decred/decrediton/pull/3199) error when not receiving VSP status response within 5 seconds
- show [unconfirmed](https://github.com/decred/decrediton/pull/3254) balances on Overview and Accounts
- better [names](https://github.com/decred/decrediton/pull/3219) for tabs and labels
- added Traditional Chinese [translation](https://github.com/decred/decrediton/pull/3086)
- continued migration to functional components using hooks and CSS modules
- increased automated test coverage
- 22 bug fixes

Merged in master:

- migrated to [grpc-js](https://github.com/decred/decrediton/pull/2936) dependency to reduce build time and binary size
- apply UI [language](https://github.com/decred/decrediton/pull/3134) change to menu bar and context menu without restarting Decrediton
- fixed [CPU-hungry](https://github.com/decred/decrediton/pull/3123) animations on Privacy pages
- 3 other bug fixes

**[Politeia](https://github.com/decred/politeia)**

- end-to-end [tests](https://github.com/decred/politeiagui/pull/2297) for admin account

CMS:

- [code stats](https://github.com/decred/politeiagui/pull/2299) for subcontractors listed in the invoice
- show [more data](https://github.com/decred/politeiagui/pull/2298) by default to prevent missing new invoices
- UI fixes

Most of the work has again been focused on the new storage backend. To differentiate Decred implementation from raw tlog a new term "tstore" was introduced, meaning a combination of Trillian transparency logs and the key-value store holding the actual data. The tstore [pull request](https://github.com/decred/politeia/pull/1180) has accumulated 438 commits since Apr 2020 and is changing more than 40K lines of code.

Most recent backend changes concerned how data is stored in unvetted and vetted states. On the frontend, the devs are adjusting the [GUI](https://github.com/decred/politeiagui/pull/2306) to backend API changes.

> I'm pretty excited about the new plugin architecture. It makes it possible to spin up different Politeia applications without needing to write any code, using just config options. Once the same plugin architecture is added to politeiawww for user features, the whole thing will be configurable. ([@lukebp](https://matrix.to/#/!ueeciPqvqEsPyPCJkp:decred.org/$fDljYk8O9Wac_LFh9W-k7PRuPJdVk-bz4OTVfTw6sdY))

**[dcrpool](https://github.com/decred/dcrpool)**

- support for [reverse proxy](https://github.com/decred/dcrpool/pull/301) deployments
- various improvements for the [Stratum](https://github.com/decred/dcrpool/pull/304) mining protocol
- fixed hash calculation spanning multiple [cycles](https://github.com/decred/dcrpool/pull/305)

**[dcrlnd](https://github.com/decred/dcrlnd)**

- check that correct wallet account is used when [unlocking](https://github.com/decred/dcrlnd/pull/106) (this allows to present a meaningful message in Decrediton)

**[cspp](https://github.com/decred/cspp)**

- validate that clients pay enough transaction [fees](https://github.com/decred/cspp/pull/58) (and close a DoS vector)
- remove [timed-out](https://github.com/decred/cspp/pull/60) clients to prevent possible server hangs
- isolate state for different [runs](https://github.com/decred/cspp/pull/61) to prevent possible aborted mixes

**[dcrdex](https://github.com/decred/dcrdex)**

Patch v0.1.5 is out fixing a few rough edges:

- handle orders that have somehow [lost](https://github.com/decred/dcrdex/pull/967) their funding coins
- make client init and redeem requests [asynchronous](https://github.com/decred/dcrdex/pull/911) to not block actions that could occur in parallel
- retry contract audits when [resuming](https://github.com/decred/dcrdex/pull/965) trades on startup and login, to prevent matches from being incorrectly revoked
- blake2 dependency [updated](https://github.com/decred/dcrdex/pull/982) to prevent silent memory corruption

Get the release notes and downloads [here](https://github.com/decred/decred-binaries/releases/tag/v1.6.1#dcrdex-v015), or grab [dcrinstall](https://github.com/decred/decred-release/releases) and run `dcrinstall --dcrdex` to download, verify and configure the programs automatically. In any case, [verify](https://docs.decred.org/advanced/verifying-binaries/) downloaded files to ensure they came unmodified.

Merged in master towards the v0.2 release:

- [estimate](https://github.com/decred/dcrdex/pull/958) low, high, and max possible fees during swap and redemption transactions to offer additional clarity on fees instead of just showing the worst-case value
- write a [backup](https://github.com/decred/dcrdex/pull/949) file prior to upgrading the database
- switch client from btcsuite's to Decred's [rpcclient](https://github.com/decred/dcrdex/pull/938) because the latter [supports](https://github.com/decred/dcrdex/issues/841) request cancellation
- move wallet locking code during [shutdown](https://github.com/decred/dcrdex/pull/928) to a better place

You can track what's coming on the milestone pages for [0.2](https://github.com/decred/dcrdex/milestone/6) (server market data, UI+backend improvements) and [0.3](https://github.com/decred/dcrdex/milestone/12) (SPV support, BCH pair, Decred 1.7).

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

- updated [French](https://github.com/planetdecred/dcrandroid/pull/535) translation
- codebase formatting and [cleanup](https://github.com/planetdecred/dcrandroid/pull/533)
- UI tweaks

[dcrlibwallet](https://github.com/planetdecred/dcrlibwallet) base library updated to [restart](https://github.com/planetdecred/dcrlibwallet/pull/156) sync when necessary and support external [loggers](https://github.com/planetdecred/dcrlibwallet/pull/178) (for easier embedding in other software).

**[dcrios](https://github.com/planetdecred/dcrios)**

- allow users to create [watch-only](https://github.com/planetdecred/dcrios/pull/734) wallet from the splash screen (without creating a new regular wallet first)
- added debug page to view the connected [peers'](https://github.com/planetdecred/dcrios/pull/730) details
- UI and translation tweaks

**[godcr](https://github.com/planetdecred/godcr)**

- added [Security Tools](https://github.com/planetdecred/godcr/pull/299) UI and [logic](https://github.com/planetdecred/godcr/pull/315) for Verify Message and Validate Address tools
- implemented logic for [Settings](https://github.com/planetdecred/godcr/pull/307) page
- implemented [vspd](https://github.com/planetdecred/godcr/pull/263) staking support
- implemented StakeShuffle account [mixing](https://github.com/planetdecred/godcr/pull/312)
- implemented [watch-only](https://github.com/planetdecred/godcr/pull/318) wallet import

**[dcrros](https://github.com/decred/dcrros)**

- [updated](https://github.com/decred/dcrros/pull/19) to comply with the Rosetta spec version 1.4.10
- added a full end-to-end [test suite](https://github.com/decred/dcrros/pull/18) to assert correct dcrros behavior, including running the required Data and Construction API tests on a local simnet that exercises a large number of situations actually found on chain

**[docs](https://github.com/decred/dcrdocs)**

- command-line [Buying Tickets](https://docs.decred.org/wallets/cli/dcrwallet-tickets/) page [updated](https://github.com/decred/dcrdocs/pull/1148) with steps for v1.6

**Kohola**

@peter\_zen [shared](https://matrix.to/#/!aNnAOHkWUdNcEXRGjJ:decred.org/$uc4-7jDq7LehB55bK3sAjq9qL-g2WDJ8wOW5HZTvknI):

> Announcing a project I and @bgptr have been working on last year: [kohola](https://github.com/peterzen/kohola)
> 
> Kohola is a dcrwallet frontend I started for my own needs which weren't covered by Decrediton. It's not feature complete yet but I've been using it as my production wallet. Work on it stalled some months ago due to other priorities but I thought I'd share it in its present state as other peeps may find it useful. In case it proves some usefulness it would be great to finish it.

From the [readme](https://github.com/peterzen/kohola), this wallet is intended for expert users and offers features like encrypted configuration, solo staking support, coin control, and more. The app is written in Go and TypeScript using React and Redux frameworks. Notably, Kohola means "whale" in Hawaiian.

Other:

- u/interfux announced Debian/Ubuntu [packages](https://www.reddit.com/r/decred/comments/lr8kut/debianubuntu_packages_for_decred_software/) and an unofficial APT repo for easy installation and updating of Decred command-line programs. Feedback is welcome, especially from experienced packagers to push it further and ultimately publish in official Debian/Ubuntu repos.
- @dezryth shared a Python [program](https://github.com/dezryth/VotedTicketNotifier) that will send push notifications to your mobile device when your tickets vote
- most projects are now building and testing with Go 1.16

## People

Welcome to new first time contributors with code merged to master: @bochinchero ([dcrlnd](https://github.com/decred/dcrlnd/commits?author=bochinchero)) and @fintechtrades ([dcrdocs](https://github.com/decred/dcrdocs/pull/1150))!

@arij was interviewed on the Decred in Depth podcast, see [Media](#media).

Community stats as of Mar 1:

- [Twitter](https://twitter.com/decredproject) followers: 42,922 (+1,121)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 10,559 (+358)
- [Matrix](https://chat.decred.org/) #general users: 382 (+38)
- [Discord](https://discord.gg/GJ2GXfz) users: 1,444 (-473) - pruned inactive users
- [Telegram](https://t.me/Decred) users: 2,518 (+90)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,420 (+100), views: 175K (+6K)
- [LinkedIn](https://www.linkedin.com/company/decredproject) followers: 978 (+16)
- GitHub [dcrd](https://github.com/decred/dcrd) stars: 584 (+9), forks: 252 (+3)

Notable changes detected for the [tracked](https://github.com/decredcommunity/social-media-stats) accounts:

- Twitter, Reddit, and YouTube listed above all got a higher than usual increase in following and views
- [CoinMarketCap](https://coinmarketcap.com/currencies/decred/) page got another +3K watchers to 29K
- [DecredKorea](https://twitter.com/DecredKorea) and [DecredNederland](https://twitter.com/DecredNederland) Twitter accounts have emerged in Jan and started tweeting in Korean and Dutch
- [DecredDEX](https://twitter.com/DecredDEX) has joined [decredexplorer](https://twitter.com/decredexplorer) and now we have two product-focused Twitter accounts
- [@Checkmate](https://twitter.com/_Checkmatey_) gained +30% followers (to 5K) and posted 1.2K tweets at a crazy rate of ~41/day
- [ConsensusRough](https://twitter.com/ConsensusRough) got +18% followers, to 438

## Governance

In February the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 10,444 DCR and spent 3,010 DCR (actually payments didn't go out until Mar 2). Using February's daily average DCR/USD rate of $113.76, this is $1.2M received and $342K spent. At January's average daily rate of $54.25, the USD figure billed for past work is $163K. As of Mar 3, the Treasury balance is 653,000 DCR (97.2 million USD at $148.86).

After the record-breaking turnout for two proposals at the start of Feb (covered in the [last issue](202101.md#governance)), the rest of the month was relatively quiet, with two further proposals being approved.

- The Decred Journal 2021 [proposal](https://proposals.decred.org/proposals/1d74b88) was approved with 92.4% Yes votes and turnout of 51%. The max amount of funding requested for the year is $39,000, and it also covers Politeia Digest and all of the associated design work. Thanks to all the stakeholders who voted for the Journal's first solo proposal! Don't hesitate to share your thoughts on [Reddit](https://www.reddit.com/r/decred/search?q=decred+journal&restrict_sr=on&t=all&sort=new), [GitHub](https://github.com/xaur/decred-news/issues) or [Matrix](https://chat.decred.org/#/room/#writers:decred.org), especially if you [voted No](https://explorer.dcrdata.org/proposal/decred-journal-2021) (we can survive the criticism).

- The Open Source Research 2021 [proposal](https://proposals.decred.org/proposals/020b8b0) from @richard-red was approved with 75.4% Yes votes and turnout of 60%. The requested budget has increased to $40,000, and $9,150 of this is set aside for the expansion of @bee's open data collection initiative. 

@ammarooni posted a [reflection](https://twitter.com/Ammarooni/status/1359352089714061313) on his book [proposal](https://proposals.decred.org/proposals/9e1d644) and is looking for some honest feedback.

## Network

**Hashrate**: February's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kkf13di6-kltwy2po&scale=linear&bin=block&axis=time) opened at ~428 Ph/s and closed ~420 Ph/s, bottoming at 278 Ph/s and peaking at 537 Ph/s throughout the month.

Pool hashrate [distribution](https://miningpoolstats.stream/decred) as of Mar 1: Poolin 36%, Antpool 34%, F2Pool 8%, Luxor 2%, BTC.com 1.5%, Huobipool 0.8%, Coinmine 0.08%, UUPool 0.03%, unknown 18%.

Instant snapshots are too volatile, so compare that to how 1,000 blocks (3.5 days) mined before Mar 1 have been distributed: Antpool 41%, Poolin 29%, easy2mine 11%, F2Pool 6%, Luxor 1.5%, Huobipool 0.4%, unknown 11%.

UUPool's reported hashrate has dropped from the top spot to the bottom and it looks like its miners have migrated to Antpool and F2Pool. New unidentified addresses are also showing up.

**Staking**: [Ticket price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kkf13di6-kltwy2po&axis=time&visibility=true-true&mode=stepped) varied between 154.3-220.4 DCR, with 30-day [average](https://dcrstats.com/) at 181.7 DCR (+8.5). The [locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kkf13di6-kltwy2po&scale=linear&bin=block&axis=time) was 6.74-7.30 million DCR, meaning that 53.6-57.7% of the circulating supply [participated](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kkf13di6-kltwy2po&scale=linear&bin=block&axis=time) in proof-of-stake.

It looks like we are [breaking](https://twitter.com/michae2xl/status/1359609723541213186) a record every month in terms of both ticket price and participation!

**Nodes**: Throughout February there were around 220 reachable nodes according to [dcrextdata](https://dcrextdata.planetdecred.org/nodes). Average version distribution from dcr.farm: 35% dcrd v1.6.0, 10% dcrd v1.6.1, 10% dcrd v1.5.2, 7% dcrd v1.5.1, 5% dcrd v1.6 dev and RC builds, 4% dcrd v1.7 dev builds, 2% dcrd v1.5.0, 1.5% dcrd v1.5 dev and RC builds, 9% dcrwallet v1.6.0, 4% dcrwallet v1.6.1, 3% dcrwallet v1.5.1, ~9% others.

[charts.dcr.farm](https://charts.dcr.farm/) has been shut down due to low demand and high operating costs to keep it running in a sustainable way. We thank the operators for all the network insights shared over the years. dcr.farm's legacy and new [VSP](https://dcr.farm/) are still operational.

The share of [mixed coins](https://explorer.dcrdata.org/charts?chart=coin-supply&zoom=jzk7rn6n-kmfblq6m&bin=day&axis=time&visibility=true-true-true) has grown from 31% to 38% in Feb alone, possibly thanks to the GUI for it added in v1.6. [@CoinShuffle_BOT](https://twitter.com/CoinShuffle_BOT) posts mixing stats daily.

Decred's [Lightning Network](https://ln-map.jholdstock.uk/) has seen 30 nodes (+2), 56 channels (+9) with a total capacity of 16.8 DCR (+8.5), as of Mar 1.

@matheusd shared some ticket splitting [stats](https://www.reddit.com/r/decred/comments/lj2her/og_ticket/gnj3zqq/): over almost 3 years 2,679 split tickets were purchased at an average rate of 81/month, meaning that roughly 0.2% of tickets are being split. This was discussed in the context of v1.6 and the new vspd staking where ticket splitting is not supported. A new splitting/matching protocol and a rewrite of both server and client are required to make it work with vspd, which is unlikely to happen at this time given the low demand.

## Integrations

Three VSPs have enabled support for the new vspd staking: [decredvoting.com](https://decredvoting.com/), [ibitlin.com](https://dcrpool.ibitlin.com/), and [coinmine.pl](https://vsp.coinmine.pl). We now have a total of 11 vspd instances and 17 legacy VSP instances.

The [VSP listing](https://decred.org/vsp/) was updated to show vspd tickets along the legacy ones. As of Mar 1, vspd servers held 4.4K live tickets, or 11% of the target ticket pool. Legacy VSP servers held 6.5K live tickets, or 16% of the target.

[SwapSwop.io](https://swapswop.io/) exchange platform came to [say hi](https://www.reddit.com/r/decred/comments/lfgr64/buy_dcr_at_swapswopio_a_crypto_exchange_platform/) on r/decred and answered a few questions about liquidity sources, jurisdiction, and their KYC processes. DCR was [listed](https://twitter.com/swapswopio/status/1308107303032369152) in Sep 2020.

A new [#services](https://chat.decred.org/#/room/#services:decred.org) public chat room welcomes everyone to collect information about the growing Decred ecosystem (exchanges, payment processors, VSPs - anything).

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Several Decred contributors answered all kinds of questions in Decred AMA on [r/CryptoCurrency](https://www.reddit.com/r/CryptoCurrency/comments/lqlone/decred_ama_ask_us_about_privacy_daos_lightning/). The thread got 171 comment and 140 upvotes.

@elima\_iii has started the second season of the Decred in Depth series, featuring new guests and more community engagement. Questions to guests are collected [on Twitter](https://twitter.com/elima_iii/status/1363280047059132417) (even more for the [@matheusd](https://twitter.com/elima_iii/status/1365424755906670595) episode), video of both host and guest is available and YouTube is the primary location now.

@pavel shared an [update](https://github.com/decredcommunity/proposals/blob/master/proposals/2bf72e/updates/20210208.md) for the withDecred [proposal](https://proposals.decred.org/proposals/2bf72e6):

> Due to the massive price action in last weeks, I've suspended the giveaways as it seems no longer necessary to generate social buzz. At the time of activity, [@withDecred](https://twitter.com/withdecred) Twitter account had around 100K impressions monthly and generated some good conversations (and some shilling as well). (...) I'm now thinking how to go forward from here with WithDecred activities (web + Twitter), for the moment I'm supporting community-created content. If you have some suggestions, feel free to ping me [here](https://chat.decred.org/#/room/#proposals:decred.org) or on [Twitter](https://twitter.com/paveldcr).


Monde PR's achievements for February:

- created/pitched 3 stories to finance and crypto publications
- responded to 3 requests for comments
- secured 2 media interviews

## Events

Attended:

- Feb 3 - [Decred 5 Years Giveaway](https://decredcommunity.github.io/events/index/20210203.1) - Internet. Decred in Spanish team organized a sophisticated giveaway to mark Decred's 5th anniversary. A total of $130 in DCR was awarded for various tasks like retweets, answering questions (after digging some [dcrdata](https://explorer.dcrdata.org/)), answering "what do you like about Decred?", or competing in a meme generation. This activity engaged more than 60 people, generated over 57K Twitter impressions, and onboarded 100+ Twitter followers and 40+ [Telegram](https://t.me/DecredES) users. Details in the [report](https://decredcommunity.github.io/events/index/20210203.1).
- Feb 6 - [Blockchain, AI, and Big Data](https://decredcommunity.github.io/events/index/20210206.1) - Casablanca, Morocco. @arij and OMJD organized an event to mark Decred's 5th anniversary. There were 3 talks on machine learning, big data, and blockchains. In the latter, @arij talked about how Decred blockchain was used in Brazil municipal elections. 20 people were expected but 40 showed up, and ~500 watched it live. In the end, there was a small celebration of the anniversary _(involving... hold on)_.
- Feb 9 - [Decred intro and features](https://decredcommunity.github.io/events/index/20210209.1) - Internet. @michae2xl was invited by Monnos (Brazilian exchange that listed DCR in [January](202101.md#integrations)) to introduce Decred in an Instagram live. Together with Rodrigo Soeiro (CEO) they have addressed new people in the space, showed Decred's products, and discussed their potential.
- Feb 20 - [Alternative Consensus: Let’s Talk PoS](https://decredcommunity.github.io/events/index/20210220.1) - Internet. @elian talked all things Decred with [Criptodemia](https://twitter.com/criptodemia) and [Kevin Negocios](https://twitter.com/KevinNegocios) from [Veinte Exchange](https://twitter.com/Veinte_ven) of Venezuela in a 1+ hour livestream.

![Decred Cake 3](../img/202102.3.github.jpg)

Upcoming:

- Mar 12-14 - [Hackathon Nayarit 2021](https://www.facebook.com/EduNayarit/posts/2982126628674008) - Internet. Decred in Spanish will sponsor the hackathon organized by the Ministry of Education of Nayarit. To prepare participants, the Spanish team hosted Blockchain Education training week, consisting of 5 webinars.

## Media

Selected articles:

- Decred v1.6 with co-founder & project lead, Jake Yocom-Piatt ([coinscrum.com](https://www.coinscrum.com/decred-with-jake-yocom-piatt/)) - a Jan video reworked into an article, compares the new treasury code to "minimally complex hardwired smart contact" and explains key features of v1.6 in simple terms
- DCRDEX was listed among the top DEXes to watch in 2021 in the January research [report](https://xangle.io/research/600a3251b7cb8c849dfa26b9) by Xangle

Videos:

- Decred News Update - Feb 14th - Massive 1.6 release, vote for $75M DAO, LN, privacy, & more! by @Exitus ([youtube](https://www.youtube.com/watch?v=f2ooNJXpR7I))
- Decred Privacy Tutorial: Mix your coins by @Exitus ([youtube](https://www.youtube.com/watch?v=QC65PBNwAK4))
- Insaf Nori interview Decred in Depth (live) by @elima\_iii ([youtube](https://www.youtube.com/watch?v=hUXk1GWhE-0))
- Being your own bank by Society Decentralised ([youtube](https://www.youtube.com/watch?v=Vb-9vvU0fDU))
- Decred Price Analysis - 24th February 2021 by Brave New Coin ([youtube](https://www.youtube.com/watch?v=O6iTIABl2Lw))

Audio:

- Rough Consensus 17: Spidey reunion. The long lost co-host @mr.black rejoins the pod to talk about crypto and finance. ([libsyn](https://roughconsensus.libsyn.com/episode-17-spidey-reunion))
- past Decred in Depth episodes (up to 33rd) have been uploaded to the main YouTube [channel](https://www.youtube.com/decredchannel)

Art and fun:

- @karamble's Decred v1.6 digital announcement [clip](https://twitter.com/karamblez/status/1356921573647745024) _(try spotting "taco"!)_
- glitchy and loud 5th anniversary [clip](https://twitter.com/New_Copernicus/status/1357574854535487488) by @New\_Copernicus
- the ultimate explanation of how [atomic swaps](https://twitter.com/RichardRed0x/status/1356719226724220930) work by @richardred
- [The Rewards](https://www.reddit.com/r/decred/comments/lfxqef/the_rewards/) by @AGNFAB1
- "I wish to be [irrisistible](https://twitter.com/Decred_ES/status/1358855083396653062) to men!"
- introducing [Decred Pączki](https://twitter.com/LolekBolek74/status/1359866192538787843) (doughnuts)

![Decred doughnuts](../img/202102.2.github.jpg)

Translations:

- Decred News Update Jan 24 - with [Spanish](https://www.youtube.com/watch?v=Quf8u1Ksm4M) subtitles by @francov\_
- Building a transparent future with the Decred blockchain - [in Arabic](https://insaf01.github.io/decred-arabic/articles/building-a-transparent-future-with-decred-blockchain.html) by @arij and @abdulrahman4
- Decred Journal January 2021 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), and Spanish (@francov\_). Thank you all for spreading Decred news!

## Community Discussions

There have been more attempts to scam people recently. Please remember that real developers and admins will never DM you with offers of free money or technical assistance. Pay close attention to _user display name_ and _user ID_ you chat with to avoid smart ways to [impersonate](https://twitter.com/GrapheneOS/status/1365881076229488641). Tell your friends to stay vigilant, too.

Selected Reddit posts:

- an idea to rename tickets to ["OG tickets"](https://www.reddit.com/r/decred/comments/lj2her/og_ticket/) and call its 1/10th part a regular "ticket"
- one of the [price discussions](https://www.reddit.com/r/decred/comments/llnzvu/dcr_breaking_through_all_time_high_price_usd/) became unusually intelligent and touched the topic of recruiting (we keep saying it: not only developers are [wanted](https://www.reddit.com/r/decred/comments/llnzvu/dcr_breaking_through_all_time_high_price_usd/gnr3kpf/))
- DCRDEX vs [Bisq](https://www.reddit.com/r/decred/comments/ln7co5/dcrdex_vs_bisq/)
- a few interesting facts about [seed words](https://www.reddit.com/r/decred/comments/lo72lf/discussion_around_33_word_seed_vs_bip_39/) and metal wallets

Selected Twitter discussions:

- @jy-p reminds [why](https://twitter.com/behindtext/status/1363118198749597698) we are still here
- another great [thread](https://twitter.com/cburniske/status/1362146220123201536) from @cburniske

> As someone who's followed @decredproject since 2016, the strength of its community, fundamentals, and market traction thus far in 2021 has surprised even me. ([@cburniske](https://twitter.com/cburniske/status/1362146231116460032))

## Markets

In February DCR was trading between USD 66.95-169.90 / BTC 0.0018-0.0030. The average daily rate was $113.76.

@Checkmate posted a [mega](https://twitter.com/_Checkmatey_/status/1358968202898755584) on-chain thread with many (all?) indicators going ATH. Feb 9 prediction "I would be surprised if the train slows down from here, it's just not in character!" was correct.

Unusually large bids have been [observed](https://twitter.com/_Checkmatey_/status/1363709306885922826) on Binance.

[DCRDEX](https://dex.decred.org/) has traded 390K DCR and 1K BTC in February, averaging to 14K DCR and 36 BTC daily. The price varied between 0.0019-0.0030 with an average of 0.0026.

## Relevant External

Yearn Finance was February's largest DeFi [Fail](https://cryptobriefing.com/hacker-spends-8-3-million-fees-attack-yearn-finance/), with a flash loan attack exploiting its users for $11 million. In an interesting development for this kind of attack, most of the exploited funds were paid in [fees](https://twitter.com/FrankResearcher/status/1357639434380992512) to various liquidity pools and staking services, with just $2.7 million ending up in the attacker's wallet, and the rest presumably fuelling the DeFi economy. The victims of the attack have been [compensated](https://twitter.com/iearnfinance/status/1359108691677614080) from the new pool of YFI Treasury funds that were recently minted - within 4 days of the hack the Yearn team were able to mobilize 9.7 million DAI to distribute, and no token voting was required. YFI and the Treasury are currently under the direct control of the Multisig holders, and that "empowerment" is being [extended](https://gov.yearn.finance/t/yip-59-temporarily-extend-multisig-empowerment/9746) until May 24.

Yearn Finance is also [changing](https://gov.yearn.finance/t/yip-56-buyback-and-build/8929) up its Treasury and governance funding model [significantly](https://gov.yearn.finance/t/yip-56-buyback-and-build/8929), major changes include scrapping YFI staking because of its uncompetitive yield and instead switching to a buyback model and allowing YFI holders who have deployed their tokens in a liquidity pool to also use them to vote. 

Bitcoin developers are in the [process](https://twitter.com/AndreCronjeTech/status/1359934584612212738) of deciding how the [Taproot](https://bitcoinmagazine.com/technical/taproot-coming-what-it-and-how-it-will-benefit-bitcoin) upgrade should be activated, with the point of contention being whether the Bitcoin Core update should ship with a setting that has it activating at the end of the signalling period regardless of whether the supermajority threshold is met (like the User Activated Soft Fork) or take a more cautious approach and avoid forcing the issue initially. Miner signalling for the month to Mar 2 showed 89% support for Taproot from pools according to their hashrate. Additionally, Poolin contributed a consensus effort [compiling](https://taprootactivation.com/) pools' sentiment and preferred activation methods.

The New York Attorney General reached a [settlement](https://www.reuters.com/article/new-york-ifinex-settlement/bitfinex-tether-owner-pays-18-5-mln-fine-to-settle-nyag-cryptocurrency-cover-up-charges-idUSL1N2KT16E) on charges against Tether and Bitfinex which saw the company pay $18.5 million fine but avoid having to admit to any wrongdoing.

The Central Bank of Nigeria has moved to remind banks that "dealing in cryptocurrencies or facilitating payments for cryptocurrency exchanges is prohibited" and [instructed](https://www.coindesk.com/nigerias-central-bank-orders-banks-to-close-accounts-of-all-crypto-users) them to close the accounts of all people and entities who trade in cryptocurrencies.

The US Federal Reserve experienced an [issue](https://www.theregister.com/2021/02/24/federal_reserve_outage/) with its inter-bank transfer system which impaired service for hours. This happened soon after US Treasury Secretary Janet Yellen had [warned](https://www.cnbc.com/2021/02/22/yellen-sounds-warning-about-extremely-inefficient-bitcoin.html) that Bitcoin is "extremely inefficient" and poses risk to investors.

@notsofast urges everyone to learn from his [mistakes](https://cryptonews.com/news/trader-s-lesson-why-you-shouldn-t-keep-large-amounts-of-cry-9302.htm) that have led to losing ~$100,000 in crypto in a security breach: get a good password manager, use a hardware wallet, isolate dangerous browser extensions like Metamask in separate browser profiles or devices.

## About This Issue

This is issue 35 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

You can submit a story [here](https://github.com/xaur/decred-news/labels/next%20release) to be considered for the next release. [Feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, richardred
- reviews and feedback: davecgh, jholdstock, peter\_zen
- title image: saender
- funding: Decred stakeholders
