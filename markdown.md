# Classroom Student Selectors

**Version:** 1.1.0

**Release Date:** September 15, 2026

**Target Platform:** Interactive Whiteboards, Smart Boards, Touch Displays, Desktop & Tablet Browsers

**File Architecture:** Standalone Single-File Application (`HTML5`, `Vanilla CSS3`, `Modern JavaScript ES6+`)

---

## Overview

The **Classroom Student Selectors** application is a lightweight, zero-dependency, touch-optimized web utility engineered specifically for classroom instruction on interactive displays. It provides equitable, randomized, and engaging mechanisms for selecting students, student pairs, seats, and cooperative teams.

The app uses game-show visual conventions—including physical ease-out deceleration curves, animated mechanical flippers, dynamic slice elimination, and responsive sound design—while keeping tools straightforward for rapid classroom transitions.

---

## System Requirements & Portability

* **Dependencies:** None (`0` external libraries, frameworks, or web fonts).
* **Audio Engine:** Native Web Audio API with procedural synthesis (runs completely offline without external `.mp3` or `.wav` assets).
* **Storage:** Native browser `localStorage` for auto-persisting user settings across sessions.
* **Display Target:** Adaptive scaling ranging from 10.5" tablets up to 85"+ 4K interactive interactive flat panels.

---

## Core Tool Modules

```
┌────────────────────────────────────────────────────────────────────────┐
│                        APP SIDEBAR NAVIGATION                          │
├───────────────────┬────────────────────────────────────────────────────┤
│ 1. Seat Selector  │ Single wheel (Seats 3–6), fallback plan, no-repeat │
│ 2. Partner Picker │ Alternating A/B wheel (Emerald/Gold), flip mode    │
│ 3. Seat Sequencer │ Shell-game vertical column shuffle (Seats 3–6)     │
│ 4. Team Selector  │ Configurable wheel (Teams 3–9) with no-repeat      │
│ 5. Team & Student │ Dual side-by-side synchronized interactive wheels  │
│ 6. Team Sequencer │ Single-column shell-game ordering (Teams 3–9)      │
└───────────────────┴────────────────────────────────────────────────────┘

```

### 1. Seat Selector

* **Function:** Chooses which seat at a student table answers.
* **Configurable Range:** Defaults to 4 seats, adjustable between 3 and 6 via stepper controls.
* **Wheel Layout:** Multi-wedge arrangement (repeats the seat sequence across two cycles) to provide a visually balanced wheel.
* **Color Palette:**
* **Seat 1:** Amber / Yellow (`#f59e0b`)
* **Seat 2:** Emerald Green (`#10b981`)
* **Seat 3:** Royal Blue (`#3b82f6`)
* **Seat 4:** Crimson Red (`#ef4444`)
* **Seat 5:** Amethyst Purple (`#8b5cf6`)
* **Seat 6:** Cyan Teal (`#06b6d4`)


* **Absentee Contingency Plan:** Dynamically calculates an alternate seat in the bottom-right corner (e.g., `Seat 2`) using modular clockwise succession ($(\text{Seat} \pmod N) + 1$) if the selected seat is unoccupied.
* **No-Repeat Option:** When active, chosen seats are removed from the active selection pool and darkened on the wheel canvas until the pool resets.

### 2. Partner Selector

* **Function:** Selects whether Partner A or Partner B initiates paired dialogue or cooperative activities.
* **Color Configuration:** Uses distinct high-contrast classroom colors (**Emerald Teal** `#059669` and **Warm Amber Gold** `#d97706`) rather than standard commercial color pairings.
* **Wedge Density:** Defaults to 8 alternating wedges, adjustable between 4 and 16 wedges for a realistic wheel feel.
* **Operation Modes:**
* **Random Spin:** Unbiased 50/50 probability.
* **Alternate A/B:** Deterministic alternating rotation ensuring exact parity between turns.



### 3. Seat Sequencer

* **Function:** Establishes the turn order of seats for sharing, presentations, or group roles.
* **Range:** Configurable between 3 and 6 seats.
* **Presentation:** Formatted as a single, centered vertical column with card colors matching the Seat Selector wheel palette.
* **Shell-Game Shuffle:** When initiated, cards translate, swap positions, and play mechanical audio clicks over several iterations before settling into the final randomized order.

### 4. Team Selector

* **Function:** Calls on an entire student table or project group.
* **Capacity:** Defaults to 8 teams, adjustable from 3 to 9 teams.
* **Elimination Tracking:** Features a persistent "No Repeat" toggle. Slices that have already been chosen turn dark charcoal gray (`#11151f`) on the wheel to indicate they have already participated.

### 5. Team & Student (Dual Spinner)

