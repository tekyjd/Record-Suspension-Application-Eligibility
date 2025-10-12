<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Record Suspension Eligibility</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom styles to match the desired theme */
        body {
            font-family: 'Inter', sans-serif;
            background: #f0f2f6; /* Light gray/blue background */
        }
        .container-card {
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            max-width: 90%;
            margin: 2rem auto;
            background-color: #ffffff;
        }
        .section-header {
            color: #1a4d8c; /* Dark blue */
            border-bottom: 2px solid #e6f2ff;
            padding-bottom: 0.5rem;
            margin-bottom: 1.5rem;
            font-weight: 600;
        }
        
        /* ---------------------------------------------------------------------- */
        /* CUSTOM DATE INPUT STYLING TO MOVE ICON LEFT (SIMULATED) */
        /* ---------------------------------------------------------------------- */
        
        /* 1. Hide the browser's native calendar icon/picker indicator */
        input[type="date"]::-webkit-calendar-picker-indicator {
            opacity: 0; /* Make it invisible but still clickable */
            width: 100%; /* Make the whole field the target */
            position: absolute; /* Position it over the entire field */
            cursor: pointer;
        }
        /* Fallback for other browsers (less effective but attempts to hide) */
        input[type="date"]::-moz-calendar-picker-indicator {
            display: none;
        }

        /* 2. Adjust input padding to make room for the custom icon on the left */
        input[type="date"] {
            border: 1px solid #d1d5db;
            padding: 0.6rem 1rem 0.6rem 2.5rem; /* Increased left padding (2.5rem) */
            border-radius: 0.5rem;
            /* Note: Width is now controlled by the parent div (w-44) */
            width: 100%; 
            transition: border-color 0.15s ease-in-out, box-shadow: 0.15s ease-in-out;
            background-color: #f9fafb;
            cursor: pointer; 
            position: relative; 
        }
        
        /* 3. Ensure other inputs/selects are styled correctly */
        select {
            border: 1px solid #d1d5db;
            padding: 0.6rem 1rem;
            border-radius: 0.5rem;
            width: 100%;
            transition: border-color 0.15s ease-in-out, box-shadow: 0.15s ease-in-out;
            background-color: #f9fafb;
            cursor: pointer;
        }
        
        input[type="date"]:focus, select:focus {
            border-color: #4f46e5; 
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.3);
            outline: none;
        }
        /* Style for disabled date inputs */
        input[type="date"]:disabled {
            background-color: #e5e7eb; /* Lighter background for disabled field */
            color: #9ca3af;
            cursor: not-allowed;
            padding-left: 1rem; /* Remove extra padding when disabled/icon is useless */
        }
        
        /* Ensure the label is also clickable */
        .clickable-label {
            cursor: pointer;
        }
        /* Adjust layout for date row */
        .date-input-group {
            display: flex;
            align-items: center;
        }
    </style>
