<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <title>Pardon Eligibility Checker</title>

    <style>
        /* ------------------------------------------------------- */
        /* BASE PAGE STYLES */
        /* ------------------------------------------------------- */
        html, body {
            height: 100%;
            width: 100%;
            margin: 0;
            padding: 0;
            background: #ffffff; /* your intended background */
        }
        body {
            font-family: 'Inter', sans-serif;
            display: flex;
            flex-direction: column;
        }
        /* ------------------------------------------------------- */
        /* CARD STYLING */
        /* ------------------------------------------------------- */
        .container-card {
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            max-width: 90%;
            margin: 2rem auto;
            background-color: #ffffff;
            border-radius: 0.75rem;
        }
        /* Mobile adjustment */
        @media (max-width: 640px) {
            .container-card {
                max-width: 100%;
                margin: 0;
                border-radius: 0;
                box-shadow: none;
            }
        }
        .section-header {
            color: #1a4d8c;
            border-bottom: 2px solid #e6f2ff;
            padding-bottom: 0.5rem;
            margin-bottom: 1.5rem;
            font-weight: 600;
        }
        /* ------------------------------------------------------- */
        /* DATE INPUT STYLING - UPDATED TO BE LONGER (w-52) */
        /* ------------------------------------------------------- */
        input[type="date"]::-webkit-calendar-picker-indicator {
            opacity: 0;
            width: 100%;
            position: absolute;
            cursor: pointer;
        }
        input[type="date"]::-moz-calendar-picker-indicator {
            /* Firefox does not support opacity trick, so hide completely */
            display: none;
        }
        input[type="date"] {
            border: 1px solid #d1d5db;
            padding: 0.6rem 1rem 0.6rem 2.5rem;
            border-radius: 0.5rem;
            width: 100%;
            transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
            background-color: #f9fafb;
            cursor: pointer;
            position: relative;
        }
        select {
            border: 1px solid #d1d5db;
            padding: 0.6rem 1rem;
            border-radius: 0.5rem;
            width: 100%;
            transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
            background-color: #f9fafb;
            cursor: pointer;
        }
        input[type="date"]:focus, select:focus {
            border-color: #4f46e5;
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.3);
            outline: none;
        }
        input[type="date"]:disabled {
            background-color: #e5e7eb;
            color: #9ca3af;
            cursor: not-allowed;
            padding-left: 1rem; /* Adjust padding when icon is hidden */
        }
        .clickable-label {
            cursor: pointer;
        }
        .date-input-group {
            display: flex;
            align-items: center;
        }
    </style>
</head>

