# DHG508 Critical Digital History

Course workspace, Term 1 2026-27, Lingnan University.

Everything for the course starts here. You will fork this repository and work in your own copy.

---

## Before class on Wednesday, 9 September

Five things. Budget about an hour. Bring the laptop you actually work on.

### 1. Install opencode

opencode is the terminal coding agent we will use in class.

Terminal version, recommended:

```bash
curl -fsSL https://opencode.ai/install | bash
```

Other ways to install it: `brew install anomalyco/tap/opencode` on macOS, `scoop install opencode` or `choco install opencode` on Windows, `npm install -g opencode-ai` anywhere Node is already installed. On Windows the smoothest setup is inside WSL.

If the terminal feels like too much for now, the desktop version is fine to start with: https://opencode.ai/download

It works when you can type `opencode` in a terminal and the agent starts.

### 2. Get a model behind it

opencode is only the interface. The model is a separate subscription, and you need one.

- If you already pay for Codex or Claude, use that. Do not buy anything else.
- If you do not, subscribe to opencode go, US$10 a month, cancel any time: https://opencode.ai/go

### 3. Register three accounts

- GitHub: https://github.com
- OpenRouter: https://openrouter.ai
- DeepSeek: https://platform.deepseek.com

Free registration is enough. You do not need to add credit before class.

### 4. Install VS Code and GitHub Desktop

- VS Code: https://code.visualstudio.com
- GitHub Desktop: https://desktop.github.com

### 5. Fork this repository, then clone it with opencode

1. Fork this repository using the Fork button at the top right of this page. The copy that appears under your own account is yours.
2. Open a terminal and start `opencode`.
3. Ask it, in your own words:

   > Explain how GitHub works and what I need in order to use it. My fork is at [paste the URL of your fork]. Walk me through cloning it to my computer, and tell me what each step is actually doing.

4. Let the agent do the work, but make it explain while it works. Ask again whenever an answer stays vague.
5. Open the cloned folder in VS Code. You should see this README.
6. Add the same folder in GitHub Desktop, so you can watch your own changes.

Clone your fork, not this repository. That difference is the whole point of step 1.

Bring to class: the cloned folder on your laptop, one thing the agent explained that you did not know, and one thing you still do not understand. The second one is the more useful of the two.

If something breaks, stop after thirty minutes, take a screenshot of the error, and bring it in. We will look at it together.

---

## What is in this repository

- `templates/project_template/` the structure every project in this course starts from: `research/`, `sources/`, `artifacts/`, `code/`
- `projects/` where your own work will live, one folder per project
- `skills/` research doctrine you can hand to an agent
- `AGENTS.md` the rules an agent follows inside this workspace
- `WORKSPACE.md` how the pieces fit together and how to start a project

Nothing here needs to be read before Wednesday. We will open it together in class.
