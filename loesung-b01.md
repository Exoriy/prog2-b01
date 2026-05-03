# Lösung zu Blatt 01: Git Basics, Gradle

## 1. Git Status erklären

Die Ausgabe von `git status` beschreibt den aktuellen Zustand der lokalen Arbeitskopie.

```text
On branch b03
```

Das bedeutet, dass man sich aktuell auf dem Branch `b03` befinde.

```text
Changes not staged for commit:
    modified: CONTRIBUTING.md
    modified: homework/b03.md
```

Die Dateien `CONTRIBUTING.md` und `homework/b03.md` wurden verändert. Diese Änderungen sind aber noch nicht in der Staging Area. Sie würden also noch nicht in den nächsten Commit aufgenommen werden.

Git schlägt hier vor, dass man mit `git add <file>` Änderungen zur Staging Area hinzufügen kann. Mit `git restore <file>` könnte man Änderungen in der Working Copy wieder verwerfen.

```text
Untracked files:
    foo.java
```

Die Datei `foo.java` ist neu. Git kennt diese Datei noch nicht, weil sie bisher nicht getrackt wird. Sie ist also noch nicht Teil der Versionsverwaltung.

```text
no changes added to commit
```

Das bedeutet, dass aktuell keine Änderung für den nächsten Commit vorgemerkt ist. Die Staging Area ist leer.

Um nur die Datei `foo.java` zu committen, verwendet man folgende Befehle:

```bash
git add foo.java
git commit -m "Add foo.java"
```

Mit `git add foo.java` wird nur die Datei `foo.java` zur Staging Area hinzugefügt.

Mit `git commit -m "Add foo.java"` wird danach ein neuer Commit erzeugt, der nur diese Datei enthält.

Man verwendet hier bewusst nicht:

```bash
git add .
```

Denn dadurch würden möglicherweise auch andere Dateien zur Staging Area hinzugefügt.

Man verwendet außerdem nicht:

```bash
git commit -a
```

Denn `git commit -a` würde Änderungen an bereits getrackten Dateien automatisch committen. Dadurch könnten auch die Änderungen an `CONTRIBUTING.md` und `homework/b03.md` versehentlich in den Commit gelangen.