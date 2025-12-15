<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSM Master Command Center | RLS Operations</title>
    <style>
        /* CSS Variables & Global Styles */
        :root {
            --primary: #003366; /* Deep Blue */
            --secondary: #00509d; /* Medium Blue */
            --accent: #f5cd4e; /* RLS Gold/Yellow */
            --bg: #f8f9fa;
            --text: #333;
            --step-border: #e9ecef;
        }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: var(--bg); color: var(--text); line-height: 1.6; margin: 0; padding: 20px; }
        .container { max-width: 1000px; margin: auto; background: white; padding: 30px; border-radius: 12px; box-shadow: 0 10px 40px rgba(0,0,0,0.15); }
        h1 { color: var(--primary); border-bottom: 4px solid var(--accent); padding-bottom: 10px; text-align: center; margin-bottom: 25px; }
        
        /* Navigation Styles */
        .phase-nav { display: flex; gap: 8px; margin-bottom: 30px; flex-wrap: wrap; justify-content: center; background: var(--step-border); padding: 10px; border-radius: 8px; }
        .phase-btn { padding: 12px 18px; border: none; background: #fff; border-radius: 6px; cursor: pointer; font-weight: bold; transition: 0.3s; font-size: 0.9em; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .phase-btn:hover { background: var(--accent); color: var(--primary); }
        .phase-btn.active { background: var(--primary); color: white; box-shadow: 0 4px 8px rgba(0,0,0,0.2); }
        .phase-content { display: none; }
        
        /* Step Card Styles */
        .step-card { 
            background: #fff; 
            border: 1px solid var(--step-border); 
            padding: 25px; 
            margin-bottom: 25px; 
            border-radius: 8px; 
            display: none; 
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }
        .step-card.active { display: block; animation: fadeIn 0.5s ease; }
        .step-card h3 { color: var(--secondary); margin-top: 0; border-bottom: 2px dashed var(--accent); padding-bottom: 10px; }
        
        /* Interactive/Button Area */
        .interactive-area { background: #f0f4f8; padding: 15px; border-radius: 8px; margin-top: 15px; border-left: 5px solid var(--accent); }
        button.action, .logic-btn { 
            background: var(--accent); 
            color: var(--primary); 
            border: none; 
            padding: 10px 15px; 
            border-radius: 5px; 
            cursor: pointer; 
            margin: 5px 5px 5px 0; 
            font-weight: bold; 
            transition: 0.2s;
        }
        button.action:hover, .logic-btn:hover { background: #e0b43f; }
        
        /* Links and Resources */
        .resource-link { font-size: 0.9em; color: var(--secondary); font-style: italic; display: block; margin-top: 15px; padding-left: 10px; border-left: 3px solid var(--accent); }
        .tool-link { font-weight: bold; color: var(--primary); text-decoration: none; }
        .tool-link:hover { text-decoration: underline; }

        .timeline-box { 
            border: 1px solid #ddd; 
            padding: 15px; 
            background: #fff7e6; 
            border-radius: 5px; 
            margin-top: 10px;
        }
        .timeline-box strong { color: #cc6600; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        
        /* Progress Bar */
        .progress-bar { width: 100%; background: #e0e0e0; height: 10px; border-radius: 5px; margin-bottom: 20px; }
        .progress-fill { height: 100%; background: var(--secondary); width: 0%; border-radius: 5px; transition: 0.5s; }
    </style>
</head>
<body>

<div class="container">
    <h1>CSM MASTER COMMAND CENTER</h1>
    
    <div class="progress-bar"><div class="progress-fill" id="progress"></div></div>

    <div class="phase-nav" id="phase-navigation">
        <button class="phase-btn" data-phase="intake">1. Intake</button>
        <button class="phase-btn" data-phase="koc">2. KOC</button>
        <button class="phase-btn" data-phase="sourcing">3. Sourcing</button>
        <button class="phase-btn" data-phase="hiring">4. Hiring</button>
        <button class="phase-btn" data-phase="onboarding">5. Handover</button>
        <button class="phase-btn" data-phase="growth">6. Growth & Risk</button>
    </div>

    <div id="phase-intake" class="phase-content">
        <div id="step-intake-start" class="step-card active">
            <h3>Phase 1: Intake & Buyer Intent (The Strategy Setter)</h3>
            <p>Review the new client request and generate the score to set the engagement strategy.</p>
            <ol>
                <li>Receive the Client Request and sales notes via the Recruiting Slack channel.</li>
                <li>**SC/CSM:** Use the Buyer Intent Scoring tool to generate the client's Intent Score (0-7).</li>
            </ol>
            <div class="interactive-area">
                <p>What is the final Buyer Intent Score?</p>
                <button class="logic-btn" onclick="nextStep('intake-hot', 'intake')">Score 6-7 (Hot)</button>
                <button class="logic-btn" onclick="nextStep('intake-warm', 'intake')">Score 4-5 (Warm)</button>
                <button class="logic-btn" onclick="nextStep('intake-cold', 'intake')">Score 0-3 (Cold/Explorer)</button>
            </div>
            <span class="resource-link">Ref: CSM Guide Client Hiring Process.pdf</span>
        </div>

        <div id="step-intake-hot" class="step-card">
            <h3 style="color: green;">Outcome: HOT BUYER</h3>
            <p>**Immediate Action:** Proceed to KOC Preparation. Notify the Recruiter and SC that this is a high-priority search ready for action.</p>
            <button class="action" onclick="showPhase('koc')">Move to Phase 2: KOC Prep →</button>
        </div>

        <div id="step-intake-warm" class="step-card">
            <h3 style="color: orange;">Outcome: WARM BUYER</h3>
            <p>**Action:** Schedule the KOC. Be prepared to provide extra reassurance and social proof during the call to build momentum.</p>
            <button class="action" onclick="showPhase('koc')">Move to Phase 2: KOC Prep →</button>
        </div>

        <div id="step-intake-cold" class="step-card">
            <h3 style="color: red;">Outcome: COLD/NON-BUYER</h3>
            <p><strong>STOP.</strong> Notify the Operations Manager (OM). Do not trigger recruiting effort. Schedule a "Clarity Call" to determine genuine urgency and readiness before moving forward.</p>
        </div>
    </div>

    <div id="phase-koc" class="phase-content">
        <div id="step-koc-start" class="step-card active">
            <h3>Phase 2.1: Intelligence Generation & KOC Prep</h3>
            <ol>
                <li>Review firm history and existing JD/notes.</li>
                <li>**Generate Intelligence Master Prompt:** Use the client data to populate the master prompt template.</li>
                <li>**AI Summary & Questions:** Feed the prompt output into AI to create a call summary and extract the key questions for an effective KOC.</li>
            </ol>
            <div class="interactive-area">
                <p>Have you completed all KOC prep steps (Intelligence Prompt & AI Summary)?</p>
                <button class="logic-btn" onclick="nextStep('koc-execute', 'koc')">Yes, Ready to Execute KOC</button>
            </div>
            <span class="resource-link">Resource: <a href="https://docs.google.com/document/d/1aMIKGI5GMBdoKrodA7JMsZQYAl20vNTGJ-ofsP3lUPM/edit?tab=t.0#heading=h.1pavpxi5z5xo" target="_blank" class="tool-link">Intelligence Master Prompt Template</a></span>
        </div>
        
        <div id="step-koc-execute" class="step-card">
            <h3>Phase 2.2: KOC Execution & Contingency Planning</h3>
            <p>Lead the KOC, focusing on the problem the role solves and confirming the **3-business-day handover rule**.</p>
            <div class="interactive-area">
                <p>Did the client raise any task-related roadblocks during the call?</p>
                <button class="logic-btn" onclick="nextStep('koc-delegate-issue', 'koc')">Client doesn't know what to delegate</button>
                <button class="logic-btn" onclick="nextStep('koc-physical-issue', 'koc')">Client asks about remote physical tasks / local hiring</button>
                <button class="logic-btn" onclick="nextStep('koc-summary', 'koc')">No roadblocks, Proceed to Summary</button>
            </div>
        </div>

        <div id="step-koc-delegate-issue" class="step-card">
            <h3 style="color: var(--accent);">Contingency: Delegation Assistance</h3>
            <p>**Action:** Share the Delegation Guide to help the client identify tasks that can be outsourced immediately. Use this to pivot the conversation back to their urgent needs.</p>
            <button class="action" onclick="nextStep('koc-summary', 'koc')">Continue to KOC Summary →</button>
            <span class="resource-link">Resource: <a href="https://docs.google.com/spreadsheets/d/1VaNRbiTwSMSJtk1uE94UBgL3V_JoLw4aDe-NrKfBg5Q/edit" target="_blank" class="tool-link">Tasks to Delegate Guide (Spreadsheet)</a></span>
        </div>

        <div id="step-koc-physical-issue" class="step-card">
            <h3 style="color: var(--accent);">Contingency: Remote Task/Local Hiring</h3>
            <p>**Action:** Use the provided data sheet and talking points to confidently address remote capabilities and the advantages over local hiring.</p>
            <button class="action" onclick="nextStep('koc-summary', 'koc')">Continue to KOC Summary →</button>
            <span class="resource-link">Resource 1 (Data): <a href="https://docs.google.com/spreadsheets/d/1-jDWIOl6tGZKSktlxaDVs007v6_2sDeIXsjwXAMWt2U/edit" target="_blank" class="tool-link">Remote Staff Physical Tasks List</a><br>Resource 2 (Talking Points): <a href="https://docs.google.com/document/d/1pNk9seItinSmOy3mqHMKas3zsq1Q7KLmSpCyjfcut8M/edit?tab=t.0" target="_blank" class="tool-link">Local Hiring/Remote Talking Points</a></span>
        </div>

        <div id="step-koc-summary" class="step-card">
            <h3>Phase 2.3: Post-KOC Handoff</h3>
            <ol>
                <li>**Summarize Notes:** Use the KOC Summary GPT to finalize notes.</li>
                <li>**Notify Recruiting:** Share the summary in the Recruiting Slack thread to trigger sourcing.</li>
            </ol>
            <button class="action" onclick="showPhase('sourcing')">Move to Phase 3: Sourcing & Follow-up →</button>
            <span class="resource-link">Tool: <a href="https://chatgpt.com/g/g-67fc87ce799c8191902227ff1eacd5d0-kick-off-call-summary" target="_blank" class="tool-link">Kick-Off Call Summary GPT</a></span>
        </div>
    </div>

    <div id="phase-sourcing" class="phase-content">
        <div id="step-sourcing-start" class="step-card active">
            <h3>Phase 3.1: Sourcing Timeline & Follow-up</h3>
            <p>The sourcing process is now active. Your role is to manage the timeline and communication.</p>
            <div class="timeline-box">
                **0 Hours:** KOC Summary shared. Sourcing begins. <br>
                **48 Hours:** **Action:** Follow up with recruiters if no updates on candidates yet. <br>
                **72 Hours:** **Target:** Candidates should be ready for endorsement.
            </div>
            <div class="interactive-area">
                <p>Is the first batch of candidates ready for Candidate Review Call (CRC)?</p>
                <button class="logic-btn" onclick="nextStep('sourcing-prep-crc', 'sourcing')">Yes, candidates ready (after 72h)</button>
            </div>
            <span class="resource-link">Ref: CSM Guide Client Hiring Process.pdf</span>
        </div>

        <div id="step-sourcing-prep-crc" class="step-card">
            <h3>Phase 3.2: Candidate Review Call (CRC) Prep</h3>
            <ol>
                <li>**Candidate Summary:** For each candidate, use the Interview Question Builder GPT to create a comprehensive professional summary, anticipating misalignments. (SC assists).</li>
                <li>**CRC Execution:** Present the summaries to the client.</li>
            </ol>
            <div class="interactive-area">
                <p>What was the client's decision after the CRC?</p>
                <button class="logic-btn" onclick="nextStep('sourcing-interview-select', 'sourcing')">Client selected candidates for interview</button>
                <button class="logic-btn" onclick="nextStep('sourcing-reject-batch', 'sourcing')">Client rejected all candidates (Need Batch 2)</button>
            </div>
            <span class="resource-link">Tool: <a href="https://chatgpt.com/g/g-67fc8e7ade9c8191b79e3e75d10a09f8-interview-question-builder" target="_blank" class="tool-link">Interview Question Builder GPT (for Summary/Prep)</a></span>
        </div>

        <div id="step-sourcing-reject-batch" class="step-card">
            <h3 style="color: red;">Outcome: Batch Rejected</h3>
            <p>**Action:** Update the Monday board and notify the Recruiter. **Restart Sourcing Loop:** Go back to the **48-hour follow-up** timeline for the second batch of candidates.</p>
            <button class="action" onclick="showPhase('sourcing')">Go Back to Sourcing Follow-up (Phase 3.1) →</button>
        </div>

        <div id="step-sourcing-interview-select" class="step-card">
            <h3>Phase 3.3: Client Interview Preparation</h3>
            <ol>
                <li>Schedule the Client Interview and notify the Recruiter.</li>
                <li>**Interview Questions:** Use the Interview Question Builder GPT to prepare focused interview questions based on the candidate profiles and specific job requirements.</li>
                <li>**Facilitate:** Confirm attendance, provide the Interview Grading Form to the client.</li>
            </ol>
            <button class="action" onclick="showPhase('hiring')">Move to Phase 4: Interview & Final Decision →</button>
            <span class="resource-link">Tool: <a href="https://chatgpt.com/g/g-67fc8e7ade9c8191b79e3e75d10a09f8-interview-question-builder" target="_blank" class="tool-link">Interview Question Builder GPT (for Interview Questions)</a></span>
        </div>
    </div>

    <div id="phase-hiring" class="phase-content">
        <div id="step-hiring-start" class="step-card active">
            <h3>Phase 4.1: Post-Interview Debrief</h3>
            <p>Conduct the comprehensive debrief immediately after the final interview.</p>
            <div class="interactive-area">
                <p>What was the final decision?</p>
                <button class="logic-btn" onclick="nextStep('hiring-offer', 'hiring')">Client selected a candidate (HIRE)</button>
                <button class="logic-btn" onclick="nextStep('hiring-reject-final', 'hiring')">Client did NOT select a candidate (REJECT)</button>
            </div>
            <span class="resource-link">Ref: CSM Guide Client Hiring Process.pdf</span>
        </div>

        <div id="step-hiring-reject-final" class="step-card">
            <h3 style="color: red;">Outcome: No Hire</h3>
            <p>**Action:** Realign with the client on what went wrong (Skill vs. Culture). Share detailed feedback with the Recruiter. **Restart Sourcing Loop** and continue the process until a hire is made.</p>
            <button class="action" onclick="showPhase('sourcing')">Restart Sourcing Loop (Go to Phase 3.1) →</button>
        </div>
        
        <div id="step-hiring-offer" class="step-card">
            <h3>Phase 4.2: Payment & Offer</h3>
            <ol>
                <li>**Payment Link:** Generate the payment link for the client's remaining balance.</li>
                <li>**Finance Confirmation:** Wait for Finance to confirm payment.</li>
                <li>**Job Offer:** Initiate Job Offer Request and wait for the staff's agreement.</li>
            </ol>
            <div class="interactive-area">
                <p>Has Finance confirmed payment and the staff accepted the offer?</p>
                <button class="logic-btn" onclick="showPhase('onboarding')">Yes, Ready for Handover →</button>
            </div>
            <span class="resource-link">Tool: <a href="https://docs.google.com/spreadsheets/d/1AOKlAkY12IZPHy7qcvgYJFfDzpUBOloWy2PnZvQpuoc/edit" target="_blank" class="tool-link">Payment Link Generator (Spreadsheet)</a></span>
        </div>
    </div>

    <div id="phase-onboarding" class="phase-content">
        <div id="step-onboarding-start" class="step-card active">
            <h3>Phase 5: Staff & Client Handover (The Safety Net)</h3>
            <p>Ensure a smooth start and reinforce the partnership in the critical first week.</p>
            <ol>
                <li>**Start Date:** Confirm start date (Min. **3 business days** from payment).</li>
                <li>**Client Onboarding Call:** Schedule and facilitate **no later than 1 business day prior** to deployment. Request client to send the staff a calendar invite.</li>
                <li>**Handover Email:** Send the Email Introduction to formally endorse the staff and set expectations.</li>
                <li>**Day 1 Check-in (CSM):** Send a mid-day check-in email to the client to gauge training progress.</li>
                <li>**Week 1 Mastery:** Conduct **Daily Check-ins** with the client to monitor progress and address issues promptly.</li>
            </ol>
            <div class="interactive-area">
                <p>Is the first week successfully completed with no major issues?</p>
                <button class="action" onclick="showPhase('growth')">Move to Phase 6: Retention & Growth →</button>
            </div>
            <span class="resource-link">Ref: Handover Process.pdf</span>
        </div>
    </div>

    <div id="phase-growth" class="phase-content">
        <div id="step-growth-start" class="step-card active">
            <h3>Phase 6.1: Monthly Health Check & GAC Prep</h3>
            <p>Review monthly satisfaction survey results to determine the next course of action.</p>
            <ol>
                <li>**Monthly Survey Review:** (Start of Month) Review client scores and feedback.</li>
                <li>**GAC Scheduling:** (Weeks 1 & 2) Send calendar invites for the Growth Alignment Call (GAC).</li>
            </ol>
            <div class="interactive-area">
                <p>What was the client's Satisfaction Survey Score?</p>
                <button class="logic-btn" onclick="nextStep('growth-high', 'growth')">Score 9-10 (High Satisfaction)</button>
                <button class="logic-btn" onclick="nextStep('growth-low', 'growth')">Score < 7 (Low Satisfaction / Escalation)</button>
            </div>
        </div>

        <div id="step-growth-high" class="step-card">
            <h3>Phase 6.2: Growth Alignment Call (GAC)</h3>
            <p>Lead the GAC to reinforce trust and create growth openings (referrals, upsells).</p>
            <ol>
                <li>**Prep:** Review Hubstaff data and coaching logs.</li>
                <li>**Execution:** Translate productivity into **Business Outcomes (ROI)**.</li>
                <li>**Coaching:** Use the "Why" Coaching Framework to drive strategic conversations.</li>
            </ol>
            <button class="action" onclick="showPhase('intake')">Client Expansion? Start a New Intake →</button>
            <span class="resource-link">Ref: Growth Alignment Call Mastery.pdf | Untitled document (7).pdf (Coaching)</span>
        </div>

        <div id="step-growth-low" class="step-card" style="border-left-color: red;">
            <h3>🚨 Phase 6.3: Escalation Protocol</h3>
            <p>**Immediate Action Required** (Ref: Client Success Team Escalations Checklist.pdf)</p>
            <ol>
                <li>**Step 1 (Report):** Immediately Report to SC, CSM, OM, and Log in Incident Tracker.</li>
                <li>**Step 2 (Gather):** SC audits screenshots, coaching logs, and surveys.</li>
                <li>**Step 3 (Analyze):** CSM pre-determines root cause (**Skill, Knowledge, or Will**).</li>
                <li>**Step 4 (Resolution):** Collaborate with OM on communication strategy.</li>
            </ol>
            <div class="interactive-area">
                <p>Does the analysis require a staff replacement?</p>
                <button class="logic-btn" onclick="nextStep('growth-continuity', 'growth')">Yes, Replacement is needed</button>
                <button class="logic-btn" onclick="nextStep('growth-high', 'growth')">No, Resolution Found (Go back to GAC)</button>
            </div>
        </div>
        
        <div id="step-growth-continuity" class="step-card" style="border-left-color: darkgoldenrod;">
            <h3>Phase 6.4: Continuity Care Program</h3>
            <p>Proactively manage the staff transition to minimize client disruption.</p>
            <ol>
                <li>Proactive Client Communication.</li>
                <li>Implement **100% Daily Screenshot Audits** for the *new* staff (first 2 weeks).</li>
                <li>Conduct a formal **1st Month Confidence Check** call with the client.</li>
            </ol>
            <button class="action" onclick="showPhase('intake')">New Staff Sourcing Required (Start Intake) →</button>
            <span class="resource-link">Ref: Continuity Care Program (1).pdf</span>
        </div>
    </div>
</div>

<script>
    // JAVASCRIPT LOGIC for Interactivity
    const phases = ['intake', 'koc', 'sourcing', 'hiring', 'onboarding', 'growth'];

    function showPhase(phaseId) {
        // Find the index of the phase to update the progress bar
        const index = phases.indexOf(phaseId);
        
        // Hide all phases and remove active class from all step-cards
        document.querySelectorAll('.phase-content').forEach(p => p.style.display = 'none');
        document.querySelectorAll('.step-card').forEach(s => s.classList.remove('active'));

        // Show the target phase content
        const targetPhase = document.getElementById('phase-' + phaseId);
        if (targetPhase) {
            targetPhase.style.display = 'block';
            // Find the *first* step-card in the target phase and make it active
            const startStep = targetPhase.querySelector('.step-card');
            if (startStep) {
                startStep.classList.add('active');
            }
        }
        
        // Update Nav UI
        document.querySelectorAll('.phase-btn').forEach(btn => btn.classList.remove('active'));
        const phaseBtn = document.querySelector(`.phase-btn[data-phase="${phaseId}"]`);
        if (phaseBtn) {
            phaseBtn.classList.add('active');
        }

        // Update Progress Bar
        document.getElementById('progress').style.width = ((index + 1) / phases.length * 100) + '%';
    }

    function nextStep(stepId, currentPhaseId) {
        // Find the current phase content
        const currentPhase = document.getElementById('phase-' + currentPhaseId);
        if (currentPhase) {
            // Hide all step-cards within the current phase
            currentPhase.querySelectorAll('.step-card').forEach(s => s.classList.remove('active'));
        }

        // Show the target step-card
        const targetStep = document.getElementById('step-' + stepId);
        if (targetStep) {
            targetStep.classList.add('active');
        }
    }

    function initPortal() {
        // Add event listeners to phase buttons
        document.querySelectorAll('.phase-btn').forEach(button => {
            button.addEventListener('click', (e) => {
                showPhase(e.target.getAttribute('data-phase'));
            });
        });

        // Initialize the portal by showing the first phase
        showPhase('intake');
    }

    // Run the initialization function when the window loads
    window.onload = initPortal;
</script>

</body>
</html>
