<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>StudyHub – Business Studies</title>
<style>
  body { font-family: Arial, sans-serif; background: #fdf6f9; color: #374151; margin: 0; padding: 20px; }
  .container { max-width: 1000px; margin: auto; }
  .section { background: white; padding: 15px; border-radius: 10px; margin-bottom: 15px; box-shadow: 0 3px 8px rgba(0,0,0,0.05); }
  textarea { width: 100%; padding: 10px; border-radius: 6px; border: 1px solid #ddd; background: #f8f8ff; }
  button { padding: 8px 14px; border: none; border-radius: 6px; cursor: pointer; font-size: 14px; margin: 4px; }
  .btn-study { background: #c3e8f2; } /* pastel blue */
  .btn-learn { background: #ffd9e8; } /* pastel pink */
  .btn-next { background: #c2fbd7; } /* pastel mint */
  button:hover { opacity: 0.8; }
</style>
</head>
<body>
<div class="container">
  <h1>📚 StudyHub – Business Studies (Junior Cert)</h1>
  <p>Choose a chapter below to review notes or test yourself with flashcards.</p>

  <!-- NOTES SECTIONS -->
  <div class="section">
    <h2>Chapter 4 – Recording Actual Income & Expenditure</h2>
    <textarea id="ch4Notes" rows="5" oninput="saveNotes('ch4Notes')"></textarea>
    <button class="btn-study" onclick="startFlashcards('ch4')">Study Flashcards</button>
    <button class="btn-learn" onclick="startLearnMode('ch4')">Learn Mode</button>
  </div>

  <div class="section">
    <h2>Chapter 18 – Business Finance</h2>
    <textarea id="ch18Notes" rows="5" oninput="saveNotes('ch18Notes')"></textarea>
    <button class="btn-study" onclick="startFlashcards('ch18')">Study Flashcards</button>
    <button class="btn-learn" onclick="startLearnMode('ch18')">Learn Mode</button>
  </div>

  <div class="section">
    <h2>Chapter 19 – Business Documents</h2>
    <textarea id="ch19Notes" rows="5" oninput="saveNotes('ch19Notes')"></textarea>
    <button class="btn-study" onclick="startFlashcards('ch19')">Study Flashcards</button>
    <button class="btn-learn" onclick="startLearnMode('ch19')">Learn Mode</button>
  </div>

  <div id="flashcardArea" class="section"></div>
</div>

<script>
// NOTES STORAGE
function saveNotes(id){ localStorage.setItem(id, document.getElementById(id).value); }
function loadNotes(){ ['ch4Notes','ch18Notes','ch19Notes'].forEach(id=>{
  document.getElementById(id).value = localStorage.getItem(id) || '';
}); }
window.onload = loadNotes;

// FLASHCARDS DATA
const flashcards = { 
  ch4: [
    {q: "What is a budget?", a: "A plan of future income and spending", opts:["A record of past expenses","A plan of future income and spending","A loan arrangement","A type of tax"]},
    {q: "Fixed expenditure is:", a: "Unchanging regular costs", opts:["Unplanned once-off cost","Changing weekly costs","Unchanging regular costs","Money received"]},
    {q: "Irregular expenditure refers to:", a: "Expected but not regular payments", opts:["Unexpected emergencies","Expected but not regular payments","Weekly bills","Income tax"]},
    {q: "What is discretionary spending?", a: "Non-essential expenses", opts:["Mortgage","Rent","Non-essential expenses","Insurance"]},
    {q: "Overspending occurs when:", a: "Actual > planned spending", opts:["Planned > actual spending","Actual > planned spending","Income reduces","Savings increase"]},
    {q: "Opportunity cost means:", a: "Next best alternative foregone", opts:["What you gain","What friends choose","Money saved","Next best alternative foregone"]},
    {q: "What is income?", a: "Money received", opts:["Money spent","Money received","A loan","A tax rate"]},
    {q: "Financial record is:", a: "A written record of transactions", opts:["Budget only","Written record of transactions","An invoice","The cash flow"]},
    {q: "What is a cash flow problem?", a: "Not enough cash to pay expenses", opts:["Too much profit","High income","Not enough cash to pay expenses","Incorrect budgeting"]},
    {q: "What is gross income?", a: "Income before deductions", opts:["Income after deductions","Income before deductions","Extra earnings","Net tax"]},
    {q: "Net income is:", a: "Take-home pay after deductions", opts:["Income before tax","Business profit","Take-home pay after deductions","Bonus payment"]},
    {q: "Capital expenditure refers to:", a: "Long-term investment items", opts:["Daily supplies","Long-term investment items","Loan repayments","Salaries"]},
    {q: "Current expenditure:", a: "Day-to-day spending", opts:["Investment","Day-to-day spending","Tax refunds","Interest earned"]},
    {q: "What is a household budget?", a: "Plan for spending and income", opts:["Loan plan","Tax statement","Plan for spending and income","Receipt tracker"]},
    {q: "A surplus in budgeting means:", a: "Income > expenditure", opts:["Expenditure > income","Income > expenditure","No money left","Loan required"]},
    {q: "Deficit occurs when:", a: "Spending exceeds income", opts:["Income is stable","Saving increases","Spending exceeds income","Budget is balanced"]},
    {q: "What is a need?", a: "Essential for survival", opts:["Luxury purchases","Essential for survival","Non-essential","Optional extra"]},
    {q: "Want is:", a: "Non-essential desire", opts:["Tax rate","Essential expense","Non-essential desire","Fixed cost"]},
    {q: "What is credit?", a: "Buying now, paying later", opts:["Pay now","Pay monthly bill","Buying now, paying later","No payment needed"]},
    {q: "What is debt?", a: "Money owed", opts:["Money earned","Money owed","Loan approval","Extra savings"]},
    {q: "Why is budgeting important?", a: "Helps avoid overspending", opts:["To increase debt","To ignore expenses","Helps avoid overspending","For higher taxes"]},
    {q: "Balanced budget means:", a: "Income equals expenditure", opts:["Income > expenditure","Income equals expenditure","Income < expenditure","No spending planned"]},
    {q: "Income can come from:", a: "Wages, pensions, benefits", opts:["Only wages","Only business","Wages, pensions, benefits","Sales only"]},
    {q: "Savings are:", a: "Money set aside", opts:["Deduction","Tax refund","Money set aside","Debt repayment"]},
    {q: "What causes overspending?", a: "Poor budgeting", opts:["High salary","Poor budgeting","Low taxes","Extra savings"]},
    {q: "A financial goal is:", a: "A target of what to save or buy", opts:["Emergency cost","A target of what to save or buy","Fixed expense","Loan amount"]},
    {q: "A receipt records:", a: "Proof of payment", opts:["Proof of debt","Loan terms","Proof of payment","Income tax"]},
    {q: "What is cash flow?", a: "Movement of money in/out", opts:["Money saved","Bonus earned","Movement of money in/out","Only business transactions"]},
    {q: "What are deductions?", a: "Money taken from gross income", opts:["Extra income","Bonus payments","Money taken from gross income","Bank charges"]},
    {q: "Why keep financial records?", a: "To track and plan finances", opts:["Increase debt","Avoid saving","To track and plan finances","Ignore bills"]}
  ],
  ch18: [
    {q: "What is working capital?", a: "Current assets minus current liabilities", opts:["Loan amount","Profit minus tax","Current assets minus current liabilities","Long-term investment"]},
    {q: "Long-term finance lasts for:", a: "More than 5 years", opts:["Less than 1 year","1–5 years","More than 5 years","Daily costs"]},
    {q: "Short-term finance is used for:", a: "Everyday expenses", opts:["Buying buildings","Everyday expenses","Machinery","Factory upgrades"]},
    {q: "What is a grant?", a: "Money given that doesn’t need to be repaid", opts:["Bank loan","Money given that doesn’t need to be repaid","Overdraft","Business tax"]},
    {q: "Retained earnings are:", a: "Profits kept in the business", opts:["Loans","Profits kept in the business","Share capital","Donations"]},
    {q: "What is equity capital?", a: "Money from owner/investors", opts:["Loan","Money from owner/investors","Government funding","VAT"]},
    {q: "Debt capital must be:", a: "Repaid with interest", opts:["Given away","Repaid with interest","Taxed","Ignored"]},
    {q: "What is liquidity?", a: "Ability to pay debts on time", opts:["Profit level","Total sales","Ability to pay debts on time","Share value"]},
    {q: "A cash flow forecast predicts:", a: "Future income & expenditure", opts:["Past debt","Employee salaries","Future income & expenditure","Investment risk"]},
    {q: "Overdraft is:", a: "Short-term bank finance", opts:["Long-term loan","Short-term bank finance","Grant","Sales revenue"]},
    {q: "A lease allows:", a: "Use of asset without buying it", opts:["Immediate ownership","Use of asset without buying it","Direct purchase","Currency exchange"]},
    {q: "Trade credit means:", a: "Buy now, pay later", opts:["Pay now","Cash only","Buy now, pay later","Prepaid contract"]},
    {q: "Profit is:", a: "Revenue minus expenses", opts:["Income only","Revenue minus expenses","Loan amount","VAT added"]},
    {q: "What is collateral?", a: "Security for a loan", opts:["Borrowed cash","Security for a loan","Sales revenue","Tax deduction"]},
    {q: "Medium-term loan duration:", a: "1–5 years", opts:["<1 year","1–5 years","5+ years","Daily"]},
    {q: "What is venture capital?", a: "Investment from entrepreneurs", opts:["Government grant","Investment from entrepreneurs","Bank loan","Tax refund"]},
    {q: "Gross profit is:", a: "Sales – cost of goods sold", opts:["Sales – expenses","Sales – tax","Sales – cost of goods sold","Sales – loans"]},
    {q: "Net profit:", a: "Gross profit – expenses", opts:["Gross profit only","Loan payments","Employee wages","Gross profit – expenses"]},
    {q: "Fixed capital is used for:", a: "Long-term assets", opts:["Daily expenses","Long-term assets","Travel costs","Savings"]},
    {q: "What is factoring?", a: "Selling debts for cash", opts:["Buying stock","Hiring staff","Selling debts for cash","Issuing shares"]},
    {q: "What is a loan?", a: "Borrowed money to be repaid", opts:["Gift","Borrowed money to be repaid","Profit","Tax rebate"]},
    {q: "What is solvency?", a: "Ability to meet long-term debts", opts:["Short-term cash issues","Ability to meet long-term debts","Low income","Tax liability"]},
    {q: "Why is budgeting important?", a: "Helps plan financial goals", opts:["Increase spending","Borrow more","Helps plan financial goals","Ignore profit"]},
    {q: "What is a mortgage?", a: "Loan to purchase property", opts:["Overdraft","Loan to purchase property","Short-term trade credit","Grant"]},
    {q: "Capital expenditure is spent on:", a: "Long-term items", opts:["Daily bills","Employee wages","Long-term items","Marketing only"]},
    {q: "Current assets include:", a: "Cash and stock", opts:["Machinery","Cash and stock","Buildings","Patent"]},
    {q: "Current liabilities include:", a: "Money owed within 12 months", opts:["Rent","Bank loans > 5 years","Money owed within 12 months","Share capital"]},
    {q: "Why use a grant?", a: "No repayment needed", opts:["High interest","No repayment needed","Short term","For salaries"]},
    {q: "Retained profits are good because:", a: "No debt is created", opts:["Interest required","No debt is created","High risk","Tax refund"]},
    {q: "Who provides venture capital?", a: "Investors taking risk", opts:["Suppliers","Investors taking risk","Employees","Government"]}
  ],
  ch19: [
    {q: "What is a letter of enquiry?", a: "A request for information and prices", opts:["A receipt","A request for information and prices","A bill","Payment confirmation"]},
    {q: "What is a quotation?", a: "Details of terms and prices offered", opts:["Final invoice","Employee contract","Details of terms and prices offered","Receipt of payment"]},
    {q: "COD means:", a: "Cash on delivery", opts:["Care of department","Cash on deposit","Cash on delivery","Confirmed order docket"]},
    {q: "CWO means:", a: "Cash with order", opts:["Cash when overdue","Credit with obligation","Cash with order","Cash without ownership"]},
    {q: "What are terms of sale?", a: "Payment and delivery conditions", opts:["VAT details","Contract terms","Payment and delivery conditions","Tax report"]},
    {q: "Purpose of a delivery docket:", a: "Proof goods were received", opts:["Request payment","Proof goods were received","Apply for discounts","Confirm purchase order"]},
    {q: "An invoice is:", a: "A bill for goods/services", opts:["A quotation","A reminder","A bill for goods/services","A signed delivery docket"]},
    {q: "What does E&OE stand for?", a: "Errors and omissions excepted", opts:["Electronic order entry","Estimated order expenses","Errors and omissions excepted","Email order evaluation"]},
    {q: "A credit note is:", a: "Issued for returned goods", opts:["Proof of payment","Issued for returned goods","Delivery confirmation","Request for stock"]},
    {q: "A statement shows:", a: "Transactions and balance owed", opts:["Daily income","Transaction sales only","Transactions and balance owed","Purchase orders only"]},
    {q: "What is effective purchasing?", a: "Getting best deal on price & quality", opts:["Cheapest supplier only","Low delivery charges","Getting best deal on price & quality","Single seller only"]},
    {q: "What is VAT?", a: "Tax added to goods/services", opts:["Discount","Tax added to goods/services","Profit","Loan interest"]},
    {q: "Trade discount is for:", a: "Bulk or loyal customers", opts:["Late payments","Bulk or loyal customers","Online orders","New businesses only"]},
    {q: "Cash discount encourages:", a: "Quick payment", opts:["Bulk orders","Quick payment","Late delivery","High expenses"]},
    {q: "Why check creditworthiness?", a: "To reduce risk of non-payment", opts:["Lower VAT","Offer lower prices","To reduce risk of non-payment","Give trade discount"]},
    {q: "EDI stands for:", a: "Electronic Data Interchange", opts:["Electronic Debit Invoice","Enterprise Document Info","Electronic Data Interchange","Encrypted Department Issue"]},
    {q: "Advantage of EDI:", a: "Fast and paperless", opts:["Slower delivery","Higher cost","Fast and paperless","More postage used"]},
    {q: "What is an order?", a: "Request to supply goods", opts:["Proof of receipt","Request to supply goods","Payment method","Invoice due"]},
    {q: "Order of documents:", a: "Enquiry → Quotation → Order → Delivery → Invoice → Payment → Receipt", opts:["Order → Enquiry → Delivery","Quotation → Receipt → Payment","Enquiry → Quotation → Order → Delivery → Invoice → Payment → Receipt","Invoice first → Order later"]},
    {q: "Who sends a quotation?", a: "Seller to buyer", opts:["Bank","Seller to buyer","Buyer to seller","Courier"]},
    {q: "Who issues sales invoice?", a: "Seller", opts:["Customer","Bank","Seller","Government"]},
    {q: "Bank reference checks:", a: "Customer's financial stability", opts:["Email access","Customer's financial stability","Tax payments","VAT eligibility"]},
    {q: "What is a receipt?", a: "Proof of payment", opts:["Quote","Order","Proof of payment","Request to pay"]},
    {q: "Statement helps buyer:", a: "Check amount due", opts:["Confirm delivery","Check amount due","See stock levels","Apply for discount"]},
    {q: "Why use business documents?", a: "To track transactions accurately", opts:["Increase cost","Avoid records","To track transactions accurately","To hide details"]},
    {q: "When is a credit note used?", a: "After goods are returned", opts:["When payment made","After goods are returned","Before order placed","After receipt"]},
    {q: "What is a quotation used for?", a: "To compare offers for best deal", opts:["To pay bills","To compare offers for best deal","To track sales","To calculate wages"]},
    {q: "What does 'credit sale' mean?", a: "Pay later for goods received", opts:["Pay now","Refund immediately","Pay later for goods received","Pay on delivery only"]},
    {q: "A trade reference checks:", a: "Reliability of customer payment", opts:["Stock prices","Reliability of customer payment","Tax status","Bank charges"]},
    {q: "Why keep copies of documents?", a: "For records and legal proof", opts:["To avoid planning","For records and legal proof","To increase costs","To delete data"]}
  ]
};

// FLASHCARD LOGIC
let currentSet = [];
let index = 0;

function startFlashcards(chapter){
  currentSet = flashcards[chapter];
  index = 0;
  showFlashcard();
}

function showFlashcard(){
  if(!currentSet[index]) {
    document.getElementById("flashcardArea").innerHTML = "<h3>🎉 You've finished this chapter!</h3><button class='btn-next' onclick='index=0; showFlashcard()'>Restart</button>";
    return;
  }

  let card = currentSet[index];
  document.getElementById("flashcardArea").innerHTML = `
    <h3>Flashcard ${index+1} / ${currentSet.length}</h3>
    <p><strong>${card.q}</strong></p>
    ${card.opts.map(o => `<button onclick="checkAnswer('${o}','${card.a}')">${o}</button>`).join("<br>")}
    <br><button class="btn-next" onclick="nextFlashcard()">Next</button>
  `;
}

function checkAnswer(selected, correct){
  if(selected === correct){
    alert("✔ Correct!");
  } else {
    alert("❌ Incorrect. Correct answer: " + correct);
  }
}

function nextFlashcard(){ index++; showFlashcard(); }

// LEARN MODE — Same but without 'Next' until they answer
function startLearnMode(chapter){
  currentSet = flashcards[chapter];
  index = 0;
  showLearnCard();
}

function showLearnCard(){
  if(!currentSet[index]){
    document.getElementById("flashcardArea").innerHTML = "<h3>🎊 Learn Mode Completed!</h3>";
    return;
  }

  let card = currentSet[index];
  document.getElementById("flashcardArea").innerHTML = `
    <h3>Learn Mode ${index+1} / ${currentSet.length}</h3>
    <p><strong>${card.q}</strong></p>
    ${card.opts.map(o => `<button onclick="answerLearn('${o}','${card.a}')">${o}</button>`).join("<br>")}
  `;
}

function answerLearn(selected, correct){
  if(selected === correct){
    alert("✔ Correct!");
    index++;
    showLearnCard();
  } else {
    alert("❌ Incorrect. Try again.");
  }
}
</script>

</body>
</html>
