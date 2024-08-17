---
# Copyright (C) 2019-2021 Julian Valentin, LTeX Development Community
#
# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at https://mozilla.org/MPL/2.0/.

title: "Commands"
permalink: "/vscode-ltex/commands-de.html"
sidebar: "sidebar"
---

Change language of this page: [English](commands.html), [German](commands-de.html)

<!-- ltex: language=de-DE -->

Um einen Befehl auszuführen, öffnen Sie die Befehlspalette (`Ctrl+Shift+P`) und beginnen Sie mit der Eingabe des Befehlsnamens.

## `LTeX: Aktiviere Erweiterung`

Aktiviert die Erweiterung; macht nichts, falls die Erweiterung bereits aktiviert ist.

Die Erweiterung wird automatisch aktiviert, wenn Dateien mit unterstützten Code-Sprachmodi (= Voreinstellung von [`ltex.enabled`](../settings-de.html#ltexenabled)) im Editor geöffnet werden. Benutzen Sie diesen Befehl, wenn Sie LTeX für Dateien mit nicht unterstützten Code-Sprachmodi benutzen möchten.

## `LTeX: Auswahl prüfen`

Löst eine Prüfung der primären Auswahl des aktiven Dokuments aus und löscht alle durch LTeX gemeldeten Schreibfehler im aktiven Dokument außerhalb der primären Auswahl.

Das aktive Dokument ist dasjenige, dessen Editor momentan den Fokus besitzt, oder, falls kein Editor den Fokus besitzt, welches als letztes geändert wurde.

Es ist normalerweise nicht nötig, diesen Befehl auszuführen, da LTeX alle unterstützten Dokumente prüft, wenn sie geöffnet oder geändert werden.

## `LTeX: Aktuelles Dokument prüfen`

Löst eine Prüfung des aktiven Dokuments aus.

Das aktive Dokument ist dasjenige, dessen Editor momentan den Fokus besitzt, oder, falls kein Editor den Fokus besitzt, welches als letztes geändert wurde.

Es ist normalerweise nicht nötig, diesen Befehl auszuführen, da LTeX alle unterstützten Dokumente prüft, wenn sie geöffnet oder geändert werden.

## `LTeX: Alle Dokumente im Arbeitsbereich prüfen`

Löst eine Prüfung aller Markdown- und LaTeX-Dokumente im Arbeitsbereich aus.

Dies führt eine Suche nach Dateien mit typischen Endungen der Dateitypen in allen Ordnern des Arbeitsbereiches durch, je nachdem, für welche Dateitypen LTeX aktiviert wurde (siehe [`ltex.enabled`](../settings-de.html#ltexenabled)). Unbenannte und ungespeicherte Dokumente werden nicht überprüft. Die Dokumenttypen werden anhand der Dateinamen-Erweiterungen erkannt. Um die Überprüfung von bestimmten Dateien oder Ordnern zu überspringen, fügen Sie sie zu `files.exclude` hinzu.

Die Dokumente müssen in der UTF-8-Kodierung vorliegen. Dies funktioniert nicht, falls keine Ordner im Arbeitsbereich geöffnet sind.

## `LTeX: Schreibfehler in aktuellem Dokument löschen`

Löscht alle durch LTeX gemeldeten Schreibfehler im aktiven Dokument.

Das aktive Dokument ist dasjenige, dessen Editor momentan den Fokus besitzt, oder, falls kein Editor den Fokus besitzt, welches als letztes geändert wurde.

## `LTeX: Alle Schreibfehler löschen`

Löscht alle durch LTeX gemeldeten Schreibfehler.

## `LTeX: Statusinformationen zeigen`

Zeigt Informationen über den aktuellen Status von LTeX im Protokoll `LTeX Language Client`.

Informationen über ltex-ls werden nur angezeigt, wenn ltex-ls gerade läuft und nicht ein Dokument überprüft.

## `LTeX: Zurücksetzen und neu starten`

Setzt den aktuellen Zustand der Erweiterung zurück und startet LTeX LS neu.

Dies ist äquivalent dazu, das Fenster von VS Code neuzuladen und die Erweiterung zu aktivieren. Benutzen Sie diesen Befehl, falls sich LTeX nicht wie erwartet verhält.

## `LTeX: Bug in LTeX melden`

Zeigt eine Meldung an, die einen Link zu Anweisungen über wie man Bugs in LTeX meldet und einen Knopf zum Kopieren eines Bug-Berichts enthält.

Wenn der Knopf gedrückt wird, dann kopiert LTeX einen vorausgefüllten Bug-Bericht in die Zwischenablage, die anschließend in das GitHub-Problem eingefügt werden kann.

## `LTeX: Feature in LTeX wünschen`

Erstellt einen neuen Feature-Wunsch für LTeX, indem die GitHub-Webseite geöffnet wird.
