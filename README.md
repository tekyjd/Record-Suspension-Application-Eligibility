<html lang="en">
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
            margin: 0; 
            padding: 0; 
            min-height: 100vh; 
        }
        .container-card {
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            max-width: 90%;
            margin: 2rem auto; 
            background-color: #ffffff;
            border-radius: 0.75rem; 
        }
        /* Mobile adjustment: Remove margin and make card full width on small screens */
        @media (max-width: 640px) {
            .container-card {
                max-width: 100%;
                margin: 0; 
                border-radius: 0; 
                box-shadow: none; 
            }
        }
        .section-header {
            color: #1a4d8c; /* Dark blue */
            border-bottom: 2px solid #e6f2ff;
            padding-bottom: 0.5rem;
            margin-bottom: 1.5rem;
            font-weight: 600;
        }
        
        /* ---------------------------------------------------------------------- */
        /* INPUT STYLING */
        /* ---------------------------------------------------------------------- */
        
        input[type="date"], select {
            border: 1px solid #d1d5db;
            padding: 0.6rem 1rem; 
            border-radius: 0.5rem;
            width: 100%; 
            transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
            background-color: #f9fafb;
            cursor: pointer; 
            appearance: none;
            -webkit-appearance: none;
        }
        
        input[type="date"]:focus, select:focus {
            border-color: #4f46e5; 
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.3);
            outline: none;
        }
        
        /* Style for disabled date inputs */
        input[type="date"]:disabled {
            background-color: #e5e7eb; 
            color: #9ca3af;
            cursor: not-allowed;
        }
        
        /* Override to make native calendar icon visible and interactive */
        input[type="date"]::-webkit-calendar-picker-indicator {
            opacity: 100;
            display: block;
            cursor: pointer;
        }

        /* Custom brown color for the Schedule 1 exception text */
        .color-brown {
            color: #6D4C41; 
        }
    </style>
