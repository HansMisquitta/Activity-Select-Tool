# Activity Selection Problem — Interactive Visualizer

An interactive, single-file teaching tool that animates the Activity Selection greedy algorithm step by step. Built with zero external libraries — pure HTML, CSS, JavaScript, and SVG.

**[Live Demo →](https://your-username.github.io/your-repo-name/)**

---

## What It Does

You load a set of activities (each with a start and finish time), press Play, and watch the algorithm work in real time:

1. **Phase 1** — activities are sorted by finish time, with each comparison and swap animated
2. **Phase 2** — the greedy scan selects the maximum set of non-overlapping activities, highlighting each decision with a plain-English explanation

Every step is explained, every line of pseudocode is highlighted, and every decision is logged.

---

## Features

### Core Visualizer
- **Animated Gantt chart** — activity bars change color as they move through states: pending → comparing → candidate → selected / rejected
- **Sort bars panel** — secondary visualization showing finish times as bars, with compared/swapped pairs highlighted in yellow
- **Pseudocode panel** — synced line-by-line highlighting that auto-scrolls to the active line; hover any line for a plain-English tooltip
- **Step explanation box** — real variable values injected at every step (e.g. *"start=3 < lastFinish=4 — overlaps D"*)
- **Playback engine** — Build Steps / Step / Play / Pause / Reset with a speed slider (0.25× to 4×) and a step counter
- **Step history table** — scrollable log of every action taken; click any row to jump the animation back to that exact state
- **Live statistics** — comparisons, swaps, selected, rejected — update in real time; actual comparisons verified against theoretical n·log₂n after completion

### Educational Tabs

| Tab | What's Inside |
|---|---|
| **Visualizer** | Main animation, pseudocode, history table |
| **CLO-1: Complexity** | Time/space complexity table, interactive O(n log n) vs O(n²) growth curve chart (adjustable up to n=500), operations count reference table |
| **CLO-2: Sorting** | Four sorting strategy comparison (finish time / start time / duration / none), conflict heatmap (n×n matrix showing which activities overlap) |
| **CLO-3: Greedy** | Exchange argument proof diagram, interactive what-if widget, counterexample showing why sort-by-start fails |
| **Overview** | Problem statement, fully worked CLRS example (n=11), key concepts, common mistakes |

### Bonus Features
- **What-if widget** — click any activity to force it as the first greedy pick and see how the result compares to the true greedy optimum
- **Preset mini-previews** — hover over any preset button to see a tiny Gantt preview before loading
- **Voice narration** — toggle on to have each step explanation read aloud via the Web Speech API
- **PNG export** — download the current Gantt chart state as an image via the Canvas API
- **Responsive layout** — two-column design collapses to single column on screens under 980px

---

## Presets

| Preset | Description |
|---|---|
| Classic CLRS | Textbook example from Chapter 16.1, n=11 |
| Worst Case | All activities heavily overlap — maximum rejections |
| Best Case | No conflicts at all — every activity selected |
| Busy Day | Dense conflicts, n=8 |
| Unsorted Demo | Input intentionally out of order — shows why sorting is critical |
| Ties in Finish Time | Two activities share a finish time — demonstrates tiebreaking |

---

## How to Use

### Run Locally
Just open `index.html` in any modern browser. No server, no install, no dependencies.

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
open index.html        # macOS
# or double-click index.html on Windows/Linux
```

### Custom Input
Type activities in the left panel using the format:
```
ActivityName, StartTime, FinishTime
```
Example:
```
Meeting, 9, 10
Lecture, 9.5, 11
Lunch, 11, 12
Workshop, 12, 14
```
Then click **Load Input** → **Build Steps** → **Play**.

---

## Tech Stack

| Technology | Used For |
|---|---|
| HTML5 | Page structure and layout |
| CSS3 | Dark theme, CSS Grid, CSS variables, transitions, responsive breakpoint |
| JavaScript ES6+ | Algorithm logic, animation engine, state management, DOM manipulation |
| SVG | All visualizations — Gantt chart, sort bars, growth curve, heatmap, proof diagram, mini previews |
| Web Speech API | Voice narration |
| Canvas API | PNG export |
| GitHub Pages | Static deployment |

Zero external libraries. No React, no D3, no Chart.js, no jQuery, no Bootstrap.

---

## Algorithm Reference

**Problem:** Given n activities with start times sᵢ and finish times fᵢ, find the maximum subset of mutually compatible (non-overlapping) activities.

**Algorithm:**
```
1. Sort activities by finish time          // O(n log n)
2. Select the first activity
3. For each remaining activity:
     if activity.start ≥ lastFinish:
         select it, update lastFinish      // O(n)
4. Return selected set
```

**Complexity:** O(n log n) time, O(n) space

**Correctness:** Proven by the exchange argument — any optimal solution can be modified to include the greedy first choice (earliest finish) without reducing its size, because f(a₁) ≤ f(a₁') guarantees all subsequent activities remain compatible after the swap.

**Reference:** Cormen et al., *Introduction to Algorithms*, 4th ed., Chapter 16.1

---

## Project Structure

```
index.html        ← everything: HTML + CSS + JavaScript + SVG (single file)
README.md
```

---

## Screenshots

> *(Add screenshots here after deployment)*
> 
> Suggested shots:
> - Visualizer tab mid-animation (mix of green selected and red rejected bars)
> - CLO-2 tab showing the four sorting strategies side by side
> - CLO-3 tab showing the what-if widget with a forced non-greedy pick

---

## License

MIT — free to use, modify, and share.
