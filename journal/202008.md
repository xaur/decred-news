# Decred Journal – August 2020

![abstract art](../img/journal-202008-384.png)

_Image: Bidirectional by @saender_

Highlights for August:

- A v1.5.2 patch was released to fix a potential denial of service vector.
- Team dcrdex is up to 6 active members, and they must be burning through keyboards with over 50 PRs merged in the month, clearing up bugs and edge cases as these are revealed by testing.
- Review of the epic Treasury decentralization PR has concluded and the finishing touches are being applied.
- vspd has been receiving some polish and work has now moved on to Decrediton and dcrwallet integrations.
- The key elements for Politeia's switch to tlog are now in place, once some refactoring to accommodate these is completed, testing will begin.

## v1.5.2 Patch Release

This release closes a potential denial of service vector. People running their own nodes as well as Proof-of-Work miners are advised to upgrade.

New binaries for dcrd and Decrediton are available [here](https://github.com/decred/decred-binaries/releases/tag/v1.5.2). Make sure to [verify them](https://docs.decred.org/advanced/verifying-binaries/) - the instructions are more detailed and friendly now.

On Sep 10 it was [disclosed](https://invdos.net/) that the vulnerability is [CVE-2018-17145](https://nvd.nist.gov/vuln/detail/CVE-2018-17145). It was reported to Decred team on Jul 7 and patched Jul 8. The v1.5.2 binary release came out on Aug 27.

As of Sep 10, more than 20% of nodes have upgraded according to [dcr.farm](https://charts.dcr.farm/d/000000014/nodes).

## Development

Unless otherwise noted, the work reported here has the "merged to master" status. It means that the work is completed, reviewed, and integrated into the source code that advanced users can build and run, but is not yet available in release binaries for regular users. 

Speaking of building from source, changes in v1.5.2 were actually backported from an earlier [fix](https://github.com/decred/dcrd/pull/2253) on the master branch. It means that people building from source received it 1.5 months in advance of the binary release. If you would like to try it a new detailed and gentle [walkthrough](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c) by @kozel is available to help.

> by compiling your Decred software from source you can make use of code upgrades, bug fixes, and, amongst others, @davecgh's epic performance optimisations the moment they come out, without having to wait for an official release that they will be featured in. (...) this is as cutting-edge as it gets.

[dcrd](https://github.com/decred/dcrd):

- several historical [release notes](https://github.com/decred/dcrd/pull/2314) added to the repository. Compared to using GitHub's Release pages only, this better protects these documents from loss, reduces dependency on GitHub, and allows people to contribute improvements in a standard workflow.
- added [simnet](https://github.com/decred/dcrd/pull/2315) environment documentation and setup script. This increases developer productivity when testing and also facilitates writing reproducible bug reports using a common setup.
- introduced [contrib](https://github.com/decred/dcrd/pull/2317) directory to house optional tools which may be useful when working with dcrd and related software. Currently, this includes operating system service configurations and the new simnet setup script.
- added a database [migration](https://github.com/decred/dcrd/pull/2321) to remove block index data that is no longer needed after all the recent optimizations. This results in ~19.5% less memory used by dcrd.
- [limited](https://github.com/decred/dcrd/pull/2337) the amount of [data](https://github.com/decred/dcrd/pull/2338) read from seeder response
- the build was updated to Go 1.15 which brings substantial linker improvements that result in ~5% smaller binaries
- improved documentation and test coverage

Notably, the handling of `notfound` messages that triggered the v1.5.2 release was quickly [backported](https://github.com/btcsuite/btcd/pull/1603) to btcd and was part of its August [release](https://github.com/btcsuite/btcd/releases/tag/v0.21.0-beta).

In progress:

- The majority of time has been spent on the [decentralized treasury](https://github.com/decred/dcrd/pull/2170) work and the [passing](https://twitter.com/marco_peereboom/status/1296908604243611655) of all tests was achieved.

[dcrwallet](https://github.com/decred/dcrwallet):

- implemented basic VSP v3 (vspd) [infrastructure](https://github.com/decred/dcrwallet/pull/1785)
- added discovery of [mix accounts](https://github.com/decred/dcrwallet/pull/1773) to restore wallets with CoinJoin transactions
- added optional [account](https://github.com/decred/dcrwallet/pull/1787) parameter to the `listlockunspent` command (originally requested by dcrdex, but it is useful in general too)
- [allow](https://github.com/decred/dcrwallet/pull/1807) wallets to be created from standard input (useful for automated testing, this has helped multiple other projects)
- optimized [database](https://github.com/decred/dcrwallet/pull/1817) layout for faster access and less reads/writes
- limited the amount of [data](https://github.com/decred/dcrwallet/pull/1826) read from seeder response and the [duration](https://github.com/decred/dcrwallet/pull/1824) of the call
- [fixed](https://github.com/decred/dcrwallet/pull/1806) a bug where `listunspent` was reporting stake outputs even when they were locked

[Decrediton](https://github.com/decred/decrediton):

- added support for running LN wallet with the base wallet in [SPV mode](https://github.com/decred/decrediton/pull/2629) and enabled SPV by default
- added support for restoring wallets with [mixed accounts](https://github.com/decred/decrediton/pull/2565)
- [restored](https://github.com/decred/decrediton/pull/2604) refactored legacy code to support both old and new staking models
- continued upgrading to using functional components, custom hooks, and CSS modules
- added first [automated tests](https://github.com/decred/decrediton/pull/2606) for the sidebar component
- numerous bug fixes

There have been many questions about staking with hardware wallets. @jz [summarized](https://www.reddit.com/r/decred/comments/imbv74/staking_decred_with_ledger/) the recent developments as of Sep 4:

- @JoeGruff has ticket purchasing with Trezor [working](https://matrix.to/#/!frQxfmcoOmtseMqzby:decred.org/$D02jsxFbrVDCXsdbMx71fy6wluJfIaw-en-GwEAyj9E) on simnet with Decrediton and a PR to their firmware repo is forthcoming.
- Before that's usable by regular people the firmware changes will need to be reviewed and merged upstream by the Trezor people.
- As far as I know nobody is working on Ledger support right now, that may get tackled after Trezor is complete.
- It's unreasonable to expect that staking will ever be supported in Ledger Live (their software wallet), as it would require a large commitment on their part, it's not something we can do for them.

[Politeia](https://github.com/decred/politeia):

- backend support for [TOTP](https://github.com/decred/politeia/pull/1210) (time-based codes for 2FA)
- improved handling of [reconnection](https://github.com/decred/politeia/pull/1274) to dcrdata in Politeia and [CMS](https://github.com/decred/politeia/pull/1232)
- RFP proposal fetching [optimized](https://github.com/decred/politeiagui/pull/2084) with finite state machines
- numerous bugfixes

The Contractor Management System (CMS) is steadily developing to improve accountability and spending efficiency:

- UI for [reviewing](https://github.com/decred/politeiagui/pull/2051) same domain invoices
- added new contractor [type](https://github.com/decred/politeia/pull/1276) for those who have been approved by a proposal but not a DCC, and a rule that such contractors cannot see domain invoices
- added a [limit](https://github.com/decred/politeia/pull/1275) where contractors of same domain can only see each other's 6 past months of invoices
- removed the use of [cache](https://github.com/decred/politeia/pull/1282) to prepare for tlog migration

Progress update on tlog migration from @lukebp:

> The politeiad tlog backend and the politeiad plugins work is complete. The current focus is on refactoring politeiawww. The CockroachDB cache dependency has been removed, which was heavily relied upon by politeiawww previously, so refactoring the politeiawww routes involves what is essentially a full rewrite. We never hammered out a proper plugin architecture for the git backend, leading us to rely on the cache far too much. Now that we do have proper plugin architecture with tlog we're having to pull apart large parts of the politeiawww logic and move it into the plugin layer. Over reliance on the cache also meant not building out the politeiad API since it was faster and easier to run the same queries against the cache. All of this is now having to be addressed.
> 
> Once the politieiawww refactor is complete we can run performance tests. If performance tests go off without any issues we'll be able to put the tlog work up on testnet and start prepping for a release.

[vspd](https://github.com/decred/vspd):

- Basic HTTP [authentication](https://github.com/decred/vspd/pull/167) for admin status endpoint (used for automated monitoring)
- write a backup [after](https://github.com/decred/vspd/pull/169) closing the database, not before
- multiple smaller updates

Thanks to @isuldor ([test.stakey.net](https://test.stakey.net/)) and @sethsimmons ([vspd.realprivacy.cc](https://vspd.realprivacy.cc/)) for helping to test vspd.

Final changes for the minimum viable vspd have been merged and the next step is to complete dcrwallet and Decrediton integrations.

[dcrpool](https://github.com/decred/dcrpool):

- test harness [improvements](https://github.com/decred/dcrpool/pull/243)

[dcrlnd](https://github.com/decred/dcrlnd):

- made config options [saner](https://github.com/decred/dcrlnd/pull/107)

[dcrdex](https://github.com/decred/dcrdex):

- taker/maker contract [lock times](https://github.com/decred/dcrdex/pull/612) changed from 24/48 to 8/20 hours
- allow to [zoom out](https://github.com/decred/dcrdex/pull/573) to see more orders on the the depth chart
- added ["split"](https://github.com/decred/dcrdex/pull/562) transactions to prepare outputs of the right size. At the cost of one extra transaction, this allows the user to better control how much funds are locked and to free up funds for more orders, thus creating a healthier order book and a better user experience.
- indicate immediate [time-in-force](https://github.com/decred/dcrdex/pull/586) for user orders on markets view
- [notifications](https://github.com/decred/dcrdex/pull/537) for penalized accounts
- [asynchronous](https://github.com/decred/dcrdex/pull/565) request/notification handling and parallel new match negotiation to fix long-running client `init` and `redeem` requests and a few other issues
- [disable](https://github.com/decred/dcrdex/pull/519) account on the client side if it is not recognized by the server
- added [myorders](https://github.com/decred/dcrdex/pull/581) endpoint with some pre-computed useful information such as age of the order and amount settled
- deduplicated [websocket](https://github.com/decred/dcrdex/pull/585) code
- updated and locked down npm [dependencies](https://github.com/decred/dcrdex/pull/584)
- fixed [balance](https://github.com/decred/dcrdex/pull/548) calculation
- fixed multiple concurrency bugs
- lots of other backend and UI changes

A total of 51 PRs from 6 contributors were [merged](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-08-01..2020-08-31+sort%3Aupdated-asc), adding 19K and deleting 4K lines of code.

Thanks to everyone who [joined](https://twitter.com/stakeynet/status/1291960465904435200) the alpha testing.

[dcrandroid](https://github.com/planetdecred/dcrandroid):

- added [rebroadcast](https://github.com/planetdecred/dcrandroid/pull/495) button to pending transaction dialog
- UI tweaks and translation updates

[dcrios](https://github.com/planetdecred/dcrios):

- show ticket [reward](https://github.com/planetdecred/dcrios/pull/706) and days it took to vote on the transactions list page
- added [rebroadcast](https://github.com/planetdecred/dcrios/pull/709) button to pending transaction dialog
- added button to [switch](https://github.com/planetdecred/dcrios/pull/714) currency of the amount input field

[godcr](https://github.com/planetdecred/godcr):

- account [rename](https://github.com/planetdecred/godcr/pull/247) feature
- show [network](https://github.com/planetdecred/godcr/pull/248) in window title
- custom [editor](https://github.com/planetdecred/godcr/pull/223) with rounded corners
- bug fixes

[dcrdata](https://github.com/decred/dcrdata):

- show hashes and links for [alternative](https://github.com/decred/dcrdata/pull/1735) (sidechain) blocks on the Block page
- short URL for [Treasury](https://github.com/decred/dcrdata/pull/1752) address page
- filter to only list [unspent](https://github.com/decred/dcrdata/pull/1724) outputs on the Address page

[docs](https://github.com/decred/dcrdocs):

- [added](https://github.com/decred/dcrdocs/pull/1118) page describing LN [Watchtowers](https://docs.decred.org/lightning-network/watchtowers/)
- [reworked](https://github.com/decred/dcrdocs/pull/1120) PoS FAQ
- added info on how full node [maturation](https://github.com/decred/dcrdocs/pull/1122) can take several days before accepting inbound connections ([Configuration](https://docs.decred.org/faq/configuration/#6-why-do-i-have-no-inbound-connections-after-forwarding-the-appropriate-port) FAQ)
- added info on contractor [pay rates](https://github.com/decred/dcrdocs/pull/1123) ([Contributor Compensation](https://docs.decred.org/contributing/contributor-compensation/#pay-rates) page)
- [added](https://github.com/decred/dcrdocs/pull/1121) a page for [Mobile Wallets](https://docs.decred.org/wallets/mobile-wallets/)

[decred.org](https://github.com/decred/dcrweb):

- icon updates and bug fixes

Other:

- most projects build and test with Go [1.15](https://github.com/decred/dcrd/pull/2334), which [came out](https://golang.org/doc/go1.15) in August
- multiple developers used the [release](https://github.com/decred/release) tool to [reproduce](https://matrix.to/#/!zefvTnlxYHPKvJMThI:decred.org/$l62fxKNyrDN_RhzY93vopaCLwh0Y9aulr6j7DjbFVd0) the v1.5.2 build and computed the same manifest hash

## People

Welcome to new first time contributors with code merged to master: @hsyia ([dcrdocs](https://github.com/decred/dcrdocs/pull/1122)), @brandoncurtis ([decred-release](https://github.com/decred/decred-release/pull/173)), @isuldor ([dcrwebapi](https://github.com/decred/dcrwebapi/pull/107)), @JustinBeBoy ([dcrios](https://github.com/planetdecred/dcrios/commits?author=JustinBeBoy)).

Community stats as of Sep 1:

- Twitter followers: 40,816 (+179)
- Reddit subscribers: 9,906 (+31), online: 320
- Matrix #general users: 174 (+50) \*
- Discord users: 1,394 (+22)
- Telegram users: 2,468 (-52)
- YouTube subscribers: 4,180 (+30), views: 154K (+3K)
- LinkedIn followers: 875 (+13)
- GitHub dcrd stars: 557 (+7), forks: 246 (+6)

\* reminder: Matrix had a big "purge" [in July](202007.md#people).

Some observations from other accounts tracked by the [social-media-data](https://github.com/decredcommunity/social-media-stats) repository:

- Facebook: [decredbrasil](https://www.facebook.com/groups/decredbrasil/) 5,799 members (-36) and 57 posts in 30 days, [decredinternational](https://www.facebook.com/groups/decredinternational/) 802 members and 20 posts in 30 days
- Instagram: [decred_es](https://www.instagram.com/decred_es/) 390 followers (+15), [decredbr](https://www.instagram.com/decredbr/) 767 followers (+50), [decredproject](https://www.instagram.com/decredproject/) 578 followers (+2). Unlike the other two, English account has no active maintainer (_hint_).
- Twitter: [DecredArabia](https://twitter.com/DecredArabia) 218 followers (+5), [DecredAustralia](https://twitter.com/DecredAustralia) 436 followers, [Decred_BR](https://twitter.com/Decred_BR) 540 followers (+13), [Decred_CA](https://twitter.com/Decred_CA) 334 followers, [Decred_ES](https://twitter.com/Decred_ES) 909 followers (+49), [Decred_PL](https://twitter.com/Decred_PL) 226 followers (+3)
- YouTube: [Decred Arabia](https://www.youtube.com/channel/UCCtB2BfsA2VdT0FJXpsYICA) 29 subscribers and 0.6K views, [Decred Brasil](https://www.youtube.com/channel/UC73wa2ddXuPWsmenVfeFTYg) 369 subscribers (+108) and 13K views (+4K), [Decred en Español](https://www.youtube.com/channel/UCCprOo4gR1vsjJTAzv8BMBQ) 74 subscribers (+28) and 1.3K views (+0.4K)
- #planetdecred Matrix room at the planetdecred.org homeserver has 151 users

## Governance

In August the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 12,961 DCR and spent 10,787 DCR. Using August's daily average DCR/USD rate of $17.02, this is $221K received and $184K spent. At July's average daily rate of $15.13, the USD figure billed for work completed in that month is $163K. As of Sep 6, Treasury balance is 634,747 DCR (8.5 million USD at $13.37).

New and concluded proposals:

- [proposal](https://proposals.decred.org/proposals/1dc1571) for design domain funding to cover 6 months of work in subdomains for UI/UX ($35K), Identity ($16K), and Visual Comms ($14K) - was approved with 80% yes votes and 25% turnout
- [proposal](https://proposals.decred.org/proposals/32cba00) to continue paying the moderators of Politeia, Matrix, Discord, and Telegram (max $9K over 6 months) was approved with 73% yes votes and a voter turnout of 29%
- [proposal](https://proposals.decred.org/proposals/2dcbc3e) to pay $50K for integration and promotional campaigns on two travel booking sites was rejected with 15% approval and a voter turnout of 24%
- a new [proposal](https://proposals.decred.org/proposals/1e55a41) for video production from @Exitus was published in early September
- early September also saw the first RFP [proposal](https://proposals.decred.org/proposals/91becea) published, it aims to change the messaging on decred.org and is inviting proposals for which changes to make

Four proposals have been abandoned: [augmented reality posters](https://proposals.decred.org/proposals/dedf452), [marketing by @fst_nml](https://proposals.decred.org/proposals/3372cfc), [social media memes](https://proposals.decred.org/proposals/4f81031) and [Decred poker series](https://proposals.decred.org/proposals/7a67ed5) (@darthcrypto plans to return with a more developed proposal).

@pavel shared a [screenshot](https://twitter.com/_Checkmatey_/status/1295858198260248576) and an update on the development of the [Decred OnChain](https://proposals.decred.org/proposals/0230918) website:

> Chart subpages are almost done. From UX/UI perspective, we are working on homepage. I would say we are ±75% done. ([chat](https://matrix.to/#/!qYpAAClAYrHaUIGkLs:decred.org/$3FcfGt9YIOR81fM5CnqEFib4d7HYJPqGe_2oE3Q4JL4?via=decred.org&via=matrix.org&via=planetdecred.org))

Pre-proposals:

- @kozel is shepherding a [pre-proposal](https://www.reddit.com/r/decred/comments/igfqjc/decred_content_and_asset_translation_proposal_an/) for content translation
- @lewildbeast is gathering feedback on a [pre-proposal](https://github.com/decredcommunity/proposals/pull/6) to offer awards to developers and researchers who pioneered new technology that Decred benefits from (e.g. HD wallets)

@bee is testing GitHub-based "proposal drafting infrastructure" that allows multiple people to edit the draft, get feedback and formatting help, track revisions, and post comments. Keeping drafts in a well-known place makes them discoverable and allows to save any progress for others to pick up even if the original author stops developing the proposal. Currently @lewildbeast's [awards](https://github.com/decredcommunity/proposals/pull/6) and @elian's [BTCPay](https://github.com/decredcommunity/proposals/pull/7) integration pre-proposals are hosted. To use this, submit a pull request to [proposals](https://github.com/decredcommunity/proposals/pulls) repo or ping @bee in [Matrix](https://decred.org/matrix/) #proposals room.

Check Politeia Digest [issue 34](https://blockcommons.red/politeia-digest/issue034/) and [issue 35](https://blockcommons.red/politeia-digest/issue035/) for a more detailed review of the governance activity.

## Network

Hashrate: [August's hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kd8zvp86-kek04pzi&scale=linear&bin=block&axis=time) opened at ~313 Ph/s and closed ~486 Ph/s, bottoming at 248 Ph/s and peaking at 557 Ph/s throughout the month. Pool [hashrate distribution](https://dcrstats.com/pow) as of Sep 1: UUPool 39%, Poolin 30%, lab.antpool.com 9%, BTC.com 2.3%, Luxor 0.8%, F2Pool 0.6%, BeePool 0.09%, CoinMine 0.03%, Suprnova 0.02% and others ~19%.

Staking: [30-day average](https://dcrstats.com/) ticket price was 151.4 DCR (+7.1). The [price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kd8zvp86-kek04pzi&axis=time&visibility=true-false&mode=stepped) varied between 141.2-168.1 DCR. [Locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kd8zvp86-kek04pzi&bin=block&axis=time) was 5.82-6.09 million DCR, which corresponded to 49.11-51.03% of the available supply [participating](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kd8zvp86-kek04pzi&bin=block&axis=time) in PoS.

Ticket price hit 168.12 DCR, which is a new high since the change of the price algorithm in 2017.

Nodes: Throughout [August](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1596240000000&to=1598918400000) there was an average of 141 public listening nodes and 139 total nodes per dcr.farm (the total was ~250 before a sharp drop on Aug 10, some data might have been missed). Average version distribution for August: 41% dcrd v1.5.1, 11% dcrd v1.5.0, 7% dcrd v1.5.2, 6% dcrd v1.6 dev builds, 5% dcrd v1.5 dev and RC builds, 0.9% dcrd v1.4, 10% dcrwallet v1.5.1, 1.1% dcrwallet v1.5, 1% dcrwallet v1.4, 16% others.

Our Network [update](https://ournetwork.substack.com/p/our-network-issue-34) by @Checkmate shares observations about an average of 100K DCR mixed daily making a significant part of the on-chain volume, hashrate boost following some market recovery above the "thermocap", and changes in three Decred-specific metrics.

New [research piece](https://medium.com/@_Checkmatey_/decred-mining-market-mechanics-fd26b921dc46) by @Checkmate gives a comprehensive overview of Decred mining market mechanics. For those preferring video/audio format, a summary overview of the paper and charts is available on [YouTube](https://www.youtube.com/watch?v=TJn6qTko0Xw). A full read is highly recommended.

> Understanding the incentives, mechanics, and performance metrics of the Decred chain's largest natural seller sheds light on both market pricing, and the strength of network security. This research should provide a sound basis for interpreting the context and performance of the Decred mining market.

## Integrations

Transak [tweeted](https://twitter.com/transak_finance/status/1294322399031316480) that DCR can be bought in 32 countries via its service.

BitcoinToYou now [allows](https://twitter.com/bitcointoyou/status/1291473453812535301) to buy and sell DCR for the Brazilian fiat currency BRL. @michae2xl presented Decred in a [livestream](https://www.youtube.com/watch?v=dk_2WYZ4EDU) on their channel.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Decentralized Treasury work is making some well-deserved [noise](https://twitter.com/marco_peereboom/status/1293364590399512577) on Twitter. Thanks to all developers for posting dev updates and everyone [amplifying](https://twitter.com/_Checkmatey_/status/1293370599977361409) [them](https://twitter.com/jz_bz/status/1295447838843908098).

Decred Latam team published [second](https://www.reddit.com/r/decred/comments/i7ue8h/activities_report_decred_en_espa%C3%B1ol_proposal_2/) and [third](https://www.reddit.com/r/decred/comments/ip0uke/activities_report_3_decred_en_espa%C3%B1ol_proposal_2/) activities reports for their marketing [proposal](https://proposals.decred.org/proposals/3c02b67). All three reports are polished and archived in the [proposals](https://github.com/decredcommunity/proposals/tree/master/proposals/3c02b67/updates) knowledge base.

@michae2xl [reported](https://www.reddit.com/r/decred/comments/ijhxzn/august_report_for_brazil_proposal/) on his August activities for the Brazil marketing [proposal](https://proposals.decred.org/proposals/bc20f98) ([archived](https://github.com/decredcommunity/proposals/blob/master/proposals/bc20f98/updates/20200830.md)).

Monde PR's achievements for August:

- updated the PR Calendar with suggested pitches and story ideas for the next 6 months
- created and pitched 2 story ideas to the media
- secured two email Q&As with crypto and mainstream publications
- submitted comments from Decred spokespeople to one news story

News coverage secured by Monde PR:

- an article in [AMB Crypto](https://eng.ambcrypto.com/bitcoin-on-chain-solutions-are-punching-above-its-weight-again/) featuring commentary by @jy-p on Bitcoin scaling, syndicated to 4 news outlets including [Fintech Zoom](https://fintechzoom.com/fintech_news_bitcoin-news/bitcoin-on-chain-solutions-are-punching-above-its-weight-again/) and [Sunrise Reads](https://sunriseread.com/bitcoin-on-chain-solutions-are-punching-above-its-weight-again/109311/)
- an article in [Finance Magnates](https://www.financemagnates.com/cryptocurrency/news/are-crypto-platforms-taking-personal-data-protection-seriously-enough/) featuring commentary by @jy-p on personal data protection
- an article in [Cointelegraph](https://cointelegraph.com/news/ledger-cto-discusses-wallet-s-safety-after-multiple-security-setbacks) featuring commentary by @jy-p on Ledger's security setbacks, syndicated to 7 media outlets including [The Union Journal](https://theunionjournal.com/ledger-cto-discusses-wallets-safety-after-multiple-security-setbacks/) and [Armenian Reporter](https://www.reporter.am/ledger-cto-discusses-wallets-safety-after-multiple-security-setbacks/)

## Events

Attended:

- Aug 5 - [Governance and blockchain](https://twitter.com/BlockSummitLA/status/1291029494065778689) in Latin America - Internet. @elian joined Cristobal Pereira and Ernesto Contreras of Dash to discuss blockchain governance of Decred in comparison to Dash, mechanics of Decred Treasury, Politeia, and the proposal process. The event was announced on [Spanish Cointelegraph](https://es.cointelegraph.com/news/online-seminar-on-governance-in-the-blockchain-and-its-contributions-to-latin-america). ([video](https://www.youtube.com/watch?v=Sh3obx4Mx_0))
- Aug 8 - [Hablemos Decred 8](https://twitter.com/Decred_ES/status/1288633074050306052) - Internet. @elian and guest José Manuel Da Silva from [criptolugares.io](https://www.criptolugares.io/) talked about cryptocurrencies and commerce, particularly in Venezuela, and the prospects of adoption from a medium of exchange perspective. ([video](https://www.youtube.com/watch?v=z-6a_tgE89E))
- Aug 11 - [Decred Talk 1](https://twitter.com/Decred_BR/status/1292842513846460417) - Internet. In this first episode of the Brazilian version of Decred Talk, @michae2xl and André Horta (CEO BitcoinToYou) talked about Decred DAO and autonomous ecosystems. The event was streamed on BitcoinToYou's channel. ([video](https://www.youtube.com/watch?v=dk_2WYZ4EDU))
- Aug 17 - Decred Talk 2 - Internet. Second edition of Decred Talk was hosted on Instagram. The goal was to engage with new/unknown community members and answer their questions. ([video](https://www.instagram.com/tv/CEAenAhF7m0/))
- Aug 20 - [Hablemos Decred 9](https://twitter.com/Decred_ES/status/1294416104723488769) - Internet. @adcade and guest Mauricio Ocampo of [technolawgeek.com](https://www.technolawgeek.com/) discussed legal perspectives of cryptocurrencies. ([video](https://www.youtube.com/watch?v=VzELuWRqCo4))
- Aug 28 - [Legal status of Bitcoin](https://twitter.com/paxful_LATAM/status/1297912240511881216) - Internet. Organized by [Paxful Latam](https://twitter.com/paxful_LATAM).
- Aug 28 - [Hablemos Decred 10](https://twitter.com/Decred_ES/status/1298432664245084161) - Internet. @adcade, @elian and guest [Carlos Ramirez](https://twitter.com/Ciberagente) discussed cybersecurity, privacy and cybercrime. ([video](https://www.youtube.com/watch?v=GosMlhxWK3M))
- Aug 29 - [From laws to protocols](https://twitter.com/Decred_ES/status/1299506004607094784) - Internet. Hosted by [Students for Liberty](https://twitter.com/SFLMexico) Mexico. ([video](https://www.facebook.com/894983097182840/videos/312801089791414))
- Aug 31 - [Future of organizational structures](https://twitter.com/Decred_ES/status/1298275771333705728): Centralized vs decentralized - Internet. @elian joined a panel with John DeVadoss (Neo) and Ernesto Contreras (Dash) to discuss governance in decentralized organizations. ([video](https://www.youtube.com/watch?v=yIlVTSObIzU)) Organized by [Fintech Advisory Services](https://www.fintech-advisory.com/). ([video](https://www.youtube.com/watch?v=yIlVTSObIzU))

In other news, @eSizeDave is facilitating a webinar to help academics from the Australian RMIT university to learn about Decred as part of their research.

## Media

Selected articles:

- Decred, mining market mechanics by @Checkmate ([medium](https://medium.com/@_Checkmatey_/decred-mining-market-mechanics-fd26b921dc46))
- Utility of cryptoassets by @mm ([stakey.club](https://stakey.club/en/utility-of-cryptoassets/))
- Blockchain governance - Part 1 by @mm ([stakey.club](https://stakey.club/en/blockchain-gov-part1/))
- Our Network #34 features another Decred update from @Checkmate ([substack.com](https://ournetwork.substack.com/p/our-network-issue-34))

Translations:

- @mm's own new and old articles are available [in Portuguese](https://stakey.club/pt/articles/)
- Decred, Mining Market Mechanics - [in Spanish](https://territorioblockchain.com/decred-mecanica-del-mercado-minero/) by territorioblockchain.com
- Politeia Digest issues 33-35 - [in Arabic](https://insaf01.github.io/politeia-digest-ar/) (@arij, @abdulrahman4) and [in Spanish](https://medium.com/decred-es/politeia-digest-spanish/home) (@pablito)
- Decred Journal - July 2020 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), Portuguese (@mm) and Spanish (@francov\_). Polish May and June by @kozel are now available too. Thank you all!

In other non-English content:

- We totally missed the creation of [Decred Arabia](https://www.youtube.com/channel/UCCtB2BfsA2VdT0FJXpsYICA) YouTube channel back in [May](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$15908512441460kIGQx:decred.org) (_seriously folks, [submit your stories](https://github.com/xaur/decred-news/blob/docs/contributing.md)!_). The channel now has 7 videos: 2 original on the [history of money](https://www.youtube.com/watch?v=OFONdBbYbBc) and [history of Decred](https://www.youtube.com/watch?v=_7Ae_Klwqo0), and 5 strategic English videos with Arabic subtitles such as [How Decred is Unique](https://www.youtube.com/watch?v=N0DmpjhuD38) and [How to Stake Decred](https://www.youtube.com/watch?v=JuKw3BHO0v0). The same subtitles are also available in original English videos. Source files are [on GitHub](https://github.com/Insaf01/Decred-Videos-Ar) for collaboration and reuse. If you would like to submit your translated subtitles to Decred's videos please contact @Exitus.
- @elian was featured in Spanish Territorio Bitcoin podcast in [Feb](https://www.ivoox.com/episodio-105-entrevista-jesus-sanchez-bermejo-audios-mp3_rf_47751087_1.html) and [Jun](https://www.ivoox.com/que-es-decred-entrevista-profundidad-elian-audios-mp3_rf_52242080_1.html), which got 7K and 5K views, respectively.
- @elian was [quoted](https://es.cointelegraph.com/news/cryptology-and-marketing-the-challenges-of-organic-growth) in Spanish Cointelegraph on marketing and challenges of organic growth.

Videos:

- Decred bi-weekly news update - August 18th, 2020 by @Exitus ([youtube](https://www.youtube.com/watch?v=hjOi4sfvdNU))
- Top 5 bullish signals for Decred by LiteLiger ([youtube](https://www.youtube.com/watch?v=186jzRRJ-80))
- Mining market mechanics - Decred research read-through by @Checkmate ([youtube](https://www.youtube.com/watch?v=TJn6qTko0Xw))
- Did you know Decred has Governance by Decred Society ([youtube](https://www.youtube.com/watch?v=1BNW60RE0rQ)) - a quick overview of the Politeia proposal process

Audio:

- Staked Podcast Episode 0.0. "It [took](https://twitter.com/elima_iii/status/1299306383146471426) me over a year to build up the bravery to do this". Congrats to Eduardo for launching the podcast! ([anchor.fm](https://anchor.fm/staked-podcast/episodes/Staked-Podcast-Episode-0-0-eimmd6/a-a31v0tg), [tweet](https://twitter.com/stakedpodcast/status/1299305564258938880))
- Rough Consensus 10. In this episode, the spidermen are joined by @notsofast - a cryptocurrency OG with wide ranging expertise, and pick his brain surrounding: Bitcoin vs altcoins, why Decred, mining, investment/trading approach, and much more. ([libsyn](https://roughconsensus.libsyn.com/episode-10-bitcoin-decred-altcoins-with-notsofast))

Even though the memes [proposal](https://proposals.decred.org/proposals/4f81031) was abandoned, people started generating memes independently:

- [contributing](https://twitter.com/coveryfire7777/status/1292966872560918529) to the DAO
- [attacking](https://twitter.com/coveryfire7777/status/1293719678985146369) Decred
- [strong doge](https://twitter.com/coveryfire7777/status/1293984002349699072)
- [attack cost](https://twitter.com/svitekpavel/status/1289793785669484544)
- Decred chilling with some [features](https://twitter.com/lukebp_/status/1292622538560872448) while Bitcoin and Ethereum wrestle

## Community Discussions

Selected Reddit posts:

- newcomer [wonders](https://www.reddit.com/r/decred/comments/i5jcjp/dcrdex_seems_like_the_greatest_thing_ever_why_is/) why the wider crypto community is not paying attention to DCRDEX
- [question](https://www.reddit.com/r/decred/comments/i9ufxy/decred_team_and_treasury_fund_management/) about Treasury fund management had several in depth answers
- Jul 31 Forward Thinking Friday focused on [Contrarian Messaging](https://www.reddit.com/r/decred/comments/i1gumi/forward_thinking_friday_contrarian_messaging_31/) where @Checkmate suggested two potential areas for Decred marketing to rally around, "Decred is Ready" and "Own the Name, Decentralised Credits, in the face of 'De'Fi"
- Aug 7 [Forward](https://www.reddit.com/r/decred/comments/i5cy0y/forward_thinking_friday_7_aug_2020/) Thinking Friday mostly concerned marketing ideas, and it's where the idea to reward Bitcoin developers who produced work that is useful to Decred was first discussed
- Aug 14 Forward [Thinking](https://www.reddit.com/r/decred/comments/i9w54z/forward_thinking_friday_14_aug_2020/) Friday's top comment was about building private DAEs on Decred
- Aug 28 Forward Thinking [Friday](https://www.reddit.com/r/decred/comments/iip7ap/forward_thinking_friday_28_aug_2020/)'s top comment was about creating a crypto index using DCRDEX

Selected Twitter discussions:

- Reluctant Raccoon just cannot find that "DeFi governance token" [satisfaction](https://twitter.com/ypical_/status/1292439057168060416) anywhere outside Decred
- @DecredSociety [noted](https://twitter.com/DecredSociety/status/1292039718679580673) Decred's "market maturity" component of the FCAS rating is down, but overall the project is still A-grade
- @degeri [reminds](https://twitter.com/degeri_crypto/status/1293729682584674304) that Decred is always hiring (and tagging some company that was "restructured" recently)
- @CATO\_io [explored](https://twitter.com/CATO_io/status/1299756617722925056) how Decred's ethics and risk-sharing lead to a more robust system. Good example of creative outreach that exposes new sides of the project.

## Markets

In August DCR was trading between USD 15.25-23.49 / BTC 0.00134-0.00202. The average daily rate was $17.02.

After hitting a new high of ~$12,100 on Aug 2, BTC/USD crashed to $10,550 within minutes and triggered a spectacular liquidation of more than $1 billion worth of futures. ZeroHedge [wrote](https://www.zerohedge.com/markets/bitcoin-hits-1-year-high-then-plummets-after-someone-liquidates-1-billion-seconds-hammer) that price manipulation is likely since it's not in the best interest of the seller to "take out the entire bidstack in one transaction".

In a Twitter convo, @Checkmate shared his [model](https://twitter.com/_Checkmatey_/status/1293652411316281344) where DCR's bear market was hugely affected by compulsory selling by ASIC miners that invested in hardware at the peak bull market.

## Relevant External

Bitcoin Cash is warming up for another community splitting hard fork. The developers of the BitcoinABC client [announced](https://www.bitcoinabc.org/2020-08-24-celebrating-bchd-slp/) that the next bi-annual hard fork on Nov 15 will add a requirement that a portion of each block reward goes to an address controlled by the developers. Roger Ver and others have [tweeted](https://twitter.com/rogerkver/status/1300908197113458688) this is not acceptable and they won't be joining the fork.

Ethereum Classic has suffered [another](https://cryptobriefing.com/after-second-double-spend-attack-ethereum-classics-future-is-question/) [two](https://www.coindesk.com/ethereum-classic-attacker-successfully-double-spends-1-68m-in-second-attack-report) double spend reorg attacks, with the attacker gaining $5.6 million from the first attack, which was executed with $204,000 worth of rented hashpower. The attacks reorged so many blocks that some implementations ignored them and the network [partitioned](https://blog.coinbase.com/coinbases-perspective-on-the-recent-ethereum-classic-etc-double-spend-incidents-1fd19ef215f3).

Charles Hoskinson of IOHK and Cardano has [proposed](https://cointelegraph.com/news/charles-hoskinson-s-iohk-submitted-a-decentralized-treasury-proposal-to-the-ethereum-classic-community) two ECIPs for ETC, one to add checkpointing which would stop the long reorgs, and a second to add a development fund which receives 20% of block rewards. The block reward proposal seems highly controversial in the community, with ETC labs rejecting the idea.

The YAM token and protocol was [born](https://medium.com/@yamfinance/yam-finance-d0ad577250c7) and [died](https://coingeek.com/defi-strikes-again-yam-protocol-bug-leads-to-750000-loss/) in August, its cycle lasted for about 3 days, which is fast even for DeFi. The token was billed as a "governance token" for the YAM protocol, but as soon as the system started it became clear it was fundamentally broken. There was a short window where YAM farmers were mobilized to act and save the protocol but there was a bug in the solution as well so it's dead now. YAM was covered in disclaimers about being experimental, unaudited, and was produced in a 10 day period by smashing other smart contracts together - one hour after launch, $76 million was invested, rising to $300 million the next day before the fatal flaw was announced.

MakerDAO activated an executive "spell" contract which was supposed to raise the ceiling for WBTC but [instead](https://twitter.com/nanexcool/status/1292287024767082496) set it to zero. It seems no harm was done on this occasion other than delaying the availability of more WBTC.

Zcash Foundation is [selecting](https://decrypt.co/39105/a-five-member-board-to-control-36-million-treasury-for-zcash) a 5 member board to control the share of block reward funding which it is due to begin receiving. The board will be selected by votes of the Community Advisory Panel, which currently has 62 members, but each member can now invite one additional member.

Coinbase CEO [confirmed](https://www.theblockcrypto.com/linked/76588/coinbase-ceo-interview-token-service) that the company is developing a platform to join in the initial exchange offering (IEO) business, provisionally titled Coinbase Launch.

Cryptocurrency adoption is most widespread in Nigeria and Vietnam according to Statista Global [Consumer Survey](https://www.zerohedge.com/crypto/youll-never-guess-which-country-has-most-widespread-adoption-crypto-world).

The fintech company Plaid (as [used by](https://enegnei.github.io/This-Month-In-Bitcoin-Privacy/July_2020/#july-1st---class-action-lawsuit-against-plaid-inc) Coinbase, Gemini, and others) has been hit with a $5M+ class action [lawsuit](https://www.natlawreview.com/article/fintech-startup-plaid-inc-hit-5m-class-action-lawsuit).

> 1\. Imagine there is a company that knows every dollar you deposit or withdraw, every dollar you charge or pay to your credit card, and every dollar you put away for retirement, within hours after you make the transaction. Imagine this includes every book or movie ticket or meal you purchase, every bill you pay to a doctor or hospital, and every payment you make (or miss) on your mortgage, student loan or credit card bill. Imagine this company maintains a file on you containing all of this information going back five years. Imagine that this company uses your username and password to log into the online account you maintain with your bank and updates that file multiple times a day to stay up to date on every financial move you make.
> 
> 2\. Imagine this company is not your bank. Imagine that, as far as you know, you never provided your username and password to this company or otherwise authorized it to access your online accounts. Imagine you never heard of this company at all.

Imagine someone got a hold of their database and used it to identify cryptocurrency holders.

Top cryptocurrency exchanges are [drafting](https://www.coindesk.com/crypto-exchange-group-eyes-bulletin-board-system-for-fatf-compliance-coinbase-exec) a white paper on sharing customer data to comply with FATF's "travel route" requirements.

Class action [lawsuit](https://cointelegraph.com/news/600m-crypto-ad-ban-class-action-filed-in-australian-courts) against Google and Facebook was filed in Australia. Tech giants are accused of anti-competitive behavior for banning crypto ads in 2018, which allegedly killed the ICO market, damaging the wider crypto industry while not efficiently blocking impersonation scams.

A bipartisan group of members of US Congress have [written](https://www.coincenter.org/congress-to-irs-proof-of-stake-block-rewards-should-not-be-taxed-as-income/) to the IRS to urge a clarification on how PoS rewards are treated for tax purposes - and asking that these be treated not as income but as a good produced by the validator, to be taxed when it is sold.

The United States Postal Service [filed]( https://www.zerohedge.com/crypto/usps-just-filed-patent-blockchain-based-secure-voting-system) a patent for a blockchain-based secure voting system.

## About This Issue

This is issue 29 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

You can submit a story [here](https://github.com/xaur/decred-news/labels/next%20release) to be considered for the next release. [Feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, lukebp, richardred
- reviews and feedback: davecgh, jholdstock, jrick, jz, Exitus, michae2xl
- title image: saender