</head>
<body>

    <div id="app" class="container-card p-6 md:p-10">
        
        <!-- Header -->
        <div class="flex items-center justify-between pb-4 mb-6">
            <h1 class="text-2xl md:text-3xl font-extrabold text-gray-900 flex-shrink-0">
                Pardon Eligibility Checker
            </h1>
            <img 
                src="https://www.torontomu.ca/content/dam/law/images/TMU-Law-rgb.svg" 
                alt="Toronto Metropolitan University Law Logo" 
                class="h-14 md:h-24 ml-4 object-contain"
                onerror="this.onerror=null; this.src='https://placehold.co/150x40/444/FFF?text=Logo';"
            >
        </div>

        
        <!-- Disclaimer -->
        <section class="mb-8 p-4 bg-blue-50 border-l-4 border-blue-500 rounded-lg">
            <h2 class="text-xl section-header text-blue-700">Disclaimer</h2>
            <p class="text-sm text-blue-600 mb-4">Eligibility results are for informational purposes only. They are provided in good faith, based solely on the information you enter. This tool does not constitute legal advice, and using it does not guarantee that a record suspension will be granted or denied by the Parole Board of Canada.</p>
            <label class="flex items-center space-x-2 cursor-pointer">
                <input type="checkbox" id="disclaimer-accepted" class="form-checkbox h-5 w-5 text-blue-500 rounded-md">
                <span class="text-sm text-gray-700 font-medium">I accept the disclaimer and wish to proceed</span>
            </label>
        </section>

        
        <!-- Input Form -->
        <section id="input-form" class="space-y-6" style="display: none;">
            <h2 class="text-xl section-header">Conviction Details</h2>

            
            <!-- Conviction Date -->
            <div class="space-y-2">
                <label for="conviction-date" class="block text-sm font-medium text-gray-700 clickable-label">Conviction Date</label>
                <!-- ADDED 'flex items-center' HERE to align date input and checkbox -->
                <div class="date-input-group space-x-4 flex items-center">
                    <div class="w-40">
                        <input type="date" id="conviction-date" class="w-full">
                    </div>
                    <label class="flex items-center space-x-2 text-sm">
                        <input type="checkbox" id="dont-know-conv-date" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span>I'm not sure</span>
                    </label>
                </div>
            </div>

            
            <!-- Sentence Completion Date -->
            <div class="space-y-2">
                <label for="sentence-completion-date" class="block text-sm font-medium text-gray-700 clickable-label">Sentence Completion Date</label>
                 <!-- ADDED 'flex items-center' HERE to align date input and checkbox -->
                <div class="date-input-group space-x-4 flex items-center">
                    <div class="w-40">
                        <input type="date" id="sentence-completion-date" class="w-full">
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

            
            <!-- Schedule 1 Offence -->
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
                    <p class="pt-3 mb-1 font-bold underline">Common Schedule 1 Offences</p>
                    <ul class="list-disc list-inside space-y-0.5 ml-4">
                        <li>Sexual interference (s. 151)</li>
                        <li>Invitation to sexual touching (s. 152)</li>
                        <li>Child pornography (s. 163.1)</li>
                        <li>Luring a child (s. 172.1)</li>
                    </ul>
                    <p class="mt-2 font-bold"><a href="https://laws-lois.justice.gc.ca/eng/acts/c-47/page-4.html" target="_blank" class="text-blue-700 hover:text-blue-900">See the full list here.</a></p>
                </div>
            </div>

            
            <!-- 3+ Convictions of 2+ Years Imprisonment -->
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
            </div>
            <div id="missing-info-details" class="mt-4 hidden p-4 bg-yellow-50 border-l-4 border-yellow-500 rounded text-sm text-yellow-800">
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

            // Hyperlink content for the Serious Personal Injury Offence (SPIO) definition
            const criminalCodeLink = '<a href="https://laws-lois.justice.gc.ca/eng/acts/C-46/section-752.html" target="_blank" class="text-blue-600 hover:text-blue-800 underline">752 of the <i>Criminal Code</i></a>';

            // Hyperlink content for the Parole Board of Canada website (New Requirement)
            const pbcWebsiteLink = '<a href="https://www.canada.ca/en/parole-board/services/record-suspensions/applying-for-a-record-suspension.html#step6" target="_blank" class="text-blue-600 hover:text-blue-800 underline">Parole Board of Canada website</a>';

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
                
                // A. Schedule 1 Check (Known 'Yes') - EDITS 1 & 2 APPLIED HERE
                if (schedule1Offence === "Yes") {
                    const schedule1Message = `
                        <p class="mb-3">
                            Generally, individuals convicted of a <b>Schedule 1</b> offence are ineligible for a record suspension.
                        </p>
                        <p class="font-semibold mt-3 mb-2 text-sm">However, exceptions under Section 4(3) of the <i>Criminal Records Act</i> may apply if the convicted person:</p>
                        <ul class="list-disc list-inside space-y-2 ml-4 text-sm">
                            <li>was not in a position of trust or authority toward the victim;</li>
                            <li>did not use, threaten to use or attempt to use violence, intimidation or coercion in relation to the victim; and</li>
                            <li>was less than five years older than the victim.</li>
                        </ul>
                        <p class="mt-4 text-sm">For more information, consult the ${pbcWebsiteLink}.</p>
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
                    if (isConvictionDateUnknown) essentialUnknowns.push("Conviction Date");
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");

                    if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");
                    if (isTwoYearImprisonmentUnknown) essentialUnknowns.push("Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?");
                    
                    essentialUnknowns = Array.from(new Set(essentialUnknowns));

                    return { 
                        status: "unclear",
                        message: "The required information to determine your eligibility is missing. Please review the missing details below.", 
                        eligibleDate: null, 
                        missingAnswers: essentialUnknowns 
                    };
                }
                
                // D. Potentially Eligible (Date Unclear) Check (Only date/prosecution type are missing) - REFINED TIMELINE RANGE HERE
                if (isConvictionDateUnknown || isCompletionDateUnknown || isProsecutionTypeUnknown) {
                    if (isConvictionDateUnknown) essentialUnknowns.push("Conviction Date");
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    
                    let postD3Range = "5–10 years"; // Default broad range if prosecution type is unknown

                    // Refine range based on known prosecution type (User Request)
                    if (!isProsecutionTypeUnknown) {
                        if (prosecutionType === "Indictment") {
                            postD3Range = "10 years"; // Fixed 10 years for Indictment post-D3
                        } else if (prosecutionType === "Summary") {
                            postD3Range = "5 years"; // Fixed 5 years for Summary post-D3
                        }
                    }

                    essentialUnknowns = Array.from(new Set(essentialUnknowns));
                    return {
                        status: "eligible_unclear",
                        message: "You appear to be eligible for a record suspension based on the conviction type and history. However, your exact eligibility date depends on the missing date and prosecution type details.",
                        eligibleDate: null,
                        missingAnswers: essentialUnknowns,
                        timelineRange: postD3Range // <-- Using the refined range
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
                    
                    // Since Sch 1 is 'No' here, we don't need to flag it as missing, but we proceed to SPIO check.
                    
                    if (isCompletionDateUnknown) {
                         // Case 1: Completion Date is UNKNOWN
                         missingInfo.push("Sentence Completion Date (to calculate the start of the waiting period)");
                         
                         ambiguityMessage = `
                            <p class="mt-2 text-base">
                                The eligibility date depends on whether the conviction was for a <b>'serious personal injury offence'</b> (within the meaning of ${criminalCodeLink}), for which you were sentenced to a prison term of 2 years or more.
                            </p>

                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If you were convicted of a serious personal injury offence: Your waiting period is <b>10 years</b>.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If you were NOT convicted of a serious personal injury offence: Your waiting period is <b>5 years</b>.</span>
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
                                The eligibility date depends on whether the conviction was for a <b>'serious personal injury offence'</b> (within the meaning of ${criminalCodeLink}), for which you were sentenced to a prison term of 2 years or more.
                            </p>

                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If you were convicted of a serious personal injury offence: Your eligibility date is <b>${date10yrStr}</b>.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If you were NOT convicted of a serious personal injury offence: Your eligibility date is <b>${date5yrStr}</b>.</span>
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
                    
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");

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
                    
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    
                    // NEW CHECK: Schedule 1 is now flagged as essential for D1-D3 if unknown
                    if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");

                    // --- APPLY RANGES FOR UNKNOWNS IN D1-D3 PERIOD ---
                    
                    // IMPLEMENTING USER REQUEST: Summary + Sch 1 = No (Fixed 3 years) 
                    if (prosecutionType === "Summary" && schedule1Offence === "No" && !isProsecutionTypeUnknown && !isSchedule1Unknown) {
                        range = "3 years";
                    } 
                    // Rule: Summary + Sch 1 = Yes (Fixed 5 years)
                    else if (prosecutionType === "Summary" && schedule1Offence === "Yes" && !isProsecutionTypeUnknown && !isSchedule1Unknown) {
                        range = "5 years";
                    }
                    // Rule: Indictment + Sch 1 = Yes (Fixed 10 years)
                    else if (prosecutionType === "Indictment" && schedule1Offence === "Yes" && !isProsecutionTypeUnknown && !isSchedule1Unknown) {
                        range = "10 years";
                    }
                    // Ambiguous Scenarios (Involving SPIO or unknown Schedule 1 status)
                    // Rule: Indictable (Non-Sch1 or Sch1 Unknown) -> 5-10 years (SPIO ambiguity)
                    else if (prosecutionType === "Indictment" && !isProsecutionTypeUnknown) {
                        range = "5–10 years";
                    } 
                    // Rule: Summary + Sch 1 = Unknown -> 3-5 years
                    else if (prosecutionType === "Summary" && isSchedule1Unknown && !isProsecutionTypeUnknown) {
                        range = "3–5 years";
                    }
                    // Original Rule 3: Unknown Prosecution & (Schedule 1 = No or Unknown) -> 3-10 years
                    else if (isProsecutionTypeUnknown && (schedule1Offence === "No" || isSchedule1Unknown)) {
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
                    // MESSAGE REFORMATTED FOR READABILITY (User Request) - EDITS 1 & 2 APPLIED HERE
                    const schedule1Message = `
                        <p class="mb-3">
                            Generally, individuals convicted of a <b>Schedule 1</b> offence are ineligible for a record suspension.
                        </p>
                        <p class="font-semibold mt-3 mb-2 text-sm">However, exceptions under Section 4(3) of the <i>Criminal Records Act</i> may apply if the convicted person:</p>
                        <ul class="list-disc list-inside space-y-2 ml-4 text-sm">
                            <li>was not in a position of trust or authority toward the victim;</li>
                            <li>did not use, threaten to use or attempt to use violence, intimidation or coercion in relation to the victim; and</li>
                            <li>was less than five years older than the victim.</li>
                        </ul>
                        <p class="mt-4 text-sm">For more information, consult the ${pbcWebsiteLink}.</p>
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
                if (isConvictionDateUnknown) essentialUnknowns.push("Conviction Date");
                if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
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
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    // Conviction Date is the main reason we are here, so add it
                    essentialUnknowns.push("Conviction Date");
                    
                    // Customize range based on known non-date factors:
                    if (prosecutionType === "Indictment" && !isProsecutionTypeUnknown) {
                        // If Indictment is KNOWN, the min wait time is 5, max is 10 (pre-D1 vs post-D3)
                        range = "5–10 years";
                    } else if (prosecutionType === "Summary" && !isProsecutionTypeUnknown) {
                        // If Summary is KNOWN, the min wait time is 3, max is 5 (pre-D1 vs post-D3)
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
                return { status: "unclear", message: "Eligibility calculation failed: Unhandled date range.", eligibleDate: null, missingAnswers: [] };
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
                // On or after March 13, 2012 (Current Rules) - CONFIRMED LOGIC
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
                    message: `You are eligible to apply for a record suspension now. The waiting period was determined to be <b>${waitPeriodYears} years</b>.`,
                    eligibleDate: eligibleDate,
                    missingAnswers: []
                };
            } else {
                const dateString = formatEligibleDate(eligibleDate);
                return {
                    status: "eligible_future",
                    message: `You will be eligible on ${dateString}. The required waiting period is <b>${waitPeriodYears} years</b> from your sentence completion date.`,
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
         * Renders the result object to the UI, applying custom styling for Schedule 1 exception.
         */
        function displayResult(result) {
            elements.resultHeader.classList.remove('hidden');
            elements.missingInfoDetails.classList.add('hidden');
            // Reset base classes, adding shadow and transition back
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
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-green-600">🎉</span><h3 class="font-bold text-xl"><b>Eligible Now!</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    break;

                case 'eligible_future':
                    styleClasses = 'bg-blue-100 border-l-8 border-blue-600 text-blue-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-blue-600">&#9202;</span><h3 class="font-bold text-xl"><b>Eligible in the Future</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    break;

                case 'ineligible':
                    styleClasses = 'bg-red-100 border-l-8 border-red-600 text-red-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-red-600">&#10060;</span><h3 class="font-bold text-xl"><b>Ineligible</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    break;

                case 'schedule1_exception':
                    // Custom style applied: Background/Border kept yellow/amber, but text color removed for custom handling.
                    styleClasses = 'bg-yellow-100 border-l-8 border-amber-600'; 
                    
                    // Heading color set to black (text-black)
                    // Body message wrapped in color-brown custom class
                    htmlContent = `
                        <div class="flex items-center space-x-3">
                            <span class="text-3xl text-amber-600">⚠️</span>
                            <h3 class="font-bold text-xl text-black"><b>Schedule 1 Offence — Possible Exception</b></h3>
                        </div>
                        <div class="color-brown mt-2">
                            ${result.message}
                        </div>
                    `;
                    break;

                case 'eligible_unclear':
                    styleClasses = 'bg-indigo-100 border-l-8 border-indigo-600 text-indigo-800'; 
                    // Blue Checkmark: &#10003;
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-indigo-600">&#10003;</span><h3 class="font-bold text-xl"><b>Likely Eligible (Timeline Ambiguous)</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    
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
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-yellow-600">&#63;</span><h3 class="font-bold text-xl"><b>Eligibility Unclear</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    
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
</html>
