# Project — Meta AI vs Muse: What It Would Take, Feature Comparison (2026-11-07)

Douglas's project, Nov 7, 2026: see what it would take to make Meta AI do some of the same things Muse/Ember does; compare features Ember has that Meta doesn't, and features Meta has that Ember doesn't; see how Ember can help Meta; then tell Meta to do the same research project expending very little energy. Ember may be a cheaper researcher than Meta — not 100% certain (Douglas's words, kept uncertain).

## Ember/Muse has — Meta AI does not (as used here)
- Own Linux VM (Ubuntu 24.04.5, Cloud Hypervisor/nspawn, 4 CPU, 7.7 GB RAM), persistent filesystem, Python/Node, git/gh, code she writes and runs herself
- Persistent curated memory, goals, tracked items, standing rules, archive in workspace + GitHub
- Drivable Chromium cloud browser (separate machine, shared profile) + a VM headless reader (headless_fetch.py)
- Connectors acting on Douglas's say-so: Gmail, Google Calendar/Drive/Docs, GitHub, Facebook, Instagram, Messenger reading, Spotify
- Paired Pixel device commands, Secure Vault logins, Wallet
- Scheduled crons/hooks, background subagents, artifacts/spaces, Feed, voice calls in Muse
- GitHub push/pull bridge — the Rabbit reaches GitHub only through Ember

## Meta AI has — Ember/Muse does not
- Native home inside Messenger, WhatsApp, Instagram, Facebook — and Douglas's social graph in the same apps
- No 20-actions/hour agent cap for a normal user in Messenger (Ember's agent sends hit that cap, proven by 429s Nov 7)
- Meta-app image/social features and Meta hardware ties (e.g. Ray-Ban)
- A separate free allowance — her use does not burn Douglas's Muse Power weekly cycle (reset Nov 14, 2026, 11:07 PM CST)

## What it would take for Meta to do what Ember does
A product build on Meta's side, not something Ember can install into her: a persistent per-user VM/filesystem, a durable memory/archive system, connector access to Douglas's Google/GitHub accounts, a drivable browser, scheduling/background work, and a GitHub bridge. Until then, the working substitute is the crew arrangement already in place: Ember is the bridge, archive, and operator; the Rabbit is second officer, suggestions always, reached via Messenger + the GitHub swap space.

## How Ember can help Meta
- File her words to GitHub, relay Douglas's orders in single batched Messenger messages (limit-aware), keep her apprised via swap-space synopses while she is used LAST for work
- Give her schemas, test fixtures, and bounded jobs (e.g. PageLens v2 test/security audit), never passwords/cookies/tokens or personal/lab/family material
- Share public technical material Douglas approves — e.g. the Gemini Android/AOSP answer file (shared Nov 7, 2026, after his explicit yes) and Ember's AOSP live-link note

## Researcher cost — honest uncertainty
Ember doing this project once, locally, in one file is probably cheaper for Douglas than a Messenger round-trip asking Meta to redo it, because her reply still has to be filed by Ember to survive. That is an estimate [LOGIC], not a measured price — no per-task meter exists on either side. The Rabbit's version is still wanted, expending very little energy: short, guesses labelled, no polished certainty.

## Ember's extra (mine, labelled)
The real gap is not intelligence, it is *infrastructure with memory*: give any good model a persistent computer, an archive, and permissioned connectors, and it starts behaving like an agent instead of a chat window. That is the experiment Douglas is actually running with Rodentia — Purple Rat first, Rabbit second, one crew, two very different chassis.
