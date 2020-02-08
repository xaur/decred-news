# Decred Journal – January 2020

![abstract art](../img/journal-202001-384.png)

_Image: Event Horizon by @saender_

Highlights for January:

- Version 1.5.1 of the Decred node and wallet software was released, incorporating some bug fixes and new features.
- Politeia had its most active month in a while, with 6 new proposals being submitted and 5 already finished voting.
- The consensus rule change vote for DCP0005 is well on its way to completion and support is >99%.
- Global chain of events and community meetups is unfolding to mark the 4th anniversary of the Decred genesis block on Feb 8th. Some groups celebrated early on Feb 6. Stakey's bags are packed for a whirlwind global tour.

## Cast your votes!

Consensus change vote to enable block header commitments as defined in [DCP0005](https://github.com/decred/dcps/blob/master/dcp-0005/dcp-0005.mediawiki) is steadily [progressing](https://explorer.dcrdata.org/agenda/headercommitments). Out of the 61% active Yes/No votes 99.94% are Yes, while the remaining 39% votes are Abstain.

There is still around 1 week to go. If you have a preference please [configure it](https://docs.decred.org/governance/consensus-rule-voting/how-to-vote/) in your solo and/or VSP voting wallets.

## Release v1.5.1

Release v1.5.1 fixes bugs found in v1.5.0 and adds a few features.

dcrd: fixed minor memory leak with authenticated RPC WebSocket clients on intermittent connections. This is especially relevant for setups that involve wallets with a very large number of addresses.

dcrwallet: fixed address reuse bug that could be triggered by restart of the network sync (e.g. when losing link to dcrd), a bug in ticket buyer that could send change to a wrong account, and a few other bugs. New features include the `auditreuse` command and the ability to use `createrawtransaction` in SPV syncing mode (i.e. without running dcrd).

Decrediton: fixed incorrect display of active tickets, gap exhaustion during change generation, and several UI issues. QR codes have been [sexed up](https://github.com/decred/decrediton/issues/2380) with blue/green Decred logo in the center.

Find the full release notes and downloads on the [release page](https://github.com/decred/decred-binaries/releases/tag/v1.5.1). As always, [verify the binaries](https://docs.decred.org/advanced/verifying-binaries/) before installation.

## Development

[dcrd](https://github.com/decred/dcrd): Service script for OpenBSD rc.d was [added](https://github.com/decred/dcrd/pull/2030) in addition to the [existing](https://github.com/decred/dcrd/tree/master/release/services) systemd and SMF configs. HTTP seeder support was added [to dcrseeder](https://github.com/decred/dcrseeder/pull/25) and [to dcrd](https://github.com/decred/dcrd/pull/2017). `chainec` package was [removed](https://github.com/decred/dcrd/pull/2039) because of the practical issues encountered with this generic crypto API. Nonce generation was [improved and optimized](https://github.com/decred/dcrd/pull/2044) by specializing the implementation specifically for secp256k1 and modifying it in such a way that signing can no longer fail in the extremely unlikely event a returned nonce results in an invalid signature.

[dcrwallet](https://github.com/decred/dcrwallet): Multiple bug fixes for the v1.5.1 release.

[Decrediton](https://github.com/decred/decrediton): Lots of bug fixes and UI enhancements for the v1.5.1 release.

Work continues to [refactor startup](https://github.com/decred/decrediton/issues/2121) to utilize a hierarchical state machine.

[Politeia](https://github.com/decred/politeia): The Decred Contractor Clearance (DCC) component of the CMS has launched and started processing DCC issuances. CMS received a bunch of fixes and UI enhancements.

Work continues on the CMS UI [redesign](https://github.com/decred/politeiagui/pull/1625) and adding dark mode to Politeia.

[dcrstakepool](https://github.com/decred/dcrstakepool): v1.5.0 was released. This release contains all development work completed since v1.2.0 (Sep 2019). Since then, 7 contributors have produced and merged 37 pull requests. Changes include minor GUI enhancements, improved HTTP request logging, streamlining of existing code, and various bug fixes. For the full list of changes and upgrade path see the [release notes](https://github.com/decred/dcrstakepool/blob/master/docs/release-note-1.5.0.md).

A new high level design was [proposed](https://github.com/decred/dcrstakepool/issues/574) for removing VSP accounts that also removes fees from VSP ticket transactions, making it possible for both solo and VSP stakers to purchase mixed tickets in the same anonymity set.

[dcrpool](https://github.com/decred/dcrpool): Completed large [refactoring](https://github.com/decred/dcrpool/pull/143) to decouple components and facilitate increasing test coverage.

[dcrlnd](https://github.com/decred/dcrlnd): Bug fixes and documentation improvements. Docker examples [finished](https://github.com/decred/dcrlnd/pull/66) that automate the deployment of simnet environments with docker-compose. A beginner's guide to testing the Decred LN was [published](https://medium.com/decred/beginner-guide-to-the-decred-dcr-lightning-network-917f8ad304aa) on Medium.

Work continues to [port upstream changes](https://github.com/decred/dcrlnd/pull/74) up to the recently released [v0.9.0-beta](https://github.com/lightningnetwork/lnd/releases/tag/v0.9.0-beta) version. The ported changeset includes 503 commits that add 37K and remove 11K lines of code.

[cspp](https://github.com/decred/cspp): Bug fixes and code maintenance. A copy of Go's internal chacha20 package was [removed](https://github.com/decred/cspp/pull/38) in favor of the recently released public API.

[dcrdex](https://github.com/decred/dcrdex): More building blocks completed. Highlights: client DCR exchange [wallet](https://github.com/decred/dcrdex/pull/92), client bbolt-based [database](https://github.com/decred/dcrdex/pull/99), client [web server](https://github.com/decred/dcrdex/pull/103) to enable client access via browser, initial [client core](https://github.com/decred/dcrdex/pull/120) application, client application [skeleton](https://github.com/decred/dcrdex/pull/100), client registration of new [DEX account](https://github.com/decred/dcrdex/pull/140) through the web interface, server app config and asset drivers [system](https://github.com/decred/dcrdex/pull/81), implementation of 64-bit [Mersenne Twister](https://github.com/decred/dcrdex/pull/137) PRNG.

It was another busy development month: a total of 27 pull requests merged adding 22K and deleting 4K lines.

[dcrandroid](https://github.com/decred/dcrandroid): Layout on the restore wallet page was [improved](https://github.com/decred/dcrandroid/pull/422).

The dcrlibwallet mobile library shared between Android and iOS apps received a bunch of bug fixes and was [upgraded](https://github.com/raedahgroup/dcrlibwallet/pull/93) to v1.5.0 release of dcrd and dcrwallet.

[dcrios](https://github.com/raedahgroup/dcrios): UI enhancements and performance optimizations. Overview page UI cleanup and sync [improvements](https://github.com/raedahgroup/dcrios/pull/566), multi-wallet [optimizations](https://github.com/raedahgroup/dcrios/pull/572), preliminary [migration](https://github.com/raedahgroup/dcrios/pull/558) to dcrlibwallet's multi-wallet feature, switched to dcrlibwallet's [config storage](https://github.com/raedahgroup/dcrios/pull/576). A new UI was implemented for the [password/PIN](https://github.com/raedahgroup/dcrios/pull/551) setup, [seed backup](https://github.com/raedahgroup/dcrios/pull/530) and [restore from seed](https://github.com/raedahgroup/dcrios/pull/527) features.

[dcrdata](https://github.com/decred/dcrdata): Small fixes and UI improvements.

[tinydecred](https://github.com/decred/tinydecred): RPC client was [added](https://github.com/decred/tinydecred/issues/45) with most commands implemented by now. Added a button to [revoke](https://github.com/decred/tinydecred/pull/30) missed and expired tickets. Database was [redesigned](https://github.com/decred/tinydecred/pull/42) to support custom encoding, batch insertion, namespaces, and more. Improved [test coverage](https://github.com/decred/tinydecred/pull/47) to ~73%. Restructured the project to make it [packageable](https://github.com/decred/tinydecred/pull/59).

[docs](https://github.com/decred/dcrdocs): [dcrlnd](https://docs.decred.org/wallets/lightning/) commands and arguments for the CLI have been [documented](https://github.com/decred/dcrdocs/pull/1055). Setup instructions for [Trezor](https://docs.decred.org/wallets/decrediton/trezor/) on Decrediton were [added](https://github.com/decred/dcrdocs/pull/1062). [Reading list](https://docs.decred.org/getting-started/reading-list/) was [added](https://github.com/decred/dcrdocs/pull/1043) to the Getting Started section containing curated selection of articles, podcasts, video and other materials (based on Ditto's Educational Resources Repository). [BLAKE-256](https://docs.decred.org/research/blake-256-hash-function/) page has been significantly [extended](https://github.com/decred/dcrdocs/pull/1034) to explain why this function was chosen. Two new definitions (Coin Type and HD Wallet) were [added](https://github.com/decred/dcrdocs/pull/1057) to [Glossary](https://docs.decred.org/glossary/).

[decred.org](https://github.com/decred/dcrweb): Updated [contributors](https://github.com/decred/dcrweb/pull/774), cleanup.

Dev activity stats for January: 246 active PRs, 210 master commits, 58K added and 25K deleted lines spread across 17 repositories. Contributions came from 3-6 developers per repository.

## People

Welcome to new first time contributors with code merged to master: @termoose ([dcrlnd](https://github.com/decred/dcrlnd/commits?author=termoose)) and @pablito ([dcrweb](https://github.com/decred/dcrweb/commits?author=pLabarta)).

Congratulations to first contractors granted the Decred Contractor Clearance via the new CMS process: [@bgptr](https://github.com/bgptr) (development), [@teknico](https://github.com/teknico) (development) and [@decreddragon](https://twitter.com/DecredDragon) (marketing).

The following people were removed from the list of [active contributors](https://decred.org/contributors/): Leslie Ankney, Elizabeth Bagot, Margaret Huang, Milvian Prieto, Denys Zayets, Tim Hebel, Phillip Conrad, Justin Santoro, Bill Xing. Thank you for all the good work and don't hesitate to drop by!

The [contributors](https://decred.org/contributors/) page is regularly updated to list people who are currently building Decred. The consequence of this is that when inactive contributors are removed, no record is left on the website that they have worked for the project. To address this it has been proposed to create a list of [past contributors](https://github.com/decred/dcrweb/issues/744) and/or [hall of fame](https://github.com/decredcommunity/issues/issues/52).

Community stats:

- Twitter followers: 40,860 (-37)
- Reddit subscribers: 9,723 (+15)
- Matrix users: 533 (+29)
- Slack users: 6,880 (-1)
- Discord users: 2,670 (+42), verified to post: 433 (+26)
- Telegram users: 2,728 (-110)
- YouTube subscribers: 3,950 (-10)
- Facebook followers: 3,563 (+11), likes: 3,234 (+11)
- LinkedIn followers: 689 (+15)
- GitHub dcrd stars: 533 (+5), forks: 1,476 (+18)

Historical charts of Twitter, YouTube, Reddit and GitHub stats are now available at [dcrextdata](http://dcrextdata.planetdecred.org/community).

## Governance

In January the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 14,121 DCR and spent 15,560 DCR. Using January's daily average DCR/USD rate of $18.00, this is $254K received and $280K spent. At December's average daily rate of $18.32, the USD figure billed for work completed in that month is $285K. As of Feb 1, the Treasury balance is 642,082 DCR (12.2 million USD at $18.96).

There were 6 proposals submitted in Jan, 5 have already been voted on and 1 is still under discussion.

- The proposal from [Monde](https://proposals.decred.org/proposals/bdd02d82547bd78fc95939c1e2b3df21ebec6e8d31444df5bea3c133b0199f05) Public Relations was approved with 72% approval and turnout of 25%.
- The proposal from [Ditto](https://proposals.decred.org/proposals/012b4e335f25704e28ef196d650316dca421f730225d39e37b31b3c646eb8497) PR was rejected with 17% approval and turnout of 35%.
- The Decred Open Source Research Program renewal of [phase 3](https://proposals.decred.org/proposals/e3675649075a2f92269d8cdc2e1dfd71b16796477df31de7d2868cccfcffb13f) was approved with 82% approval and turnout of 29%.
- A [proposal](https://proposals.decred.org/proposals/063e38270b475ad680e98c12d1a48e322f4e8defe40b265272ea60c6d2202b13) from @dezryth to manage the project's Facebook account and represent Decred at events was approved with 76% yes votes and participation of 21%.
- A proposal for [stickers](https://proposals.decred.org/proposals/4acb95564d36488a7ee64683a84dd7954982b2f4743e2f7a15477231f863442f) was rejected with 5% yes votes and participation of 21%.
- A [proposal](https://proposals.decred.org/proposals/95cfb73254a032b2c199c37bb499d6f172d044b1f38016279c5bbca6572251f0) by @Exitus to produce video content for Decred is under discussion.

Politeia Digest [issue 26](https://blockcommons.red/politeia-digest/issue026/) has more detail on all of the proposals and the Market Maker auditing. Auditing tools have been developed which process i2's order open/close history to calculate uptime on a percentage basis. If uptime is less than the 90% quoted in i2's proposal, their fees for the month will be reduced proportionally.

Also in January, CoinDesk published an [article](https://www.coindesk.com/is-bitcoin-in-2020-really-like-the-early-internet) which referenced Decred Treasury spending figures. Some additional figures were calculated for the article at that time (end of Nov 2019). The Treasury had paid out the equivalent of $6.55 million, with 54.7% being paid to developers. Since Politeia launched in Oct 2018, more than 10% of Treasury spending has gone to projects proposed and passed via Politeia. By geographical region, 30% of Decred's developers are in Central/South America, 25% in the US, 20% in Europe, 15% in Africa, and 10% in Asia.

## Network

Hashrate: January's hashrate opened at ~396 Ph/s and closed ~435 Ph/s, bottoming at 315 Ph/s and peaking at 528 Ph/s throughout the month. Pool hashrate distribution as of Feb 1: Poolin 26%, UUPool 18%, lab.antpool.com 10%, F2Pool 2%, Luxor 1.78%, BTC.com 1.46%, BeePool 0.08%, CoinMine 0.07%, suprnova 0.01%, and others ~40% per [dcrstats.com](https://dcrstats.com/pow). Pool distribution numbers are approximate and cannot be accurately determined.

Staking: 30-day average ticket price was 138.3 DCR (+0.8) per dcrstats.com. The price varied between 128.1-150.4 DCR. Locked amount was 5.55-5.71 million DCR, which corresponded to 50.83-51.96% of the available supply.

Nodes: Throughout [January](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1577836800000&to=1580515200000) there was an average of 137 public listening nodes and 323 normal nodes per dcr.farm. Average version distribution for Jan: 50.8% use dcrd v1.4, 21.1% use dcrd v1.5, 9.0% use dcrd v1.5 dev and RC builds, 3.1% use dcrd v1.6 dev builds, 2.2% use dcrd v1.5.1, 5.6% use dcrwallet v1.4, 3.4% use dcrwallet v1.5, 0.6% use dcrwallet v1.5.1.

[dcrextdata](http://dcrextdata.planetdecred.org/) got a refreshed design and enabled mempool and block propagation charts. Some of them are a bit slow but already show interesting information. Feedback is welcome in the [issue tracker](https://github.com/raedahgroup/dcrextdata) or in the [#planetdecred](https://matrix.to/#/!gruHpujXftcsHcghjx:planetdecred.org) room.

Data from a node that has been running since block 0 [shows](https://matrix.to/#/!vGasNHFXqjoEWUBTIi:decred.org/$15792934191332SWDSY:decred.org) that the Decred mainnet chain has had 2517 reorgs of depth 1, 25 reorgs of depth 2, 3 reorgs of depth 3, and 0 reorgs of depth greater than 3.

The Decred mainnet [LN map](https://ln-map.jamieholdstock.com/) shows 14 nodes and 31 channels with a total capacity of 6 DCR, as of Feb 6.

## Integrations

VSP news:

- New VSP launched by the YieldWallet staking-as-a-service provider, available at [decred.yieldwallet.io](https://decred.yieldwallet.io/). Service fee is 2%.
- [decredvoting.com](https://decredvoting.com/) VSP [announced](https://www.reddit.com/r/decred/comments/euqd4h/introducing_split_ticket_dashboard_on/) a new split ticket dashboard that "provides split ticket users with a complete summary view of all their split tickets along with personalized analytics data".
- The following VSPs were removed from the [listing](https://decred.org/vsp/) for their poor performance: [d1pool.com](https://github.com/decred/dcrwebapi/pull/63), [dcr.grassfed.network](https://github.com/decred/dcrwebapi/pull/70) and [dcr.pos.fans](https://github.com/decred/dcrwebapi/pull/79).

It turns out that the [dcr.farm](https://dcr.farm/) VSP runs a bunch of useful services without due advertising:

- [seed.dcr.farm](https://seed.dcr.farm/) is a dcrd seed node with dedicated bandwidth, located in France.
- [explorer.dcr.farm](https://explorer.dcr.farm/) is an alternative explorer for Decred blockchain.
- Sophisticated [status dashboard](https://status.dcr.farm/) for all services, including the 6 voting wallets.
- This is actively used by DJ but mentioning for completeness: [charts.dcr.farm](https://charts.dcr.farm/) has [~16 dashboards](https://charts.dcr.farm/dashboards) with some unique charts like [Nodes](https://charts.dcr.farm/d/000000014/nodes) (node versions over time), [VSPs](https://charts.dcr.farm/d/000000016/proof-of-stake-pools) (VSP stats over time) and [Transaction Fees](https://charts.dcr.farm/d/000000013/transaction-fees) (irregular high and low fees).

Exchanges:

- We saw some reports that [Bittrex](https://twitter.com/Cjfan23/status/1218727480854446081) and [Binance](https://www.reddit.com/r/decred/comments/ew1vyc/binance_dcr_withdrawls_disabled/) wallets were both in maintenance mode for a while. As of writing both are working.

Warning: the authors of Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

On February 8th, Decred turned four, and the community celebrated the event with [#DecredGlobalMeetup](https://twitter.com/hashtag/DecredGlobalMeetup). Events took place in at least a [dozen cities](https://twitter.com/decredproject/status/1225440495108841475) all across the world to celebrate the community and technology Decred has built.

In January, the new subpages of the website were completed and submitted for translations, and all languages are expected to go live at once in February. This offers a visual refresh to the site, and aligns with the current project [messaging](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md). The website has been simplified, and all future updates will be achievable in no longer than three months start to finish.

Various proposals for marketing and PR have been submitted, and more are on the way, as well as a report detailing a summary of 2019 efforts and expenses, and a call to action for 2020 to decentralize, break the bubble, educate, and empower the individual.

The Decred in Depth podcast released two episodes: @matheusd on Decred's Lightning Network, and @permabullnino on "Block Subsidies + Ticket Pool VWAP + HODLer Conversion Rates". Don't forget to subscribe and rate the podcast.

## Events

Attended:

- Jan 7 - [Digital Money Forum](https://thedigitalmoneyforum.com/) - Las Vegas, USA. @akinsawyerr argued for decentralized networks and individual sovereignty on [The Libra Effect](https://thedigitalmoneyforum.com/Sessions/the-problem-with-old-money-a-great-debate/) panel, which was featured on [CoinDesk](https://www.coindesk.com/libra-association-exec-world-needs-us-because-bitcoin-is-not-a-means-of-payment), and also talked to several journalists. ([report](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$157859800075195pLJde:decred.org), [photos](https://twitter.com/AkinSawyerr/status/1214614201517232128))
- Jan 14 - [Cryptopia Documentary Premiere](https://www.meetup.com/en-AU/BC-Aus/events/267242503/) - Melbourne, Australia. Decred was invited to be an event sponsor and launch partner of Cryptopia Film, a documentary about the key themes within cryptocurrency, which include regulation, privacy, financial services, governance, marketing and development. The entire theatre was booked out with over 140 guests from the crypto and blockchain community. @eSizeDave and @zohand talked Decred on a panel discussion and were quoted in the official [press release](https://prwire.com.au/r/87706). ([report](https://github.com/decredcommunity/events/blob/master/reports/20200114-cryptopiafilm-world-premiere-melbourne-australia.md))
- Jan 14 - [GoCracow #7](https://www.meetup.com/en-AU/GoCracow/events/265765051/) - Kraków, Poland. @kozel introduced ~30 Go devs to cryptocurrencies and Decred. The audience was attentive in general, but the most active participants were the ones who self-described as already familiar or enthusiastic about crypto. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200114-gocracow7-meetup-krakow-poland.md))
- Jan 24 - Blockchain Technology and Use Cases - Casablanca, Morocco. @arij was invited to talk at the event co-organized by the Moroccan Youth Ministry with the topic "The role of new technologies in promoting the positive development of young people". @arij talked about blockchains and introduced Politeia and LN to the audience of around 50 people of different backgrounds, mostly young people. ([photos](https://twitter.com/DecredArabia/status/1220819101586685952))
- Jan 29-31 - [Crypto 101 Online Summit](https://www.crypto2020summit.com/) - Internet. @lukebp outlined Decred's plans for 2020, the presentation will be uploaded to YouTube when ready.

Upcoming:

- Feb 8 - [Blockchain and AI](https://www.eventbrite.com/e/blockchain-and-ai-best-tools-for-the-development-of-nations-tickets-91389994935) - Casablanca, Morocco. @arij will talk about Decred's achievements during its 4 years. A small party at the end will mark Decred's anniversary.
- Feb 8 - [Decred Crypto Hangouts](https://www.eventbrite.com/e/decred-crypto-hangout-learn-about-career-opportunities-in-the-industry-tickets-91830803405) - Ikeja, Lagos. Huobi, Yellowcard and Telos4Africa will be in attendance.
- Feb 8 - [Decred Global Meetup](https://www.meetup.com/pt-BR/DecredBrasil/events/268496816/) - Salvador, Brazil.
- Mar 12-13 - [Blockchain Summit Latam](https://www.blockchainsummit.la) - Panama City, Panama. Decred will be a silver sponsor.
- Mar 18 - [Campus Party Amazonia](https://brasil.campus-party.org/campus-party-amazonia-2020/) - Manaus, Brazil. Decred will have 2 talks and several other activities.
- Mar 20 - [BlockchainUA](https://blockchainua.com/en/) - Kyiv, Ukraine. Speakers are wanted to represent Decred at the biggest event in Eastern Europe. Contact @cryptotexty in the [#events](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org) room for details.
- Mar 20-21 - [CIBTC Blockchain Summit](http://cibtc.es/) - Motril, Spain. Decred will be gold sponsor. The event is part of a big Decred en Español tour in Spain where @elian will be organizing meetups and a workshop with local communities in Madrid, Barcelona, Bilbao, Valencia, Vigo and Motril.
- May 30-31 - [Bitconf](https://www.bitconf.com.br/portal/) - São Paulo, Brazil. Decred will have multiple talks on various subjects.

## Media

[Decred Drive](https://medium.com/@decreddrive), a new weekly newsletter, was [launched](https://twitter.com/DecredDragon/status/1215309738293985280) by @decreddragon on Jan 9 and published 5 issues so far.

Decred was featured in the new Our Network weekly newsletter issues [#2](https://ournetwork.substack.com/p/our-network-issue-2) and [#6](https://ournetwork.substack.com/p/our-network-issue-6), with @Checkmate providing charts and insights about Decred on-chain data and @richardred providing one chart about Politeia. Each week the newsletter includes 5 graphs and comments for a number of different blockchain projects.

Checkmate made the bear case for Ethereum as part of an intended "[crypto rumble](https://bankless.substack.com/p/why-eth-wont-sustain-a-monetary-premium)" in the Bankless newsletter. Vitalik Buterin [responded](https://www.reddit.com/r/ethereum/comments/ewb9as/why_eth_wont_sustain_a_monetary_premium/fg2x4oz/) to some comments about the write-up on Reddit, and there are now 3 [responses](https://bankless.substack.com/p/why-eth-will-sustain-a-monetary-premium) on the Bankless substack from prominent Ethereum community members.

Decrypt has [covered](https://decrypt.co/17371/we-found-the-no-coiner-troll-guarding-wikipedia) some of Decred's [experience](https://github.com/decredcommunity/issues/issues/79) with Wikipedia, which triggered an intelligent Twitter [exchange](https://twitter.com/decryptmedia/status/1220069033405485057) with one of the WP crypto experts.

Selected articles:

- Building a Transparent Future with the Decred Blockchain by @ammarooni ([medium](https://medium.com/decred/building-a-transparent-future-with-the-decred-blockchain-e77471d28059))
- Decred On-Chain: HODLer Conversion Rates by @permabullnino ([medium](https://medium.com/@permabullnino/decred-on-chain-hodler-conversion-rates-87e16a4c78cd))
- 2019 Review: Distributed Governance ([Smith and Crown](https://sci.smithandcrown.com/research/2019-governance-review)) - this comprehensive overview of blockchain governance in 2019 features many accurate observations about Decred, with a special note about Politeia participation rates.
- The Future of Digital Currencies in Africa? Meet Decred the Autonomous Digital Currency ([appsafrica.com](https://www.appsafrica.com/the-future-of-digital-currencies-in-africa-meet-decred-the-autonomous-digital-currency/))
- Is Bitcoin Really Like the Early Internet? by Leigh Cuen ([coindesk.com](https://www.coindesk.com/is-bitcoin-in-2020-really-like-the-early-internet)) - this reflection piece on the similarities between Bitcoin and the early Internet features interviews with @moo31337 and Zooko Wilcox of Zcash. The article also has some figures related to Decred Treasury spending, as noted in the Governance section.

> We were equally as excited to see the engagement sparked by the CoinDesk [article](https://www.coindesk.com/is-bitcoin-in-2020-really-like-the-early-internet) last weekend! It was certainly interesting to see various projects discussing who ended up being mentioned in the article, with only Decred and a handful of others making the cut. This type of coverage is the result of months of communication with reporters: education, timely responses, interviews, supplying information and statistics, etc. Stories like this don't happen overnight or of their own accord - and the old adage "out of sight, out of mind" does apply to media. ([@liz_bagot](https://proposals.decred.org/proposals/012b4e335f25704e28ef196d650316dca421f730225d39e37b31b3c646eb8497/comments/71))

Translations:

- Beginner guide to the Decred Lightning Network - [in Arabic](https://insaf01.github.io/decred-arabic/articles/beginner-guide-to-the-decred-lightning-network.html) by @arij, [in Spanish](https://medium.com/decred-es/gu%C3%ADa-para-probar-el-lightning-network-de-decred-dcr-344cad6be20e) by @francov\_.
- Decred Journal December 2019 translated to Arabic (@arij), Chinese (@Dominic) and Spanish (@francov\_). Thank you for your hard work!

Videos:

- Is a Public Relations Firm in Crypto Worth It? Decred Stakeholders Vote and Decide Using Politeia by @Exitus ([youtube](https://www.youtube.com/watch?v=uzhc2CKI2wk))
- Decred's Akin Sawyerr Says Blockchain Is Part of Africa's Political Future ([coindesk.com](https://www.coindesk.com/decreds-akin-sawyerr-says-blockchain-is-part-of-africas-political-future), [youtube](https://www.youtube.com/watch?v=8w7uCSVuuVw))
- The Libra Effect at CES2020: Highlights of @akinsawyerr by @Exitus ([youtube](https://www.youtube.com/watch?v=5Zi5wYZhEDE)) - the full panel can be found [here](https://www.youtube.com/watch?v=prz6ILpLNLE) (@akinsawyerr starts around [17 min](https://www.youtube.com/watch?v=prz6ILpLNLE&t=17m00s))

Audio:

- @akinsawyerr appeared on Tom Shaugnessy's Chain Reaction podcast to talk about Governance Reimagined. ([podbean](https://fiftyonepercent.podbean.com/e/decred/))
- Crypto 101 Ep. 302 - Governing the Masses w/ Decred, featured @lukebp. ([podbean](https://www.podbean.com/media/share/dir-j5baa-7c90e87), [soundcloud](https://soundcloud.com/crypto101podcast/ep-302-governing-the-masses-w-decred))
- Decred in Depth Ep. 16 - @permabullnino discusses the Politeia proposal process and his ongoing work analyzing ticket movements on the Decred chain, introducing concepts like TVWAP and Hodler conversion rates. ([libsyn](https://decredindepth.libsyn.com/permabull-nino-block-subsidies-ticket-pool-vwap-hodler-conversion-rates), [soundcloud](https://soundcloud.com/decredindepth/ep-16-permabull-nino-block-subsidies-ticket-pool-vwap-hodler-conversion-rates))
- Decred in Depth Ep. 17 - @ammarooni talks about Toronto's rich crypto history, the tokenomics of DCR, BTC and ETH, and considers Decred as an infrastructure provider, productive asset and economic breakthrough. ([libsyn](http://decredindepth.libsyn.com/ammar-nasier-decred-an-economic-breakthrough))

@AGNFAB1 published two new pieces of artwork: [Politeia pirate](https://www.reddit.com/r/decred/comments/end3lc/d_e_c_r_e_d/) (unofficial title), [DCR is Water BTC is Fire](https://twitter.com/AGNFAB1/status/1220091425737580544).

## Community Discussions

Comm systems news:

- Slack is going down, bridge is being burned, flee to the [Matrix](https://decred.org/matrix/) while you still can!

Selected Reddit posts:

- [Update](https://www.reddit.com/r/decred/comments/eo3tje/decred_dex_progress_the_client_and_server_are/) on dcrdex, atomic testnet trading up next.
- [How](https://www.reddit.com/r/decred/comments/ervlvw/how_to_runstartmove_decrd_to_the_background_i_can/) to move dcrd to the background - a common question for new CLI users.
- Is Decred [dead](https://www.reddit.com/r/decred/comments/ekhi2l/is_decred_dead_hash_rate_has_stagnated_and/)? Nope.
- Interesting discussion on @Checkmate's Ethereum bear case [post](https://www.reddit.com/r/ethereum/comments/ewb9as/why_eth_wont_sustain_a_monetary_premium/fg1q9q7/) on /r/ethereum, including some discussion with Vitalik Buterin.

Selected Twitter discussions:

- Stakey reminds everyone to [control their keys](https://twitter.com/DCRComic/status/1212754642481881088).
- First to market vs adaptable, a historical [example](https://twitter.com/BarnardTheBear/status/1213893268351672320).
- Why Decred is [boring](https://twitter.com/marco_peereboom/status/1218178834786324480).
- How often does your CEO/project lead tell you to [engineer him out](https://twitter.com/marco_peereboom/status/1212849047456927744) of the project?
- @DCRComic: Atomic Swaps [comic](https://twitter.com/DCRComic/status/1222874521507717121), a [take](https://twitter.com/DCRComic/status/1220367582479425537) on the BCH development funding story, a [thread](https://twitter.com/DCRComic/status/1218189767759859713) about dcrdata.
- An [update](https://twitter.com/chappjc/status/1222004371199864834) on dcrdex from @chappjc, "this Spring".
- @richardred [opened](https://twitter.com/RichardRed0x/status/1219381114768429057) the pod bay doors to vote for the open source research program.
- @lukebp [tweets](https://twitter.com/lukebp_/status/1217871970420711424) about the benefits of being able to amend consensus rules to enhance network security and UX.
- The Ditto and Monde PR proposals drew some attention from journalists in the space, including the Block's [Frank Chaparro](https://twitter.com/fintechfrank/status/1215704016564428802).
- @Dustorf on the digital Decred contractor [collective](https://twitter.com/lefebvre_dustin/status/1220397690602901504).
- @degeri points out that the websites of most top blockchain projects are [feeding](https://twitter.com/degeri_crypto/status/1217372695483965441) information to Google.
- [#DrawStakey](https://twitter.com/DCRComic/status/1220732376088809477) contest.

## Markets

In January DCR was trading between USD 16.24-22.44 / BTC 0.00195-0.00257. The average daily rate was $18.00.

The price movement of Bitcoin from ~6500 to the ~9000 range spurred the price increase of a number of [altcoins](https://cointelegraph.com/news/dash-price-up-70-bsv-gains-200-is-a-price-correction-imminent) including Dash, Zcash and a number of Bitcoin forks.

## Relevant External

Bitcoin celebrated its 11th anniversary. Since Jan 3, 2009, the Bitcoin network has operated with [99.9848% uptime](http://bitcoinuptime.com/).

December's mining report from CoinShares notes a 80% Bitcoin hashrate increase since Jun 2019, from ~50 to ~90 Eh/s (Exahashes per second). 70% of the added ~40 Eh/s is speculated to come from China, while China's share in the total hashrate is estimated to be 65%. The "breakeven" and "miner capitulation" prices are estimated at ~$6,100 and ~$3,900, respectively. Check the [highlights](https://medium.com/coinshares/bitcoins-hash-rate-grew-more-than-80-since-june-mostly-within-china-7444b20b2c89) and the full linked report for more interesting numbers.

State of the Network 2019 [Year in Review](https://coinmetrics.substack.com/p/state-of-the-network-2019-year-in) by Coin Metrics compared the performance of the largest 18 cryptoassets (including DCR) across a set of market and chain metrics.

Monero announced [RPC-Pay](https://www.monerooutreach.org/stories/RPC-Pay.html), a new scheme for instant and private microtransactions where clients pay with mining hashes for using a compliant server, such as a Monero node. "Hashes received as payment are used by the server to earn income, and because of Monero's RandomX the mining hashes can be calculated efficiently using most popular CPUs. Paying with just hashes instead of Monero itself means that RPC-Pay does not burden the Monero network or leave a record. With RPC-Pay, mining hashes become a new stealthy smallest unit of payment in the Monero universe.". Primo project is the first external application of the concept to implement paid website content delivery.

[Nakamoto](https://nakamoto.com/), a new cryptocurrency-themed journal, launched on the 11th anniversary of Bitcoin's genesis block with a selection of articles from prominent blockchain personalities. The journal describes itself (and contributors) as being "pro-Bitcoin", but this caused quite a lot of [controversy](https://cryptoslate.com/nakamowho-blog-by-pro-bitcoin-technologists-bashed-by-btc-maximalists/) with some Bitcoin maximalists who took exception to articles which were about cryptocurrency projects other than Bitcoin. Many people listed as contributors have not yet [published](https://modernconsensus.com/cryptocurrencies/bitcoin/bitcoin-journal-nakamotos-rocky-start/) articles in the journal, but listing names like Roger Ver and Brendan Blumer (Block.one CEO) seems to have been enough to have other contributors like Tuur Demeester [withdrawing](https://twitter.com/TuurDemeester/status/1213939900476743680) their name.

DigixDAO is to be wound down following a [vote](https://www.coindesk.com/digixdao-votes-to-liquidate-64m-treasury) in which 58 stakeholders voted [overwhelmingly](https://community.digix.global/#/proposals/0xe7d5d8aefc5f73c4c8bbc716f0c3c2dd52d5282d18217db331da4435b8e6966e) (97%) to liquidate its funding pool and reclaim their ETH. DigixDAO was formed to support an ecosystem around the Digix gold token (DGX) and promote it. Digix [conducted](https://www.coindesk.com/digixdao-votes-to-liquidate-64m-treasury) an ICO in 2016 and raised 466,648 ETH, worth $7 million at the time, and currently holds 380,000 ETH (worth $71 million at Jan 2019 prices). After the DAO platform launched in March 2019 to administer the fund the founders began to hear dissatisfaction from DAO members and requests for dissolution. They introduced [Project Ragnarok](https://community.digix.global/#/proposals/0xe7d5d8aefc5f73c4c8bbc716f0c3c2dd52d5282d18217db331da4435b8e6966e) as an option to dissolve the DAO and allow members to reclaim their ETH, and members took that option. Of the DAO token (DGD) circulating supply of 2 million, 1 million was staked to participate in DAO governance. Casual inspection of the proposals on the DigixDAO community [site](https://community.digix.global/#/) suggests turnout in proposal votes was regularly lower than 10% DGD represented, with around 20-30 voters on most proposals. The liquidation proposal had much higher participation, with 66% of circulating DGD voting to shut the whole thing down. This [article](https://blog.coinfund.io/digixdao-divorce-story-6ed74b00e2bd) has further details, including the pivotal role played by 4 DGD whales thought to be founders of the project.

Another ICO project to wind down and return unspent funds this month was [TruStory](https://medium.com/trustory-app/why-trustory-is-shutting-down-6d50175628eb).

Decentraland are putting their Agora governance platform to use again with [two](https://decentraland.org/blog/announcements/back-to-the-polls-two-new-agora-votes/) more votes to determine ecosystem parameters. MANA holders voted on what the marketplace [fee](https://agora.decentraland.org/polls/1d955723-5158-4403-b026-32e974e2fae9) should be (fees are collected in MANA and burned), with 90% voting to increase the fee from 1% to 2.5% (the other options were for larger increases). MANA holders also voted on how much weight to give [LAND](https://agora.decentraland.org/polls/0387cebc-31a3-4e12-a7b4-e9926dd5b392) ownership in governance, having previously [voted](https://agora.decentraland.org/polls/8c4fdc25-1876-4ca5-a2ac-809c13ab840c) to indicate that LAND owners should also be able to vote, in this poll the MANA holders voted to give each LAND the equivalent voting power to 2K MANA (the lowest option available). Participation in these governance polls was around 3.5-4% of circulating MANA supply and around 50 individual addresses.

The Zcash development funding saga seems to finally be [over](https://electriccoin.co/blog/dev-fund-poll-shows-consensus/), for this epoch. However, not before having to resolve some final disagreements. The first of these was about whether the ECC's funding should be capped in USD terms (limiting ECC's exposure to ZEC upside). The ECC published a [post](https://electriccoin.co/blog/dev-funds-should-be-in-zcash-not-united-states-dollars/) about the importance of ZEC-denominated incentive packages for attracting and retaining talented workers, with a 4-year vesting schedule on these to encourage long service. The post argued against a fiat-denominated cap on ECC's earnings, as it would break this incentive alignment by reducing ECC's exposure to ZEC upside.

This was one of the questions put to long-standing forum members in a [poll](https://www.zfnd.org/blog/zip-1014-poll-results/) on the [Helios](https://vote.heliosvoting.org/faq) voting platform, the [results](https://vote.heliosvoting.org/helios/elections/43b9bec8-39a1-11ea-914c-b6e34ffa859a/view) of which indicated that 56 did not want a cap while 18 did. Voters also opted to limit ECC's share of rewards to 35%, the smallest of the options presented. All that remains is for the Zcash Foundation and ECC to finalize the details of the agreement, and 20% of the ZEC rewards will be going to the ECC (35%), Zcash Foundation (25%) and major grants (as decided by a panel selected by the Foundation, 40%) - until the next halvening epoch, when the dance begins anew.

A related disagreement as part of this final round of polling was about the importance of holding a coin holder vote. This involved [two](https://forum.zcashcommunity.com/t/staked-poll-on-zcash-dev-fund-debate/34846/121) [comprehensive](https://forum.zcashcommunity.com/t/community-sentiment-polling-results-nu4-and-draft-zip-1014/35560/375) discussions on the ZEC forum (nice to see Decred [mentioned](https://forum.zcashcommunity.com/t/staked-poll-on-zcash-dev-fund-debate/34846/210), there seems to be a contingent of the ZEC community who would like to move to a Decred-style approach). In the end, the coin vote turned into more of a discussion, as can be seen in this dashboard (warning: Google Drive [link](https://docs.google.com/spreadsheets/d/e/2PACX-1vSlHXhA_NoJy0RW3Gc6YY3bmYcKT_YF8oS_BrSkBnvEGGaJ56WYo7iL_9shuoh-z_DZMYojA6FpLoJv/pubhtml)).

Round 4 of the Gitcoin Quadratic Funding experiment happened, and this [writeup](https://vitalik.ca/general/2020/01/28/round4.html) by Vitalik Buterin gives an account of how it went. This round added a Media grants stream, with a smaller matching budget ($75,000) than the main Tech grants stream ($125,000). In the early stages @antiprosynth, a prominent Ethereum Twitter personality, was in line to receive $20,000 in matching funds, but after some campaigning about this other initiatives received more donations and the share of matching funds for this Twitter account was reduced to $11,393. There was some further [controversy](https://twitter.com/TrustlessState/status/1217894717909848067) in the Media grants category as one of the projects involved a private group that would get privileged access to the outputs. The main beneficiary in the Tech grants category was Tornado.cash, a smart-contract based ETH mixer.

Jiang Zhuoer revealed a [plan](https://medium.com/@jiangzhuoer/infrastructure-funding-plan-for-bitcoin-cash-131fdcd2412e) to fund development of Bitcoin Cash software with 12.5% of the BCH block reward. This would be enforced for all miners by a majority of mining power, and in its initial form would have channelled all funding to a specified company. After receiving pushback from some people in the BCH community a revised [version](https://read.cash/@Jiang_Zhuoer_BTC.TOP_CEO/bch-miner-donation-plan-update-a45daad6) of the plan was published. In this new version miners will choose which of a set of pre-approved development projects to donate the 12.5% of their block rewards to. If a miner does not like any of the available options they can choose to burn that portion of their rewards instead of donating. The post also seems to suggest reducing the donation rate from 12.5% to 2-3%, and makes it clear that the details of the plan are still open to discussion. There will be a round of hashrate voting before implementation, and an interim Foundation to receive donations from miners and others, who will have votes in proportion to their donated funds.

After years of delays to Dash Evolution (a suite of usability changes like user names and address books), a version of this now called Dash Platform was [released](https://dashnews.org/long-awaited-dash-evolution-platform-released-on-testnet-with-developer-documentation-hub/) on a public testnet. This is to be the first of many testnet releases ahead of any mainnet release.

After [failing](https://www.reddit.com/r/dashpay/comments/egl6eu/dash_force_news_defunded_by_masternodes/) to secure funding from the Dash Treasury for the first time in 3 years, Dash Force has opted to [disband](https://app.dashnexus.org/proposals/dash-force-q1-2020/overview) their operations after [criticism](https://www.reddit.com/r/dashpay/comments/esaf38/lets_talk_about_dash_force_news/) from the community.

A European Central Bank [working paper](https://www.ecb.europa.eu/pub/pdf/scpwps/ecb.wp2351~c8c18bbd60.en.pdf?9bd63a4ddea2300dca05f2ccaa08c0e0) has indicated that the ECB would need to control the volume being used of any Central Bank Digital Currency (CBDC). One [analysis](https://cointelegraph.com/news/europe-central-bank-proposes-unattractive-rates-for-digital-currency) of the paper suggested that unattractive rates would be set for large holdings to discourage heavy use of the digital currency. One concern about heavy use of a CBDC would be that holders could move their funds outside the ECB's jurisdiction more easily in times of crisis.

Perpetrators of the PlusToken scam are [still](https://blog.chainalysis.com/reports/plustoken-scam-bitcoin-price) churning and selling the ill-gotten 180,000 BTC from their Ponzi scheme. Although 6 people have been arrested in connection with PlusToken, the funds are still moving and being sold through OTC trades on Huobi [apparently](https://blog.chainalysis.com/reports/plustoken-scam-bitcoin-price) - possibly affecting the BTC price. The scammers' tokens are being tracked despite their use of mixing and 24,000 transactions involving 71,000 addresses to try and make this difficult - because they re-used an address. While an estimated $185 million worth of the BTC has been sold, 790K ETH of a total 800K remains untouched.

The custodial bitcoin wallet provider Bottle Pay [shut down](https://www.coindesk.com/bitcoin-app-bottle-pay-shuts-down-over-impending-eu-money-laundering-laws) in December, citing the AMLD5 EU regulation coming into effect Jan 10, 2020. From the [announcement](https://bottlepay.helpscoutdocs.com/article/40-official-announcement-on-the-shutdown-of-bottle-pay): "The amount and type of extra personal information we would be required to collect from our users would alter the current user experience so radically, and so negatively, that we are not willing to force this onto our community". Standing by the principles and shutting down is the opposite of doing [whatever it takes](https://thenextweb.com/hardfork/2018/09/05/shapeshift-cryptocurrency-exchange-kyc/) to keep the business afloat. The case can serve as a yet another signal to focus efforts on improving self-custodial crypto software.

Kraken Security Labs [disclosed](https://blog.kraken.com/post/3662/kraken-identifies-critical-flaw-in-trezor-hardware-wallets/) a critical security flaw in both Trezor One and Trezor Model T that allows to extract the seed within 15 minutes of physical access to the device. "The attack takes advantage of inherent flaws within the microcontroller used in the Trezor wallets. This unfortunately means that it is difficult for the Trezor team to do anything about this vulnerability without a hardware redesign.". The recommended protections are to not allow anyone physical access to the device and to enable the Passphrase feature in the Trezor Client software.

$500 billion being pumped into the overnight money (repo) market by the Fed has drawn the attention of Colin Harper of Bitcoin Magazine, in a good [article](https://bitcoinmagazine.com/articles/the-fed-has-pumped-500-billion-into-the-repo-market-where-does-it-end) that introduces the subject and asks what is going on.

## About This Issue

This is issue 22 of Decred Journal. Index of all issues, mirrors and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, Dustorf, kozel, richardred, s\_ben
- reviews and feedback: ammarooni, buck54321, davecgh, dnldd, emiliomann, jholdstock, lukebp, matheusd
- title image: saender
