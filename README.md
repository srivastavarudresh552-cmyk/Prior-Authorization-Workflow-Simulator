# 🏥 Prior Authorization Workflow Simulator

> An interactive, gamified, drag-and-drop simulation of the US healthcare Prior Authorization (PA) process — built as a single self-contained HTML file with zero dependencies.


---

## 🔍 Overview

Prior Authorization (PA) is one of the most complex and consequential administrative processes in US healthcare. Providers must obtain advance approval from insurance payers before delivering certain services — a process that can take days, involve appeals, and significantly impact patient care.

This simulator teaches the full PA lifecycle through hands-on interaction: drag patient case cards through workflow stages, collect clinical documents, evaluate medical necessity, submit to payers, respond to denials, and navigate appeals — all with educational context at every step.

**Who it's for:**
- Medical billing & coding students
- Healthcare administration trainees
- Residency/clinical rotation orientation
- Insurance industry onboarding
- Anyone learning how US health insurance actually works

---

## 🚀 Live Demo

No server, no install, no build step needed.

```bash
# Clone or download the file
git clone https://github.com/yourusername/prior-auth-simulator.git

# Open directly in any modern browser
open prior-auth-simulator.html
```

Or simply **double-click** `prior-auth-simulator.html` — it runs entirely in the browser.

---

## ✨ Features

### 🎮 Gamified Workflow
- **Drag-and-drop** case cards between stages with move validation (no skipping, no going backward)
- **Action buttons** on each card as an alternative to dragging
- **Probabilistic outcomes** — approval/denial chances vary by scenario and how well you prepare
- **Confetti celebration** animation on successful authorization

### 🏥 Three-Lane Board
| Lane | Role | Stages |
|------|------|--------|
| 👤 **Patient** | Intake & information | Registration → Insurance Verification |
| 🩺 **Provider** | Clinical evaluation & submission | Evaluation → Necessity → Documents → Submission |
| 🏛️ **Payer** | Review & decision | Receipt → Clinical Review → Decision → Appeal/P2P → Final |

### 📚 Educational Modals
Every stage opens an educational modal explaining:
- What this step means in real healthcare
- Regulatory requirements and timelines
- Common mistakes and how to avoid them
- Clinical criteria used by payers (InterQual, MCG)

### 📊 Progress & Metrics
- **11-step progress tracker** across the top with animated pulse indicator
- **Days elapsed counter** (scenario-specific timelines)
- **Efficiency score (0–100)** updated in real time
- **Efficiency grade (A–D)** on case completion
- **Workflow summary** with full step-by-step timeline on completion

### ⚖️ Decision Outcomes
| Outcome | Description |
|---------|-------------|
| ✅ Approved | Payer authorizes the procedure |
| ❌ Denied | Criteria not met; appeal options presented |
| ⏳ Pended | Additional information requested |
| 📝 Appeal | First-level appeal with additional documentation |
| 🤝 Peer-to-Peer (P2P) | Ordering physician calls payer's Medical Director |
| ✅ Approved (after appeal) | Denial reversed on appeal |
| ❌ Final Denial | All options exhausted |

---

## 🧑‍⚕️ Patient Scenarios

Four pre-built scenarios cover the most common PA categories, each with unique documents, necessity criteria, denial probabilities, and educational content:

### 1. 🔴 Elective Surgery — Maria Chen
- **Procedure:** Total Right Knee Arthroplasty (CPT: 27447)
- **Insurance:** BlueCross PPO
- **Urgency:** Routine
- **Key challenge:** Documenting 6+ months of failed conservative treatment
- **Initial denial chance:** ~35%

### 2. 🟣 MRI Scan — James Okafor
- **Procedure:** Brain MRI w/ and w/o Contrast (CPT: 70553)
- **Insurance:** Aetna HMO
- **Urgency:** Urgent
- **Key challenge:** Justifying imaging over conservative management
- **Initial denial chance:** ~20%

