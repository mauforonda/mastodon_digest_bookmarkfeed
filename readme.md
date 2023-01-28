> An flavor of [hodgesmr/mastodon_digest](https://github.com/hodgesmr/mastodon_digest) that fits in your bookmarks

---

> *Do you use mastodon but get lost with so many new posts?*
>
> *What if something cool happened 500 posts below and you never found out ...*
>
> *You never bothered to use bookmarks consistently or at all?*

Introducing

# Mastodon Digest 
*Bookmark feed edition* ⚡

### The digest will

- **scan** your timeline
- **find** what gained most attention while compensating against account popularity, and
- **add** the top posts in your bookmarks

!["A 🤖 feed in your bookmarks"](thelooks.png "A 🤖 feed in your bookmarks")

### Unlike [previous](https://github.com/mauforonda/mastodon_digest) [versions](https://github.com/mauforonda/mastodon_email_digest/) of the [digest](https://github.com/hodgesmr/mastodon_digest):

- You can **interact with these posts**: like  ★ boost ↻ read threads and replies ⥄ say something!. 
- It's a feed already **baked in many clients**, here I'm using [elk](https://elk.zone) but chances are whatever client you use already has a "bookmarks" tab.
- If your instance has elasticsearch, you can now **search this feed** in the future. 

### Like the other feeds

- you can run it on any schedule 
- to ingest how many hours of your timeline you decide
- sort these posts in one of four ways and 
- give you the whole cream or just the cherry.

### To make your own:

1. Fork this repository
2. Create repository secrets (`Settings` → `Secrets/Actions` → `New repository secrets`) for:
  - `MASTODON_BASE_URL`: the url of your instance, like `https://mastodon.social`
  - `MASTODON_TOKEN`: a token with `read` and `write` permissions  you request in your instance settings under `Preferences` → `Development`
3. Adjust the [github workflow](.github/workflows/update.yml) however you want
  - edit `cron` to define how often you want the digest to run
  - edit the command `python run.py -n 24 -s SimpleWeighted -t lax` with your own preferences for:
```
  -n {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24}
                        The number of hours to consider (default: 12)
  -s {ExtendedSimple,ExtendedSimpleWeighted,Simple,SimpleWeighted}
                        Which post scoring criteria to use. Simple scorers take a geometric
                        mean of boosts and favs. Extended scorers include reply counts in
                        the geometric mean. Weighted scorers multiply the score by an
                        inverse sqaure root of the author's followers, to reduce the
                        influence of large accounts. (default: SimpleWeighted)
  -t {lax,normal,strict}
                        Which post threshold criteria to use. lax = 90th percentile, normal
                        = 95th percentile, strict = 98th percentile (default: normal)
```
4. Enable github actions under `Settings` → `Actions/General`. 

If you've set your secrets right you'll see new bookmarks at the time you specified. And if you want to test it right away you can always go to the `Actions` tab, select the `Mastodon Bookmark Feed` workflow and `Run workflow`, which should add new bookmarks in about a minute.

