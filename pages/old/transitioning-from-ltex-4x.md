---
# Copyright (C) 2019-2021 Julian Valentin, LTeX Development Community
#
# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at https://mozilla.org/MPL/2.0/.

title: "Transitioning from LTeX 4.x"
permalink: "/old/transitioning-from-ltex-4x.html"
sidebar: "sidebar"
---

LTeX has undergone a major rewrite in version 5.0. The most important change is that it now comes with everything included:

- All languages are now directly included in LTeX, which eliminates the need for language support extensions (e.g., `LTeX - English support`). If you still have any of them installed, you may uninstall them now.
- Due to file size restrictions of the Visual Studio Marketplace, LTeX has to download its core component (which includes LanguageTool) when activated for the first time. Read below for instructions on offline installation.
- A separate Java installation is not necessary anymore. LTeX will automatically download a Java distribution and store it in the extension folder if no suitable Java installation (Java 8 or later) has been found on your computer.
- A few settings have been renamed. Check your `settings.json` for deprecated entries.

Find more information in the [changelog](../vscode-ltex-plus/changelog.html).
