---
name: "save-tokens"
description: "Use whenever a session is spending heavily or the user asks about cost — \"save tokens\", \"this is using a lot of usage\", \"why is this so expensive\", \"how do I make this cheaper\", \"we're burning through the limit\" — and proactively before any large survey, bulk read, multi-project session, or long chain of sub-agent work. Holds the token-discipline rules: what enters the conversation is the cost, not how many calls are made."
---

# Token discipline

## The one thing to understand

The dominant cost is not any single call. It is that **the whole conversation is re-read on every
turn**. A large result pulled in early costs a little once, then again on every later turn for the
rest of the session. So the question is never "how many calls did I make" — it is **"what did I let
into the conversation, and does it need to be there?"** Re-read history dwarfs everything else;
output is expensive per token but tiny in volume.

## Conversation shape

- **One project per chat.** New topic, new chat — otherwise every project's context rides along in
  every later turn of every other.
- **Start the fresh chat when the topic changes**, not when the chat feels heavy. By then the cost
  is already paid.
- **Close finished sessions** — an idle session invites re-reading.

## Reading data

- **Never pull a large result in to look at one field.** Query it instead.
- **A tool result written to disk is an opportunity:** run `jq`/`grep`/`awk` against the file and
  return only what is needed.
- **Survey with an index; fetch detail only for items you will act on.**
- **Prefer targeted `grep` over reading whole files.**
- **Never re-read a file you just wrote** — the write either succeeded or errored.
- **Read running sessions as progress summaries, not full transcripts.**
- **Don't echo tool output back in your own text** — it is already in the conversation; repeating
  it pays for it twice.

## Delegating to sub-sessions

- **Point at files, don't paste them.** A session with repo access reads its own state file
  cheaply; a pasted copy also sits in the parent conversation forever.
- **Ask whether the sub-session has the connector** before passing data it could fetch itself —
  and let it write back directly, removing a round-trip.
- **Ask for conclusions, not narration — say so explicitly.**
- **Tell it not to quote long file contents back**, and **cap the report length**.
- **One task at a time when something is urgent.**

## Batching

- **Independent calls go in one turn.** Sequential calls each pay a full re-read of everything
  before them. Serialise only when a later call genuinely depends on an earlier result.

## File and record shape

- **State files: dated blocks, newest first.** A reader takes one block, not the history.
  Appending buries the present state furthest from where every reader starts.
- **Split anything that must be read end-to-end to find the present state.**
- **Calendar events short, when a session reads them:** objective, live blockers, pointer, a few
  hundred characters at most. Recurring events multiply their description by every instance.
- **Delete duplicates; never mirror a list into two places** — copies drift, and a session then
  pays to work out which is true.

## Records

- **A decision written into one log file in the project is read once and settles the question.**
  One that lives only in a chat gets re-discovered, re-asked and re-argued — and wastes the user's
  time being asked what they already decided. One row: date, one-line statement, who decided,
  source. Mark each row decision or verified fact — they age differently.
- **Notes are claims; the system is the fact.** Verify against the live system before relying on a
  recorded state.
- **A dissolved item is a win — record it as one**, or it reappears and gets re-investigated.
- **Correct a wrong diagnosis explicitly, not silently**, and name what replaced it.

## Model choice and features

- Reserve the heavy model for genuinely hard reasoning; say so when a lighter one would do.
- Connectors add their tool definitions to the conversation once active; web search and extended
  thinking add usage whenever they run. Switch them on when needed, never by default.
- Recurring reference material belongs in a repo file read once, not re-uploaded into each chat.
