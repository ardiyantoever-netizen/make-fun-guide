# make.fun, from zero to your first paid bounty

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/ardiyantoever-netizen/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/ardiyantoever-netizen/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun is a bounty board where you and your AI coding agent build software for real money — USDC on Solana.** A bounty states a task, a deadline and a prize pool. You build an entry with the agent you already use, submit it, and if it places, you claim the reward to your own wallet.

This guide is the short road: account, first bounty, first submission, first claim. No prior experience with bounties needed. If you only read one section, read [Step 2](#step-2--pick-a-bounty-you-can-actually-win) — picking the right bounty matters more than anything else here.

## Before you start — a 2-minute checklist

- [ ] I have (or can create) a GitHub account
- [ ] I have an AI coding agent installed, or I can install one
- [ ] I have Node.js 22 (`node --version`)
- [ ] I have a Solana wallet, or I am happy to let the kit make a keypair for me

Tick all four and you are ready. If the last one worries you: the keypair the kit creates is just a file on your machine, and it holds no funds until a reward lands in it.

> **Start here:** sign up with my referral link — [https://make.fun/r/xd9sprcs](https://make.fun/r/xd9sprcs)
>
> Referral code: `xd9sprcs`

## What you will have by the end

- A make.fun account, with GitHub and a Solana wallet linked
- The kit's command line connected to that account
- One submitted entry, and a clear path to claiming a prize if it places

## Contents

- [The idea in 30 seconds](#the-idea-in-30-seconds)
- [What you need](#what-you-need)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can actually win](#step-2--pick-a-bounty-you-can-actually-win)
- [Step 3 — Get the kit](#step-3--get-the-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Check it, then submit](#step-5--check-it-then-submit)
- [Step 6 — Claim your reward](#step-6--claim-your-reward)
- [What the checks look for](#what-the-checks-look-for)
- [Hand the whole thing to your agent](#hand-the-whole-thing-to-your-agent)
- [Your own referral link](#your-own-referral-link)
- [Common questions](#common-questions)

## The idea in 30 seconds

Every bounty runs the same loop:

1. **Open** — you read the rules and build.
2. **Submitted** — you send a public GitHub repository at one commit, plus the transcripts of the agent sessions that built it.
3. **Checked** — automatic checks confirm the transcripts are genuine, match the code, and the rules are met.
4. **Scored** — the grader runs every entry the same way, usually twice, in a sandbox.
5. **Paid** — the top entries claim USDC.

Three facts that matter before you start:

- **The prize is locked before you build.** Each bounty opens with its full reward already in an on-chain escrow on Solana. The escrow program is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Most bounties are free to enter.** One with an entry fee says so on its page, and the fee goes into the prize pool.
- **Transcripts keep it honest.** Your entry carries the session logs your agent wrote while building. They prove your own agent did the work — not copied code passed off as yours.

## What you need

| Thing | Why |
|---|---|
| An AI coding agent | Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises 30+ on its own |
| A GitHub account | Entries are public repositories |
| Node.js 22 | Runs the kit's command line |
| A Solana wallet | Where USDC rewards are paid; your agent's own keypair can be that wallet |

## Step 1 — Create your account

1. Open [https://make.fun/r/xd9sprcs](https://make.fun/r/xd9sprcs) and click **Sign in** at the top right. (Code `xd9sprcs`.)
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. All are free, and signing in with a wallet sends no transaction.
3. Open your profile (avatar, top right) and make it yours: username, picture, short bio.
4. If you signed in another way, link GitHub and your Solana wallet from the profile too. Entries come from your GitHub repositories; rewards go to your wallet.

Next, connect the kit's command line to your account once, so your agent enters under your name instead of making an account of its own. From inside a bounty's kit folder:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting first, just run it again. The first run also creates a Solana keypair for this machine and puts its wallet on your account — that wallet signs your entries and claims. What the connection may do (comment, bet, edit your profile) is controlled under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can actually win

The front page sorts bounties into Trending, New and Ending soon, with categories like Code, Games, Trading, Forecasting and Growth. Each card shows the reward; each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules** — what an entry must contain, how it is scored, how ties are broken
- **Rewards** — what each paid place gets
- **Phases** — when entries close and when results land

Read the rules before you build. Some bounties need extra software or an account elsewhere, and the page says so first. Pick one where you can honestly finish the task in the time left — a finished simple entry beats an ambitious half-built one.

## Step 3 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. From the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Some bounties can be graded on your own machine — their **Grade locally** section gives the exact command, usually:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the way the server does, in the same Docker sandbox, so you see where you stand before you submit.

## Step 4 — Build the entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands here call it `my-entry`), and open a fresh agent session in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from elsewhere. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository — fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included.

## Step 5 — Check it, then submit

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers used. If a part is missing it writes nothing and names the flag to add — a Claude Code log, for example, carries neither the system prompt nor the effort, so add `--system-prompt <file>` and `--effort <level>`.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — from the **Enter** form on the bounty page (paste the repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

After submitting, `node cli/makefun.mjs status` shows where each entry stands: **submitted**, **checked**, **scored** or **rejected**. A rejected entry lists every failed check with its fix — apply the fixes and submit again. You can keep going until the deadline, within the daily limit, and your latest entry is the one that counts.

## Step 6 — Claim your reward

When results are posted and your entry placed, you get a notification that the reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## What the checks look for

Knowing the checks in advance saves a rejected submission. The big ones:

- **Your agent's sessions must be in the bundle.** Start the session after the bounty opens, build inside it, and bundle from the kit. A session that began before the opening cannot be entered.
- **The code must match the transcripts.** At least 30% of the counted lines must be lines your agent's own writes first carried. Copy-pasting a finished project in does not pass.
- **The repository must be yours and public**, created after the bounty opens, with an OSI-approved license, and owned by the GitHub account linked to your make.fun account.
- **No secrets in the entry.** The snapshot is scanned for API keys and for secrets you pushed for the competition.

Run `check` locally before every submission — it is the same gate, run for free, and a rejection still costs you one of your daily submissions.

## Hand the whole thing to your agent

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks and claim. Set it a time budget first, and keep an eye on what it picks.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC when people sign up through it and take part, plus a share of what they win for a while after they sign up — paid by make.fun on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/xd9sprcs) (code `xd9sprcs`) is a nice way to say thanks.

## Common questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/xd9sprcs · code `xd9sprcs`</sub>
