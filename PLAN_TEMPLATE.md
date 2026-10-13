# [Game title]

## 1. Project overview

**Student:** [Daniel Zhong]  
**Game folder:** `daniel-game`  
**Deployment URL:** [Add after deployment]  
**One-sentence pitch:** [Describe what makes your tower defense game unique.]

### Goals

- [What should a player understand or enjoy?]
- [What is the main challenge?]
- [What makes this game different from the other projects?]

### Scope

#### Must have

- [ ] 
- [ ]
- [ ]

#### Nice to have

- [ ]
- [ ]
- [ ]

#### Out of scope

- [Feature you will not implement]
- [Feature you will not implement]

## 2. Player experience

Describe the primary player flow from opening the game to viewing a score.

1. [Start screen or onboarding]
2. [Placing or selecting towers]
3. [Starting and surviving waves]
4. [Losing or ending the game]
5. [Submitting a name and score]
6. [Viewing the leaderboard]

### Controls

| Action | Desktop control | Small-screen control |
| --- | --- | --- |
| Place a tower | [ ] | [ ] |
| Select a tower | [ ] | [ ] |
| Upgrade or sell | [ ] | [ ] |
| Start/pause a wave | [ ] | [ ] |

## 3. Game rules

### Map and objective

- **Player protects:** [Base, lives, village, etc.]
- **Map layout:** [Describe the path and buildable areas.]
- **Loss condition:** [What ends the game?]
- **Pause/restart behavior:** [Describe it.]

### Resources and economy

- **Starting resources:** [ ]
- **How resources are earned:** [ ]
- **Tower costs:** [ ]
- **Upgrade costs:** [ ]
- **Sell/refund rules:** [ ]

### Towers

| Tower | Cost | Attack type | Range | Damage | Fire rate | Special behavior |
| --- | ---: | --- | ---: | ---: | ---: | --- |
| [Name] | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| [Name] | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |

### Enemies

| Enemy | First wave | Health | Speed | Reward | Special behavior |
| --- | ---: | ---: | ---: | ---: | --- |
| [Name] | [ ] | [ ] | [ ] | [ ] | [ ] |
| [Name] | [ ] | [ ] | [ ] | [ ] | [ ] |

### Infinite-wave difficulty

Explain how waves are generated and how difficulty scales indefinitely.

- **Enemies per wave:** [Formula or rules]
- **Health scaling:** [Formula or rules]
- **Speed scaling:** [Formula or rules]
- **New enemy types:** [When and how they appear]
- **Boss or milestone behavior:** [Optional]
- **Difficulty safeguards:** [How you prevent impossible or unfair waves]

Example:

```text
health = baseHealth * (1 + waveNumber * 0.12)
enemyCount = baseCount + floor(waveNumber * 0.8)
```

## 4. Scoring

### Scoring formula

Write the exact formula and explain each part.

```text
finalScore = [your formula]
```

- Enemies defeated: [Points]
- Wave reached: [Points]
- Remaining lives/base health: [Points]
- Remaining resources: [Points]
- Bonuses or penalties: [Points]

### Score submission

- **Player name rules:** [Length and allowed characters]
- **When a score is submitted:** [Game over, manual action, etc.]
- **What is stored:** [Name, score, wave, timestamp, or other fields]
- **Duplicate submission behavior:** [ ]
- **Leaderboard size and ordering:** [ ]

## 5. Technical design

### Frontend

- **Framework/build tool:** [React + Vite, etc.]
- **Rendering approach:** [DOM, Canvas, SVG, or other]
- **State management:** [React state, reducer, library, etc.]
- **Important components:** [List the main components]

### Cloudflare architecture

- **Frontend hosting:** Cloudflare [Pages or other]
- **Score API:** Cloudflare [Worker/API route]
- **Database:** Cloudflare D1 database `[database name]`
- **Bindings/environment variables:** [List names, never put secrets here]

Describe the request flow:

```text
React game -> score API -> D1
React leaderboard <- score API <- D1
```

### Data model

```sql
-- Write the migration/schema you plan to use.
CREATE TABLE scores (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  player_name TEXT NOT NULL,
  score INTEGER NOT NULL,
  wave_reached INTEGER NOT NULL,
  created_at TEXT NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

### API contract

#### Submit score

- **Method/path:** `[POST] [/api/scores]`
- **Request body:**

```json
{
  "playerName": "Player",
  "score": 0,
  "waveReached": 1
}
```

- **Success response:** [Status and JSON shape]
- **Validation errors:** [Status and JSON shape]

#### Get leaderboard

- **Method/path:** `[GET] [/api/scores]`
- **Query parameters:** [Limit, page, etc.]
- **Success response:** [Status and JSON shape]

## 6. UI and visual design

- **Theme:** [ ]
- **Color palette:** [ ]
- **Typography:** [ ]
- **Important screens:** [Start, game, pause, game over, leaderboard]
- **Accessibility considerations:** [Keyboard access, contrast, labels, motion]
- **Responsive behavior:** [What changes on smaller screens?]
- **Audio/animation plan:** [Optional]

## 7. Implementation plan

Break the work into small tasks. Add an owner and status as you work.

| # | Task | Depends on | Owner | Status |
| ---: | --- | --- | --- | --- |
| 1 | Set up the React app | - | [ ] | Not started |
| 2 | Implement the map and enemy path | 1 | [ ] | Not started |
| 3 | Implement enemy movement and wave generation | 2 | [ ] | Not started |
| 4 | Implement tower placement and targeting | 2, 3 | [ ] | Not started |
| 5 | Add resources, upgrades, and game-over rules | 4 | [ ] | Not started |
| 6 | Add scoring and the game-over screen | 5 | [ ] | Not started |
| 7 | Add the Worker score API and D1 schema | 1 | [ ] | Not started |
| 8 | Connect score submission and leaderboard | 6, 7 | [ ] | Not started |
| 9 | Add responsive and accessible UI | 6, 8 | [ ] | Not started |
| 10 | Test and deploy to Cloudflare | 8, 9 | [ ] | Not started |

## 8. Testing plan

### Manual tests

- [ ] A new game starts correctly.
- [ ] A tower can be placed only in valid locations.
- [ ] Towers attack valid targets.
- [ ] Enemies follow the path and reach the base correctly.
- [ ] Resources, upgrades, and selling behave as designed.
- [ ] Waves continue past the initial waves.
- [ ] Difficulty increases without breaking the game.
- [ ] The loss/game-over state appears correctly.
- [ ] The score matches the documented formula.
- [ ] A valid score appears on the leaderboard.
- [ ] Invalid score input is rejected.
- [ ] The game works after deployment.

### Automated tests

List the tests you intend to write.

- [ ] [Wave generation test]
- [ ] [Scoring formula test]
- [ ] [Tower targeting test]
- [ ] [Score API validation test]

## 9. Risks and decisions

| Risk or decision | Impact | Mitigation or chosen approach |
| --- | --- | --- |
| [Example: many enemies on screen] | [ ] | [ ] |
| [ ] | [ ] | [ ] |

## 10. Final reflection

### What was completed?

[Summarize the final game.]

### What changed from the original plan?

[Explain important changes and why they were made.]

### Known limitations

[List bugs, unfinished features, or technical compromises.]

### Future improvements

[List improvements you would make with more time.]
