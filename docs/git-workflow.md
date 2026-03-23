# Git Workflow for Katagami

> How to manage version control when building a design system, especially in AI-assisted environments.

---

## Branch Strategy

```
main
 └─ dev (primary working branch)
      └─ concept/design-system (ALL DS changes here)
```

### Rules
- DS work happens ONLY in `concept/design-system`
- `dev` is the integration branch — merge DS via PR
- Never commit DS changes directly to `dev` or `main`
- PR review ensures quality gate before integration

---

## File Boundary Discipline

**Only touch these paths in the DS branch:**

```
✅ src/components/ds/          ← Component code
✅ src/app/demo/               ← Showcase/demo pages
✅ globals.css                  ← Token definitions
✅ tailwind.config.*           ← Token extensions
✅ src/components/ds/index.ts  ← Barrel exports

❌ src/app/ (non-demo pages)   ← Other developers' territory
❌ src/lib/                     ← Shared utilities
❌ src/api/                     ← Backend routes
❌ package.json                 ← Only if adding DS-specific deps
```

**Result:** Zero merge conflicts across the entire DS development lifecycle. Tested across 40+ components and 100+ commits.

---

## Commit Convention

```
feat(ds): add date picker molecule — 3 variants
fix(ds): correct status badge colors per UIDD §4.2
refactor(ds): remove thin wrapper organisms (DsList, DsGrid)
chore(ds): update showcase page layout
docs(ds): add component usage examples
```

### Commit Message Format
```
<type>(ds): <what changed> — <scope/count if relevant>
```

### Commit Frequency
| When | Action |
|------|--------|
| After completing a Block | Commit all Block components |
| After fixing review issues | Batch commit all fixes |
| Before ending session | Commit work-in-progress |
| After showcase updates | Include in same commit as component |

---

## Workaround: virtiofs Mount Limitation

If you're working in a VM where the mounted filesystem doesn't support `unlink` (common with virtiofs in Cowork, Lima, etc.):

### Symptoms
- `git checkout` fails with `unable to unlink` errors
- `git commit` fails because `.lock` file can't be removed
- `rm` fails on `.git/index.lock`

### Solution: Git Worktree on Local Disk

```bash
# 1. Create worktree on local (non-mounted) disk
cd /tmp
git clone --branch concept/design-system /mnt/project ds-worktree
cd ds-worktree

# 2. Make changes here (local disk = full POSIX support)
# Edit, add, commit, push — all works normally

# 3. After commit, sync back to mount
rsync -av --exclude='.git' /tmp/ds-worktree/ /mnt/project/

# 4. Clean up
rm -rf /tmp/ds-worktree
```

### Alternative: Move Lock Files
```bash
# If .git/index.lock exists and can't be deleted:
mv .git/index.lock /tmp/index.lock.bak
# Then retry your git command
```

---

## PR Workflow

### Creating a DS PR
```bash
# Push DS branch to remote
git push -u origin concept/design-system

# Create PR targeting dev
gh pr create \
  --base dev \
  --title "feat(ds): Block 2 — 11 Atoms with showcase" \
  --body "## Summary
- 11 Atom components (DsButton, DsInput, DsCheckbox, etc.)
- Interactive showcase page at /demo/design-system
- All tokens applied, zero hardcoded values
- npm run build: 0 errors

## Verification
Open localhost:3000/demo/design-system to see all components"
```

### Review Checklist for PR Reviewer
- [ ] No files outside `src/components/ds/` and `src/app/demo/`
- [ ] Zero TS errors (`npm run build`)
- [ ] All tokens from CSS variables (no hardcoded hex)
- [ ] Showcase page renders all components
- [ ] No hallucinated features (compare against UIDD)

---

## Illustrations: Bulk Commit

When adding illustrations (SVGs), commit them in a single batch:

```bash
git add public/illustrations/*.svg
git commit -m "feat(ds): add 15 illustrations — unDraw style, navy palette"
```

SVGs are text files, so diffs are readable. Large batches (50+ files) may have large line counts — this is expected.

---

## Recovery: Common Git Issues

| Issue | Command |
|-------|---------|
| Stuck `.lock` file | `mv .git/index.lock /tmp/` |
| Branch behind remote | `git pull --rebase origin concept/design-system` |
| Accidental commit to wrong branch | `git cherry-pick <hash>` to correct branch, then `git reset HEAD~1` on wrong one |
| Untracked files after branch switch | Ignore — git doesn't track them, they're virtiofs artifacts |
| Remote not found | Authenticate via `gh auth login` or verify remote URL with `git remote -v` |
