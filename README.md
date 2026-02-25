<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Retirement & Future Care Questionnaire — Email Template</title>
  <style>
    :root{
      --bg1:#06101f;
      --bg2:#0f2b52;
      --card:rgba(255,255,255,.07);
      --stroke:rgba(255,255,255,.12);
      --text:#f4f7ff;
      --muted:rgba(244,247,255,.72);
      --gold1:#d4af37;
      --gold2:#f4d77a;
      --btn:#223553;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Arial,sans-serif;
      color:var(--text);
      background:
        radial-gradient(circle at 15% 10%, rgba(212,175,55,.14), transparent 45%),
        radial-gradient(circle at 85% 30%, rgba(80,140,220,.16), transparent 42%),
        linear-gradient(135deg,var(--bg1),var(--bg2));
      min-height:100vh;
    }
    .wrap{max-width:980px;margin:0 auto;padding:22px 14px 60px;}
    h1{
      margin:0;
      font-family:Georgia,"Times New Roman",serif;
      font-weight:500;
      font-size:34px;
      background:linear-gradient(45deg,var(--gold1),var(--gold2));
      -webkit-background-clip:text;
      -webkit-text-fill-color:transparent;
    }
    .sub{margin:10px 0 0;color:var(--muted);line-height:1.55}
    .card{
      background:var(--card);
      border:1px solid var(--stroke);
      border-radius:18px;
      padding:18px;
      margin-top:14px;
      box-shadow:0 18px 55px rgba(0,0,0,.35);
      backdrop-filter: blur(12px);
    }
    label{
      display:block;margin:10px 0 6px;font-size:12px;font-weight:850;color:rgba(244,247,255,.90)
    }
    input, textarea{
      width:100%;
      padding:12px 12px;
      border-radius:14px;
      border:1px solid rgba(255,255,255,.14);
      background:rgba(9,15,24,.45);
      color:var(--text);
      font-size:15px;
      outline:none;
    }
    textarea{min-height:340px;resize:vertical;white-space:pre-wrap;line-height:1.5}
    .row{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    @media(max-width:820px){.row{grid-template-columns:1fr}}
    .actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:12px}
    .btn{
      border:none;border-radius:14px;padding:12px 14px;
      font-size:14px;font-weight:900;cursor:pointer;user-select:none
    }
    .btn.primary{background:linear-gradient(45deg,var(--gold1),var(--gold2));color:#09121f}
    .btn.secondary{background:var(--btn);color:var(--text);border:1px solid rgba(255,255,255,.12)}
    .fine{margin-top:10px;color:rgba(244,247,255,.6);font-size:12px;line-height:1.45}
    .toast{
      position:fixed;left:50%;bottom:18px;transform:translateX(-50%);
      background:rgba(0,0,0,.75);color:#fff;padding:10px 12px;border-radius:999px;
      font-size:13px;opacity:0;pointer-events:none;transition:opacity .2s ease;
    }
    .toast.show{opacity:1}
  </style>
</head>
<body>
  <div class="wrap">
    <h1>Client Questionnaire Email Template</h1>
    <p class="sub">
      Edit the fields, then use <b>Copy</b> to paste into Outlook/Gmail, or use <b>Open Email</b> to create a draft via your email app.
    </p>

    <div class="card">
      <div class="row">
        <div>
          <label>Subject</label>
          <input id="subject" value="Retirement & Future Care Planning – Personal Planning Questionnaire">
        </div>
        <div>
          <label>Client Name (for greeting)</label>
          <input id="clientName" value="[Name]">
        </div>
      </div>

      <label>Your Name (signature)</label>
      <input id="senderName" value="Tony Tharian">

      <label>Your Title (signature)</label>
      <input id="senderTitle" value="Investment Director">

      <label>Email Body</label>
      <textarea id="body"></textarea>

      <div class="actions">
        <button class="btn primary" onclick="fillTemplate()">Refresh with fields</button>
        <button class="btn secondary" onclick="copyAll()">Copy email</button>
        <button class="btn secondary" onclick="openMailto()">Open email draft</button>
        <button class="btn secondary" onclick="downloadEML()">Download .eml</button>
      </div>

      <div class="fine">
        Tip: If “Open email draft” looks too long in your email app, use <b>Copy email</b> instead and paste into your email.
      </div>
    </div>
  </div>

  <div class="toast" id="toast">Copied</div>

<script>
const template = (name, senderName, senderTitle) => `Hi ${name},

I hope you are well.

As part of our structured retirement and future care planning process, we would appreciate if you could take a few minutes to complete the short questionnaire below.

This is designed to help us clearly understand your long-term objectives, income sustainability requirements, and any potential later-life care considerations. The more clarity we have at this stage, the more precisely we can tailor a plan that aligns with your personal priorities.

---

RETIREMENT & FUTURE CARE PLANNING QUESTIONNAIRE

1) Retirement Objectives & Priorities
• What are your primary goals for retirement?
  (e.g. maintaining lifestyle, preserving capital, generating dependable income, legacy planning) • How important is predictable, stable income throughout retirement?
• Do you expect your spending levels to change over time?
  (For example, higher discretionary spending early on, potentially higher care costs later.)

2) Cash-Flow & Income Requirements
• What level of annual income do you anticipate requiring in retirement?
• Should this income rise in line with inflation?
• What other income sources will support you?
  (State pension, defined benefit schemes, rental income, dividends, business income, etc.)

3) Assets Available for Retirement
• Which assets do you intend to rely upon?
  (Pensions, ISAs, investment portfolios, property, cash reserves.) • Do you intend to draw down capital gradually, or is capital preservation a priority?

4) Future Care Considerations
• Have you considered the potential need for home or residential care later in life?
• Would you prefer to plan for:
  ☐ Full self-funding
  ☐ Partial self-funding
  ☐ Undecided at this stage
• Do you have an estimated annual care budget in mind?
• Is it important that care funding is structured so as not to materially affect family inheritance?

5) Risk & Sustainability
• How important is capital preservation alongside income generation?
• How comfortable are you with investment risk if it enhances long-term sustainability?
• Would you find value in reviewing a forward-looking cash-flow model under different economic scenarios?

6) Planning Structure
• Would you prefer a phased retirement strategy (for example, lower early withdrawals with provision for higher later-life needs)?
• How frequently would you like your retirement strategy formally reviewed?

7) Immediate Priorities
• Are there any pressing matters you would like us to address?
  (Pension consolidation, income strategy, care-cost modelling, inheritance structuring, etc.)

---

Thank you for taking the time to complete this. Your responses will allow us to build a clear, disciplined framework designed to provide income stability, structural resilience, and long-term clarity.

If preferred, we can also provide this in a secure online format, as a fillable PDF, or incorporate it into a formal onboarding pack.

Kind regards,
${senderName}
${senderTitle}
`;

function fillTemplate(){
  const name = document.getElementById('clientName').value || '[Name]';
  const senderName = document.getElementById('senderName').value || 'Tony Tharian';
  const senderTitle = document.getElementById('senderTitle').value || 'Investment Director';
  document.getElementById('body').value = template(name, senderName, senderTitle); }

function showToast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'), 1100); }

async function copyAll(){
  const subject = document.getElementById('subject').value.trim();
  const body = document.getElementById('body').value;
  const full = `Subject: ${subject}\n\n${body}`;
  try{
    await navigator.clipboard.writeText(full);
    showToast('Copied');
  } catch(e){
    // fallback
    const ta = document.createElement('textarea');
    ta.value = full;
    document.body.appendChild(ta);
    ta.select();
    document.execCommand('copy');
    document.body.removeChild(ta);
    showToast('Copied');
  }
}

function openMailto(){
  const subject = encodeURIComponent(document.getElementById('subject').value.trim());
  const body = encodeURIComponent(document.getElementById('body').value);
  // Leave TO blank so you can pick recipient; add recipient if you want.
  window.location.href = `mailto:?subject=${subject}&body=${body}`;
}

function downloadEML(){
  const subject = document.getElementById('subject').value.trim();
  const body = document.getElementById('body').value;

  const eml =
`Subject: ${subject}
MIME-Version: 1.0
Content-Type: text/plain; charset=UTF-8
Content-Transfer-Encoding: 8bit

${body}`;

  const blob = new Blob([eml], {type: 'message/rfc822'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'retirement_questionnaire_email.eml';
  document.body.appendChild(a);
  a.click();
  a.remove();
  URL.revokeObjectURL(url);
  showToast('Downloaded .eml');
}

// init
fillTemplate();
</script>
</body>
</html>
