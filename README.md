# formioResultsStatisticsNpm

> **The packaging layer.** Takes the core logic from `formioResultsStatistics` and prepares it for distribution as an npm package — making form.io submission analytics available to any JavaScript project.

[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![npm](https://img.shields.io/badge/npm-CB3837?style=flat-square&logo=npm&logoColor=white)](https://www.npmjs.com)
[![formio.js](https://img.shields.io/badge/form.io-JS_SDK-blue?style=flat-square)](https://formio.github.io/formio.js/)
[![Status](https://img.shields.io/badge/status-packaging_phase-yellow?style=flat-square)](#)

---

## What This Repo Does

`formioResultsStatisticsNpm` bridges the gap between the prototype in [`formioResultsStatistics`](https://github.com/seansqlifting29/formioResultsStatistics) and a distributable npm package.

It takes the core statistical functions developed during the research phase and structures them for:

- npm publishing (package metadata, entry points, exports)
- consumption by external projects via `npm install`
- integration into JustTrain and any other form.io-based application

> The final, production-ready TypeScript version of this library lives in [`formio-stats`](https://github.com/seansqlifting29/formio-stats).

---

## The Problem It Solves

[form.io](https://formio.github.io/formio.js/) has no native way to analyse submissions in aggregate. Given a set of form responses in JSON format, this library generates the statistical summaries needed to answer questions like:

- *What percentage of users selected each checkbox option?*
- *How has a tracked value (e.g. weight, score) changed across a population over time?*
- *What is the distribution of responses across a given field?*

This eliminates the need for external survey tools like SurveyMonkey when form.io is already handling data collection.

---

## Repository Map

```
formioResultsStatisticsNpm/
├── Formio-Results-Statistics/   # Core source functions structured for npm
├── ProjectNo.1/                 # First use case implementation
└── README.md
```

---

## Usage

Once published to npm, the package can be installed in any JavaScript project:

```bash
npm install formio-results-statistics
```

```javascript
const { distribution } = require('formio-results-statistics');

const result = distribution(formioSubmissions, 'userSatisfied');
// Returns: { percentageOfTrue: 80, percentageOfFalse: 20 }
```

### How it works

The function iterates every submission in the JSON object, then iterates every field inside `submission.data`. When it finds a field matching `checkBoxId`, it increments either `trueCount` or `falseCount`. At the end it returns the percentage split across all submissions:

```typescript
export const distribution = function(formioSubmissions: any, checkBoxId: string) {
    var trueCount = 0;
    var falseCount = 0;
    for (var key in formioSubmissions) {
        for (var sub_key in formioSubmissions[key].data) {
            if (formioSubmissions[key].data[sub_key] === true && sub_key === checkBoxId) {
                trueCount++;
            }
            if (formioSubmissions[key].data[sub_key] === false && sub_key === checkBoxId) {
                falseCount++;
            }
        }
    }
    return {
        percentageOfTrue: (trueCount * 100) / (trueCount + falseCount),
        percentageOfFalse: (falseCount * 100) / (trueCount + falseCount)
    }
}
```

---

## Related Repositories

| Repo | Role |
|---|---|
| [`formioResultsStatistics`](https://github.com/seansqlifting29/formioResultsStatistics) | Research & prototype |
| [`formioResultsStatisticsNpm`](https://github.com/seansqlifting29/formioResultsStatisticsNpm) | ← You are here — npm packaging layer |
| [`formio-stats`](https://github.com/seansqlifting29/formio-stats) | Final TypeScript library (MIT licensed) |

---

## Context: JustTrain

JustTrain is a fitness coaching application that uses form.io's JS SDK without its cloud platform. This package was developed to give coaches population-level insight from training forms — replacing expensive external analytics services with a lightweight, embeddable library.

---

## Author

**Sean Tyndale** — Creative Developer

[![Portfolio](https://img.shields.io/badge/Portfolio-seantyndale.com-informational?style=flat-square)](https://seantyndale.com)
[![GitHub](https://img.shields.io/badge/GitHub-seansqlifting29-181717?style=flat-square&logo=github)](https://github.com/seansqlifting29)
