# Alcohol Unit Tracker — Advanced

A privacy-first, local-only UK alcohol unit tracker for logging drinks, calculating units, viewing rolling 7-day trends, estimating calories and cost, planning drink-free days, and exporting your data.

The app runs as a single HTML file in the browser and stores data in `localStorage`. No account, server, database, or cloud sync is required.

---

## ⚠️ Health Notice

This project is an informational self-tracking tool, not medical advice.

UK guidance advises adults not to regularly drink more than **14 units per week**, and to spread drinking across **3 or more days** with several drink-free days. Alcohol risk is not zero, and people who are pregnant, taking medication, dependent on alcohol, or worried about their drinking should seek professional medical support.

Helpful sources:

* [NHS — Calculating alcohol units](https://www.nhs.uk/live-well/alcohol-advice/calculating-alcohol-units/)
* [GOV.UK — UK Chief Medical Officers’ low risk drinking guidelines](https://www.gov.uk/government/publications/alcohol-consumption-advice-on-low-risk-drinking)
* [Drinkaware — UK low risk drinking guidelines](https://www.drinkaware.co.uk/facts/information-about-alcohol/alcohol-and-the-facts/low-risk-drinking-guidelines)

---

## ✨ Features

### Core Tracking

* Add drinks using quick presets or a custom calculator
* UK alcohol unit calculation:

```text
units = ABV% × volume(ml) ÷ 1000
```

* Track units by day, rolling 7-day window, or Monday-to-Sunday calendar week
* Add custom labels, drink type, ABV, volume, notes, and custom timestamps
* Manually remove units for corrections
* Undo the latest entry
* Repeat or delete individual logged drinks

### Presets

Built-in quick presets include:

* Pint lager
* 440ml beer can
* 175ml wine
* 250ml wine
* Wine bottle estimate
* Single spirit
* Double spirit
* Pint cider
* Alcopop
* Cocktail estimate

You can also save your own custom presets from the calculator.

### Dashboard

The tracker shows:

* Today’s units
* Current week or rolling 7-day units
* Remaining units before the weekly goal
* Drink-free days
* Weekly calories estimate
* Weekly cost estimate
* Daily average
* Trend versus yesterday
* Current progress percentage
* Alcohol-free streak ending yesterday
* Caution-threshold days

### Charts & Visuals

Powered by Chart.js:

* Today’s consumption bar chart
* 7-day history line chart
* Today by drink type doughnut chart
* 12-week heatmap
* This-week planner calendar

### Goals & Planning

* Custom weekly unit limit
* Rolling 7-day or calendar-week tracking mode
* Daily caution threshold
* Drink-free day target
* Remaining allowance planner
* Estimated 30-day pace for units, cost, and calories

### Privacy & Data Safety

* Local-only data storage
* No backend
* No analytics
* No login
* No third-party data upload
* Privacy blur mode for hiding sensitive numbers on screen
* Recovery snapshot save/restore
* Export and import JSON
* Export CSV

### Notifications & Reminders

* Browser notification permission support
* Weekly milestone notifications
* Optional open-page reminder time
* Reminder to log drinks or mark the day as alcohol-free

### Accessibility & UX

* Dark/light mode
* Responsive layout
* Keyboard shortcuts
* Accessible labels and status regions
* High-contrast badges
* Mobile-friendly layout

---

## 🧮 Calculation Details

### Units

```text
units = ABV × ml ÷ 1000
```

Examples:

| Drink         |   ABV | Volume | Units |
| ------------- | ----: | -----: | ----: |
| Pint lager    |  4.0% |  568ml | 2.27u |
| 175ml wine    | 12.0% |  175ml | 2.10u |
| Double spirit | 40.0% |   50ml | 2.00u |
| Pint cider    |  4.5% |  568ml | 2.56u |

### Calories

The default estimate is:

```text
56 kcal per unit
```

This estimates alcohol calories only and does not include mixers, sugar, food, or other ingredients.

### Cost

Cost is estimated using the user-configurable value:

```text
cost = units × pricePerUnit
```

---

## 🚀 Quick Start

### Option 1: Open Directly

1. Download or copy the HTML file.
2. Save it as:

```text
index.html
```

3. Open it in a modern browser.

### Option 2: Run with a Local Server

This is useful if your browser blocks certain local-file features.

Using Python:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

---

## 📁 Suggested Project Structure

```text
alcohol-unit-tracker/
├── index.html
├── README.md
└── screenshots/
    ├── dashboard.png
    ├── charts.png
    └── mobile.png
```

The current app is designed as a single-file project, so only `index.html` is required.

---

## 🕹️ Usage

### Add a Preset Drink

Click one of the quick-add drink buttons. The drink is immediately added to the log with calculated units, calories, and cost.

### Add a Custom Drink

1. Enter a label.
2. Select the drink type.
3. Enter volume in ml.
4. Enter ABV percentage.
5. Optionally change the timestamp.
6. Optionally add a note.
7. Click **Add Drink**.

### Save a Custom Preset

Enter the drink details, then click **Save as Preset**. The preset will be stored locally and shown with the built-in quick presets.

### Correct a Mistake

Use one of the following:

* **Undo Last** to remove the most recent entry
* **Delete** in the entry log to remove a specific entry
* **Manual remove** to subtract units as a correction
* **Reset Today**, **Reset Week View**, or **Reset All** for larger resets

A recovery snapshot can be saved before destructive actions.

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action                             |
| -------- | ---------------------------------- |
| `A`      | Focus the custom drink label input |
| `U`      | Undo last entry                    |
| `T`      | Toggle dark/light theme            |
| `P`      | Toggle privacy blur mode           |
| `E`      | Export JSON                        |

---

## 💾 Data Storage

The app stores data in browser `localStorage` under keys such as:

```text
au_tracker_v3
au_tracker_recovery_snapshot_v3
```

Data remains on the device/browser where it was entered.

Clearing browser storage may delete the tracker data. Use JSON export for backups.

---

## 🧱 Data Model

Example exported JSON structure:

```json
{
  "settings": {
    "weeklyLimit": 14,
    "weekMode": "rolling",
    "pricePerUnit": 0,
    "kcalPerUnit": 56,
    "theme": "light",
    "dailyCaution": 6,
    "drinkFreeTarget": 3,
    "reminderTime": "20:00",
    "remindersEnabled": false
  },
  "entries": [
    {
      "id": "example-id",
      "ts": "2026-05-12T20:00:00.000Z",
      "label": "Pint Lager",
      "type": "Beer",
      "ml": 568,
      "abv": 4,
      "units": 2.27,
      "kcal": 127,
      "cost": 0,
      "note": ""
    }
  ],
  "customPresets": [],
  "meta": {
    "version": 3
  }
}
```

---

## 📤 Export & Import

### Export JSON

Use this for full backup and restore.

### Export CSV

Use this for spreadsheet analysis. CSV includes:

* ID
* Timestamp
* Date
* Label
* Drink type
* Volume
* ABV
* Units
* Calories
* Cost
* Note

### Import JSON

Import replaces the current app state after confirmation. A recovery snapshot is saved before replacement.

---

## 🔐 Privacy Model

This app is designed to be local-first:

* No server requests are made by the app logic
* Data is not uploaded
* Data is stored in browser `localStorage`
* Export files are generated locally
* Privacy mode blurs sensitive dashboard numbers

The only external dependency is Chart.js loaded from a CDN. For fully offline/private use, download Chart.js and reference it locally.

---

## 🌐 Browser Support

Recommended browsers:

* Chrome / Chromium
* Edge
* Firefox
* Safari

Required browser features:

* `localStorage`
* `FileReader`
* `Blob`
* `URL.createObjectURL`
* Optional: Notifications API
* Optional: `crypto.randomUUID`

---

## 🛠️ Customisation

### Change the Default Weekly Limit

In the JavaScript defaults object:

```js
weeklyLimit: 14
```

### Change Default Calories per Unit

```js
kcalPerUnit: 56
```

### Change Default Daily Caution Threshold

```js
dailyCaution: 6
```

### Add More Built-in Presets

Add an item to `builtInPresets`:

```js
{
  id: "example_drink",
  emoji: "🍻",
  label: "Example Drink",
  type: "Beer",
  ml: 330,
  abv: 4.5
}
```

---

## 🧪 Testing Checklist

Before publishing, test:

* [ ] Add each built-in preset
* [ ] Add a custom drink
* [ ] Save a custom preset
* [ ] Delete an entry
* [ ] Repeat an entry
* [ ] Undo last entry
* [ ] Manual remove units
* [ ] Switch rolling/calendar week mode
* [ ] Change weekly limit
* [ ] Change daily caution threshold
* [ ] Toggle dark/light mode
* [ ] Toggle privacy mode
* [ ] Export JSON
* [ ] Import JSON
* [ ] Export CSV
* [ ] Save and restore recovery snapshot
* [ ] Reset today
* [ ] Reset week view
* [ ] Reset all
* [ ] Reload page and confirm data persists
* [ ] Test on mobile width

---

## 🧭 Roadmap Ideas

Possible future improvements:

* PWA install support
* Fully offline bundled Chart.js
* Encrypted local backup export
* Optional passcode lock
* Monthly and yearly reports
* Calendar heatmap by month
* Custom drink categories
* Mood/sleep/hydration correlation notes
* Optional low/no-alcohol substitution planner
* Safer reduction plan templates
* Multi-profile support for separate local users
* Printable PDF summary
* Import from spreadsheet CSV
* Unit goal forecast using trend smoothing

---

## 🧑‍💻 Tech Stack

* HTML5
* CSS custom properties
* Vanilla JavaScript
* Chart.js
* Browser `localStorage`
* Browser File APIs
* Notifications API

No build step is required.

---

## ⚠️ Limitations

* Data is tied to the browser/device unless exported
* Clearing browser storage may erase data
* Notification delivery depends on browser permission and support
* Calorie estimates exclude mixers and non-alcohol ingredients
* Cost estimates depend on the user’s configured £/unit setting
* This app does not diagnose, treat, or assess alcohol dependency

---

## 🤝 Contributing

Ideas, fixes, and improvements are welcome.

Suggested contribution areas:

* Accessibility improvements
* Better mobile layout
* More drink presets
* Better import validation
* Offline/PWA support
* New analytics views
* Safer health messaging

---

## 📄 License

Choose a license before publishing. Suggested options:

* MIT License for open reuse
* GPL-3.0 if you want derivative projects to remain open source
* Private/internal if this is only for personal testing

---

## Disclaimer

This software is provided for educational and personal tracking purposes only. It is not medical advice. If drinking is affecting your health, relationships, safety, work, mood, sleep, or daily life, contact a healthcare professional or local support service.