### 3. 🟢 Specialty Medication — Sofia Martinez
- **Procedure:** Adalimumab / Humira 40mg (Crohn's Disease)
- **Insurance:** United Healthcare EPO
- **Urgency:** Urgent
- **Key challenge:** Step therapy compliance + mandatory safety labs (TB, Hepatitis)
- **Initial denial chance:** ~45% (highest — biologic medications are heavily scrutinized)

### 4. 🟡 Inpatient Admission — Robert Nguyen
- **Procedure:** Inpatient hospitalization for CHF exacerbation
- **Insurance:** Medicare Advantage (Humana)
- **Urgency:** Emergent
- **Key challenge:** Concurrent review / daily authorization, inpatient vs. observation status
- **Initial denial chance:** ~15%

---

## 🔄 Workflow Stages

```
[Patient Lane]                [Provider Lane]                    [Payer Lane]
      │                              │                                │
 1. Intake               3. Medical Evaluation          7. Payer Receipt
 2. Insurance Verify     4. Necessity Assessment        8. Clinical Review
                         5. Document Collection         9. Decision
                         6. PA Submission              10. Appeal / P2P
                                                       11. Final Outcome
```

Each stage adds days to the elapsed counter, and the score is adjusted based on how thoroughly you prepared at each step.

---

## 🏆 Scoring System

Start with **100 points**. Points are deducted for inefficiencies that mirror real-world consequences:

| Event | Score Impact |
|-------|-------------|
| Unmet necessity criteria at assessment | −10 |
| Missing documents at submission (per doc) | −8 |
| Pended request (additional info needed) | −8 |
| Initial denial received | −15 |
| Workflow exceeding 14 days | −5 |
| Extended processing (per day over 20) | −2/day |
| Accepting denial without appealing | −20 |
| Successful approval | +0 (no bonus needed) |
| Successful appeal/P2P reversal | +10 |
| Clean first-pass approval | +20 |

**Grade Scale:**
| Score | Grade |
|-------|-------|
| 85–100 | A |
| 70–84 | B |
| 55–69 | C |
| 0–54 | D |

---

## 🕹️ How to Use

1. **Open** `prior-auth-simulator.html` in any modern browser
2. A random patient scenario loads automatically
3. **Click the action button** on the case card, or **drag the card** to the next stage column
4. Read the educational modal at each step — it explains real-world context
5. Make decisions: check documents, assess necessity, choose to appeal or accept
6. Complete the workflow to see your **efficiency grade and full timeline**
7. Click **↺ New Patient** to load a new scenario and try again

### Tips for a High Score
- ✅ Check **all documents** before submitting
- ✅ Confirm **all necessity criteria** are met before submission
- ✅ Always **appeal a denial** rather than accepting it
- ✅ Use **P2P review** for the highest reversal rates
- ✅ Move efficiently — delays lower your score

---

## 🛠️ Customization

### Adding New Scenarios

Find the `SCENARIOS` array near the top of the `<script>` section and add a new entry:

```javascript
{
  id: 'my-new-scenario',
  type: 'Physical Therapy',
  typeBadge: 'badge-surgery',         // badge-surgery | badge-mri | badge-rx | badge-admit
  name: 'Alex Thompson',
  age: 45,
  insurance: 'Cigna PPO',
  diagnosis: 'Lumbar disc herniation (ICD-10: M51.16)',
  procedure: 'Physical Therapy — 12 sessions (CPT: 97110)',
  urgency: 'routine',                 // routine | urgent | emergent
  estimatedCost: '$2,400',
  docs: [
    'Physician referral',
    'MRI report confirming herniation',
    'Failed conservative treatment (NSAIDs)',
  ],
  necessityFactors: [
    { label: 'Imaging confirms diagnosis', met: true },
    { label: 'Failed medication management', met: false },
  ],
  initialDenialChance: 0.25,          // 0.0 – 1.0
  appealSuccessChance: 0.75,          // 0.0 – 1.0
  daysPerStep: {
    intake: 1, eval: 1, docCollection: 2,
    submit: 1, review: 3, decision: 2, appeal: 5, p2p: 2
  },
  education: {
    intake: 'Your educational text here...',
    eval: '...',
    docCollection: '...',
    submit: '...',
    review: '...',
    approved: '...',
    denied: '...',
    appeal: '...',
    p2p: '...',
  },
}
```

### Adjusting Scoring Penalties

Search for `penalizeScore(` and `rewardScore(` calls in the JavaScript to tune the point values.

### Changing Colors

All colors are defined as CSS custom properties in `:root` at the top of the `<style>` block:

```css
:root {
  --navy:      #0B2545;
  --blue:      #1565C0;
  --mid-blue:  #1E88E5;
  /* ... */
}
```

---

## 🧰 Tech Stack

| Technology | Usage |
|------------|-------|
| **HTML5** | Structure and semantic markup |
| **CSS3** | Custom properties, Flexbox, Grid, animations, responsive layout |
| **Vanilla JavaScript (ES6+)** | All state management, drag-and-drop, modal engine, scoring |

**Zero external dependencies.** No frameworks, no CDNs, no build tools, no `node_modules`.

---

```

Everything is in one file, organized in clearly commented sections:

```
<style>
  /* Design Tokens (CSS variables) */
  /* Component styles: header, progress tracker, lanes, cards, modals, etc. */
</style>

<body>
  <!-- Celebration layer (confetti) -->
  <!-- Summary panel -->
  <!-- Modal overlay -->
  <!-- App header -->
  <!-- Progress tracker -->
  <!-- Scenario bar -->
  <!-- Main 3-lane board -->
</body>

<script>
  // SCENARIOS array       ← edit this to add/change cases
  // WORKFLOW_STAGES array ← stage definitions
  // Application state     ← single state object
  // UI builders           ← buildProgressTracker(), buildLaneStages()
  // Card management       ← createCard(), placeCardInStage()
  // Drag-and-drop         ← onDragStart/End/Over/Leave/Drop
  // Stage modals          ← showStageModal() with per-stage definitions
  // Scoring               ← penalizeScore(), rewardScore()
  // Modal engine          ← openModal(), closeModal()
  // Summary panel         ← showSummaryPanel()
  // Celebration           ← launchConfetti()
</script>
```

---

## 💡 Use Cases

- **Healthcare administration courses** — assign as a hands-on lab exercise
- **Medical billing training programs** — illustrate the full PA lifecycle
- **Hospital orientation** — onboard new utilization review staff
- **Insurance company training** — help new reviewers understand the provider side
- **Personal learning** — understand why your insurance requires prior auth
- **Portfolio project** — demonstrates complex vanilla JS, drag-and-drop, and gamification

---

---

<div align="center">

Built with ❤️ using HTML, CSS & Vanilla JavaScript — no frameworks, no dependencies, no nonsense.

</div>
