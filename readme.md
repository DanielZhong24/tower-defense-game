# React Tower Defense Game

Build your own browser-based tower defense game in React. This repository is a
shared starting point for student projects: each student designs their own
theme, towers, enemies, map, and visual style while implementing the required
gameplay and score features.

## Project requirements

Every game should include:

- A React-based playable game.
- Infinite waves of enemies. The game should continue generating waves until
  the player loses or chooses to end the game.
- A meaningful tower defense loop: place or upgrade towers, defend a target,
  defeat enemies, and earn or spend resources.
- A score calculated from the player's performance.
- A way for the player to start a game and see when the game is over.
- A scoreboard or score submission flow backed by Cloudflare D1.
- A production deployment hosted on Cloudflare.
- A responsive interface that works on desktop and, where practical, smaller
  screens.

Students may choose their own:

- Theme and art direction.
- Map layout and enemy path.
- Tower types, upgrades, and abilities.
- Enemy types and special behaviors.
- Economy, difficulty scaling, and scoring formula.
- Sound and visual effects.

## Repository structure

Each student has a directory for their game:

```text
student-name/
  plan.md       # Game design and implementation plan
  ...           # React application files
```

Start by copying [`PLAN_TEMPLATE.md`](./PLAN_TEMPLATE.md) into your game
directory as `plan.md`, or use the existing `plan.md` file there.

## Suggested technology

The reference setup for this project is:

- **Frontend:** React with Vite
- **Hosting:** Cloudflare Pages
- **Score API:** Cloudflare Worker
- **Database:** Cloudflare D1
- **Local development:** Wrangler

You may use another React-compatible setup if your instructor approves it, but
your game must still be deployable to Cloudflare and store scores in Cloudflare
D1.

## Getting started

If you are starting a new game inside your assigned directory:

1. Complete your `plan.md` before writing the main gameplay code.
2. Create or place your React app in that directory.
3. Install dependencies.
4. Run the local development server.
5. Create a local D1 database and apply the score schema.
6. Test the game and score submission locally.
7. Deploy the frontend and score API to Cloudflare.

Commands depend on the chosen project setup. A typical Vite application uses:

```bash
npm install
npm run dev
npm run build
```

Do not commit secrets, API tokens, or private database credentials. Use
Wrangler configuration and Cloudflare environment variables for deployment
settings.

## Score storage

Use a D1 table with enough information to identify a score and explain how it
was earned. A minimal schema could look like this:

```sql
CREATE TABLE scores (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  player_name TEXT NOT NULL,
  score INTEGER NOT NULL,
  wave_reached INTEGER NOT NULL,
  created_at TEXT NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX scores_score_idx ON scores(score DESC);
```

The score API should:

- Validate player names and score values on the server.
- Reject missing, negative, or implausibly large values.
- Record the wave reached along with the final score.
- Return the highest scores in a predictable order.
- Avoid exposing database credentials to browser code.

The score sent by the browser is untrusted. The server should validate the
payload, and the game should clearly document its scoring rules. For a more
advanced project, add server-side protections against duplicate or automated
submissions.

## Infinite waves

Infinite waves should become more challenging without requiring a fixed final
wave. Document the difficulty formula in your plan. For example, later waves
could increase enemy health, speed, count, or combinations of enemy types.
Make sure the difficulty remains playable and that the player can understand
the current wave and the reason they lost.

## Quality checklist

Before submitting, verify that:

- [ ] The game starts from a clear start screen or control.
- [ ] Towers can be placed and interact with enemies.
- [ ] Waves continue beyond the initial test waves.
- [ ] Difficulty changes as waves increase.
- [ ] The game ends in a clear win/loss state.
- [ ] The score is calculated consistently and shown to the player.
- [ ] A score can be submitted to Cloudflare D1.
- [ ] The leaderboard loads stored scores.
- [ ] Invalid score submissions are rejected by the API.
- [ ] The production build completes successfully.
- [ ] The deployed game works on Cloudflare.
- [ ] The plan documents the final design and known limitations.

## Student submissions

Use your assigned folder, keep your plan updated as the implementation
changes, and include setup instructions specific to your game. In your final
submission, describe the deployed URL, the scoring formula, the D1/API
configuration, and any features that are incomplete.