<body>
    <div id="app" class="container-card p-6 md:p-10">
        <header class="text-center mb-6 flex items-center justify-center space-x-4">
            <h1 class="text-2xl font-bold text-gray-800 my-4">Pardon Eligibility Checker</h1>
            <img src="https://www.torontomu.ca/content/dam/law/images/TMU-Law-rgb.svg"
                alt="TMU Law Logo"
                class="h-16 w-auto"
                style="max-width: 300px;">
        </header>

        <section class="mb-8 p-4 bg-blue-50 border-l-4 border-blue-500 rounded-lg">
            <h2 class="text-xl section-header text-blue-700">Disclaimer</h2>
            <p class="text-sm text-blue-600 mb-4">Eligibility results are for informational purposes only. They are provided in good faith, based solely on the information you enter. This tool does not constitute legal advice, and using it does not guarantee that a record suspension will be granted or denied by the Parole Board of Canada.</p>
            <label class="flex items-center space-x-2 cursor-pointer">
                <input type="checkbox" id="disclaimer-accepted" class="form-checkbox h-5 w-5 text-blue-500 rounded-md">
                <span class="text-sm text-gray-700 font-medium">I accept the disclaimer and wish to proceed</span>
            </label>
        </section>

        <section id="input-form" class="space-y-6" style="display: none;">
            <h2 class="text-xl section-header">Conviction Details</h2>

            <div class="space-y-2">
                <label for="conviction-date" class="block text-sm font-medium text-gray-700 clickable-label">Date of conviction</label>
                <div class="date-input-group space-x-4">
                    <div class="relative w-52">
                        <input type="date" id="conviction-date" class="w-full">
                        <svg class="absolute left-2.5 top-1/2 -translate-y-1/2 h-5 w-5 text-gray-500 pointer-events-none" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                        </svg>
                    </div>
                    <label class="flex items-center space-x-2 text-sm">
                        <input type="checkbox" id="dont-know-conv-date" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span>I'm not sure</span>
                    </label>
                </div>
            </div>

            <div class="space-y-2">
                <label for="sentence-completion-date" class="block text-sm font-medium text-gray-700 clickable-label">Sentence completion date</label>
                <div class="date-input-group space-x-4">
                    <div class="relative w-52">
                        <input type="date" id="sentence-completion-date" class="w-full">
                        <svg class="absolute left-2.5 top-1/2 -translate-y-1/2 h-5 w-5 text-gray-500 pointer-events-none" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                        </svg>
                    </div>
                    <label class="flex items-center space-x-2 text-sm">
                        <input type="checkbox" id="dont-know-sent-comp-date" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span>I'm not sure</span>
                    </label>
                </div>
                <p class="text-xs text-blue-700 mt-1">Completion means all fines paid, probation ended, and custodial term served.</p>
            </div>

            <div class="space-y-2">
                <label for="prosecution-type" class="block text-sm font-medium text-gray-700">Prosecution type</label>
                <select id="prosecution-type" class="w-full">
                    <option value="" disabled selected>Select an option</option>
                    <option value="I'm not sure">I'm not sure</option>
                    <option value="Indictment">Indictment</option>
                    <option value="Summary">Summary</option>
                </select>
            </div>

            <div class="space-y-2">
                <label for="schedule1-offence" class="block text-sm font-medium text-gray-700 flex justify-between items-center">
                    <span>Is it a Schedule 1 offence?</span>
                    <span id="schedule1-info-toggle" class="text-blue-500 hover:text-blue-700 text-xs cursor-pointer underline">What are Schedule 1 Offences?</span>
                </label>
                <select id="schedule1-offence" class="w-full">
                    <option value="" disabled selected>Select an option</option>
                    <option value="I'm not sure">I'm not sure</option>
                    <option value="Yes">Yes</option>
                    <option value="No">No</option>
                </select>
                <div id="schedule1-info" class="hidden mt-2 p-3 text-xs bg-blue-50 border-l-4 border-blue-500 text-blue-800 rounded">
                    <p class="font-bold mb-1">Schedule 1 generally refers to sexual offences involving children.</p>
                    <p class="font-bold pt-3 mb-1">Common Schedule 1 Offences</p>
                    <ul class="list-disc list-inside space-y-0.5 ml-4">
                        <li>Sexual interference (s. 151)</li>
                        <li>Invitation to sexual touching (s. 152)</li>
                        <li>Child pornography (s. 163.1)</li>
                        <li>Luring a child (s. 172.1)</li>
                        <li>Voyeurism involving a minor (s. 162)</li>
                    </ul>
                    <p class="mt-2 font-bold"><a href="https://laws-lois.justice.gc.ca/eng/acts/c-47/page-4.html" target="_blank" class="text-blue-700 hover:text-blue-900 underline">See the full list here.</a></p>
                </div>
            </div>

            <h3 class="text-lg font-semibold mt-8 pt-4 border-t border-gray-200 text-[#1a4d8c]">History of Convictions</h3>

            <div class="space-y-2">
                <label for="three-plus-two-year-imprisonment" class="block text-sm font-medium text-gray-700">Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?</label>
                <select id="three-plus-two-year-imprisonment" class="w-full">
                    <option value="" disabled selected>Select an option</option>
                    <option value="I'm not sure">I'm not sure</option>
                    <option value="Yes">Yes</option>
                    <option value="No">No</option>
                </select>
            </div>

            <button id="check-eligibility-btn" class="w-full bg-[#1a4d8c] hover:bg-[#133a6b] text-white font-bold py-3 rounded-xl transition duration-200 shadow-md mt-6" disabled>
                Check Eligibility
            </button>
        </section>

        <section id="result-section" class="mt-8">
            <h2 class="text-xl section-header hidden" id="result-header">Your Eligibility Status</h2>
            <div id="result-message" class="rounded-xl p-5 text-lg font-semibold">
                </div>
            <div id="missing-info-details" class="mt-4 hidden p-4 bg-yellow-50 border-l-4 border-yellow-500 rounded text-sm text-yellow-800">
                </div>
        </section>

    </div>

    <script>
        // --- CONSTANTS ---
        // Date constants normalized to midnight UTC to ensure consistency across comparisons
        const D1 = new Date(Date.UTC(2010, 5, 29)); // June 29, 2010 (Start of transitional rules)
        const D2 = new Date(Date.UTC(2012, 2, 12)); // March 12, 2012 (End of transitional rules)
        const D3 = new Date(Date.UTC(2012, 2, 13)); // March 13, 2012 (Start of current rules)
        const UNKNOWN_SENTINELS = ["I'm not sure", "", null];
        const TODAY = new Date();
        TODAY.setUTCHours(0, 0, 0, 0); // Normalize today to start of UTC day for comparison consistency

        // --- UTILITY FUNCTIONS ---

        /**
         * Parses a date string into a Date object, normalized to midnight UTC.
         * Fix: Use Date.UTC for robust parsing and avoid local timezone issues.
         * @param {string} dateStr - Date string in YYYY-MM-DD format.
         * @returns {Date | null} - Normalized Date object or null if invalid.
         */
        function parseDate(dateStr) {
            if (!dateStr || typeof dateStr !== 'string') return null;
            const parts = dateStr.split('-');
            if (parts.length !== 3) return null;
            
            const year = parseInt(parts[0], 10);
            const month = parseInt(parts[1], 10) - 1; // 0-indexed month
            const day = parseInt(parts[2], 10);

            // Using Date.UTC is crucial to avoid local timezone offset issues on different systems
            const d = new Date(Date.UTC(year, month, day));
            return isNaN(d.getTime()) ? null : d;
        }

        /**
         * Adds a non-integer number of years to a Date object using 365.25 days/year.
         * @param {Date} date - The starting date (must be a UTC normalized Date object).
         * @param {number} years - The number of years to add.
         * @returns {Date} - The calculated future date (UTC normalized).
         */
        function addYears(date, years) {
            // Cloning the date to avoid modifying the original
            const newDate = new Date(date.getTime());
            // Total milliseconds to add based on 365.25 days per year
            const MS_PER_YEAR = years * 365.25 * 24 * 60 * 60 * 1000;
            newDate.setTime(newDate.getTime() + MS_PER_YEAR);
            return newDate;
        }

        /**
         * Helper function to format the calculated UTC date back to a local date string for display.
         * @param {Date} date - The calculated UTC Date object.
         * @returns {string} - Formatted date string in local time.
         */
        function formatEligibleDate(date) {
            return date.toLocaleDateString('en-US', { year: 'numeric', month: 'long', day: 'numeric', timeZone: 'UTC' });
        }

        /**
         * Calculates eligibility based on conviction details following the Criminal Records Act (Canada) rules.
         */
        function calculateEligibility(
            convictionDateStr, prosecutionType, schedule1Offence,
            sentenceCompletionDateStr, 
            threePlusTwoYearImprisonment 
        ) {
            let essentialUnknowns = [];
            let convictionDate = parseDate(convictionDateStr);
            let sentenceCompletionDate = parseDate(sentenceCompletionDateStr);

            // Helper to check for unknown values
            const isUnknown = (val) => UNKNOWN_SENTINELS.includes(val) || (typeof val === 'string' && val.trim() === '');

            // --- Helper flags for ambiguity ---
            const isConvictionDateUnknown = isUnknown(convictionDateStr) || !convictionDate;
            const isCompletionDateUnknown = isUnknown(sentenceCompletionDateStr) || !sentenceCompletionDate;
            const isProsecutionTypeUnknown = isUnknown(prosecutionType);
            const isSchedule1Unknown = isUnknown(schedule1Offence);
            const isTwoYearImprisonmentUnknown = isUnknown(threePlusTwoYearImprisonment);

            // 1. Collect all essential missing info upfront for the 'unclear' status
            if (isConvictionDateUnknown) essentialUnknowns.push("Date of conviction");
            if (isCompletionDateUnknown) essentialUnknowns.push("Sentence completion date");
            if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
            if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");
            if (isTwoYearImprisonmentUnknown) essentialUnknowns.push("Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?");
            essentialUnknowns = Array.from(new Set(essentialUnknowns));

            // --- ABSOLUTE INELIGIBILITY CHECKS (Overrides all else) ---

            // Check A: Three or more convictions resulting in imprisonment of 2 years or more
            if (threePlusTwoYearImprisonment === "Yes") {
                 return {
                    status: "ineligible",
                    message: "You are not eligible for a record suspension. This is because you have three or more convictions that resulted in a sentence of imprisonment of two years or more each.",
                    eligibleDate: null,
                    missingAnswers: []
                };
            }

            // Check B: Schedule 1 Offence (Note: This is an exception case, but generally leads to ineligibility)
            if (schedule1Offence === "Yes") {
                const schedule1Message = `
                    Based on the information you provided, you appear to have been convicted of a **Schedule 1 offence**.
                    Generally, individuals convicted of a Schedule 1 offence are ineligible for a record suspension.
                    However, under Section 4(3) of the *Criminal Records Act*, exceptions may apply (e.g., if you were not in a position of trust or if the age difference with the victim was small).
                    For more information, consult a legal professional or the Parole Board of Canada website.
                `;
                // Return 'ineligible' status but with an 'exception' message
                return { status: "ineligible_exception", message: schedule1Message, eligibleDate: null, missingAnswers: [] };
            }

            // --- UNKNOWN/AMBIGUITY CHECK (If ineligibility factors are unknown) ---
            if (isSchedule1Unknown || isTwoYearImprisonmentUnknown) {
                // If any factor that could lead to absolute ineligibility is unknown, return 'unclear'
                 return { 
                    status: "unclear", 
                    message: "The required information to determine your eligibility is missing. Please review the missing details below. The answer to 'Schedule 1 offence' and 'History of Convictions' are critical.", 
                    eligibleDate: null, 
                    missingAnswers: essentialUnknowns 
                };
            }

            // --- KNOWN ELIGIBILITY TIMELINE CALCULATIONS ---
            let yearsToWait = null;

            if (convictionDate && convictionDate >= D3) {
                // Rules for conviction on or after March 13, 2012 (D3)
                yearsToWait = (prosecutionType === "Summary") ? 5 : 10;
            } else if (convictionDate && convictionDate < D3) {
                // Rules for conviction before March 13, 2012 (Pre-D3)
                if (convictionDate < D1) {
                    // Rules for conviction before June 29, 2010 (D1)
                    yearsToWait = (prosecutionType === "Summary") ? 3 : 5;
                } else if (convictionDate >= D1 && convictionDate < D3) {
                    // Rules for conviction between D1 and D3 (Transitional Rules)
                    // Handling SPIO ambiguity for Indictment (5 or 10 years)
                    if (prosecutionType === "Indictment" && !isProsecutionTypeUnknown) {
                        let missingInfo = ["Offence status (Serious Personal Injury Offence (SPIO))"];
                        if (isCompletionDateUnknown) missingInfo.push("Sentence completion date (to calculate the start of the waiting period)");

                        const date5yr = sentenceCompletionDate ? addYears(sentenceCompletionDate, 5) : null;
                        const date10yr = sentenceCompletionDate ? addYears(sentenceCompletionDate, 10) : null;

                        let ambiguityMessage = `
                            <p class="mt-2 text-base">
                                Based on your conviction date (${formatEligibleDate(convictionDate)}), your eligibility period is either **5 or 10 years** from your sentence completion date, depending on whether the offence was considered a **'serious personal injury offence' (SPIO)**.
                            </p>
                            ${sentenceCompletionDate ? `
                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If NOT an SPIO: Your eligibility date is **${formatEligibleDate(date5yr)}**.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If an SPIO: Your eligibility date is **${formatEligibleDate(date10yr)}**.</span>
                                </p>
                            </div>
                            ` : `<p class="mt-3 text-base">Please provide the sentence completion date to see the potential eligibility dates.</p>`}
                        `;
                        
                        return { 
                            status: "eligible_unclear", 
                            message: ambiguityMessage, 
                            eligibleDate: null, 
                            missingAnswers: Array.from(new Set(missingInfo)), 
                            timelineRange: "5–10 years" 
                        };
                    } 
                    // For Summary in D1-D3, the waiting period is 5 years.
                    yearsToWait = 5; 
                }
            } else {
                // Conviction Date is Unknown - If we reached here, all ineligibility factors are 'No', so likely eligible.
                // Return 'eligible_unclear' with the broadest range.
                return {
                    status: "eligible_unclear",
                    message: "You appear to be eligible for a record suspension. However, your eligibility date depends on the missing conviction and sentence completion dates.",
                    eligibleDate: null,
                    missingAnswers: essentialUnknowns,
                    timelineRange: "3–10 years" // Broadest possible range
                };
            }

            // --- FINAL ELIGIBILITY CALCULATION (If all known and no ineligibility/ambiguity) ---

            if (isCompletionDateUnknown || !sentenceCompletionDate) {
                // If we have yearsToWait but no start date, return 'eligible_unclear'
                return {
                    status: "eligible_unclear",
                    message: `You appear to be eligible for a record suspension with a waiting period of **${yearsToWait} years** from your sentence completion date. Please provide the sentence completion date to calculate your eligibility date.`,
                    eligibleDate: null,
                    missingAnswers: ["Sentence completion date"],
                    timelineRange: `${yearsToWait} years`
                };
            }

            // Calculate final eligibility date
            const finalEligibleDate = addYears(sentenceCompletionDate, yearsToWait);

            if (finalEligibleDate > TODAY) {
                // Not yet eligible
                return {
                    status: "not_yet_eligible",
                    message: `You will be eligible for a record suspension on **${formatEligibleDate(finalEligibleDate)}**, which is **${yearsToWait} years** after your sentence completion date.`,
                    eligibleDate: finalEligibleDate,
                    missingAnswers: []
                };
            } else {
                // Eligible now
                return {
                    status: "eligible",
                    message: "You are currently **eligible** to apply for a record suspension.",
                    eligibleDate: finalEligibleDate,
                    missingAnswers: []
                };
            }

        }


        // --- EVENT HANDLERS ---

        document.addEventListener('DOMContentLoaded', () => {
            const disclaimerCheckbox = document.getElementById('disclaimer-accepted');
            const inputForm = document.getElementById('input-form');
            const checkBtn = document.getElementById('check-eligibility-btn');
            const resultSection = document.getElementById('result-section');
            const resultHeader = document.getElementById('result-header');
            const resultMessage = document.getElementById('result-message');
            const missingInfoDetails = document.getElementById('missing-info-details');
            const schedule1InfoToggle = document.getElementById('schedule1-info-toggle');
            const schedule1Info = document.getElementById('schedule1-info');

            // Get all input elements for change listener
            const inputs = document.querySelectorAll('#input-form input, #input-form select');
            const convictionDateInput = document.getElementById('conviction-date');
            const dontKnowConvDateCheckbox = document.getElementById('dont-know-conv-date');
            const sentenceCompletionDateInput = document.getElementById('sentence-completion-date');
            const dontKnowSentCompDateCheckbox = document.getElementById('dont-know-sent-comp-date');


            // Toggles visibility of the main form section and the eligibility button
            disclaimerCheckbox.addEventListener('change', () => {
                inputForm.style.display = disclaimerCheckbox.checked ? 'block' : 'none';
                checkBtn.disabled = !disclaimerCheckbox.checked;
                resultSection.style.display = disclaimerCheckbox.checked ? 'block' : 'none';
                if (!disclaimerCheckbox.checked) {
                    // Clear results when disclaimer is unchecked
                    resultHeader.classList.add('hidden');
                    resultMessage.innerHTML = '';
                    resultMessage.className = 'rounded-xl p-5 text-lg font-semibold';
                    missingInfoDetails.classList.add('hidden');
                }
            });

            // Toggle logic for "I'm not sure" checkboxes on date inputs
            function setupDateToggle(dateInput, checkbox) {
                checkbox.addEventListener('change', () => {
                    dateInput.disabled = checkbox.checked;
                    dateInput.value = ''; // Clear value when checkbox is checked
                    // Note: Date icon hide/show is handled by the :disabled CSS selector
                    checkEligibility(); // Re-run calculation on change
                });
                dateInput.addEventListener('change', () => {
                    checkbox.checked = false; // Uncheck "I'm not sure" if user enters a date
                    dateInput.disabled = false;
                    checkEligibility(); // Re-run calculation on date input change
                });
            }

            setupDateToggle(convictionDateInput, dontKnowConvDateCheckbox);
            setupDateToggle(sentenceCompletionDateInput, dontKnowSentCompDateCheckbox);

            // Toggle for Schedule 1 information
            schedule1InfoToggle.addEventListener('click', () => {
                schedule1Info.classList.toggle('hidden');
            });

            // Set up all other inputs to trigger calculation
            inputs.forEach(input => {
                // Exclude date inputs/checkboxes that are handled above, and the disclaimer checkbox
                if (input.id !== 'conviction-date' && input.id !== 'sentence-completion-date' && input.id !== 'dont-know-conv-date' && input.id !== 'dont-know-sent-comp-date' && input.id !== 'disclaimer-accepted') {
                    input.addEventListener('change', checkEligibility);
                }
            });

            // Event listener for the main button click
            checkBtn.addEventListener('click', checkEligibility);

            /**
             * Handles the eligibility check process, reading all inputs and displaying the result.
             */
            function checkEligibility() {
                // Only run if the disclaimer is accepted
                if (!disclaimerCheckbox.checked) return; 

                // --- GATHER INPUTS ---
                // The parseDate function handles the "I'm not sure" state for calculation logic
                const convictionDateStr = dontKnowConvDateCheckbox.checked ? "I'm not sure" : convictionDateInput.value;
                const sentenceCompletionDateStr = dontKnowSentCompDateCheckbox.checked ? "I'm not sure" : sentenceCompletionDateInput.value;
                const prosecutionType = document.getElementById('prosecution-type').value;
                const schedule1Offence = document.getElementById('schedule1-offence').value;
                const threePlusTwoYearImprisonment = document.getElementById('three-plus-two-year-imprisonment').value;

                // --- RUN CALCULATION ---
                const result = calculateEligibility(
                    convictionDateStr, prosecutionType, schedule1Offence,
                    sentenceCompletionDateStr,
                    threePlusTwoYearImprisonment
                );

                // --- DISPLAY RESULTS ---
                displayResult(result);
            }

            /**
             * Displays the result based on the calculation object.
             * @param {Object} result - The result object from calculateEligibility.
             */
            function displayResult(result) {
                resultHeader.classList.remove('hidden');
                resultMessage.innerHTML = result.message;
                missingInfoDetails.classList.add('hidden');
                resultMessage.classList.remove('bg-green-100', 'bg-red-100', 'bg-yellow-100', 'text-green-800', 'text-red-800', 'text-yellow-800');

                let newClasses;
                let missingListHtml = '';

                switch (result.status) {
                    case "eligible":
                        newClasses = 'bg-green-100 text-green-800';
                        break;
                    case "not_yet_eligible":
                        newClasses = 'bg-yellow-100 text-yellow-800';
                        break;
                    case "ineligible":
                    case "ineligible_exception": 
                        newClasses = 'bg-red-100 text-red-800';
                        break;
                    case "unclear":
                    case "eligible_unclear":
                        newClasses = 'bg-yellow-100 text-yellow-800';
                        if (result.missingAnswers && result.missingAnswers.length > 0) {
                            missingInfoDetails.classList.remove('hidden');
                            missingListHtml = '<strong>Missing Information:</strong><ul class="list-disc list-inside mt-1 space-y-0.5">';
                            result.missingAnswers.forEach(answer => {
                                missingListHtml += `<li>${answer}</li>`;
                            });
                            
                            // Add timeline range hint if provided
                            if (result.timelineRange) {
                                missingListHtml += `<li>* Based on current answers, your waiting period is likely between **${result.timelineRange}**.</li>`;
                            }
                            missingListHtml += '</ul>';
                            missingInfoDetails.innerHTML = missingListHtml;
                        }
                        break;
                }
                resultMessage.classList.add(newClasses);
            }
        });
    </script>
</body>
</html>
