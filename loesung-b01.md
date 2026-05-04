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

---

## 2. Git-Spiel

Zuerst das Git-Quest-Repository klonen und auf dem Branch `master` arbeiten:

```bash
git clone https://github.com/Programmiermethoden-CampusMinden/prog2_ybel_gitquest.git
cd prog2_ybel_gitquest
git checkout master
git log --oneline
```

Die Bezeichnungen wie `tag 01`, `tag 04.5` usw. sind in dieser Aufgabe die Commit-Meldungen in der Git-Historie.

### 2.1 Was passierte an `tag 01`?

Befehl:

```bash
git show 4aa8014
```

Antwort:

An `tag 01` betritt Markus den Dungeon. Er trägt ein Schwert und eine leichte Rüstung. Kurz danach trifft er auf die ersten Monster, nämlich rattenähnliche Wesen.

In diesem Commit wurde die Datei `questlog.md` geändert. An tag 01 beginnt die Geschichte.


### 2.2 Wann hat der Held zum ersten Mal 4 `experience` Punkte?

Befehle:

```bash
git log --oneline -- stats.md
git show 590fc86 -- stats.md
```

Antwort:

Der Held hat zum ersten Mal bei `tag 01.3` 4 `experience` Punkte.

Commit:

```text
590fc86 tag 01.3
```

In diesem Commit wird in `stats.md` der Wert für `experience` auf `4` gesetzt:

```markdown
| experience | 4 |
```


### 2.3 Wann hat der Held zum ersten Mal 10 `hunger` Punkte?

Befehle:

```bash
git log --oneline -- stats.md
git show 78f1f49 -- stats.md
```

Antwort:

Der Held hat zum ersten Mal bei `tag 02` 10 `hunger` Punkte.

Commit:

```text
78f1f49 tag 02
```

In diesem Commit steht in `stats.md`:

```markdown
| hunger | 10 |
```


### 2.4 Wie viele Heiltränke hat der Held insgesamt in seinem Rucksack gehabt?

Befehle:

```bash
git log --oneline -- rucksack.md
git show ec66cfc -- rucksack.md
git show 13834cd -- rucksack.md
git show 8f88b19 -- rucksack.md
```

Antwort:

Der Held hatte insgesamt `2 Heiltränke` in seinem Rucksack.

Der erste Heiltrank kommt bei `tag 03.14` in den Rucksack.

Commit:

```text
ec66cfc tag 03.14
```

Später wird dieser Heiltrank bei `tag 03.17` wieder entfernt, weil Markus ihn trinkt.

Commit:

```text
13834cd tag 03.17
```

Ein weiterer Heiltrank kommt bei `tag 04.4` in den Rucksack.

Commit:

```text
8f88b19 tag 04.4
```

Damit hatte Markus insgesamt zwei Heiltränke im Rucksack.


### 2.5 Was hat der Held im Shop gekauft? Und wie viel Gold hat er dafür bezahlt?

Befehle:

```bash
git log --oneline -- rucksack.md
git show 4ff8726 -- rucksack.md shopkeeper.md hero.md
git show ec66cfc -- rucksack.md shopkeeper.md hero.md
```

Antwort:

Der Held kauft im Shop zwei Dinge:

| Commit | Gegenstand | Preis |
|---|---:|---:|
| `tag 03.9` | `1 Brot` | `5 Gold` |
| `tag 03.14` | `1 Heiltrank` | `5 Gold` |

Insgesamt bezahlt er also `10 Gold`.

Begründung:

Bei `tag 03.9` wird aus `10 Gold` im Rucksack `5 Gold` und `1 Brot`. Deshalb kostet das Brot `5 Gold`.

Bei `tag 03.14` wird aus `5 Gold` im Rucksack ein Heiltrank. Deshalb kostet der Heiltrank ebenfalls `5 Gold`.


### 2.6 Was passierte zwischen `tag 03` und `tag 04`?

Befehle:

```bash
git log --oneline
git diff 2ffebcf..39568d5
git show 2ffebcf -- stats.md rucksack.md questlog.md
git show 39568d5 -- stats.md rucksack.md questlog.md
```

Antwort:

Zwischen `tag 03` und `tag 04` geht Markus in den Shop. Dort kauft er Brot und einen Heiltrank. Danach isst er das Brot und trinkt den Heiltrank. Dadurch ist er nicht mehr hungrig und seine Gesundheit wird wiederhergestellt.

Wichtige Änderungen:

| Datei | Bei `tag 03` | Bei `tag 04` |
|---|---|---|
| `stats.md` | `health = 5`, `hunger = 10` | `health = 10`, `hunger = 0` |
| `rucksack.md` | `10 Gold` | leerer Rucksack |
| `questlog.md` | Markus beginnt mit dem Zwerg zu verhandeln | Markus setzt die Quest erfrischt und gestärkt fort |

Die `experience` Punkte bleiben in diesem Abschnitt unverändert.


### 2.7 Hat der Held etwas gegessen? Falls ja, was und wann?

Befehle:

```bash
git show 13834cd
git show 13834cd -- hero.md rucksack.md stats.md
```

Antwort:

Ja, der Held hat etwas gegessen. Bei `tag 03.17` isst Markus Brot. In `hero.md` steht, dass Markus auf dem harten Brot kaut.

Commit:

```text
13834cd tag 03.17
```

In diesem Commit verschwinden `1 Brot` und `1 Heiltrank` aus dem Rucksack. Außerdem ändern sich die Werte in `stats.md`:

```text
health: 5 -> 10
hunger: 10 -> 0
```

Das bedeutet: Markus isst das Brot und trinkt den Heiltrank. Danach ist er nicht mehr hungrig und seine Gesundheit ist wiederhergestellt.
