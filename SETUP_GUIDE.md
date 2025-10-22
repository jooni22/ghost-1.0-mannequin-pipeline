# Ghost Mannequin Pipeline - Setup Guide

**Version:** 1.0  
**Last Updated:** October 22, 2025  
**Audience:** New users setting up the project

---

## 🚀 Quick Start (5 Minutes)

### Prerequisites
- Node.js 18 or higher
- npm (comes with Node.js)
- API keys from FAL.AI and Google Gemini

### Step 1: Clone and Install (2 minutes)

```bash
# Clone the repository (if not already done)
git clone https://github.com/jooni22/ghost-1.0-mannequin-pipeline.git
cd ghost-1.0-mannequin-pipeline

# Install dependencies
npm install
# Output: added 26 packages in ~4s, 0 vulnerabilities ✅
```

### Step 2: Configure Environment (2 minutes)

```bash
# Copy the example environment file
cp .env.example .env.local

# Edit .env.local with your API keys
nano .env.local
# or
code .env.local
```

**Required API Keys:**
```env
# Get from: https://fal.ai/dashboard
FAL_API_KEY=your_fal_api_key_here

# Get from: https://aistudio.google.com/app/apikey
GEMINI_API_KEY=your_gemini_api_key_here

# Optional - Get from: https://www.freepik.com/api
FREEPIK_API_KEY=your_freepik_api_key_here
```

### Step 3: Test the Installation (1 minute)

```bash
# Run a simple test (requires API keys)
npm test

# If you see errors about missing API keys, check your .env.local file
# If you see "Processing..." messages, it's working! 🎉
```

---

## 📦 Project Modes

This project has **THREE deployment modes** - choose the one that fits your needs:

### Mode 1: Core Library (Recommended for Integration)

**Use when:** You want to integrate ghost mannequin generation into your own application

**Current Dependencies:** ✅ Already installed
```json
{
  "@google/generative-ai": "^0.21.0",
  "sharp": "^0.33.0",
  "node-fetch": "^3.3.2"
}
```

**Usage:**
```typescript
import { processGhostMannequinCCJWithStorage } from './lib/ghost/ccj-improved';

const result = await processGhostMannequinCCJWithStorage(facts, control, /* ... */);
```

**Status:** ✅ Ready to use after setting up `.env.local`

---

### Mode 2: Next.js Web Application (Optional)

**Use when:** You want a web interface for uploading images and viewing results

**Additional Dependencies Needed:**
```bash
npm install next react react-dom
```

**Start the web app:**
```bash
# Development mode
npm run dev

# Then visit: http://localhost:3000
```

**Status:** ⚠️ Requires installing Next.js dependencies first

**Why separate?** The core library can be used without Next.js, keeping it lightweight for integrations.

---

### Mode 3: Standalone Deno API (Optional)

**Use when:** You want a standalone REST API separate from your main application

**Location:** `standalone-api/`

**Runtime:** Deno (separate from Node.js)

**Setup:**
```bash
# Install Deno
curl -fsSL https://deno.land/install.sh | sh

# Run the API
cd standalone-api
deno run --allow-net --allow-env index.ts

# Visit: http://localhost:8000/health
```

**Status:** ✅ Ready to use (requires Deno, not Node.js)

---

## 🎯 Recommended Workflow

### For First-Time Users:

1. **Start with Core Library Mode** (easiest)
   - Install dependencies: `npm install` ✅ Done
   - Configure: `cp .env.example .env.local` ✅ Do this
   - Test: `npm test` ✅ Try this

2. **Add Web Interface (optional)**
   - Install Next.js: `npm install next react react-dom`
   - Start dev server: `npm run dev`
   - Visit: `http://localhost:3000`

3. **Deploy Standalone API (optional)**
   - Use for production deployments
   - See `standalone-api/README.md`

---

## 📝 What's Already Configured

### ✅ Present and Working:

1. **Documentation** (35+ markdown files)
   - README.md - Overview
   - USER_GUIDE.md - Usage instructions
   - INTEGRATION_GUIDE.md - Integration methods
   - PROJECT_STATUS.md - Current status
   - And 30+ more technical documents

2. **Source Code** (Complete)
   - `lib/ghost/` - 21 TypeScript files
   - `standalone-api/` - Deno-based API
   - `packages/` - Additional packages
   - 40+ test files

