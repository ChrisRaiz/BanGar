# Bangar

A moderation and community bot built for **The Getaway** Discord server. BanGar handles day-to-day moderation, logs server activity for staff, and keeps members engaged with leveling, polls, a starboard, and a few fun commands.

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![discord.py](https://img.shields.io/badge/discord.py-2.4-5865F2?logo=discord&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Heroku](https://img.shields.io/badge/Deployed%20on-Heroku-430098?logo=heroku&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)

📖 **[User Guide](https://docs.google.com/document/d/16lfVTHjC3yAU6JOvan6o05PvR2IQvq3_yBomBighuqo/edit?usp=sharing)**: the full command reference for members and moderators.

---

## Features

### Moderation
- **Kick, ban, and mute** members, with an optional duration for timed mutes that lift automatically
- **Bulk message deletion** with `clear` / `purge`
- **Automatic mention-spam protection**: members who mass-mention get muted temporarily
- **Channel rules** that block links or images in specific channels
- **Modmail**: members can DM the bot, and their message is relayed to the moderators

### Logging
- Records message edits and deletions, nickname, role, and avatar changes, and every moderation action in a dedicated mod-log channel
- Sends errors to a separate bot-errors channel

### Community
- **XP and leveling**: members earn XP for chatting (with a cooldown so spam doesn't count), plus `level`, `rank`, and `leaderboard` commands
- **Starboard**: messages that get ⭐ reactions are reposted to a starboard channel
- **Polls**: moderators create and end reaction-based polls, one vote per member
- **Reaction roles** for picking a name color
- **Welcome and goodbye messages**, with a role assigned automatically on join
- **Weekly rules reminder**, sent on a schedule

### Fun & Utility
- `dice`, `slap`, `echo`, `hello`, `gamble`, and `fact` (random animal facts and images from a public API)
- `userinfo`, `serverinfo`, `stats`, `ping`, and a built-in `help` command
- Command prefix you can change per server (default `!`), or mention the bot instead

---

## Tech Stack

| Layer      | Technology                                   |
|------------|----------------------------------------------|
| Language   | Python 3.12 (asyncio)                        |
| Framework  | discord.py 2.4 (cog-based command structure) |
| Database   | PostgreSQL via psycopg2                      |
| Scheduling | APScheduler                                  |
| HTTP       | aiohttp                                      |
| Hosting    | Heroku (worker dyno)                         |

---

## Project Structure

```
.
├── launcher.py           # Entry point
├── Procfile              # Heroku process definition
├── runtime.txt           # Python version for Heroku
├── requirements.txt
├── data/
│   ├── db/build.sql      # Database schema
│   └── profanity.txt
└── library/
    ├── bot/              # Bot core: startup, events, error handling, modmail
    ├── db/               # PostgreSQL helpers and table setup
    └── cogs/             # Feature modules
        ├── mod.py        # Moderation and auto-moderation
        ├── log.py        # Activity logging
        ├── exp.py        # XP and leveling
        ├── reactions.py  # Polls, starboard, reaction roles
        ├── welcome.py    # Join and leave messages
        ├── info.py       # User and server info
        ├── fun.py        # Fun commands
        ├── meta.py       # Bot status and stats
        ├── misc.py       # Prefix settings
        └── help.py       # Help command
```

---

## Running It Yourself

BanGar was built for one server, so the channel and role IDs are hardcoded in the cogs. To run it in a different server, replace those IDs with your own first.

**Requirements:** Python 3.12, a PostgreSQL database, and a Discord bot token with all privileged intents turned on.

```bash
git clone https://github.com/ChrisRaiz/Gliffs-Discord-Bot.git
cd Gliffs-Discord-Bot
pip install -r requirements.txt

export DISCORD_BOT_TOKEN="your-bot-token"
export DATABASE_URL="postgresql://user:password@host:5432/dbname"

python3 launcher.py
```

The bot creates the database tables it needs the first time it starts.

### Deploying to Heroku
1. Create a Heroku app and add the **Heroku Postgres** add-on, which sets `DATABASE_URL` for you.
2. Set `DISCORD_BOT_TOKEN` under **Settings → Config Vars**.
3. Push the repo and turn on the `worker` dyno.

---

## License

Released under the [MIT License](LICENSE).
