# Bruh

An offline Python study library with a nested terminal browser for five documents:

1. Unit 2 Theory
2. Unit 5 Theory
3. Django Code (complete Unit 2 coding reference)
4. Docker Commands (complete Unit 5 coding reference)
5. Git Commands (supplementary cheat sheet)

The full supplied text and all four original PDFs are bundled. No runtime dependencies, API keys or internet access are needed after installation. Code and commands in references are displayed for reading, never executed.

## Install and run

Python 3.9 or newer and Git:

```powershell
python -m pip install git+https://github.com/Xvd-cpu/bruh.git
python -m bruh
```

Install while your virtual environment is active if you want to use Bruh inside it. The `bruh` command also works when your Python Scripts directory is on PATH (normally automatic in an active virtual environment).

Without Git, download the repository ZIP, extract it, open a terminal inside the extracted folder, and run `python -m pip install .`.

Not published to PyPI yet.

## Browse

```text
BRUH
==========================================
1. Unit 2 Theory
2. Unit 5 Theory
3. Django Code
4. Docker Commands
5. Git Commands
0. Exit
```

Choose a document to see its contents, with main numbered chapters only. Choose a chapter to read it, including all of its subsections. Subsections such as 2.1 and 2.2 are not separate menu options.

After reading, you stay in the same document's contents menu. Choose `0. Back to documents` to return to the five-document menu; `0. Exit` there closes Bruh. Ctrl+C or end-of-input exits cleanly.

A `Document introduction` entry preserves each document's preface and original contents page. PDF extraction can change table spacing; open the original PDF to see diagrams and exact formatting.

## Search within a document

Choose `S. Search this document`, then type a keyword or phrase such as `migrations` or `docker run`. Search is case-insensitive and treats the query literally.

Bruh lists matching sections with match counts and preview lines. Choose a result to open its section. Every matching keyword in that section is highlighted as `[[keyword]]`, which is readable on Windows, Linux and macOS. After reading a search result you return to that document's contents. `0` at search results returns without opening a result; a blank query cancels search.

Search maps each hit to its main chapter and opens that chapter with matching keywords highlighted. Contents-page hits appear under Document introduction.

## Other commands

```powershell
bruh 1                           # Open Unit 2's contents menu
bruh 3                           # Open the Django code contents menu
bruh 3 --topic 2 --plain          # Print topic 2 and exit
bruh 1 --full --plain             # Print the entire document
bruh 3 --search migrations        # Interactive document search
bruh --search Docker             # Print matches across all documents
bruh 1 --pdf                      # Open the original PDF in your desktop viewer
bruh 4 --export-pdf docker.pdf    # Save the original PDF
```

Use `python -m bruh` instead of `bruh` if the executable isn't on PATH. In piped/noninteractive CLI search, results are printed with topic numbers; open one using `--topic NUMBER`. PDF export replaces the destination file if it exists. Git is a text-only reference and has no source PDF.

## Python API

```python
from bruh import get_text, list_topics, get_topic, search_topics

print(list_topics(1))
print(get_topic(1, 2))
print(search_topics('Django', 1))
print(get_text(1))
```

## Development

```sh
python -m pip install .
python -m unittest discover -s tests -v
python -m pip wheel --no-deps . -w dist
```

The topic index is stored in `src/bruh/data/contents.json` using zero-based start and exclusive end line offsets in the bundled text. Update that index whenever reference text line boundaries change. The four original PDFs retain their source authorship.
