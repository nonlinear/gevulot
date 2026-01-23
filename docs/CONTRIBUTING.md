# CONTRIBUTING

How we build Gevulot.

---

> 🤖
>
> [CHANGELOG](CHANGELOG.md) - What we did
> [ROADMAP](ROADMAP.md) - What we wanna do
> [CONTRIBUTING](CONTRIBUTING.md) - How we do it (you are here)
> [CHECKS](CHECKS.md) - What we accept
>
> [/whatsup](../.github/prompts/whatsup.prompt.md) - The prompt that keeps us sane
>
> 🤖

---

## Quick Start

**Contributing in 3 steps:**

1. **Pick an epic** from [ROADMAP](ROADMAP.md)
2. **Create a branch:** `git checkout -b v0.X-feature-name`
3. **Before merge:** Run `/whatsup` (see [whatsup.prompt.md](../.github/prompts/whatsup.prompt.md))

---

## Branch Strategy

**One branch per epic:**

```
main (stable releases only)
  ↓
v0.2.0-core-contact-card (feature branch)
v0.3.0-group-permissions (feature branch)
v0.4.0-automatic-propagation (feature branch)
```

### Branch Naming

**Format:** `v{major}.{minor}.{patch}-{feature-name}` (or `v{major}.{minor}-{feature-name}` for first iteration)

**Examples:**

- `v0.2.0-core-contact-card` (first patch of v0.2)
- `v0.2-core-contact-card` (shorthand when patch=0)
- `v0.3.0-group-permissions`
- `v1.0.0-decentralized-sync`

**Semantic Versioning applies:**

- Use `v0.2.0` when creating the epic branch
- Bump to `v0.2.1` for hotfixes on that epic
- Minor (`v0.3.0`) for new features
- Major (`v1.0.0`) for breaking changes

---

## Epic/Branch Workflow ("Epic Dance")

1. **Create branch from main:**

   ```bash
   git checkout main
   git pull origin main
   git checkout -b v0.2.0-core-contact-card
   ```

2. **Link branch in ROADMAP.md:**

   ```markdown
   > **v0.2.0**
   > [🚧](https://github.com/user/gevulot/tree/v0.2.0-core-contact-card) **Core Contact Card**
   >
   > First working version with self-owned contact cards.
   >
   > - [ ] iOS app scaffold (Flutter)
   > - [ ] "Me Card" claim flow
   ```

3. **Work on feature with regular commits:**

   ```bash
   git add .
   git commit -m "feat: implement Me Card claim flow"
   git push origin v0.2.0-core-contact-card
   ```

4. **Stay current - rebase from main regularly:**

   ```bash
   git checkout main
   git pull origin main
   git checkout v0.2.0-core-contact-card
   git rebase main
   git push --force-with-lease origin v0.2.0-core-contact-card
   ```

   **Why rebase?**
   - Keeps linear history
   - Easier to review
   - Cleaner when merging back to main

   **When to rebase?**
   - Daily if main is active
   - Before creating PR
   - After major main updates

5. **Before merging - use `/whatsup`:**

   ```bash
   # Run pre-commit workflow (does steps 6-7 automatically)
   # See .github/prompts/whatsup.prompt.md
   ```

   **The `/whatsup` workflow will:**
   - ✅ Run all CHECKS (see [CHECKS.md](CHECKS.md))
   - ✅ Update ROADMAP (mark completed checkboxes)
   - ✅ Move epic to CHANGELOG (if complete)
   - ✅ Bump version number (semantic versioning)
   - ✅ Generate commit message

6. **Merge to main when epic complete:**

   ```bash
   git checkout main
   git pull origin main
   git merge v0.2.0-core-contact-card --no-ff

   # Tag the release
   git tag v0.2.0 -m "Epic v0.2.0: Core Contact Card complete"

   git push origin main
   git push origin v0.2.0
   ```

7. **Delete feature branch (recommended):**

   ```bash
   # Local
   git branch -d v0.2.0-core-contact-card

   # Remote (optional - keeps history clean)
   git push origin --delete v0.2.0-core-contact-card
   ```

   **Branch deletion policy:**
   - ✅ **DO delete** after successful merge (keeps branch list clean)
   - ✅ Git history preserved via tags
   - ✅ Can recreate from tag if needed: `git checkout -b v0.2.0-core-contact-card v0.2.0`
   - ❌ **DON'T delete** if you plan to make hotfixes on that version

8. **Announce release (optional):**
   - Update [README.md](../README.md) if needed
   - Post in Signal/Discord/wherever
   - Tweet/share if public release

---

## Epic Format

> 🤖 **AI: Use this syntax when writing epics in ROADMAP or CHANGELOG**

**Syntax:**