* **Function:** Allows the teacher to call on a specific student within a specific team in one view.
* **Layout:** Displays two independent canvas wheels side-by-side within a unified container:
* **Left Wheel:** Team Spinner (Teams 3–9).
* **Right Wheel:** Seat Spinner (Seats 3–6).


* **Control Ergonomics:** Contains dedicated **Spin Team** and **Spin Student** buttons alongside a **Reset Both** trigger.

### 6. Team Sequencer

* **Function:** Determines an equitable order of teams (e.g., project presentations, classroom exits, stations).
* **Single Column Architecture:** Constrained to a single, vertical column that automatically resizes using CSS `clamp()` and view-height rules, preventing uneven multi-row line breaks when displaying up to 9 teams.
* **Shell-Game Mechanics:** Features the same card-swapping animation and audio feedback used in the Seat Sequencer.

---

## Visual Design & Smart Board Ergonomics

### Container Query Responsive Sizing

To prevent UI clipping on screens with varying aspect ratios (16:9, 16:10, 4:3), display viewports use CSS Container Queries (`container-type: size`):

$$\text{Wheel Diameter} = \min(100\text{cqh} - 5.5\text{rem},\; 100\text{cqw} - 4\text{rem},\; 520\text{px})$$

Wheels expand to occupy maximum available vertical real estate, but scale down smoothly on compact viewports to keep control decks visible.

### Physical Pointer Flipping Mechanism

* Built using pure CSS hardware-accelerated transforms (`will-change: transform`).
* Slices crossing the 12 o'clock pointer trigger an immediate `-24deg` rotational kick (`.kick`) accompanied by a Web Audio tick pulse, resetting after 45ms to simulate a spring-loaded mechanical peg.

### Classroom Chalkboard & High-Contrast Themes

The application supports 9 classroom themes selectable via the Settings menu:

| Theme ID | Name | Background | Accent | Primary Font Stack |
| --- | --- | --- | --- | --- |
| `default` | Default Dark | `#131722` | `#3b82f6` | System Sans-Serif |
| `chalkboard` | Classroom Chalkboard | `#1c2e24` | `#facc15` | Chalkboard SE, Comic Sans MS |
| `neon` | Digital Neon | `#0a0a0f` | `#00ffff` | Monospace / Courier New |
| `pastel` | Warm Pastel | `#24222f` | `#a78bfa` | Quicksand, Century Gothic |
| `arcade` | Retro Arcade | `#0b0819` | `#f59e0b` | VT323, Pixel Courier |
| `cafe` | Cozy Cafe | `#1f1b18` | `#ddb892` | Georgia, Classic Serif |
| `space` | Deep Space | `#060814` | `#6366f1` | Trebuchet MS, Futura |
| `primary-edu` | Elementary Light | `#f0f4f8` | `#2563eb` | Arial Rounded MT Bold |
| `high-contrast` | High Contrast | `#000000` | `#ffff00` | Impact, Arial Black |

---

## Audio Architecture

Audio is generated via the native `AudioContext` interface, utilizing pre-gain compression and dynamic frequency ramps:

```
[ Oscillator Node ] ──► [ Gain Ramp Node ] ──► [ Pre-Gain (2.5x) ] ──► [ Master Gain ] ──► [ Dynamics Compressor ] ──► [ Output ]

```

* **Default Volume:** Initialized to **25%** (`0.25`), preserved persistently across sessions in browser storage.
* **Ticking Synthesis:** A high-passed `triangle` oscillator pulsed at 900 Hz for 35 milliseconds to produce mechanical wheel friction sound.
* **Chime Presets:**
* `none` (Silent / Mechanical ticks only)
* `bell` (Two-tone resonant sine chime)
* `harp` (Ascending 6-tone glissando)
* `beep` (Triple square pulse)
* `marimba` (Warm wooden triad)
* `arcade` (8-bit arpeggio fanfare)
* `zen` (Resonant singing bowl tone)
* `school` (Rapid dual-frequency mechanical ringer)
* `sonar` (Swept sine chirp)



---

## User Preferences & LocalStorage Keys

All interactive settings are serialized to the browser's persistent key-value store:

* `selector_volume`: Floating point volume scalar (`0.0` to `1.0`).
* `selector_chime`: Active chime preset identifier string.
* `selector_theme`: Current visual theme stylesheet key.
* `selector_speed_idx`: Active animation speed configuration (`0` = Fast, `1` = Normal, `2` = Dramatic).

---

## Setup & Deployment Instructions

1. Download or copy the application markup into a file named `selectors.html`.
2. Double-click the file to open it in Google Chrome, Microsoft Edge, Mozilla Firefox, or Apple Safari.
3. For dedicated Smart Board use, save the file to the local classroom drive and launch it in Fullscreen Mode (`F11` on Windows/ChromeOS, or `Control+Command+F` on macOS). No web server, Node.js environment, or internet connection is required.
