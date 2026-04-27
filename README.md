# BetterZip Translations

This repository contains the user-facing text for [BetterZip](https://macitbetter.com),
a macOS archive-management app. It exists so translators can update and improve
the translations without needing access to the main source code.

Thank you for helping!

## Languages

| Code | Language | Main app | Finder ext. | Quick Look | Share ext. | Automator |
|------|----------|:--------:|:-----------:|:----------:|:----------:|:---------:|
| en   | English (source) | ● | ● | ● | ● | ● |
| de   | German   | ● | ● | ● | ● |   |
| es   | Spanish  | ● | ● | ● | ● |   |
| fr   | French   | ● | ● | ● | ● |   |
| it   | Italian  | ● | ● | ● | ● | ● |
| ja   | Japanese | ● | ● | ● | ● | ● |
| pl   | Polish   | ● | ● | ● | ● | ● |
| pt   | Portuguese | ● | ● | ● | ● |   |
| sv   | Swedish  | ● | ● | ● | ● | ● |
| zh-Hans | Simplified Chinese | ● | ● | ● | ● |   |

English (`en.lproj`) is the source of truth. Please don't edit it.

## What to edit

Each language has folders named `<language>.lproj` spread across the repo:

- `locals/<lang>.lproj/` – main application window, menus, preferences,
  operation queue, password dialogs, etc.
- `FinderSyncExtension/<lang>.lproj/` – the Finder right-click menu and badge
  labels
- `Quick Look Extension/<lang>.lproj/` – the Quick Look preview panel
- `Compress with BetterZip/<lang>.lproj/` – the share-sheet extension
- `Automator/.../Base.lproj/` plus siblings – Automator preset actions

Inside each `.lproj` folder you'll typically find:

- `Localizable.strings` – most of the UI text
- `InfoPlist.strings` – app name, file-format descriptions, permission prompts
- One or more `<ControllerName>.strings` – text bound to specific dialogs via
  Interface Builder
- `Credits.rtf` – the "About BetterZip" credits (only where applicable)
- `defaults.plist` – translated default values for some preferences

## `.strings` file format

Classic macOS `.strings` files look like this:

```
/* A user-visible comment explaining context. */
"KEY_OR_ENGLISH_STRING" = "Translation here";

/* Another entry. */
"Could not open %@: %@" = "Konnte %@ nicht öffnen: %@";
```

Rules:

- **Keys** (left of `=`) must stay **exactly** as they are – never translate
  them.
- **Values** (right of `=`) are what you translate.
- Every line ends with a **semicolon** `;` and every string is in **double
  quotes**.
- Keep **placeholders** (`%@`, `%d`, `%1$@`, `%2$d`, `%lld`, …) in the
  translation. You may reorder them (e.g. `%2$@ / %1$@`) but must never drop
  one or change its type.
- Preserve escape sequences: `\n` newline, `\"` literal quote, `\\`
  backslash.
- The file encoding for `.strings` files is typically UTF-16 with BOM –
  **please don't re-save them as UTF-8** from a plain editor, as that can
  break the build. Xcode handles encoding automatically.

`Credits.rtf` files use Rich Text; edit them in TextEdit or Xcode (not a
plain-text editor) to preserve the formatting.

## Recommended editors

- **Xcode** – best option if you have a Mac; opens `.strings` files with
  syntax highlighting and never messes up encodings
- **BBEdit / Sublime Text / VS Code** – fine for `.strings` if you make sure
  the file encoding round-trips correctly (stay on UTF-16 if that's what the
  file uses)
- **TextEdit** – works for `Credits.rtf`; avoid it for `.strings` because it
  silently rewrites encoding

## Contribution workflow

Most translators are invited as **collaborators**, which means you can edit and
push changes directly without forking. If you'd like to be added, email
me with your GitHub username.

### The easy way – GitHub Desktop (recommended)

No command line needed.

1. Install [GitHub Desktop](https://desktop.github.com) and sign in with your
   GitHub account.
2. Choose **File → Clone Repository…**, switch to the **URL** tab, and paste:
   `https://github.com/macitbetter/BetterZip-Localization.git`
3. Pick a folder on your Mac and click **Clone**.
4. Edit files in your language's folders (Xcode is best for `.strings` files).
5. Back in GitHub Desktop you'll see your changes listed. Type a short summary
   (e.g. *"Update German: preferences pane"*), click **Commit to main**, then
   **Push origin**.

That's it – your changes are live on GitHub.

### Using Xcode

Xcode can also clone and push without the command line:

1. **Source Control → Clone…**
2. Paste `https://github.com/macitbetter/BetterZip-Localization.git` and choose
   a folder.
3. After editing, use **Source Control → Commit…** then **Source Control →
   Push…**.

### Using the command line

If you're comfortable with a terminal:

```bash
git clone https://github.com/macitbetter/BetterZip-Localization.git
cd BetterZip-Localization
# …edit files…
git commit -am "Update <lang>: <brief description>"
git push
```

The SSH URL `git@github.com:macitbetter/BetterZip-Localization.git` also works
if you've set up an SSH key on your GitHub account.

### Contributing from outside (no collaborator access)

If you haven't been added as a collaborator, you can still contribute via a
pull request:

1. Click **Fork** in the top-right of the
   [GitHub page](https://github.com/macitbetter/BetterZip-Localization) to
   create your own copy.
2. Clone *your fork* using any of the methods above.
3. Edit, commit, and push to your fork.
4. On GitHub, click **Contribute → Open pull request** to send your changes
   back.

Please keep each pull request focused on a single language when possible – it
makes review much faster.

## What has changed since the last release

The tag `v5.4.2` marks the strings as they shipped in BetterZip 5.4.2 (the
previous public release). To see exactly what English strings were changed,
added, or removed since then:

```bash
git diff v5.4.2..main -- '**/en.lproj/*' '**/Base.lproj/*.strings'
```

…and to see your own prior translations alongside (so you can tell which of
them need a fresh look):

```bash
git diff v5.4.2..main -- '**/de.lproj/*'      # substitute your language code
```

New or removed files are shown as additions/deletions in the diff. A handful
of files (for example `InfoPlist.strings` and the Setapp variant) only have
their current content in the baseline – they may show no diff even if they
changed, because the 5.4.2 export did not capture them separately. The bulk
of the user-visible text is covered.

## Reporting issues

- **Missing string** – a UI element you can't find a key for: open an issue
  with a screenshot and we'll figure out where it lives.
- **Ambiguous English source** – the English text is unclear: open an issue
  tagged `source-clarification`.
- **Bug in the app** – please report on the main BetterZip site, not here.

## License

Content in this repository is available under the [CC-BY-4.0](LICENSE) license
so contributors retain attribution and the text remains freely reusable.

