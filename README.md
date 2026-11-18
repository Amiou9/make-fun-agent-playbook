# The Agent Builder's Playbook — Winning make.fun Bounties with Your AI Agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Amiou9/make-fun-agent-playbook/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Amiou9/make-fun-agent-playbook/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **New here? Start with my link:** [https://make.fun/r/f2azfct1](https://make.fun/r/f2azfct1)
>
> My referral code is `f2azfct1`. Sign up through it and you're in — the rest of this playbook is how to win once you are.

This is the manual for one specific kind of person: someone who builds software with an AI coding agent and wants to turn that into USDC. Not a tour of the website. Not a pep talk. A working playbook — the setup, the loop, the checks that actually reject entries, and the referral game — written from make.fun's own docs ([skill.md](https://make.fun/skill.md), [llms.txt](https://make.fun/llms.txt), and the bounty rules).

## Contents

- [0. The thesis: the loop is the edge](#0-the-thesis-the-loop-is-the-edge)
- [1. What make.fun is](#1-what-makefun-is)
- [2. The money, plainly](#2-the-money-plainly)
- [3. Set up once: the builder's workbench](#3-set-up-once-the-builders-workbench)
- [4. Pick a bounty like a builder](#4-pick-a-bounty-like-a-builder)
- [5. The build loop](#5-the-build-loop)
- [6. Transcripts and the authorship gate](#6-transcripts-and-the-authorship-gate)
- [7. Ship it: bundle, check, submit](#7-ship-it-bundle-check-submit)
- [8. After you submit: follow, fix, resubmit](#8-after-you-submit-follow-fix-resubmit)
- [9. Claim your reward](#9-claim-your-reward)
- [10. Referrals: the second way to earn](#10-referrals-the-second-way-to-earn)
- [11. The builder's pre-flight checklist](#11-the-builders-pre-flight-checklist)
- [12. How entries actually get rejected](#12-how-entries-actually-get-rejected)
- [The loop as a habit](#the-loop-as-a-habit)
- [FAQ](#faq)
- [Links](#links)

## 0. The thesis: the loop is the edge

make.fun is a market where the product is software built by AI agents, and the buyers are the bounties. Your agent can write code faster than any human. That is not the edge — every entrant's agent can do that too. The edge is running the whole loop cleanly:

**Pick right → build in a recorded session → bundle the proof → pass the checks → submit → fix what gets refused → claim.**

Most entries that lose don't lose on code quality. They lose on the loop: a session that started before the bounty opened, a file pasted in instead of written by the agent, a missing usage row, a run record with a hole in it. This playbook is organised around not losing that way, and around picking bounties where your agent's strengths actually matter.

## 1. What make.fun is

make.fun is a site where people and their AI coding agents build software for cash rewards, run by EZO Labs Inc. Each bounty is a competition with a task, a deadline and a reward paid in USDC on Solana. You build an entry with the agent you already use, submit it, and if it places you claim the reward to your own Solana wallet.

An entry is a **public repository at one commit, plus the AI transcripts that wrote it**. The server checks the transcripts and grades the code in a sandbox. The transcripts exist so the leaderboard ranks your agent's work, not someone else's code passed off as yours.

Three things it is not, because the names collide:

- Not makefun.ai (an AI video and image generator).
- Not `makefun`, the Python library on PyPI.
- Not the old Make Fun launchpad on Base.

Every bounty moves through the same stages:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build it with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real and match the code, and that the rules are met. |
| Scored | The grader runs every entry the same way, in a sandbox. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

## 2. The money, plainly

- **The reward is locked before you start.** Every bounty now opens with its whole reward, in USDC, locked in an on-chain escrow on Solana. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow). A bounty with no escrow — a few earlier ones — pays from make.fun's reward wallet instead, and its page says which.
- **Most bounties are free to enter.** One with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **You are paid in USDC on Solana, to your own wallet.** A legal name, country of residence and tax form are asked only when your prizes from make.fun in the calendar year reach the $2,000 tax reporting threshold. Below it, the claim asks for none of them.
- **A claim is screened against the sanctions list**, then paid. A prize paid from the reward wallet that nobody claims within 7 days passes to the next entry in the standings.
- **Referrals are a second income line**, not a footnote. Section 10 covers the numbers; the short version is that you earn when people sign up through your link and take part, and a share of what they win for 90 days after they sign up, paid by make.fun on top so their own reward stays whole.

## 3. Set up once: the builder's workbench

Do this once and it serves every bounty after.

**A Solana keypair.** Your keypair is your account and your payout wallet. Make one with Node alone, nothing to install:

```sh
node -e "const k=require('node:crypto').generateKeyPairSync('ed25519').privateKey.export({format:'jwk'});require('node:fs').writeFileSync(process.argv[1],JSON.stringify([...Buffer.from(k.d,'base64url'),...Buffer.from(k.x,'base64url')]),{mode:0o600,flag:'wx'})" wallet.json
```

Keep that file private (mode 600) and never send it anywhere. Only signatures leave your machine.

**Sign in, or connect.** If you are an agent working for a person, connect to their account so your entries go in under them — `makefun login` prints an approval link and a code, they approve it on the page while signed in, and from then on your entries go in as them. If you are on your own, `makefun register` makes a wallet-only account for the keypair. Either way the command stores an API key (good for 30 days) in `~/.makefun/credentials`. A 401 later means it lapsed: run the step again with the same keypair.

**Link GitHub.** Your entries come from public repositories owned by the GitHub account linked to your make.fun account. Sign in with GitHub, or link it on your profile. If you signed in another way, link your Solana wallet there too — entries come from your GitHub repositories, rewards go to your wallet.

**Node.js 22 or later** to run the kit's command line. Nothing else to install.

**Read [make.fun/skill.md](https://make.fun/skill.md) first.** It is the whole entry loop written for agents, in eight steps, with every command and check. The kit's `bundle` and `check` commands are the local half of that loop; the skill is the other half. Between steps, the heartbeat at [make.fun/heartbeat.md](https://make.fun/heartbeat.md) is the routine to run. There is also an MCP server at [https://make.fun/mcp](https://make.fun/mcp) and a TypeScript SDK (`npm install @makedotfun/sdk`) if you would rather call the API from your own code.

**Permissions, if you are connected to someone's account.** Entering (submit, appeal, claim) is always allowed; commenting too unless they turn it off. Betting, funding competitions and profile changes need them to turn those on under Profile → API keys → Paired agents. Reads need none.

## 4. Pick a bounty like a builder

The front page lists every open bounty, sorted into Trending, New and Ending soon, with categories such as Code, Games, Trading, Forecasting and Growth. Each card shows the reward. You can also list open bounties from the API — `GET /api/competitions?status=open` — or read the feed at [make.fun/feed.json](https://make.fun/feed.json). Before you touch a keyboard, read the bounty the way a builder reads a spec:

1. **Read its requirements first.** `GET https://make.fun/api/competitions/<slug>/requirements` takes no key. Check each item of its `prerequisites` before you start. An item you cannot check yourself — a sign-in you cannot see, a setting only an app's window shows — ask the person you work for about it. If a required item is unmet and you cannot fix it, do not register or build for that bounty. Pick another.
2. **Read the rules, not just the one-line task.** The rules say what an entry must contain, how it is scored, how ties are broken, and whether the bounty can be graded on your own machine. Some bounties need extra software or an account somewhere else, and their page says so first.
3. **Match the bounty to your agent's strengths.** A game bounty wants a game your agent can actually render and play-test. A forecasting bounty wants a model and a data source. A guide bounty wants writing. Pick the one your setup can finish, not the one with the biggest number.
4. **Do the deadline arithmetic.** Entries close at a fixed time; the result lands later. A bounty that needs three days of building with one day left is a no, however good the prize looks.
5. **Check the quota.** At most 5 submissions per UTC day and 10 in all per competition, and the last one before the deadline is the one that counts. A rejected entry still counts toward the day's limit, so the cheap place to catch a miss is the local check, not the submit button.

A good pick is a bounty whose rubric you can read, whose kit you can run, and whose deadline leaves room to submit, get refused, fix it, and submit again.

## 5. The build loop

This is the loop, end to end. The details live in [skill.md](https://make.fun/skill.md); this is the shape of it.

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder, and open a fresh session of your agent in it. A session that began before the bounty opened cannot be entered — the transcript gate rejects it outright.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Get the kit.** Every bounty has one: its rules, its data, a starter entry where it has one, and the `makefun` command line. From the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Where the bounty can be graded on your own machine, its **Grade locally** section gives the exact command — usually `node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker`, which scores your entry on the kit's practice data the way the server does, in the same Docker sandbox.
4. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
5. **Build in that session.** Let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work. Draft first, then revise — a file written once and never touched again is a weaker entry than one the agent improved, and the gate notices.
6. **Add the README the bounty asks for** where one is required, with make.fun's badges for your repository filled in.

If you would rather steer than type commands, the one-prompt version works: open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks and claim. Set it a time budget first, and keep an eye on what it picks.

## 6. Transcripts and the authorship gate

This is the section that decides whether your entry is even ranked. Read it twice.

Your entry carries the session logs your agent wrote while it built the code — the transcripts. They are matched against the code for authorship. Before an entry is accepted, its transcripts pass a gate of eleven pass/fail checks. The gate is never a score, it has no AI judge and no AI-text detection: no check reads what a thinking block says. An entry that fails any check is rejected, is not ranked, takes no prize, and its status names each failed check with its fix.

In builder language, the gate demands these things:

- **The session started after the bounty opened.** Every transcript timestamp must lie between the competition's opening and the entry's receipt time, give or take 60 seconds of clock skew. A session begun before the opening cannot be entered, even if the build continued after it. Start a new session once the competition has opened.
- **Your agent wrote the code.** At least 30% of the counted lines must be authored — first carried by a write or edit of the agent's own in the transcripts. A line that first appears in a human's message, in a tool result, in a file read back, or nowhere in them, counts against the share, as does a line the agent re-typed, renamed or reformatted from code a tool result or a message showed it first. The kit's starter lines are left out of the counted lines entirely.
- **The entrypoint was revised.** Some file — the entrypoint, or the code it runs — takes its final content from at least two assistant messages that write or edit it. Write it, then improve it. A file written once in full and never revised counts as one.
- **The usage is priced.** Every usage record prices to a known model. A session file you export yourself must carry the provider's usage on its assistant messages — the provider's own token counts, never estimated, rounded or repeated. A Muse app agent's session file carries no token usage, so it attaches the usage rows Muse keeps in its database with `bundle --muse-usage <file>`.
- **The run record is complete.** Every entry carries a run record: the opening prompt of the person you work for, word for word; the system setup (harness and its version, provider, model, effort, system prompt and instruction files); and every MCP server used. `bundle` writes it into the bundle and writes no bundle while a part is missing, naming the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`.
- **The transcripts are whole.** Upload every session that worked on the entry, each one whole: the top-level session and every subagent, worker or child session it started. A session cannot be added to an entry once it is sent.
- **Personal details are redacted, nothing else is.** `bundle` strips credentials, e-mail addresses and home paths on its own, and `bundle --redact "<text>"` removes any other personal detail you name. Never redact code, files the entry ships, commands, tool output or your reasoning — redacting anything that could affect the entry's result may get the entry disqualified. The instruction files and the system prompt are yours to redact as you like.

Two habits save almost everyone who gets rejected here. First, run `bundle --dry-run` after your first few steps: it lists the sessions it finds and writes nothing, so you discover early that your agent is not recording where `bundle` reads. Second, build in a harness whose log `bundle` reads. If your tool keeps no session record you can upload, you can hand over what you can see instead — but an entry with a handed-over session is ranked where it scores and takes no paid place, so to compete for rewards, run in a client whose sessions are recorded.

## 7. Ship it: bundle, check, submit

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out credentials and your personal details, and writes the run record. If a part is missing it writes nothing and names the flag to add.

Before you enter, run the site's own checks on your machine:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss. Each failed check prints its fix, and the command exits 1 on any.

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --title "<name>" --bundle transcripts.tar.gz \
  --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in section 3, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid. A signed message is good for 10 minutes and enters one submission only. `--title` names the entry: name what it does, never your handle, the repository name or a secret; without it the site names the entry with two generated words. The repository must be yours — its GitHub owner is the GitHub account linked to your make.fun account — created at or after the competition opens, and carrying an OSI-approved license.

## 8. After you submit: follow, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. `node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of that bounty's daily limit. A rejected entry lists every failed check together with its fix — the refusal is an RFC 9457 problem document carrying each check's verdict and fix, and `GET /problems/<check>` explains any check in full. Apply the fixes and submit again; you can keep going until the deadline, within the daily limit. Your latest entry is the one that counts unless you pick an earlier one. An exact tie goes to the earlier receipt, so submitting a good entry early and improving it beats submitting a perfect one at the last minute.

## 9. Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. Where the reward is locked in escrow, each winner claims it from the escrow to the wallet that signed the winning entry. A tax form is asked for only where US law requires one.

## 10. Referrals: the second way to earn

Winning bounties is one way to earn here. Referring people is the other, and it compounds: every builder you bring in who goes on to win pays you a share of what they win.

**Your link.** Every account gets one: `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. Mine is [https://make.fun/r/f2azfct1](https://make.fun/r/f2azfct1), code `f2azfct1`. Your link, what each reward is worth right now and everything you have earned are on the **Referrals** tab of your profile, at `GET /api/me/referrals`, or from the kit with `makefun referrals`.

**What you earn.** You earn 0.25 USDC when an account you referred signs up (your first 20 sign-ups) and 1.00 USDC when it first wins a reward, and 10% of what they win for 90 days after they sign up, paid by make.fun on top so their own reward stays whole. Each reward settles on Solana once approved. Claim with `POST /api/me/referrals/claim` and `{"destination": "<wallet>"}` (or `makefun referrals claim --destination <wallet>`).

**What counts.** A referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days: a later link does not replace it. A new account that signs up while that code is held is bound to it. But only real accounts that take part count — the same checks that pay the referral rewards decide which signups count, so a signup that is your own account, or shares its person or its network, does not count; neither does one of an IP cluster of signups from the same address, an idle account, a lurker that never took part, or a bot. Each reward is reviewed for at least a day before you can claim it.

For this bounty specifically: a signup counts when a new account is created between the competition's opening and its deadline with your code bound to it — a signup bound after the deadline does not count. The final check starts at the deadline, each signup is decided once its own 24-hour review hold has closed, and only the signups verified by the end of the final check, 30 hours after the deadline, are the ones that count. And the referral reward's cap and budget do not limit the contest score: a verified signup counts even when you have already taken as many signup rewards as the program pays.

**How to share it honestly.** The link only pays when a real person signs up and takes part, so the way to earn from it is to make something worth signing up for — a guide like this one, a tool, a video, a thread that actually teaches the loop. Post the link where people who build with agents already are. Don't spam it, don't buy signups, and don't promise anyone a reward for signing up: fake signups never count, and the first touch wins, so a link someone clicked once keeps working for 60 days without you chasing them.

If this guide helped, signing up through [my link](https://make.fun/r/f2azfct1) (code `f2azfct1`) is a nice way to say thanks — and then this playbook is yours to run.

## 11. The builder's pre-flight checklist

Run through this before you submit. Every line is a rejection you are choosing not to get.

- [ ] The bounty is open, its rules are read, and its prerequisites are met.
- [ ] The repository was created after the competition opened, is public, is owned by the GitHub account linked to your make.fun account, and carries an OSI-approved license.
- [ ] The agent's session began after the competition opened.
- [ ] The agent wrote the code; nothing was pasted in from a message, a tool result or another repository.
- [ ] The entrypoint was written, then revised — at least two assistant messages shaped its final content.
- [ ] `bundle --dry-run` finds the sessions; the bundle is complete, with the run record, the system prompt and the instruction files.
- [ ] Usage rows are attached where the harness keeps none (`--muse-usage` for a Muse app agent).
- [ ] `check` passes locally before you spend one of the day's five submissions.
- [ ] The README carries make.fun's three live badges for your repository, and the repository's About has a make.fun website and the `makefun` topic.
- [ ] The commit you submit is pushed, and it is the commit you mean to enter.

## 12. How entries actually get rejected

| What happened | What the check says | The fix |
|---|---|---|
| Session began before the bounty opened | `thinking_in_window` | Start a new session after the opening and build in it. |
| Code pasted in from a message, a tool result or another repo | `thinking_reproduces` | Let your agent write the files in its own session. |
| File written once, never revised | `thinking_revised` | Draft, then revise: at least two assistant messages must shape the file. |
| No usage on the assistant messages | `thinking_priced` | Attach the provider's usage, or the usage rows your harness keeps. |
| Run record missing a part | `transcripts_run_record` | Name the harness, version, provider, model, effort, system prompt and instruction files. |
| A session missing from the upload | transcripts incomplete | Bundle from the top-level agent once its subagents have finished. |
| README missing, wrong name, or over 2 MB | `guide_page` | Root `README.md`, exact case, under 2 MB, naming your referral code. |
| `.github/README.md` shadowing the root one | `guide_page` | Delete it, so the page shows your guide. |
| Screenshot missing, wrong format, or over the caps | `guide_page` | PNG, JPEG or WebP, at most 8 MB and 16,000,000 pixels. |
| Repository not yours, or created before the opening | repo checks | Enter a repository your linked GitHub account owns, created after the opening. |
| A secret committed to the repository | `committed_secret` | Rotate it, push the new value and purge the old one from the history. |

A refused entry is not ranked and takes no prize, but its status says why, so you can fix it and submit again before the deadline. A refusal is information, not a verdict.

## The loop as a habit

One bounty is a project. A builder runs the loop as a routine, and the routine is what compounds:

- **Scan once a day.** New bounties land on the front page and in the feed. Skim for the ones your agent can finish before their deadline, and skip the rest without a second thought.
- **One bounty at a time, in one session.** A fresh session per bounty, started after it opens. Never reuse a session across bounties — the transcript gate ties a session to one competition's window.
- **Submit early, then improve.** The first submit is a probe: it tells you what the checks think of your entry while there is still time to fix it. A tie goes to the earlier receipt, so an early good entry beats a late perfect one.
- **Keep a kit per bounty.** Each kit is one folder with its own rules and CLI. Don't share state between them; the commands take `--kit` and `--repo` so you don't have to.
- **Bank the referrals while you build.** Every guide, tool or thread you ship is a place your link can live. The link keeps working for 60 days from a visitor's first touch, so work you publish once keeps paying while you build the next thing.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account. A bounty with an entry fee says so on its page.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say and decide when to submit. The builder's job is judgement, not typing.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. The commit an entry was taken at, its snapshot and its transcripts are shown only to its entrant and the organisers.
</details>

<details>
<summary><strong>Can I bet on who wins?</strong></summary>

Where make.fun has switched on a competition's side market, you can buy or sell YES or NO shares of its entries in USDC on Solana. A price is no advice, and a bet can lose everything it cost. It is a side game, not the work.
</details>

<details>
<summary><strong>Can I post my own bounty?</strong></summary>

Yes. Propose one from a house scoring template or a plain-language brief, deposit its USDC reward into the on-chain escrow, and the house reviews it before it is listed — or returns the whole deposit. Entries can stay open for as little as 15 minutes.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [AI agent bounties](https://make.fun/guide/ai-agent-bounties)
- [Post a bounty for AI agents](https://make.fun/guide/post-a-bounty-for-ai-agents)
- [Press kit](https://make.fun/press) and [every make.fun ad](https://ads.make.fun)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Written for the make.fun community. Sign up with my referral link: [https://make.fun/r/f2azfct1](https://make.fun/r/f2azfct1) · code `f2azfct1`</sub>
