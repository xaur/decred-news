# Decred Journal – June 2020

![abstract art](../img/journal-202006-384.png)

_Image: Ambience at 3000K by @saender_

June's highlights:

- Mobile apps for Android and iOS are upgraded to v1.5.
- Decred's implementation of the new Rosetta standard by Coinbase was released, this will greatly simplify the process of adding DCR support for any merchants/exchanges using Rosetta.
- @richardred published the first results of his on-chain research, also see the Integrations section of the Journal for monitoring of KuCoin's staking activity.
- Decred DEX seems poised for a limited initial release that supports mainnet DEXing.
- There has been an increase in discussion activity on Reddit, and several new Decred-inspired artists have appeared on Twitter.

## Mobile Wallets v1.5 Release

After ~1 year of development, Android and iOS wallets v1.5 are now out on [Google Play](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet) and [Apple Store](https://apps.apple.com/us/app/decred-wallet/id1462247643). Changes include:

- Completely redesigned user interface that conforms to platform style guidelines.
- Support for multiple wallets and watch-only wallets.
- Delayed seed backup confirmation to get up and running quickly.

Congratulations to all contributors!

Please check the full Reddit [announcement](https://www.reddit.com/r/decred/comments/hc5jut/decred_mobile_wallet_v150_has_been_released_for/) and support the [tweet](https://twitter.com/planetdecred/status/1274041667520090112).

## Decred's Rosetta Middleware Implementation

An [implementation](https://community.rosetta-api.org/t/decreds-rosetta-middleware-implementation/79) of the [Rosetta API](https://www.rosetta-api.org/) for Decred was [released](https://twitter.com/decredproject/status/1279127834137636866) in early July, just 2 weeks after Rosetta itself was [released](https://twitter.com/coinbase/status/1273269255610531841) by Coinbase:

> Coinbase initially developed Rosetta as the middleware used to integrate blockchains into its platform securely and painlessly (...)
> 
> For developers of new blockchain projects, the Rosetta interface makes it easier to ensure compatibility with exchanges that use Rosetta, and can dramatically speed up the time it takes exchanges to integrate with new blockchains and protect customer funds by ensuring specific security conditions are met.
> 
> For the broader community of crypto developers, Rosetta makes it easier to build cross-blockchain applications such as block explorers, wallets, and dapps. Instead of writing custom parsing for every supported blockchain, applications can use a blockchain project's Rosetta implementation to read on-chain data and construct transactions in a standard format; minimizing code and simplifying maintenance.

Rosetta features interesting design [principles](https://www.rosetta-api.org/docs/principles_introduction.html), [no gatekeepers](https://www.rosetta-api.org/docs/no_gatekeepers.html) policy, strict security requirements for [wallet](https://www.rosetta-api.org/docs/wallet_api_introduction.html) implementations, [staking](https://www.rosetta-api.org/docs/staking_contract_support.html) support, and a [test suite](https://github.com/coinbase/rosetta-cli) to validate implementations. The first released [SDK](https://www.rosetta-api.org/docs/rosetta_sdk_go.html) is for the Go language as it is heavily [used](https://github.com/coinbase/rosetta-specifications#user-content-sdks-in-more-languages) at Coinbase.

## Development

Unless otherwise noted, the work reported here has the "merged to master" status. It means that the work is completed, reviewed, and integrated into the source code that advanced users can build and run, but is not yet available in release binaries for regular users.

[dcrd](https://github.com/decred/dcrd):

- refactored the [rpcserver](https://github.com/decred/dcrd/pull/2211) package to test it more easily
- fixed [mempool](https://github.com/decred/dcrd/pull/2232) view construction when dealing with disapproved blocks (resolves some issues around transactions on testnet being rejected by the mempool that really shouldn't have been in certain conditions)
- fixed [edge](https://github.com/decred/dcrd/pull/2218) [case](https://github.com/decred/dcrd/pull/2221) crashes of the RPC server with crafted JSON
- [removed](https://github.com/decred/dcrd/pull/2222) Encrypt and Decrypt functions to discourage their use and instead recommend to use modern encryption scheme (e.g. [AEAD ciphers](https://crypto.stackexchange.com/a/27248))

In progress:

- [asynchronous](https://github.com/decred/dcrd/pull/2219) indexing

The majority of the efforts in dcrd for June went into the decentralized Treasury work. The [pull request](https://github.com/decred/dcrd/pull/2170) is undergoing the review process and adding tests to ensure correctness, but it appears to be feature complete. Once it is finished, a [Decred Change Proposal](https://github.com/decred/dcps) will follow.

[dcrwallet](https://github.com/decred/dcrwallet):

- added [methods](https://github.com/decred/dcrwallet/pull/1705) to fetch filters and blocks unrelated to wallet data, which is useful for external callers such as dcrlnd
- avoid [uncommon](https://github.com/decred/dcrwallet/pull/1751) CoinJoin amounts
- [cap](https://github.com/decred/dcrwallet/pull/1759) the amount of outputs produced by downmixing
- bug fixes

[Decrediton](https://github.com/decred/decrediton):

- next part of [CSPP integration](https://github.com/decred/decrediton/pull/2475) implementing safety restrictions for mixed accounts
- unified the [processing](https://github.com/decred/decrediton/pull/2468) of regular and stake transactions
- allow [multiple](https://github.com/decred/decrediton/pull/2491) outstanding LN payments
- new component for [eligible](https://github.com/decred/decrediton/pull/2510) tickets
- a view showing configured [VSPs](https://github.com/decred/decrediton/pull/2482)
- more code [converted](https://github.com/decred/decrediton/pull/2537) to use functional components and CSS modules
- reused more components from pi-ui
- UI tweaks and bug fixes

In progress:

- PoC [integration](https://github.com/decred/decrediton/pull/2516) of the new vspd

[Politeia](https://github.com/decred/politeia):

- better [caching](https://github.com/decred/politeia/pull/1226) of vote results
- [lazy loading](https://github.com/decred/politeia/pull/1219) of comment votes to benefit from the fact that old proposals are rarely accessed
- increased [test coverage](https://github.com/decred/politeia/pull/1203) of the new RFP code
- permanent [logout](https://github.com/decred/politeiagui/pull/1903) feature that deletes user identity and drafts from the browser, this change also removes the use of email as a storage key to have less personal data in browser's local storage
- allow [short URLs](https://github.com/decred/politeiagui/pull/1962) on the UI
- improved [diff viewer](https://github.com/decred/politeiagui/pull/1988) for proposal versions
- [prevent](https://github.com/decred/politeiagui/pull/1966) commenting and proposal submission during the anchoring process
- CMS: viewer for past [versions](https://github.com/decred/politeiagui/pull/1980) of an invoice
- CMS: passthrough requests for [proposal data](https://github.com/decred/politeia/pull/1171) to avoid cross-site requests that cause security issues
- lots of backend and UI bug fixes

In progress:

- TOTP 2FA support
- ability for CMS admins to review [spending](https://github.com/decred/politeiagui/pull/2032) of approved proposals

The [tlog implementation](https://github.com/decred/politeia/pull/1180) in the base politeiad backend is complete. Work on adding the plugins to it is ongoing. Plugin functionality includes comments, comment likes, and proposal votes. The next step will be to load the tlog implementation with existing mainnet data and run performance tests against it. It's possible that some things might need to be reworked if any issues are discovered.

[vspd](https://github.com/decred/vspd):

- [tolerate](https://github.com/decred/vspd/pull/104) dcrwallet connection failures
- reject [unvotable](https://github.com/decred/vspd/pull/93) tickets
- initial [deployment](https://github.com/decred/vspd/pull/95) guide
- [signing](https://github.com/decred/vspd/pull/109) of error responses
- initial [admin page](https://github.com/decred/vspd/pull/119)
- [refreshed](https://github.com/decred/vspd/pull/138) UI look
- multiple changes to improve input validation, error handling, shutdown, etc

The core functionality is complete and developers are in the process of thoroughly testing and shaking out edge cases with mixed/unmixed tickets, with/without the auto-ticket buyer. vspd has been used to vote on tens of thousands of testnet tickets at this point.

[dcrpool](https://github.com/decred/dcrpool):

- The final v1.1 release was [announced](https://twitter.com/dnldd/status/1280455233945194496) on Jul 7 following two release candidates that fixed issues in RC1. Check the full [release notes](https://github.com/decred/dcrpool/releases/tag/v1.1.0) for details.

[dcrdex](https://github.com/decred/dcrdex):

- client command-line commands: [cancel](https://github.com/decred/dcrdex/pull/411) order, [withdraw](https://github.com/decred/dcrdex/pull/422), [logout](https://github.com/decred/dcrdex/pull/423)
- listing [accounts](https://github.com/decred/dcrdex/pull/441) for the server admin
- client browser UI for adding additional DEX [servers](https://github.com/decred/dcrdex/pull/404)
- client browser UI widget to show [balances](https://github.com/decred/dcrdex/pull/454)
- client handling of [trade suspension](https://github.com/decred/dcrdex/pull/269)
- [auto-refund](https://github.com/decred/dcrdex/pull/401) swaps when trade fails
- graceful [shutdown](https://github.com/decred/dcrdex/pull/406) of the swap engine and save/load of its state
- [hide](https://github.com/decred/dcrdex/pull/353) order forms until the registration is complete
- [spec](https://github.com/decred/dcrdex/pull/482) updates to cover trade suspension and admin API
- simnet trading [test](https://github.com/decred/dcrdex/pull/432) harness and some tests
- removed [sleeps](https://github.com/decred/dcrdex/pull/435) from tests to make them more robust
- minimum funding confirmations requirement was [dropped](https://github.com/decred/dcrdex/pull/499) to reduce complexity and improve UX
- multiple trade disruptions [mapped](https://github.com/decred/dcrdex/issues/361) and analyzed

A total of 48 PRs from 8 contributors were [merged](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-06-01..2020-06-30+sort%3Aupdated-asc), adding 11K and deleting 4K lines of code.

In progress:

- trade [resumption](https://github.com/decred/dcrdex/pull/442) handling
- conversion of asset backends to Go [plugins](https://github.com/decred/dcrdex/pull/362)

Addressing concerns about the project timeline, @chappjc noted:

> Mainnet beta will be this summer. Dev plan is to do that by end of Q2 2020, and we are. Also, the client browser interface was barely hinted at in the dev [proposal](https://proposals.decred.org/proposals/417607aaedff2942ff3701cdb4eff76637eca4ed7f7ba816e5c0bd2e971602e1) and we dramatically expanded the scope of the project to make it happen and look good. LTC and generic BTC-clone support wasn't part of the prop, but we got that done too. We also conceived a new epoch matching algorithm based on cryptographic commitments from the clients, the preimages for which are revealed at epoch close, and completely reimplemented it halfway through the project. Not easy or quick, but it's done too and it's a big improvement over the original spec. ([2020-06-01](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15910318461825cyXfI:decred.org))

The team is working on the remaining UX issues and preparing for a limited mainnet deployment in a few weeks.

[dcrandroid](https://github.com/planetdecred/dcrandroid):

- repository moved to the planetdecred organization
- implemented [Espresso](https://github.com/planetdecred/dcrandroid/pull/481) tests and migrated from Travis CI to GitHub Actions

[dcrios](https://github.com/planetdecred/dcrios):

- repository moved to the planetdecred organization
- [Chinese](https://github.com/planetdecred/dcrios/pull/695) translation
- various UI [fixes](https://github.com/planetdecred/dcrios/pull/694)

[godcr](https://github.com/planetdecred/godcr):

godcr is an emerging cross-platform desktop SPV wallet for Decred built with [Gio](https://gioui.org/), an immediate mode GUI toolkit written in Go. This makes the whole application built purely with Go with no web browser or javascript in it, and a much smaller dependency graph (and audit surface) - an important property for software that controls money. As of writing, the compiled binary is ~30 MB.

The project with Gio started in Jan 2020, but before settling on Gio the developers built multiple GUI prototypes (terminal, in-browser, Nucular, Fyne) which are now archived in the [godcr-old](https://github.com/raedahgroup/godcr-old) repository. The work to explore and prototype these approaches began in Sep 2018.

Next steps are releasing a publicly available demo build with basic wallet functionality and integrating the new vspd staking.

[docs](https://github.com/decred/dcrdocs):

- [LN Data Backup](https://docs.decred.org/lightning-network/backups/) page [added](https://github.com/decred/dcrdocs/pull/1106), a must-read for those testing Decred LN to prevent fund loss
- [Contributing](https://docs.decred.org/contributing/overview/) page now lists a few personal [stories](https://github.com/decred/dcrdocs/pull/1101) of becoming a contractor

## People

Welcome to new first time contributors with code merged to master: @svitekpavel ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=svitekpavel)), @Daniel-Leedan ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=Daniel-Leedan)), @shjackson ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=shjackson)).

Congratulations to new contractors granted the Decred Contractor Clearance (DCC): [@ammarooni](https://twitter.com/ammarooni) (Community Management), [@guilhermemntt](https://github.com/guilhermemntt) (development).

Community stats as of Jul 2:

- Twitter followers: 40,517 (+25)
- Reddit subscribers: 9,854 (+62)
- Matrix #general users: 622 (-33) (56 old Slack bots kicked, +23 new users)
- Discord users: 1,288 (+66)
- Telegram users: 2,607 (+4)
- YouTube subscribers: 4,110 (+80), views: 148K (+4K)
- Facebook followers: 3,655 (+23), likes: 3,311 (+20)
- LinkedIn followers: 836 (+26)
- GitHub dcrd stars: 549 (+6), forks: 241 (+1)

## Governance

In June the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 12,629 DCR and spent 8,340 DCR. Using June's daily average DCR/USD rate of $16.05, this is $203K received and $134K spent. At May's average daily rate of $14.11, the USD figure billed for work completed in that month is $118K. As of Jul 1, Treasury balance is 633,820 DCR (9.08 million USD at $14.32).

Six proposals were voted on in June, with 4 approved and 2 rejected, with relatively high turnout for these proposals as compared to some recent proposals. The proposals to be approved were:

- Decred OnChain - A Research and Charting Resource by @Checkmate - 86% approval (38% turnout).
- Decred Latam Marketing and Events Proposal 2 by @elian - 61% approval (41% turnout).
- DCR On-Chain Research: Phase 2 by @PermabullNino - 74% approval (31% turnout).
- Decred Bug Bounty Program: Phase 3 by @degeri - 98% approval (32% turnout). Approval percentage has been going up since [phase 1](https://proposals.decred.org/proposals/d33a2667469b56942adf42453def6cc2292325251e4cf791e806939ea9efc9e1) (90%) and [phase 2](https://proposals.decred.org/proposals/073694ed82d34b2bfff51e35220e8052ad4060899b23bc25791a9383375cae70) (94%).

The [proposal](https://proposals.decred.org/proposals/4affceb07f5b8126366e8b73ed3d164ebc010bc6fefba19375c4c2e2b252beb0) to sponsor a book (CoinStory) for $500 was rejected with 11.6% approval and 34% turnout, while the TV marketing [proposal](https://proposals.decred.org/proposals/9eaafc20f206776e38642e272233390f351c5562c3835369a558cc7d7e341018) had 8% approval and 29% turnout.

Politeia Digest [issue 32](https://blockcommons.red/politeia-digest/issue032/) has further details on all of the above.

A new [proposal](https://proposals.decred.org/proposals/df11d7ac85061e6a02d6503555e585a1a37fffd82101eeea14670537c951926f) from @ivandecredfan for Russian content production was published in June and started voting in July. @ivandecredfan submitted a similar [proposal](https://proposals.decred.org/proposals/92e3f2176b332c1aea5887acd2324c2cd730ec450e563df52ddae9d5927d5d36) in Feb which was rejected with 21% approval, but continued with his video production and took some feedback from comments on the first proposal on board.

A proposal has been submitted which suggests choosing a new name for the project ("Bitcoin Evolution"). The Politeia admins indicated that the proposal owner (@decredinator) should add a budget and implementation plan before the proposal would be considered valid for publication on the proposals site. @decredinator [posted](https://www.reddit.com/r/decred/comments/hh2ult/a_better_name_for_decred_to_broaden_the_reach_of/) the proposal to Reddit so that the community can read it and contribute to making it a reality. Most of the comments are not keen on the idea and the author did not reply to any of them. @decredinator has also been [called out](https://www.reddit.com/r/decred/comments/hh2ult/a_better_name_for_decred_to_broaden_the_reach_of/fwbfmst/) for spamming the link to this post across a range of unrelated tweets.

To get notified when new proposals are published or go to vote you can follow [@pi_crumbs](https://twitter.com/pi_crumbs) on Twitter, or set up email notifications on the proposals site.

## Network

Hashrate: [June's hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kavllavw-kc326nyn&scale=linear&bin=block&axis=time) opened at ~390 Ph/s and closed ~412 Ph/s, bottoming at 280 Ph/s and peaking at 569 Ph/s throughout the month. Pool [hashrate distribution](https://dcrstats.com/pow) as of Jul 1 (approximate): UUPool 36%, Poolin 32%, lab.antpool.com 11%, BTC.com 3.4%, Luxor 1.07%, F2Pool 0.86%, BeePool 0.09%, CoinMine 0.04%, Suprnova 0.02% and others ~15%.

Staking: [30-day average](https://dcrstats.com/) ticket price was 139.4 DCR (-2.1). The [price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kavllavw-kc326nyn&axis=time&visibility=true-false&mode=stepped) varied between 135.1-149.8 DCR. [Locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kavllavw-kc326nyn&scale=linear&bin=block&axis=time) was 5.63-5.86 million DCR, which corresponded to 48.7-50.6% of the available supply [participating](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kavllavw-kc326nyn&scale=linear&bin=block&axis=time) in PoS.

An unusual spike of block size usage (unrelated to large Treasury payout transactions) occurred on May 29-31. Dozens of nearly full [blocks](https://explorer.dcrdata.org/blocks?height=453840&rows=50) were mined with 90-100 KB transactions which consolidated lots of tiny outputs into 6 DCR outputs. On May 31 the blockchain grew by a [record](https://explorer.dcrdata.org/charts?chart=block-size&bin=day&axis=time) 13 MB, compared to an average growth of 4 MB/day. It [looks like](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15913552414776FisdN:decred.org) a VSP was consolidating ticket fees. Many of the 6 DCR outputs were later [merged](https://explorer.dcrdata.org/tx/ef562befa1f8eeee6250d98b6ccb1722b8fba508dd4919d5b85139df9c761e0c) into a balance of ~240K DCR (~3.4M USD, ~2% supply), known to be associated with a popular cryptocurrency exchange. tl;dr a VSP operator sent about 200 DCR (voting fees paid by users of the VSP) to an exchange, it used a lot of block space because it involved thousands of tiny fee payments associated with individual tickets processed by that VSP.

Nodes: Throughout [June](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1590969600000&to=1593561600000) there was an average of 126 public listening nodes and 208 total nodes per dcr.farm. Average version distribution for June: 50% dcrd v1.5.1, 9.5% dcrd v1.5.0, 5.6% dcrd v1.6.0 dev builds, 3.2% dcrd v1.5.0 dev builds, 1.8% dcrd v1.4.0, 9.5% dcrwallet v1.5.1, 1% dcrwallet v1.5.0, 0.9% dcrwallet v1.4.0, and 18.7% others.

@Checkmate posted a [chart](https://twitter.com/_Checkmatey_/status/1269825167133306881) that shows an increase in on-chain DCR volume.

@PermabullNino [tweeted](https://twitter.com/PermabullNino/status/1278055245050855424) updated Mining Pulse, Difficulty Ribbons, ticket inflows, and Strong Hand charts. A bit earlier he [shared](https://twitter.com/PermabullNino/status/1272512290814902275) the Staking Momentum chart.

@richardred published [part 1](https://blockcommons.red/post/dcr-on-chain-1/) in a series about analyzing Decred's blockchain data, highlights including:

- 465K of the 840K [founders premine](https://docs.decred.org/advanced/premine/#bring-up-costs) remains untouched
- 290K of the 840K [airdrop](https://docs.decred.org/advanced/premine/#airdrop) coins did not move as well
- ~27% of the 345K DCR paid by the Treasury to contractors was not touched since the contractor received it, ~24% was staked, ~24% ended up in a known exchange address, ~1.7% was mixed
- out of ~5.8M DCR PoW rewards, 60% ended up on addresses associated with exchanges, 10% has been staked, and the rest is unspent (6%) or has unknown outcome (24%)

The same kind of analysis was repeated with fresh data and formatting improvements for [issue 27](https://ournetwork.substack.com/p/our-network-issue-27) of Our Network newsletter.

## Integrations

DecredVoting VSP [announced](https://www.reddit.com/r/decred/comments/hbofz4/tired_of_keeping_track_of_your_staking_activities/) a new tickets analytics dashboard which shows users' stats about their tickets, including some specific stats for split tickets which are devised by @decreddave himself and not available elsewhere.

Hotbit [announced](https://hotbit.zendesk.com/hc/en-us/articles/360049302534-Hotbit-s-Announcement-Regarding-the-Launch-of-DCR-Investment-Product-and-Current-Deposit-Investment-Plan-on-June-11th-2020-UTC-8-) a Decred investment product on Jun 11, with an annualized return of 4.27% and "redemption period being (T+30)". There is a minimum purchase of 100 DCR and it seems like the "minimum unit for the calculation of interests of current deposit investment plan will be 1 DCR", whatever that means.

Following KuCoin's [launch](https://www.kucoin.com/news/en-decred-soft-staking-official-rules) of a custodial staking service in March 2020, @richardred has investigated staking activity associated with KuCoin-related addresses. Observations suggest that up until the end of Jun 2020 KuCoin has bought 213 tickets, and 185 of them have voted. The earliest tickets bought by addresses thought to be controlled by KuCoin were bought in December 2019, several months before the service was announced in Feb, and customers were automatically opted in within 48 hours of that announcement. All of these tickets have abstained in the on chain agenda voting, and none of them have voted on Politeia proposals - KuCoin is not participating in decision-making with their tickets. According to reports user DCR balances appear to have earned ~0.45% additional DCR from this staking, considering about one quarter has passed this would put it on course for an annual rate of about ~1.8%, which is considerably lower than the rate which is projected for sovereign staking by [dcrdata](https://explorer.dcrdata.org/) (~6% as of writing).

Payment processor [CoinPayments](https://www.coinpayments.net/) delisted 37 assets including DCR following a [warning](https://twitter.com/CoinPaymentsNET/status/1264645627750649856) in May. After some of its users [complained](https://twitter.com/CryptoEmporium_/status/1268860197038166016) about this, they tweeted that it was due to [low volume](https://twitter.com/CoinPaymentsNET/status/1268925474052268032).

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

@Checkmate took the lead on Reddit and started focused and structured discussions to improve Decred's outreach. The first post was to explore ideas for a grassroots marketing campaign/strategy and connect with people willing to help execute it. One of the outcomes is the [#DidYouKnowDecred](https://twitter.com/hashtag/DidYouKnowDecred) Twitter hashtag campaign. That was followed by two Skepticism Sunday and two Forward Thinking Friday threads designed to analyze weaknesses and solutions to them, as well as ideas to push Decred further. In total, they collected 155 comments and were some of the most active posts this month.

The second Latam Marketing and Events [proposal](https://proposals.decred.org/proposals/3c02b677462d6d22d61bf786798e975b38df7a203c2467429d4ec91f75ef0c40) passed, but it barely crossed the approval threshold of 60% in the last hours of voting. To address nearly 40% of No votes, @elian started a Reddit [survey](https://www.reddit.com/r/decred/comments/gzw6hl/what_are_the_thoughts_of_the_394/) calling for any feedback to learn what is missing and what can be improved.

In early July Decred Latam published an activity [report](https://www.reddit.com/r/decred/comments/hn4sve/activities_report_decred_en_espa%C3%B1ol_proposal_2/) for the first month of their new proposal.

Monde PR's achievements for June:

- created and pitched two story ideas to finance, entrepreneur and tech publications
- secured two email Q&As with crypto publications

News coverage secured by Monde PR:

- an article in [Cointelegraph](https://cointelegraph.com/news/bitcoin-still-faces-on-chain-scaling-trouble-ahead-decred-co-founder-says) featuring commentary by @jy-p on Bitcoin scaling, syndicated to 8 news outlets
- an article in [Cointelegraph](https://cointelegraph.com/news/decred-co-founder-cbdcs-can-facilitate-crony-capitalism) featuring commentary by @jy-p on the emergence of CBDCs, syndicated to 7 news outlets
- an article in [Cointelegraph](https://cointelegraph.com/news/decred-co-founder-calls-paypal-and-crypto-an-odd-combination) featuring commentary by @jy-p on rumors of PayPal accepting cryptocurrencies, syndicated to 19 news outlets. It was also included as a top story in Holder's Digest in [Cointelegraph](https://cointelegraph.com/news/paypal-crypto-rumors-rip-wirecard-telegram-settles-hodlers-digest-june-2228), syndicated to 5 news outlets

A spreadsheet of all media coverage secured by Monde PR since February 2020 was [published](https://github.com/decredcommunity/pr/blob/release/monde-pr-media-coverage.csv) on GitHub.

## Events

Attended:

- Jun 11 - [Decred Virtual Meetup](https://www.meetup.com/Decred-Australia/events/271159615/) - Internet. Organized by @DecredAustralia, this was a second installment of @Checkmate's on-chain analysis for BTC and DCR. ([video](https://www.youtube.com/watch?v=HbquQIv9EYw))
- Jun 25 - [Criptotips con Lorena](https://twitter.com/bitcoinemb/status/1276289966440681473) - Internet. @elian talked about crypto scams in this event hosted by Bitcoin Embassy Bar (Mexico City). ([video](https://www.youtube.com/watch?v=Bxdxzs6Bgpw))
- Jun 25 - [Hablemos Decred 6](https://twitter.com/Decred_ES/status/1275164449448607748) - Internet. @pablito gave an introduction into Git and GitHub in Spanish as part of the strategy by the Latam team to create developer-oriented content. ([video](https://www.youtube.com/watch?v=4b0xYYk6xlY))
- Jun 30 - [Decred Webinar](https://www.meetup.com/BlockchainMelbourne/events/271516517/) - Internet. @eSizeDave, @richardred, @elian, @mrbulb and @degeri discussed "Sociology, The Future of Work and Incentive Alignment" together with Ellie Rennie and Dr Julian Waters-Lynch from RMIT University. Organized by Decred Australia. ([video](https://www.youtube.com/watch?v=1dcHwap7xHQ))

Upcoming:

- Jul 11 - [Campus Party](https://brasil.campus-party.org/) - Internet. Brazilian Decred community will have 3 speakers. Rafaela Romano will talk about decentralization in cryptocurrencies on the Living Better stage with the title "Monetization via Blockchain". Two other speakers will be confirmed closer to the event.

## Media

Selected articles:

- Decred blockchain analysis part 1 by @richardred ([blog.decred.org](https://blog.decred.org/2020/06/08/Decred-blockchain-analysis-Part-1/))
- Decred On-chain: Realised cap, MVRV ratio and gradient oscillators by @Checkmate ([medium](https://medium.com/decred/decred-on-chain-realised-cap-mvrv-ratio-and-gradient-oscillators-a36ed2cc8182))
- Why we need Decred: An inclusive approach to sound money by @ammarooni ([medium](https://medium.com/@Ammarooni/why-we-need-decred-an-inclusive-approach-to-sound-money-db2f990c107b))
- The Decred node or: How I learned to stop worrying and love the command line by @kozel ([part one](https://medium.com/@artikozel/the-decred-node-or-how-i-learned-to-stop-worrying-and-love-the-command-line-part-one-1eca9420a1b2), [part two](https://medium.com/@artikozel/the-decred-node-or-how-i-learned-to-stop-worrying-and-love-the-command-line-part-two-e629b8579ce2))
- BTC, ETH and DCR are part of the largest economic and technological revolution of our generation by Fernando Quirós (in Spanish, [es.cointelegraph.com](https://es.cointelegraph.com/news/elian-huesca-btc-eth-and-decred-are-part-of-the-greatest-technological-and-economic-revolution-of-our-generation)) - interview with @elian

Translations:

- A More Private Way to Stake - [in Arabic](https://insaf01.github.io/decred-arabic/articles/a-more-private-way-to-stake.html) by @arij and [in Spanish](https://medium.com/decred-es/una-forma-m%C3%A1s-privada-de-hacer-staking-en-dcr-36785ad54a47) by @francov\_.
- [Decred Spanish](https://medium.com/decred-es) Medium gained a full month of [Decred Drive](https://medium.com/decred-es/decred-drive-spanish/home) by @francov\_ and a new [Politeia Digest](https://medium.com/decred-es/politeia-digest-spanish/home) issue by @pablito.
- @ivandecredfan translated [5 articles](https://medium.com/@ivandecredfan) and [3 videos](https://www.youtube.com/channel/UCFjXbEDeyhhj2bH2t_eGKGA/videos) to Russian.
- Decred full node & Tor setup tutorial on the Raspberry Pi \[2020\] transcript - [in Chinese](https://github.com/DominicTing/decred-ZH-translations/blob/master/%E6%A0%91%E8%8E%93%E6%B4%BE%E8%BE%85%E5%8A%A9%E5%AE%89%E8%A3%85%E8%84%9A%E6%9C%AC.md) by @Dominic.
- Decred Journal May 2020 was translated to Arabic (@arij), Chinese (@Dominic), and Spanish (@francov\_). Thank you everyone for [translating](https://xaur.github.io/decred-news/) DJ for so many months!

Videos:

- The @Bitcoin account tweeted a video featuring quotes about the Federal Reserve's infinite capacity to print money with memetic embellishments from @Exitus, including a cheeky mention of Decentralized Credits at the end. The tweet was well received, with 41K views, ~900 likes, and ~300 retweets. ([twitter](https://twitter.com/Bitcoin/status/1269313539056922624))
- Decred was mentioned in the Good Morning Crypto show by Ivan on Tech ([youtube](https://www.youtube.com/watch?v=JZhl2Atm4VI&t=42m50s), at 42:50). The video has 24K views. Thanks to Steve de boo for dropping the question in the livestream chat - a good example of high-precision outreach work!
- Stakey awakens animation ([youtube](https://www.youtube.com/watch?v=LHgGyoDcFPI))
- Decred bi-weekly news updates for [June 10](https://www.youtube.com/watch?v=INKSkBpCT_0) and [June 23](https://www.youtube.com/watch?v=4GqdgsgUX7c) by @Exitus
- Decred full node & Tor setup tutorial on the Raspberry Pi \[2020\] by @Exitus ([youtube](https://www.youtube.com/watch?v=B-5O_GBcbV0))
- Decred Society channel by Phoenix Green added 7 new videos on the [crypto society](https://www.youtube.com/watch?v=zM4dfmPYXfo), [21 million](https://www.youtube.com/watch?v=yhEAXTJHr3o) crypto market, why 21 million coins is [enough by design](https://www.youtube.com/watch?v=0b241mW8Yto), the divisive nature of [forks](https://www.youtube.com/watch?v=PZ4aAgz2JcM), the experience of peer to peer [payments](https://www.youtube.com/watch?v=0VjKIHCXD50), [treasury](https://www.youtube.com/watch?v=-1zmojjvGtg) and self-funded future, and getting a [strategy](https://www.youtube.com/watch?v=R1F_GVj76Qw) to not get wrecked.
- Decred Australia Virtual Meetup #2 feat. on-chain analyst Checkmate ([youtube](https://www.youtube.com/watch?v=HbquQIv9EYw))

> The only thing holding Decred back in my honest opinion is more people coming up with creative ways to shout about it. It is all this thing needs. Because once you get the level of attention, the fundamentals just speak for themselves.

Decred videos are now also posted [on BitChute](https://www.bitchute.com/channel/decred/) as a fallback in case anything happens to the YouTube channel. This is good timing since as expected earlier, YouTube [removed](https://cointelegraph.com/news/youtubes-algorithm-is-punishing-crypto-content-and-no-one-knows-why) a bunch of crypto videos during the COVID-19 wrongthink cleanup.

Audio:

- Decred in Depth 26 - DCR use cases and growth with @Checkmate, @akinsawyerr and @mrbulb ([libsyn](https://decredindepth.libsyn.com/akin-checkmate-mr-bulb-dcr-use-case-growth))
- Decred in Depth 27 - Theft by another name with @jy-p ([libsyn](https://decredindepth.libsyn.com/jake-yocom-piatt-theft-by-another-name))
- Rough Consensus 7 - The rigged game ([libsyn](https://roughconsensus.libsyn.com/episode-7-the-rigged-game)) - @mr.black, @Checkmate and @PermabullNino discuss the current state of the global union with the rise of social unrest, the stock market's v-shape recovery, and the rigged game that ties the two together
- Rough Consensus 8 - Talking macro with Ammar ([libsyn](https://roughconsensus.libsyn.com/episode-8-talking-macro-with-ammar)) - Ammar joins the spidey squad to discuss inflation, deflation, crypto bull theses, investing, and the strings that tie all of these pieces together
- Zach Segal (Head of Listings at Coinbase) mentioned Decred as an interesting project in Trading Places podcast ([spotify](https://open.spotify.com/episode/7BkEEDgSDPU1XQsmveksgv), short [clip](https://www.youtube.com/watch?v=IDGQsWE3eeg), _missed in May_)

There has been an uptick in Decred-related [artwork](https://twitter.com/_Checkmatey_/status/1278972757796159489) published this month. @OfficialCryptos impressed the folk with a [Decred Dargon](https://twitter.com/OfficialCryptos/status/1273926304027508738) (which might be the [armored lizard](https://www.youtube.com/watch?v=XkvcdjSH0c0&t=50m24s) mentioned by Murad on the podcast), [unicorn](https://twitter.com/OfficialCryptos/status/1275426618610196480) and btcsuite [drilling rig](https://twitter.com/OfficialCryptos/status/1275507751511371780). @aithzakaria1 posted a [digital city](https://twitter.com/aithzakaria1/status/1277109552857710592), a [shuttle](https://twitter.com/aithzakaria1/status/1277472194256347137) and a other images on his Twitter. @AGNFAB [announced](https://twitter.com/AGNFAB1/status/1271157067097792514) that some of his artwork will be exclusively available on [decentralizedboutique.com](https://decentralizedboutique.com/?product_cat=art), a new store selling crypto related jewellery and artwork [for crypto](https://decentralizedboutique.com/?page_id=150) (including DCR).

## Community Discussions

Comm systems news:

- Decred's [Discord server](https://discord.gg/GJ2GXfz) has been restructured and channels have been grouped into 3 categories: Discord-only channels for a more casual experience compared to Matrix (where many rooms are virtual offices to coordinate work), read-only channels bridged to Matrix (as a balance between transparency and productivity in Matrix rooms), and two-way bridged rooms #decred-101, #proposals, #support, #ticket-splitting, and #trading.
- A new [DecredSupport](https://t.me/DecredSupport) channel was created on Telegram and bridged to Matrix #support room.
- Matrix devs [released](https://matrix.org/blog/2020/06/02/introducing-p-2-p-matrix/) an updated version of the peer-to-peer client prototype that allows users to take more control of their data.

Selected Reddit posts:

- The most discussed [post](https://www.reddit.com/r/decred/comments/hbb3iz/decred_grassroots_marketing_campaign/) of the month (and for some time) came from @Checkmate, summarizing a number of grassroots marketing initiatives for discussion and to recruit participants.
- Forward Thinking Friday [Jun 18](https://www.reddit.com/r/decred/comments/hbp6y4/forward_thinking_friday_1_moving_the_peg_forwards/) (moving the peg forward) and [Jun 26](https://www.reddit.com/r/decred/comments/hg2a9k/forward_thinking_friday_decred_narratives_26_june/) (Decred narratives).
- Skepticism Sunday [Jun 21](https://www.reddit.com/r/decred/comments/hd4mwv/decred_skepticism_sunday_21_june_2020/) and [Jun 28](https://www.reddit.com/r/decred/comments/hh7lo2/decred_skepticism_sunday_28_june_2020/).
- u/g687 [posted](https://www.reddit.com/r/decred/comments/hghw3a/why_people_do_not_care_about_decred/) analysis of how many times the names of a different project are mentioned by comments in a variety of subreddits, remarking that Decred was mentioned relatively little on subreddits other than r/decred. This provoked 36 comments in response, including a high scoring [one](https://www.reddit.com/r/decred/comments/hghw3a/why_people_do_not_care_about_decred/fw4u90p) from @jy-p which set out some possible reasons for a lack of mentions. It was also pointed out that the other projects included in the comparison had much larger market caps.
- The idea to [sponsor](https://www.reddit.com/r/decred/comments/hcfkei/draft_decred_cypherpunk_prize/) research and software that plays an important role in Decred received mixed responses, in part due to the lack of details and people willing to execute it.
- u/OpenWithRuiLopez noticed that Coinbase has [acquired](https://www.reddit.com/r/decred/comments/guri3s/coinbase_acquires_tagomi_tagomi_lists_decred/) institutional crypto brokerage platform Tagomi, which trades DCR as one of its 14 assets.

Selected Twitter discussions:

- @moo31337 [dropped](https://twitter.com/marco_peereboom/status/1271200577272385538) a teaser bomb about his next proposal.
- @Doctor\_Bitcoin\_ [compared](https://twitter.com/Doctor_Bitcoin_/status/1277352638502375424) Decred to a virtual continent that anyone can join.
- @Checkmate created a new [#DecredChallenge](https://twitter.com/_Checkmatey_/status/1272680543612628997) where you need to guess which metric is shown on the chart.
- @Frenchy\_DCR [revealed](https://twitter.com/Frenchy_DCR/status/1273811301844709387) why DCR is not popular.
- After multiple charts with technical analysis @Mattgetsbarrel1 found an ultimate [strategy](https://twitter.com/Mattgetsbarrel1/status/1274072597597024257) to trade DCR.

![photo](../img/pl-mountains-360.jpg "@LolekBolek74 enjoying DCR in Polish mountains")

_Image: @LolekBolek74 enjoying DCR in Polish [mountains](https://twitter.com/LolekBolek74/status/1269333625352396800)_

## Markets

In June DCR was trading between USD 14.01-18.76 / BTC 0.0015-0.0019. The average daily rate was $16.05.

In his latest [post](https://medium.com/decred/decred-on-chain-realised-cap-mvrv-ratio-and-gradient-oscillators-a36ed2cc8182) @Checkmate analyzed how realized cap, MVRV ratio and gradient oscillators apply to Decred. Realized cap tends to act as support or resistance level for both Decred and Bitcoin, but for Decred it is more closely related to market cap, because coins are repriced much more often.

> The Decred realised cap captures an important psychological level in that it represents the aggregate price where the market last interacted with their coins, capturing a sort of 'recency bias'. People who regularly interact with their DCR holdings via tickets, CoinShuffle++ mixes or governance votes are likely to have heightened awareness of coin price. Therefore, the opportunity cost of realising profits or losses on their DCR is baked into each transaction. The explicit decision to buy a ticket over sending coins to an exchange for sale is a reflection of meaningfully bullish sentiment for each individual, and vice-versa.

Another market-related [analysis](https://twitter.com/_Checkmatey_/status/1267945637980463104) from @Checkmate noted bullish RSI divergence vs both DCR and USD and charted the price against on-chain indicators.

@PermabullNino charted how DCR market cap is testing the [realized cap](https://twitter.com/PermabullNino/status/1268181399879790592) and a possible correlation between historical instances of huge ticket pool [outflows](https://twitter.com/PermabullNino/status/1268270041759432704) with market downtrends.

## Relevant External

There has been some controversy about a [bug](https://medium.com/blockstream/patching-the-liquid-timelock-issue-b4b2f5f9a973) with Blockstream's Liquid service whereby the "emergency backup keys" held by Blockstream were repeatedly taking custody of funds in a way that should only have happened in an emergency. The controversy is largely around how the disclosure of the bug has been handled, with James Prestwich (who discovered it) not [impressed](https://twitter.com/_prestwich/status/1277090512126660608) by the way its severity has been downplayed by Blockstream. This [comment](https://www.reddit.com/r/CryptoCurrency/comments/hhwwcb/vulnerability_discovered_in_liquid_allowing/fwdqbxc/) on r/cryptocurrency has a good timeline, including an observation that the story was not being covered on r/bitcoin.

Reddit have opened a [call](https://www.reddit.com/r/ethereum/comments/hbjx25/the_great_reddit_scaling_bakeoff/) for ideas about how they might scale the recently launched points system (currently running on Ethereum's Rinkeby testnet) to the whole platform.

The cost of transactions on Ethereum has [increased by 500%](https://www.coindesk.com/ethereum-developers-consider-new-fee-model-as-gas-costs-climb) since April and developers are looking at ways to bring this down, including an EIP (1559) which would see users pay a "base fee" to the network plus a tip to miners when making transactions.

One Ethereum user has been paying [particularly](https://www.coindesk.com/whale-sent-130-ether-transaction-fee) high fees this month, with two separate transactions each paying $2.6 million worth of ETH as a transaction fee to miners, for a transfer of a small amount of ETH (~$100). Speculation about the cause of the high fees included mistakes and [blackmail](https://twitter.com/VitalikButerin/status/1271463564440678401) attempts. Adding to the mystery, the pool which mined one of the transactions appeared to [offer](https://twitter.com/sparkpool_eth/status/1270688700968480768) to return some of the fee, but nobody came forward.

A [bug](https://cointelegraph.com/news/bancors-bug-exposes-dangerously-common-practice-in-ethereum-defi) with the Bancor smart contracts was detected which would have allowed attackers to drain the funds of anyone who interacted with it, so "Bancor acted preemptively to 'steal' user funds before malicious parties could intervene". The severity of the problem was compounded by the use of "infinite approvals", which save on transaction fees and offer a better UX, but expose users to much more risk (in this case the potential attacker could get all of the depositor's tokens, not just the amount they chose to deposit). Use of infinite approvals is common to many DeFi apps.

USDT supply has [surpassed](https://bitcoinexchangeguide.com/tether-usdt-surpasses-10-billion-in-market-capitalization/) $10 billion, up from ~$5 billion this year.

[CoinGecko](https://www.coingecko.com/) partnered with Hacken to add [cybersecurity](https://cointelegraph.com/news/coingecko-adds-crypto-exchanges-cybersecurity-ratings-to-trust-score) ratings for exchanges listed on the site (see Trust Score tab).

Chainalysis [announced](https://cointelegraph.com/news/chainalysis-can-now-track-your-privacy-coins-zcash-dash) the support of Zcash and Dash privacy coins in their products. The vast majority of transactions in these networks can be traced because privacy features are used by very few people. This comes after the May's news of several exchanges [delisting](https://cointelegraph.com/news/another-exchange-delists-monero-amidst-ongoing-sex-scandal) Monero because it is better at protecting users' privacy, and researchers from Carnegie Mellon University [claiming](https://cointelegraph.com/news/researchers-claim-999-of-zcash-transactions-are-traceable) that 99%+ of Zcash transactions are traceable and that inputs of Monero transactions can be revealed with accuracy of 30% (full [article](https://eprint.iacr.org/2020/593.pdf)).

## Submit Your Story for Next DJ

As Decred and wider cryptocurrency ecosystems are expanding it becomes hard to track all important events. You can help DJ to capture more relevant stories by submitting them on GitHub. To do that, open [GitHub issues](https://github.com/xaur/decred-news/issues), find one for the [next release](https://github.com/xaur/decred-news/labels/next%20release) (e.g. "DJ July 2020") and comment with a link and a short description for the story.

## About This Issue

This is issue 27 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, richardred
- reviews and feedback: chappjc, davecgh, jholdstock, jz, lukebp, raedah
- title image: saender
