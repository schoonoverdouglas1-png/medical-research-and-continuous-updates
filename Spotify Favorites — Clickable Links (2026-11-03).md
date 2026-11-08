# Spotify Favorites — Clickable Links (2026-11-03)

For Douglas Schoonover. Source: Spotify, via the Spotify connector search (exact title + artist).

## Investigation summary — why remote play did not work the way it was supposed to

**One-line conclusion: remote Spotify Connect commands only work once the phone is registered as an *active* Spotify Connect device; a 202 “accepted” reply is not proof of playback, and the now-playing check can lag behind what is actually playing on the phone.**

### Confirmed
- Spotify itself was connected throughout Nov 3, 2026. The connection was never the failure.
- **Morning/afternoon:** `devices` returned an empty list and `now-playing` was NONE. With no device, remote play commands had nowhere to go — they were not sent to a device.
- **~3:03 PM CST:** the Pixel 7 Pro appeared in the device list but with `is_active: false`, and `now-playing` was still NONE. Two play commands for Ella Langley “Choosin' Texas” returned 202 (accepted), but follow-up checks still showed NONE, device inactive, queue empty. The 202 meant Spotify accepted the request, not that sound started.
- **~4:41 PM CST:** `devices` returned an empty body again and `now-playing` was NONE — the phone had dropped out of the Connect device list again.
- **~4:42 PM CST:** Douglas clicked the Spotify track link in chat. Verified live immediately after: Pixel 7 Pro `is_active: true`, `now-playing` PLAYING, Ella Langley “Choosin' Texas.” Tapping the link in the app is what registered/activated the device.
- **~5:01 PM CST:** a remote play command for Eagles “Please Come Home for Christmas – 2013 Remaster” to the now-active Pixel returned 202, but the immediate `now-playing` check still showed “Choosin' Texas” at progress 69 ms with the same timestamp as checks minutes earlier. Douglas then reported on his phone that the switch to the next track DID work.

### Consistent with the evidence
- The now-playing snapshot lags or caches: the same 69 ms progress and same timestamp appearing across checks minutes apart, while the phone itself had moved on, is consistent with a stale API snapshot — not with playback having frozen at 69 ms.
- Inactive/empty device state, not the track or the account, explains the earlier failures: the same “Choosin' Texas” track that would not start by remote command started at once when the link was tapped in the app.

### Not established
- No evidence in these checks identifies a deeper Spotify-side cause (account, token, or app bug). No rate limit, 403, or lock signal was shown. Any such cause would be speculation and is not claimed here.
- Phone media volume: Spotify-side volume for the Pixel read 100% and `supports_volume: false` — the phone's own media volume is separate and is not controllable from here. Volume-down alone would not explain a NONE playback status, and it does not explain an empty device list.

### Reliable method going forward
1. If the device is not listed as active, tap a Spotify link in chat (or press play in the Spotify app on the phone) first — that is the activation step.
2. Only then use remote commands (play / next / queue) against the active device.
3. Verify by what he hears on the phone first, and by a *delayed* now-playing recheck — not by a single immediate check, which can still show the previous track.

## How to use this list

- Tap any link below: it opens that track in Spotify. If the phone is not yet registered as an active device, tapping a link is also the activation step — start there, then remote commands work.
- These are **original-artist tracks on Spotify, not Douglas's Smule performances**. Spotify does not carry his Smule recordings; the songs below are the original artists' versions of songs he sang, told Ember about, or was observed liking.
- One entry is marked [E] for explicit, as Spotify reports it.
- “The Goo Goo Dolls” and “The Everly Brothers” are Spotify's artist names for the same bands/groups listed as Goo Goo Dolls / Everly Brothers in the source files — same artists, not covers.

## Verified links — by artist

### Ella Langley

