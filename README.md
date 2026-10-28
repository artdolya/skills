# Skills

Reusable agent skills, maintained in Git so they can be backed up, used across
computers, and shared individually. Edit skills in this checkout, then commit and
push changes; installed copies are not the source of truth.

## Available skills

| Skill | Purpose | Requirements |
| --- | --- | --- |
| [prompt-architect](skills/prompt-architect/SKILL.md) | Create, improve, or evaluate prompts and reusable instruction templates. | A compatible agent; no scripts, API keys, or external tools required. |

Example after installation:

```text
$prompt-architect Improve this prompt for clarity and make the output format explicit: …
```

## Repository layout

```text
.
├── README.md
├── .gitattributes
├── .gitignore
└── skills/
    └── prompt-architect/
        ├── SKILL.md
        └── agents/
            └── openai.yaml
```

Keep each skill in `skills/<skill-name>/`, with its own `SKILL.md`. Its YAML
frontmatter must include `name` and `description`. Add `references/`, `scripts/`,
or `assets/` inside that folder only when needed. `agents/openai.yaml` contains
Codex-specific UI metadata.

Keep every skill self-contained: use relative paths within its folder and avoid
dependencies on sibling skills or repository-level files. Individual installation
copies only the chosen folder. Document any required tools or configuration in
the skill, and keep credentials and computer-specific paths out of it.

`README.md` holds the catalog and maintenance instructions. `.gitignore` excludes
local settings, credentials, backups, and generated files. `.gitattributes` keeps
Markdown, YAML, and scripts in LF format across operating systems. Do not commit
machine-specific symlinks or a copy of your entire Codex home directory.

## Prerequisites and discovery

Use a current Codex client with local skill support. Git is needed to maintain a
checkout; access to this repository is needed to download it. `prompt-architect`
itself needs no Python, API key, MCP server, or personal Codex configuration.

The shell examples below use Bash on macOS, Linux, or WSL. Run them in the
environment where Codex loads skills: WSL and native Windows have separate homes.
In native Windows PowerShell, use `$HOME` or `$env:USERPROFILE` for that user's
home, and copy directories with `Copy-Item -Recurse`. Do not reuse another
laptop's absolute paths.

