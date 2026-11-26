# EE599-Project-Presentation

The final presentation of the EE 599 project *Learning to Map Feasible Design Spaces of Amplifier Topologies*: one
Beamer deck built from one file per teammate. The latest compiled deck is [`main.pdf`](main.pdf); GitHub Actions
rebuilds it on every push to `main`.

## Who edits what

| File | Owner | What |
|---|---|---|
| `main.tex`, `preamble.tex` | Renzhi | title, order of the parts, theme, shared macros |
| `sections/intro.tex`, `sections/conclusion.tex` | Renzhi | the problem, the shared environment, conclusions |
| `sections/taman.tex` | Taman | evolution strategies |
| `sections/samir.tex` | Samir | PPO |
| `sections/hungyu.tex` | Hungyu | DQN, NSGA-II, MAP-Elites |
| `sections/renzhi.tex` | Renzhi | comparison across methods; the LLM designer loop |
| `sections/zhaoyan.tex` | Zhaoyan | post-training a small model (Qwen3-8B) |
| `figures/<name>/` | each owner | your figures |

**Edit only your own section file and your own figures folder.** Since nobody else touches them, your changes never
conflict with anyone else's.

**This repo is public.** Nothing from a private process (TSMC 65 nm) goes on a slide or in `figures/`: no numbers,
plots, device names or model details. SKY130 and GF180 results are fine.

Need something in a shared file, such as a package, a change to the theme or a new shared macro? Ask Renzhi. For a
macro only you use, define it at the top of your own file with your name as a prefix, e.g.
`\newcommand{\tamanBudget}{600}`.

## Writing your slides

`main.tex` makes the deck's cover, the contents slide and, for each section, its title and a cover slide with the
presenter's name. Your file holds only your frames, starting with four placeholders: method, training setup, results,
takeaways. Replace them, and add or remove frames as you like. To rename your section, ask Renzhi.

- **Figures:** put them in `figures/<name>/` and write `\includegraphics[width=0.8\linewidth]{<name>/plot.pdf}`.
  Prefer PDF or PNG, each under a few MB.
- **Shared macros** (in `preamble.tex`):
  - `\todo{...}`: an orange reminder; remove every one before the talk;
  - `\placeholder{...}`: a grey box where a figure will go;
  - `\rulename`, `\passfail`, `\prederr`: the names everyone uses for the baseline and the two measures.
- **Backup slides:** put them at the end of your file as `\begin{frame}[noframenumbering]{Backup: ...}`.
- **Two columns:** see the "training setup" frame in your file.

## Building

You need a TeX installation with `latexmk` (TeX Live or MiKTeX), or Overleaf.

| To build | Run | Output |
|---|---|---|
| only your part (cover, contents and your section) | `latexmk -pdf solo_<name>.tex` | `solo_<name>.pdf` |
| the whole deck | `latexmk -pdf main.tex` | `main.pdf` |
| clean up | `latexmk -C` | |

In Overleaf, set the main document to `solo_<name>.tex` while you work, and to `main.tex` for the whole deck.

## Workflow

1. `git pull` before you start.
2. Edit your file and build `solo_<name>.tex` until it compiles cleanly.
3. Commit only your own files. Don't commit PDFs other than figures; `.gitignore` already skips build files.
4. Push, either to `main` or to a branch with a pull request:
   - **Direct to `main`:** `git pull --rebase && git push`. Your files are yours, so this never conflicts.
   - **Branch + pull request** (`<name>/<topic>`): the build check runs on the pull request.

On every pull request, GitHub Actions checks that each `solo_<name>.tex` and `main.tex` compiles. A broken file stops
the whole deck from building, so compile before you push.
