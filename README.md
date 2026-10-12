# Python Fundamentals for C# Developers

A set of Jupyter notebooks for learning Python if you already know C#.
Each notebook covers **one concept**. It explains the idea in Markdown, shows the matching
C# code where there is one, and then shows Python you can run.

## Getting started

The project uses [uv](https://docs.astral.sh/uv/) and needs Python 3.14 (pinned in `.python-version`).

```bash
uv sync                 # create .venv and install dependencies (≈ dotnet restore)
uv run jupyter lab      # open the notebooks in JupyterLab
```

**VS Code:** open any `.ipynb` file and choose the `.venv` interpreter
(`.venv/bin/python`) as the kernel.

To check that every notebook runs from top to bottom:

```bash
find 01-syntax 02-standard-library -name '*.ipynb' | sort | while read -r nb; do
  uv run jupyter nbconvert --to notebook --execute --stdout "$nb" > /dev/null || echo "FAILED: $nb"
done
```

## How the notebooks are organised

```
<NN-group>/                    big topic area, e.g. 01-syntax, 02-standard-library
  <NN-concept>/                one programming concept, e.g. 05-collections
    <NNN-topic>.ipynb          one idea per notebook, e.g. 001-lists.ipynb
```

- **Groups** and **concept folders** have two-digit numbers. **Notebooks** have three-digit
  numbers, and the count starts again at `001` in each concept folder. Work through them in order.
- To add a notebook, give it the next number in its folder. Existing files never need renaming.
- Every notebook has the same layout:
  1. **Title and goals.** What you will learn.
  2. **C# mental model.** How the idea maps to what you already know.
  3. **Sections.** An explanation, then the C# version (where there is one), then Python you can run.
  4. **⚠️ Gotchas.** Places where C# habits will catch you out.
  5. **Summary table.** C# and Python side by side.
  6. **Exercises.** Solutions are in a collapsible block.
- Notebooks do not depend on each other, so you can open any one and run it on its own.

## Curriculum

### 01 · Syntax (available now)

| Folder | Notebooks |
|---|---|
| `01-basics` | running Python code · variables & names · comments & docstrings · indentation & blocks · printing & input |
| `02-data-types` | numbers · strings · string formatting · booleans & truthiness · `None` · type conversion & checking · mutability & identity |
| `03-operators` | arithmetic & assignment · comparison & logical · bitwise · membership & identity |
| `04-control-flow` | `if`/`elif`/`else` · `match` · `for` & `range` · `while` · `break`/`continue`/loop-`else` |
| `05-collections` | lists · tuples · dictionaries · sets · slicing · unpacking · comprehensions |
| `06-functions` | defining functions · parameters & arguments · `*args`/`**kwargs` · scope & closures · lambdas & higher-order functions · decorators |
| `07-classes-and-oop` | classes & objects · class & static members · properties · encapsulation · inheritance & `super` · ABCs & protocols · dunder methods · dataclasses · enums |
| `08-error-handling` | `try`/`except`/`finally` · raising & custom exceptions · context managers |
| `09-iterators-and-generators` | iterables & iterators · generators · generator expressions & lazy evaluation |
| `10-type-hints` | type annotations · generics · advanced types |
| `11-modules-and-packages` | importing modules · creating modules & packages · environments & dependencies with uv |
| `12-async` | `async`/`await` · running tasks concurrently |

### 02 · Standard Library (available now)

This group moves from the language to the standard library, much like moving from C# the language
to the BCL (`System.*`). The layout is the same as `01-syntax`. Instead of a "C# mental model"
section, each notebook opens with a **.NET mental model** that names the closest BCL type or namespace.
Where .NET has nothing equivalent, the notebook says so. Every notebook runs offline. Network demos
use a local server on `127.0.0.1`, and file demos work in a temporary directory.

| Folder | Notebooks | Closest .NET equivalent |
|---|---|---|
| `01-text-processing` | `re` · `string` & `textwrap` · `difflib` · Unicode, bytes & encodings | `System.Text`, `System.Text.RegularExpressions` |
| `02-data-structures` | `deque` · `Counter` · `defaultdict`/`OrderedDict`/`ChainMap` · `heapq` · `bisect` · `array` & `memoryview` | `System.Collections.Generic` (`Queue`, `PriorityQueue`, `SortedList`), `Span<T>` |
| `03-functional-tools` | `itertools` essentials · `itertools` combinatorics & grouping · `functools` · `operator` | LINQ (`System.Linq`) |
| `04-numbers-and-math` | `math` · `statistics` · `decimal` · `fractions` · `random` · `secrets` | `System.Math`, `decimal`, `System.Random`, `RandomNumberGenerator` |
| `05-dates-and-times` | dates, times & timedeltas · formatting & parsing · time zones (`zoneinfo`) · clocks & measuring time · `calendar` | `DateTime`, `DateOnly`, `TimeSpan`, `TimeZoneInfo`, `Stopwatch` |
| `06-files-and-paths` | `pathlib` · reading & writing files · `os` & `shutil` · `tempfile` · in-memory streams (`io`) | `System.IO` (`Path`, `File`, `Directory`, `Stream`, `MemoryStream`) |
| `07-data-formats` | `json` · `csv` · `tomllib` · XML (`ElementTree`) · `pickle` · `base64` & `hashlib` | `System.Text.Json`, `System.Xml.Linq`, `System.Security.Cryptography` |
| `08-persistence` | `sqlite3` basics · `sqlite3` transactions & row factories · `shelve` & `dbm` | ADO.NET, `Microsoft.Data.Sqlite` |
| `09-system-and-cli` | `sys` · environment & platform · `argparse` · `subprocess` | `Environment`, `System.CommandLine`, `Process` |
| `10-logging-and-config` | `logging` basics · configuring logging · `configparser` · `warnings` | `Microsoft.Extensions.Logging`, `IConfiguration`, `[Obsolete]` |
| `11-concurrency` | threads · locks, events & queues · `concurrent.futures` · `multiprocessing` · `asyncio` in depth | `System.Threading`, TPL, `Channel<T>` |
| `12-networking` | HTTP requests with `urllib` · a simple HTTP server · sockets · building email messages | `HttpClient`, `HttpListener`, `System.Net.Sockets`, `MailMessage` |
| `13-testing-and-debugging` | `unittest` · `unittest.mock` · `doctest` · `pdb` · timing & profiling | xUnit/NUnit/MSTest, Moq, debugger, BenchmarkDotNet |

### Later groups

Once the standard library is covered, later groups can be added with the same layout, for example
`03-testing` (pytest), `04-packaging-and-tooling` (ruff, pyright, publishing), and `05-ecosystem`
(popular third-party libraries).
