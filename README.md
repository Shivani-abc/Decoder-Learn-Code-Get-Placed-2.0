# Decoder — learning and coding platform prototype

A responsive learning-platform prototype preserving the existing dark/purple visual design and animated background, with course paths, embedded video lessons, quizzes, progress, certificates, coding practice, hackathons, internships, resources, and a Razorpay checkout starter.

## Run the website

For ordinary UI exploration, `index.html` can be opened in a browser. **For payment testing, do not use file:// or VS Code Live Server.** The payment API must be served by the Express backend:

1. Install Node.js 18+.
2. Open a terminal in `backend/`.
3. Run `npm install`.
4. Copy `.env.example` to `.env` and add your Razorpay **test-mode** credentials.
5. Run `npm start` and keep the terminal open.
6. Visit **http://localhost:3000**.
7. Sign in to the demo profile, navigate to **Payments & Plans**, and click **Check backend** before checkout.

See `backend/README.md` for payment error troubleshooting and production requirements. Never put the Razorpay Key Secret in frontend code or commit `.env`.

## Payment notes

The checkout UI now shows payment connection diagnostics, uses clearer errors, avoids loading the checkout script repeatedly, verifies the checkout response server-side, and the backend attempts to capture authorized payments. It still needs real test keys and a successful Razorpay test transaction to verify the end-to-end flow in your environment.

## Prototype limitations

- Demo login and student progress are stored in the browser, not a shared authenticated database.
- The coding practice runner is not a secure multi-language hidden-test judge. Never run untrusted code directly on a production server.
- Certificates are prototype credentials, not accredited qualifications.
- Hackathon pages link to event organizers/listings; confirm current dates, eligibility, and registration status on the official event page.
- Before accepting real payments, implement persistent orders, users, entitlements, webhooks, idempotency, refunds, rate limits, HTTPS, and server-side access checks.


## Demo payment mode (no account or API keys)

The Payments & Plans page now has a local demo upgrade for student presentations. Click **Try demo upgrade — no payment** to enable demo Pro access in this browser. It does not contact Razorpay, charge money, or verify a purchase. The payment history labels this as DEMO. No backend is required for this simulated flow. Do not present demo access as a real transaction.

## New learning features (v2.1)

- **AI Coding Mentor (local mode):** choose a language and goal, paste a snippet, and receive lightweight rule-based hints. It runs in the browser, does not upload code, and is explicitly not presented as a connected generative-AI model. A real conversational AI provider requires a configured provider API and secure server-side integration; no API key is bundled.
- **XP, streaks and badges:** course lesson completion, quiz submissions and coding submissions record a local activity day. Existing XP awards are preserved. Badge unlocks are calculated from saved progress, quiz results, sample-judge results and streaks.
- **Progress Analytics:** course completion bars, quiz score overview, coding submission count and a 28-day activity calendar.
- **Storage:** learning activity remains in the browser's local storage on that device. Clearing browser storage or switching devices can remove/change this data; it is not a global account-backed service.

### Smoke tests

From the project root, run:

```bash
node tests/smoke-test.js
```

The test checks that the new routes/features are present and the single-file distribution matches `index.html`. Also validate inline JavaScript with:

```bash
node -e "const fs=require('fs');const s=fs.readFileSync('index.html','utf8');fs.writeFileSync(require('os').tmpdir()+'/decoder-inline.js',[...s.matchAll(/<script>([\\s\\S]*?)<\\/script>/g)].map(x=>x[1]).join('\\n'))"
node --check "%TEMP%\\decoder-inline.js"
```

The smoke tests do not replace a full browser QA run. Payment processing remains demo-only unless a real provider account and correctly configured server-side keys are added.

## Career prep and design expansion (v2.2)

- **Additional courses:** Java & OOP, Machine Learning Foundations, React Frontend Development, Cloud Computing & AWS Basics, and Cybersecurity Essentials. These use public video embeds; video IDs and timestamps are curated examples, and playback depends on the source owner allowing embedding.
- **Practice Tasks:** extra prompts for arrays, strings, hashing, sliding windows, trees, graphs, dynamic programming, SQL, OS, DBMS, networking, system design and behavioral interviews. They are original practice prompts, not claimed to be official company questions.
- **Mock Interview Studio:** choose a target company, role and level; move through six practice questions; save answer notes locally; use a self-review checklist. Completion records local activity and a demo XP reward. It does not record audio or use a live AI interviewer.
- **Expanded company directory:** 60 company targets for organizing practice, including Google, Microsoft, Amazon, TCS, Infosys, Wipro, Accenture, Zoho, Adobe, NVIDIA, Flipkart, Goldman Sachs, PayPal, Uber, PhonePe, Razorpay and others. The names are preparation labels only; Decoder is not affiliated with these employers and the prompts are not verified company interview questions.
- **Visual refresh:** brighter white card outlines, improved hover/focus states, richer multicolor hero gradients and cleaner company chips while preserving the existing dark/purple theme and animated background.
- **Local persistence:** mock interview target, question progress and notes are stored in browser local storage. No cross-device sync is provided.

