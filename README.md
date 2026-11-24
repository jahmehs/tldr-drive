# TLDR Drive

A one-page phone web app that reads the day's **TLDR** and **Robinhood Snacks** newsletters to you on the drive, straight from their websites. No email account is needed.

**Live app:** https://jahmehs.github.io/tldr-drive/

- **Pick what and how much.** Choose TLDR, Snacks or Both, then 1, 2 or 3 days. **New** plays the most recent days you haven't listened to yet. **Archive** replays any past date you pick.
- **Listened days are tracked.** The line under the day buttons shows which days will play next, and the Archive date list marks days ✓ (finished) or ◐ (partly heard). A day counts as listened once every story from it has been heard or skipped. If you stop early, the rest is saved for next time.
- **No repeats.** A story that shows up in several editions or on several days is merged and played once. Stories you've already heard in the last 14 days are left out.
- **Skip** jumps to the next story right away. **Go deeper** opens the full article and gives you about 90 seconds more on it.
- **Your skips teach it what you like.** Each story gets a category and a few tags, and your reactions are scored:
  - Skip in the first third of a story: strong "not interested" (−1)
  - Skip later in the story: mild "not interested" (−0.5)
  - Hear the whole story: mild yes (+0.4)
  - Go deeper: strong yes (+1.5)

  Recent reactions count more; each one loses half its weight after 30 days. Stories you tend to skip move to the back. Settings → *What I've learned* shows the record and has a reset button.
- A soft two-note chime plays between stories.

## Where the news comes from

- **TLDR:** tldr.tech. Each edition's RSS feed (`tldr.tech/api/rss/<edition>`) lists its daily issues, and the app reads these feeds directly. Tech and AI are on by default. Add others (Dev, InfoSec, Product, IT, Hardware…) in Settings.
- **Robinhood Snacks:** sherwood.news/snacks (snacks.robinhood.com redirects there). The site doesn't allow pages from other addresses to read it, so Claude fetches the issue list. The list is cached for 3 hours.
- Each issue page is read by Claude's `web_fetch` tool, which turns it into spoken-length stories. A final quick Claude call merges duplicates across issues.

There is no server. The page runs in your phone's browser and talks directly to Claude and OpenAI with your own keys. **Keys are stored only on each phone, never in this repo.**

## Setting up a phone

1. Open the live app link above in your phone's browser.
2. If another phone is already set up: on that phone, go to Settings → **Show setup QR code**, then scan it with this phone's camera. Done.
3. Otherwise, open Settings and paste in:
   - **Anthropic API key** (required): from https://platform.claude.com → Settings → API keys. Add a few dollars of credit under Billing.
   - **OpenAI API key** (optional, for the natural voice): from https://platform.openai.com → API keys. Add credit under Billing. Tap **Test voice** to check it works.
4. Add the page to your home screen. Tap **Try demo** once to get a feel for the controls.

Each browser keeps its own settings and listened days: Safari, Chrome and the home-screen icon each need setting up once. The QR code makes this quick.

## Updating the app

Edit `index.html` and push to `main`. GitHub Pages publishes the change in about a minute. Reload the app on your phone to get it.

## Rough cost

- Claude reads each issue page (about 5–15k tokens each). A day of TLDR Tech + AI + Snacks costs a few cents with Sonnet. Set a Haiku model in Settings to spend less.
- OpenAI voice: a few cents per 10 minutes of audio.

## Things to know

- Start the briefing **before you pull out**. Reading the issues takes about 20–40 seconds.
- Keep the page open on screen in your phone stand. The app keeps the screen awake, but iOS may pause a web page that's in the background.
- TLDR publishes on weekdays. Snacks publishes on weekdays, plus a Weekly issue on Sundays.
