# Question 

I have installed dart version:

```sh
➜  craftinginterpreters git:(casiano) ✗ dart --version
Dart SDK version: 3.10.7 (stable) (Tue Dec 23 00:01:57 2025 -0800) on "macos_x64"
```
and then I tried `make get` for the Makefile of the munificent/craftinginterpreters repository. I assume it get the tools needed for building the book, but:

```
➜  craftinginterpreters git:(casiano) ✗ make get
Resolving dependencies... 
The lower bound of "sdk: '>2.11.0 <3.0.0'" must be 2.12.0'
or higher to enable null safety.

The current Dart SDK (3.10.7) only supports null safety.

For details, see https://dart.dev/null-safety
make: *** [get] Error 65
```

How can I fix this error?  Shall I install a lower version of dart? How?

# ChatGPT Answer

You’ve hit a **classic Dart ecosystem time-warp problem**, not a mistake on your side 👍
Short version: **your Dart is too new for that repo**.

Let’s unpack it and then I’ll give you **two clean fixes**, from “recommended” to “quick hack”.

---

## What’s going on (in plain English)

The `craftinginterpreters` repo includes some **Dart tooling** (for building the book) whose `pubspec.yaml` says something like:

```
sdk: '>2.11.0 <3.0.0'
```

That means:

* ❌ It explicitly **does NOT support Dart 3**
* ❌ It predates **null safety**
* ✅ It expects **Dart 2.12 – 2.19-ish**

Your Dart:

```
Dart SDK version: 3.10.7
```

Dart 3:

* **requires null safety**
* **refuses to run pre–null-safety packages**

So Dart is correctly saying:

> “I’m not going to run this ancient code.”

---

## ✅ Recommended fix: install an older Dart (side-by-side)

**Yes — you need an older Dart**, but **don’t downgrade your system Dart**.
Instead, install a **project-local Dart 2.19.x**.

### Option A: Using Homebrew (simplest on macOS)

Homebrew supports versioned Dart.

```bash
brew uninstall dart   # optional, only if you want
brew install dart@2.19
```

Then activate it:

```bash
brew link --force dart@2.19
```

Check:

```bash
dart --version
```

You should see something like:

```
Dart SDK version: 2.19.x
```

Now retry:

```bash
make get
```

✅ This usually works immediately.

---

### Option B (cleaner): Use a local Dart SDK (no system changes)

This is my **preferred “engineering” solution**.

1. Download Dart 2.19 SDK:

   ```bash
   curl -O https://storage.googleapis.com/dart-archive/channels/stable/release/2.19.6/sdk/dartsdk-macos-x64-release.zip
   ```

2. Unzip it:

   ```bash
   unzip dartsdk-macos-x64-release.zip
   ```

3. Use it *only* for this project:

   ```bash
   export PATH="$PWD/dart-sdk/bin:$PATH"
   ```

4. Verify:

   ```bash
   dart --version
   ```

5. Run:

   ```bash
   make get
   ```

📌 This keeps Dart 3 for everything else and avoids global breakage.

---

## ⚠️ Quick hack (not recommended, but works)

You *can* edit the SDK constraint to allow Dart 3:

```yaml
environment:
  sdk: '>=2.12.0 <4.0.0'
```

But:

* ❌ This **often breaks later**
* ❌ Some packages genuinely won’t run on Dart 3
* ❌ You’re fighting the repo instead of respecting it

I don’t recommend this unless you enjoy archaeology.

---

## Why the book hasn’t been updated

`craftinginterpreters`:

* is **intentionally frozen**
* targets **Dart 2-era tooling**
* focuses on language design, not Dart evolution

Bob Nystrom has explicitly avoided chasing SDK churn.

---

## TL;DR

✔️ **Yes, install an older Dart**
✔️ **Use Dart 2.19.x**
✔️ **Best solution: project-local SDK or Homebrew dart@2.19**
❌ Don’t try to force Dart 3

---

If you want, tell me:

* whether you’re building **HTML, PDF, or EPUB**
* and whether you plan to touch the **Dart code at all**

I can suggest a *minimal* setup that avoids Dart pain entirely 👌
