<div align="right">

🇬🇧 English | [🇫🇷 Français](README.fr.md)

</div>

<div align="center">

<img src="docs/banner.gif" alt="Mona: Michelangelo's David drawn in ASCII with a scanning light" width="420">

# MONA

**See your website the way a first-time visitor does.**

[![License](https://img.shields.io/badge/license-personal%20use%20only-d9b877?labelColor=141413)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.10%2B-d9b877?labelColor=141413&logo=python&logoColor=white)](https://www.python.org/downloads/)
![OS](https://img.shields.io/badge/Windows%20·%20macOS%20·%20Linux-8a8a84?labelColor=141413)
![AI](https://img.shields.io/badge/AI-runs%20on%20your%20PC-9bc7a8?labelColor=141413)
![Models](https://img.shields.io/badge/models-ONNX%20included-9bc7a8?labelColor=141413&logo=onnx&logoColor=white)
![Chrome](https://img.shields.io/badge/capture-real%20Chrome-d9b877?labelColor=141413&logo=googlechrome&logoColor=white)
![Cloud](https://img.shields.io/badge/cloud-none-d98577?labelColor=141413)

<br>

**You designed the page. You can't see it for the first time anymore.**

**Mona predicts where a first-time visitor's eyes land, and tells you what gets in the way.**

*Built by Liam DB, with the help of AI.*

</div>

---

<div align="center">

<img src="docs/demo.gif" width="760" alt="Mona analyzing a web page: ASCII animation, then the report">

*Mona on a web page: an ASCII statue while it works, then the report.*

</div>

---

> Mona is a small desktop app for web designers. It opens your page in a test Chrome, scrolls it to the bottom like a visitor, then runs AI models **on your own PC** to predict gaze, estimate the brain's reaction and check readability. Nothing is uploaded.

<div align="center">
<table>
<tr>
<td align="center" width="16%">

**👁️ Gaze**<br>
A heat map of where<br>
people look first,<br>
from 2 models

</td>
<td align="center" width="16%">

**🧠 Brain**<br>
Response of 20 visual<br>
areas of the cortex<br>
(indicative)

</td>
<td align="center" width="16%">

**📊 Score /100**<br>
Six readability<br>
checks, with advice<br>
per screen

</td>
<td align="center" width="16%">

**🔎 Detector**<br>
Finds text, buttons,<br>
images, fields, icons<br>
in any screenshot

</td>
<td align="center" width="16%">

**🏠 100% local**<br>
No account, no cloud,<br>
no tracking

</td>
<td align="center" width="16%">

**⚙️ Adapts to your PC**<br>
Reads your CPU, RAM,<br>
GPU, then picks<br>
how hard to work

</td>
</tr>
</table>
</div>

---

## 📏 Why Mona

An opinion about a design is easy to give and hard to check. Mona gives numbers, measured on cases **never seen during training**.

| What | Result |
|---|:---:|
| Gaze vs. real eye-tracking (UEyes) | correlation **0.68** |
| Gaze on web pages from another dataset (Imp1k) | correlation **0.56** |
| UI element detector (text, button, image) | F1 **0.64** |
| Score from an image alone vs. from the page code | **5.5 points** out of 100 apart on average |

Mona is not right about everything. The brain model comes from a single subject: an indication, not a diagnosis. Mona measures readability and attention, **not taste**, and it does not replace a test with real people or an accessibility audit. The method and the limits are on the [website](https://mona.devliam.com/benchmarks.html).

---

## 🎯 What it's useful for

- **Checking a design before showing it:** where does the eye go first, and is it the right place?
- **Finding the main button:** is the call to action visible in the first screen, which counts for half of the score?
- **Contrast and text size:** a quick WCAG-style pass on every screen of a long page.
- **Mockups and Figma exports:** drop an image, the detector reads the interface from the pixels.
- **Comparing two versions:** analyze each one, keep both reports, compare the two scores.
- **Your own sites, your own machine:** no need to send an unpublished design to an online tool.

---

## 📦 Installation

> Requirements: **Python 3.10+**. The AI models are already in the repository.
>
> Tested on **Windows 11** and **Ubuntu** (WSL). macOS is not tested yet.

[Download the ZIP](https://github.com/LiamLitle/mona-local/archive/refs/heads/main.zip) or clone the repository, then:

| | |
|---|---|
| **Windows** | double-click **`Mona.bat`** |
| **macOS, Linux** | run **`./mona.sh`** |

The first time, the launcher installs everything: the Python packages and the test Chrome, about 150 MB, a few minutes. After that, the app opens straight away in its own window.

**Prefer to do it by hand?**

```bash
pip install -r requirements.txt
python -m mona setup      # installs the test Chrome, once
python -m mona            # opens the app
```

For a native window instead of a Chrome/Edge app window: `pip install -r requirements-app.txt`.

---

## 🚀 Usage

### 1. Analyze a site

Paste an address. Mona opens it in a 1440 × 900 test Chrome, scrolls to the very bottom (up to 12 screens), reads the texts, sizes, colors and buttons of each screen, then runs the models.

### 2. Analyze an image

Drop a screenshot, a mockup or a Figma export. Long images are cut into screens, the **detector** finds the interface elements, and **plan B** rebuilds what the page code would have given. The score is then indicative (about 5.5 points of difference).

### 3. Read the report

A gaze map and a score for each screen, a brain reaction, advice per rule. The first screen counts for half of the final score. Reports stay in the app's own storage on your PC. Export them as JSON or print them to PDF.

### 4. Use the command line *(optional)*

```bash
python -m mona analyze https://example.com    # analyze without the interface
python -m mona analyze screenshot.png         # analyze an image
python -m mona doctor               # your PC, the settings Mona chose, the state of the models
python -m mona serve                # server only, no window
```

### 5. Run the tests *(optional)*

```bash
python -m pytest
```

Environment variables: `MONA_PORT`, `MONA_MAX_SCREENS` (default 12), `MONA_HEADLESS=1` (hide the test Chrome), `MONA_HOME` (where settings are stored).

---

## 🗿 The AI models

Mona contains **its own AI models**, in [`models/`](models). They do not write text and they do not talk to you: each one turns a page into a map or a list.

| Model | File | What it does |
|---|---|---|
| **Gaze A and B** | `gaze_a.onnx`, `gaze_b.onnx` | Predict where eyes land. Their two maps are averaged. Trained on eye-tracking data (62 people, 1,980 interfaces). |
| **Brain** | `brain.onnx` | Estimates the response of 20 visual areas, as a percentile against about 500 web pages. Trained on fMRI data. Indicative, not part of the score. |
| **Detector** | `detector.onnx` | Finds text, buttons, images, fields and icons on a screenshot. |
| **Plan B** | `plan_b_params.json` | Turns the detector's output into the same information as the page code. |

- **Where they run:** on your CPU or GPU, in ONNX format, through onnxruntime. No cloud, no API call. [`mona/hardware.py`](mona/hardware.py) reads your PC and chooses threads and parallelism, and leaves a quarter of your cores free.
- **Integrity:** `models/MODELS.json` lists the size and SHA-256 of every file, used to check that the files are intact.
- **Licenses:** training data and pretrained weights have their own terms. The brain model derives from research-only images and is for non-commercial research use.

The role, input, output, training data and license of each model are in [`docs/MODELS.md`](docs/MODELS.md).

---

<details>
<summary><b>🗂️ File structure</b></summary>
<br>

```
mona-local/
├── Mona.bat · mona.sh    ← one-click launchers ← START HERE
├── models/               ← THE AI MODELS (*.onnx) + MODELS.json
├── mona/                 ← the application
│   ├── ai/               ← run the models: gaze, brain, detector, plan B
│   ├── capture.py        ← the test Chrome: open, scroll, capture
│   ├── rules.py          ← six readability rules and the score
│   ├── pipeline.py       ← chains everything, reports progress as events
│   ├── server.py         ← local API (127.0.0.1 only)
│   ├── desktop.py        ← starts the server, opens the window
│   ├── hardware.py       ← reads your PC, picks the settings
│   └── web/              ← the interface (plain files, no build step)
├── docs/                 ← ARCHITECTURE.md, MODELS.md, banner and demo
├── tests/                ← automatic tests
├── tools/                ← maintenance scripts
└── LICENSE, TERMS.md, PRIVACY.md, NOTICE.md
```

</details>

---

<details open>
<summary><b>📐 The six readability rules</b></summary>
<br>

| Rule | What it checks | In practice |
|---|---|---|
| **Text contrast** | Contrast between each text and the color behind it | Grey on white that fails WCAG gets flagged |
| **Text size** | Size of the texts that are read | Body text too small to read comfortably |
| **Main button** | Is the main action visible and easy to find | A call to action lost among other things |
| **Visual hierarchy** | Does one thing clearly come first | Everything is the same size, nothing leads |
| **Amount of text** | How many words compete for attention | A wall of text above the fold |
| **Clutter** | How crowded the screen is | Too many elements fighting for the eye |

Each screen gets a score. The first screen counts for half of the final score out of 100. The rules are in [`mona/rules.py`](mona/rules.py) and ported to the website with the same thresholds and weights.

</details>

---

<details>
<summary><b>⚙️ How it works inside</b></summary>
<br>

```
window ──► server.py ──► pipeline.py ──► capture.py (test Chrome: open, scroll, read)
(pywebview,   (FastAPI,      │
 or Chrome/    127.0.0.1)    ├── ai/  gaze + brain + detector (ONNX, onnxruntime)
 Edge app)                   └── rules.py  six rules ──► score /100
```

- **Open:** the test Chrome loads the address in a 1440 × 900 window. For an image, Mona cuts it into 900 px screens instead.
- **Read:** for each screen, the page code gives texts, sizes, colors and buttons. For an image, the detector finds them and plan B rebuilds the same information.
- **Look:** two models predict where eyes land and their maps are averaged. One model estimates the brain's response.
- **Judge:** the six rules give a score per screen, then the final score out of 100.

The full diagram and the file by file tour are in [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md).

</details>

---

<details>
<summary><b>❓ FAQ</b></summary>
<br>

**Is it free?**
Yes, for personal, non-commercial use. See the license below.

**Can I use it for client work or in my product?**
Not without written permission from the author. See [LICENSE](LICENSE).

**Does it work on a phone?**
No, it is a desktop app (Windows, macOS, Linux).

**Is it fast?**
On a recent PC, an image takes a few seconds and a page about ten seconds. `python -m mona doctor` shows what Mona chose for your machine.

**Where do my reports go?**
Nowhere: they stay in the app's own storage on your PC. The only network traffic is the visit to the site you analyze.

**Do I need a GPU or an account?**
No. Mona uses a GPU when it finds one, and otherwise runs on the CPU. No account, no API key.

**Can it analyze a page behind a login, or on localhost?**
Not yet. The test Chrome opens public addresses. For a private page, take a screenshot and drop the image.

</details>

---

## 📖 Story & credits

<details>
<summary><b>🙏 Credits: who and what made Mona</b></summary>
<br>

Mona was **written with AI, and we say it plainly.**

| Who | Role |
|---|---|
| **Liam DB** | Creator. The idea, the direction, the decisions, the testing. |
| **[Claude Code](https://claude.com/claude-code)** (Anthropic) | Wrote the code of the project under Liam DB's direction. |

**Built on:** eye-tracking data from UEyes and Imp1k, fMRI data from THINGS, [ONNX Runtime](https://onnxruntime.ai/), [Playwright](https://playwright.dev/) and [FastAPI](https://fastapi.tiangolo.com/).

**Find the creator:** [devliam.com](https://devliam.com) · [mona.devliam.com](https://mona.devliam.com)

The complete list of data, models, libraries and licenses is in [NOTICE.md](NOTICE.md). To cite Mona, use the "Cite this repository" button on GitHub ([CITATION.cff](CITATION.cff)).

</details>

---

## ⚖️ License

**Mona Personal Use License** ([LICENSE](LICENSE), with French translation)

✅ Free to use for yourself: personal, educational, research
✅ Reading and modifying the code for your own use
✅ Your reports are yours
❌ No redistribution, no selling, no use to make money (client work and online services included)
❌ No training other models with it
❌ Credit required ("Mona by Liam DB") whenever you show or publish something that uses it

It is *source-available*, not open source. For anything else, ask the author first.

[Terms of use](TERMS.md) · [Privacy policy](PRIVACY.md) · [Third-party data and licenses](NOTICE.md)

---

<div align="center">

Built by Liam DB, with the help of AI.

</div>

<sub>Keywords: web page analysis, visual saliency, eye-tracking prediction, attention heat map, UX audit, readability score, WCAG contrast, Figma mockup analysis, UI element detection, ONNX, Playwright, desktop app.</sub>
