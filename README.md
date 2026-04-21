# EduMatch 🎓
## Currently all information are dummy but website is fully functional

> **Connecting students and parents with the right tutors — instantly, locally, for free.**
EduMatch is a lightweight tutor discovery platform built for India. Students and parents can browse verified tutors by city, locality, board, subject, and teaching mode — while tutors can register their profiles in under 2 minutes. No login. No app. Just open the link and find your match.

---

## ✨ Features

### For Students & Parents
- Browse tutor cards with name, qualification, experience, subjects, location, and teaching style
- Filter by **City**, **Locality**, **Board** (CBSE / ICSE / State / IB), **Experience**, **Mode**, and **Subject**
- One-tap **Call** and **WhatsApp** contact buttons on every card
- Mobile-friendly layout — works seamlessly on any device

### For Tutors
- Simple registration form — takes less than 2 minutes
- Fields include: Name, Phone, Email, Qualification, Experience, Boards, Standards, Subjects, Locality, City, Address, Description, and Teaching Mode
- Profile goes live **instantly** after submission — no approval wait

### Platform
- **No login system** — zero friction for both students and tutors
- **Live data** — every page load fetches directly from Google Sheets, so updates reflect immediately
- **Free forever** — no subscriptions, no ads, no paywalls

---

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Backend | Google Apps Script (Web App) |
| Database | Google Sheets |
| Fonts | Playfair Display + DM Sans (Google Fonts) |
| Hosting | Any static host (GitHub Pages, Netlify, Vercel) |

No frameworks. No npm. No build step. Just four files.

---

## 📁 Project Structure

```
edumatch/
├── index.html              # Home page — role selector (Student / Tutor)
├── student.html            # Tutor listing page with filters
├── teacher.html            # Tutor registration form
└── google_apps_script.js   # Backend — paste into Apps Script editor
```

---

## 🚀 Setup & Deployment

### 1. Set up the Backend (Google Apps Script)

1. Open your Google Sheet → **Extensions → Apps Script**
2. Delete all existing code → paste the contents of `google_apps_script.js`
3. Click **Deploy → New deployment**
   - Type: **Web App**
   - Execute as: **Me**
   - Who has access: **Anyone**
4. Copy the deployment URL

### 2. Update the Frontend

Open `student.html` and `teacher.html` and replace the `API_URL` value with your deployment URL:

```js
const API_URL = "https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec";
```

### 3. Host the Frontend

Upload `index.html`, `student.html`, and `teacher.html` to any static host:

- **GitHub Pages** — free, works out of the box
- **Netlify** — drag and drop the folder
- **Vercel** — connect your GitHub repo

All three files must be in the **same folder**.

---

## 🗃️ Google Sheet Structure

The backend expects a sheet tab named **Tutors** with these columns in order:

| A | B | C | D | E | F | G | H | I | J | K | L | M | N |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Timestamp | Name | Phone | Email | Qualification | Experience | Boards | Standards | Subjects | Locality | City | Address | Description | Mode |

The script creates headers automatically on first run if the sheet is empty.

**Tips for manual entries:**
- **Boards** → comma-separated: `CBSE, ICSE`
- **Standards** → comma-separated: `6-8, 9-10`
- **Mode** → exactly `Home`, `Online`, or `Both`
- **Experience** → number only, e.g. `5`

---

## ⚡ How It Works

```
Student opens student.html
        ↓
Page fetches GET ?action=getTutors → Apps Script reads Google Sheet
        ↓
All tutor rows returned as JSON → rendered as cards
        ↓
Filters apply instantly in-browser (no extra requests)
```

```
Tutor fills teacher.html form → submits
        ↓
GET ?action=register&data={...} → Apps Script appends row to sheet
        ↓
Next student page load shows the new tutor
```

> **Why GET for writes?** Google Apps Script redirects cross-origin POST requests, causing browsers to drop the request body (a known Fetch API + Apps Script quirk). Encoding the payload as a GET query parameter bypasses this entirely.

---

## 📱 Pages Overview

### `index.html` — Home
Landing page with animated background and two role-selection cards. Students/parents go to the listing page; tutors go to the registration form.

### `student.html` — Find a Tutor
Displays all tutors as responsive cards. Sidebar filters let users narrow down by city, locality, board, experience, mode, and subject. Each card has direct Call and WhatsApp buttons.

### `teacher.html` — Register as Tutor
Clean registration form with chip-style multi-selects for boards and standards, radio buttons for teaching mode, and instant toast feedback on submission.

---

## 🙌 Contributing

Pull requests are welcome! If you find a bug or want to suggest a feature, open an issue.

Some ideas for future improvements:
- Add a tutor search bar
- Add pagination for large tutor lists
- Add a "Featured Tutors" section
- Admin panel to approve/reject tutor submissions
- SMS notification on new registration

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

*Built with ❤️ for students and teachers across India.*
