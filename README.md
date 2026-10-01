# KAP Recorder: setup on GitHub Pages + Firebase

KAP data-collection tool for the study "Effect of a Waiting-Room Educational Video and QPL on Palliative Care KAP among Oncology Outpatients", Oncology OPD, HIMS, SRHU.

The page is hosted on GitHub Pages. The records are saved in Firebase Firestore. Only the Google accounts named in `firestore.rules` can open them.

Setup takes about 20 minutes. Do the steps in order.

---

## Step 1. Create the Firebase project

1. Go to https://console.firebase.google.com and sign in with the study Google account.
2. Click **Create a project**. Name it, for example, `kap-palliative-hims`.
3. Google Analytics is not needed. Switch it off and click **Create project**.

## Step 2. Create the database

1. In the left menu, open **Build › Firestore Database**.
2. Click **Create database**.
3. Location: choose **asia-south1 (Mumbai)**. This keeps the data in India. The location cannot be changed later.
4. Choose **Start in production mode**. Click **Create**.

## Step 3. Switch on Google sign-in

1. In the left menu, open **Build › Authentication**. Click **Get started**.
2. Under **Sign-in method**, choose **Google**. Switch it on, pick a support email and click **Save**.

## Step 4. Set the access list (security rules)

1. Open `firestore.rules` from this folder in any text editor.
2. Replace `STUDENT_EMAIL@gmail.com` and `GUIDE_EMAIL@gmail.com` with the two real Google account emails. Add more emails in the same format if needed, separated by commas.
3. In Firebase, open **Firestore Database › Rules**.
4. Delete everything there, paste the whole edited file, and click **Publish**.

Anyone whose email is not on this list sees "This account can't open the study records".

## Step 5. Connect the page to Firebase

1. In Firebase, click the gear icon › **Project settings**.
2. Under **Your apps**, click the web icon `</>`. Give it a nickname such as `kap-web`. Don't tick Firebase Hosting. Click **Register app**.
3. Firebase shows a block of code with `const firebaseConfig = { ... }`. Copy the six values inside it.
4. Open `index.html`. Near the top of the script, find `FIREBASE_CONFIG`. Replace each `PASTE_HERE` with the matching value. Keep the quotation marks.

These values are not passwords. It is safe for them to be visible in a public GitHub repository. The security rules in step 4 are what protect the data.

## Step 6. Put the page on GitHub Pages

1. Create a new repository on GitHub, for example `kap-recorder`.
2. Upload `index.html` (and this README). Do not upload any exported CSV files to the repository.
3. Open **Settings › Pages**. Under **Source**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`. Click **Save**.
4. After a minute, GitHub shows the address, for example `https://username.github.io/kap-recorder/`.

## Step 7. Allow sign-in from the GitHub address

1. In Firebase, open **Authentication › Settings › Authorized domains**.
2. Click **Add domain** and enter `username.github.io` (your GitHub username, without `https://` and without the repository name).

## Step 8. Test before the first patient

1. Open the GitHub Pages address. Click **Sign in with Google**.
2. Enrol a test participant and complete a T0.
3. Open the same address on a second device. The test record should appear.
4. Delete the test record. Real enrolment starts at KAP-001 only if no test records remain.

---

## Using the tool day to day

- Write the study code (KAP-001 and so on) on the signed consent form. Keep the code-to-name and phone list on paper, in the locked cabinet. Never type names or phone numbers into the tool.
- A record counts only after you press **Save** on the last screen.
- If the OPD has no internet, the tool still saves on the device. The record shows **Not uploaded** until the connection returns. Don't clear the browser's data while anything shows **Not uploaded**.
- Export the CSV every week and keep a copy in the study Google Drive.

## Limits of the free Firebase plan (Spark)

The study needs about 50 records. The free plan allows 1 GB of storage and 20,000 writes and 50,000 reads a day. The study will use a tiny fraction of this, so no billing is needed.
