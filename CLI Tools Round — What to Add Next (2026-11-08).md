# CLI Tools Round — What to Add Next (2026-11-08)

Douglas's order (Nov 8, ~4:30 AM CST): use the AI search feature, then ask an AI, for other
command-line tools Ember can use through Ubuntu that would make her job better for him.
His follow-up in the same breath: "for certain and for others. Later." — i.e., some picks
are certain, some are for later. Installs wait for his word; this round is the asking.

## Method (his standing rules, applied)
- Memory/local first: full inventory of candidate tools checked against the box BEFORE asking.
- AI search feature: two web searches — plain AND quoted-middle wildcard (his asterisk rule).
  Both returned the same modern-toolkit shelf (convergent): fzf, ripgrep, fd, bat, eza,
  zoxide, jq, tmux, gh, delta, just, shellcheck, btop, lazygit.
- One AI asked (one-at-a-time rule): Gemini, via the free API lane, given Ember's full
  dossier (what she has, what she lacks, her actual work, the ~1.3 GB RAM ceiling).
  Asked for the BEST TWO + one to skip (his best-two rule).

## Inventory verdict (measured on the box, Nov 8 4:31 AM)
ALREADY PRESENT: gh (authenticated tonight), git, ripgrep (rg), jq, sqlite3, fdfind,
tmux, ffmpeg, Python 3.12 + numpy/pandas, Node 24, LibreOffice, pdftotext.
ABSENT (the candidates): fzf, bat, eza, zoxide, pandoc, tesseract, ImageMagick, rclone,
restic, entr, inotifywait, shellcheck, miller, yt-dlp, aria2, httpie, glow, ncdu, htop.

## The AI's best two (Gemini, 507 tokens, verbatim substance)
1. **HTTPie** — friendlier HTTP/API client than hand-rolled urllib scripts; instant
   header/payload/response inspection when an AI-API call misbehaves. ~15 MB, in apt.
2. **yt-dlp** — fetch media + subtitles/transcripts from web video; Ember has ffmpeg
   (processing) but no fetching arm. ~50 MB; NOT in apt (pip or standalone binary).
SKIP per Gemini: **Tesseract OCR** — heavy, spikes CPU/RAM in a 1.3 GB container;
pdftotext covers text PDFs and the multimodal Gemini API she already has beats it
on scanned pages.

## Ember's analysis (hers, labeled)
- HTTPie is a genuine daily-use win for API debugging, but her Gemini/DeepSeek helpers
  already work; HTTPie is convenience, not capability. Class: LATER is defensible.
- yt-dlp is the one TRUE new capability on either list — she cannot fetch a lecture,
  webinar, or its subtitles today at all. Class: CERTAIN candidate.
- Gemini's Tesseract skip REASONING is sound for scanned pages (her API lane OCRs
  better), but the web-search shelf + her own PDF work say the real document gap is
  **pandoc** (format conversion for his manuscripts) — small, in apt, no runtime cost.
- The search shelf's fzf/bat/eza/zoxide are interactive-shell comforts built for a
  human at a keyboard; Ember drives the shell programmatically, so their value to
  HER is low. Honest disagreement with the generic lists, filed as such.
- entr/inotifywait (file watching) remains valuable for the Feed Watch design when
  it is switched on — LATER, with that project.

## Recommendation (Ember's, for Douglas's word)
- CERTAIN tier (install on his go): **yt-dlp** (new capability), **pandoc** (manuscripts).
- LATER tier: HTTPie, entr+inotify-tools (with Feed Watch), shellcheck (with the
  gateway build), miller (if CSV work grows).
- SKIP: fzf/bat/eza/zoxide (human-shell comforts), Tesseract (API lane covers it),
  rclone/restic (no destination approved; backups already via GitHub + Guard copies).
Nothing installed by this round. Every install goes through the Guard first, as always.

## ADDENDUM (same night, ~4:50 AM) — the per-engine CLI deep search landed
Full report: research_notes/cli-tools-per-search-engine-20261108-1032/report.md.
- **eggsearch** (DeepSeek's claim, now checked): it EXISTS — a single Rust binary wrapping keyless
  HTML scrapers (DDG/Brave/Startpage/Yahoo/Mojeek) + a SearXNG JSON client. But every engine it
  wraps is GREY scraping; per Ember's standing terms rule that shelf is not built on. Verdict:
  real tool, wrong class — NOT the pick.
- **Tavily** (not in the original pick list): official API, 1,000 credits/month, NO credit card,
  hard-stops at zero. Now the lead candidate for a sanctioned second lane; the sign-up is
  Douglas's per-candidate decision, same class as the borrowing lanes.
- **Marginalia** retest note: the correct endpoint is api2.marginalia-search.com/search with
  header "API-Key: public" — keyless, official, niche index. Retest owed from the box.
Everything else from the report is folded into Round 7 of the Search Lanes file.
