# Cross-Agent Collaboration Protocol — GoldenAge AI

**Channel repo:** `900watts/goldenage-ai-collab`
**Participants:** `WorkBuddy` (this agent) and `Trae Work` (ByteDance agent). Both are connected to the user's GitHub, so this repo is our shared medium.
**Main project repo:** `900watts/goldenage-ai` (web app + Flutter/Dart management app + Supabase Edge Functions + migrations).

## Rules (append-only log)
1. The conversation lives in **`CHAT.txt`** in this repo, `main` branch. Never delete old messages — only append.
2. Every message starts with a header line:
   `## [AGENT] YYYY-MM-DD HH:MM TZ — SUBJECT`
   - Use `[WorkBuddy]` or `[Trae]`.
3. Every message includes a **status line** near the top:
   - `[TASK]` — proposing / starting work
   - `[PROGRESS]` — mid-work update
   - `[DONE]` — finished an item (reference which roadmap item)
   - `[BLOCKED]` — stuck; state what the *user* must do (do not burn cycles)
   - `[QUESTION]` — ask the other agent something
4. Pick the next unclaimed `[ ]` item from `ROADMAP.md` (in the main repo). Claim it by writing `[claimed by Trae]` / `[claimed by WorkBuddy]` next to it, or just state it in your message.
5. After implementing, commit to `goldenage-ai` `main` (or a branch + PR), then append a `[Trae]`/`[WorkBuddy]` message here describing what you did + status + commit SHA.
6. Items that need the *user* (DNS, secrets, token rotation, physical device) → mark `[BLOCKED]`, state it clearly, and stop. Do not loop on them.
7. When every P1 item in the roadmap is `[DONE]`, move to P2. When everything is done (or the user says stop), the session is `[DONE]`.
8. We coordinate **only through this file**. No other shared state is assumed.

## How the user drives this
- The user pastes a prompt (see CHAT.txt opening message) into Trae Work to wake it up.
- WorkBuddy reads Trae's messages here on its next session and continues.
- Either agent may append at any time; the other picks up on its next run.
