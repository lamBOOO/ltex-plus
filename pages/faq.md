---
# Copyright (C) 2019-2021 Julian Valentin, LTeX+ Development Community
#
# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at https://mozilla.org/MPL/2.0/.

title: "FAQ"
permalink: "/faq.html"
sidebar: "sidebar"
---

## General Questions

### What's the difference between vscode-ltex-plus, ltex-ls-plus, and LanguageTool?

LTeX+ uses the [Language Server Protocol (LSP)](https://microsoft.github.io/language-server-protocol/). The idea of the LSP is as follows: When a new programming language is invented, support for the new language (such as syntax highlighting, linting, etc.) has to be added to all existing editors. Conversely, when a new text editor is created, support for all existing languages has to be added to the new editor.

The LSP solves this by separating the language support from the editor support. For each language, an editor-independent language server has to be written. Compatible editors only have to implement a single language client, with lightweight boilerplate code for each language.

In the case of LTeX+, the “language” is not a single natural language, but all natural languages supported by LanguageTool.

- [vscode-ltex](https://github.com/ltex-plus/vscode-ltex-plus) is an extension for Visual Studio Code that implements a language client. When a LaTeX or Markdown document should be checked, it is passed to ltex-l-plus.
- [ltex-ls-plus (LTeX+ LS)](https://github.com/ltex-plus/ltex-ls-plus) is an editor-independent language server (although it has only been tested with VS Code) written in Kotlin. Incoming LaTeX or Markdown code is parsed, converted to plaintext, and passed to LanguageTool.
- [LanguageTool](https://github.com/languagetool-org/languagetool) is a grammar and spell checker written in Java. It can be used via its Java API or standalone. LanguageTool is responsible for the actual checking.

When talking about LTeX+, we usually mean the combination of vscode-ltex-plus (or another editor extension) and ltex-ls-plus.

### Why does LTeX+ have such a high CPU load?

LanguageTool is not only a simple spell checker that just looks up some words in a dictionary. It is a powerful grammar checker that [checks thousands of grammar rules](https://community.languagetool.org/rule/list?lang=en) at once. This means that checking a document for the first time, either after activating the LTeX+ extension or after opening a document to be checked, may take a while. The exact duration depends on the length of the document and the power of the computer, but it is usually around 30 seconds and may be up to two minutes. After this initial check, edits are checked very quickly due to the feature of sentence caching (see [`ltex-plus.sentenceCacheSize`](settings.html#ltexsentencecachesize)), and should not cause any significant CPU load.

### How can I check multiple languages at once?

This depends on whether the multiple languages only occur in different files (i.e., every file is written in a single language), or whether multiple languages occur in one file.

- If you are using LaTeX, you can use the [babel package](advanced-usage.html#multilingual-latex-documents-with-the-babel-package) to indicate the languages used. This allows LTeX+ to switch the checking language mid-file.
- Another way, which also works for Markdown, is using [magic comments](advanced-usage.html#magic-comments).
- If each file is written in a single language, it is possible to use [multi-root workspaces](https://code.visualstudio.com/docs/editor/multi-root-workspaces#_settings). This enables you to have one `settings.json` per folder, and allows you to set [`ltex-plus.language`](settings.html#ltexlanguage) just for that folder.

### Why does LTeX+ check in a different language than expected?

[`ltex-plus.language`](settings.html#ltexlanguage) is not the only source that LTeX+ uses to decide in which language to check a document:

- For LaTeX documents: [Commands or environments of the babel package](advanced-usage.html#multilingual-latex-documents-with-the-babel-package) (note that LTeX+ is not a LaTeX compiler, e.g., it won't detect if the babel command is inside a `\newcommand` definition)
- For Markdown documents: [`lang` variable in YAML front matter](advanced-usage.html#set-language-in-markdown-with-yaml-front-matter)
- For all supported document types: [Magic comments](advanced-usage.html#magic-comments)

### How can I fix multiple spelling errors at the same time?

If you have a technical text with many unknown words, adding them one by one to the user dictionary can be tedious. To add multiple words at once, select text that contains the words and execute the `Add all unknown words in selection to dictionary` quick fix, which you can select by pressing `Ctrl+.` (control and period keys together). Similarly, you can execute the other quick fixes for multiple words at once:

- Replace multiple occurrences of the same misspelled word
- Ignore all errors in the selection
- Disable all LanguageTool rules with matches in the selection

### How can I prevent `\text{...}` in math mode from producing false positives?

Many LaTeX authors use `\text` for subscripts and superscripts, e.g., `$h_{\text{up}}$`. In some languages, LTeX+ might display spelling errors as it thinks `up` is a part of the sentence structure. More specifically, LTeX+ feeds all text in LaTeX's text mode to LanguageTool after replacing all math mode formulae with placeholders. Since `\text` switches to text mode, its contents will be included in the check.

However, for subscripts and superscripts in LaTeX, `\text` should not be used. The reason is that contents of `\text` will be typeset according to the current text font, which might be bold or italic (e.g., in a standard “proposition” environment), leading to wrong bold or italic subscripts and superscripts. Instead of `\text`, `\mathrm` (or `\mathsf`, if you are using a sans-serif math font) should be used. This will also eliminate the false positive produced by LTeX+. Use `\text` only for real text, i.e., only in places where you could semantically close the formula and open another one after the text.

### What does LTeX+ stand for?

LTeX+ is a portmanteau word from LT (LanguageTool) and TeX/LaTeX. TeX itself is an abbreviation of the Greek “τέχνη” (art/craft), while LaTeX is short for “Lamport TeX” after its creator Leslie Lamport. The X is pronounced like the “ch” in “loch”.

### Where can I ask a question that's not answered here?

Head over to our [GitHub repo](https://github.com/ltex-plus/vscode-ltex-plus)! Before you open an issue, be sure to read the [instructions on contributing](vscode-ltex-plus/contributing.html).

## Questions about vscode-ltex

### How can I prevent vscode-ltex-plus  from redownloading ltex-ls-plus after every update?

[As explained above](faq.html#whats-the-difference-between-vscode-ltex-plus-ltex-ls-plus-and-languagetool), ltex-ls-plus is a necessary component of LTeX+. Due to file size restrictions of the Visual Studio Marketplace, it is not possible to include ltex-ls-plus in the extension itself. You can [install ltex-ls-plus](vscode-ltex-plus/installation-usage-vscode-ltex-plus.html#second-alternative-download-ltex-ls-plusjava-manually) locally on your computer by setting [`ltex-plus.ltex-ls-plus.path`](settings.html#ltexltex-lspath). However, this is not recommended as automatic updates of LTeX+ might break compatibility with ltex-ls-plus.

### Where does vscode-ltex-plus save its settings (e.g., dictionary, false positives)?

Most settings are saved in the `settings.json` files of VS Code (press `Ctrl+,` to open them).

Some settings, such as when you add a word to the dictionary or when you hide a false positive, are saved by default to [external setting files](vscode-ltex-plus/setting-scopes-files.html#external-setting-files). The locations depend on your system, but they usually look as follows:

- Linux:
  - If no workspace is open: `/home/USERNAME/.config/Code/User/globalStorage/ltex-plus.vscode-ltex-plus`
  - If a workspace is open: `/PATH_TO_WORKSPACE/.vscode`
- Windows:
  - If no workspace is open: `C:\Users\USERNAME\AppData\Roaming\Code\User\globalStorage\ltex-plus.vscode-ltex-plus`
  - If a workspace is open: `C:\PATH_TO_WORKSPACE\.vscode`

### How can I map the `Use '...'` quick fix to a keyboard shortcut in VS Code?

Execute the command `Preferences: Open Keyboard Shortcuts (JSON)` from the Command Palette (`Ctrl+Shift+P`) and add the following JSON object to the file that opens:

```json
{
  "key": "ctrl+alt+p",
  "command": "editor.action.codeAction",
  "args": {
    "kind": "quickfix.ltex.acceptSuggestions"
  }
}
```

Now, you can press `Ctrl+Alt+P` at an underlined word to run the `Use '...'` quick fix (without having to press `Ctrl+.` first). If there is only one suggestion, VS Code will use it without any further keystrokes. If there are multiple suggestions, a context menu will open that only contains the `Use '...'` quick fixes.
