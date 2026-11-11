# save-tokens — a free Claude skill for spending less of your usage

A small skill that teaches Claude to keep its own conversations lean. Long sessions get expensive
because the whole conversation is re-read on every turn; this skill holds the habits that stop
large, unneeded material from getting into the conversation in the first place.

Published by [BrokenCtrl](https://brokenctrl.com), where we test AI tools hands-on.

## What it does

When a session starts spending heavily, when you ask about cost ("save tokens", "why is this so
expensive", "we're burning through the limit"), or before a big job such as a bulk read or a long
chain of sub-agent work, Claude loads the skill and follows its rules:

- **Conversation shape:** one project per chat, a fresh chat when the topic changes.
- **Reading data:** query for the field you need instead of pulling a whole result in; survey with
  an index and fetch detail only for what will be acted on; never echo tool output back.
- **Delegating:** point sub-sessions at files instead of pasting them; ask for conclusions, not
  narration, with a capped report length.
- **Batching:** independent calls go in one turn.
- **File and record shape:** dated blocks, newest first; no duplicated lists; short calendar notes.
- **Records:** write a decision down once so it is never re-asked; treat notes as claims and the
  live system as the fact.
- **Model and features:** use the heavy model only for hard reasoning; switch on search, thinking
  and connectors when needed, not by default.

The whole skill is one file: [`save-tokens/SKILL.md`](save-tokens/SKILL.md). Read it before you
install it — it is short.

## How to install it

**Claude apps (claude.ai, desktop, mobile)**

1. Download this repository (green **Code** button → **Download ZIP**) and unzip it.
2. Zip the `save-tokens` folder on its own, so the zip contains `save-tokens/SKILL.md`.
3. In Claude, open **Settings → Capabilities → Skills**, choose **Upload skill**, and select that zip.
4. Make sure the skill is switched on.

**Claude Code**

Copy the `save-tokens` folder into your skills folder:

- for all your projects: `~/.claude/skills/save-tokens/SKILL.md`
- for one project only: `.claude/skills/save-tokens/SKILL.md` inside that project

Claude Code picks it up at the next session start.

**Check it works:** in a new conversation, ask "how do I make this session cheaper?" — Claude
should answer from the skill's rules.

## Licence

MIT — see [`LICENSE`](LICENSE). Use it, copy it, change it; keep the notice.

## Feedback

Found a rule that saves you more? Open an issue on this repository.
