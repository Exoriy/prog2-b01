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



---

## 3. Letzten Commit `tag 04.5` ändern

Beim letzten Commit `tag 04.5` wurden versehentlich zu wenig `experience` Punkte eingetragen. Deshalb ändere ich den letzten Commit mit `git commit --amend`.

Vorher stand in `stats.md`:

```markdown
| experience | 40 |
```

Ich ändere den Wert auf:

```markdown
| experience | 42 |
```

Befehle:

```bash
git checkout master
notepad stats.md
git diff
git add stats.md
git commit --amend --no-edit
```

Mit `git commit --amend --no-edit` wird der letzte Commit geändert, aber die Commit-Meldung `tag 04.5` bleibt erhalten.

Danach überprüfe ich die Änderung mit:

```bash
git log --oneline -5
type stats.md
```


---

## 4. Neuer Commit `tag 04.6`

Für `tag 04.6` ändere ich nur die Datei `questlog.md`.

Neuer Text am Ende von `questlog.md`:

```markdown
Markus hörte in der Ferne ein leises Klingeln. Vorsichtig folgte er dem Geräusch durch einen schmalen Gang und entdeckte eine alte, verfallene Steintreppe, die noch tiefer in das Dungeon führte.
```

Befehle:

```bash
git status
notepad questlog.md
git diff --stat
git add questlog.md
git commit -m "tag 04.6"
```

Mit `git diff --stat` überprüfe ich vorher, dass wirklich nur `questlog.md` geändert wurde.



---

## 5. Neuer Commit `tag 04.7`

Für `tag 04.7` führe ich die Geschichte weiter fort. Diesmal ändere ich mehrere Dateien in einem gemeinsamen Commit, weil die Änderungen inhaltlich zusammengehören.

Änderung in `questlog.md`:

```markdown
Am Fuße der Treppe stand Markus plötzlich einen Boss gegenüber. Der Kampf war kurz, aber heftig. Markus ging als Sieger hervor, erlitt jedoch leichte Verletzungen und entdeckte in der Nähe ein Schlüssel.
```

Änderung in `stats.md`:

```markdown
| health | 7 |
| experience | 45 |
| hunger | 2 |
```

Begründung:

- Markus wurde im Kampf verletzt, deshalb sinkt `health`.
- Markus gewinnt den Kampf, deshalb steigt `experience`.
- Die Reise geht weiter, deshalb steigt `hunger`.

Änderung in `rucksack.md`:

```markdown
| 1 | 1 Schlüssel |
```

Befehle:

```bash
git status
notepad questlog.md
notepad stats.md
notepad rucksack.md
git diff --stat
git add questlog.md stats.md rucksack.md
git commit -m "tag 04.7"
```

Mit `git diff --stat` überprüfe ich, dass die drei gewünschten Dateien geändert wurden. Danach werden alle drei Änderungen gemeinsam in einem Commit gespeichert.



---

## 6. Neuer Commit `tag 04.8`: Ausrüstung aus `stats.md` auslagern

Bisher stehen Statuspunkte und Ausrüstung gemeinsam in `stats.md`. Das ist unübersichtlich. Deshalb verschiebe ich die Ausrüstung in eine neue Datei `gear.md`.

Vorher enthält `stats.md` auch:

```markdown
| weapon | sword (3 dmg) |
| armor | light (2 dmg) |
```

Diese Zeilen entferne ich aus `stats.md`.

Danach enthält `stats.md` nur noch die Statuswerte:

```markdown
# Stats

| Property | Value |
|------------|---------------|
| health | 7 |
| experience | 45 |
| hunger | 2 |
```

Neue Datei `gear.md`:

```markdown
# Gear

| Property | Value |
|------------|---------------|
| weapon | sword (3 dmg) |
| armor | light (2 dmg) |
```

Befehle:

```bash
git status
notepad stats.md
notepad gear.md
git add stats.md gear.md
git commit -m "tag 04.8"
git log --oneline -8
```

Durch diesen Commit sind Statuswerte und Ausrüstung getrennt. `stats.md` enthält nur noch Werte wie `health`, `experience` und `hunger`. Die Ausrüstung steht jetzt in `gear.md`.



---

## 7. Gradle-Projekt über die Konsole

Ich habe über die Konsole ein neues Gradle-Projekt für eine Java-Applikation erstellt.

Dafür habe ich zuerst einen neuen Ordner angelegt:

```bash
cd D:\aLearning\prog2
mkdir prog2-gradle-demo
cd prog2-gradle-demo
```

Danach habe ich das Gradle-Projekt mit `gradle init` erzeugt:

```bash
gradle init --type java-application --dsl groovy --test-framework junit-jupiter --project-name prog2-gradle-demo --package prog2.demo
```

Bei den Rückfragen habe ich folgende Optionen gewählt:

