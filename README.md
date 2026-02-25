<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Structured Retirement & Future Care Diagnostic</title>

<style>
body{
  margin:0;
  font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Arial,sans-serif;
  background:linear-gradient(135deg,#06101f,#0f2b52);
  color:white;
  padding:20px;
}
h1{
  font-family:Georgia,serif;
  background:linear-gradient(45deg,#d4af37,#f4d77a);
  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent;
}
.card{
  background:rgba(255,255,255,0.08);
  padding:18px;
  border-radius:16px;
  margin-top:15px;
}
input,select,textarea{
  width:100%;
  padding:12px;
  margin-top:6px;
  border-radius:10px;
  border:none;
  font-size:16px;
}
button{
  margin-top:15px;
  padding:12px;
  width:100%;
  border:none;
  border-radius:10px;
  font-weight:bold;
  background:linear-gradient(45deg,#d4af37,#f4d77a);
  color:#09121f;
  font-size:16px;
}
.small{
  font-size:13px;
  opacity:.8;
}
.hidden{display:none;}
</style>
</head>

<body>

<h1>Structured Retirement & Care Review</h1>

<div class="card" id="step1">
<h3>Questionnaire</h3>

<label>Your retirement goals</label>
<textarea id="goals"></textarea>

<label>Annual income needed (£)</label>
<input type="number" id="income" value="60000">

<label>Other guaranteed income (£)</label>
<input type="number" id="guaranteed" value="11500">

<label>Later-life income need (£)</label>
<input type="number" id="phase2" value="80000">

<label>Years until later-life uplift</label>
<input type="number" id="years" value="8">

<button onclick="goStep2()">Continue to Modelling</button>
</div>

<div class="card hidden" id="step2">
<h3>Modelling Assumptions</h3>

<label>Investable capital (£)</label>
<input type="number" id="capital" value="1000000">

<label>Your age</label>
<input type="number" id="age" value="67">

<label>Return assumption (%)</label>
<input type="number" id="return" value="5">

<label>Inflation (%)</label>
<input type="number" id="inflation" value="3">

<button onclick="calculate()">Run Analysis</button>
</div>

<div class="card hidden" id="step3">
<h3>Summary</h3>

<p id="result"></p>

<button onclick="emailResults()">Email My Results</button>

<form action="https://formspree.io/f/mojnewoq" method="POST">
<input type="hidden" name="results" id="hiddenResults">
<label>Your Name</label>
<input type="text" name="name" required>
<label>Your Email</label>
<input type="email" name="email" required>
<button type="submit">Send Securely</button>
</form>

</div>

<script>

function goStep2(){
  document.getElementById("step1").classList.add("hidden");
  document.getElementById("step2").classList.remove("hidden");
}

function calculate(){

  let capital = Number(document.getElementById("capital").value);
  let age = Number(document.getElementById("age").value);
  let income = Number(document.getElementById("income").value);
  let guaranteed = Number(document.getElementById("guaranteed").value);
  let phase2 = Number(document.getElementById("phase2").value);
  let years = Number(document.getElementById("years").value);
  let ret = Number(document.getElementById("return").value)/100;
  let inf = Number(document.getElementById("inflation").value)/100;

  let advisorFee = 0.25;
  let grossYield = 5.08;
  let netYield = grossYield - advisorFee;

  let netIncome = capital * netYield/100;

  let draw1 = income - guaranteed;
  let draw2 = phase2 - guaranteed;

  let balance = capital;
  let depletionAge = "Not within 40 years";

  for(let i=0;i<40;i++){
    let withdrawal = (i<years?draw1:draw2) * Math.pow(1+inf,i);
    balance = balance*(1+ret) - withdrawal;
    if(balance<=0){
      depletionAge = age+i;
      break;
    }
  }

  let output = `
Net Yield After Advisory: ${netYield.toFixed(2)}%
Estimated Annual Net Income: £${Math.round(netIncome).toLocaleString()}
Phase One Withdrawal: £${draw1.toLocaleString()}
Phase Two Withdrawal: £${draw2.toLocaleString()}
Estimated Depletion Age: ${depletionAge}
`;

  document.getElementById("result").innerText = output;
  document.getElementById("hiddenResults").value = output;

  document.getElementById("step2").classList.add("hidden");
  document.getElementById("step3").classList.remove("hidden");
}

function emailResults(){
  let body = encodeURIComponent(document.getElementById("result").innerText);
  window.location.href = `mailto:tony.tharian@canaccord.com,naseer.dean@canaccord.com?subject=Retirement Diagnostic&body=${body}`;
}

</script>

</body>
</html>
