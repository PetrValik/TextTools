# TextTools

A small command-line utility for line-oriented text processing, written in Java. It reads a text file and applies a chain of filtering/sorting operations followed by a terminal operation such as printing, counting, or finding the most similar lines.

## About

TextTools processes a text file line by line. Operations are split into two kinds:

- **Intermediate operations** transform the working set of lines (filter unique lines, filter duplicates, sort by natural ordering). They can be combined and are applied in sequence.
- **Terminal operations** produce the final output (print lines, count lines, print each line's length, or find the pair(s) of most similar distinct lines by **Levenshtein distance**). Exactly one terminal operation runs; `lines` is the default.

The project was a good exercise in clean object-oriented design, working with Java collections, exception handling, and integrating a third-party command-line parsing library (JCommander).

## Tech stack

- **Java 11**
- **Maven** — build, packaging, and dependency management
- **JCommander** — command-line argument parsing
- **JUnit 5** and **AssertJ** — testing
- **Checkstyle** — enforced code-style checks during the build

## Build & run

Build and package (produces a runnable fat JAR at `target/application.jar`):

```bash
mvn clean install
```

To build while skipping the Checkstyle failure gate:

```bash
mvn clean install -Dcheckstyle.fail=false
```

Run:

```bash
java -jar target/application.jar --file path/to/file.txt [operations]
```

## Usage

### Operations

| Operation    | Type         | CLI option | Description |
| ------------ | ------------ | ---------- | ----------- |
| unique       | intermediate | `-u`       | Keep only unique lines |
| sort         | intermediate | `-s`       | Sort lines by natural ordering |
| duplicates   | intermediate | `-d`       | Keep only duplicate lines |
| lines        | terminal     | `lines`    | Print lines (default) |
| count        | terminal     | `count`    | Print the number of lines |
| sizes        | terminal     | `sizes`    | Print each line's character length |
| similar      | terminal     | `similar`  | Print the most similar distinct line pairs by Levenshtein distance |

### Options

| CLI option | Description |
| ---------- | ----------- |
| `--file`   | Path to the input file (required) |
| `--help`   | Print application usage |

### Examples

```bash
# Print file lines (default operation)
java -jar target/application.jar --file duplicities.txt lines

# Print sorted lines
java -jar target/application.jar --file duplicities.txt -s

# Count the unique lines
java -jar target/application.jar --file duplicities.txt -u count

# Find the most similar lines by Levenshtein distance
java -jar target/application.jar --file duplicities.txt similar
```

Combining `-u` and `-d` is invalid and prints an error followed by the usage message.

## Notes

University assignment for **Masaryk University, course PB162 (Java)** — 2021. The task focused on object-oriented design and correct use of collections and exceptions. No AI tools were used in the original implementation.