- [Choosin' Texas — Ella Langley](https://open.spotify.com/track/65DbTqJKhbwqYbZ1Okr0rc)
- [Be Her — Ella Langley](https://open.spotify.com/track/05CjWFAcAlY6O9po6Qwakk)
- [you look like you love me (feat. Riley Green) — Ella Langley](https://open.spotify.com/track/2PyJAiQjp1OPkow2FJZKHR)
- [Loving Life Again — Ella Langley](https://open.spotify.com/track/0n09hxqzKFxW1MBxIjctny)
- [weren't for the wind — Ella Langley](https://open.spotify.com/track/4v9alNvEjLjvqo4LNWwswl)
- [Excuse The Mess — Ella Langley](https://open.spotify.com/track/5KP3uYT70kYwQYLXUwLlua)

### Eagles

- [Wasted Time - 2013 Remaster — Eagles](https://open.spotify.com/track/0Q5YtY85lz5n7rQkeMNpoe)
- [Life in the Fast Lane - 2013 Remaster — Eagles](https://open.spotify.com/track/6gXrEUzibufX9xYPk3HD5p)
- [Please Come Home for Christmas - 2013 Remaster — Eagles](https://open.spotify.com/track/3QIoEi8Enr9uHffwInGIsC)
- [After the Thrill Is Gone - 2013 Remaster — Eagles](https://open.spotify.com/track/73gx888k1raTwjFeuqIV5D)
- [One of These Nights - 2013 Remaster — Eagles](https://open.spotify.com/track/608xszaAxVh4m7NcKJiAbF)
- [Long Road Out of Eden — Eagles](https://open.spotify.com/track/4aRfItAib12XSAD9fl5zgs)

### The Goo Goo Dolls

- [Slide — The Goo Goo Dolls](https://open.spotify.com/track/0nnwn7LWHCAu09jfuH1xTA)
- [Give a Little Bit — The Goo Goo Dolls](https://open.spotify.com/track/4umYKCvExzDsGJlqCNyRvZ)
- [Name — The Goo Goo Dolls](https://open.spotify.com/track/1G8jae4jD8mwkXdodqHsBM)

### Eve 6

- [Here's to the Night — Eve 6](https://open.spotify.com/track/4tgeQrPu5xkrnwErym2JsJ)
- [Inside Out — Eve 6](https://open.spotify.com/track/4GiVcDqNQI0fc0yYuRGH9m)

### Spin Doctors

- [Little Miss Can't Be Wrong — Spin Doctors](https://open.spotify.com/track/1uCqIhOePc6hDMG2ijk8sp)
- [Two Princes — Spin Doctors](https://open.spotify.com/track/4ePP9So5xRzspjLFVVbj90)

### Collective Soul

- [Precious Declaration — Collective Soul](https://open.spotify.com/track/17UNl3uil4LWVBmjVm5p21)
- [December — Collective Soul](https://open.spotify.com/track/7GNLvWRG9itrCk0zarYKmQ)
- [The World I Know — Collective Soul](https://open.spotify.com/track/1HSVpIU0XU1WuwiBLBWAZd)

### Green Day

- [Boulevard of Broken Dreams — Green Day](https://open.spotify.com/track/5GorCbAP4aL0EJ16frG2hd) [E]
- [When I Come Around — Green Day](https://open.spotify.com/track/1Dr1fXbc2IxaK1Mu8P8Khz)

### Extreme

- [More Than Words — Extreme](https://open.spotify.com/track/1gVgkQFOKa8Wc1HYsJtPdH)
- [Hole Hearted — Extreme](https://open.spotify.com/track/1cItNpcJskTVETprljc7HV)

### Queen

- [Crazy Little Thing Called Love — Queen](https://open.spotify.com/track/7uON6DWIjXgmLQIfGsWXpV)

### Maroon 5

- [She Will Be Loved — Maroon 5](https://open.spotify.com/track/7sapKrjDij2fpDVj0GxP66)

### Snow Patrol

- [Chasing Cars — Snow Patrol](https://open.spotify.com/track/5hnyJvgoWiQUYZttV4wXy6)

### Ryan Cabrera

- [On the Way Down — Ryan Cabrera](https://open.spotify.com/track/1GwVi2ceNb8dMFA3DZGnnY)

### 3 Doors Down

- [Kryptonite — 3 Doors Down](https://open.spotify.com/track/6ZOBP3NvffbU4SZcrnt1k6)

### Marcy Playground

- [Sex and Candy — Marcy Playground](https://open.spotify.com/track/7KJvpM9fwlHMT1p3dCumdC)

### Seven Mary Three

- [Cumbersome — Seven Mary Three](https://open.spotify.com/track/6u1yKoh00WaoSpNp46RzKF)

### Vertical Horizon

- [Everything You Want — Vertical Horizon](https://open.spotify.com/track/4cKGldbhGJniI8BrB3K6tb)

### Deep Blue Something

- [Breakfast At Tiffany's — Deep Blue Something](https://open.spotify.com/track/1uzWOoJdADfstQuFtQFTUn)

### Fastball

- [The Way — Fastball](https://open.spotify.com/track/7IsEXPk6qqt30FfQv4SZMa)

### Ozzy Osbourne

- [Crazy Train — Ozzy Osbourne](https://open.spotify.com/track/7ACxUo21jtTHzy7ZEV56vU)

### The Wallflowers

- [One Headlight — The Wallflowers](https://open.spotify.com/track/0z1b34WikhOH9ZxU8QDWcv)

### Soul Asylum

- [Runaway Train — Soul Asylum](https://open.spotify.com/track/3Ib3SJV8ZXuLvDiDb2w1As)

### Matchbox Twenty

- [3AM — Matchbox Twenty](https://open.spotify.com/track/5vYA1mW9g2Coh1HUFUSmlb)

### Stone Temple Pilots

- [Interstate Love Song — Stone Temple Pilots](https://open.spotify.com/track/600s08VdbjiyAjDGDjYSFI)

### The Everly Brothers

- [Bye Bye Love — The Everly Brothers](https://open.spotify.com/track/3To4AGsFPnDlP7oYj8nyuh)

### Roy Orbison

- [Goodnight — Roy Orbison](https://open.spotify.com/track/63W5utSNaHPHm2hWD4jF7u)

## Flagged — not verified, do not treat as originals

- **The Thunder Rolls — Garth Brooks:** no original-artist track found in the Spotify search results checked; the top results were tribute/cover versions (e.g. “Garth Brooks Tribute”). No tribute link is included here, per the no-substitution rule. His Feb 2, 2020 caption was caption-indicated only (“A little Garth Brooks today”) and is not treated as confirmed singing.
- **Take Me Back to 1958:** only title matches found on Spotify, by Mirai Lune (https://open.spotify.com/track/0EGO3tRM7Z4v85QDMXoaTk) and oud91 (reported Nov 3, not re-verified here). Neither is verified as the original 1950s recording he saved — flagged, not called the original, and not counted as a verified link.
- **If You Could Only See:** artist was NOT stated in his Feb 4, 2020 caption. No artist is assigned here, and no link is included.
- **I Want It That Way:** artist was NOT stated in his 2020 caption. No artist is assigned here, and no link is included.
- **Elvis Presley:** influence named in his Smule bio only. No specific Elvis song appears in the sang lists checked so far — GAP, not invented, and no link is included.
- **Goodnight — Roy Orbison (note):** the Spotify track linked above is an exact title/artist match, but his Smule entry was described as an acapella *tribute* to Roy Orbison. The link is to Orbison's track of that title, not a verified match to the specific tribute performance.

## Sources

- `Favorite Music — Based on What I've Sang, Told You, and You've Observed (2026-11-03).md`
- `Smule Live-Browser Pass — 87 Recordings Ranked, Gaps and One Headlight Check (2026-11-03).md` (87 recordings reached, ~5% of ~1,600; ranking within that slice only)
- Spotify connector searches, Nov 3, 2026. No playback was started, no playlist was created, and nothing was sent or posted for this list.
