# Decred Journal – April 2021

![abstract art by @saender](../img/202104.1.github.png)

_Image: Point Integral by @saender_

April's highlights:

- Decred's 6th consensus vote has passed with unanimous approval and high voter turnout.
- Politeia v1.0 is now live with more scalable and future-proof infrastructure.
- Politeia's first proposal is being voted on to formalize the development roadmap and budget.
- DCRDEX is heading towards v0.2 update with several backend and UX improvements, as well as the foundations for future exciting features.
- Initial DCRDEX integration has been merged in Decrediton.

Contents:

- [Development](#development)
- [People](#people)
- [Governance](#governance)
- [Network](#network)
- [Ecosystem](#ecosystem)
- [Outreach](#outreach)
- [Events](#events)
- [Media](#media)
- [Community Discussions](#community-discussions)
- [Markets](#markets)
- [Relevant External](#relevant-external)

## Development

The work reported below has the "merged to master" status unless noted otherwise. It means that the work is completed, reviewed, and integrated into the source code that advanced users can [build and run](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c), but is not yet available in release binaries for regular users.

<a id="dcrd" />

**[dcrd](https://github.com/decred/dcrd)**

- codebase [converted](https://github.com/decred/dcrd/pull/2625) to use the new `stdaddr` package. Code that deals with addresses now supports different script versions and is one step closer to being able to cleanly introduce new scripting language versions. As common for large changes, to make review easier this one was split into a series of individual commits such that everything builds and passes all tests each step of the way.
- introduced [UTXO database](https://github.com/decred/dcrd/pull/2632). It paves the way for a specialized UTXO database implementation that can be made more efficient in terms of both processing time and memory usage.
- added [median time](https://github.com/decred/dcrd/pull/2638) over the last 11 blocks to verbose `getblock` and `getblockheader` results (used by DCRDEX)
- allow to specify network interfaces to listen by their [names](https://github.com/decred/dcrd/pull/2623) in addition to exact IP addresses

Initial chain sync [comparison](https://www.reddit.com/r/decred/comments/mi4ezt/initial_chain_sync_comparison_between_dcrd_v140/) between dcrd v1.4.0 and latest shows how all the improvements have accumulated into a big difference in performance. Despite there now being ~70% more blocks, the latest version takes almost the same time to sync while allocating way less memory.

<a id="dcrwallet" />

**[dcrwallet](https://github.com/decred/dcrwallet)**

- a new method that returns wallet's [sync status](https://github.com/decred/dcrwallet/pull/1991)
- handle ticket status when the VSP has [received](https://github.com/decred/dcrwallet/pull/1965) its fee tx but has not yet broadcast it
- fixed bugs found when used by DCRDEX

<a id="decrediton" />

**[Decrediton](https://github.com/decred/decrediton)**

- initial [DEX integration](https://github.com/decred/decrediton/pull/3356)
- a form for [funding](https://github.com/decred/decrediton/pull/3426) the DEX account from the registration view
- allow to use an [existing](https://github.com/decred/decrediton/pull/3438) wallet account for the DEX instead of making a new one
- added [QR code](https://github.com/decred/decrediton/pull/3112) generation to export active tickets (for tracking with the Decred Address Scanner app)
- [remember](https://github.com/decred/decrediton/pull/3441) ticket auto-buyer settings
- added a migration to initialize [account](https://github.com/decred/decrediton/pull/2664) passphrases with the wallet passphrase. Also, some operations (send, purchase ticket, mixing, revoke) switched to only unlock a single account instead of unlocking an entire wallet.
- lock [new accounts](https://github.com/decred/decrediton/pull/3424) after creation
- allow restoring hex seeds up to 128 characters (including BIP0039 seeds)
- updated design of [Transactions](https://github.com/decred/decrediton/pull/3326), [Proposals](https://github.com/decred/decrediton/pull/3345) and [Purchase tickets](https://github.com/decred/decrediton/pull/3349) views
- many smaller design tweaks
- switched to a strict Protobuf generation without `eval()` and restricted to only access external servers via `https` in production builds using the [CSP header](https://github.com/decred/decrediton/pull/3366)
- refactoring of state management, separation of concerns, dependency upgrades
- increased test coverage
- ~24 bug fixes

Release [v1.6.3](https://github.com/decred/decrediton/tree/release-v1.6%2B) is being prepared including many of the above changes.

<a id="politeia" />

**[Politeia](https://github.com/decred/politeia)**

Politeia v1.0.0 has been released with the new storage backend, streamlined API, new plugin architecture, and 5 plugins. Read the [release notes](https://github.com/decred/politeia/releases/tag/v1.0.0) for full details on each feature. The new version has been deployed at [proposals.decred.org](https://proposals.decred.org/).

2FA support tried hard to escape our attention and is now live. Users can set it up in account settings. Don't forget to backup the key.

Merged in April:

- list [proposals](https://github.com/decred/politeiagui/pull/2340) from [proposals-archive.decred.org](https://proposals-archive.decred.org/) on proposals.decred.org for convenience
- [verify](https://github.com/decred/politeia/pull/1377) comment and vote bundles with the new `politeiaverify` tool
- list registration fee in the [history](https://github.com/decred/politeiagui/pull/2322) of purchases
- ~24 bugs discovered in the new version have been fixed

One notable change is the addition of [timestamps](https://github.com/decred/politeia/pull/1395) to cast votes. In Git backend precise timestamps were not stored to improve voter privacy, and as a result, it was only possible to determine if a vote was cast within a ~60 min period. In tstore backend timestamp is already being recorded by Trillian and this cannot be changed without writing a custom Trillian implementation. Because vote timestamp is now public data anyway, adding it directly to the vote structure allows dcrdata to obtain it much easier (e.g. to build its vote [graphs](https://dcrdata.decred.org/proposal/video-content-production-for-decred-phase-3)). But it also means a bit lower privacy for people casting all their votes at once. People who want to protect their privacy are strongly advised to use `politeiavoter`'s [trickling feature](https://github.com/decred/politeia/blob/master/politeiawww/cmd/politeiavoter/README.md#privacy-considerations).

@lukebp talked about Politeia development, latest releases, and future directions on Decred in Depth [podcast](https://www.youtube.com/watch?v=J6IAjmwkki0) (starts at 12 min).

Politeia's own first [proposal](https://proposals.decred.org/record/91cfcc8) is now live (and voting), formalizing its development roadmap and budget until the end of 2021.

<a id="dcrpool" />

**[dcrpool](https://github.com/decred/dcrpool)**

- improved [connectivity](https://github.com/decred/dcrpool/pull/317)
- more [efficient](https://github.com/decred/dcrpool/pull/318) [miner](https://github.com/decred/dcrpool/pull/319) [handling](https://github.com/decred/dcrpool/pull/320)

<a id="dcrlnd" />

**[dcrlnd](https://github.com/decred/dcrlnd)**

- support [unlocking](https://github.com/decred/dcrlnd/pull/136) a specific account (for Decrediton)

<a id="dcrdex" />

**[DCRDEX](https://github.com/decred/dcrdex)**

- show important [server info](https://github.com/decred/dcrdex/pull/1042) (like the lot size - minimum tradeable amount) before the user pays registration fee
- better handling of [inactive](https://github.com/decred/dcrdex/pull/1030) orders
- use [median time](https://github.com/decred/dcrdex/pull/1058) for transaction finalization
- ensure all [fee rates](https://github.com/decred/dcrdex/pull/1060) are capped by config
- reduced [memory](https://github.com/decred/dcrdex/pull/1070) usage during database upgrade
- [responsive](https://github.com/decred/dcrdex/pull/1016) GUI
- support for CPU and HTTP [profiling](https://github.com/decred/dcrdex/pull/1035)
- improved [couch testing](https://github.com/decred/dcrdex/pull/1038) experience
- added versioning for [server API](https://github.com/decred/dcrdex/pull/1047) and [asset](https://github.com/decred/dcrdex/pull/1054) backends
- fixed some sync issues

An [update](https://www.reddit.com/r/decred/comments/n9i8z2/dcrdex_updates_v02_release_decrediton_integration/) on Phase 2 development was posted in May with the following key points:

- v0.2 release has finished beta testing, expect binaries and server update soon
- v0.2 brings many improvements, including support for the upcoming Decrediton integration
- SPV wallet support for both Decred and Bitcoin are planned in next releases this year
- ETH development is in progress and is expected to release toward the end of Phase 2
- for more exciting features read the [update](https://www.reddit.com/r/decred/comments/n9i8z2/dcrdex_updates_v02_release_decrediton_integration/) and the linked release notes

<a id="dcrandroid" />

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

- show [USD equivalent](https://github.com/planetdecred/dcrandroid/pull/539) balance on Overview page
- dcrlibwallet [updated](https://github.com/planetdecred/dcrlibwallet/pull/183) to new dcrwallet module

<a id="dcrios" />

**[dcrios](https://github.com/planetdecred/dcrios)**

- show Politeia [proposals](https://github.com/planetdecred/dcrios/pull/715) and notify on certain events (new proposal, vote started, vote ended)
- database [upgraded](https://github.com/planetdecred/dcrios/pull/742) to BadgerDB

<a id="godcr" />

**[godcr](https://github.com/planetdecred/godcr)**

- show Politeia [proposals](https://github.com/planetdecred/godcr/pull/331)
- polished UI on [Transactions](https://github.com/planetdecred/godcr/pull/356), [Wallet](https://github.com/planetdecred/godcr/pull/355), and [Receive](https://github.com/planetdecred/godcr/pull/354) pages
- show USD equivalent on the [nav bar](https://github.com/planetdecred/godcr/pull/380) and on the [Send](https://github.com/planetdecred/godcr/pull/371) confirmation popup
- added sending to own [account](https://github.com/planetdecred/godcr/pull/353)
- numerous smaller UX tweaks

<a id="dcrdata" />

**[dcrdata](https://github.com/decred/dcrdata)**

- improved [Attack cost](https://github.com/decred/dcrdata/pull/1777) page layout
- improved display of [Treasury](https://github.com/decred/dcrdata/pull/1817)-related tx
- updated to [Webpack 5](https://github.com/decred/dcrdata/pull/1809) and other dependencies

<a id="dcrdocs" />

**[docs](https://github.com/decred/dcrdocs)**

- [dark mode](https://github.com/decred/dcrdocs/pull/1161)!
- [Migrations](https://github.com/decred/dcrdocs/pull/1163) page for the upcoming Decrediton v1.6.3

## People

Get to know Decred contributors in the new interviews with [@lukebp](https://www.youtube.com/watch?v=J6IAjmwkki0) and [@phoenixgreen](https://www.youtube.com/watch?v=WOVUvzsp3Eo).

Community stats as of May 1:

- [Twitter](https://twitter.com/decredproject) followers: 44,391 (+763)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 10,987 (+190)
- [Matrix](https://chat.decred.org/) #general users: 434 (+27)
- [Discord](https://discord.gg/GJ2GXfz) users: 1,566 (+157)
- [Telegram](https://t.me/Decred) users: 2,645 (+51)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,500 (+40), views: 182K (+3K)
- GitHub [dcrd](https://github.com/decred/dcrd) stars: 591 (+2), forks: 254 (-1)

See the [April report](https://decredcommunity.github.io/social-media-stats/posts/20210506.1) for notable social media stats updates.

## Governance

In April the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 10,949 DCR and spent 984 DCR. Using April's average DCR rate of $198.60, this is $2.17M received and $195K spent. At March's average rate of $161.01, the USD billed for past work is $158K. As of May 2, the Treasury balance is 672,768 DCR (140 million USD at $208.13).

The consensus vote to enable the new treasury has [passed](https://explorer.dcrdata.org/agenda/treasury) with 99.9% approval and 83% voter participation. This is the second highest voter turnout in Decred's history after the [stake difficulty](https://dcrdata.decred.org/agenda/sdiffalgorithm) vote in 2017 (88%).

Proposal news:

- A new [proposal](https://proposals.decred.org/record/91cfcc8) for funding Politeia development accompanied the deployment of v1.0.0. This proposal requests a maximum budget of $118K to cover a range of new features, expected to be delivered over a six month period. The features on this roadmap include another upgrade to the plugin architecture, user API overhaul, email-free accounts, extra metadata for proposals, proposal life cycles, and proposal author updates. The vote started on May 11.
- The video production phase 3 [proposal](https://proposals-archive.decred.org/proposals/95a1409) was approved with 98% approval and voter participation of 40%.
- The Design domain [proposal](https://proposals-archive.decred.org/proposals/76eba5a) for the remainder of 2021 was approved with 97% approval and voter participation of 28%.

See Politeia Digest [issue 42](https://blockcommons.red/politeia-digest/issue042/) for more details on the month's proposals.

## Network

**Hashrate**: April's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kmvlwq6x-ko7rp8zy&scale=linear&bin=block&axis=time) opened at ~464 Ph/s and closed ~429 Ph/s, bottoming at 219 Ph/s and peaking at 587 Ph/s throughout the month.

Distribution of hashrate [reported](https://miningpoolstats.stream/decred) by the pools on May 1: Poolin 35%, Antpool 28%, F2Pool 18%, Easy2Mine 4%, BTC.com 1.8%, Luxor 1.3%, UUPool 0.09%, Coinmine 0.06%, Huobipool 0.02%, others 12%. This time the reported hashrate closely matched the distribution of 1,000 actually [mined blocks](https://miningpoolstats.stream/decred).

A sharp hashrate drop around Apr 15-20 has been attributed to a major [power outage](https://www.reddit.com/r/decred/comments/mvk976/network_hashrate_plummeting/) in China.

**Staking**: [Ticket price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kmvlwq6x-ko7rp8zy&axis=time&visibility=true-false&mode=stepped) varied between 163.5-204.1 DCR, with 30-day [average](https://dcrstats.com/) at 185.8 DCR (+7.8).

The [locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kmvlwq6x-ko7rp8zy&scale=linear&bin=block&axis=time) was 7.11-7.51 million DCR, meaning that 55.4-58.5% of the circulating supply [participated](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kmvlwq6x-ko7rp8zy&scale=linear&bin=block&axis=time) in proof-of-stake.

**VSP**: On May 1, 7.1K (+0.5K) live tickets were managed by vspd servers and 2.2K (-1.8K) by the [listed](https://decred.org/vsp/) legacy dcrstakepool servers. Collectively the 15 legacy and 13 new VSPs managed 23% of the ticket pool. The 2 recently delisted legacy VSPs still had 105 live tickets.

**Nodes**: Throughout April there were around ~210 reachable nodes according to [dcrextdata](https://dcrextdata.planetdecred.org/nodes).

Node versions as of May 1 [snapshot](https://nodes.jholdstock.uk/user_agents) (257 total, dcrd only): v1.6.0 - 26%, v1.6.2 - 24%, v1.6.1 - 22%, v1.5.2 - 7%, v1.5.1 - 7%, v1.7 dev builds - 7%, v1.6 dev builds - 4%, v1.5.0 - 2%.

The share of [mixed coins](https://explorer.dcrdata.org/charts?chart=coin-supply&zoom=kmvlwq6x-ko7rp8zy&bin=day&axis=time&visibility=true-true-true) has slightly declined from 44% to 42%. Daily [mixed amount](https://explorer.dcrdata.org/charts?chart=privacy-participation&zoom=kguk0rxu-koc4hs00&bin=day&axis=time) varied between 150-300K DCR.

Bison's presence has been spotted on [LN](https://ln-map.jholdstock.uk/) as a node called "El Gran Bisonte ⚡🐂⚡".

## Ecosystem

Welcome the new [vspd](https://github.com/decred/vspd) server from [stakey.com](https://vspd.stakey.com/) with 0.3% fee - lowest on the market as of writing. Its legacy VSP server has been removed from the [listing](https://decred.org/vsp/) but is still operational with 80 [live tickets](https://stakey.com/stats) as of May 7.

dcr.farm's [legacy VSP](https://dcr.farm/stats) was observed with a 30% fee, possibly to discourage new registrations. Pay attention to the fees to not buy a high-fee ticket by accident. dcr.farm's [vspd server](https://vsp.dcr.farm/) has a normal 0.95% fee.

[Baap ATM](https://baap.app/) [tweeted](https://twitter.com/baapapp/status/1376975012830326786) that their ATMs and agents will help to [buy DCR](https://baap.app/buy-decred-coin/) for CAD in some locations in Canada.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to anyone.

Join our [#services](https://chat.decred.org/#/room/#services:decred.org) chat to follow Decred ecosystem updates.

## Outreach

A new process has been set up to broadcast important project announcements on multiple platforms. The "ANNs" are issued only for important updates and have much lower traffic compared to Decred's [Twitter](https://twitter.com/decredproject). Matrix room [#dcr](https://chat.decred.org/#/room/#dcr:decred.org) is the newest addition, the other destinations being: [Twitter](https://twitter.com/decredproject), [Telegram](https://t.me/DCRann), Discord, [Reddit](https://www.reddit.com/r/decred/), [CoinGecko](https://www.coingecko.com/en/coins/decred), [Blockfolio](https://blockfolio.com/coin/DCR), and [Gab](https://gab.com/decredproject).

Supporters on Reddit have made the case for Decred in multiple relevant conversations on r/CryptoCurrency ([one](https://www.reddit.com/r/CryptoCurrency/comments/m03ay0/what_are_your_favorite_top_100_coins_to_stake_and/), [two](https://www.reddit.com/r/CryptoCurrency/comments/m2cza0/lets_talk_about_dexs_and_do_we_really_need_so_many/), [three](https://www.reddit.com/r/CryptoCurrency/comments/m895oa/which_is_your_favorite_dao/), [four](https://www.reddit.com/r/CryptoCurrency/comments/madahw/you_can_buy_5_coins_now_anf_only_access_them/), [five](https://www.reddit.com/r/CryptoCurrency/comments/mcqzk7/too_many_post_your_undervalued_coins_posts_here/), [six](https://www.reddit.com/r/CryptoCurrency/comments/msifo2/one_crypto_for_the_rest_of_your_life/)). Thank you all for spreading awareness.

Monde PR's achievements for April:

- created/pitched 2 stories to finance and crypto publications
- secured 2 media interviews
- responded to 1 request for comment

News coverage secured by Monde PR:

- the Decred treasury announcement was covered by [Bankless Times](https://www.banklesstimes.com/2021/04/12/decred-makes-consensus-change-to-further-decentralize-128m-treasury/)
- an interview with @lukebp on the [Keyword: Crypto podcast](https://www.keywordcrypto.com/luke-p-from-decred/)

## Events

Attended:

- Apr 21 - [Blockchain Land](https://blockchainland.talent-republic.tv/) - Internet. @adcade talked about "[Opinions](https://blockchainland.talent-republic.tv/on-demand/que-opinar-sobre-las-criptomonedas/) on cryptocurrencies" and the [future](https://blockchainland.talent-republic.tv/on-demand/blockchains-futuro-escalabilidad-u-oportunismo/) of crypto as part of Decred participation in Blockchain Land by Talent Land. The panels were streamed in [virtual worlds](https://es.cointelegraph.com/news/first-massive-spanish-speaking-blockchain-event-created-by-decentraland-and-cryptovoxels) Decentraland and Cryptovoxels.

## Media

Selected articles:

- Decred makes consensus change to further decentralize $128M treasury ([banklesstimes.com](https://www.banklesstimes.com/2021/04/12/decred-makes-consensus-change-to-further-decentralize-128m-treasury/))
- What is Decred and DCR? by Ivan on Tech ([ivanontech.com](https://academy.ivanontech.com/blog/what-is-decred-and-dcr))
- Q1'21 currency sector review by Mira Christanto ([messari.io](https://messari.io/article/q1-21-currency-sector-review)) - Messari [tweeted](https://twitter.com/MessariCrypto/status/1381654632515174402) that DCR is second biggest mover after DOGE in Q1 2021

Videos:

- Luke Powell interview Decred in Depth (live) by @elima\_iii ([youtube](https://www.youtube.com/watch?v=J6IAjmwkki0))
- Decred Society interview Decred in Depth (live) @elima\_iii ([youtube](https://www.youtube.com/watch?v=WOVUvzsp3Eo))
- Decred's proposal platform Politeia: The decision-making force behind the ~$125M Decred DAO by @Exitus ([youtube](https://www.youtube.com/watch?v=dfpUgwXBUmM))
- The evolution of money - Decred fundamentals by @phoenixgreen ([youtube](https://www.youtube.com/watch?v=1qadfuFuqzs))
- Interoperability for digital cash by @phoenixgreen ([youtube](https://www.youtube.com/watch?v=iBN0ZzlEKMA))
- Decred Price Analysis - 27th April 2021 by Josh Olszewicz of Brave New Coin ([youtube](https://www.youtube.com/watch?v=NfSp5IjPtAI))

@karamble has mirrored all Decred YouTube [channel](https://www.youtube.com/decredchannel) videos at [tube.decredcommunity.org](https://tube.decredcommunity.org/). It is powered by [PeerTube](https://joinpeertube.org/) - an open-source, self-hosted, lightweight alternative to YouTube that can connect to the [Fediverse](https://en.wikipedia.org/wiki/Fediverse). [Here](https://docs.joinpeertube.org/use-third-party-application) is a list of tools for regular users. Admins running PeerTube instances can help to make the content even more resilient by setting up [following and redundancy](https://docs.joinpeertube.org/admin-following-instances).

Audio:

- Rough Consensus 18: Bull market blues - Checkmate, Permabull Nino & Mister Black ([libsyn](https://roughconsensus.libsyn.com/episode-18-bull-market-blues), [spotify](https://open.spotify.com/episode/0E7k86gme05YINpdBlVPqy))
- Keyword: Crypto Podcast - Luke P. from Decred ([youtube](https://www.youtube.com/watch?v=pRJ1zJFVoFo), [keywordcrypto.com](https://www.keywordcrypto.com/luke-p-from-decred/))

Translations:

- Decred Blockchain Analysis - Part 2 PoW wow - [in Spanish](https://medium.com/decred-es/an%C3%A1lisis-de-la-blockchain-de-decred-pt-2-pow-wow-376aab0be23c) by @francov\_
- Decred Journal March 2021 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), and Spanish (@francov\_). Thank you all!

Other non-English content:

- @Dominic talked to Mable Jiang on 51% Podcast episode 20 titled "On Decred's Hybrid Consensus and Collective Wisdom", hosted by Multicoin Capital ([apple](https://podcasts.apple.com/cn/podcast/51-with-mable-jiang-presented-by-multicoin-capital/id1540917284?l=en&i=1000515571194), [simplecast.com](https://51-with-mable-jiang-presented-by-multicoin-capital.simplecast.com/episodes/ep20-cn-dt-decred))

## Community Discussions

Comm systems news:

- a new flavor of scammers are DMing people as they join #support. Please be warned, no admins or devs will ever DM you, or ask you for money!

Selected Reddit posts:

- [r/decred](https://www.reddit.com/r/decred/new/) now has weekly Trader Talk Thursdays and Many Musings Mondays to host content that would otherwise be removed as duplicate price talks or off-topic
- a marketing idea to run Decred-funded [mail service](https://www.reddit.com/r/decred/comments/n11zwu/decredmail_a_marketing_idea/)

Selected Twitter discussions:

- @lukebp clears up what a [DAO](https://twitter.com/lukebp_/status/1378381506947784706) is
- @overthrowy shared his Decred [investment deck](https://twitter.com/overthrowy/status/1381097293122740225)

> For people who believe that "the market" makes the best decisions, Bitcoin may be the right choice. During any contentious change, the network may split into two or more forks that will compete (fight) for the financial and social support of PoW miners, developers, investors, and exchanges.
> 
> For people who believe in collaboration, who aspire to pursue the common good, and who are willing to align themselves behind the general will of the decentralized voter collective, Decred may be the right choice.
> 
> Bitcoin and Decred are different social contracts. _They can coexist._ ([@overthrowy](https://twitter.com/overthrowy/status/1381104927108296707))

## Markets

In April DCR was trading between USD 169.50-243.70 / BTC 0.0031-0.0040. The average daily rate was $198.60.

## Relevant External

The Fei "stablecoin" was [launched](https://www.coindesk.com/1b-fei-stablecoins-rocky-start-is-a-wake-up-call-for-defi-investors) in early April but defied expectations by trading at significantly lower than the target of $1. This left many investors in a position where they were unable to exit their FEI position without taking heavy losses, due to the complex and unpredictable behavior of the novel incentive and burn mechanisms. FEI did eventually [attain](https://www.coindesk.com/1b-stablecoin-fei-hits-price-target-for-first-time-a-month-after-launch) its $1 target after about 1 month after launch.

The Yearn Finance community have been discussing [YIP-61](https://gov.yearn.finance/t/yip-61-governance-2-0/10460/25) "Governance 2.0", which extends the multisig arrangement put in place temporarily by YIP-41, and [approving](https://snapshot.org/#/ybaby.eth/proposal/QmSMyYeKrRpnA7Xn56o2NtbCUzxmhzCupL7LxMA1reXxq4) it with 99.97% yes votes. This proposal also delegates certain powers to a set of Yearn contributor teams ("yTeams"), and "clarifies" the role of YFI holders as being primarily about delegating powers to these teams and approving YIPs.

The NFT sub-community is crowdfunding its own new media platform ([NFTs WTF](https://nfts.wtf)), via the mechanism of selling 100 NFTs that confer voting rights in a DAO that will support the platform. It is interesting to note that the [post](https://nfts.wtf/crowdfunding-the-worlds-first-d-zine/) announcing the first phase of the crowdsale, in which 51 of the 100 controlling tokens were sold, only 3 were sold to Venture Capitalists, and only as individuals and not representatives of their organizations.

Coinbase started [selling](https://uk.finance.yahoo.com/news/coinbase-direct-listing-stock-cryptocurrency-bitcoin-172655492.html) shares on the Nasdaq, unlike an IPO this did not involve creating new shares but instead the existing shareholders bringing some of theirs to market.

That's all for April. Submit your stories [here](https://github.com/xaur/decred-news/labels/next%20release) or simply share your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback). We're always looking for [contributors](https://github.com/xaur/decred-news/blob/docs/contributing.md) to improve DJ!

## About

This is issue 37 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, richardred
- reviews and feedback: chappjc, davecgh, jholdstock, lukebp
- title image: saender
- funding: Decred stakeholders