### Test the updated build

From the project root run `node tests/smoke-test.js`. The test checks required feature markers and that `decoder-single-file.html` exactly matches `index.html`. Validate inline JavaScript syntax using the command in the smoke-test section above. This is static/smoke validation, not full end-to-end browser QA.


## Internship board expansion (v2.3)

- **Internship & early-career panel:** 28 role-specific search paths across Microsoft, Google, Amazon, Adobe, NVIDIA, IBM, Accenture, Deloitte, Infosys, TCS, Wipro, Zoho, Freshworks, PhonePe, Razorpay, Swiggy, Flipkart, Atlassian, Cisco, Salesforce, JPMorgan Chase, Goldman Sachs, Intel, Dell and startup-role boards.
- **Search and filters:** search company, role and skills; filter by area and remote-friendly search boards.
- **Application tracker:** track a role from the listing, add an optional application URL, update status (Planning, Applied, Assessment, Interview, Offer or Rejected), and remove entries. Entries are saved locally in this browser.
- **Important accuracy note:** these are links to employer career pages or job-search portals, not a live feed of verified vacancies. Availability, eligibility, location and deadlines must be checked on the destination site. Decoder does not apply to jobs on the user's behalf.
- **Design:** the panel uses the existing purple animated theme with brighter white borders, gradients and responsive cards.

### Current smoke tests

Run `node tests/smoke-test.js` from the project root. It checks the internship catalogue, filters, tracker controls, key routes and single-file parity. This is static validation and does not confirm that any employer currently has an open internship.

## Placement panel: internships and drives

The Placement Drives panel now includes a searchable internship preview alongside placement-drive targets. Internship paths include company, role, focus area, location/work-mode notes, skills, official career/search links, and a **Track role** action that saves to the browser-local application tracker. Use **Browse all internships** for the full catalogue. Employer links are search/career pages, not confirmation that a vacancy is currently open. The drive dates and salary figures are sample/demo content and should be verified before use.

Additional feature ideas for a future release: resume-to-internship skill matching, application deadline calendar and reminders, company-specific preparation roadmaps, a placement readiness score based on transparent criteria, and opt-in vacancy alerts from a verified job feed.


## Placement Command Centre (new)

Open **Placement Command Centre** from the Tools section after signing in. It includes:

- Resume-to-role keyword overlap checker (local-only; not an ATS guarantee)
- Placement readiness checklist and practice indicator
- Application Kanban statuses (Saved, Applied, Assessment, Interview, Offer, Rejected)
- Deadline list, company preparation roadmaps, and a searchable company target directory
- Five-question aptitude mini-test and HR interview practice notes
- Referral contact tracker and saved internship/job-search preferences
- Local JSON export and a prototype admin summary

The toolkit stores its data in this browser's local storage. It does not send applications, issue real-time job alerts, send notifications, verify open vacancies, or provide a secure multi-user admin system. A production version would need authentication, server-side roles, a database, a job-feed integration, and appropriate privacy/security controls. Company and role names are research targets; verify openings and application details on official employer websites.

## Run smoke tests

From the project folder, run:

```bash
node tests/smoke-test.js
```

The smoke tests check expected feature markers and consistency between the regular and single-file HTML. They are not a substitute for full browser or end-to-end tests.

## Latest placement toolkit additions

- **Offer comparison planner:** locally save company, role, and user-entered compensation estimates; remove entries as needed.
- **Weekly placement study planner:** check off DSA, aptitude, CS fundamentals, project/resume work, mock interview, and application-review goals.
- These are planning utilities, not salary research or job offers. Data is stored in the current browser profile.

## Download troubleshooting

If a `sandbox:` download link does not react when clicked, try opening ChatGPT in a desktop browser, right-clicking the download link and selecting **Save link as…**, or refreshing the conversation and trying again. The ZIP is an ordinary archive and can be extracted with Windows File Explorer.

## Resume builder and reliability improvements

The Resume Builder now has structured fields for contact details, target role, professional summary, education, grade (optional), skills, project title/description, experience/leadership, and professional links. It updates a preview safely (user text is escaped), saves drafts in the current browser, includes a basic completeness checklist, and supports browser Print / Save as PDF plus standalone HTML export. The checklist is an advisory heuristic, not a certified ATS score. Resume draft data stays in local browser storage unless the user exports it.

The Course Library now supports filtering by difficulty and course category, with a visible result count and a clearer empty-filter state. Placement-drive tracking choices persist in the current browser. All local features remain browser-local; they are not synchronized across accounts/devices.


## Additional tools in this update

- **Project Portfolio Tracker**: add projects, stack, summary, repository/demo links and status; remove projects and export the inventory to JSON.
- **Technical Interview Deck**: generate practice questions by topic (DSA, web, SQL/DBMS, operating systems, system design, AI/ML), save answer notes locally, remove notes and export them as JSON.

Both tools use browser local storage and are accessible from the Tools menu. They do not require external API keys. Interview prompts are practice material and are not represented as official employer questions.