```text
Java version: 25
Application structure: Single application project
Generate build using new APIs and behavior: no
```

Nach der Erstellung habe ich nicht mehr den global installierten Gradle-Befehl `gradle`, sondern den Gradle Wrapper verwendet:

```bash
.\gradlew
```

Der Gradle Wrapper ist wichtig, weil dadurch das Projekt mit einer passenden Gradle-Version gebaut werden kann, auch wenn auf einem anderen Rechner Gradle nicht global installiert ist.

---

### 7.1 Verfügbare Gradle-Tasks anzeigen

Mit folgendem Befehl habe ich die verfügbaren Tasks angezeigt:

```bash
.\gradlew tasks
```

Dabei wurden unter anderem folgende Tasks angezeigt:

| Task | Bedeutung |
|---|---|
| `run` | startet die Anwendung |
| `build` | baut das Projekt und führt Tests aus |
| `test` | führt die Tests aus |
| `clean` | löscht generierte Build-Dateien |
| `jar` | erzeugt eine JAR-Datei |
| `javadoc` | erzeugt die API-Dokumentation |

Für eine ausführlichere Liste kann man verwenden:

```bash
.\gradlew tasks --all
```

---

### 7.2 Anwendung starten

Die Anwendung habe ich mit folgendem Befehl gestartet:

```bash
.\gradlew :app:run
```

Die Ausgabe war:

```text
Hello World!
```

Damit ist gezeigt, dass die Java-Anwendung erfolgreich gebaut und gestartet werden kann.

---

### 7.3 Tests ausführen

Die Tests habe ich mit folgendem Befehl ausgeführt:

```bash
.\gradlew :app:test
```

Der Build war erfolgreich:

```text
BUILD SUCCESSFUL
```

---

### 7.4 Projekt bauen

Das gesamte Projekt habe ich mit folgendem Befehl gebaut:

```bash
.\gradlew build
```

Auch dieser Befehl wurde erfolgreich ausgeführt:

```text
BUILD SUCCESSFUL
```

Der Task `build` ist besonders wichtig, weil er das Projekt nicht nur kompiliert, sondern auch die Tests ausführt.


---

## 8. Projektlayout des Gradle-Projekts

Das mit `gradle init` erzeugte Projekt hat folgende Grundstruktur:

```text
prog2-gradle-demo
├── app
│   ├── build.gradle
│   └── src
│       ├── main
│       │   └── java
│       │       └── prog2
│       │           └── demo
│       │               └── App.java
│       └── test
│           └── java
│               └── prog2
│                   └── demo
│                       └── AppTest.java
├── gradle
│   ├── libs.versions.toml
│   └── wrapper
├── gradlew
├── gradlew.bat
├── settings.gradle
└── gradle.properties
```

Die wichtigsten Dateien und Ordner haben folgende Bedeutung:

| Datei / Ordner | Bedeutung |
|---|---|
| `settings.gradle` | beschreibt das Gradle-Projekt und bindet das Teilprojekt `app` ein |
| `app/build.gradle` | enthält die Build-Konfiguration für die Java-Applikation |
| `app/src/main/java` | enthält den eigentlichen Java-Quellcode |
| `app/src/test/java` | enthält die Testklassen |
| `App.java` | enthält das Beispielprogramm |
| `AppTest.java` | enthält einen Beispieltest |
| `gradlew` | Gradle Wrapper für Linux/macOS |
| `gradlew.bat` | Gradle Wrapper für Windows |
| `gradle/wrapper` | enthält die Wrapper-Konfiguration |
| `gradle/libs.versions.toml` | enthält zentral definierte Versionen von Abhängigkeiten |
| `gradle.properties` | enthält Gradle-Einstellungen für das Projekt |

Der wichtigste Unterschied ist:

- Produktivcode liegt unter `src/main/java`.
- Testcode liegt unter `src/test/java`.

Dadurch kann Gradle automatisch unterscheiden, welche Dateien zur Anwendung gehören und welche Dateien nur für Tests verwendet werden.

---

## 9. Buildskript erklären

Das wichtigste Buildskript befindet sich hier:

```text
app/build.gradle
```

Dort wird beschrieben, wie das Java-Projekt gebaut, getestet und gestartet wird.

---

### 9.1 `plugins`

Im Abschnitt `plugins` werden Gradle-Plugins aktiviert.

Beispiel:

```groovy
plugins {
    id 'application'
}
```

Das Plugin `application` macht aus dem Projekt eine ausführbare Java-Anwendung. Dadurch stehen unter anderem Tasks wie `run`, `distZip`, `distTar` und `installDist` zur Verfügung.

Der Task `run` wird verwendet, um die Anwendung direkt mit Gradle zu starten.

---

### 9.2 `repositories`

Im Abschnitt `repositories` wird festgelegt, von wo Gradle externe Bibliotheken herunterladen darf.

Beispiel:

