# Blipword (daily flash-word game)

Renamed from Blinkword on Nov 2 (v1.9): an iPhone speed-reading app already uses "Blinkword". Jeff picked Blipword. Collection and localStorage keys keep the bw code (bw_devices, bw-day-…). Old folder /mnt/project-files/blinkword/ is the pre-rename copy.

Jeff's idea (Nov 2, 2026): a word flashes on the screen quickly, then you get 4 definitions and pick the one for the word you saw.

- Source: index.html (single file, no build). Owner page: owner.html (Google sign-in, jgold51@gmail.com).
- Daily: 10 words a day, day 1 = Nov 2, 2026. Each word flashes once, faster each round: 0.35, 0.3, 0.25, 0.21, 0.18, 0.15, 0.13, then the Hard words 0.32, 0.28, 0.24 sec (SPEED, since v1.5). Solid blocks (as many as the longest word in the group) show first (0.65 sec), then the word, then the blocks again (0.3 sec) so it can't linger.
- Choices: GROUPS_TXT has 100 groups of 4 look-alike words (BRAKE/BREAK/BRAVE/BAKER), each with a definition. Each day deals 10 groups from a seeded shuffled deck (no repeats for 10 days, then a new shuffle) and picks one word per group as the answer. Add groups to make the cycle longer (keep a multiple of 10).
- Saved per day in localStorage bw-day-YYYY-MM-DD; the flash is saved as "seen" before it shows, so a reload can't replay it.
- Practice (menu and results screen): 10 random groups, not saved or counted.
- Usage: collection bw_devices in aislerun-88e79 (game code bw). Fields: first, last, days, v, opens, plays, done, perfect, streak, best, terms, desk, t, o (opens per ET day), h (words right 0-10 per ET day). Website copy only (smaisle.app / github.io), after tapping Play on How to Play.
- smAisle Daily: writes "bw" to localStorage smaisle_done when today's game is over. Top bar and menu link "‹ smAisle Daily".
- Not yet: GitHub repo (needs SmAisle/Blipword created), smaisle.app invite gate, hub games.js entry, stats.html entry.

## v1.0 (Nov 2)
- First version.

## v1.1 (Nov 2)
- Before and after the flash, solid blocks the length of the word (one per letter) replace the "+" and the random-symbol mask, so it looks purposeful (Jeff's request).

## v1.2 (Nov 2)
- Harder (Jeff: too easy). Flashes about twice as fast: 0.35 sec down to 0.08. The blocks are as long as the longest word in the round's group, so they no longer give away the letter count.

## v1.3 (Nov 2)
- Whole game always fits on one screen, no scrolling (Jeff's request). #app is one screen tall; fit() steps through fit1..fit5 (smaller card, choices, buttons) until nothing overflows. Checked every round of several games at 320x480 up to 768x1000. The results screen's word list moved to a "See today's words" sheet. After you pick, the word name sits to the right of each choice instead of under it.

## v1.4 (Nov 2)
- Last 3 words each day are Hard (Jeff: make the last words longer and more obscure): HARD_TXT has 40 groups of long, rare look-alikes (PERSPICACIOUS/PERSPICUOUS/PERNICIOUS/PERTINACIOUS). Rounds 1-7 come from the 100 normal groups (14 days per shuffle), rounds 8-10 from the hard groups (13 days per shuffle). The speed tag says "Hard". No. 1 (Nov 2) keeps its original deal (puzzleV1) so saved games still match.
- Long words shrink to fit the flash box. "Got it ✓ / Missed ✕" moved from a stamp on the box to the line above it so it never covers the word.

## v1.5 (Nov 2)
- Hard words were too hard (Jeff). Words 8-10 now flash for 0.32, 0.28, 0.24 sec instead of 0.11, 0.095, 0.08. Words 1-7 unchanged.

## v1.6 (Nov 2)
- smAisle Daily Plus game (Jeff: Jexicon, Capital Ship and Blinkword are Plus-only in smAisle Daily, no Plus or purchase of their own). Preview mode = URL ?preview=1, or inside the app when window.DG_APP.plus isn't true: today's first 3 words, then "Unlock the rest with smAisle Daily Plus" with a yellow "‹ smAisle Daily" button (sends {cmd:'home'} to the app, then goes to smaisle.app/daily/). Words 4-10 show a lock; Archive and Practice open a Plus sheet. When the app calls dgNative('store',{plus:true}) the game unlocks and continues at word 4. Without ?preview=1 on the website, the full game plays.
- Icon: paper-style card with "blink" on yellow, three flash rays and five mask blocks. icon-1024/512/192/180.png; the 180 is embedded as favicon and apple-touch-icon (for the GitHub copy, link icon-180.png instead).

## v1.7 (Nov 2)
- Practice: tap a number at the top to jump to that word (for testing speeds; Jeff asked for it "for now"). Words after it are cleared.

## v1.8 (Nov 2)
- Flash time is worked out from the word's length (Jeff): PER_LETTER ms per letter per round (64, 55, 46, 38, 33, 27, 24, then Hard 29, 25, 22) times the letters, rounded to 10 ms, minimum 0.08 sec. The speed tag, the Tap to flash card and the word list show each word's own time.

## v1.9 (Nov 2)
- Renamed Blipword (title, top bar, menu, share text and link smaisle.app/Blipword/, owner page). Icon now says "blip". Game code stays bw.

## v2.0 (Nov 2)
- Speed option (Jeff): 🐢 Slow / ⚡ Normal / 🔥 Fast, picked on word 1's screen (and anytime in Practice) or in the menu. Each has its own ms-per-letter table (SPEEDS): Slow about 1.6x Normal with a 0.12 sec floor, Normal = v1.8, Fast about 0.65x with a 0.05 sec floor. Saved in localStorage bw-speed. A day's game locks its speed at the first flash (G.spd); the results card and share text show the speed. Check-in adds field sp (current speed setting).

## v2.1 (Nov 2)
- Home screen (Jeff): shows when the game opens. Title, tagline, today's game card (Play / Continue / See result, with score or speed), speed picker, Archive · Practice · Stats · How to Play, and links "‹ smAisle Daily" and "‹ smAisle Home" (smaisle.app). Tap the title in the top bar or Menu → Home to come back. In preview mode the card says "Free preview · 3 words" and Archive/Practice show a lock.

## v2.2 (Nov 2)
- Today's game (No. 1, Nov 2) now uses the current rules too (Jeff): 7 normal + 3 Hard words. The old No. 1 freeze is gone and every day deals from k = day - 1. A No. 1 game saved under the old deal is cleared once (localStorage flag bw-mig22) so it can be replayed.

## v2.3 (Nov 2)
- How to Play rewritten to fit an iPhone without scrolling (4 short steps), with a looping demo at the top: blocks, BRAKE blips on, blocks, then the 4 look-alike choices and the right one lights up. If it still doesn't fit (very small screens), the sheet switches to a tighter layout.

## v2.4 (Nov 2)
- smAisle finish-screen standard: the results screen and the preview lock screen have a "‹ smAisle Daily" button and a "More smAisle games" row (icons from smaisle.app/daily/icons, links to each game; list in MORE, from daily/games.js). Share link stays hardcoded to https://smaisle.app/Blipword/.
