# Decred Ecosystem News Workflow

For now we'll host documentation along DJ docs but keep the data in a [separate repo](https://github.com/xaur/econews) until the process is tested and polished.

Anything is subject to feedback and revision!


## How to discover stories

- Scan sources { to be clarified }


## How to write news entries

See an example of the end result here: https://github.com/xaur/econews/blob/master/econews/202312.md

- All editing churn happens in the `drafts` branch. Unlike DJ we will have just one drafts branch for simplicitly. When a story is finished it is added to the `master` branch and posted in chats (and possibly other targets in the future).

- Title and body combined must take under **1,930 bytes** (which is 1,930 characters if's just ASCII) so it could published in Discord.

- Markdown body is made of bullets.

- First bullet must summarize the story and contain a key fact or two.

- Each remaining bullet must cover notable aspects of the story.

- Links to announcements (as `Announcements: ...` bullet), media coverage (as `Coverage: ...` bullet) and community discussions (as `Discussions: ...`) must be the last bullets.


## Publishing checklist

- [ ] Write item draft in the drafts branch
- [ ] Review by someone
- [ ] Add all contributors to `authors`
- [ ] Add relevant `tags`
- [ ] Publish in Git repo's release branch
  - Fill `published_utc`
- [ ] Publish in Matrix
  - Format for Matrix { to be clarified }


## Metadata format

All stories begin with a metadata block that looks like this:

```
\`\`\`
event_id: 20240131.1
title: Cryptopower released for Android and iOS
author: alice, bob
published_utc: 2024-02-02
updated_utc: 2024-02-05
tags: wallets, Cryptopower
\`\`\`
```

Metadata is placed in this block to facilitate the generation of web pages.

- `event_id` is a unique identifier for a news *event*. It is based on event's date e.g. `20240115.1`. The numeric suffix (`.1`, `.2`, ...) is added to differentiate multiple events on the same date. The date must be a UTC date, i.e. if the event occurred on 2024-01-16 02:00 in the UTC+8 timezone, its UTC date is 2024-01-15. Because event's date is captured by this field we won't store it again in a human friendly format (`2024-01-15`) and instead derive it to avoid duplication. `event_id` will be used in the generated short links.

- `title` is a concise title of the event. If it containts a colon `:`, wrap the whole title in double quotes e.g. `"New DCR mining pool: dcr.gopool.cash"`. The title must be in "Sentence case".

- `author` is a comma-separated list of authors, co-authors, and editors who worked on the news entry. Authors who did more work must come first. Prefer authors' best known *usernames* e.g. `johnz`. These usernames will be used in the links to authors' pages. More information about the authors like their full display name (`John Zoo`) will be stored elsewhere.

- `published_utc` is the UTC date when the news entry was published in the "original release location" which is the Matrix chat room for entries before a Git repository was created, or the Git repository after it was created. { to be clarified }

- `updated_utc` is only added if the entry was updated after it was published.

- `tags` is a comma-separated list of tags. Tags must not contain spaces and use underscore `_` instead.

Valid tags:

- community_efforts
- exchanges
- loans
- mining
- regulation
- releases
- security
- staking
- vsps
- wallets
- (any hardware/software product name)
- (any organization name)
- (any country name)


## File format

- `.md` file extension, can't use custom extension without breaking GitHub's Markdown rendering.
- `----` is a story separator.
- Metadata before the story is surrounded by `\`\`\``. We'd pick more disctinct syntax but this was chosen as a compromise with GitHub.
- Items are sorted as "oldest `published_utc` first".
