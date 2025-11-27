Made by Shane Henry 
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>StudyHub — Business Studies (3rd Year)</title>
<style>
  :root{
    --bg:#f4f7fb; --card:#fff; --muted:#6b7280; --accent:#2563eb; --good:#10b981; --bad:#ef4444;
  }
  body{font-family:Inter,system-ui,Arial,sans-serif;background:var(--bg);margin:0;color:#0f172a}
  .wrap{max-width:1100px;margin:28px auto;padding:20px}
  header{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px;gap:12px}
  h1{font-size:20px;margin:0}
  .subtitle{color:var(--muted);font-size:13px}
  .top-controls{display:flex;gap:10px;align-items:center}
  select,input[type="checkbox"]{padding:8px;border-radius:6px;border:1px solid #d1d5db}
  .grid{display:grid;grid-template-columns:280px 1fr;gap:18px}
  .panel{background:var(--card);padding:14px;border-radius:10px;box-shadow:0 6px 18px rgba(15,23,42,0.06)}
  .sections-list button{display:block;width:100%;text-align:left;padding:8px;border-radius:8px;border:0;background:transparent;cursor:pointer}
  .sections-list button.active{background:#eef2ff;font-weight:600}
  .stats{font-size:13px;color:var(--muted);margin-top:8px}
  .flashcard-wrap{display:flex;flex-direction:column;gap:12px}
  .card{background:linear-gradient(180deg,#fff,#fbfdff);padding:22px;border-radius:12px;min-height:160px;display:flex;flex-direction:column;justify-content:space-between}
  .q{font-weight:600;font-size:18px}
  .meta{display:flex;gap:10px;align-items:center;font-size:13px;color:var(--muted)}
  .controls{display:flex;gap:8px}
  .btn{padding:8px 12px;border-radius:8px;border:0;cursor:pointer;background:var(--accent);color:white}
  .btn.ghost{background:transparent;border:1px solid #e6e9ef;color:var(--muted)}
  .btn.good{background:var(--good)}
  .btn.bad{background:var(--bad)}
  .small{padding:6px 8px;font-size:13px}
  .progress-row{display:flex;gap:8px;align-items:center;margin-top:8px}
  .bar{height:10px;background:#e6eefc;border-radius:999px;overflow:hidden;flex:1}
  .bar > i{display:block;height:100%;background:var(--accent);width:0%}
  .controls-bottom{display:flex;gap:10px;align-items:center}
  .list-card{padding:10px;border-radius:8px;border:1px solid #eef2ff;margin-bottom:8px}
  .flash-mode{display:flex;gap:10px;align-items:center}
  .footer{margin-top:16px;font-size:13px;color:var(--muted)}
  .learn-area{margin-top:12px;background:#fff;padding:12px;border-radius:8px;border:1px solid #eef2ff}
  .mc-option{display:block;padding:10px;border-radius:6px;border:1px solid #e6eefc;margin:8px 0;background:#fff;cursor:pointer;text-align:left}
  .mc-option.correct{border-color:var(--good);background:#ecfdf5}
  .mc-option.wrong{border-color:var(--bad);background:#fff1f2}
  .row{display:flex;gap:8px;align-items:center}
  .badge{padding:6px 8px;border-radius:999px;background:#eef2ff;color:#075985;font-weight:600;font-size:12px}
  /* responsive */
  @media (max-width:880px){.grid{grid-template-columns:1fr;}.panel{padding:12px}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div style="flex:1">
      <h1>StudyHub — Business Studies (3rd Year, Ireland)</h1>
      <div class="subtitle">Chapters: ACB 4 · World of Work 12 · Digital Tech 16 · Planning 17 · Finance 18 · Documents 19 · Payslips 11</div>
    </div>
    <div class="top-controls">
      <label style="font-size:13px;color:var(--muted)">Randomize</label>
      <input id="randToggle" type="checkbox" title="Randomize order" />
      <button id="exportBtn" class="btn small">Export Progress</button>
      <button id="resetAllBtn" class="btn small" style="background:#ef4444">Reset All</button>
    </div>
  </header>

  <div class="grid">
    <!-- Left panel: sections -->
    <aside class="panel">
      <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
        <strong>Sections</strong>
        <small class="subtitle">Choose chapter</small>
      </div>
      <div class="sections-list" id="sectionsList"></div>
      <div class="stats" id="globalStats"></div>
      <hr style="margin:12px 0;border:none;border-top:1px solid #eef2ff" />
      <div style="font-size:13px;color:var(--muted)"><strong>Filters</strong></div>
      <div style="margin-top:8px;display:flex;gap:8px;">
        <select id="difficultyFilter">
          <option value="all">All difficulties</option>
          <option value="Easy">Easy</option>
          <option value="Medium">Medium</option>
          <option value="Hard">Hard</option>
        </select>
        <button id="shuffleBtn" class="btn small">Shuffle</button>
      </div>
      <div class="footer">
        Tip: use <strong>Learn</strong> for multiple-choice practice. Progress saves in your browser.
      </div>
    </aside>

    <!-- Right panel: flashcards -->
    <main>
      <div class="panel">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div>
            <div style="font-size:14px;font-weight:700" id="sectionTitle">Loading...</div>
            <div class="subtitle" id="sectionSubtitle">0 cards · 0 known</div>
          </div>
          <div style="display:flex;gap:8px;align-items:center">
            <div class="flash-mode">
              <label class="subtitle">Mode</label>
              <select id="modeSelect">
                <option value="sequential">Sequential</option>
                <option value="study">Study (repeat unknown)</option>
                <option value="random">Random</option>
              </select>
            </div>
            <button id="learnModeBtn" class="btn small">Start Learn Mode</button>
            <button id="printBtn" class="btn small ghost">Print</button>
            <button id="resetSectionBtn" class="btn small ghost">Reset Section</button>
          </div>
        </div>

        <div class="flashcard-wrap" style="margin-top:12px">
          <div class="card" id="flashcard">
            <div>
              <div class="meta"><span id="cardIdx">1/30</span><span id="difficultyBadge" class="badge" style="margin-left:8px">Easy</span></div>
              <div class="q" id="questionText">Question will appear here</div>
            </div>
            <div style="display:flex;justify-content:space-between;align-items:center">
              <div class="meta" id="answerReveal" style="display:none">
                <div><strong>Answer:</strong> <span id="answerText"></span></div>
              </div>
              <div class="controls" style="margin-left:auto">
                <button id="prevBtn" class="btn ghost small">Prev</button>
                <button id="showBtn" class="btn small">Show Answer</button>
                <button id="nextBtn" class="btn ghost small">Next</button>
              </div>
            </div>
          </div>

          <div style="display:flex;justify-content:space-between;align-items:center">
            <div class="controls-bottom">
              <button id="knowBtn" class="btn good small">I know this</button>
              <button id="reviseBtn" class="btn bad small">Needs revision</button>
              <button id="markHardBtn" class="btn ghost small">Toggle Hard</button>
            </div>
            <div style="text-align:right">
              <div class="progress-row"><div style="font-size:13px;color:var(--muted)">Progress</div><div class="bar" style="width:220px;margin-left:8px"><i id="progressBar"></i></div><div style="width:46px;text-align:right;font-weight:600" id="progressPct">0%</div></div>
              <div style="margin-top:6px;font-size:13px;color:var(--muted)"><span id="knownCount">Known: 0</span> · <span id="reviseCount">To revise: 0</span></div>
            </div>
          </div>

        </div>

        <div id="learnContainer" class="learn-area" style="display:none">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <strong>Learn Mode (Multiple Choice)</strong>
            <button id="endLearnBtn" class="btn ghost small">Exit Learn Mode</button>
          </div>
          <div id="learnArea" style="margin-top:10px"></div>
        </div>

        <hr style="margin:14px 0;border:none;border-top:1px solid #eef2ff" />

        <div id="listPanel"></div>
      </div>
    </main>
  </div>
</div>

<script>
/* ============================
  Flashcards data (30 per section)
  Tailored for 3rd-year Business Studies (Ireland)
============================ */
const DATA = {
  "ACB - Chapter 4": [
    {q:"What is the primary purpose of a statement of financial position (balance sheet)?", a:"To show a business's assets, liabilities and owner's equity at a specific date.", difficulty:"Easy"},
    {q:"Define 'current asset'.", a:"An asset expected to be converted to cash or used within 12 months (e.g., inventory).", difficulty:"Easy"},
    {q:"What is 'depreciation'?", a:"Allocation of an asset's cost over its useful life to reflect wear and value loss.", difficulty:"Medium"},
    {q:"Explain 'accruals' in accounting.", a:"Expenses or income recognised when incurred/earned, not when cash changes hands.", difficulty:"Medium"},
    {q:"Profit vs cash — what's the difference?", a:"Profit is accounting measure (income − costs); cash is actual money in bank.", difficulty:"Easy"},
    {q:"Why prepare a trial balance?", a:"To check that total debits equal total credits before final accounts.", difficulty:"Easy"},
    {q:"Define 'ordinary share capital'.", a:"Capital from issuing ordinary shares which represent ownership in a company.", difficulty:"Easy"},
    {q:"What is a creditors control account?", a:"A summary account for all supplier transactions reconciled with individual ledgers.", difficulty:"Medium"},
    {q:"What is a bad debt?", a:"A receivable that cannot be collected and is written off as an expense.", difficulty:"Medium"},
    {q:"Give an example of a prepayment.", a:"Prepaid insurance paid in advance recorded as an asset until used.", difficulty:"Easy"},
    {q:"How do intangible assets differ from tangible assets?", a:"Intangibles lack physical form (e.g., patents); tangibles are physical (e.g., equipment).", difficulty:"Easy"},
    {q:"What does 'working capital' indicate?", a:"Short-term liquidity: current assets − current liabilities.", difficulty:"Medium"},
    {q:"Name a method to value inventory.", a:"FIFO, LIFO or weighted average cost (FIFO commonly used).", difficulty:"Medium"},
    {q:"What is owner's equity?", a:"Residual interest in assets after liabilities are deducted (capital + retained earnings).", difficulty:"Easy"},
    {q:"Why do bank reconciliations matter?", a:"To find and correct differences between company and bank records.", difficulty:"Easy"},
    {q:"Define 'capital expenditure'.", a:"Spending on assets that will benefit the business for more than one year.", difficulty:"Easy"},
    {q:"Explain the matching principle.", a:"Expenses are matched to the revenues they helped generate in the same period.", difficulty:"Medium"},
    {q:"What are retained earnings?", a:"Accumulated profits kept in the business after dividends.", difficulty:"Easy"},
    {q:"How is gross profit computed?", a:"Net sales minus cost of goods sold.", difficulty:"Easy"},
    {q:"Give an example of a liquidity ratio.", a:"Current ratio = current assets / current liabilities.", difficulty:"Medium"},
    {q:"What is a provision?", a:"A liability of uncertain timing or amount recognised for probable future expenses.", difficulty:"Hard"},
    {q:"Capital vs revenue expenditure — one difference?", a:"Capital adds long-term value; revenue is day-to-day running costs.", difficulty:"Medium"},
    {q:"How are discounts allowed and received recorded?", a:"Discount allowed is an expense; discount received reduces purchase cost.", difficulty:"Medium"},
    {q:"What is double-entry bookkeeping?", a:"Each transaction records equal debits and credits to keep accounting balanced.", difficulty:"Easy"},
    {q:"Why have an allowance for doubtful accounts?", a:"To estimate potential receivable losses and present realistic receivables.", difficulty:"Medium"},
    {q:"Formula for straight-line depreciation?", a:"(Cost − Residual value) ÷ Useful life (years).", difficulty:"Medium"},
    {q:"What is goodwill?", a:"Excess paid over fair value in a business acquisition reflecting reputation and customer base.", difficulty:"Hard"},
    {q:"What are deferred tax liabilities?", a:"Taxes payable in future due to temporary differences between accounting and tax treatments.", difficulty:"Hard"},
    {q:"How does issuing shares affect the balance sheet?", a:"Increases assets (cash) and increases equity (share capital).", difficulty:"Easy"},
    {q:"Why is consistency of accounting policies important?", a:"Ensures comparability of financial statements over time.", difficulty:"Medium"}
  ],

  "World of Work - Chapter 12": [
    {q:"Define 'labour market'.", a:"Where employers seek workers and workers seek jobs — supply and demand for labour.", difficulty:"Easy"},
    {q:"What is a CV — two important elements?", a:"Curriculum Vitae; includes education and relevant work experience.", difficulty:"Easy"},
    {q:"Explain 'person specification'.", a:"A list of skills, qualifications and attributes required for a job.", difficulty:"Medium"},
    {q:"What is 'equal opportunities' at work?", a:"Fair treatment of employees regardless of age, gender, disability, etc.", difficulty:"Easy"},
    {q:"Name two flexible working types.", a:"Part-time and remote (work from home).", difficulty:"Easy"},
    {q:"What are soft skills? Examples.", a:"Interpersonal skills like communication, teamwork and problem solving.", difficulty:"Easy"},
    {q:"How do trade unions help workers?", a:"Negotiate pay/conditions and represent members in disputes.", difficulty:"Medium"},
    {q:"What is employee onboarding?", a:"Process to integrate new employees into a company and role.", difficulty:"Easy"},
    {q:"Define 'gig economy'.", a:"Market where short-term, freelance, or contract jobs are common.", difficulty:"Medium"},
    {q:"What is workplace health & safety?", a:"Practices and laws to reduce risk of injury and illness at work.", difficulty:"Easy"},
    {q:"Why tailor a CV?", a:"To match the job requirements and increase interview chances.", difficulty:"Medium"},
    {q:"Explain 'apprenticeship'.", a:"Combination of paid work and training to develop job skills.", difficulty:"Easy"},
    {q:"What is 'employer branding'?", a:"Company's reputation as an employer used to attract staff.", difficulty:"Medium"},
    {q:"Two recruitment methods employers use?", a:"Online job listings and recruitment agencies.", difficulty:"Easy"},
    {q:"Benefit of workplace diversity?", a:"Broader ideas, creativity and improved problem solving.", difficulty:"Medium"},
    {q:"What is a performance appraisal?", a:"Review of an employee’s work to set objectives and give feedback.", difficulty:"Medium"},
    {q:"Difference: résumé vs CV?", a:"Résumé is short and tailored; CV is more detailed and comprehensive.", difficulty:"Medium"},
    {q:"Name one legal employee right in Ireland.", a:"Entitlement to minimum wage or paid holiday (subject to law).", difficulty:"Easy"},
    {q:"What is networking?", a:"Building professional relationships that can lead to opportunities.", difficulty:"Easy"},
    {q:"Explain work-life balance.", a:"Managing work demands and personal life to avoid burnout.", difficulty:"Easy"},
    {q:"What is redundancy?", a:"Job loss due to position being eliminated or company restructuring.", difficulty:"Medium"},
    {q:"How to improve employability?", a:"Gain qualifications, experience and transferable skills.", difficulty:"Easy"},
    {q:"What are transferable skills?", a:"Skills useful across jobs, e.g., communication or IT skills.", difficulty:"Easy"},
    {q:"Define 'internship'.", a:"Short placement to gain work experience, often linked to study.", difficulty:"Easy"},
    {q:"What is constructive dismissal?", a:"When employer behaviour forces an employee to resign (legally complex).", difficulty:"Hard"},
    {q:"Social media's effect on job search?", a:"Employers may screen candidates; profile can enhance visibility.", difficulty:"Medium"},
    {q:"Purpose of a covering letter?", a:"Explain why you're applying and highlight relevant skills.", difficulty:"Easy"},
    {q:"One trend changing work today?", a:"Remote working and automation shaping job roles.", difficulty:"Medium"},
    {q:"What is upskilling?", a:"Learning new skills to stay relevant in the job market.", difficulty:"Easy"},
    {q:"Why are references important?", a:"They validate past performance for prospective employers.", difficulty:"Easy"}
  ],

  "Digital Tech - Chapter 16": [
    {q:"What is digital transformation?", a:"Using digital tech to improve processes, services or customer experience.", difficulty:"Medium"},
    {q:"Define cloud computing.", a:"Accessing storage and computing power over the internet (online servers).", difficulty:"Easy"},
    {q:"What does ICT stand for?", a:"Information and Communications Technology used to manage data and communication.", difficulty:"Easy"},
    {q:"Advantage of MIS?", a:"Better management decisions through timely information.", difficulty:"Medium"},
    {q:"What is cybersecurity?", a:"Protecting systems and data from digital attacks and unauthorised access.", difficulty:"Easy"},
    {q:"Define e-commerce.", a:"Buying and selling goods/services online.", difficulty:"Easy"},
    {q:"Why is data privacy important?", a:"To respect rights and comply with laws (e.g., GDPR).", difficulty:"Medium"},
    {q:"Give a productivity tool example.", a:"Spreadsheets like Excel or collaboration apps like Teams.", difficulty:"Easy"},
    {q:"What is an ERP system?", a:"Enterprise Resource Planning integrates core business functions.", difficulty:"Hard"},
    {q:"Explain mobile-first design.", a:"Designing primarily for mobile users to ensure good UX on small screens.", difficulty:"Medium"},
    {q:"Define 'big data'.", a:"Large complex datasets analysed for insights and trends.", difficulty:"Hard"},
    {q:"How does automation affect jobs?", a:"Reduces manual tasks but may change required skills.", difficulty:"Medium"},
    {q:"What is an API?", a:"A set of rules allowing different software to communicate.", difficulty:"Medium"},
    {q:"Example of digital marketing.", a:"Using social media ads to target customers.", difficulty:"Easy"},
    {q:"What is phishing?", a:"Fraudulent messages seeking sensitive information.", difficulty:"Easy"},
    {q:"Why back up data?", a:"To prevent permanent loss from failure or attack.", difficulty:"Easy"},
    {q:"Explain IoT briefly.", a:"Connected devices that share data over networks.", difficulty:"Medium"},
    {q:"What is responsive design?", a:"Design that adapts to different screen sizes for usability.", difficulty:"Easy"},
    {q:"Role of analytics in e-commerce?", a:"Track behaviour and optimise conversions and sales.", difficulty:"Medium"},
    {q:"Define two-factor authentication.", a:"Security using two proofs of identity (password + code).", difficulty:"Easy"},
    {q:"What is open-source software?", a:"Software whose source code is freely available to use and modify.", difficulty:"Medium"},
    {q:"How can SMEs benefit from digital tools?", a:"Improve reach, reduce costs and automate tasks.", difficulty:"Easy"},
    {q:"What is virtual collaboration?", a:"Remote teamwork using video, chat and shared docs.", difficulty:"Easy"},
    {q:"Explain bandwidth simply.", a:"Internet capacity; higher bandwidth allows faster data transfer.", difficulty:"Easy"},
    {q:"What is encryption?", a:"Encoding data to prevent unauthorised access.", difficulty:"Medium"},
    {q:"Why is UX important?", a:"Good UX increases satisfaction and conversion rates.", difficulty:"Medium"},
    {q:"What is blockchain (short)?", a:"Distributed ledger keeping secure records across many nodes.", difficulty:"Hard"},
    {q:"One legal issue collecting customer data?", a:"Ensuring consent and GDPR compliance.", difficulty:"Medium"},
    {q:"What is a CMS?", a:"Content Management System for creating and managing websites.", difficulty:"Easy"}
  ],

  "Planning a Business - Chapter 17": [
    {q:"What is a business plan?", a:"A document outlining objectives, strategy and financial forecasts for a business.", difficulty:"Easy"},
    {q:"Name three business plan components.", a:"Executive summary, market analysis and financial projections.", difficulty:"Easy"},
    {q:"What is a SWOT analysis?", a:"Assessment of Strengths, Weaknesses, Opportunities and Threats.", difficulty:"Easy"},
    {q:"Why do market research?", a:"To understand customer needs and competition and reduce risk.", difficulty:"Medium"},
    {q:"Define target market.", a:"A specific group of customers a business aims to serve.", difficulty:"Easy"},
    {q:"Example of a revenue stream.", a:"Product sales, subscriptions or service fees.", difficulty:"Easy"},
    {q:"What is a break-even point?", a:"When total revenue equals total costs; no profit or loss.", difficulty:"Medium"},
    {q:"Fixed vs variable costs — difference?", a:"Fixed costs don't change with output; variable costs do.", difficulty:"Easy"},
    {q:"Purpose of cash flow forecasting?", a:"Predict inflows/outflows to ensure business can meet obligations.", difficulty:"Medium"},
    {q:"What is a USP?", a:"Unique Selling Proposition that differentiates a product/service.", difficulty:"Medium"},
    {q:"Why set SMART objectives?", a:"To ensure goals are clear and measurable (Specific, Measurable, Achievable, Relevant, Time-bound).", difficulty:"Easy"},
    {q:"What is market segmentation?", a:"Dividing market into groups with similar needs or behaviours.", difficulty:"Medium"},
    {q:"Explain market positioning.", a:"How a product is viewed relative to competitors by customers.", difficulty:"Medium"},
    {q:"Why is pricing strategy important?", a:"It influences demand, revenue and competitive positioning.", difficulty:"Medium"},
    {q:"Two PEST factors?", a:"Political and Economic (also Social, Technological).", difficulty:"Easy"},
    {q:"Define scalability.", a:"Ability to grow without proportional cost increases.", difficulty:"Medium"},
    {q:"Why have an exit strategy?", a:"To plan how owners will realise value in future (sell or transfer).", difficulty:"Hard"},
    {q:"What is market share?", a:"Proportion of total sales in market captured by a business.", difficulty:"Easy"},
    {q:"What is bootstrapping?", a:"Starting and growing using limited personal funds.", difficulty:"Medium"},
    {q:"Why forecast finances 3–5 years?", a:"To show viability and plan for growth and investment needs.", difficulty:"Medium"},
    {q:"Define competitive advantage.", a:"Attributes that allow a business to outperform rivals.", difficulty:"Medium"},
    {q:"Explain operational plan.", a:"Detailed plan of processes, resources and timelines to run the business.", difficulty:"Medium"},
    {q:"Market penetration strategy meaning?", a:"Increasing sales of existing products in existing markets.", difficulty:"Medium"},
    {q:"Role of branding?", a:"Creates recognition, trust and differentiation.", difficulty:"Easy"},
    {q:"What is a feasibility study?", a:"Testing if a business idea is practical and worthwhile.", difficulty:"Medium"},
    {q:"Why include contingency plans?", a:"To prepare for unexpected events and reduce risk.", difficulty:"Medium"},
    {q:"Describe customer persona.", a:"Detailed representation of a typical target customer.", difficulty:"Medium"},
    {q:"What is a distribution strategy?", a:"How a product reaches customers (online, retail, wholesalers).", difficulty:"Medium"},
    {q:"Why keep cash reserves?", a:"To cover unexpected costs and maintain liquidity.", difficulty:"Easy"}
  ],

  "Business Finance - Chapter 18": [
    {q:"Purpose of a cash flow statement?", a:"Shows cash inflows and outflows over a period to monitor liquidity.", difficulty:"Easy"},
    {q:"Define capital.", a:"Money or assets used to start and run a business.", difficulty:"Easy"},
    {q:"Debt vs equity finance — difference?", a:"Debt must be repaid with interest; equity gives ownership without fixed repayment.", difficulty:"Medium"},
    {q:"What is an overdraft?", a:"Short-term bank borrowing allowing account to go negative within limit.", difficulty:"Medium"},
    {q:"What is working capital management?", a:"Managing current assets and liabilities to ensure liquidity.", difficulty:"Medium"},
    {q:"Advantage of leasing equipment?", a:"Lower upfront cost and easier upgrades than buying.", difficulty:"Medium"},
    {q:"Define ROI.", a:"Return on investment = (gain − cost) ÷ cost.", difficulty:"Medium"},
    {q:"What is loan amortisation?", a:"Repayment schedule splitting principal and interest over time.", difficulty:"Hard"},
    {q:"Why is credit rating important?", a:"Affects borrowing ability and interest rates offered.", difficulty:"Medium"},
    {q:"What are business angels?", a:"Investors who provide capital and often expertise for equity.", difficulty:"Medium"},
    {q:"Define gross margin.", a:"Gross profit as a percentage of sales.", difficulty:"Medium"},
    {q:"Purpose of budgeting?", a:"Plan expected income/expenditure to control finances.", difficulty:"Easy"},
    {q:"What is capital budgeting?", a:"Evaluating long-term investments using methods like NPV or payback.", difficulty:"Hard"},
    {q:"Define trade credit.", a:"Suppliers allowing delayed payment as short-term finance.", difficulty:"Easy"},
    {q:"Why keep cash reserves?", a:"To meet unexpected payments and reduce insolvency risk.", difficulty:"Easy"},
    {q:"Liquidity vs solvency?", a:"Liquidity is short-term payment ability; solvency is long-term debt viability.", difficulty:"Medium"},
    {q:"What is invoice factoring?", a:"Selling invoices to a third party for immediate cash minus fee.", difficulty:"Hard"},
    {q:"Interest rates effect on investment?", a:"Higher rates raise borrowing costs and can reduce investment.", difficulty:"Medium"},
    {q:"Use of retained earnings?", a:"Reinvesting profits into business or paying debt.", difficulty:"Easy"},
    {q:"What is COGS?", a:"Direct costs of producing goods sold by a company.", difficulty:"Easy"},
    {q:"What is variance analysis?", a:"Comparing actual results to budget and explaining differences.", difficulty:"Medium"},
    {q:"Why diversify funding sources?", a:"Reduce reliance on one source and lower financial risk.", difficulty:"Medium"},
    {q:"What is equity dilution?", a:"Reducing ownership percentage when new shares are issued.", difficulty:"Medium"},
    {q:"Define NPV briefly.", a:"Net present value of future cash flows discounted to present.", difficulty:"Hard"},
    {q:"What is cost of capital?", a:"Required return for an investment, weighted across debt & equity.", difficulty:"Hard"},
    {q:"How do taxes affect finance decisions?", a:"They change cash flows, returns and structure choices.", difficulty:"Medium"},
    {q:"Budgetary control meaning?", a:"Monitoring performance against budget and correcting variances.", difficulty:"Medium"},
    {q:"Define insolvency.", a:"Unable to pay debts when due or liabilities exceed assets.", difficulty:"Hard"},
    {q:"Why issue bonds instead of shares?", a:"Raise funds without losing ownership, but it creates debt obligations.", difficulty:"Medium"},
    {q:"What is the working capital cycle?", a:"Time to convert net current assets into cash (inventory → sales → receivables → cash).", difficulty:"Medium"}
  ],

  "Business Documents - Chapter 19": [
    {q:"What is an invoice?", a:"A document requesting payment with seller, buyer, date, items and amounts.", difficulty:"Easy"},
    {q:"Define delivery note.", a:"Document confirming goods delivered, often signed by the receiver.", difficulty:"Easy"},
    {q:"What is remittance advice?", a:"Notification from buyer that payment has been made for invoices.", difficulty:"Medium"},
    {q:"What is a purchase order (PO)?", a:"Buyer's formal order listing quantities, prices and delivery terms.", difficulty:"Easy"},
    {q:"Why keep accurate business records?", a:"For legal compliance, control and informed decisions.", difficulty:"Easy"},
    {q:"What is a credit note?", a:"Issued to reduce amount due when goods are returned or overcharged.", difficulty:"Medium"},
    {q:"What is a receipt?", a:"Proof that payment has been received by the seller.", difficulty:"Easy"},
    {q:"Explain statement of account.", a:"Periodic summary of transactions between buyer and seller showing balance.", difficulty:"Medium"},
    {q:"Role of VAT invoices in Ireland?", a:"Record VAT charged and needed for VAT returns and input credit.", difficulty:"Medium"},
    {q:"Example of internal document.", a:"Timesheet, expense claim or internal memo.", difficulty:"Easy"},
    {q:"What is credit control?", a:"Procedures to ensure customers pay on time (reminders, collections).", difficulty:"Medium"},
    {q:"Why use delivery notes for returns?", a:"They verify delivered items when processing returns.", difficulty:"Easy"},
    {q:"Define proforma invoice.", a:"Preliminary invoice providing details before sale or shipment.", difficulty:"Medium"},
    {q:"Ledger vs journal — difference?", a:"Journal records transactions chronologically; ledger organises by account.", difficulty:"Medium"},
    {q:"What is order acknowledgement?", a:"Seller confirms receipt and acceptance of a buyer's order.", difficulty:"Easy"},
    {q:"Why use standardised templates?", a:"Consistency, brand professionalism and easier record keeping.", difficulty:"Easy"},
    {q:"What are terms & conditions on invoices?", a:"Rules covering payment, delivery and liabilities.", difficulty:"Medium"},
    {q:"Handling confidential documents?", a:"Store securely, limit access and dispose safely.", difficulty:"Medium"},
    {q:"What is a packing list?", a:"List of items in a shipment to assist receiving.", difficulty:"Easy"},
    {q:"What details does a payslip include?", a:"Employee name, gross pay, deductions, net pay and pay period.", difficulty:"Easy"},
    {q:"Why keep digital backups?", a:"Protect against data loss and enable recovery.", difficulty:"Easy"},
    {q:"What is accounts receivable ledger?", a:"Record of amounts owed by each customer.", difficulty:"Medium"},
    {q:"Supporting documentation for expenses?", a:"Receipts and invoices that justify recorded expenses.", difficulty:"Medium"},
    {q:"Reason for version control?", a:"To track document updates and approved revisions.", difficulty:"Medium"},
    {q:"What is a statement of purpose in documents?", a:"Short explanation of the document's aim (e.g., proposal).", difficulty:"Medium"},
    {q:"How long keep financial records in Ireland?", a:"Typically around 6 years; check current legal requirements.", difficulty:"Hard"},
    {q:"Define audit trail.", a:"Record showing how financial figures and decisions were made.", difficulty:"Hard"},
    {q:"Why signatures matter on contracts?", a:"They indicate consent and help enforce agreements.", difficulty:"Easy"},
    {q:"Invoice vs receipt — difference?", a:"Invoice requests payment; receipt confirms payment received.", difficulty:"Easy"},
    {q:"Handling corrected documents?", a:"Amend clearly, date the change and keep originals for audit.", difficulty:"Medium"}
  ],

  "Payslips - Chapter 11": [
    {q:"What is a payslip?", a:"Document detailing an employee's earnings and deductions for a pay period.", difficulty:"Easy"},
    {q:"Define gross pay.", a:"Total earnings before deductions.", difficulty:"Easy"},
    {q:"Define net pay.", a:"Take-home pay after all deductions.", difficulty:"Easy"},
    {q:"Examples of statutory deductions in Ireland?", a:"PAYE, PRSI and USC.", difficulty:"Easy"},
    {q:"What is PAYE?", a:"Pay As You Earn — income tax deducted at source from wages.", difficulty:"Easy"},
    {q:"What is PRSI?", a:"Pay Related Social Insurance — contributions for social welfare benefits.", difficulty:"Easy"},
    {q:"What is USC?", a:"Universal Social Charge applied to gross income at set rates.", difficulty:"Medium"},
    {q:"What is a PPS number used for?", a:"Personal Public Service number for tax and social welfare identification.", difficulty:"Easy"},
    {q:"Explain tax credits briefly.", a:"Reductions that lower the amount of income tax payable.", difficulty:"Medium"},
    {q:"What is an employer contribution?", a:"Amounts the employer pays on top of employee pay (e.g., employer PRSI).", difficulty:"Medium"},
    {q:"Why show hours on a payslip?", a:"To verify pay calculations for hourly and overtime pay.", difficulty:"Easy"},
    {q:"How is overtime shown?", a:"As separate lines with additional rate or extra hours.", difficulty:"Medium"},
    {q:"Statutory leave effect on payslip?", a:"Paid leave included as earnings and affects gross pay.", difficulty:"Medium"},
    {q:"Records employers must keep about pay?", a:"Payroll records showing amounts, deductions and hours for audit.", difficulty:"Medium"},
    {q:"What is a pay period?", a:"Frequency employees are paid (weekly, fortnightly, monthly).", difficulty:"Easy"},
    {q:"Why include employer name/address on payslip?", a:"For identification and contact for queries.", difficulty:"Easy"},
    {q:"What is Year-to-Date (YTD)?", a:"Totals since the start of the tax year for earnings and deductions.", difficulty:"Medium"},
    {q:"How correct incorrect payslips?", a:"Issue revised payslip and adjust payroll; document the change.", difficulty:"Medium"},
    {q:"Minimum wage relevance on payslip?", a:"Payslip shows hourly rate to confirm compliance with minimum wage.", difficulty:"Easy"},
    {q:"Why show pension contributions separately?", a:"For clarity and because they may receive tax relief or employer match.", difficulty:"Medium"},
    {q:"Employer PRSI vs employee PRSI?", a:"Employer PRSI paid by employer; employee PRSI deducted from employee pay.", difficulty:"Medium"},
    {q:"Define taxable benefit with an example.", a:"Non-cash benefit subject to tax like a company car.", difficulty:"Medium"},
    {q:"How statutory redundancy shows on payslip?", a:"As separate payment with specific tax treatment depending on law.", difficulty:"Hard"},
    {q:"Why keep payslips confidential?", a:"To protect employees' personal financial information.", difficulty:"Easy"},
    {q:"What identifies an employee on payslip?", a:"Name, PPS number and employee ID.", difficulty:"Easy"},
    {q:"Net-to-gross calculation meaning?", a:"Estimating gross from net pay; complex due to tax bands.", difficulty:"Hard"},
    {q:"If tax code seems wrong, what to do?", a:"Contact employer payroll and Revenue to verify and correct.", difficulty:"Easy"},
    {q:"How often audit payslips internally?", a:"Regular checks each payroll and periodic audits for compliance.", difficulty:"Medium"},
    {q:"Why keep payslips for years?", a:"For tax records, proof of income and resolving disputes.", difficulty:"Medium"}
  ]
};

/* ============================
  State & persistence helpers
============================ */
const SECTION_KEYS = Object.keys(DATA);
const STORAGE_PREFIX = 'studyhub_v2_';
function progressKey(section){ return STORAGE_PREFIX + section.replace(/\s+/g,'_') + '_progress'; }
function orderKey(section){ return STORAGE_PREFIX + section.replace(/\s+/g,'_') + '_order'; }

function loadProgress(section){
  const raw = localStorage.getItem(progressKey(section));
  if(!raw){
    const init = DATA[section].map(()=>({known:false,revise:false,markedHard:false,seen:0}));
    localStorage.setItem(progressKey(section), JSON.stringify(init));
    return init;
  }
  try{ return JSON.parse(raw); } catch(e){
    const init = DATA[section].map(()=>({known:false,revise:false,markedHard:false,seen:0}));
    localStorage.setItem(progressKey(section), JSON.stringify(init));
    return init;
  }
}
function saveProgress(section, prog){ localStorage.setItem(progressKey(section), JSON.stringify(prog)); }

function loadOrder(section){
  const raw = localStorage.getItem(orderKey(section));
  if(raw) try{ const arr = JSON.parse(raw); if(Array.isArray(arr) && arr.length===DATA[section].length) return arr; } catch(e){}
  const base = DATA[section].map((_,i)=>i); localStorage.setItem(orderKey(section), JSON.stringify(base)); return base;
}
function saveOrder(section, order){ localStorage.setItem(orderKey(section), JSON.stringify(order)); }

/* ============================
  UI elements & state
============================ */
let currentSection = SECTION_KEYS[0];
let order = [];
let prog = [];
let index = 0;
let inLearnMode = false;
let learnRemaining = []; // indices remaining in learn mode

const elements = {
  sectionsList: document.getElementById('sectionsList'),
  sectionTitle: document.getElementById('sectionTitle'),
  sectionSubtitle: document.getElementById('sectionSubtitle'),
  questionText: document.getElementById('questionText'),
  answerText: document.getElementById('answerText'),
  answerReveal: document.getElementById('answerReveal'),
  difficultyBadge: document.getElementById('difficultyBadge'),
  cardIdx: document.getElementById('cardIdx'),
  prevBtn: document.getElementById('prevBtn'),
  nextBtn: document.getElementById('nextBtn'),
  showBtn: document.getElementById('showBtn'),
  knowBtn: document.getElementById('knowBtn'),
  reviseBtn: document.getElementById('reviseBtn'),
  markHardBtn: document.getElementById('markHardBtn'),
  randToggle: document.getElementById('randToggle'),
  modeSelect: document.getElementById('modeSelect'),
  difficultyFilter: document.getElementById('difficultyFilter'),
  shuffleBtn: document.getElementById('shuffleBtn'),
  progressBar: document.getElementById('progressBar'),
  progressPct: document.getElementById('progressPct'),
  knownCount: document.getElementById('knownCount'),
  reviseCount: document.getElementById('reviseCount'),
  listPanel: document.getElementById('listPanel'),
  printBtn: document.getElementById('printBtn'),
  resetSectionBtn: document.getElementById('resetSectionBtn'),
  resetAllBtn: document.getElementById('resetAllBtn'),
  exportBtn: document.getElementById('exportBtn'),
  learnModeBtn: document.getElementById('learnModeBtn'),
  learnContainer: document.getElementById('learnContainer'),
  learnArea: document.getElementById('learnArea'),
  endLearnBtn: document.getElementById('endLearnBtn')
};

function renderSections(){
  elements.sectionsList.innerHTML = '';
  SECTION_KEYS.forEach((s, i) => {
    const btn = document.createElement('button');
    btn.textContent = s;
    btn.className = (s===currentSection ? 'active' : '');
    btn.onclick = ()=>{ if(inLearnMode) endLearnMode(); selectSection(s); };
    elements.sectionsList.appendChild(btn);
  });
}

function selectSection(section){
  currentSection = section;
  order = loadOrder(section);
  prog = loadProgress(section);
  index = 0;
  updateSectionHeader();
  renderCard();
  renderListPanel();
  renderGlobalStats();
  // mark active
  Array.from(elements.sectionsList.children).forEach(b=>b.className = (b.textContent===section? 'active':'' ));
}

function updateSectionHeader(){
  elements.sectionTitle.textContent = currentSection;
  const total = DATA[currentSection].length;
  const known = prog.filter(p=>p.known).length;
  elements.sectionSubtitle.textContent = `${total} cards · Known: ${known}`;
}

function visibleOrder(){
  const diff = elements.difficultyFilter.value;
  const arr = order.filter(i=>{
    if(diff==='all') return true;
    return DATA[currentSection][i].difficulty===diff;
  });
  return arr;
}

function renderCard(){
  // if learn mode active, hide flashcard area and show learn area
  if(inLearnMode){
    elements.learnContainer.style.display = 'block';
    elements.learnArea.style.display = 'block';
    elements.learnArea.focus && elements.learnArea.focus();
    return;
  } else {
    elements.learnContainer.style.display = 'none';
  }

  const arr = visibleOrder();
  if(arr.length===0){
    elements.questionText.textContent = 'No cards match the filter.';
    elements.answerText.textContent = '';
    elements.answerReveal.style.display='none';
    elements.cardIdx.textContent = '0/0';
    elements.difficultyBadge.textContent = '';
    elements.progressBar.style.width='0%';
    elements.progressPct.textContent='0%';
    return;
  }
  if(index >= arr.length) index = 0;
  if(index < 0) index = arr.length - 1;
  const idx = arr[index];
  const card = DATA[currentSection][idx];
  elements.questionText.textContent = card.q;
  elements.answerText.textContent = card.a;
  elements.answerReveal.style.display = 'none';
  elements.cardIdx.textContent = (index+1) + '/' + arr.length;
  elements.difficultyBadge.textContent = card.difficulty;
  // update progress
  const total = DATA[currentSection].length;
  const known = prog.filter(p=>p.known).length;
  const revise = prog.filter(p=>p.revise).length;
  const pct = Math.round((known/total)*100);
  elements.progressBar.style.width = pct + '%';
  elements.progressPct.textContent = pct + '%';
  elements.knownCount.textContent = 'Known: ' + known;
  elements.reviseCount.textContent = 'To revise: ' + revise;
  elements.sectionSubtitle.textContent = `${total} cards · Known: ${known}`;
  // markHard button text
  const state = prog[idx].markedHard ? 'Unmark Hard' : 'Mark Hard';
  elements.markHardBtn.textContent = state;
}

/* Event handlers */
elements.showBtn.onclick = ()=>{ elements.answerReveal.style.display = 'block'; };
elements.nextBtn.onclick = ()=>{
  const arr = visibleOrder();
  index = (index+1) % arr.length;
  renderCard();
};
elements.prevBtn.onclick = ()=>{
  const arr = visibleOrder();
  index = (index-1 + arr.length) % arr.length;
  renderCard();
};
elements.knowBtn.onclick = ()=>{
  const arr = visibleOrder();
  const idx = arr[index];
  prog[idx].known = true;
  prog[idx].revise = false;
  prog[idx].seen++;
  saveProgress(currentSection, prog);
  renderCard();
  renderListPanel();
  renderGlobalStats();
};
elements.reviseBtn.onclick = ()=>{
  const arr = visibleOrder();
  const idx = arr[index];
  prog[idx].revise = true;
  prog[idx].known = false;
  prog[idx].seen++;
  saveProgress(currentSection, prog);
  renderCard();
  renderListPanel();
  renderGlobalStats();
};
elements.markHardBtn.onclick = ()=>{
  const arr = visibleOrder();
  const idx = arr[index];
  prog[idx].markedHard = !prog[idx].markedHard;
  saveProgress(currentSection, prog);
  renderCard();
  renderListPanel();
};

elements.shuffleBtn.onclick = ()=>{
  const ord = DATA[currentSection].map((_,i)=>i);
  for(let i=ord.length-1;i>0;i--){
    const j = Math.floor(Math.random()*(i+1));
    [ord[i], ord[j]]=[ord[j], ord[i]];
  }
  order = ord;
  saveOrder(currentSection, order);
  index = 0;
  renderCard();
  renderListPanel();
};

elements.resetSectionBtn.onclick = ()=>{
  if(!confirm('Reset progress for this section?')) return;
  prog = DATA[currentSection].map(()=>({known:false,revise:false,markedHard:false,seen:0}));
  saveProgress(currentSection, prog);
  order = DATA[currentSection].map((_,i)=>i);
  saveOrder(currentSection, order);
  index = 0;
  renderCard();
  renderListPanel();
  renderGlobalStats();
};

elements.resetAllBtn.onclick = ()=>{
  if(!confirm('Reset ALL progress for all sections?')) return;
  SECTION_KEYS.forEach(s=>{
    localStorage.removeItem(progressKey(s));
    localStorage.removeItem(orderKey(s));
  });
  selectSection(SECTION_KEYS[0]);
  renderGlobalStats();
};

elements.randToggle.onchange = ()=>{
  if(elements.randToggle.checked){
    const ord = DATA[currentSection].map((_,i)=>i);
    for(let i=ord.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [ord[i],ord[j]]=[ord[j],ord[i]]; }
    order = ord; saveOrder(currentSection, order); index=0; renderCard(); renderListPanel();
  } else { order = DATA[currentSection].map((_,i)=>i); saveOrder(currentSection, order); index=0; renderCard(); renderListPanel();}
};

elements.difficultyFilter.onchange = ()=>{ index = 0; renderCard(); };

elements.modeSelect.onchange = ()=>{
  if(elements.modeSelect.value === 'random'){
    const ord = DATA[currentSection].map((_,i)=>i);
    for(let i=ord.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [ord[i],ord[j]]=[ord[j],ord[i]]; }
    order = ord; saveOrder(currentSection, order); index=0; renderCard();
  } else if(elements.modeSelect.value === 'study'){
    const unknowns = []; const knowns = [];
    for(let i=0;i<DATA[currentSection].length;i++){
      if(prog[i] && prog[i].known) knowns.push(i); else unknowns.push(i);
    }
    order = unknowns.concat(knowns); saveOrder(currentSection, order); index=0; renderCard();
  } else {
    order = DATA[currentSection].map((_,i)=>i); saveOrder(currentSection, order); index=0; renderCard();
  }
};

elements.printBtn.onclick = ()=>{
  const name = currentSection;
  let html = `<html><head><title>Print - ${name}</title><style>body{font-family:Arial;padding:20px}</style></head><body><h1>${name} — Flashcards</h1>`;
  DATA[currentSection].forEach((c,i)=>{
    html += `<div style="margin-bottom:10px"><strong>Q${i+1}:</strong> ${c.q}<br><strong>A:</strong> ${c.a}</div>`;
  });
  html += '</body></html>';
  const w = window.open('','_blank');
  w.document.write(html); w.document.close(); w.print();
};

elements.exportBtn.onclick = ()=>{
  const exportData = {};
  SECTION_KEYS.forEach(s=>{
    exportData[s] = {
      data: DATA[s],
      progress: loadProgress(s)
    };
  });
  const blob = new Blob([JSON.stringify(exportData, null, 2)], {type:'application/json'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href=url; a.download='studyhub_progress.json'; a.click(); URL.revokeObjectURL(url);
};

/* List panel shows mini list and per-card info */
function renderListPanel(){
  const arr = DATA[currentSection];
  const nodes = arr.map((c,i)=>{
    const p = prog[i] || {known:false,revise:false,markedHard:false,seen:0};
    return `<div class="list-card" style="${p.known? 'border-left:4px solid var(--good)': p.revise? 'border-left:4px solid var(--bad)':'' }">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <div style="font-weight:600">${'Q'+(i+1)} — ${c.q}</div>
        <div style="text-align:right">
          <div style="font-size:12px;color:var(--muted)">Seen: ${p.seen}</div>
          <div style="font-size:12px">${p.markedHard? '<span style=\"color:#b91c1c\">Hard</span>':''}</div>
        </div>
      </div>
    </div>`;
  }).join('');
  elements.listPanel.innerHTML = `<div style="max-height:240px;overflow:auto">${nodes}</div>`;
}

/* Global stats */
function renderGlobalStats(){
  let total=0, known=0;
  SECTION_KEYS.forEach(s=>{
    const progS = loadProgress(s);
    total += progS.length;
    known += progS.filter(p=>p.known).length;
  });
  elements.globalStats.textContent = `Total cards: ${total} · Known: ${known} · Mastery: ${Math.round((known/total)*100)}%`;
}

/* ============================
  Learn Mode (Quizlet-like multiple choice)
  - Uses DATA[currentSection]
  - Repeats incorrect cards until all are correct
============================ */

function startLearnMode(){
  if(inLearnMode) return;
  inLearnMode = true;
  elements.learnContainer.style.display = 'block';
  elements.learnArea.innerHTML = '';
  learnRemaining = DATA[currentSection].map((_,i)=>i);
  // small shuffle
  for(let i=learnRemaining.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [learnRemaining[i],learnRemaining[j]]=[learnRemaining[j],learnRemaining[i]]; }
  renderNextLearnCard();
}

function endLearnMode(){
  inLearnMode = false;
  elements.learnContainer.style.display = 'none';
  elements.learnArea.innerHTML = '';
  renderCard();
}

elements.learnModeBtn.onclick = ()=>{ startLearnMode(); };
elements.endLearnBtn.onclick = ()=>{ if(confirm('Exit learn mode?')) endLearnMode(); };

function renderNextLearnCard(){
  if(!inLearnMode) return;
  const area = elements.learnArea;
  area.innerHTML = '';
  if(learnRemaining.length === 0){
    area.innerHTML = '<div style="padding:12px">🎉 Great job — you completed Learn Mode for this section!</div>';
    return;
  }
  // pick a random remaining index
  const pickIndex = Math.floor(Math.random()*learnRemaining.length);
  const cardIdx = learnRemaining[pickIndex];
  const card = DATA[currentSection][cardIdx];

  // Build options: correct answer + 3 distractors from same section (unique)
  const answers = new Set([card.a]);
  const distractors = [];
  const pool = DATA[currentSection].map(c=>c.a).filter(a=>a!==card.a);
  while(answers.size < 4 && pool.length){
    const cand = pool.splice(Math.floor(Math.random()*pool.length),1)[0];
    answers.add(cand);
  }
  // if still less than 4 (section short), duplicate won't happen because sections have 30
  const opts = Array.from(answers).sort(()=>Math.random()-0.5);

  const qDiv = document.createElement('div');
  qDiv.innerHTML = `<div style="font-weight:600;margin-bottom:8px">${card.q}</div>`;
  opts.forEach(opt=>{
    const btn = document.createElement('button');
    btn.className = 'mc-option';
    btn.innerText = opt;
    btn.onclick = () => {
      handleLearnAnswer(pickIndex, cardIdx, opt, btn);
    };
    qDiv.appendChild(btn);
  });
  // progress display
  const progDiv = document.createElement('div');
  progDiv.style.marginTop = '10px';
  const done = DATA[currentSection].length - learnRemaining.length;
  progDiv.innerHTML = `<small style="color:var(--muted)">${done} / ${DATA[currentSection].length} completed</small>`;
  area.appendChild(qDiv);
  area.appendChild(progDiv);
}

function handleLearnAnswer(pickPos, cardIdx, selected, btnElement){
  const correct = DATA[currentSection][cardIdx].a;
  // visually show result
  const options = Array.from(document.querySelectorAll('.mc-option'));
  options.forEach(o=>o.disabled = true);
  if(selected === correct){
    btnElement.classList.add('correct');
    // remove this card from remaining
    learnRemaining.splice(pickPos,1);
    // update progress markers optionally
    prog[cardIdx].seen = (prog[cardIdx].seen || 0) + 1;
    prog[cardIdx].known = true;
    prog[cardIdx].revise = false;
    saveProgress(currentSection, prog);
    setTimeout(()=>{ renderNextLearnCard(); renderListPanel(); renderGlobalStats(); }, 700);
  } else {
    btnElement.classList.add('wrong');
    // keep card in remaining and mark revise
    prog[cardIdx].seen = (prog[cardIdx].seen || 0) + 1;
    prog[cardIdx].revise = true;
    prog[cardIdx].known = false;
    saveProgress(currentSection, prog);
    // highlight correct option
    setTimeout(()=> {
      const opts = Array.from(document.querySelectorAll('.mc-option'));
      opts.forEach(o => { if(o.innerText === correct) o.classList.add('correct'); });
    }, 300);
    // then move on but keep the card in the remaining list
    setTimeout(()=>{ renderNextLearnCard(); renderListPanel(); renderGlobalStats(); }, 1100);
  }
}

/* ============================
  Init UI
============================ */
function init(){
  // ensure progress & order exist for every section
  SECTION_KEYS.forEach(s=>{
    loadProgress(s);
    loadOrder(s);
  });
  renderSections();
  selectSection(currentSection);
  renderGlobalStats();
}
init();

/* Save on unload */
window.addEventListener('beforeunload', ()=>{ saveOrder(currentSection, order); saveProgress(currentSection, prog); });

</script>
</body>
</html>
