# TLDR Drive

A one-page phone web app that reads your newsletter emails to you on the drive: **TLDR** (all editions) and **Robinhood Snacks**.

**Live app:** https://jahmehs.github.io/tldr-drive/

- **Pick what and how long.** Choose TLDR, Snacks or Both, then 5, 10 or 15 minutes. Stories play in order of importance and the briefing stops when the time is up.
- **No repeats.** A story that shows up in several emails is merged into one and played once. For example, one Jensen Huang story appeared in TLDR, TLDR Hardware and TLDR AI.
- **Snacks handled properly.** Each Snacks issue is mostly one long article, so it plays as one fuller summary. The jokes, link list, Snack Fact and ads are left out.
- **Skip** jumps to the next story right away. **Go deeper** gives you about 90 seconds more on the story. For TLDR it opens the full article; for Snacks it uses the full write-up in the email.
- **Your skips teach it what you like.** Each story gets a category (for example "Robotics" or "Markets & stocks") plus a few tags, and your reactions are scored:
  - Skip in the first third of a story: strong "not interested" (−1)
  - Skip later in the story: mild "not interested" (−0.5)
  - Hear the whole story: mild yes (+0.4)
  - Go deeper: strong yes (+1.5)

  Recent reactions count more; each one loses half its weight after 30 days. Stories you tend to skip move to the back of the briefing. Settings → *What I've learned* shows the record and has a reset button.
- **Unread or Archive.** Unread plays new emails from the past week. Archive replays older ones by calendar month ("1 month ago", "2 months ago"…), whether they're read or archived. The screen turns plum and amber in Archive mode so you can tell the two apart.
- **Tidy inbox.** Afterwards it marks an email read only if you heard or skipped every story in it. Archive mode never changes your emails.
- A soft two-note chime plays between stories.

There is no server. The page runs in your phone's browser and talks directly to Gmail, Claude and OpenAI with your own keys. **Keys are stored only on each phone, never in this repo.**

## Setting up a phone

1. Open the live app link above in your phone's browser.
2. If another phone is already set up: on that phone, go to Settings → **Show setup QR code**, then scan it with this phone's camera. Done.
3. Otherwise, open Settings and paste in:
   - **Anthropic API key** (required): from https://platform.claude.com → Settings → API keys. Add a few dollars of credit under Billing.
   - **OpenAI API key** (optional, for the natural voice): from https://platform.openai.com → API keys. Add credit under Billing. Tap **Test voice** to check it works.
4. Add the page to your home screen. Tap **Try demo** once to get a feel for the controls.

Each browser keeps its own settings: Safari, Chrome and the home-screen icon each need setting up once. The QR code makes this quick.

The Google sign-in client ID is built in. It only works on addresses listed in Google Cloud → Google Auth Platform → Clients → TLDR Drive → **Authorized JavaScript origins**. Those are currently `https://jahmehs.github.io` and `https://tldrdrive.netlify.app`.

## Updating the app

Edit `index.html` and push to `main`. GitHub Pages publishes the change in about a minute. Reload the app on your phone to get it.

## Rough cost per 10-minute drive

- Claude summarizing about 10 emails: a few cents with Sonnet. Set a Haiku model in Settings to spend less.
- OpenAI voice for about 10 minutes of audio: a few cents.

## Things to know

- Start the briefing **before you pull out**. Signing in and summarizing takes about 20–40 seconds.
- Keep the page open on screen in your phone stand. The app keeps the screen awake, but iOS may pause a web page that's in the background.
- If you skip a few days, a briefing covers at most about twice as many stories as the drive can fit, so the request stays a manageable size.
- To add another newsletter, put its sender address in Settings → **Other senders**.
