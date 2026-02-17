# A-Maze-ing Project Plan  
**Total Time: 1 month (≈ 30 days)**  
**Goal: Complete delivery + reusable package + fully functional visualization**  
**Focus: Learn by doing + prioritize everything that gets evaluated by the moulinette**

## 1. Visualization Decision (CRITICAL)
**Chosen: ASCII rendering in the terminal (absolute priority)**

Reasons:
- 100% pure Python (simple `print` + ANSI colors, or `rich` if you want to polish it)
- Meets **ALL** interaction requirements from the subject
- The official example in the subject is exactly this
- Can be completed in 3–4 days once the maze logic is ready
- Gives you 7–10 extra days for the hard parts (algorithm + reusable package)

MiniLibX (MLX42 Python binding):
- Only as a bonus **IF** by day 21 everything else is already finished
- If the binding is not available on campus or you get stuck → switch back to ASCII immediately

## 2. Repository Structure (required for evaluation)

```
a-maze-ing/
├── a_maze_ing.py              # ← Mandatory filename
├── config.txt                 # Default config (committed)
├── Makefile
├── README.md
├── requirements.txt
├── .gitignore
├── mazegen/                   # ← Pip-installable package (Chapter VI)
│   ├── init.py
│   ├── generator.py           # MazeGenerator class
│   └── version.py
└── src/                       # Non-reusable code
├── config_parser.py
├── output_writer.py
├── validator.py
└── visual_ascii.py
```

## 3. Weekly Plan (Realistic & Achievable)

### Week 1 (Day 1–7) – Core Setup & Maze Generation
- Day 1–2: Project structure, complete Makefile (`install`, `run`, `lint`, `clean`, `debug`), venv, flake8 + mypy passing
- Day 3–4: Config parser (`config.txt` → KEY=VALUE, ignore # comments, validate mandatory keys, elegant error messages)
- Day 5–7: **MazeGenerator class** (`mazegen/generator.py`)
  - Internal grid representation
  - Recursive Backtracker algorithm (easiest for perfect mazes)
  - Reproducible with seed (`random.seed`)
  - `generate(width, height, entry, exit, perfect=False, seed=None)`

**Milestone**: `python a_maze_ing.py config.txt` → creates `output_maze.txt` with the hex grid only

### Week 2 (Day 8–14) – Validation & Hard Requirements
- Coherent walls (east wall of one cell = west wall of neighbor)
- Full connectivity (DFS/BFS to ensure no isolated cells)
- Perfect maze support (`PERFECT=True` → exactly one path)
- Hidden "42" pattern (cells with 0xF = all walls closed)
  - Fixed positions based on size
  - If too small → clear console message and skip
- Shortest path with BFS → save as "NSEW..." string
- Complete output format (grid + entry + exit + path)

**Milestone**: `output_maze.txt` passes the validation script mentioned in the subject

### Week 3 (Day 15–21) – Visualization & User Interactions
- Beautiful ASCII visualizer (walls, entry, exit, path, "42" with colors)
- Interactive terminal menu:
```
1. Regenerate a new maze
2. Show/Hide shortest path
3. Change wall colors (cycles pallettes)
4. Quit
```
- Optional bonus: MLX42 version (only if you have spare time)

**Milestone**: Fully interactive program running in the terminal

### Week 4 (Day 22–30) – Reusable Package + README + Polish
- Package `mazegen` (use `pyproject.toml` or `setup.py`)
- `pip install -e .` must work
- Proper documentation in `__init__.py`
- Complete `README.md` (see Chapter VII):
- First line in italic: *This project was created as part of the 42 curriculum by your_login*
- Chosen algorithm + why
- Reusable part and how to use it
- AI usage (what and where)
- Planning + how it evolved
- Edge-case testing (1×1, no space for "42", perfect=False, etc.)
- `make lint` and `make lint-strict` + mypy clean + Google-style docstrings

## 4. AI Usage (Chapter II – Very Important)
**Allowed & valued:**
- Explaining concepts (e.g., "how recursive backtracker works")
- Reviewing your pseudocode
- Suggesting test cases
- Improving README

**Never copy code** → you must be able to explain everything during defense

## 5. Recommended Tools
- Notion / Trello → daily checklist
- Frequent Git commits with clear messages
- Run `make lint` after every change
- Keep this `PLAN.md` file and check off tasks ✓

## 6. Final Pre-Push Checklist
- [ ] `a_maze_ing.py` works with default config
- [ ] `mazegen` installs via pip and can be imported
- [ ] Output file is valid
- [ ] ASCII visualization with all interactions
- [ ] README.md contains every required section
- [ ] `make lint` and `make lint-strict` pass
- [ ] mypy passes with zero errors
- [ ] Docstrings present on all functions