```groovy
repositories {
    mavenCentral()
}
```

`mavenCentral()` bedeutet, dass Gradle Abhängigkeiten aus dem Maven Central Repository herunterladen kann.

---

### 9.3 `dependencies`

Im Abschnitt `dependencies` werden externe Bibliotheken eingetragen, die das Projekt benötigt.

Beispiel:

```groovy
dependencies {
    testImplementation libs.junit.jupiter
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}
```

`testImplementation` bedeutet, dass diese Abhängigkeit nur für Tests verwendet wird.

JUnit Jupiter wird für die Unit Tests verwendet.

Falls zusätzlich eine Zeile wie diese vorhanden ist:

```groovy
implementation libs.guava
```

bedeutet das, dass die Bibliothek `guava` für den normalen Anwendungscode verwendet werden darf.

---

### 9.4 `java`

Im Abschnitt `java` wird die Java-Version für das Projekt festgelegt.

Beispiel:

```groovy
java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(25)
    }
}
```

Damit wird festgelegt, dass das Projekt mit Java 25 gebaut werden soll.

Das ist wichtig, weil die Aufgabe Java SE Development Kit 25 verlangt.

---

### 9.5 `application`

Im Abschnitt `application` wird die Hauptklasse der Anwendung festgelegt.

Beispiel:

```groovy
application {
    mainClass = 'prog2.demo.App'
}
```

Die Klasse `prog2.demo.App` enthält die `main`-Methode. Wenn ich den Task `run` ausführe, startet Gradle genau diese Klasse.

Der Start erfolgt mit:

```bash
.\gradlew :app:run
```

---

### 9.6 `test`

Der Test-Task wird so konfiguriert, dass JUnit verwendet wird.

Beispiel:

```groovy
tasks.named('test') {
    useJUnitPlatform()
}
```

`useJUnitPlatform()` ist notwendig, damit JUnit Jupiter Tests korrekt ausgeführt werden.

Die Tests starte ich mit:

```bash
.\gradlew :app:test
```

---

## 10. Zusammenhang wichtiger Gradle-Tasks

Einige wichtige Tasks hängen logisch zusammen.

| Task | Bedeutung |
|---|---|
| `run` | startet die Anwendung |
| `test` | führt die Tests aus |
| `jar` | erstellt eine JAR-Datei |
| `assemble` | erzeugt die Build-Artefakte |
| `check` | führt Prüfungen aus, zum Beispiel Tests |
| `build` | führt `assemble` und `check` aus |
| `clean` | löscht den Build-Ordner |

Der Zusammenhang ist ungefähr:

```text
build
├── assemble
│   └── jar
└── check
    └── test
```

Das bedeutet: Wenn ich `build` ausführe, wird das Projekt gebaut und getestet.

Befehl:

```bash
.\gradlew build
```


---

## 11. Gradle-Projekt in IntelliJ IDEA öffnen

Ich habe das über die Konsole erzeugte Gradle-Projekt in IntelliJ IDEA geöffnet.

Dafür habe ich in IntelliJ folgenden Weg verwendet:

```text
File -> Open -> D:\aLearning\prog2\prog2-b01\gradle-demo
```

Wichtig ist, dass der Projektordner geöffnet wird und nicht nur der Ordner `app` oder `src`.

Nach dem Öffnen wurde das Projekt als Gradle-Projekt importiert.

---

### 11.1 Gradle-Einstellungen in IntelliJ

In IntelliJ habe ich die Gradle-Einstellungen geprüft:

```text
File -> Settings -> Build, Execution, Deployment -> Build Tools -> Gradle
```

Dabei sind folgende Einstellungen wichtig:

| Einstellung | Wert |
|---|---|
| Build and run using | Gradle |
| Run tests using | Gradle |
| Gradle JVM | JDK 25 |
| Use Gradle from | Gradle Wrapper |

Der Gradle Wrapper ist sinnvoll, weil dadurch die im Projekt konfigurierte Gradle-Version verwendet wird.

---

### 11.2 Gradle-Tasks in der IDE

Die Gradle-Tasks können in IntelliJ über das Gradle-Toolfenster ausgeführt werden.

Dort gibt es zum Beispiel folgende Task-Gruppen:

| Gruppe | Beispiele |
|---|---|
| `application` | `run` |
| `build` | `build`, `clean`, `jar` |
| `verification` | `test` |
| `help` | `tasks` |

Ich habe in IntelliJ folgende Tasks ausgeführt:

```text
application -> run
verification -> test
build -> build
```

Die Anwendung wurde erfolgreich gestartet und hat ausgegeben:

```text
Hello World!
```

Auch die Tests und der Build wurden erfolgreich ausgeführt.

Damit ist gezeigt, dass das Gradle-Projekt sowohl über die Konsole als auch über IntelliJ IDEA mit Gradle verwendet werden kann.

