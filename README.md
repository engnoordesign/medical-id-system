# Medical National System — prototype

A working, clickable prototype of a unified medical ID system that connects **patients, doctors, clinic secretaries, pharmacies, laboratories and radiology/ultrasound centers** through one profile per patient. The patient's national ID card number (or passport number) is the patient ID, and a QR code opens the profile.

Bilingual interface (Arabic RTL / English), with the language switch in the top bar.

> This is a front-end prototype. All people, clinics and facilities are fictional demo data, and everything you enter is stored only in your own browser (localStorage). No real email is sent.

## Run it

Open `index.html` in a browser. To share it as a web page, enable **GitHub Pages** for this repository (Settings → Pages → Deploy from branch → `main` / root). The camera QR scanner works on GitHub Pages over HTTPS; otherwise use "Upload a photo of the QR code" or type the patient ID.

## Demo accounts

| Role | How to sign in |
|---|---|
| Patient | `omar` / `1234` (has allergies, open prescription, lab and echo orders) · `sara` / `1234` · `yousif` / `1234` |
| Doctor | Pick any doctor; the cardiologist pre-selected has booked patients |
| Secretary | Pick any clinic; the cardiology clinic has pending requests |
| Pharmacy / Lab / Radiology | Pick any facility |

"Reset demo data" in the footer restores the original data.

## What each role can do

**Patient**
- Register: username, password, email → personal and health information with a required photo → identity check by 12-digit national ID or passport → email confirmation code → QR medical card.
- See the full record: visits, prescriptions, lab results with high/low flags, radiology and ultrasound reports, next visit dates.
- Browse 31 specialties and ~110 elite and premium doctors, search, sort by rating, experience or fee.
- Book weekly: pick a free slot this week or next week; the secretary approves. One active booking per doctor per week.
- Cancel bookings, rate doctors after a completed visit (ratings feed the doctor's average).
- Choose a preferred pharmacy, lab and radiology center.
- Notifications inbox showing every email the system sends (booking received, approved, declined, 24-hour reminder, new prescription, dispensed, tests ordered, results ready, follow-up scheduled).
- Access log showing every doctor, pharmacy, lab or imaging center that opened the record.

**Doctor**
- Today's and next 7 days' confirmed patients; start a visit from an appointment or by scanning a patient.
- Visit form: diagnosis, notes, prescription lines (with allergy cross-check), lab tests by group, radiology/ultrasound requests (X-ray, CT, MRI, ultrasound, Doppler, echo, mammography), next visit date (creates a follow-up request for the secretary).
- Full patient history, reservations (current, upcoming, history), ratings and reviews.

**Secretary**
- Pending requests with approve/decline (prevents double-booking), weekly calendar grid, cancel and no-show, reservation history.

**Pharmacy / Laboratory / Radiology**
- Open a patient by QR (camera or photo), patient ID, or from the waiting queue.
- Each sees only what it needs: pharmacy sees allergies and prescriptions, lab sees lab orders, radiology sees imaging orders.
- Pharmacy dispenses all or part of a prescription; lab marks sample collected and enters results; radiology writes findings and impression. Results land on the patient profile and the patient is emailed.

## Planned production build

Stack chosen for the real system: **Node.js + React + PostgreSQL**.

Main tables: `patients`, `identity_documents`, `doctors`, `specialties`, `secretaries`, `facilities` (pharmacy / lab / radiology), `doctor_schedules`, `appointments`, `visits`, `prescriptions`, `prescription_items`, `lab_orders`, `lab_results`, `imaging_orders`, `imaging_reports`, `ratings`, `notifications`, `access_log`.

Items the production version needs beyond this prototype:
- Hashed passwords, sessions/JWT, role-based authorization enforced on the server, two-factor login for staff.
- Real identity verification against the national ID or passport (manual review or an official API), document storage.
- Signed QR codes (a token, not the raw ID) so a printed QR cannot be forged.
- Real email delivery (e.g. SMTP / transactional email service) and scheduled reminder jobs.
- Encryption at rest, audit logging, backups, and compliance with Iraqi health-data rules.
- Admin panel to onboard and verify doctors, pharmacies, labs and imaging centers.