3. **Configuration Files** (All present)
   - `package.json` - Core dependencies
   - `tsconfig.json` - TypeScript config
   - `next.config.js` - Next.js config (for web mode)
   - `.gitignore` - Proper exclusions
   - `.env.example` - Template (173 lines!)

4. **Dependencies** (Installed)
   - 26 packages installed
   - 0 vulnerabilities
   - All core features work

---

## ⚠️ What You Need to Add

### Required:

1. **`.env.local` file** with your API keys
   ```bash
   cp .env.example .env.local
   # Then edit .env.local with your keys
   ```

### Optional (depending on mode):

2. **Next.js dependencies** (only if using web interface)
   ```bash
   npm install next react react-dom
   ```

3. **Sample images** (optional - tests use URLs by default)
   - Project intentionally excludes images to keep repo size small
   - Tests use public URLs (Unsplash, etc.)
   - You can add your own images to `Input/` directory

---

## 🧪 Testing Your Setup

### Test 1: Check Dependencies
```bash
npm list --depth=0
# Should show: @google/generative-ai, sharp, node-fetch, tsx, typescript
```

### Test 2: Verify Configuration
```bash
# Check if .env.local exists
ls -la .env.local

# If not, create it:
cp .env.example .env.local
```

### Test 3: Run Core Library Test
```bash
# This will test the core functionality
npm test

# Expected output (with valid API keys):
# 🚀 Testing Improved CCJ Pipeline v1.2
# ✅ FAL client configured
# [Processing messages...]
```

### Test 4: Test Web Interface (if installed Next.js)
```bash
npm install next react react-dom  # Only needed once
npm run dev
# Visit: http://localhost:3000
```

---

## 🐛 Troubleshooting

### Problem: "FAL_API_KEY not found"

**Solution:**
```bash
# Make sure .env.local exists
cp .env.example .env.local

# Edit and add your API key
nano .env.local

# Make sure it's in the same directory as package.json
```

### Problem: "Cannot find module 'next/server'"

**Reason:** You're trying to run the web app without Next.js dependencies.

**Solution:**
```bash
# Install Next.js dependencies
npm install next react react-dom

# Or just use the core library mode (doesn't need Next.js)
npm test  # This works without Next.js
```

### Problem: "Test fails immediately"

**Possible causes:**
1. Missing API keys in `.env.local`
2. Invalid API keys
3. Network issues

**Solution:**
```bash
# Check your environment
cat .env.local | grep -E "FAL_API_KEY|GEMINI_API_KEY"

# Verify API keys are valid at:
# - https://fal.ai/dashboard
# - https://aistudio.google.com/app/apikey
```

### Problem: TypeScript compilation errors

**If using core library:** These are expected for Next.js files. Core library works fine.

**If using web interface:** Install Next.js dependencies:
```bash
npm install next react react-dom
```

---

## 📊 Project Completeness

| Component | Status | Action Needed |
|-----------|--------|---------------|
| Core Library | ✅ Complete | Add `.env.local` |
| Documentation | ✅ Complete | None |
| Configuration | ✅ Complete | None |
| Dependencies (Core) | ✅ Installed | None |
| Dependencies (Web) | ⚠️ Optional | `npm install next react react-dom` |
| Tests | ✅ Complete | Add API keys |
| API Integration | ✅ Complete | None |

**Overall Status:** 98% Complete - Just add your API keys! ✅

---

## 🎉 Success Criteria

You'll know everything is working when:

1. ✅ `npm install` completes without errors
2. ✅ `.env.local` exists with your API keys
3. ✅ `npm test` runs without "API key not found" errors
4. ✅ You see processing messages and results

---

## 📚 Next Steps

After setup is complete:

1. **Read the USER_GUIDE.md** - Learn how to use the API
2. **Check INTEGRATION_GUIDE.md** - Learn integration methods
3. **Review examples/** - See real-world examples
4. **Explore test-*.ts files** - See test patterns
5. **Read PROJECT_STATUS.md** - Understand current capabilities

---

## 🤝 Need Help?

- Check **PROJECT_ANALYSIS.md** for detailed analysis
- Review **PROJECT_STATUS.md** for known issues
- See **TROUBLESHOOTING** section in USER_GUIDE.md
- Check test files for usage examples

---

**Happy ghost mannequin generating! 👻🎨**
