FMS - FLEET FINANCIAL MANAGEMENT SYSTEM (multi-company)

FILES: index.html, config.js, firebase-rules.json, manifest.webmanifest, sw.js, icon-192.png, icon-512.png

1. DEPLOY
   New GitHub repo (e.g. fms), upload all files, then Netlify > Import from GitHub (leave build settings empty).
   Out of the box it runs in DEMO MODE: data stays in one browser and is NOT secure. Use it only to try the screens.

2. GO LIVE (secure, shared) - free Firebase account, easiest on a computer
   a. console.firebase.google.com > Add project.
   b. Build > Realtime Database > Create database (locked mode).
   c. Rules tab: paste the whole content of firebase-rules.json, then Publish.
   d. Build > Authentication > Get started > Email/Password > Enable.
   e. Authentication > Users > Add user: your ADMIN email + password. Copy that user's UID.
   f. Realtime Database > Data: add child  admins  with a child named by that UID and value  true
   g. Project settings (gear) > General: copy the Web API Key. Copy the database URL from the Data tab.
   h. Edit config.js, paste both values, commit. Netlify redeploys.

3. HOW IT WORKS
   Admin: Admin tab, your admin email and password. Approve, suspend, open or delete companies.
   Company: Register tab (gets a Company ID like C12345). Admin approves. Then sign in with Company ID + User ID + password.
   Workers: the company Owner creates them in Staff. They sign in with Company ID + Worker ID + password.
   Access levels: Owner (all), Manager (fleet, imports, ledger, rates, reports), Accountant (ledger, rates, reports), Viewer (read-only dashboards).
   Each company only reads and writes its own data. The database rules enforce this on the server.

4. LIMITS - PLEASE READ
   - I could not test the rules or live login against a real Firebase project. Test with two test companies before real use,
     using the Rules Playground in the Firebase console.
   - Passwords cannot be reset from the app. To "reset" a worker: remove the worker and create a new login.
   - The Download buttons are hidden for Viewers, but a Viewer can still read the data they are allowed to see.
   - Do not enter vehicle or driver data you are not allowed to store. Check local data protection rules.
