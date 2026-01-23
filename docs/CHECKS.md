# CHECKS

Stability requirements before any commit. ALL checks must pass.

---

## Truth Triangle: Conversation ↔ System ↔ Docs

Every commit must validate 3 sources are in sync:

1. **Conversation** (chat history, commit messages) → New ideas
2. **System** (actual code/files) → What exists
3. **Status Files** (ROADMAP/CHANGELOG) → What's documented

**Conflicts to detect:**

- 💬 Conversation has ideas → Not in ROADMAP = undocumented plans
- 💻 System has code → Not in ROADMAP/CHANGELOG = undocumented features
- 📋 ROADMAP has checkboxes → Code doesn't exist = broken promises

---

## For AI: Automated Test Sequence

Run this before every commit:

```bash
#!/bin/bash

echo "🔍 Running Gevulot stability checks..."

# 1. Documentation exists
echo ""
echo "1️⃣ Documentation check..."
if [[ -f "README.md" && -f "docs/ROADMAP.md" && -f "docs/CHANGELOG.md" ]]; then
    echo "✅ Core docs exist"
else
    echo "❌ Missing required documentation"
    exit 1
fi

# 2. README has navigation block
echo ""
echo "2️⃣ README navigation check..."
if grep -q "🤖" README.md; then
    echo "✅ README has navigation block"
else
    echo "❌ README missing 🤖 navigation block"
    exit 1
fi

# 3. Truth Triangle: Conversation ↔ System ↔ Docs
echo ""
echo "3️⃣ Truth Triangle validation..."

# 3A. System → Docs (code exists but undocumented?)
if [[ -n $(git status --porcelain) ]]; then
    CHANGED_FILES=$(git diff --name-only)
    echo "   💻 System changes: $CHANGED_FILES"

    # Check if work is tracked in ROADMAP
    if grep -q "🚧" docs/ROADMAP.md; then
        echo "   ✅ Changes tracked in ROADMAP (🚧 epic exists)"
    else
        echo "   ❌ FAIL: Code changes without epic in ROADMAP"
        echo "   → Add epic to ROADMAP before committing"
        exit 1
    fi
else
    echo "   ✅ No uncommitted system changes"
fi

# 3B. Docs → System (promises kept?)
echo ""
echo "4️⃣ Promised features verification..."

COMPLETED_COUNT=$(grep -c "- \[x\]" docs/ROADMAP.md 2>/dev/null || echo "0")

if [[ $COMPLETED_COUNT -gt 0 ]]; then
    echo "   📋 ROADMAP shows $COMPLETED_COUNT completed items"
    echo "   ⚠️  AI: Verify these features exist in codebase"

    # Example: check if Flutter project exists when ROADMAP mentions it
    if grep -q "Flutter\|iOS app" docs/ROADMAP.md && [[ ! -f "pubspec.yaml" ]]; then
        echo "   ❌ ROADMAP mentions Flutter but pubspec.yaml missing"
        exit 1
    fi
else
    echo "   ✅ No completed items to verify yet"
fi

# 3C. Conversation → Docs (recent commits should match ROADMAP)
echo ""
echo "5️⃣ Conversation sync (recent commits vs ROADMAP)..."

LAST_COMMITS=$(git log --oneline -5 --pretty=format:"%s" 2>/dev/null || echo "")

if [[ -n "$LAST_COMMITS" ]]; then
    echo "   💬 Recent work:"
    echo "$LAST_COMMITS" | sed 's/^/      - /'
    echo "   ℹ️  AI: Ensure these align with ROADMAP epics"
else
    echo "   ✅ No commit history yet (new repo)"
fi

echo ""
echo "✅ All checks complete."
```

---

> 🤖
>
> - [README](../README.md) - What is Gevulot
> - [CHANGELOG](CHANGELOG.md) - What we did
> - [ROADMAP](ROADMAP.md) - What we wanna do
> - [CONTRIBUTING](CONTRIBUTING.md) - How we do it
> - [CHECKS](CHECKS.md) - What we accept
> - [/whatsup](../.github/prompts/whatsup.prompt.md) - The prompt that keeps us sane
>
> 🤖

### Code Quality (when code exists)

- [ ] App runs without crashes
- [ ] No compilation errors
- [ ] Tests pass (when tests exist)
- [ ] Code follows style guide

### Version Control

- [ ] Meaningful commit messages
- [ ] No sensitive data in commits
- [ ] Branch names follow convention (if applicable)

---

## Adding New Checks

When the project grows, add checks here:

```bash
# Example: Flutter app checks
flutter analyze
flutter test
dart format --output=none --set-exit-if-changed .
```

---

> 🤖
>
> - [README](../README.md) - What is Gevulot
> - [CHANGELOG](CHANGELOG.md) - What we did
> - [ROADMAP](ROADMAP.md) - What we wanna do
> - [CONTRIBUTING](CONTRIBUTING.md) - How we do it
> - [CHECKS](CHECKS.md) - What we accept
> - [/whatsup](../.github/prompts/whatsup.prompt.md) - The prompt that keeps us sane
>
> 🤖

---

**Last updated:** 2026-01-23
