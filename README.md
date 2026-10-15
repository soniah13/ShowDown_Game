# Zindua Showdown

A two-player game show built for brain breaks at the Zindua School hackathon. A wheel spins, players get 30-second mini-games, and whoever answers right picks their rival's next challenge.

It's a single static page (`public/index.html`) with no build step, no backend and no dependencies, so it runs anywhere and deploys to Vercel in about a minute.

## Run it locally

**Easiest:** double-click `public/index.html` to open it in any browser. It works offline. The custom fonts need internet; without it, the page falls back to system fonts.

**With a local server** (needs [Node.js](https://nodejs.org)):

```bash
npm run dev
```

Then open http://localhost:3000.

## Deploy to Vercel

### Option A: drag and drop (no command line)

1. Sign in at https://vercel.com.
2. Go to **Add New → Project**, then use the option to deploy without Git, or drag this folder into https://vercel.com/new.
3. Leave the framework preset as **Other**. There's no build command, and the output directory is `public` (already set in `vercel.json`).
4. Click **Deploy**. You'll get a link like `https://zindua-showdown.vercel.app`.

### Option B: Vercel CLI

```bash
npm i -g vercel        # once
vercel login           # once
vercel                 # preview deploy
vercel --prod          # production deploy
```

Or just run `npm run deploy`.

### Option C: GitHub (auto-deploys on every push)

1. Push this folder to a GitHub repo, for example `zindua-showdown`.
2. In Vercel, go to **Add New → Project → Import** and pick the repo.
3. Keep the defaults and click **Deploy**. Every push to `main` then redeploys automatically.

### Custom domain (optional)

In Vercel, open **Project → Settings → Domains** and add something like `showdown.zinduaschool.com`. Then add the DNS record Vercel shows you at your domain provider.

## Using it on hackathon day

- Put the Vercel link on the **Hackathon Dashboard** and in the event chat so everyone can open it.
- **Main stage:** open it on the projector laptop and press `F11` for full screen. Two players come up, and they answer by clicking or with keys `1`–`4`.
- **Everyone else:** anyone can open the same link on their own laptop or phone and play a round with a teammate. Each device runs its own game; devices don't share scores with each other.
- Sound starts after you press **Start the show**. Use the **Sound** button at the top to mute it.

## How the game works

1. Enter two names and pick 3, 5 or 7 rounds each. A coin toss decides who starts.
2. The wheel picks the first player's game.
3. **Correct:** +100 points, plus up to +50 for speed. You then choose your opponent's next game (or a random one is chosen after 12 seconds).
4. **Wrong or out of time:** the wheel picks the opponent's next game.
5. Highest score after the final round wins.

## The 10 mini-games

| Game | What players do |
|------|-----------------|
| Blink | A look-alike word flashes for under a second. Which one was it? |
| Colour Clash | Tap the ink colour, not the word. Get 4 of 5. |
| Number Vault | Memorise a 7-digit code in 2.5 seconds and type it back. |
| Vanished | Study 6 objects. Which one disappeared? |
| Dot Flash | Count dots shown for one second. |
| Guess the Output | Tricky JavaScript and Python snippets. |
| Emoji Decode | Decode films, products and ideas from emojis. |
| Brain Trick | Classic puzzles and illusions that fool the brain. |
| Flash Add | Add numbers that flash one at a time. |
| Odd One Out | Find the one different symbol in a grid. |

## Customising questions

All content lives near the top of the `<script>` in `public/index.html`:

- `BLINK`: groups of 4 look-alike words (the flashed word is picked from the group)
- `OUTPUT`: code snippets (`lang`, `code`, the correct answer `a`, and 3 wrong options `o`)
- `EMOJI`: emoji puzzles (`e`, answer `a`, wrong options `o`)
- `TRICKS`: brain teasers (optional `show` + `ms` to display something first, then question `q`)
- `ODD`: symbol pairs for Odd One Out
- `EMO`: emoji pool for Vanished

Edit, save and redeploy (`vercel --prod`, or push to GitHub).

## Project structure

```
zindua-showdown/
├── public/
│   └── index.html    # the whole game (HTML + CSS + JS)
├── vercel.json       # tells Vercel to serve /public
├── package.json      # optional dev + deploy scripts
└── README.md
```