Verified on 2026-10-28 against the
[official skills documentation](https://learn.chatgpt.com/docs/build-skills):

| Scope | Discovery location |
| --- | --- |
| User | `~/.agents/skills/` |
| Repository | `.agents/skills/` in each directory from the working directory up to the repository root |
| Administrator | `/etc/codex/skills/` |
| System | Skills bundled with Codex |

Codex follows symlinked skill folders. This repository's plain `skills/` folder
stores source files; cloning it alone does not install them. Codex normally
detects changes automatically; restart it if a skill or update does not appear.

The bundled `skill-installer` inspected for this setup defaults to
`$CODEX_HOME/skills` (or `~/.codex/skills` when unset), and supports an explicit
destination. This differs from the current documentation's user path above.
Check both locations when migrating an existing installation, plus any
project-local install. Keep one active installation of a given skill per
environment; identical names are not merged.

## Install only prompt-architect

Once this skill has been committed and pushed to `master`, ask **inside Codex**:

```text
$skill-installer Install only skills/prompt-architect from https://github.com/artdolya/skills/tree/master/skills/prompt-architect into my user ~/.agents/skills directory. Preserve any existing installation and its local edits.
```

The URL uses this checkout's existing GitHub remote and branch. For a fork, use
`https://github.com/<OWNER>/<REPOSITORY>/tree/<REF>/skills/prompt-architect`.
Use a tag or commit for a fixed version. Only the selected skill folder is
installed, including `agents/openai.yaml`; repository settings are not installed.

The bundled installer makes a copy and refuses to overwrite an existing
destination. Copies do not follow Git updates. Use the update procedure below
when replacing one. If the installer is unavailable, copy from a checkout as
described next.

Invoke the installed skill with the `$prompt-architect` example above. It can
also be selected automatically when a request matches its existing description.

## Use across your own computers

On each macOS, Linux, or WSL environment where Codex runs, clone the repository
once. Skip cloning if you already have this checkout:

```bash
mkdir -p "$HOME/sources"
git clone https://github.com/artdolya/skills.git "$HOME/sources/skills"
cd "$HOME/sources/skills"
```

For your maintained checkouts, a local symlink makes edits and pulls immediately
available to Codex. First reconcile any existing installation as described
below, then run from the repository root:

```bash
skill_dest="$HOME/.agents/skills/prompt-architect"
if [ -e "$skill_dest" ] || [ -L "$skill_dest" ]; then
  echo "Already installed: compare and back up this destination first."
else
  mkdir -p "$HOME/.agents/skills" &&
    ln -s "$PWD/skills/prompt-architect" "$skill_dest"
fi
```

Recreate the link locally on each laptop. Moving the checkout requires updating
the link; switching branches also changes the active skill. A link is best when
you want to use the version you are editing.

For recipients, or when you prefer a stable installed snapshot, use a copy.
Use the same guarded block above, replacing the `ln -s` line with:

```bash
    cp -R ./skills/prompt-architect "$skill_dest"
```

Copies are also the simplest choice for native Windows when symlink permissions
are inconvenient. From a Windows checkout, a fresh install in PowerShell is:

```powershell
$skillDest = Join-Path $HOME '.agents/skills/prompt-architect'
if (Test-Path -LiteralPath $skillDest) { throw 'Compare and back up the existing install first.' }
New-Item -ItemType Directory -Force (Split-Path $skillDest) | Out-Null
Copy-Item -Recurse -LiteralPath './skills/prompt-architect' -Destination $skillDest
```

## Edit, validate, and back up

Before editing, check for local work and pull the latest commits. Commit or stash
your existing changes first; if a fast-forward fails, reconcile the divergence
before retrying. Do not force-reset local work.

```bash
git status --short
git pull --ff-only
```

Edit `skills/prompt-architect/` in the repository. If you need a new branch, use
`git switch -c artdolya/<change-name>` and push that branch deliberately.

Before committing:

- Check YAML frontmatter has `name` and `description`, and the name matches the
  folder. Parse `agents/openai.yaml` after metadata edits.
- Check supporting links stay within the skill and point to existing files.
- If your installed `skill-creator` includes `scripts/quick_validate.py`, run it
  with this skill folder as the argument using Python with PyYAML installed.
  Resolve its location from that laptop's installed creator; do not vendor it.
- Try a representative request after behavioral changes. Structural validation
  alone does not establish prompt quality.
- Review the intended files for private material; ignore rules do not detect all
  secrets or remove files that Git already tracks.

For the initial backup, stage only these files, inspect the staged changes, then
commit and push. Run from the repository root:

```bash
git add README.md .gitignore .gitattributes skills/prompt-architect/SKILL.md skills/prompt-architect/agents/openai.yaml
git diff --cached --check
git diff --cached
git commit -m "Back up prompt-architect and document skill maintenance"
git push -u origin HEAD
```

For later changes, stage only the relevant files and use a descriptive commit
message. A local copy or commit is not an off-laptop backup until pushed.
On another laptop, pull the same published branch with `git pull --ff-only`.
Linked installs then reflect the checkout; copied installs need replacement.

## Existing installs, updates, and restoration

Before replacing an installed copy, set `installed_skill` to its actual path and
compare it with the repository copy:

```bash
installed_skill="$HOME/.agents/skills/prompt-architect"
git diff --no-index --ignore-space-at-eol -- "$installed_skill" ./skills/prompt-architect
```

This comparison ignores trailing whitespace, including CRLF differences; exit
status 1 means differences were found. Check errors separately. Merge any wanted
local edits into the repository, validate, and commit them before replacement.
For a symlink, check its target and that checkout's Git status instead: the
installed skill may already be the same files you are editing.

Move the old installation **outside all skill discovery directories** after
reviewing it. Renaming it to `prompt-architect-old` inside a skill directory can
leave it discoverable. This Bash example keeps a uniquely named backup:

```bash
mkdir -p "$HOME/skill-backups" &&
  skill_backup=$(mktemp -d "$HOME/skill-backups/prompt-architect.XXXXXX") &&
  mv "$installed_skill" "$skill_backup/prompt-architect"
```

If the old installation is a symlink, this moves only the link; preserve its
target checkout and uncommitted changes too. For a copy, the backup contains the
old files. In PowerShell, use `Move-Item` to a new folder outside discovery paths.

Now install a fresh copy or link using the guarded steps above (or rerun the
installer). Replacing the entire folder also removes stale files from the active
version. Avoid copying into an existing directory, which can nest the skill or
leave deleted resources behind. If installation fails, move the backup back to
its original, now-empty path.

To restore a lost laptop, clone the repository and reinstall or relink the
selected folders. To restore an earlier skill revision, first preserve current
work, find the desired commit with `git log -- skills/prompt-architect`, then run:

```bash
git restore --source=<COMMIT> -- skills/prompt-architect
```

Review, validate, and commit that restoration; push it and update other laptops
normally. Git can restore only work that was committed, and another laptop can
retrieve only work that was pushed.

## Adding and sharing skills

- Use lowercase, hyphenated folder names matching the skill's `name`.
- Add the skill to the table above with its purpose and requirements.
- Check frontmatter, referenced files, and any scripts; try a representative
  request before sharing a changed workflow.
- Keep private or company-specific skills in a separate private repository.
- For an existing skill, copy its complete folder into an unused
  `skills/<skill-name>/` destination, preserving instructions, metadata,
  resources, and license notices; compare with the original before committing.

## Plugin packaging and licensing

Direct folder installation is sufficient initially for your laptops and people
who want one selected skill. OpenAI recommends plugins for reusable distribution
and directory discovery. Consider that when you need a discoverable listing or
an intentionally bundled set of skills.

A minimal portable plugin can add a root `plugin.json` and reuse this `skills/`
layout; an MCP server is optional. A root plugin packages the skill collection,
so distribute a package containing only the intended skill(s) when selection
matters. Consult the current
[plugin packaging guide](https://developers.openai.com/plugins/build/plugins)
when needed. No plugin manifest, installer, synchronization service, or release
pipeline is needed for the initial Git workflow.

No license was found in the repository or the original `prompt-architect` skill.
The owner still needs to choose the reuse, modification, and redistribution
terms before offering it for reuse; this setup does not select a license.
Preserve upstream licenses and attribution when importing others' work. Once
terms are chosen, keep the applicable license and notices inside each separately
installed skill folder so they travel with it; a repository-level license alone
would not be copied by an individual-skill install.

The initial `prompt-architect` import preserves its existing instructions and UI
metadata, with line endings normalized for cross-platform Git use.
