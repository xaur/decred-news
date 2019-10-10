# Decred Journal – September 2019

![abstract art](../img/journal-201909-384.jpg)

_Image: On-Chain Seasonality by @saender_

* The family of Decred projects was joined by new stratum PoW mining pool software, dcrpool. High quality open source pool software is rare, and the need for such software is a barrier to starting a new mining pool. dcrpool fills this gap, levelling the playing field so that anyone can start their private or public mining pool. This should benefit the decentralization of PoW mining power by curtailing the economies of scale that favor large pools.
* dcrstakepool v1.2.0 is out. This release is the culmination of development work that began in September 2017 and brings a number of enhancements, including a proper interface for admins to handle tickets purchased with insufficient fees, an overhauled front-end design, security enhancements, updated terminology, reduced dependencies on third parties, and various bug fixes.
* September has been a big month for integrations, with DCR support being added to Trust Wallet, Exodus mobile wallet, Joule Chrome extension for paying with LN, among other services.

## Development

[dcrd](https://github.com/decred/dcrd): Version 2 compact filters have been [implemented](https://github.com/decred/dcrd/pull/1856). These use less space than v1 filters, which will be an improvement for light clients (SPV). Also, v2 filters will be used in [block header commitments](https://proposals.decred.org/proposals/0a1ff846ec271184ea4e3a921a3ccd8d478f69948b984445ee1852f272d54c58).

The `mempool` module [received](https://github.com/decred/dcrd/pull/1901) finer grained error codes. A bunch of old mining-related code was removed, including the [removal](https://github.com/decred/dcrd/pull/1736) of `getblocktemplate` in favor of `getwork`.

Multiple smaller changes for refactoring, improved test coverage and documentation, and bug fixes.

[dcrwallet](https://github.com/decred/dcrwallet): dcrwallet's Go code now uses `decred.org` instead of `github.com` in its module name. The idea to adopt this more widely to reduce dependence on GitHub is discussed [here](https://github.com/decred/dcrd/issues/1264).

Build support was added for Go 1.13 and dropped for 1.11.

Work continues on integrating [CoinShuffle++ support](https://github.com/decred/dcrwallet/pull/1541).

[Decrediton](https://github.com/decred/decrediton): Account view received incremental [improvements](https://github.com/decred/decrediton/pull/2178), while Security view gained the display of [derivation](https://github.com/decred/decrediton/pull/2184) info for addresses owned by the wallet (useful for debugging purposes).

Lightning Network integration is [nearing completion](https://github.com/decred/decrediton/pull/2107). Work continues to [refactor startup](https://github.com/decred/decrediton/pull/2182) to a finite state machine in order to make it more robust.

[Politeia](https://github.com/decred/politeia): Politeia's redesign is live on [testnet](https://test-proposals.decred.org/) and testing/feedback is welcome.

Significant progress is being made on the CMS, with the DCC Proposal System [foundation](https://github.com/decred/politeia/pull/980) and [functionality](https://github.com/decred/politeia/pull/981) for contractors to interact with it being merged along with a range of smaller improvements and bug fixes for both CMS and proposals site. Upcoming priorities on the proposals site are [RFP proposals](https://github.com/decred/politeia/issues/966) and [Trillian](https://github.com/google/trillian) integration which will allow for timestamping of individual pieces of content.

[dcrstakepool](https://github.com/decred/dcrstakepool): Major v1.2 release has landed on master.

A new admin-only page for handling low-fee tickets has been added to the front-end. This page will list all tickets which have been purchased with an insufficient fee, and allow the admin to manually add or remove those tickets from the list of eligible voting tickets. Previously this operation had to be performed manually by directly manipulating the database.

A new front-end design brings dcrstakepool up to the professional standard seen in other Decred software such as Decrediton.

Requested by VSP operators, support for encrypted SMTP connections has been implemented, including support for self-signed certificates. This allows VSPs to protect registration and account recovery emails in transit with SMTPS.

All communication with dcrwallet now goes through stakepoold. This architectural change lowers the number of RPC calls going over the network, decreases code complexity and allows ports between dcrstakepool and dcrwallet to be closed.

A custom MySQL data store has replaced the file-based storage solution for storing session cookies. This addresses several known security issues related to session data.

Google's reCAPTCHA has been replaced with a self-hosted solution implemented [in Go](https://github.com/dchest/captcha). All resources required for it are now hosted by the VSP rather than by a third party. The front-end included in this release executes no external JavaScript at all, granting a significant boost to user security and privacy.

Several security improvements were made to prevent cross-site request forgery (CSRF) attacks, leaking of private data to third parties, malicious links and caching of sensitive information by browsers.

The release is a result of 160 pull requests from 20 contributors made since Sep 2017. For full details of the release, see [release notes](https://github.com/decred/dcrstakepool/releases/tag/v1.2.0).

[dcrpool](https://github.com/decred/dcrpool): After more than a year in the making, Decred's open source mining pool is finally [released](https://twitter.com/decredproject/status/1176914732399439873) along with a blog [post](https://blog.decred.org/2019/09/25/Introducing-Dcrpool/) about it. dcrpool features:

* can operate as private or publicly available pool
* supports all relevant miners
* PPS and PPLNS payment modes
* a web UI with stats and account data
* connection details for all miners
* account work and payment analysis

Developed by @dnldd in Go, this software is an important step in decentralizing PoW mining for Decred. Congrats on the release!

[dcrlnd](https://github.com/decred/dcrlnd): The big work to port pull requests from the upstream lnd is finally [merged](https://github.com/decred/dcrlnd/pull/36).

Work has begun on enabling [remote wallet](https://github.com/decred/dcrlnd/pull/40) functionality. This allows users to use their existing wallet instead of having to manage a separate wallet with separate seed for dcrlnd. It also allows users to launch a LN wallet directly for a wallet running in Decrediton, easing the UX.

[cspp](https://github.com/decred/cspp): added [reconnection](https://github.com/decred/cspp/pull/18) support, updated setup instructions, added Go 1.13 builds, bug fixes.

[dcrdex](https://github.com/decred/dcrdex): The [foundations](https://github.com/decred/dcrdex/issues/8) are being laid out with thousands of lines of code merged in master. Initial backends for [DCR](https://github.com/decred/dcrdex/pull/17) and [BTC](https://github.com/decred/dcrdex/pull/26) have been added. The spec has undergone several minor [changes](https://github.com/decred/dcrdex/pulls?q=is%3Apr+is%3Aclosed+label%3Aspec+merged%3A2019-09-01..2019-09-30).

Unlike other software using the ISC license, dcrdex chose BlueOak. Motivation was discussed in [this chat](https://matrix.to/#/!EzTSRQITaqHuFBDFhM:decred.org/$RaxvOZy5x4cby5rwhph7gUED6LR0yQkKIihst4C5Og4).

[dcrandroid](https://github.com/decred/dcrandroid): Work on the new UI continues with an overhauled [home page](https://github.com/decred/dcrandroid/pull/401) and other improvements to bring the app into alignment with the standard app design recommendations for Android. Work has begun on [multi-wallet support](https://github.com/raedahgroup/dcrlibwallet/pull/57). This will allow users to import their public key from Decrediton so that they can monitor the status of their tickets from their phone.

[dcrios](https://github.com/raedahgroup/dcrios): Refactoring is underway to take advantage of new [tx filter methods](https://github.com/raedahgroup/dcrlibwallet/pull/48) in dcrlibwallet. This includes an overhaul of the [history page](https://github.com/raedahgroup/dcrios/pull/515), a new data [structure](https://github.com/raedahgroup/dcrios/pull/520) for storing transactions and an overhaul of the [send page](https://github.com/raedahgroup/dcrios/pull/521) to enable users to send DCR to multiple destinations simultaneously.

[Background sync](https://github.com/raedahgroup/dcrios/pull/518) was streamlined and made more reliable. This addresses an issue some users were encountering when syncing the blockchain was stopped due to the phone going to sleep.

UI optimization continues with overhaul of [home page](https://github.com/raedahgroup/dcrios/pull/512).

[docs](https://github.com/decred/dcrdocs): A page for [dcrtime](https://docs.decred.org/advanced/dcrtime/) has been [added](https://github.com/decred/dcrdocs/pull/960).

Work continues on developer documentation, which is expected to be ported from a private repo to the Decred GitHub organization soon for wider visibility.

[decred.org](https://github.com/decred/dcrweb): updated [Roadmap](https://decred.org/roadmap/), [Wallets](https://decred.org/wallets/) and [Exchanges](https://decred.org/exchanges/) pages.

Several projects have switched their continuous integration (CI) system from Travis CI to GitHub Actions. Actions are faster, better integrated, are open source and shareable, and it's overall much more flexible in terms of what it will allow.

Dev activity stats for September: 248 active PRs, 201 master commits, 28K added and 17K deleted lines spread across 15 repositories. Contributions came from 2-8 developers per repository.

## People

Welcome to new first time contributors with code merged to master: imestin ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=imestin)), Muharem Hrnjadovic ([politeia](https://github.com/decred/politeia/commits?author=al-maisan)), Amir Massarwa ([politeiagui](https://github.com/decred/politeiagui/commits?author=amassarwi)).

@s\_ben wrote a great Medium [piece](https://medium.com/@seth.benton/i-dump-coins-on-you-ee6db4331e18) on his experience of working for the Decred DAO and makes observations on liquidity, volatility, shilling and his plans for the future.

Community stats as of Oct 2:

* Politeia users: 181 (+7)
* Twitter followers: 40,578 (-19)
* Reddit subscribers: 9,631 (+37)
* Matrix users: 436 (+24)
* Slack users: 6,851 (+17)
* Discord users: 2,487 (+45), verified to post: 325 (+15)
* Telegram users: 3,048 (-100)
* YouTube subscribers: 3,830 (+11)
* Facebook followers: 3,278 (+7), likes: 3,003 (+4)
* LinkedIn followers: 622 (+19)
* GitHub dcrd stars: 517 (+1), forks: 1,394 (+11)

## Governance

In September the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 14,510 DCR and spent 7,810 DCR (note: the spend occurred in early October). Using September's daily average DCR/USD rate of $22.02, this is $320K received and $172K spent. As these payments were for work completed in August, it is also informative to consider them in the context of the August average daily rate of $26.23 - in which case the USD spent figure is $205K. As of Oct 2, Treasury balance is 641,802 DCR (11 million USD at $17.12).

i2 Trading won the competition to become Decred's designated market maker, with approval of 68% vs 49% for Tantra Labs and 47% for Grapefruit Trading. i2 also attracted higher ticket participation of 41%, compared to 36% for Tantra and 33% for Grapefruit (the turnout is now visible on [dcrdata alpha](https://alpha.dcrdata.org/proposals)).

Tantra Labs congratulated i2, published a [post](https://medium.com/@TantraLabs/proof-of-politeia-ac87f52243f4) about their experience on Politeia, and stated that they intend to continue with their plan to make DCR markets and will consult with i2 on this.

@permabullnino's [proposal](https://proposals.decred.org/proposals/f0d1bd7447182328b44c691de88cb660b63df17f1f3a94990af19acea57c09bb) for "Research & Publication of On-Chain DCRUSD & DCRBTC Indicators" was approved with 83% Yes votes and 27% turnout. Permabull will deliver 4-6 articles on the subject of the The Hyperactive HODLer's Price (HHP), over the course of around 3 months. $3,500 will be billed for Permabull's already published work and $13,000 will be billed for the new work.

The [proposal](https://proposals.decred.org/proposals/fdd68c87961549750adf29e178128210cb310294080211cf6a35792aa1bb7f63) for "DECRED Events & Meetups in the CIS in 2019-2020" was rejected with 4% Yes votes and 25% turnout.

Politeia Digest [issue 22](https://medium.com/politeia-digest/issue-22-september-1-12-2019-d82f5f617c92) has more info about these proposals. The second half of Sep has been quiet on Politeia, a new issue of Politeia Digest will be published when there are some new proposals.

## Network

Hashrate: September's hashrate opened at ~619 Ph/s and closed ~472 Ph/s, bottoming at 404 Ph/s and peaking at 679 Ph/s throughout the month. Pool hashrate distribution as of Oct 2: UUPool 21%, Poolin 19%, F2Pool 19%, lab.antpool.com 5.8%, BTC.com 2.9%, Luxor 2.12%, Coinmine 0.10%, BeePool 0.10%, suprnova 0.03% and others 30% per [dcrstats.com](https://dcrstats.com/pow). Pool distribution numbers are approximate and cannot be accurately determined.

Staking: 30-day average ticket price was 128.70 DCR (-1.35) per dcrstats.com. The price varied between 121.92-134.4 DCR. Locked amount was 5.22-5.33 million DCR, which corresponded to 49.87-51.15% of the available supply.

Nodes: Throughout [September](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1567296000000&to=1569888000000) there were around 182 listening nodes and 406 total nodes per dcr.farm. Roughly 81% run dcrd v1.4.0, 6.5% are dcrwallet v1.4.0 and 6% are v1.5.0(pre) dev builds as of Oct 4.

On average for the month of [September](https://charts.dcr.farm/d/DHPdAO4Wz/lightning-network?orgId=1&from=1567296000000&to=1569888000000) the DCR testnet LN shows 17 nodes, 35 channels and a total capacity of 227 DCR.

## Integrations

[Trust Wallet](https://trustwallet.com/), the [official](https://www.binance.com/en/blog/295063453682311168/Trust-Wallet-20-One-App-for-All-Your-Crypto) wallet for Binance, [announced](https://twitter.com/TrustWalletApp/status/1175864708961845253) the addition of Decred.

Exodus [added](https://twitter.com/exodus_io/status/1168886493617840131) Decred to its mobile wallet. This had been highly requested. In response to a question on Twitter, Exodus linked to their [position](https://support.exodus.io/article/89-is-exodus-open-source) on open source.

Decred support has been [added](https://github.com/joule-labs/joule-extension/pull/230) to [Joule](https://lightningjoule.com/), a popular Chrome extension that allows users to pay via Lightning Network and use their node as an identity on the web.

[Uphold](https://uphold.com/) exchange added [support](https://twitter.com/UpholdInc/status/1172526504837693440) for [Decred](https://twitter.com/decredproject/status/1172564615546511362) as part of their #15daysofcrypto campaign.

[StealthEX](https://stealthex.io/) has [added](https://twitter.com/StealthEX_io/status/1172201037958008837) DCR. The service offers anonymous and accountless instant exchange of crypto.

[InstaEx](https://instaex.io/) instant exchanger [added](https://twitter.com/instaex_io/status/1174367851139850241) DCR trading and submitted a [pull request](https://github.com/decred/dcrweb/pull/720) to get added on decred.org. In a short [comparison](https://medium.com/@instaex/instant-crypto-exchange-comparison-instaex-vs-changelly-vs-changenow-47770175bd54) with competitors, the service claims that no KYC or email is required, among other benefits.

Terms of both [StealthEx](https://stealthex.io/terms) and [InstaEx](https://instaex.io/) prohibit use from a range of countries.

[Tokenview](https://tokenview.com/en) has [added](https://twitter.com/tokenview2018/status/1176394157327147008) the display of Decred [blockchain data](https://dcr.tokenview.com/en) to their multi-asset block explorer.

Warning: the authors of Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Decred outreach in September focused on education and awareness regarding the recent privacy implementation. Presentations were created for [Surveying the Privacy Landscape](https://www.notion.so/Transaction-Privacy-75c4bd707c194de18ff5d943f8909e26) and [Decred Privacy](https://www.notion.so/Privacy-Keynote-4902c63379894765a545351f8fcc7d7f), and Decred community organizers across the world have presented Privacy at various meetups. @jy-p travelled to San Francisco and Los Angeles, presenting Privacy at Decred meetups in both cities, and presenting the privacy landscape to the San Francisco Bitcoin Meetup. @Dustorf published a blog, [Decred Privacy, Taking the Long Road](https://medium.com/decred/decred-privacy-taking-the-long-road-62d218223db6), contextualizing privacy from a values and development perspective.

Decred in Depth released an [episode](https://soundcloud.com/decredindepth/dcr-checkmate) featuring @Checkmate, where he delved into his research on Decred. Decred Assembly will shortly release a Deep Dive episode fetauring Decred developer @jrick, where he discussed many of the nuances of Decred's path to privacy, the implementation, and next steps.

Decred and Exodus hosted a [giveaway](https://twitter.com/decredproject/status/1171900177365569536) of Trezor Model Ts to 3 best tweets explaining why the author loves Decred. Congrats to the winners [@encldi](https://twitter.com/decredproject/status/1172577786227281920), [@OfficialCryptos](https://twitter.com/decredproject/status/1172578137948983297) and [@dcrstack](https://twitter.com/decredproject/status/1172578432343040000)!

Ditto's September achievements:

* Secured media coverage: feature on Decred's treasury in [Crypto Briefing](https://cryptobriefing.com/decred-venture-capital-centralizing/) based on interview with @richardred; interview with @jy-p on POV Crypto Podcast, the episode aptly titled "[In Search of Sovereignty](https://povcryptopod.libsyn.com/77-discovering-decred-w-jake-y-p)"; an [interview](https://open.spotify.com/show/4y3hF660v5FNPpRlg9muCC) with @lukebp in The Daily Chain podcast; Decred profile in [Blockchain Tech News](https://www.blockchaintechnews.com/articles/company-profile-decred-aims-to-deliver-decentralized-future/).
* Secured a keynote speaking slot for @jy-p at the SF Bitcoin Meetup, where he gave a presentation on the privacy landscape. There were 50+ attendees from a variety of projects. Overall a big win to have Decred speak at a Bitcoin Meetup! Jake's speech was [livestreamed](https://www.youtube.com/watch?v=LgLfMLFfOHQ?t=191). Ditto also spent quality time with @anshaw and @jy-p during their visit to San Francisco.
* Coordinated with journalists and other crypto enthusiasts in LA and SF to drive attendees to the meetups in the last week of September.
* Coordinated with the organizers of Voice of Blockchain in Chicago, where @jy-p will give not 1 but 2 presentations: one on The Decentralized Grant and Funding Process (as part of a panel with The Block), and one on Why Direct Sovereignty & Multi-Stakeholder Inclusive Governance Will Last.
* Secured two interviews with @jy-p.
* @liz\_bagot was recorded on the Decred in Depth podcast with @anshaw - episode coming soon.
* Moved the educational resources repository closer to completion.
* Coordinated with the community to continue pushing Decred's privacy narrative across Twitter.
* New Ditto team member Anastasia has joined Margaret Mei, Leslie Ankeny, and Liz Bagot on all our various Decred projects. Welcome!

## Events

Attended:

* Aug 25 - Poolin China Mining Tour - Shanghai, China. @Dominic was invited to participate in a panel discussion on PoW and delivered a keynote speech on Decred. Trivia - Poolin recently became [2nd largest](https://twitter.com/officialpoolin/status/1171451086999191557) mining pool for Bitcoin, and is contributing around [90 Ph/s](https://twitter.com/NoahPierau/status/1171527633391079424) to Decred network. ([event stats](https://twitter.com/officialpoolin/status/1166702227727310848), [photos](https://twitter.com/wanbihou/status/1166028812305321985), _missed in Aug issue_)
* Sep 4 - [Campus Party](https://brasil.campus-party.org/campus-party-goias/) - Goiânia, Brazil. Decred team members delivered a total of 5 talks about blockchain, consensus, Decred and Lightning Network. (photos: [1](https://twitter.com/Decred_BR/status/1171402110031847424), [2](https://twitter.com/Decred_BR/status/1170136831272325121), [3](https://twitter.com/Decred_BR/status/1169812440051109888))
* Sep 5 - [Blockchain Summit](https://blockchainsummit.uy/) - Montevideo, Uruguay. @camilolwi and @pablito presented an overview of Decred called "Governing Together" and talked to devs and journalists after the event. Full report with all media links was [published](https://github.com/decredcommunity/events/blob/master/reports/20190905-blockchainsummituy-montevideo-uruguay.md) in the events repository.
* Sep 5 - [Digital Economy](https://twitter.com/Decred_ES/status/1169677346506297344) - La Paz, Bolivia. @elian's team presented the project to the local community of entrepreneurs and enthusiasts Bolivian Mind Blockchain. ([report](https://twitter.com/elianhuesca/status/1170055934284111872) with photos)
* Sep 7 - Tech4Amazonia - La Paz, Bolivia. The event was collecting donations to fight the wildfires on the Bolivian side of the Amazon River. @elian presented the project to engineering students of El Alto Public University. ([photos](https://twitter.com/elianhuesca/status/1171034359027195904))
* Sep 10 - [Decred Privacy](https://www.meetup.com/Permissionless-Society/events/dnkzvqyzmbnb/) - Amsterdam, Netherlands. @Haon gave an overview of existing privacy projects and introduced Decred's approach. Full report with media links is [here](https://github.com/decredcommunity/events/blob/master/reports/20190910-decred-privacy-amsterdam-netherlands.md).
* Sep 12 - [Decred Meetup](https://twitter.com/Decred_ES/status/1171471998989389824) - Morelia, Mexico. @francov\_ and @luisantoniocrag hosted the first meetup in Morelia and among other things, answered questions from a little kid who seemed to understand Decred. ([photos](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$1568342471606746ojsnf:matrix.org))
* Sep 18 - [Bitcoin and Blockchains Workshop](https://www.facebook.com/events/959839374354073/) - Oaxaca, Mexico.
* Sep 18 - [The Great Bitcoin vs Blockchain Debate](https://www.meetup.com/BlockchainMelbourne/events/264425160/) - Melbourne, Australia. @eSizeDave participated in the debate around the topic "Does blockchain have a viable use case outside of sound money?" as a member of Bitcoin Team, against the Blockchain Team that represented the "blockchain-for-everything" mindset. The setup of the event was not in favor of the Bitcoin team and it lost in the final voting. However, @eSizeDave managed to put Decred and governance in the spotlight quite a few times, including a fabulous Decred T-shirt "coming out". Read his full story, along with some wisdom about attending events efficiently, in [this report](https://github.com/decredcommunity/events/blob/master/reports/20190918-the-great-bitcoin-vs-blockchain-debate-melbourne-australia.md).
* Sep 20 - [A Framework for Blockchain Governance](https://www.eventbrite.com/e/a-framework-for-blockchain-governance-tickets-70134180221) - Washington DC, USA. @akinsawyerr participated in a governance presentation with Thomas Cox of [StrongBlock](https://strongblock.io/) at [Blockshop](https://www.blockshopdc.com/). Engaged in a Q&A session on Blockchain Governance and perspectives on Decred's governance process.
* Sep 21 - [French Vibes Connection](https://twitter.com/Decred_ES/status/1160669435989856256) - Mexico City, Mexico. This was a promo experiment where the Decred logo was blended with visual effects while electronic bands played their tracks to a crowd. @francov\_ notes: "It was extraordinary, Decred's designs were incredible and, together with the music, an environment was created where Decred stood out a lot, there were interested people who asked who we are.". (videos: [1](https://twitter.com/elianhuesca/status/1175609208705863681), [2](https://twitter.com/elianhuesca/status/1175610899006197761); [instagram](https://www.instagram.com/p/B268Uougtbo/))
* Sep 21 - [Decred Meetup](https://twitter.com/DecredArabia/status/1171117988461854721) - Casablanca, Morocco. @arij (@butterfly) talked about her experience as Decred contributor, Decred's governance, privacy and her future plans. People were quite interested and eager to learn, to the point where they stayed an hour after the event was supposed to end, and requested more meetups and even courses in universities and associations. ([report](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156914094936513JoWdj:decred.org), [photos](https://twitter.com/in_insaf/status/1175692906826481664))
* Sep 23 - [SF Bitcoin Meetup](https://www.meetup.com/San-Francisco-Bitcoin-Social/events/dhdhsqyzmbgc/) - San Francisco, USA. @liz\_bagot noted: "@jy-p gave a solid overview of the privacy coins and got a lot of questions at the end. About 50 people showed up from a variety of projects and backgrounds. A big success for Decred - nobody from Decred has ever spoken at a Bitcoin meetup before!" _(to be fair, @camilolwi and @pablito bravely [risked](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156529022111295SCOiX:decred.org) their lives one month [earlier](201908.md#events) at Espacio Bitcoin)_. The event was hosted by [Starfish](https://twitter.com/starfishsf) and the talk was [livestreamed](https://www.youtube.com/watch?v=LgLfMLFfOHQ?t=191) on YouTube.
* Sep 24 - [Decred Privacy](https://twitter.com/decredproject/status/1174374566359183360) - San Francisco, USA. @jy-p gave an overview of the privacy landscape and a deep dive on Decred's implementation. Sponsored and hosted by Coinbase Custody. ([photos](https://twitter.com/HaileyLennonBTC/status/1176697168196849664))
* Sep 25 - [La Conexión](https://twitter.com/Conexion_Events/status/1165075848782852101) - Buenos Aires, Argentina. @elian presented a high level overview of Decred and its history, ran a small booth and talked to the attendees. The day before the event, @elian and @victorarubin had a lunch with several local crypto personalities. Argentinians are very advanced and are looking into alternatives to their currency that may hit 50% inflation this year: "From cap drivers to shop vendors they all know about bitcoin and other cryptocurrencies.". ([report](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15704543735491DFGIA:decred.org), photos: [1](https://twitter.com/victorarubin/status/1176926844916043782), [2](https://twitter.com/victorarubin/status/1176933542762287104)).
* Sep 26 - [Inaugural Decred Meetup](https://twitter.com/MattDavidKaye/status/1164974520081342464) - Los Angeles, USA. @jy-p talked about fundamentals, tech, governance and future of Decred. Hosted by Blockhead Capital. (photos: [1](https://twitter.com/Tantra_Labs/status/1177412535059808256), [2](https://twitter.com/degeri_crypto/status/1177412554101932032))
* Sep 27 - [Crypto Fest](https://argentinacryptofest.com/) - Córdoba, Argentina. @elian and @victorarubin delivered another high level overview of Decred and took the opportunity to connect with members of the local Bitcoin and blockchain community. Notably, the event was endorsed by the local government. Read @elian's full report and impressions about Argentina [here](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15704543735491DFGIA:decred.org) (or wait for GitHub version). (photos: [1](https://twitter.com/victorarubin/status/1177976167145586693), [2](https://twitter.com/victorarubin/status/1178038340505030658))
* Sep 27 - [Blockchain for Business and Government](https://www.eventbrite.com/e/blockchain-para-empresas-y-gobierno-tickets-72417321157) - Monterrey, Mexico. Alteumx (an exchange in Mexico) invited @luisantoniocrag to be present at this event where he had the opportunity to talk about Decred to the public (businessmen and politicians). ([photos](https://twitter.com/Decred_ES/status/1178690139008229376))
* Sep 28 - [Bali Block Confex](https://bali.blockconfex.com/) - Legian, Indonesia. Duyen Em talked to people at the event about Decred, handed out postcards and made some connections. Most people hear about Decred for the first time, and many get interested pretty quickly. Full report is [here](https://github.com/decredcommunity/events/blob/master/reports/20190928-bali-block-confex-legian-indonesia.md).
* Sep 30 - [Voice of Blockchain](https://twitter.com/BlockchainVoice/status/1154772731575099392) - Chicago, USA. @jy-p talked about decentralizing the allocation of capital and why direct sovereignty will last into the future. (photos: [1](https://twitter.com/BlockchainVoice/status/1179100328102203392), [2](https://twitter.com/BlockchainVoice/status/1179088345638621185))

Upcoming:

* Oct 17 - Blockchain and Decred - Morelia, Mexico. @luisantoniocrag and @francov\_ will talk about blockchain and Decred in a university at Morelia city.
* Oct 29-31 - [World Crypto Conference](https://worldcryptocon.com/) - Las Vegas, USA. @akinsawyerr will be speaking on a panel on "Governance Practices" and will also give a presentation titled: "Governing the Crypto Commons". The presentation will highlight Decred's governance process in contrast with other efforts across the public blockchain space.
* Oct 31 - Blockchain APAC - To be confirmed and announced.
* Nov 4-7 - [Web Summit](https://websummit.com/) - Lisbon, Portugal. Decred will have a booth.
* Nov 16 - [BitConf](https://www.bitconf.com.br/portal/) - São Paulo, Brazil. This is one of the biggest crypto events in Latin America. Decred team will present around 3 lectures.

A total of 4 new reports were added to the [events repo](https://github.com/decredcommunity/events), and 1 more is coming. As a reminder, the events repo serves to collect experiences from worldwide events in one place and gives you an accessible report link to disseminate. The repo can be easily replicated to protect the data, and you can even submit a report without leaving your terminal.

Thanks to everybody for writing and submitting reports to grow our knowledge base!

## Media

Selected articles:

* Decred: An Investment Thesis by Wally Hansen ([medium](https://medium.com/coinmonks/decred-an-investment-thesis-bf9ba3cd1042)) - This comprehensive summary of Decred and assessment of opportunities and risks arrived out of the blue, pieced together from public sources by an enthusiastic stakeholder.
* Introducing Dcrpool by @dnldd ([blog.decred.org](https://blog.decred.org/2019/09/25/Introducing-Dcrpool/)) - A blog post introducing and describing the rationale for building an open source stratum mining pool for Decred.
* I Dump Coins on You by @s\_ben ([medium](https://medium.com/@seth.benton/i-dump-coins-on-you-ee6db4331e18))
* Decred Privacy: Taking the Long Road by @Dustorf ([medium](https://medium.com/decred/decred-privacy-taking-the-long-road-62d218223db6))
* Writing Proposals on Politeia (Pi) by Decred Dragon ([medium](https://medium.com/@decreddragon/writing-proposals-on-politeia-pi-e345621652a2))
* How Decred Aims to Build a Decrentralized Governance Model by @evok3d ([bitsonline](https://bitsonline.com/decred-decentralized-governance/))
* The Decred Experiment: Can Decentralization Help Mexico? by @evok3d ([medium](https://medium.com/@evok3d/the-decred-experiment-can-decentralization-help-mexico-1e0e8156430c))
* Proof of Politeia by Tantra Labs ([medium](https://medium.com/@TantraLabs/proof-of-politeia-ac87f52243f4))
* DAOs and the Missing Link: Reputation Protocols by @s\_ben ([medium](https://medium.com/sourcecred/the-dao-missing-link-reputation-protocols-8e141355cef2))
* Decred Lead: Venture Capital Is a "Very Centralizing" Force by Paddy Baker ([cryptobriefing.com](https://cryptobriefing.com/decred-venture-capital-centralizing/))

Translations:

* Iterating Privacy [in Arabic](https://github.com/Insaf01/decred-arabic/blob/master/articles/iterating-privacy.md) by @arij, [in Russian](https://medium.com/decred-russia/iterating-privacy-6d242f78a648) by @DZ and [in Portuguese](https://stakey.club/translated/iterating-privacy/) by @mm
* Turns out a lot of earlier articles were translated to Portuguese as well at [stakey.club](https://stakey.club/pt/translated/)
* More translations of Decred Journal to Arabic (@arij), Chinese (@Dominic and co), Polish (@kozel), Russian (@DZ), Spanish (@francov\_ and @luisantoniocrag) and Vietnamese (@duyenemdo). Thank you for spreading the word!

Videos:

* Decred Assembly Deep Dive: Decentralizing the Treasury with Marco Peereboom ([youtube](https://www.youtube.com/watch?v=4N8Fq1tU3XM))
* @jy-p talks privacy at the San Francisco Bitcoin Meetup ([youtube](https://www.youtube.com/watch?v=LgLfMLFfOHQ?t=191))
* @akinsawyerr talks about Blockchain and Decentralized Finance's Impact on Emerging and Frontier Markets on the Global Startup Movement ([youtube](https://www.youtube.com/watch?v=OIO1q1UO4qM))

Audio:

* Decred in Depth Ep. 8 with @Checkmate - Checkmate talks about the DCR value stack and stock to flow ratio, Bitcoin and Decred on-chain metrics, monetary premiums, sustainable funding to attract committed contributors, and his own research plans. ([youtube](https://www.youtube.com/watch?v=2JbMWgJUoSQ), [soundcloud](https://soundcloud.com/decredindepth/dcr-checkmate))
* POV Crypto Podcast Ep. 76 - @jy-p joins the POV Crypto crew for an episode titled "In Search of Sovereignty" which considers Bitcoin and Decred fundamentals, sovereignty, backwards compatibility and privacy. ([youtube](https://www.youtube.com/watch?v=WnY3c-F5caw), [libsyn](https://povcryptopod.libsyn.com/77-discovering-decred-w-jake-y-p))

## Community Discussions

Comm systems news:

* Chris Burniske's Telegram account was [compromised](https://twitter.com/cburniske/status/1177747319426621440) and was asking people to send him crypto. Make sure to [set your password](https://twitter.com/cburniske/status/1180527281350955008) in Telegram. This is also a good reminder to check your defenses against SIM swapping attacks.
* Impersonation on Discord via Discord Nitro is becoming more common. Nitro allows to change your name _and_ the ID code.
* Decred [airdrop](https://archive.today/GXimX) where you get free ETH is obviously not your friend.
* In general, pay attention and report any suspicious accounts and groups on all platforms.

Selected Reddit posts:

This section tends to feature Reddit threads that had a significant number of comments, many of these posts have low scores and therefore low visibility on Reddit.

* Abstract terminology about [levels of privacy](https://www.reddit.com/r/decred/comments/d0jg3l/abstract_terminology_about_levels_of_privacy/) - discussion of the privacy overview blog post.
* Random Decred Reddit community [question](https://www.reddit.com/r/decred/comments/d6kt1v/random_decred_reddit_community_question/) - about why the number of online members on /r/decred is consistently high relative to total subscribers.
* What Decred [feature or tool](https://www.reddit.com/r/decred/comments/dappgf/what_decred_feature_or_tool_would_you_want_more/) would you want more community members to use?
* Ticket splitting [guide available?](https://www.reddit.com/r/decred/comments/d50wkw/ticket_splitting_guide_available/)
* [Analysis](https://www.reddit.com/r/decred/comments/d1c69a/analysis_of_ticket_voting_so_far_on_the_market/) of ticket voting so far on the market maker proposals.

Selected Twitter discussions:

* @Dustorf's Decred thesis in 2 minutes ([9 tweets](https://twitter.com/lefebvre_dustin/status/1174789127105105928)), based on Wally Hansen's thesis.
* @karamblez [video](https://twitter.com/karamblez/status/1178346009178644481) visualizing activity of btcsuite and Decred repositories since 2013.
* @Checkmate on Decred [hashrate](https://twitter.com/_Checkmatey_/status/1177650799050133504) growth as compared to other assets.
* @Checkmate on Decred and Bitcoin [Stock to Flow](https://twitter.com/_Checkmatey_/status/1173672584933777408).
* dcrpool announcement and summary [tweet](https://twitter.com/decredproject/status/1176914732399439873).
* @jholdstock's pull request to Joule was [merged](https://twitter.com/JamieHoldstock/status/1171347711536357378).
* @matheusd [tweets](https://twitter.com/matheusd_tech/status/1168897318432706561) about bringing 400+ pull requests from upstream Lightning Network's repository to dcrlnd.
* @fernandoabolafio [invites](https://twitter.com/oxfernando/status/1174268398458609664) people to check out the Politeia redesign.
* @moo31337 [suggests](https://twitter.com/marco_peereboom/status/1176856040991801345) that when the markets are down, it's a good opportunity to join a project like Decred and get paid.
* @lukebp's [prediction](https://twitter.com/lukebp_/status/1175441776041058304) about smart contract platforms vs permissionless money and society transformation.
* [Summary](https://twitter.com/jcliff42/status/1170039176277835776) of Decred privacy tech from Jordan Clifford of Scalar Capital.

## Markets

In September DCR was trading between USD 16.49-25.20 / BTC 0.0020-0.0024. The average daily rate was $22.02.

DCR/USD lost more than 20% together with BTC/USD around Sep 24. Among possible causes discussed in the media are: [sharp drop](https://www.ccn.com/bitcoin-hashrate-flashcrash-price-slump/) of Bitcoin's hashrate, [disappointing launch](https://cryptobriefing.com/bakkt-crypto-launch/) of Bakkt that didn't bring the anticipated institutional bull run, and [liquidations](https://bitcoinist.com/yes-bitmex-liquidations-caused-bitcoin-price-to-crash-heres-how/) on derivatives trading platforms.

## Relevant External

The [Crypto Rating Council](https://www.cryptoratingcouncil.com/) was [announced](https://blog.coinbase.com/introducing-the-crypto-rating-council-d6ee33a8f34d), this is a group of cryptocurrency businesses producing ratings of whether cryptoassets are likely to be considered as securities by the SEC. An initial set of 20 [ratings](https://www.cryptoratingcouncil.com/asset-ratings) which position assets on a scale between 1 (not a security) to 5 (very likely a security) were released. Bitcoin, Litecoin, Monero and DAI received the best score (1). Assets like EOS, Tezos, Stellar and Hedera Hashgraph all received a 3.75 score, XRP got 4 and Polymath 4.5. The CRC will not publish the names of projects that received a rating of 5. More ratings will be published in the future. While the methodology is not published, it can be inferred from the bullet-point summaries of ratings that emphasis is placed on whether there was a token sale, whether that occurred before the system had utility, whether there was investment-like language in promotional materials for a token sale, and whether there is decentralized development and usage of the system.

More than 640 crypto projects did not publish any new code in 2019, according to a [study](https://blog.coincodecap.com/analyzing-cryptocurrencies-github-activity/) by CoinCodeCap. The combined cap of these currencies is around $415 million, with the highest individual cap of $85 million. The exchange and market cap data for these tokens is incomplete, but in what is available, YoBit leads the exchanges listing such tokens by having 62 of them.

A settlement between the SEC and EOS was [announced](https://www.sec.gov/news/press-release/2019-202) in which Block.One must pay $24 million in penalties for conducting an unregistered securities sale. This relates to the sale of ERC-20 EOS tokens in a year-long ICO that raised $4.1 billion, the fine amounting to 0.6% of the raised amount. According to Block.One's [press release](https://block.one/news/block-one-announces-settlement-with-us-securities-and-exchange-commission/) the settlement only applies to the ERC-20 tokens, which have since been swapped for EOS mainnet tokens, considered to be in the clear and not require SEC registration for trading.

The Bisq network [announced](https://bisq.network/blog/bisq-dao-first-four-cycles/) that four monthly cycles of its funding DAO have been completed. The Bisq DAO can mint BSQ colored coins to fund development work, and these are burned when used to pay trading fees. Proposals include compensation requests, bonded roles which receive ongoing compensation, parameter changes (trading fees were increased) and signalling approval for other development decisions. In each cycle the number of proposals was around 20 and the number of votes 200-300. The first and second cycles were highly inflationary, with much more BSQ minted than burned, but the 3rd cycle had similar levels of burning and minting and in the 4th cycle more BSQ was burned than minted. _(missed in Aug issue)_

The OKCoin exchange [launched](https://twitter.com/OKCoin/status/1168917669493579776) an [initiative](https://www.okcoin.com/1000btc) on Sep 3 to donate up to 1,000 BTC to the developers of BTC, BCH and BSV software. Verified OKCoin users can vote for the project they prefer and that project's developers will receive 0.02 BTC per vote. This initiative was much discussed on Twitter, with some Bitcoiners promoting it to support the developers while others adopted a more disdainful attitude citing issues with the inclusion of BCH and BSV and the historical timeline presented. As of Oct 2 voting has closed and there are only 47 votes in total (equating to 0.94 BTC) but OKCoin have bumped the total amount donated up to 20 BTC.

CasperLabs, a startup led by Vlad Zamfir, has [received](https://www.theblockcrypto.com/post/39087/vlad-zamfir-led-blockchain-project-casperlabs-bags-14-5m-series-a-to-improve-ethereum-2-0-scalability) $14.5M in Series A funding to work on Ethereum 2.0 Scalability.

Ethereum miners [voted](https://decrypt.co/9573/ethereum-expands-blockchain-capacity-by-25-percent) to increase the gas limit for blocks (and therefore block size) by 25%, in response to rising transaction fees. Miners control the Ethereum gas limit directly and can each edge the limit up or down slightly, so it took some time for the 25% increase to be settled on.

Ethereum also saw the deployment of the Istanbul hard fork on the Ropsten testnet this month, which [happened](https://www.coindesk.com/ethereums-istanbul-upgrade-arrives-early-causes-testnet-split) earlier than expected and caused a chain split. This hard fork is expected to break a number of smart contracts in use on Ethereum mainnet, [including](https://www.coindesk.com/ethereums-istanbul-upgrade-will-break-680-smart-contracts-on-aragon) around 680 of Aragon's smart contracts.

Stellar [launched](https://www.coindesk.com/stellar-to-airdrop-2-billion-xlm-into-keybase-wallets) an airdrop campaign giving users of Keybase free XLM, over the next 20 months Keybase users will receive monthly airdrops of 100 million XLM. Over the course of the 20 months this method of distribution will increase the circulating supply of XLM by 10%. Current circulation is 20 billion XLM out of 105 billion and Stellar Development Foundation controls the distribution.

Stellar Development Foundation also [announced](https://medium.com/stellar-development-foundation/our-proposal-to-disable-inflation-8c9f8b80387) a plan to disable inflation of XLM as part of the version 12 upgrade. Stellar validators will vote to accept or reject this change. XLM inflation was intended as a way for holders to fund projects by setting an address to which their inflationary rewards would accrue. In practice, XLM holders have tended to nominate addresses they control or to join pools so that they can receive the inflation for their XLM holdings themselves. The inflation mechanism is not serving its intended purpose and therefore SDF wishes to disband it.

Dash launched the [Dash Investment Foundation](https://www.dashinvests.org), an entity which will apply for Dash Treasury funds and then invest these in projects which aim to enhance the Dash ecosystem. The DIF is a legal entity which can make loans or investments in exchange for equity in the endeavours it funds. Decisions about what to invest in will be made by a board of elected supervisors.

Tezos Foundation [announced](https://tezos.foundation/news/announcing-second-cohort-of-tezos-ecosystem-grants) funding for a second cohort of 14 Tezos Ecosystem Grants, again with no details of how much was awarded or under what terms. In an FAQ the Foundation explained that they do not disclose details of grants as it would harm their negotiating position. The Tezos Foundation Biannual [update](https://tezos.foundation/news/tezos-foundation-releases-first-biannual-report) (released and missed in Aug issue) does have some information about how the Foundation is spending its resources. In the previous year $14.8M was spent on Research, Education & Core Development, $14.1M was spent on Community grants, and $8.5M was spent on Ecosystem Tools and Applications Grants. On Jul 31 2019 the Foundation held assets valued at $652M, 61% as BTC, 15% as XTZ, 15% in a "stability fund" (diversified portfolio of Bonds, ETFs, Commodities), and 6% as USD fiat.

[Miniscript](http://bitcoin.sipa.be/miniscript/) was [announced](https://twitter.com/pwuille/status/1163592166062473217) by Pieter Wuille, it is a way to write some Bitcoin scripts in a structured way which allows static analysis, generic signing and compilation of policies. It is effectively a set of tools which make it easier to write Bitcoin scripts and be sure of how they will behave. _(missed in Aug issue)_

A large Bitcoin transaction of $1 billion caused [speculation](https://cointelegraph.com/news/someone-just-moved-1b-in-bitcoin-for-700-fee-overpaying-20-times) about who was behind it and what the purpose of the transaction was.

France has [decided](https://cointelegraph.com/news/france-wont-tax-crypto-only-trades-will-tax-crypto-to-fiat-sales) to not tax crypto-to-crypto trades. Only sells of crypto for fiat will be taxed.

European Central Bank (ECB) [started](https://www.bloomberg.com/news/articles/2019-09-12/ecb-cuts-rates-restarts-qe-to-fight-slowdown-as-draghi-era-ends) another round of quantitative easing (QE). It will "purchase" bonds (pumping the price) at a rate of 20 billion EUR per month for "as long as necessary" to hit its euro devaluation goal. This is to "stimluate" the economic growth. Or, as Murad [puts it](https://www.youtube.com/watch?v=XkvcdjSH0c0&t=9m21s), to "electrocute" people. Another good [quote](https://www.youtube.com/watch?v=XkvcdjSH0c0&t=6m21s) comes to mind: "people in cryptocurrencies believe that no living human being should have the power to create wealth from thin air". If you hold EUR or were looking to purchase bonds on a fair market, a good question to ask ECB is where the money comes from and if they worked as hard as you to earn it. Also notice how the language is carefully chosen to not call it what it is, and how hard it is to find a news piece that would explicitly mention the source of money for these "purchases".

GitHub user "DecredCoin" registered on Oct 1 2019 released ["v1.5.0 Mandatory Update"](https://archive.today/Huxft) for Decred. This is obviously a scam, as confirmed by the [virus scan](https://www.virustotal.com/gui/file/ffac37aab22c85952ba022079205700864514f44ea39cdf2bb01504ce2bb9d56/detection). Please report such things as soon as you see them.

For people who like to follow the Bitcoin discussion on Twitter, be careful what you say, as it seems the threshold for being [blocked](https://twitter.com/NickSzabo4/status/1169992390339227648) is getting lower and the overton window of acceptable discussion points or opinions is shrinking.

## About This Issue

This is issue 18 of Decred Journal. Index of all issues, mirrors and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

* writing and editing: akinsawyerr, anastasia, bee, degeri, Dustorf, richardred, s\_ben
* reviews and feedback: davecgh, emiliomann, isuldor, jholdstock, lukebp, matheusd, raedah
* title image: saender

