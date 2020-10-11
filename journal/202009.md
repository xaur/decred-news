# Decred Journal – September 2020

![abstract art](../img/journal-202009-384.png)

_Image: Hidden Structures on Quadratic Orbit by @saender_

Decred's highlights for September:

- The decentralize Treasury spending PR is finally merged, after a comprehensive review process.
- dcrdex is addressing many sophisticated trustless swap scenarios discovered in early testing, the first mainnet swap was conducted in early Oct and the MVP should be ready for general use soon.
- The first RFP proposal on Politeia, to change messaging on decred.org, was approved, and received 4 candidate proposals. Voting will begin on these soon.
- The dcronchain.com on-chain metrics site, as approved by a proposal in June, has now launched.
- The withdecred.org onboarding portal had its initial launch, and also had an associated proposal submitted to fund promotional giveaways, approved in early Oct.

## Development

Unless otherwise noted, the work reported here has the "merged to master" status. It means that the work is completed, reviewed, and integrated into the source code that advanced users can build and run, but is not yet available in release binaries for regular users.

[dcrd](https://github.com/decred/dcrd):

The decentralize treasury spending [pull request](https://github.com/decred/dcrd/pull/2170) is [merged](https://twitter.com/marco_peereboom/status/1308125042149134336) to master. It got 576 review comments, changed 115 files, added 15K lines of code, and took 5 months since the first draft was published. Several developers have been pulled from other projects to thoroughly review and test this consensus-critical code. Thanks to everyone for the hard work on this epic change!

DCP0006 describing the upcoming consensus change is under [review](https://github.com/decred/dcps/pull/17).

Merged follow-up treasury work:

- one-way [migration](https://github.com/decred/dcrd/pull/2336) of the database to support the new treasury implementation
- [tracking](https://github.com/decred/dcrd/pull/2350) of tspend (treasury spend) transactions in the mempool
- new peer messages to [relay](https://github.com/decred/dcrd/pull/2349) tspend transactions as nodes startup (this is to help both mining nodes and the voting wallets discover tspends in a timely manner)
- new RPC command to [tally](https://github.com/decred/dcrd/pull/2351) the vote count of tspend transactions (initially only tspends in the mempool or that were mined can be queried)
- removed [footguns](https://github.com/decred/dcrd/pull/2389) from code for calculating tspend window values
- reworked [consistency](https://github.com/decred/dcrd/pull/2394) in the `standalone` package and brought the test coverage back to 100%

Other merged work:

- optimized signature [cache](https://github.com/decred/dcrd/pull/2358) to proactively evict entries related to transactions in a block that is already 2 blocks deep
- consolidated ban [disable/whitelist](https://github.com/decred/dcrd/pull/2363) logic
- more restrictive systemd service [privileges](https://github.com/decred/dcrd/pull/2357)
- updated [checkpoints](https://github.com/decred/dcrd/pull/2370) and min known [chain work](https://github.com/decred/dcrd/pull/2371) for the upcoming release
- dependency updates to prepare for the release
- lots of smaller improvements in test coverage, logging, error handling, etc

@matheusd wrote a standalone [tool](https://github.com/matheusd/tspend) to generate tspend transactions that can be used on air-gapped setups (without requiring a network connection to an underlying dcrd instance). It works in combination with @jrick's [ss](https://github.com/jrick/ss) tool for post-quantum file and stream encryption.

[dcrwallet](https://github.com/decred/dcrwallet):

- decentralized treasury spending [support](https://github.com/decred/dcrwallet/pull/1714), including a new tool for network operators to generate treasury keys
- [warn](https://github.com/decred/dcrwallet/pull/1822) when dumping extended public keys (if the xpub is leaked in combination with any account private key, this reveals all private keys of the account)
- handle [change](https://github.com/decred/dcrwallet/pull/1830) for unmixed ticket buying
- saving of [unpublished](https://github.com/decred/dcrwallet/pull/1838) transactions to the database (necessary to prevent some previous wallet outputs from being double spent across restarts, or to persist partially signed tx; this will be used by vspd clients)
- new flag to only add tickets [manually](https://github.com/decred/dcrwallet/pull/1833) and not discover them through network sync (this flag will be used by vspd admins to prevent their users getting free votes by reusing their voting address. With this flag set, tickets can only be added to the vspd through the proper API)
- add redeem script for P2SH [listunspent](https://github.com/decred/dcrwallet/pull/1842) results (this is for dcrdex)
- changes to support [vspd](https://github.com/decred/dcrwallet/pull/1840)
- implemented [sendrawtransaction](https://github.com/decred/dcrwallet/pull/1846) method
- extensive testing by vspd and dcrdex clients helped to identify and fix numerous bugs

[Decrediton](https://github.com/decred/decrediton):

- reuse [checkbox](https://github.com/decred/decrediton/pull/2663) component from pi-ui
- continued refactoring to functional components and CSS modules
- multiple bug fixes

In progress:

- LN [watchtower](https://github.com/decred/decrediton/pull/2638) support
- LN [UI/UX](https://github.com/decred/decrediton/pull/2641) improvements

[Politeia](https://github.com/decred/politeia):

- added [tests](https://github.com/decred/politeia/pull/1296) for the user database
- optimized memory usage with [pagination](https://github.com/decred/politeia/pull/1306)
- admin TOTP [reset](https://github.com/decred/politeia/pull/1298) command

CMS:

- added user [search](https://github.com/decred/politeiagui/pull/2131) back
- replaced remaining [cache](https://github.com/decred/politeia/pull/1300) usage to clear the way for tlog migration
- added [LevelDB](https://github.com/decred/politeia/pull/1302) implementation for testing infrastructure

In progress:

- 2FA login with [TOTP](https://github.com/decred/politeia/pull/1212) (time-based codes)
- querying contractor's [code stats](https://github.com/decred/politeia/pull/1185) for CMS admins
- tlog implementation on the [backend](https://github.com/decred/politeia/pull/1180) and the [GUI](https://github.com/decred/politeiagui/pull/2142)

Status update from @lukebp:

> Most of the politeia development was focused on tlog this past month. The frontend and backend work to match the existing politeia functionality is complete. The next few weeks are focused on testing tlog, working through bugs, writing documentation, and adding test coverage to the code. The only feature that has yet to be implemented is the ability to retrieve the inclusion proof for a specific piece of politeia data. The politeiad backend currently supports this, but the corresponding politeiawww routes need to be added as well as a way to display/download the inclusion proofs in the GUI. This functionality will be added before launch.

[vspd](https://github.com/decred/vspd):

- store records of up to 10 vote choice [changes](https://github.com/decred/vspd/pull/180) for each ticket, for two-way accountability
- require that dcrwallet runs in [manual tickets](https://github.com/decred/vspd/pull/187) mode

[dcrpool](https://github.com/decred/dcrpool):

- updated the codebase to Go 1.13 [error types](https://github.com/decred/dcrpool/pull/245)
- fixed reconnection [error](https://github.com/decred/dcrpool/pull/247)

[dcrlnd](https://github.com/decred/dcrlnd):

- the PR for [porting](https://github.com/decred/dcrlnd/pull/103) the upstream work has been updated with all work done up to [v0.11.1-beta](https://github.com/lightningnetwork/lnd/releases/tag/v0.11.1-beta) version. That'll bring us on par with the current latest lnd release.

[dcrdex](https://github.com/decred/dcrdex):

- implemented [order history](https://github.com/decred/dcrdex/pull/644) view with filters and infinite scrolling, and order details view with all matches and relevant transaction outputs
- show amounts [locked](https://github.com/decred/dcrdex/pull/683) in contracts and update balances in more cases
- added [`match_status`](https://github.com/decred/dcrdex/issues/643) and [`order_status`](https://github.com/decred/dcrdex/pull/687) routes to recover from unusual cases discovered in testing, like laptops suspending or poor connectivity causing clients to miss the `revoke_match` step (restarting the dexc program fixed it but it was poor UX)
- improved [reconnection](https://github.com/decred/dcrdex/pull/663) handling
- more robust handling of [missing](https://github.com/decred/dcrdex/pull/661) matches
- return [active orders](https://github.com/decred/dcrdex/pull/677) on `connect` response
- [unlock](https://github.com/decred/dcrdex/pull/648) coins in more cases when no longer needed (read [this](https://github.com/decred/dcrdex/pull/648#issuecomment-688585289) random comment to get a taste of how many cases must be considered in a trustless swap protocol)
- [notify](https://github.com/decred/dcrdex/pull/649) user of penalty
- grace period for new users when [cancellation](https://github.com/decred/dcrdex/pull/638) rate threshold is not enforced
- better handling of [redemption](https://github.com/decred/dcrdex/pull/513) when Maker goes dark after Taker swap
- multiple [inaction](https://github.com/decred/dcrdex/pull/680) check fixes
- require [password](https://github.com/decred/dcrdex/pull/621) for client RPC
- opt-in debug [logging](https://github.com/decred/dcrdex/pull/654) in the UI
- many internal changes and bug fixes

A total of 35 PRs from 4 contributors were [merged](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-09-01..2020-09-30+sort%3Aupdated-asc), adding 9K and deleting 2.6K lines of code.

Twitter [poll](https://twitter.com/chappjc/status/1302795835248439296) showed interest in LTC support in mainnet beta.

> The first DCR-BTC mainnet atomic swaps coordinated by #dcrdex were conducted yesterday. Testing and development continues, but talk has moved to software distribution and tutorials. Exciting times for @decredproject. (@chappjc on [Oct 9](https://twitter.com/chappjc/status/1314436781891301376))

[dcrandroid](https://github.com/planetdecred/dcrandroid):

- updated [Chinese](https://github.com/planetdecred/dcrandroid/pull/515) translation
- bug fixes

In progress:

- show Politeia [proposals](https://github.com/planetdecred/dcrandroid/pull/503)

[dcrios](https://github.com/planetdecred/dcrios):

- bug fixes

In progress:

- show Politeia [proposals](https://github.com/planetdecred/dcrios/pull/715)
- automated UI [testing](https://github.com/planetdecred/dcrios/pull/707)

[dcrros](https://github.com/decred/dcrros):

- [updated](https://github.com/decred/dcrros/pull/6) to the v1.4.4 of the Rosetta specs which includes the ability to construct, sign, and publish transactions. The `check:construction` suite of tests of the corresponding rosetta-cli for this spec is passing on this PR.

Rosetta v1.4 released the [Construction API](https://www.rosetta-api.org/docs/construction_api_introduction.html) (formerly Wallet API) for constructing transactions in a standard format, which was not finished when we announced Decred's Rosetta implementation back in [June](202006.md). This API is supported by the latest dcrros and work is ongoing to keep it up with the spec, as well as the upcoming changes in Decred consensus.

[docs](https://github.com/decred/dcrdocs):

- replaced example dev [proposal](https://github.com/decred/dcrdocs/pull/1127) with a larger scale one
- replace OS-specific collapsible sections with proper [tabs](https://github.com/decred/dcrdocs/pull/1129)

[dev docs](https://github.com/decred/dcrdevdocs):

- [Ticket Selection](https://devdocs.decred.org/developer-guides/ticket-selection/) page [moved](https://github.com/decred/dcrdocs/pull/1126) from dcrdocs
- [Overview](https://devdocs.decred.org/developer-guides/transactions/txscript/overview/) and [Opcodes](https://devdocs.decred.org/developer-guides/transactions/txscript/opcodes/) reference [added](https://github.com/decred/dcrdevdocs/pull/86) for the txscript system used in Decred (it is a simple, stack-based, Forth-like programming language)

[decred.org](https://github.com/decred/dcrweb):

- added [Latam](https://github.com/decred/dcrweb/pull/909) contributors
- backend updates

Other:

- Bug Bounty program posted a new [update](https://bounty.decred.org/2020/09/status-update/) and made [changes](https://github.com/decred/dcrbounty/pull/71/files) to the rules and scope based on experience with recent submissions

## People

Community stats as of Oct 1:

- Twitter followers: 40,790 (-26)
- Reddit subscribers: 9,929 (+23)
- Matrix #general users: 197 (+23)
- Discord users: 1,396 (+2)
- Telegram users: 2,434 (-34)
- YouTube subscribers: 4,210 (+30), views: 156K (+1.7K)
- LinkedIn followers: 891 (+16)
- GitHub dcrd stars: 563 (+6), forks: 248 (+2)

Charts of these stats are available in the [social-media-stats](https://github.com/decredcommunity/social-media-stats/blob/graphs/graphs/index.md) repository (more accounts tracked) and on Planet Decred's [dcrextdata](https://dcrextdata.planetdecred.org/community) instance (dynamic charts with high resolution).

## Governance

In September the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 12,300 DCR and spent 5,740 DCR. Using September's daily average DCR/USD rate of $13.26, this is $163K received and $76K spent. At August's average daily rate of $17.02, the USD figure billed for work completed in that month is $98K. As of Oct 3, Treasury balance is 640,000 DCR (7.5 million USD at $11.69).

- The [proposal](https://proposals.decred.org/proposals/1e55a41) from @Exitus for video production was approved with 94.6% yes votes and turnout of 31%.
- A [proposal](https://proposals.decred.org/proposals/2bf72e6) to promote the new withDecred.org site with DCR giveaways was submitted in Sep and approved in early Oct with 62% yes votes and 37% turnout.
- A [proposal](https://proposals.decred.org/proposals/f279ed5) to pay @alexsolo for work done in 2016-18 was rejected with 8% yes votes and turnout of 28%.
- An RFP [proposal](https://proposals.decred.org/proposals/91becea) to change the messaging on decred.org was approved with 85% approval and 29% turnout. There were 4 proposals submitted before the deadline of Sep 28, and once they are all ready run-off voting will begin. Only one of these proposals can be approved, and it still has to meet the usual approval and quorum requirements.

See Politeia Digest [issue 36](https://blockcommons.red/politeia-digest/issue036/) and [issue 37](https://blockcommons.red/politeia-digest/issue037/) for more detailed coverage of proposals.

@bee published a comprehensive [checklist](https://github.com/decredcommunity/guidelines/blob/master/proposals.md) for successful Politeia proposals based on experience with past proposals.

4 proposal updates have been imported in the [proposals](https://github.com/decredcommunity/proposals/tree/master/proposals) repository. There is no convenient index yet but direct links work ([example](https://github.com/decredcommunity/proposals/blob/master/proposals/95cfb73/updates/20200902.md)). Please submit your updates to help collect them all in one place.

## Network

Hashrate: September's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kegbelov-kfrbnmg7&scale=linear&bin=block&axis=time) opened at ~460 Ph/s and closed ~450 Ph/s, bottoming at 338 Ph/s and peaking at 609 Ph/s throughout the month. Pool hashrate [distribution](https://miningpoolstats.stream/decred) as of Oct 1: UUPool 35%, Poolin 27%, Huobipool 11%, easy2mine 10%, Antpool 9%, BTC.com 3%, Luxor 0.9%, F2Pool 0.5%, okex 0.2%, CoinMine 0.02%, and the rest ~3%. Note that we have switched from [dcrstats.com/pow](https://dcrstats.com/pow) to [miningpoolstats.stream](https://miningpoolstats.stream/decred) because the latter identifies about ~20% more hashrate.

Staking: [30-day average](https://dcrstats.com/) ticket price was 148.6 DCR (-2.8). The [price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kegbelov-kfrbnmg7&bin=window&axis=time&visibility=true-false&mode=stepped) varied between 144.7-152.5 DCR. [Locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kegbelov-kfrbnmg7&bin=block&axis=time) was 6.06-6.12 million DCR, which corresponded to 50.38-51.04% of the available supply [participating](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kegbelov-kfrbnmg7&bin=block&axis=time) in PoS.

Nodes: Throughout [September](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1598918400000&to=1601510400000) there was an average of 108 public listening nodes and 133 total nodes per dcr.farm. Average version distribution for September: 26% dcrd v1.5.1, 22% dcrd v1.5.2, 7% dcrd v1.6 dev builds, 7% dcrd v1.5.0, 4% dcrd v1.5 dev and RC builds, 0.8% dcrd v1.4, 17% dcrwallet v1.5.1, 1.6% dcrwallet v1.5, 1.1% dcrwallet v1.4, 15% others.

[dcronchain.com](https://dcronchain.com/) has launched four months since its [proposal](https://proposals.decred.org/proposals/0230918) was approved in June. The initial version includes 5 interactive charts derived from Decred's on-chain data, based on research by @Checkmate and @PermabullNino. The team is welcoming any feedback on [Reddit](https://www.reddit.com/r/decred/comments/j3589s/release_dcronchaincom_onchain_researchgraphs_in/). Source code is available on [GitHub](https://github.com/Decred-Bulls/dcronchain). Congrats with the launch!

## Integrations

Brazilian NovaDAX exchange that [listed](https://twitter.com/Decred_BR/status/1275190825060794377) DCR in June now [added](https://twitter.com/Decred_BR/status/1305922555124035584) DCR support on their debit cards. This will allow access to over 23,000 ATMs and POS terminals around the country.

> NovaDAX is top 3 in the BR market. With the new debit card, it's possible to pay any bill in places that accept [Elo](https://en.wikipedia.org/wiki/Elo_(card_association)), which in Brazil has the same adoption as Visa and Mastercard. In addition, it's possible to make bank transfers in BRL, deducting DCR from your account and without paying transfer fees, something that all banks in Brazil charge for. It's also possible to exchange DCR for BRL in Banco24horas ATMs, with around 23 thousand machines in Brazil. NovaDAX is opening a branch in Portugal and intends to do the same in the European market. ([@emiliomann](https://matrix.to/#/!rLQWsgjPJFAClvskmU:decred.org/$QD-Fxk-3mm9wiuR3f1DQqJ-K4yQQcFFmoQYfx8r40jE))

Australian [Swyftx](https://swyftx.com.au/) was [added](https://github.com/decred/dcrweb/pull/907) to decred.org, although it had DCR for a while. The exchange has many [features](https://swyftx.com.au/features/) and allows users to buy DCR with AUD.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

@Exitus' second [proposal](https://proposals.decred.org/proposals/1e55a41) for making video content for another 6 months was approved with very high support. @Checkmate will join in the second phase to help with scripts and feedback. The proposal shared some stats for the last 6 months: 21K views gained with 98% like rate, ~500 subscribers gained and ~250 lost, 170 comments received. The most popular video was [DCR 101 - How to Stake Decred 2020](https://www.youtube.com/watch?v=m5lcm6yttEk) with 1.6K views. Various videos uploaded to Twitter gained ~18K views.

@pavel, @pablito, and @el\_capitan [launched](https://www.reddit.com/r/decred/comments/it9mkf/withdecredorg_new_portal_to_onboard_newcomers_to/) a new website [withdecred.org](https://withdecred.org/) to find a new scalable approach for how to onboard new users to Decred community. The website contains a series of articles that form a structured "funnel" that leads the person to purchase a few DCR. A [proposal](https://proposals.decred.org/proposals/2bf72e6) followed to fund the operations and a distribution of $5,000 worth of DCR to drive initial engagement, approved in early October. Historically, some community members have been skeptical about giveaways and this project will finally bring some empirical data and gauge the ROI of that model. Companion Twitter handle is [@withdecred](https://twitter.com/withdecred).

A few community members [organized](https://www.reddit.com/r/decred/comments/it0idm/decred_on_quora/) to answer a stash of questions about Decred on Quora.

@pavel started experimenting with publishing [Decred](https://www.publish0x.com/withdecred/why-we-need-decred-an-inclusive-approach-to-sound-money-xgdwkjl) [content](https://www.publish0x.com/crypto-as-an-agent-for-change/monero-and-decred-are-the-new-bitcoin-xlldpze) on Publish0x since it is a [promising](https://github.com/Decred-Bulls/decred-marketing#why-to-invest-time-into-publish0xcom) crypto portal.

@pablito and @caibarrad launched the first episode of Decred en Español podcast, available on [YouTube](https://twitter.com/Decred_ES/status/1310654270056923136) and [Spotify](https://twitter.com/Decred_ES/status/1310055071200292869).

@jazzah posted a [contest](https://www.reddit.com/r/decred/comments/ifyb03/contest/) themed "KYC vs Shuffle++" where participants need to complete non-trivial tasks by inspecting a crazy hilarious image. Prize #1 has been claimed but prizes 2-4 are still open for anyone.

Monde PR's achievements for September:

- created/pitched 2 story ideas to the finance and crypto publications
- responded to 3 requests for comments
- responded to 2 news stories about DCR

News coverage secured by Monde PR:

- an article in [Authority Magazine](https://medium.com/authority-magazine/meet-the-disruptors-how-jake-yocom-piatt-of-decred-aims-to-redefine-governance-with-blockchain-5c3724f20e74) featuring commentary by @jy-p on how Decred aims to redefine governance with blockchain technology
- an article in [AMB Crypto](https://eng.ambcrypto.com/will-defi-crash-the-crypto-economy-the-same-way-cdos-did/) featuring commentary by @richardred on the 'DeFi bubble', syndicated to 12 news outlets including [Crypto Fund Report](https://www.cryptofundreport.com/articles/will-defi-crash-the-crypto-economy-the-same-way-cdos-did/) and [Coingenius.news](https://coingenius.news/will-defi-crash-the-crypto-economy-the-same-way)
- an article in [The Daily Chain](https://thedailychain.com/decred-clarify-details-of-reported-vulnerability/) featuring commentary by @davecgh clarifying details of a reported vulnerability

## Events

Attended:

- Sep 4 - [Hablemos Decred 11](https://twitter.com/Decred_ES/status/1301583356644282368) - Internet. @elian and guest Jose Zarate from Stamping.io discussed timestamping on blockchains. ([video](https://www.youtube.com/watch?v=QwsWiJ8v5qE))
- Sep 10 - [Hablemos Decred 12](https://twitter.com/Decred_ES/status/1304153821631791104) - Internet. @caibarrad and @elian invited David Riascos from @cLabs to talk about the importance of the community in the development of open protocols and the challenges of adoption in the cryptocurrency industry. ([video](https://www.youtube.com/watch?v=QC5_1PqJb_4))
- Sep 17 - [Hablemos Decred 13](https://twitter.com/Decred_ES/status/1305595709257846785) - Internet. @adcade and @elian talked with guest Nancy Salazar from Platzi about how to start a career in technology and how to overcome the challenges of complex areas such as blockchains. ([video](https://www.youtube.com/watch?v=f_ppC-GVDk8))
- Sep 25 - [Hablemos Decred 14](https://twitter.com/Decred_ES/status/1308582624772927494) - Internet. @elian and guest Eloisa Cadenas from CryptoFintech explored the origins of [maximalism](https://es.cointelegraph.com/news/wild-crypto-maximalism), the risks of such lines of thought, the future of interoperable blockchains and what are the challenges for adoption and innovation in the cryptocurrency space. The event was [announced](https://es.cointelegraph.com/news/virtual-talk-where-does-the-concept-of-maximalist-come-from) on Cointelegraph Spanish. ([video](https://www.youtube.com/watch?v=EGaMhQX3Wd4))

Upcoming:

- Oct 15 - Hablemos Decred 17 - Internet. @elian and Gus Grilliesca will explore the future of art and cryptocurrencies.
- Oct 17 - [Introduction to blockchain API](https://www.eventbrite.com/e/open-source-workshop-introduccion-a-blockchain-api-de-decred-dcrdata-tickets-124107662359) - Internet. A workshop to explore Decred blockchain with dcrdata API.
- Oct 19 - [Open Source Software Summit](https://www.eventbrite.com.mx/e/cumbre-de-contribuidores-de-open-source-software-ccoss-2020-tickets-91491063233) - Internet. @adcade will present Decred with the talk "open source contractor model in the cryptocurrency industry".

## Media

Decred was mentioned in a long [report](https://medium.com/greenfield-one/the-state-of-blockchain-governance-governance-by-and-of-blockchains-f6418c46077) on blockchain governance. Full 115-page PDF is [here](https://65eocu3ftlpiygeym3g5kply6zy2dtdjyrhbm4m26cb6bt3msyla.arweave.net/90jhU2Wa3owYmGbN1T149nGhzGnEThZxmvCD4M9slhY) (Decred on pages 64-66).

Selected articles:

- Why I Decred by Decred Citizen ([medium](https://medium.com/@decred.citizen/why-i-decred-8d83081b6fb8))
- Decred on-chain: DAO + Treasury accounting by @permabullnino ([medium](https://medium.com/@permabullnino/decred-on-chain-dao-treasury-accounting-afb1ed989b0a))
- Blockchain governance - Part 2 by @mm ([stakey.club](https://stakey.club/en/blockchain-gov-part2/))
- Meet the Disruptors: How Jake Yocom-Piatt of Decred aims to redefine governance, with blockchain technology by Tyler Gallagher ([medium](https://medium.com/authority-magazine/meet-the-disruptors-how-jake-yocom-piatt-of-decred-aims-to-redefine-governance-with-blockchain-5c3724f20e74))
- Monero and Decred are the new Bitcoin by John Dennehy ([medium](https://medium.com/@john_dennehy/monero-and-decred-are-the-new-bitcoin-34a8c1fb2515))

> Since decentralization is a founding principle of the crypto-space it gets a lot of lip-service but one of the oldest problems with power is that it is extremely rare that once someone has it, they will give it up voluntarily. Decred is a rare exception and notable in the progress its developers have made in converting the project's resources into this autonomous system. Monero is another outlier here, as its development is completely funded by community donations.

Crypto media has picked up the [INVDoS](https://invdos.net/) vulnerability disclosed on Sep 9, which brought some mixed press for Decred. [CoinDesk](https://www.coindesk.com/high-severity-bug-in-bitcoin-software-revealed-2-years-after-fix) release was the first and didn't mention Decred at all. Notably, it was published just 45 min after the PDF was last updated at invdos.net and 28 min _before_ the email on [bitcoin-dev](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2020-September/018164.html) mailing list. [ZDNet](https://www.zdnet.com/article/researcher-kept-a-major-bitcoin-bug-secret-for-two-years-to-prevent-attacks/) briefly mentioned Decred's bug bounty program. [Decrypt](https://decrypt.co/41685/developers-reveal-2018-bitcoin-bug-used-to-crash-entire-networks) has overblown the issue and posted some inaccuracies. [The Daily Chain](https://thedailychain.com/bitcoin-engineers-identify-and-patch-vulnerability-in-decred-btcd-blockchains/) went as far as to say that "Bitcoin engineers patched vulnerability in Decred". A common pattern is that these outlets didn't reach out for comments from the experts most familiar with the software (Decred developers). @l1ndseymm contacted The Daily Chain and they posted a follow-up [clarification](https://thedailychain.com/decred-clarify-details-of-reported-vulnerability/) with a comment from @davecgh. @degeri addressed the misinformation in a tweet [thread](https://twitter.com/degeri_crypto/status/1305591774698786821). A detailed account of media coverage, misinformation, timeline of events and reflection is available [here](https://github.com/xaur/notes/blob/master/invdos.md).

Translations:

- Meet the Disruptors: How Jake Yocom-Piatt of Decred aims to redefine governance, with blockchain technology - [in Chinese](https://github.com/Decred-CN/articles/blob/master/Meet%20The%20Disruptors.md) by @Dominic
- Politeia Digest issues 36-37 - [in Arabic](https://insaf01.github.io/politeia-digest-ar/) by @arij and @abdulrahman4
- Decred Journal August 2020 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic) and Spanish (@francov\_). Thank you all for spreading the word!

A list of all known translations of Decred content has been compiled [here](https://github.com/decredcommunity/translations/blob/master/index.md). If you enjoy DJ for reading about all the work being done for Decred, open this ~280 item list and scroll it for a minute to get a similar injection.

If you translate content, join the new public [#translations](https://chat.decred.org/#/room/#translations:decred.org) chat room to coordinate with others.

Videos:

- The Cost of attacking Decred by Decred Society ([youtube](https://www.youtube.com/watch?v=yv2wzRsK6zc))
- Security and coin supply by Decred Society ([youtube](https://www.youtube.com/watch?v=M5HWV_a1gj8))
- Going down the Decred rabbit hole by Decred Society ([youtube](https://www.youtube.com/watch?v=cI1jbIAe4YE))
- Decred price analysis - 6th September 2020 by Brave New Coin ([youtube](https://www.youtube.com/watch?v=ABjp9RYnDrk))

Audio:

- Decred in Depth 30 with @eSizeDave and @zohand of the Decred Australia team talking about their experiences presenting Decred to various audiences - what sticks, and what misses ([libsyn](https://decredindepth.libsyn.com/zohand-dave-decred-australia), [player.fm](https://player.fm/series/decred-in-depth/zohand-dave-decred-australia))
- Decred in Depth 31 with @l1ndseymm giving her take on the role of PR, her experience of working with Decred's community and going through the proposal process, and strategies for raising the project's profile. ([libsyn](https://decredindepth.libsyn.com/lindsey-mcconaghy-dcr-pr-marketing-2020), [anchor.fm](https://anchor.fm/staked-podcast/episodes/Staked-Podcast-Episode-0-0-3-ejq685/a-a38c12o))
- Cyber Hacker podcast: Crypto-Security and blockchain innovations featuring @jy-p ([player.fm](https://player.fm/series/cyber-hacker/crypto-security-and-block-chain-innovations), [apple](https://podcasts.apple.com/au/podcast/cyber-hacker/id1462830605?i=1000489977562))

The Decred dork has been busy this month, with 4 episodes of the new Staked Podcast:

- Episode 0.0.1 - History of Decred
- Episode 0.0.2 - Decred Constitution
- Staked podcast interview with @pavel
- Episode 0.0.3 - Decred investment thesis

Staked Podcast is available on [YouTube](https://www.youtube.com/channel/UCWoknbkENz-W4pg18p57rNA) (with video), [anchor.fm](https://anchor.fm/staked-podcast), [Spotify](https://open.spotify.com/show/4KWpxBXn26Ek4VVeNg8D3S) and [Google](https://podcasts.google.com/feed/aHR0cHM6Ly9hbmNob3IuZm0vcy8xNDY5ZjRlYy9wb2RjYXN0L3Jzcw==).

## Community Discussions

Comm systems news:

- traders rejoice, #trading chat is now available via [Telegram](https://t.me/DecredTrading) and is bridged to Matrix and Discord

Selected Reddit posts:

- everyone's favorite Wall Street CEO, u/jamie-demon, has been busy publishing [dcrdocs](https://www.reddit.com/r/decred/comments/j1ia6k/dcrdocs_on_ipfs_and_zeronet/), [decredpower](https://www.reddit.com/r/decred/comments/iu9f31/decredpower_on_the_ipfs/), and [DCRComic](https://www.reddit.com/r/decred/comments/iw333o/dcr_comic_on_ipfs/) to IPFS and ZeroNet distributed web networks
- a [post](https://www.reddit.com/r/decred/comments/iwu75w/bch_has_some_funding_and_governance_issues/) about BCH funding and governance issues attracted 45 comments, mostly in response to someone complaining about DCR
- @pavel is arranging an AMA interview and submitted a [post](https://www.reddit.com/r/decred/comments/j2gz5f/ask_me_anything_ama_what_would_you_ask_decreds/) to collect questions at the end of the month
- in-depth [discussion](https://www.reddit.com/r/decred/comments/i11tjv/porting_cloak_coins_enigma_protocol_and/g4psjpr/) about the merits of CloakCoin's Enigma privacy protocol with one of that project's developers

Selected Twitter discussions:

- @richardred [tweeted](https://twitter.com/RichardRed0x/status/1310700935216271360) an animated painting, titled "Ticket Price All Time Highs Again"
- latest development news breaking on twitter from [@moo31337](https://twitter.com/marco_peereboom/status/1308125042149134336) (Decentralize Treasury Spending) and [@chappjc](https://twitter.com/chappjc/status/1302798545439817730) (dcrdex)
- @jz asserts that Decred is a [#ChadCoin](https://twitter.com/jz_bz/status/1310639727477915648)

## Markets

In September DCR was trading between USD 11.03-17.30 / BTC 0.00106-0.00148. The average daily rate was $13.26.

## Relevant External

The Wasabi wallet was subject to a DoS [vulnerability](https://blog.wasabiwallet.io/responsible-disclosure-v4-hard-fork/) which would have allowed an attacker to halt the CoinJoin process for all participants without revealing themselves - fixed before it could be exploited.

Bitcoin Cash's current situation was [summarised](https://read.cash/@Cain/the-current-bch-drama-for-outsiders-50b4dbb8) nicely by Cain. The BCH (aka BCH ABC) chain looks set to fork over a dispute about developer funding. The Bitcoin ABC developers are adding a rule from Nov 15 that 8% of the block reward must go to an address controlled by them, to fund infrastructure development. This idea has been controversial in the BCH community for some time, and an alternative BCHN implementation is planned. This sets up an interesting hash war scenario, where ABC miners will not mine on BCHN blocks without a developers' reward, whereas the BCHN miners will mine on anything - if the BCHN chain does not have a significant majority of hashpower, BCHN miners would be likely to see a lot of orphaned blocks. BCH has a checkpointing system, which adds some further intrigue around the possibility of chain splits and new nodes ending up on different chains. So far around 50% of PoW mining power is signalling for BCHN, and the rest is not signalling for anything.

BitShares has a [forthcoming](https://finbold.com/binance-huobi-announces-support-for-upcoming-bitshares-hardfork/) hardfork which is being supported by Binance and Huobi, after the BitShares China Association alleged that one of the BitShares developers had tampered with voting system code without community approval.

The SushiSwap saga provided peak DeFi drama in September. SushiSwap is a "decentralized exchange" running on Ethereum which copied the open source smart contracts of an established (VC-funded) decentralized exchange, UniSwap. When the SushiSwap developer, Chef Nomi, announced that SushiSwap would do a "fair launch" and grant almost all the SUSHI tokens to liquidity providers, SushiSwap began to draw a lot of liquidity away from UniSwap, and SUSHI gained considerable value in a short space of time. 10% of all the SUSHI tokens go into a development fund, and when the hype was peaking Chef Nomi [liquidated](https://www.coindesk.com/sushiswap-liquidation-weekend) the dev SUSHI (worth over $10 million at the time) for ETH and announced that he was not exit scamming because he would still be around to do development, but he had sold all the dev SUSHI. This was not well received by the SUSHI community, who sought to replace Nomi in short order, with Nomi then handing the reigns (keys?) to Sam Bankman-Fried of the FTX exchange. SushiSwap then went on to elect a set of multi-sig governors with a token vote. Subsequently, Chef Nomi [returned](https://www.coindesk.com/sushiswap-creator-chef-nomi-returns-dev-fund) along with the ETH they had obtained by selling dev SUSHI, offering that the community determine how much they should be rewarded for their part. There was some speculation that Chef Nomi had been effectively unmasked and did not want to live with the stigma of their hasty exit.

UniSwap [launched](https://uniswap.org/blog/uni/) their own token, UNI, in response to SUSHI's success and the amount of liquidity it was attracting. 60% of the genesis tokens (intended to cover the first four years) are available to liquidity providers, with an initial 15% being allocated to people who had used UniSwap before a cut-off of early Sep. The remaining 40% of UNI is allocated to investors and employees.

Ethereum Classic Labs have [teamed](https://medium.com/etc-core/ethereum-classic-labs-teams-up-with-openrelay-and-chainsafe-8248d1182612) up with Chainsafe and OpenRelay to develop a solution which prevents further 51% attacks. 3 days after the teaming up announcement there is already a comprehensive [MESS](https://medium.com/etc-core/agreeing-to-disagree-proposing-a-weakly-subjective-finality-solution-for-ethereum-classic-7daad47efc0e) plan for weakly-subjective finality.

The KuCoin exchange (which lists DCR) was hacked, and a [reported](https://www.coindesk.com/hackers-drain-kucoin-crypto-exchanges-funds) $150 million was stolen, later [upgraded](https://www.coindesk.com/kucoin-ceo-says-perpetrators-of-281m-hack-identified-authorities-on-the-case) to $281 million, although $204 million was subsequently [recovered](https://www.coindesk.com/kucoin-ceo-says-perpetrators-of-281m-hack-identified-authorities-on-the-case) (with help from the operators of centralized stablecoins), and KuCoin claims to have identified the suspects and reported them to law enforcement authorities.

Coinbase Pro [announced](https://twitter.com/CoinbasePro/status/1306641678506360832) that fees for crypto withdrawals would now be passed on to customers (Coinbase had previously covered these to provide "free" withdrawals).

The bZxHQ DeFi lender was subjected to another [exploit](https://www.coindesk.com/defi-lender-bzx-third-attack), this time for $8 million, which is larger than the previous two exploits earlier this year. They have an insurance fund which is covering the damage. According to CoinDesk, "the bug managed to remain undetected in two extensive code audits from cybersecurity firms Certik and Peckshield".

Square [formed](https://www.coindesk.com/square-alliance-patents-crypto) the Cryptocurrency Open Patent Alliance (COPA), where members pledge to never assert patent rights for offensive purposes, and in turn can use the patents of any member organization defensively if required. Blockstream [tweeted](https://twitter.com/Blockstream/status/1304529416131940352) about joining COPA as the next step in their defensive patent strategy.

The Polkadot Treasury received its first [proposals](https://polkadot.network/writing-history-the-first-teams-submit-their-proposal-to-the-polkadot-treasury-2/). Polkadot's Treasury is funded by transaction fees, slashing and staking inefficiencies - and every 24 days if these funds are not used 1% of the balance is burned. The funds are presently administered by the Polkadot Council, and the first four teams to be funded this way are working on a development environment for pallet-contracts, a Go Substrate RPC Client, Polkascan, and a platform for local community currencies and self-issued universal basic income.

This [article](https://decrypt.co/41024/researchers-find-new-way-for-criminals-to-launder-money-using-bitcoin) about "private mining", where a user gives their transaction to a specific miner, who collects the associated reward whenever they mine it in a block, sees it as a possible tool for money laundering, and in the future potentially also a legitimate source of miner income.

The United States Internal Revenue Service are [offering](https://cointelegraph.com/news/the-irs-offers-a-625-000-bounty-to-anyone-who-can-break-monero-and-lightning) a bounty of $625,000 to anyone who can provide a working prototype of technology to trace Monero or Lightning Network transactions. The deadline was Sep 16, so unfortunately it is now too late to cash in on that privacy-breaking prototype, if you happen to have one to hand.

Relevant External fans will likely enjoy the [@Scams_alarms](https://twitter.com/Scams_alarms) Twitter account for more horrifying stories.

## About

This is issue 30 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

You can submit a story [here](https://github.com/xaur/decred-news/labels/next%20release) to be considered for the next release. [Feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, elian, l1ndseymm, lukebp, matheusd, richardred
- reviews and feedback: Checkmate, davecgh, jazzah, jholdstock, pavel
- title image: saender