</head>
<body>

    <div id="app" class="container-card p-6 md:p-10 rounded-xl">
        <header class="text-center mb-6 flex items-center justify-center space-x-4">
            
            <h1 class="text-2xl font-bold text-gray-800 my-4">Pardon Eligibility Checker</h1>
            
            <!-- TMU Law Logo: Increased height to h-16 -->
            <img src="https://www.torontomu.ca/content/dam/law/images/TMU-Law-rgb.svg" 
                 alt="TMU Law Logo" 
                 class="h-16 w-auto" 
                 style="max-width: 300px;">
            
        </header>

        <!-- Disclaimer Section -->
        <section class="mb-8 p-4 bg-blue-50 border-l-4 border-blue-500 rounded-lg">
            <h2 class="text-xl section-header text-blue-700">Disclaimer</h2>
            <p class="text-sm text-blue-600 mb-4">Eligibility results are for informational purposes only. They are provided in good faith, based solely on the information you enter. This tool does not constitute legal advice, and using it does not guarantee that a record suspension will be granted or denied by the Parole Board of Canada.</p>
            <label class="flex items-center space-x-2 cursor-pointer">
                <input type="checkbox" id="disclaimer-accepted" class="form-checkbox h-5 w-5 text-blue-500 rounded-md">
                <span class="text-sm text-gray-700 font-medium">I accept the disclaimer and wish to proceed</span>
            </label>
        </section>

        <!-- Input Form Section -->
        <section id="input-form" class="space-y-6" style="display: none;">
            <h2 class="text-xl section-header">Conviction Details</h2>

            <!-- Conviction Date -->
            <div class="space-y-2">
                <label for="conviction-date" class="block text-sm font-medium text-gray-700 clickable-label">Date of conviction</label>
                <div class="date-input-group space-x-4">
                    <!-- Date Input Container: Changed flex-grow to w-44 to shorten the box -->
                    <div class="relative w-44">
                        <input type="date" id="conviction-date" class="w-full">
                        <!-- Custom Icon (positioned on the left) -->
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

            <!-- Sentence Completion Date -->
            <div class="space-y-2">
                <label for="sentence-completion-date" class="block text-sm font-medium text-gray-700 clickable-label">Sentence completion date</label>
                <div class="date-input-group space-x-4">
                    <!-- Date Input Container: Changed flex-grow to w-44 to shorten the box -->
                    <div class="relative w-44">
                        <input type="date" id="sentence-completion-date" class="w-full">
                        <!-- Custom Icon (positioned on the left) -->
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


            <!-- Prosecution Type -->
            <div class="space-y-2">
                <label for="prosecution-type" class="block text-sm font-medium text-gray-700">Prosecution type</label>
                <select id="prosecution-type" class="w-full">
                    <option value="" disabled selected>Select an option</option>
                    <option value="I'm not sure">I'm not sure</option>
                    <option value="Indictment">Indictment</option>
                    <option value="Summary">Summary</option>
                </select>
            </div>

            <!-- Schedule 1 Offence (Updated Info Section) -->
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
                <!-- UPDATED CONTENT FOR SCHEDULE 1 INFO -->
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

            <!-- History of Convictions Section -->
            <h3 class="text-lg font-semibold mt-8 pt-4 border-t border-gray-200 text-[#1a4d8c]">History of Convictions</h3>

            <!-- Imprisonment Question -->
            <div class="space-y-2">
                <label for="three-plus-two-year-imprisonment" class="block text-sm font-medium text-gray-700">Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?</label>
                <select id="three-plus-two-year-imprisonment" class="w-full">
                    <option value="" disabled selected>Select an option</option>
                    <option value="I'm not sure">I'm not sure</option>
                    <option value="Yes">Yes</option>
                    <option value="No">No</option>
                </select>
            </div>

            <button id="check-eligibility-btn" class="w-full bg-[#1a4d8c] hover:bg-[#133a6b] text-white font-bold py-3 rounded-xl transition duration-200 shadow-md mt-6">
                Check Eligibility
            </button>
        </section>

        <!-- Result Section -->
        <section id="result-section" class="mt-8">
            <h2 class="text-xl section-header hidden" id="result-header">Your Eligibility Status</h2>
            <div id="result-message" class="rounded-xl p-5 text-lg font-semibold">
                <!-- Results will be displayed here -->
            </div>
            <div id="missing-info-details" class="mt-4 hidden p-4 bg-yellow-50 border-l-4 border-yellow-500 rounded text-sm text-yellow-800">
                <!-- Missing answers list will be displayed here -->
            </div>
        </section>

    </div>

    <script>
        // Date constants normalized to midnight UTC to ensure consistency across comparisons
        const D1 = new Date(Date.UTC(2010, 5, 29)); // June 29, 2010 (Start of transitional rules)
        const D2 = new Date(Date.UTC(2012, 2, 12)); // March 12, 2012 (End of transitional rules)
        const D3 = new Date(Date.UTC(2012, 2, 13)); // March 13, 2012 (Start of current rules)
        const TODAY = new Date();
        TODAY.setHours(0, 0, 0, 0); // Normalize today to start of the local day

        /**
         * Parses a date string into a Date object, normalized to midnight UTC.
         * @param {string} dateStr - Date string in YYYY-MM-DD format.
         * @returns {Date | null} - Normalized Date object or null if invalid.
         */
        function parseDate(dateStr) {
            if (!dateStr) return null;
            const parts = dateStr.split('-');
            if (parts.length !== 3) return null;
            
            const year = parseInt(parts[0], 10);
            const month = parseInt(parts[1], 10) - 1; // 0-indexed month
            const day = parseInt(parts[2], 10);

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
        
        // Updated to use the consistent phrase "I'm not sure"
        const UNKNOWN_SENTINELS = ["I'm not sure", ""]; 

        /**
         * Calculates eligibility based on conviction details following the Criminal Records Act (Canada) rules.
         */
        function calculateEligibility(
            convictionDateStr, prosecutionType, schedule1Offence,
            sentenceCompletionDateStr, 
            threePlusTwoYearImprisonment 
        ) {
            let essentialUnknowns = [];
            let eligibleDate = null;
            let convictionDate = parseDate(convictionDateStr);
            let sentenceCompletionDate = parseDate(sentenceCompletionDateStr);

            // Helper to check for unknown values
            const isUnknown = (val) => UNKNOWN_SENTINELS.includes(val);

            // --- Helper flags for ambiguity ---
            const isConvictionDateUnknown = isUnknown(convictionDateStr) || !convictionDate;
            const isCompletionDateUnknown = isUnknown(sentenceCompletionDateStr) || !sentenceCompletionDate;
            const isProsecutionTypeUnknown = isUnknown(prosecutionType);
            const isSchedule1Unknown = isUnknown(schedule1Offence);
            const isTwoYearImprisonmentUnknown = isUnknown(threePlusTwoYearImprisonment);

            
            // 1. Prioritized Check for Convictions on or after March 13, 2012 (D3)
            if (convictionDate && convictionDate >= D3) {
                
                // A. Schedule 1 Check (Known 'Yes')
                if (schedule1Offence === "Yes") {
                    const schedule1Message = `
                        Based on the information you provided, you appear to have been convicted of a Schedule 1 offence.
                        Generally, individuals convicted of a Schedule 1 offence are ineligible for a record suspension.
                        However, under Section 4(3) of the *Criminal Records Act*, exceptions may apply (e.g., if you were not in a position of trust or if the age difference with the victim was small).
                        For more information, consult a legal professional or the Parole Board of Canada website.
                    `;
                    return { status: "schedule1_exception", message: schedule1Message, eligibleDate: null, missingAnswers: [] };
                }

                // B. Multiple Serious Conviction Check (Known 'Yes') -> INELIGIBLE
                if (threePlusTwoYearImprisonment === "Yes") {
                    return {
                        status: "ineligible",
                        message: "You are not eligible for a record suspension. This is because you have three or more convictions that resulted in a sentence of imprisonment of two years or more each.",
                        eligibleDate: null,
                        missingAnswers: []
                    };
                }
                
                // C. AMBIGUITY CHECK (Post-D3): If any INELIGIBILITY-RELATED factor is UNKNOWN.
                const missingIneligibilityFactor = isSchedule1Unknown || isTwoYearImprisonmentUnknown;

                if (missingIneligibilityFactor) {
                    if (isConvictionDateUnknown) essentialUnknowns.push("Date of conviction");
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence completion date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");

                    if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");
                    if (isTwoYearImprisonmentUnknown) essentialUnknowns.push("Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?");
                    
                    essentialUnknowns = Array.from(new Set(essentialUnknowns));

                    return { 
                        status: "unclear",
                        // Using the requested general wording:
                        message: "The required information to determine your eligibility is missing. Please review the missing details below.", 
                        eligibleDate: null, 
                        missingAnswers: essentialUnknowns 
                    };
                }
                
                // D. Potentially Eligible (Date Unclear) Check (Only date/prosecution type are missing)
                if (isConvictionDateUnknown || isCompletionDateUnknown || isProsecutionTypeUnknown) {
                    if (isConvictionDateUnknown) essentialUnknowns.push("Date of conviction");
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence completion date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    
                    essentialUnknowns = Array.from(new Set(essentialUnknowns));
                    return {
                        status: "eligible_unclear",
                        message: "You appear to be eligible for a record suspension based on the conviction type and history. However, your exact eligibility date depends on the missing date and prosecution type details.",
                        eligibleDate: null,
                        missingAnswers: essentialUnknowns,
                        timelineRange: "5–10 years" // Applicable range for Post-D3 rules (5 years for Summary, 10 years for Indictable)
                    };
                }
                
                // If we reach here, all info is known, continue to Step 4
            } 
            
            // 2. Prioritized Check for Convictions before March 13, 2012 (Pre-D3)
            else if (convictionDate && convictionDate < D3) { 
                
                // --- SPECIAL AMBIGUITY CHECK (2010-2012 Transitional Period for Indictments/Unknown) ---
                
                // Check if prosecution type is Indictment OR Unknown (I'm not sure or empty string)
                const isAmbiguousProsecutionType = prosecutionType === "Indictment" || isProsecutionTypeUnknown;

                // Rule: Conviction Date between D1 and D2 AND (Indictment OR Unknown) AND Not Schedule 1
                if (convictionDate >= D1 && convictionDate <= D2 && isAmbiguousProsecutionType && schedule1Offence === "No") {
                    
                    let missingInfo = ["Offence status (Serious Personal Injury Offence (SPIO))"];
                    let ambiguityMessage = '';
                    
                    if (isCompletionDateUnknown) {
                         // Case 1: Completion Date is UNKNOWN
                         missingInfo.push("Sentence completion date (to calculate the start of the waiting period)");
                         
                         ambiguityMessage = `
                            <p class="mt-2 text-base">
                                The eligibility date depends on whether the conviction was for a **'serious personal injury offence'** (within the meaning of 752 of the *Criminal Code*), for which you were sentenced to a prison term of 2 years or more.
                            </p>

                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If you were convicted of a serious personal injury offence: Your waiting period is **10 years**.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If you were NOT of a serious personal injury offence: Your waiting period is **5 years**.</span>
                                </p>
                            </div>
                        `;

                    } else {
                        // Case 2: Completion Date is KNOWN
                        const date5yr = addYears(sentenceCompletionDate, 5);
                        const date10yr = addYears(sentenceCompletionDate, 10);

                        const date5yrStr = formatEligibleDate(date5yr);
                        const date10yrStr = formatEligibleDate(date10yr);

                        // Use requested exact wording and formatting
                        ambiguityMessage = `
                            <p class="mt-2 text-base">
                                The eligibility date depends on whether the conviction was for a **'serious personal injury offence'** (within the meaning of 752 of the *Criminal Code*), for which you were sentenced to a prison term of 2 years or more.
                            </p>

                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If you were convicted of a serious personal injury offence: Your eligibility date is **${date10yrStr}**.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If you were NOT of a serious personal injury offence: Your eligibility date is **${date5yrStr}**.</span>
                                </p>
                            </div>
                        `;
                    }
                    
                    return {
                        status: "eligible_unclear", 
                        message: ambiguityMessage,
                        eligibleDate: null,
                        missingAnswers: missingInfo,
                        timelineRange: "5–10 years" // Applicable range for Transitional SPIO ambiguity (5 or 10 years)
                    };
                }

                // Collect other unknowns for Pre-D3 
                essentialUnknowns = [];
                let range = "3–10 years"; // Default to broadest range

                // Case: Conviction Date is before D1 (Pre-June 29, 2010)
                if (convictionDate < D1) {
                    
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence completion date");

                    if (isProsecutionTypeUnknown) {
                         essentialUnknowns.push("Prosecution type");
                         range = "3–5 years"; // Unknown type before D1 is max 5 years
                    } else if (prosecutionType === "Indictment") {
                         range = "5 years";
                    } else if (prosecutionType === "Summary") {
                         range = "3 years";
                    }
                } 
                
                // Case: Conviction Date is between D1 and D3 (June 29, 2010 – March 12, 2012)
                else if (convictionDate >= D1 && convictionDate < D3) {
                    
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence completion date");
                    
                    // --- APPLY USER'S REQUESTED RANGES FOR UNKNOWNS IN D1-D3 PERIOD ---
                    
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");

                    // NEW SPECIFIC RULE: Summary + Schedule 1 = Yes (Fixed 5 years wait)
                    if (prosecutionType === "Summary" && schedule1Offence === "Yes" && !isProsecutionTypeUnknown && !isSchedule1Unknown) {
                        range = "5 years";
                    }
                    // Rule 1: Indictable -> 5-10 years (Non-SPIO vs SPIO ambiguity)
                    else if (prosecutionType === "Indictment" && !isProsecutionTypeUnknown) {
                        range = "5–10 years";
                    } 
                    // Original Rule 2: Summary (Non-Sch1 or Sch1 Unknown) -> 3-5 years
                    else if (prosecutionType === "Summary" && !isProsecutionTypeUnknown) {
                        // This case is for Summary where Sch1 is 'No' or 'I'm not sure'.
                        if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");
                        range = "3–5 years";
                    }
                    // Original Rule 3: Unknown Prosecution & (Schedule 1 = No or Unknown) -> 3-10 years
                    else if (isProsecutionTypeUnknown && (schedule1Offence === "No" || isSchedule1Unknown)) {
                        if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");
                        range = "3–10 years";
                    }
                    // Original Rule 4: Unknown Prosecution & (Schedule 1 = Yes) -> 5-10 years
                    else if (isProsecutionTypeUnknown && schedule1Offence === "Yes") {
                        range = "5–10 years";
                    }
                }
                
                // If there are unknowns, return the 'eligible_unclear' status with the determined range
                if (essentialUnknowns.length > 0) {
                     return { 
                        status: "eligible_unclear", 
                        message: "You may be eligible for a record suspension. However, your eligibility date will depend on the missing information.", 
                        eligibleDate: null, 
                        missingAnswers: Array.from(new Set(essentialUnknowns)),
                        timelineRange: range 
                    };
                }
                
                // If we reach here, all info is known and we continue to Step 4
            } 
            
            // 3. Fallback if Conviction Date is UNKNOWN (Conviction Date is 'I'm not sure' or empty)
            else if (isConvictionDateUnknown) {

                // A. Check for known ineligibility (Sch 1 is Yes OR 3+ Convictions is Yes)
                if (schedule1Offence === "Yes" && !isSchedule1Unknown) {
                    const schedule1Message = `
                        Based on the information you provided, you appear to have been convicted of a Schedule 1 offence.
                        Generally, individuals convicted of a Schedule 1 offence are ineligible for a record suspension.
                        However, under Section 4(3) of the *Criminal Records Act*, exceptions may apply (e.g., if you were not in a position of trust or if the age difference with the victim was small).
                        For more information, consult a legal professional or the Parole Board of Canada website.
                    `;
                    return { status: "schedule1_exception", message: schedule1Message, eligibleDate: null, missingAnswers: [] };
                }

                if (threePlusTwoYearImprisonment === "Yes" && !isTwoYearImprisonmentUnknown) {
                    return {
                        status: "ineligible",
                        message: "You are not eligible for a record suspension. This is because you have three or more convictions that resulted in a sentence of imprisonment of two years or more each.",
                        eligibleDate: null,
                        missingAnswers: []
                    };
                }

                // B. Check if we are missing information about absolute ineligibility 
                essentialUnknowns = [];
                if (isConvictionDateUnknown) essentialUnknowns.push("Date of conviction");
                if (isCompletionDateUnknown) essentialUnknowns.push("Sentence completion date");
                if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                
                if (isSchedule1Unknown || isTwoYearImprisonmentUnknown) {
                    // Fallback to "unclear" if we can't rule out ineligibility
                    if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");
                    if (isTwoYearImprisonmentUnknown) essentialUnknowns.push("Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?");

                    return {
                        status: "unclear",
                        // Using the requested general wording:
                        message: "The required information to determine your eligibility is missing. Please review the missing details below.",
                        eligibleDate: null,
                        missingAnswers: Array.from(new Set(essentialUnknowns))
                    };
                }

                // C. If we reach here: Conviction Date is Unknown, Sch 1='No', and 3+ Conv='No'. Likely Eligible but Timeline Unknown.
                if (schedule1Offence === "No" && threePlusTwoYearImprisonment === "No") {
                    
                    let range = "3–10 years"; // Default to broadest range (Conviction Date is unknown, so 3-10 years is possible)
                    
                    // Collect remaining unknowns
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence completion date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    // Conviction Date is the main reason we are here, so add it
                    essentialUnknowns.push("Date of conviction");
                    
                    // Customize range based on known non-date factors:
                    if (prosecutionType === "Indictment" && !isProsecutionTypeUnknown) {
                        // If Indictment is KNOWN, the minimum waiting period is 5 years 
                        // (Pre-D1 Indictment is 5, Post-D3 Indictment is 10)
                        range = "5–10 years";
                    } else if (prosecutionType === "Summary" && !isProsecutionTypeUnknown) {
                        // If Summary is KNOWN, the maximum waiting period is 5 years
                        range = "3–5 years";
                    }
                    // Since Sch1 is 'No', we don't need to check the Sch1 condition here.

                    return {
                        status: "eligible_unclear",
                        message: "You appear to be eligible based on the conviction type and history, but your conviction date is needed to determine the applicable waiting period (3, 5, or 10 years).",
                        eligibleDate: null,
                        missingAnswers: Array.from(new Set(essentialUnknowns)),
                        timelineRange: range
                    };
                }
                
                // Fallback (should be unreachable)
                return { status: "unclear", message: "Eligibility is fully unclear. Calculation error.", eligibleDate: null, missingAnswers: [] };
            }


            // 4. Calculate Wait Period (All required info is known and no ambiguity was found)
            let waitPeriodYears = 0;

            if (convictionDate < D1) {
                // Before June 29, 2010 (Old Rules) - Fixed 3 or 5 years.
                waitPeriodYears = (prosecutionType === "Indictment") ? 5 : 3;
            } else if (convictionDate >= D1 && convictionDate <= D2) {
                // Between June 29, 2010 and March 12, 2012 (Transitional Rules)
                
                if (schedule1Offence === "Yes") {
                    // Indictment/Summary with Schedule 1 conviction (10 years if Indictment, 5 years if Summary)
                    waitPeriodYears = (prosecutionType === "Indictment") ? 10 : 5; 
                } else if (prosecutionType === "Summary") { 
                    // Summary and Not Schedule 1 (3 years - using old rule)
                    waitPeriodYears = 3;
                } else {
                    // Indictment and Not Schedule 1 (SPIO check was avoided in the ambiguity section, so we assume 5 years as the non-SPIO Indictable time)
                    waitPeriodYears = 5;
                }
            } else if (convictionDate >= D3) {
                // On or after March 13, 2012 (Current Rules)
                waitPeriodYears = (prosecutionType === "Indictment") ? 10 : 5;
            } else {
                // Fallback for unhandled date
                return { status: "unclear", message: "Eligibility calculation failed: Unhandled date range.", eligibleDate: null, missingAnswers: [] };
            }

            // 5. Final Status Determination
            eligibleDate = addYears(sentenceCompletionDate, waitPeriodYears);

            if (eligibleDate <= TODAY) {
                return {
                    status: "eligible_now",
                    message: `You are eligible to apply for a record suspension now. The waiting period was determined to be **${waitPeriodYears} years**.`,
                    eligibleDate: eligibleDate,
                    missingAnswers: []
                };
            } else {
                const dateString = formatEligibleDate(eligibleDate);
                return {
                    status: "eligible_future",
                    message: `You will be eligible on ${dateString}. The required waiting period is **${waitPeriodYears} years** from your sentence completion date.`,
                    eligibleDate: eligibleDate,
                    missingAnswers: []
                };
            }
        }

        // --- UI Logic and Event Handlers ---

        const elements = {
            disclaimerCheckbox: document.getElementById('disclaimer-accepted'),
            inputForm: document.getElementById('input-form'),
            checkEligibilityBtn: document.getElementById('check-eligibility-btn'),
            resultSection: document.getElementById('result-section'),
            resultHeader: document.getElementById('result-header'),
            resultMessage: document.getElementById('result-message'),
            missingInfoDetails: document.getElementById('missing-info-details'),
            // Inputs
            convictionDate: document.getElementById('conviction-date'),
            dontKnowConvDate: document.getElementById('dont-know-conv-date'),
            sentenceCompletionDate: document.getElementById('sentence-completion-date'),
            dontKnowSentCompDate: document.getElementById('dont-know-sent-comp-date'),
            prosecutionType: document.getElementById('prosecution-type'),
            schedule1Offence: document.getElementById('schedule1-offence'),
            threePlusTwoYearImprisonment: document.getElementById('three-plus-two-year-imprisonment'),
            schedule1InfoToggle: document.getElementById('schedule1-info-toggle'),
            schedule1Info: document.getElementById('schedule1-info'),
        };

        // Conditional display for "I'm not sure" date handling
        function updateConditionalInputs() {
            // Conviction Date
            if (elements.dontKnowConvDate.checked) {
                elements.convictionDate.disabled = true;
                elements.convictionDate.value = ''; // Clear value when disabled for user-friendly
            } else {
                elements.convictionDate.disabled = false;
            }

            // Sentence Completion Date
            if (elements.dontKnowSentCompDate.checked) {
                elements.sentenceCompletionDate.disabled = true;
                elements.sentenceCompletionDate.value = ''; // Clear value when disabled for user-friendly
            } else {
                elements.sentenceCompletionDate.disabled = false;
            }
        }

        // Event listener setup
        elements.dontKnowConvDate.addEventListener('change', updateConditionalInputs);
        elements.dontKnowSentCompDate.addEventListener('change', updateConditionalInputs);
        window.addEventListener('load', updateConditionalInputs); 

        // Toggle Schedule 1 Info
        elements.schedule1InfoToggle.addEventListener('click', () => {
            elements.schedule1Info.classList.toggle('hidden');
            elements.schedule1InfoToggle.innerHTML = elements.schedule1Info.classList.contains('hidden') ? '<u>What are Schedule 1 Offences?</u>' : '[x] Close';
        });
        // Initial setup for the toggle text
        elements.schedule1InfoToggle.innerHTML = '<u>What are Schedule 1 Offences?</u>';


        // Event listener for disclaimer
        elements.disclaimerCheckbox.addEventListener('change', () => {
            elements.inputForm.style.display = elements.disclaimerCheckbox.checked ? 'block' : 'none';
            // Clear results on uncheck
            elements.resultHeader.classList.add('hidden');
            elements.resultMessage.innerHTML = '';
            elements.missingInfoDetails.classList.add('hidden');
        });

        // Event listener for eligibility check
        elements.checkEligibilityBtn.addEventListener('click', () => {
            if (!elements.disclaimerCheckbox.checked) {
                // Using a custom message box instead of alert()
                displayResult({ status: 'unclear', message: 'Please accept the disclaimer to check eligibility.', eligibleDate: null, missingAnswers: [] });
                return;
            }

            // Get date strings, prioritizing 'I'm not sure' checkbox over the date picker value
            const convictionDateInputStr = elements.dontKnowConvDate.checked ? "I'm not sure" : elements.convictionDate.value;
            const sentenceCompletionDateInputStr = elements.dontKnowSentCompDate.checked ? "I'm not sure" : elements.sentenceCompletionDate.value;
            
            // Get multiconviction value
            const threePlusTwoYearImprisonmentVal = elements.threePlusTwoYearImprisonment.value;
            
            // Call calculateEligibility with the updated argument list
            const result = calculateEligibility(
                convictionDateInputStr,
                elements.prosecutionType.value,
                elements.schedule1Offence.value,
                sentenceCompletionDateInputStr,
                threePlusTwoYearImprisonmentVal
            );

            displayResult(result);
        });

        /**
         * Renders the result object to the UI.
         */
        function displayResult(result) {
            elements.resultHeader.classList.remove('hidden');
            elements.missingInfoDetails.classList.add('hidden');
            elements.resultMessage.className = 'rounded-xl p-5 text-lg font-semibold mt-4 shadow-lg transition-all duration-300';
            let htmlContent = '';
            let styleClasses = '';
            let missingListHTML = '';
            
            // HTML for courthouse contact info (as requested)
            const courthouseContactHtml = `
                <p class="mt-4 font-bold">You can obtain this information from the courthouse where you were convicted:</p>
                <p class="mt-1 text-sm">
                    <a href="https://www.ontario.ca/locations/courts" target="_blank" class="text-blue-600 hover:underline">Ontario Courthouse Contact</a>
                </p>
            `;


            switch (result.status) {
                case 'eligible_now':
                    styleClasses = 'bg-green-100 border-l-8 border-green-600 text-green-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-green-600">🎉</span><h3 class="font-bold text-xl">Eligible Now!</h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    break;

                case 'eligible_future':
                    styleClasses = 'bg-blue-100 border-l-8 border-blue-600 text-blue-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-blue-600">&#9202;</span><h3 class="font-bold text-xl">Eligible in the Future</h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    break;

                case 'ineligible':
                    styleClasses = 'bg-red-100 border-l-8 border-red-600 text-red-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-red-600">&#10060;</span><h3 class="font-bold text-xl">Ineligible</h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    break;

                case 'schedule1_exception':
                    styleClasses = 'bg-yellow-100 border-l-8 border-amber-600 text-amber-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-amber-600">⚠️</span><h3 class="font-bold text-xl">Schedule 1 Offence — Possible Exception</h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    break;

                case 'eligible_unclear':
                    styleClasses = 'bg-indigo-100 border-l-8 border-indigo-600 text-indigo-800'; 
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-indigo-600">&#63;</span><h3 class="font-bold text-xl">Likely Eligible (Timeline Ambiguous)</h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    
                    if (result.timelineRange) {
                        htmlContent += `<p class="mt-3 text-sm font-bold bg-indigo-200 p-2 rounded-lg inline-block">Potential eligibility timeline: ${result.timelineRange}</p>`;
                    }

                    elements.missingInfoDetails.classList.remove('hidden');
                    missingListHTML = result.missingAnswers.map(ans => `<li>${ans}</li>`).join('');
                    
                    // Append contact information
                    elements.missingInfoDetails.innerHTML = `<p class="font-bold">To determine your exact eligibility date, please provide answers for:</p><ul class="list-disc list-inside mt-2 ml-4">${missingListHTML}</ul><p class="mt-2">Please try to locate this information before applying, as the date of eligibility depends on it.</p>` + courthouseContactHtml;
                    break;

                case 'unclear':
                default:
                    styleClasses = 'bg-yellow-100 border-l-8 border-yellow-600 text-yellow-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-yellow-600">&#63;</span><h3 class="font-bold text-xl">Eligibility Unclear</h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    
                    if (result.missingAnswers.length > 0) {
                        elements.missingInfoDetails.classList.remove('hidden');
                        missingListHTML = result.missingAnswers.map(ans => `<li>${ans}</li>`).join('');
                        
                        // Append contact information
                        elements.missingInfoDetails.innerHTML = `<p class="font-bold">To get a clearer assessment, please provide answers for:</p><ul class="list-disc list-inside mt-2 ml-4">${missingListHTML}</ul><p class="mt-2">The timing and definitive status of your eligibility depends on these details.</p>` + courthouseContactHtml;
                    }
                    break;
            }

            elements.resultMessage.classList.add(...styleClasses.split(' '));
            elements.resultMessage.innerHTML = htmlContent;
        }

    </script>
</body>