```markdown
### v0.X.0

#### Epic Title

[commit](link) ← ROADMAP: only if branch exists | CHANGELOG: always (merge commit)

Epic description (what problem does this solve?)

- [ ] Task to complete (roadmap only)
- [x] Completed task (roadmap only)
- Completed task (changelog only, in past tense)

❌ Anti-pattern (what NOT to do)
✅ Best practice (with link if applicable)
🗒️ Note

---
```

**Link rules:**

- **ROADMAP**: `[commit](branch-url)` if branch exists, nothing if planned
- **CHANGELOG**: `[commit](merge-commit-url)` always points to main

**Examples:**

```markdown
### v0.3.0

#### Delta Indexing

[commit](https://github.com/user/repo/tree/v0.3.0-delta-indexing)

Automatic change detection for incremental book indexing

- [x] Detect filesystem changes
- [ ] Auto-reindex affected topics

✅ Use folder_path from metadata for accuracy
❌ Don't parse topic_id with string splitting
```

Automatic change detection for incremental book indexing

- [x] Detect filesystem changes
- [ ] Auto-reindex affected topics

✅ Use folder_path from metadata for accuracy
❌ Don't parse topic_id with string splitting

````

---

## Epic Development Strategy

**Each epic = one feature branch:**

- Branch naming: `v{major}.{minor}.{patch}-{feature-name}` (ex: `v0.3.0-group-permissions`)
- Regular rebase from `main` to stay current
- When complete → merge to `main` → move to CHANGELOG.md

**When epic completes:**

1. Run `/whatsup` (marks checkboxes, validates checks)
2. Move entire epic from ROADMAP → CHANGELOG
3. Change status: `🚧` → `✅`
4. Merge branch to main with `--no-ff`
5. Tag release: `git tag v0.3.0 -m "Epic v0.3.0 complete"`
6. Delete feature branch (recommended, history preserved via tags)
7. Announce release

---

## Semantic Versioning

**For Gevulot:**

| Type      | Version Change  | Example                        | Breaking? |
| --------- | --------------- | ------------------------------ | --------- |
| **Patch** | v0.2.0 → v0.2.1 | Bug fixes, minor tweaks        | No        |
| **Minor** | v0.2.x → v0.3.0 | New features (backward compat) | No        |
| **Major** | v0.x → v1.0     | Breaking changes               | Yes       |

**Examples:**

- **Patch:** Bug fixes, typos, minor corrections
  - `fix: correct contact sync edge case`
  - `fix: handle nil pointer in propagation`

- **Minor:** New features, backward compatible
  - `feat: add group permissions system`
  - `feat: implement grey rock mode`

- **Major:** Breaking changes, architecture changes
  - `feat!: migrate to decentralized backend (BREAKING)`
  - `refactor!: change contact storage format`

---

## Rebase vs Merge

**Use rebase for:**

- ✅ Keeping feature branch current with main
- ✅ Cleaning up local history before pushing
- ✅ Maintaining linear git history

**Use merge for:**

- ✅ Integrating completed features into main
- ✅ Preserving complete feature development history
- ✅ Creating clear version boundaries

**Never rebase:**

- ❌ Public/shared branches after others have pulled
- ❌ Main branch itself
- ❌ After a branch has been merged

**Rebase conflicts?**

```bash
# During rebase, if conflicts occur:
git status                    # See conflicting files
# Fix conflicts in editor
git add <resolved-files>
git rebase --continue

# If rebase gets messy:
git rebase --abort           # Start over
````

---

## Commit Messages

**Format:**

```
<type>: <subject>

[optional body]
[optional footer]
```

**Types:**

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation only
- `refactor:` Code restructuring (no feature change)
- `test:` Adding tests
- `chore:` Maintenance (dependencies, build, etc.)

**Examples:**

```
feat: add group permissions system
fix: resolve contact propagation bug
docs: update ROADMAP with v0.3 epic
refactor: simplify permission checking logic
```

---

## Pre-Commit Workflow

**ALWAYS run before merging to main:**

1. **Use `/whatsup` prompt** (see [../.github/prompts/whatsup.prompt.md](../.github/prompts/whatsup.prompt.md))
2. **Check CHECKS.md** for stability requirements
3. **Update ROADMAP** - mark completed checkboxes
4. **Move to CHANGELOG** - if epic complete
5. **Run all tests** - ensure nothing broke (when tests exist)

---

## Status Files Location

Check [README](../README.md) for navigation block pointing to:

- **CHANGELOG**: `/docs/CHANGELOG.md`
- **ROADMAP**: `/docs/ROADMAP.md`
- **CHECKS**: `/docs/CHECKS.md`
- **CONTRIBUTING**: `/docs/CONTRIBUTING.md`
