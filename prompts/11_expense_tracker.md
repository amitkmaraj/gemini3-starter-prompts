
**Project Title:** ReceiptSnap - Mobile Expense Tracker & OCR Scanner

**Role:** Expert Full-Stack Developer & UI/UX Designer specializing in Mobile-First Web Apps.

**Goal:** Build a fully functional, mobile-responsive web application using **React** and **Tailwind CSS** that allows users to photograph receipts, extract data (simulate OCR), and track their monthly expenses.

**Core Tech Stack:**
* React (Functional Components, Hooks)
* Tailwind CSS (for styling)
* Lucide-React (for icons)
* Recharts (for data visualization)
* LocalStorage (for data persistence)

**Design Requirements:**
1.  **Mobile-First UI:** The interface must look and feel like a native iOS/Android app. Use a bottom navigation bar (fixed position) for main menu items.
2.  **Aesthetics:** Clean, modern, "Apple-esque" design. Use rounded corners, subtle shadows, and a large, thumb-friendly font size.
3.  **Theme:** Light mode by default with a toggle for Dark mode. Use a primary color of Emerald Green (#10B981) for financial positivity.

**Key Features & Functionality:**

1.  **The "Scan" Interface (Center Tab):**
    * A large, prominent circular floating action button (FAB) in the center of the bottom nav.
    * When clicked, trigger the device camera (use `<input type="file" accept="image/*" capture="environment" />`).
    * **Simulated OCR:** Since we cannot implement a backend OCR API right now, create a "Scanning..." animation overlay. After 2 seconds, simulate a successful scan by populating a form with mock data (random merchant name like "Starbucks" or "Target", random date, and random amount).
    * Display the captured image thumbnail next to the form.

2.  **Expense Entry Form:**
    * Allow the user to edit the "Scanned" details.
    * Fields: Merchant Name, Total Amount, Date, Category (Dropdown: Food, Transport, Utilities, Entertainment, Other), and Notes.
    * "Save Expense" button.

3.  **Dashboard (Home Tab):**
    * **Summary Cards:** Show "Total Spent This Month" and "Remaining Budget" (allow user to set a simple budget in settings).
    * **Visuals:** A Donut chart showing spending distribution by Category (e.g., how much spent on Food vs. Transport).
    * **Recent Activity:** A scrollable list of the last 5 transactions.

4.  **History / List View (List Tab):**
    * A searchable list of all past expenses grouped by Month/Year.
    * Each row should show the Category Icon, Merchant Name, Date, and Amount.
    * Clicking a row opens a modal to view the receipt image and details.

5.  **Settings & Data:**
    * Option to set a Monthly Budget limit.
    * "Export Data" button that downloads all expenses as a `.CSV` file.
    * "Clear All Data" button (with a confirmation warning).

**Technical Implementation Details:**
* Use `localStorage` to save the array of expense objects so data persists when the browser is refreshed.
* Ensure the app is fully responsive and prevents horizontal scrolling.
* Handle the "empty state" (if no expenses exist) with a friendly illustration and text guiding the user to scan their first receipt.