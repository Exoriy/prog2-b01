# Lösung zu Blatt 01: Git Basics, Gradle

## 1. Git Status erklären

Die Ausgabe von `git status` zeigt den aktuellen Zustand der Arbeitskopie.

`On branch b03` bedeutet, dass ich mich auf dem Branch `b03` befinde.

Die Dateien `CONTRIBUTING.md` und `homework/b03.md` wurden verändert, aber noch nicht zur Staging Area hinzugefügt.

Die Datei `foo.java` ist neu und wird von Git noch nicht getrackt.

Um nur `foo.java` zu committen, verwende ich:

```bash
git add foo.java
git commit -m "Add foo.java"