# Decred Journal – December 2020

![abstract art](../img/journal-202012-384.png)

_Image: Restructuring III by @saender_

Happy New Year everyone!

December highlights:

- After another month of polishing, v1.6 is looking very shiny indeed. Stand by for Release Candidate 5.
- On chain metrics went wild in December, including a big jump for the ticket price to 191 DCR.
- Social media metrics are also taking off, with @decredproject breaking through a key resistance level.
- DCR was delisted from Upbit, causing the price to spike, and margin trading was added to several other exchanges.

## Development

Unless otherwise noted, the work reported here has the "merged to master" status. It means that the work is completed, reviewed, and integrated into the source code that advanced users can build and run, but is not yet available in release binaries for regular users.

**[dcrd](https://github.com/decred/dcrd)**

Merged in master and backported to v1.6 release:

- corrected [fee calculations](https://github.com/decred/dcrd/pull/2530) to fix some transactions being considered lower priority in some reorg scenarios
- whitelisted DCP-5 [violations](https://github.com/decred/dcrd/pull/2533). Due to a bug that has since been fixed, 5 blocks were accepted with an old block version 6 when the majority of the network had already upgraded to version 7. The blocks were otherwise valid and are now whitelisted to allow fully syncing the chain without checkpoints.

Merged in master:

- moved [context checks](https://github.com/decred/dcrd/pull/2481) from sanity/positional functions to proper locations to restore the intended restrictions that were in place before the decentralized treasury work. These will be necessary to decouple block processing order from download order.
- changed main chain [block cache](https://github.com/decred/dcrd/pull/2488) semantics to be less dependent on the order the block data is seen
- extracted block manager into its own [`netsync`](https://github.com/decred/dcrd/pull/2500) package to improve its testability and more cleanly split syncing with the network from consensus validation
- several other changes towards [multi-peer](https://github.com/decred/dcrd/issues/1145) block downloading
- added mining [test harness](https://github.com/decred/dcrd/pull/2480) that will make it easier to add test coverage and help to optimize block template generation code
- changed RPC server [authentication](https://github.com/decred/dcrd/pull/2486) to use HMAC-SHA256 with random key unique to each startup to harden against certain classes of memory dumping attacks
- more [rpcserver](https://github.com/decred/dcrd/issues/2069) test coverage
- multiple places updated to follow error handling [best practices](https://github.com/decred/dcrd/issues/2181)
- smaller code and test updates across the board

A total of 51 PRs and 92 commits from 6 contributors were [merged](https://github.com/decred/dcrd/pulls?q=is%3Apr+merged%3A2020-12-01..2020-12-31+sort%3Aupdated-asc), adding 10K and deleting 8K lines of code.

In other news, there have been commits on Dec 30 and Jan 1 but thankfully none on Dec 31!

**[dcrwallet](https://github.com/decred/dcrwallet)**

- [random coin](https://github.com/decred/dcrwallet/pull/1937) selection for paying VSP fees (this also enables to retry and complete some VSP ticket purchases that were always failing before)
- fixed [unpublished](https://github.com/decred/dcrwallet/pull/1941) outputs being used for funding other transactions (occurred with VSP fees that stay in unpublished state until the ticket is submitted with the VSP)
- code refactoring

In progress:

- ability to [import](https://github.com/decred/dcrwallet/pull/1945) voting accounts derived from a different seed (to support Trezor staking)

**[Decrediton](https://github.com/decred/decrediton)**

- added button to mix [all funds](https://github.com/decred/decrediton/pull/3041)
- added 1.6 [release notes](https://github.com/decred/decrediton/pull/3048) and animated images
- updated translations (Arabic, Chinese, German, Japanese, Italian, Polish, Spanish)
- ~23 fixes and UI tweaks

There will very likely be an RC5 soon fixing a few remaining issues.

**[Politeia](https://github.com/decred/politeia)**

- removed [CSRF](https://github.com/decred/politeia/pull/1356) on public routes to prevent the possibility to link trickled votes by the CSRF token. The privacy impact was minimal: linking CSRF tokens to trickled votes would require writing additional code, since it is not done automatically by the CSRF library used.
- end-to-end UI tests for proposal [editing](https://github.com/decred/politeiagui/pull/2227)
- removed annoying Logout modal and moved the rarely used "Logout permanently" function to Account tab
- new `politeiavoter` command to [verify](https://github.com/decred/politeia/pull/1355) votes
- UX improvements for CMS invoice handling and review
- Politeia and CMS bug fixes

tlog integration update from @lukebp:

> The ability to retrieve the full timestamp (inclusion proof) for any piece of user submitted data has been added. Frontend work for this is still ongoing. The backend tlog branch is now feature complete and we'll be starting the code review process.

**[vspd](https://github.com/decred/vspd)**

- reject reused or old [timestamps](https://github.com/decred/vspd/pull/215)
- more test coverage for database code
- smaller fixes and preparations for v1.0 release

**[dcrpool](https://github.com/decred/dcrpool)**

- [single miner](https://github.com/decred/dcrpool/pull/274) endpoint
- save [client info](https://github.com/decred/dcrpool/pull/293) in the database and make it available on any dcrpool instance
- support for NiceHash pool [validator](https://github.com/decred/dcrpool/pull/294) (allows it to connect to dcrpool and query basic stats)

**[dcrdex](https://github.com/decred/dcrdex)**

- new [max order](https://github.com/decred/dcrdex/pull/842) button that populates quantity fields with the maximum amount possible based on market, market side and wallet balance
- public [market data](https://github.com/decred/dcrdex/pull/796) API endpoints via HTTP and WebSockets
- show [account ID](https://github.com/decred/dcrdex/pull/825) for each DEX server
- favor [confirmed](https://github.com/decred/dcrdex/pull/865) outputs for funding BTC orders
- [resume](https://github.com/decred/dcrdex/pull/856) swapper from the database (better than the previous approach and less code)
- allow apps to listen on [IPv6](https://github.com/decred/dcrdex/pull/899) addresses
- improve colors to differentiate between buy and sell orders
- many bug fixes and dependency upgrades

A total of 28 PRs from 7 contributors were [merged](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-12-01..2020-12-31+sort%3Aupdated-asc), adding 8K and deleting 5K lines of code.

Patch release [v0.1.4](https://github.com/decred/dcrdex/milestone/10) is getting close.

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

- notification when cfilters are [fetched](https://github.com/planetdecred/dcrandroid/pull/523)
- bug fixes

Merged in dcrlibwallet shared library:

- [vspd](https://github.com/planetdecred/dcrlibwallet/pull/163) support
- method to query information about connected SPV [peers](https://github.com/planetdecred/dcrlibwallet/pull/160)
- dependency upgrades and bug fixes

Note that features added to dcrlibwallet become available for consumption by dcrandroid, dcrios and godcr, assuming these apps add necessary UI.

**[dcrios](https://github.com/planetdecred/dcrios)**

- [automated](https://github.com/planetdecred/dcrios/pull/707) UI tests for some scenarios using XCUI

**[godcr](https://github.com/planetdecred/godcr)**

- [coin selection](https://github.com/planetdecred/godcr/pull/261) interface
- [notifications](https://github.com/planetdecred/godcr/pull/274) when text is copied or transaction is created
- new UI design for main [Wallets](https://github.com/planetdecred/godcr/pull/276) page
- UI tweaks
- bug fixes and optimizations

API for overlaying widgets is required to fully implement the intended designs for godcr. This was brought to the attention of the Gio team on their Slack and is being treated as a priority.

**[tinydecred](https://github.com/decred/tinydecred)**

In progress:

- script to [recover](https://github.com/decred/tinydecred/pull/194) funds from old Copay web wallets (one was previously at wallet.decred.org). The script has already helped to recover someone's mainnet funds.

**[dcrros](https://github.com/decred/dcrros)**

- [offline mode](https://github.com/decred/dcrros/pull/14) support to fully fulfill the specs for the [Construction API](https://www.rosetta-api.org/docs/construction_api_introduction.html), where certain operations are only performed in offline instances

**[decred.org](https://github.com/decred/dcrweb)**

- removed [inactive](https://github.com/decred/dcrweb/pull/935) contributors
- dependency upgrades

Other:

- researchers from Electric Capital have mapped most [repositories](https://www.reddit.com/r/decred/comments/k9g76v/decred_developer_ecosystem_repositories/) in the Decred ecosystem and built a tool to visualize their activity

## People

Welcome to new first time contributors with code merged to master: @piotrdelikat ([decrediton](https://github.com/decred/decrediton/commits?author=piotrdelikat))!

Community stats as of Jan 2:

- Twitter followers: 41,320 (+423)
- Reddit subscribers: 10,051 (+69)
- Matrix #general users: 287 (+34)
- Discord users: 1,723 (+222)
- Telegram users: 2,338 (-1)
- YouTube subscribers: 4,300 (+50), views: 165K (+3K)
- LinkedIn followers: 944 (+12)
- GitHub dcrd stars: 570 (+3), forks: 247 (+1)

A few highlights from the stats we [track](https://github.com/decredcommunity/social-media-stats):

- [@decredproject](https://twitter.com/decredproject) Twitter broke the magic ["resistance"](https://github.com/decredcommunity/social-media-stats/blob/graphs/graphs/index.md) of 41K followers with an unusual jump by +423
- [Reddit](https://www.reddit.com/r/decred/) broke 10K subs :tada:
- [Discord](https://discord.gg/GJ2GXfz) got a nice +14%
- [DecredTrading](https://t.me/DecredTrading) Telegram got +72% users, to 158 _(God help us)_
- [@Checkmate](https://twitter.com/_Checkmatey_) got +11% followers (to 3.5K) and made _another_ 1K tweets (~34/day)
- [DecredES](https://t.me/DecredES) Telegram gained +18% (to 245)
- [CoinMarketCap](https://coinmarketcap.com/currencies/decred/) has 17.8K watchers for Decred

Thanks to Decred ambassadors on all platforms for raising awareness about the project!

## Governance

In December the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 12,099 DCR and spent 7,466 DCR. Using December's daily average DCR/USD rate of $31.07, this is $376K received and $232K spent. At October's average daily rate of $18.19, the USD figure billed for past work is $136K. As of Jan 5, Treasury balance is 641,260 DCR (30.2 million USD at $47.16).

Two proposals were submitted and voted on in December:

- The third [proposal](https://proposals.decred.org/proposals/350f64b) from the Decred ES team requested $14,800 to fund six months work, scaled down from an initial ask of $42,000, with items relating to Talent Land Blockchain Challenge and Codigo Decred being cut. This proposal was rejected with 54.5% Yes votes, having failed to meet the 60% threshold - turnout was 37%.
- The Decred Hackathons and LATAM Initial Chapter [proposal](https://proposals.decred.org/proposals/5ce1636) submitted after the hackathons element of the LATAM marketing proposal was cut, the people behind it are members of the ES team. The proposal requested a max budget of $17,000 to create materials for hackathons and run two hackathons, with $3,500 of the budget reserved for prizes. The proposal was rejected with 50.2% yes votes and turnout of 36%.

December is the last billable month for [US](https://proposals.decred.org/proposals/c830ea5), [Latam](https://proposals.decred.org/proposals/3c02b67) and [Brazil](https://proposals.decred.org/proposals/bc20f98) marketing proposals. Contractors working for them will need to submit renewal proposals to stay funded.

@JoeGruff has published three short progress and expense [updates](https://github.com/decredcommunity/proposals/tree/master/proposals/3943bff/updates) for his [address scanner](https://proposals.decred.org/proposals/3943bff) proposal.

While December was a quiet month for proposals, there are already two new ones in January, for renewed funding of [DCRDEX](https://proposals.decred.org/proposals/d462ac3) and [Decred in Depth](https://proposals.decred.org/proposals/391108e) (under new management).

Politeia Digest took a break in December but will be back soon.

## Network

Hashrate: December's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=ki3ivfpm-kjej4ggy&scale=linear&bin=block&axis=time) opened at ~292 Ph/s and closed ~340 Ph/s, bottoming at 240 Ph/s and peaking at 452 Ph/s throughout the month. Pool hashrate [distribution](https://miningpoolstats.stream/decred) as of Jan 1: UUPool 42%, Poolin 35%, easy2mine 12%, F2Pool 3.9%, Antpool 2.7%, Huobipool 2.6%, BTC.com 1.3%, Luxor 1.2%, CoinMine 0.02%.

Staking: [30-day average](https://dcrstats.com/) ticket price was 163.9 DCR (+5.2). The [price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=ki3ivfpm-kjej4ggy&axis=time&visibility=true-false&mode=stepped) varied between 150.6-190.99 DCR. [Locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=ki3ivfpm-kjej4ggy&scale=linear&bin=block&axis=time) was 6.42-6.68 million DCR, which corresponded to 52.01-54.20% of the available supply [participating](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=ki3ivfpm-kjej4ggy&scale=linear&bin=block&axis=time) in PoS.

Another month, another high broken. Ticket price peaked at 190.9 DCR and stake participation at 54.2%.

Nodes: Throughout [December](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1606780800000&to=1609459200000) there was an average of 87 public listening nodes and 200 total nodes per dcr.farm. Average version distribution for December: 27% dcrd v1.5.2, 21% dcrd v1.6 dev and RC builds, 16% dcrd v1.5.1, 5% dcrd v1.7 dev builds, 5% dcrd v1.5.0, 3% dcrd v1.5 dev and RC builds, 0.7% dcrd v1.4, 10% dcrwallet v1.5.1, 1.3% dcrwallet v1.6 dev and RC builds, 1% dcrwallet v1.5, 0.7% dcrwallet v1.4, 9% others.

@Checkmate reports via [Our Network](https://ournetwork.substack.com/p/our-network-issue-50-part-2) newsletter that a number of on-chain metrics are hitting all time highs.

@PermabullNino reports a ~500K DCR [increase](https://twitter.com/PermabullNino/status/1338497116864438273) in ticket pool balance over the 28-day period.

Mainnet Lightning Network is slowly growing. Throughout 2020 there was an average of 15 nodes, 30 channels and 6 DCR capacity. As of Jan 8 there are 24 nodes, 42 channels and a total capacity of 8.7 DCR according to @jholdstock's [LN map](https://ln-map.jamieholdstock.com/).

## Integrations

[Ultravsp](https://ultravsp.uk/) (formerly Ultrapool) and [Ubiq](https://dcrvsp.ubiqsmart.com/) VSPs have both launched mainnet instances of the new [vspd](https://github.com/decred/vspd) voting software. Their [dcrstakepool](https://github.com/decred/dcrstakepool) servers will continue running at [legacy.ultravsp.uk](https://legacy.ultravsp.uk/) and [dcr.ubiqsmart.com](https://dcr.ubiqsmart.com/), respectively.

Note that Ultravsp had to migrate from ultrapool.eu to a UK domain [ultravsp.uk](https://ultravsp.uk/) due to the Brexit [domain mess](https://www.theregister.com/2021/01/05/brexit_81000_eu_domains/), and there will be no automatic redirection due to prohibitive complexity of setting it up. VSP users who bought tickets recently have been notified via email.

Bittrex [added](https://twitter.com/BittrexExchange/status/1341801493964308482) an [instant exchange](https://bittrex.com/instant) feature that allows users to quickly buy assets with a debit card or exchange's fiat balance. DCR was reported to work.

Binance has enabled [margin trading](https://www.binance.com/en/support/announcement/d3614081a4254d1c815eb07e09f6cda8) for DCR/BTC and DCR/USDT, and announced a 1-week "zero-interest promotion for borrowing DCR". ([discussion](https://www.reddit.com/r/decred/comments/k8gy0d/margin_trading_for_dcr_enabled_on_binance/)) :supervillain:

[MXC Exchange](https://www.mxc.com/) [added](https://twitter.com/MXC_Exchange/status/1334707659900035075) 5x leverage margin trading DCR/USDT pair in addition to regular DCR/USDT pair they listed in 2019.

Turkish exchange [Bitexen](https://www.bitexen.com/) [announced](https://twitter.com/bitexencom/status/1339858540614266880) the listing of DCR among 11 other [assets](https://destek.bitexen.com/portal/tr/kb/articles/bitexen-11-adet-yeni-coin).

Malta-based instant exchange aggregator [Swapzone](https://swapzone.io/) has DCR support since [May](https://twiter.com/swapzoneio/status/1263049492963774465) or earlier but in December it got on our radar and was [added](https://github.com/decred/dcrweb/pull/937) to decred.org [exchanges](https://decred.org/exchanges/) page.

Korean Upbit has [delisted](https://www.reddit.com/r/decred/comments/kfu4sb/whats_going_on_in_korea_upbit/) DCR, apparently in disagreement with Decred's mission to protect individual privacy. :supervillain:

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Decred in Spanish team published the final [6th report](https://github.com/decredcommunity/proposals/blob/master/proposals/3c02b67/updates/20201211.md) for their 2nd proposal. Voting has ended for their 3rd proposal with significant 54.5% and 50.2% Yes votes but did not reach the required threshold of 60%. The team is collecting [feedback](https://www.reddit.com/r/decred/comments/kkb97s/what_are_your_thoughts_on_the_decred_in_spanish/) on Reddit and planning what to do next.

@michae2xl published the final [report](https://github.com/decredcommunity/proposals/blob/master/proposals/bc20f98/updates/20210105.md) that covers December activities for the Brazil marketing proposal.

Monde PR's achievements for December:

- created and pitched two story ideas to finance and crypto publications

News coverage secured by Monde PR:

- @jy-p was interviewed by [NASDAQ Trade Talks](https://www.nasdaq.com/videos/tradetalks:-how-can-blockchain-can-be-used-in-elections) talking about Decred's use in Brazilian elections. The interview was mentioned in subsequent articles in [Coin Journal](https://coinjournal.net/news/decred-bounces-off-42-after-spiking-50/), [Crypto Potato](https://cryptopotato.com/decred-dcr-pumps-50-as-social-sentiment-surges/), [Coin Market Cap](https://coinmarketcap.com/headlines/signals/decred-co-founder-on-nasdaq-tradetalks-decred/) and [CryptoMode](https://cryptomode.com/5-reasons-why-you-shouldnt-overlook-decred-dcr/)
- details of the DCRDEX launch and Decred's use in Brazilian elections were featured in [Cointelegraph](https://cointelegraph.com/news/bitcoin-bull-market-pulls-kusama-ksm-decred-dcr-and-qtum-price-higher)
- @jy-p was interviewed by the [Geek Insider Podcast](https://www.youtube.com/watch?v=mYK_Awn1wTk) talking about the origin of Decred, the DCRDEX launch and Decred's use in Brazilian elections
- details of the DCRDEX launch were also featured in [Brave New Coin](https://bravenewcoin.com/insights/decred-price-analysis-active-addresses-hit-all-time-highs-as-trend-metrics)
- comments from @jy-p's Cointelegraph interview about Bitcoin bull and bear cycles were featured in [Forex Academy](https://www.forex.academy/how-to-spot-bitcoin-bull-bear-cycles-beginners-edition/) and [Inside Bitcoin](https://insidebitcoins.com/news/bitcoin-btc-price-prediction-november-29-2020-2)
- @jy-p's comments about Ledger's security challenges were featured in [The Union Journal](https://www.theunionjournal.com/ledger-cto-discusses-wallets-safety-after-multiple-security-setbacks/)

## Events

Attended:

- Dec 3 - [Hablemos Decred 24](https://decredcommunity.github.io/events/index/20201203.1) - Internet. @elian and @pablito discussed how private cryptocurrencies are.
- Dec 5 - [World Blockchain Conference](https://decredcommunity.github.io/events/index/20201205.1) - Wuhan, China. There was no formal Decred event but @Dominic met with old friends at Cobo Wallet, F2Pool and others, to introduce them to the upcoming v1.6 and new consensus rules.
- Dec 10 - [Hablemos Decred 25](https://decredcommunity.github.io/events/index/20201210.1) - Internet. Decred in Spanish team gathered to review 1 year working in the DAO, the good, the bad, the challenges, and what's coming for 2021.
- Dec 11 - [Cripto Latin Fest Online 2020](https://decredcommunity.github.io/events/index/20201211.1) - Internet. Co-organized by Paxful Latam. Decred was a VIP sponsor. @elian presented common talking points for Decred and the upcoming Hidden Hydra, which got 1.6K views on Facebook and ~800 on YouTube. In another panel he talked about how to prevent crypto scams.
- Dec 16 - [UAM Xochimilco](https://twitter.com/addcade/status/1338544856344317953) - Mexico City, Mexico. @adcade talked about Decred's organization and Politeia at Aula Multimedia lab of the UAM Xochimilco university.
- Dec 18 - [New Year at CR!](https://decredcommunity.github.io/events/index/20201218.1) - Internet. Crypto Resources Academy organized a year-end event and invited partners like Decred, Bitso, Prime XBT DAI, Binance, and others. During the governance panel @elian presented how Decred governance works, the role of Politeia and the decentralization of the Treasury.
- Dec 24 - [Decred AMA](https://decredcommunity.github.io/events/index/20201224.1) - Internet. This AMA for OKEx in Spanish community took place on their [Telegram](https://t.me/OKExLATAM) with ~500 users. Over 30 questions were asked about Decred's governance, privacy, future developments, history and the DEX. There was also a DCR giveaway ($20 from OKEx and $30 from Decred in Spanish). Over 30 new members joined [@DecredES](https://t.me/DecredES) channel.
- Dec 30 - [Decred in Spanish New Year Giveaway](https://decredcommunity.github.io/events/index/20201230.1) - Internet. To participate, people needed to join @DecredES Telegram and tell what they like about Decred. Out of 28 comments, 9 best were selected based on the knowledge and understanding of the project and received 3 DCR in total.

The information above is available in greater detail in our [events tracker](https://decredcommunity.github.io/events/index/) that is being built to learn what works and improve reporting of marketing efforts. Thanks to everyone [submitting](https://github.com/decredcommunity/events/blob/master/docs/submit-index.md) and reviewing events.

## Media

@mm completed his 7-part series on blockchain governance:

- [part 1](https://stakey.club/en/blockchain-gov-part1/) introduces cryptocurrencies, money printing and Bitcoin
- [part 2](https://stakey.club/en/blockchain-gov-part2/) covers the technology behind cryptocurrencies, Proof-of-Work security, incentives and inflation
- [part 3](https://stakey.club/en/blockchain-gov-part3/) explains basic architecture types (permissionless/permissioned, public/private), Bitcoin governance, privacy and fungibility, and applications of blockchain beyond digital money (esp. e-voting)
- [part 4](https://stakey.club/en/blockchain-gov-part4/) introduces Decred Project fundamentals (security, consensus, funding, skin in the game) and compares it to pure PoW and PoS approaches
- [part 5](https://stakey.club/en/blockchain-gov-part5/) assesses blockchain security and governance of Bitcoin vs Decred using @mm's [InvalidationGame](https://github.com/mmartins000/invalidationgame) attack simulator, considering external and internal attacks. Among other details, it provides separate estimates for capex and opex required for attacking Bitcoin and Decred.
- [part 6](https://stakey.club/en/blockchain-gov-part6/) tests a number of hypotheses against real data (topics include correlation of on-chain metrics with price, voter turnout, OLS model, and more)
- [part 7](https://stakey.club/en/blockchain-gov-part7/) concludes the series by summarizing simulation results, findings on security, and what Decred can offer to the world

> Decred Project not only aims to provide an alternative to financial systems that depend on a trusted third party and to people that depend on the good will of giant financial institutions but also to show how e-voting may happen in a secure and transparent fashion.

Code in Python/R/SQL used in the research is available on [GitHub](https://github.com/mmartins000?tab=repositories).

Selected articles:

- Decred price analysis - Active addresses hit all-time highs as trend metrics flip bullish by Josh Olszewicz ([bravenewcoin.com](https://bravenewcoin.com/insights/decred-price-analysis-active-addresses-hit-all-time-highs-as-trend-metrics)) - comes with a [video](https://www.youtube.com/watch?v=oCYZS_qJ7us) version

Videos:

- Decred bi-weekly news update - Privacy page revamped, lots of dev updates, 1.6 inbound, and more! by @Exitus ([youtube](https://www.youtube.com/watch?v=-3s9_jMWNuA))
- New yearly high for Decred by Decred Society ([youtube](https://www.youtube.com/watch?v=qw-ohbTObeo))
- Decred is ideal for savers by Decred Society ([youtube](https://www.youtube.com/watch?v=zYDT0n59C7k))
- Decred crypto analysis - King DCR AWAKENS! Every action has an equal and opposite reaction! by DubDigital ([youtube](https://www.youtube.com/watch?v=kqAD_PSgyME))
- Jake Yocom-Piatt talks Decred and blockchain at Geek Insider ([youtube](https://www.youtube.com/watch?v=mYK_Awn1wTk))
- How can blockchain can be used in elections? with Jake Yocom-Piatt and Jill Malandrino of NASDAQ TradeTalks ([youtube](https://www.youtube.com/watch?v=pBSn_CdQYts))
- Staked Podcast: Episode 0.0.5 ([youtube](https://www.youtube.com/watch?v=BbBcngzuxCw)) - update on the state of the podcast and an announcement regarding Eduardo and Decred
- Interview with @BTC\_Uncle by Staked Podcast ([youtube](https://www.youtube.com/watch?v=__7LTz3nQKk), short [clip](https://www.youtube.com/watch?v=3ubS_27FEhE) on why Decred)
- Interview with Ammar Naseer (@Ammarooni) by Staked Podcast ([youtube](https://www.youtube.com/watch?v=g0bFMuHXrkU))
- 2020 onchain close out session BTC + DCR by @Checkmate ([youtube](https://www.youtube.com/watch?v=g60ovCl54OA))
- Decred Deep Dive: Hidden hydra release is incoming! by @Checkmate ([youtube](https://www.youtube.com/watch?v=3AxBa-EE8RM), [discussion](https://www.reddit.com/r/decred/comments/klz8ue/decred_deep_dive_hidden_hydra/))

Audio:

- Rough Consensus 14: Rehashing bull market happenings. @Checkmate and @PermabullNino share their thoughts on Bitcoin ATHs, ETH 2.0, DCR 1.6, and more. ([libsyn](https://roughconsensus.libsyn.com/episode-14-rehashing-bull-market-happenings))
- Rough Consensus 15: The next paradigm. Mav from Ready Set Crypto hops on the pod to talk big picture crypto. ([libsyn](https://roughconsensus.libsyn.com/episode-15-the-next-paradigm-with-mav-ready-set-crypto))

Art/fun:

- hilarious Decred [GOT cover](https://streamable.com/iam635) by @degeri
- "They [don't know](https://twitter.com/aithzakaria1/status/1335706207395450880) I have Decred" by @aithzakaria1
- it's [time](https://twitter.com/aithzakaria1/status/1330999761634258948) for Decred, Ben! by @aithzakaria1
- survival through adaptation - [merch](https://twitter.com/OfficialCryptos/status/1338551937818562561) design by @OfficialCryptos
- DCR violently [cutting through CMC](https://twitter.com/exitusdcr/status/1343774006344880130) by @Exitus
- [Digital Nation State](https://twitter.com/AGNFAB1/status/1338963085537718275) by @AGNFAB
- @New\_Copernicus shared more teaser clips on [Hidden Hydra](https://twitter.com/New_Copernicus/status/1336044535370092546), [Decred Rabbit Hole](https://twitter.com/New_Copernicus/status/1339649654842126337), cheerful [Happy Holidays!](https://twitter.com/New_Copernicus/status/1341665478935076865) and [Happy New Year!](https://twitter.com/New_Copernicus/status/1344509258176622593)

Translations:

- Arabic translation of "Decred: Where did it all begin?" published at [satoshiat.com](https://www.satoshiat.com/2020/12/%d8%a7%d9%84%d8%af%d9%8a%d9%83%d8%b1%d9%8a%d8%af-%d9%85%d9%86-%d8%a3%d9%8a%d9%86-%d8%a8%d8%af%d8%a3%d8%aa%d8%9f/) crypto-focused website.
- The general "Utility of cryptoassets" and more technical "Security hardening for digital wallets" and "Verifying digital signatures: Decred" from stakey.club translated to Spanish by @francov\_ (see Spanish [translations](https://github.com/DecredES/traducciones) repo and their [Medium](https://medium.com/decred-es))
- Decred Journal November 2020 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), and Spanish (@francov\_). Thank you all for spreading Decred news!
- all known translations are tracked in [this index](https://github.com/decredcommunity/translations/blob/master/index.md) that has 305 items as of writing

Other non-English content:

- "The Decred cryptocurrency increased by 50% and surpassed DeFi coins" ([es.cointelegraph.com](https://es.cointelegraph.com/news/the-decred-cryptocurrency-increased-by-50-and-surpassed-defi-coins))
- @arij recorded a greatly improved Decred introduction in Arabic ([youtube](https://www.youtube.com/watch?v=k6xXL_ttSDI))

## Community Discussions

Selected Reddit posts:

- adding [ERC-20](https://www.reddit.com/r/decred/comments/khnc35/adding_erc20_to_the_dex/) on DCRDEX
- Is [churning](https://www.reddit.com/r/decred/comments/kho4db/is_churning_useful_with_coinshuffle/) (sending to self) useful with CoinShuffle++? (hint: CSPP is a non-trivial incentive to stake DCR)
- [trade-offs](https://www.reddit.com/r/decred/comments/k6dn93/what_are_the_trade_offs_for_decreds_privacy/) of Decred privacy features
- the benefits of the upcoming changes to the VSP system from a perspective of a [VSP operator](https://www.reddit.com/r/decred/comments/k9hegy/upcoming_changes_in_16_for_proofofstake_using_vsps/)

Selected Twitter discussions:

- @Ammarooni reminds that December 15 marked the [5th anniversary](https://twitter.com/Ammarooni/status/1338898342722605057) of Decred's first [announcement](https://bitcointalk.org/index.php?topic=1290358.0) on bitcointalk forum
- short [history](https://twitter.com/lefebvre_dustin/status/1333816694922485761) how Decred coded on regardless of the oracles, by @Dustorf

## Markets

In December DCR was trading between USD 24.01-41.59 / BTC 0.0012-0.0020. The average daily rate was $31.07.

With the massive Bitcoin runup, Decred has also been raising in USD without losing much ground in BTC value.

DCR was trading [unusually](https://www.reddit.com/r/decred/comments/kfu4sb/whats_going_on_in_korea_upbit/) high up to $350 on Upbit until it was delisted there.

During the 48 days of DCRDEX operation it has [traded](https://ournetwork.substack.com/p/our-network-issue-50-part-2) ~600K DCR, which is 30% of Binance volume over the same period. Unlike any centralized exchange though, this volume is much more reliable and harder to cheat.

@bochinchero [published](https://twitter.com/TheBochinchero/status/1339202616153284608) his first on-chain analysis piece on Decred, proposing new valuation metrics:

> Staked Realised Value is a metric that is analogous to the Realised Value but applied exclusively to coins circulating within the ticket pool, essentially treating every ticket as a UTXO. \[it\] provides a more accurate valuation of the capital locked into the security and governance of the network. During past sharp sell-offs it has acted as a psychological bottom - the point of maximum pain, where the buyers of last resort step in.

@Checkmate [announced](https://twitter.com/_Checkmatey_/status/1338418991212052485) the launch of [checkonchain.com](https://checkonchain.com/) with many, many (many) charts:

> Now this is something I have been working on for a very long time. If you want serious edge in this market, pay attention to the beating heart of the chain. A full blown masterclass to learn how to properly apply each metric is coming in hot soon after.

## Relevant External

The Cover Protocol, a DeFi insurance project which "allows DeFi users to be protected against smart contract risk", was [hacked](https://www.coindesk.com/cover-protocol-plans-new-token-after-attack) and the attacker minted 40 quintillion COVER tokens, liquidating these for $4 million, but later returning the funds to the smart contract. The team are now looking at creating a new version of the COVER token with a snapshot to refund COVER holders, because otherwise those extra 40 quintillion tokens would mess up the tokenomics.

Nexus Mutual's CEO was hacked for $8.3 million when an attacker tricked him into signing a transaction that sent all his NXM to the attacker's wallet. The attacker [laundered](https://coingeek.com/nexus-mutual-attacker-cashes-out-3-million/) $2.7 million to BTC, and this sent the NXM price lower, they then sent a message on the Ethereum blockchain offering to return the rest (so NXM could avoid further pain) for a [ransom](https://coingeek.com/nexus-mutual-attacker-wants-3-million-in-ransom-money/) of $2.8 million in ETH.

December's top DeFi rug pull was [Compounder finance](https://www.coindesk.com/compounder-developers-implicated-alleged-smart-contract-rug-pull), whose devs absconded with $10.8 million of investor funds after utilizing a hidden backdoor in the contracts.

December's top flash loan attack victim was [Warp Finance](https://decrypt.co/52125/warp-finance-recovers-5-8-million-days-after-hack), with the exploit weighing in at $7.7 million, but $5.85 million is being returned to holders. This is arguably December's top DeFi hack refund too, but COVER is a contender for that title because although the dollar amount being returned was smaller, it represented a ridiculous proportion of the COVER supply.

Gitcoin ended a [strong 2020](https://gitcoin.co/blog/gitcoin-year-in-review/) with its 8th round of Ethereum funding seeing a matching pool of $450K, and also the first round of non-Ethereum funding for Zcash projects was [completed](https://electriccoin.co/blog/zcash-gitcoin-grants-round-1-retrospective/), dispensing a $25K matching pool from Zcash Foundation but attracting just 156 donations totalling $2,137.

A bill was [introduced](https://www.coindesk.com/us-lawmakers-introduce-bill-that-would-require-stablecoin-issuers-to-obtain-bank-charters) in US Congress that would require stablecoin issuers to obtain bank charters, requiring approval from the Federal Reserve and various other bodies before circulating any coins.

The front line in crypto regulations then [shifted](https://www.coindesk.com/self-hosted-bitcoin-wallets-become-front-line-in-fight-over-crypto-regulations) to "self-hosted wallets" (i.e. any self-custodied crypto) and the degree of due diligence that exchanges are required to carry out on transactions involving these questionable entities.

Bittrex announced that it will be [delisting](https://www.coindesk.com/bittrex-to-delist-privacy-coins-monero-dash-and-zcash) privacy coins Monero, Zcash and Dash on Jan 15, without stating a specific reason. Around a month before that the same coins have been [delisted](https://www.coindesk.com/shapeshift-delists-privacy-coin-zcash-over-regulatory-concerns) by ShapeShift.

Bittrex also became the eleventh exchange to [delist](https://decrypt.co/52855/even-bittrex-is-halting-trading-of-xrp) XRP, a week after US SEC charged Ripple Labs with raising $1.3 billion by selling the coin in unregistered securities sales. This reminds that raising funds is a long-term systemic risk that may backfire years after the ICO.

In an effort to shake off regulators, Facebook's Libra [rebranded](https://www.forbes.com/sites/jasonbrett/2020/12/02/facebooks-libra-renamed-to-diem-prior-to-stablecoin-launch) to Diem and dropped the aspiration of being backed by a basket of currencies in favor of straight USD backing.

Ledger's leak of customer data, originally reported in July, has now been [dumped](https://cointelegraph.com/news/ledger-data-leak-a-simple-mistake-exposed-270k-crypto-wallet-buyers) publicly. In the original announcement Ledger stated that more detailed information such as physical address had been accessed for 9.5K customers, but it seems [now](https://www.ledger.com/message-ledgers-ceo-data-leak/) that this information was harvested for 272K customers.

## Support DJ on the web!

We don't know what you guys did but November DJ was an anomaly. 100+ Twitter likes up from average 60, 1K+ Medium claps vs regular ~300, hitting [top 10](https://medium.com/tag/decentralized-exchange/archive/2020/12) December posts tagged "DEX" on Medium, good views on Publish0x, and so on.

Thank you for pressing all these buttons! Please keep going to bring visibility for the best cryptocurrency project.

## About This Issue

This is issue 33 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

You can submit a story [here](https://github.com/xaur/decred-news/labels/next%20release) to be considered for the next release. [Feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, lukebp, richardred
- reviews and feedback: davecgh, elian, JoeGruff, oshorefueled
- title image: saender
- funding: Decred Treasury
