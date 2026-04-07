<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="FI Revamp">
<meta name="theme-color" content="#1a3a2a">
<title>Floral Image — Revamp Log</title>
<link rel="apple-touch-icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect width='100' height='100' rx='20' fill='%231a3a2a'/><text y='.9em' font-size='72' x='50%' text-anchor='middle'>🌸</text></svg>">
<style>
  @import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=DM+Sans:wght@300;400;500&display=swap');

  :root {
    --green-deep: #1a3a2a;
    --green-mid: #2d6649;
    --green-light: #4a9968;
    --green-pale: #e8f2ec;
    --cream: #faf8f4;
    --text: #1a2a1e;
    --text-muted: #6b8070;
    --border: rgba(45,102,73,0.18);
    --radius: 14px;
    --radius-sm: 8px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

  html, body {
    height: 100%;
    background: var(--cream);
    font-family: 'DM Sans', sans-serif;
    color: var(--text);
    overscroll-behavior: none;
  }

  .app {
    min-height: 100vh;
    min-height: -webkit-fill-available;
    display: flex;
    flex-direction: column;
  }

  /* Header */
  .header {
    background: var(--green-deep);
    padding: env(safe-area-inset-top, 0) 0 0;
    position: sticky;
    top: 0;
    z-index: 10;
  }
  .header-inner {
    padding: 14px 20px 12px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .header-logo { font-size: 22px; }
  .header-text h1 {
    font-family: 'DM Serif Display', serif;
    font-size: 17px;
    color: #fff;
    font-weight: 400;
    letter-spacing: 0.01em;
  }
  .header-text p {
    font-size: 11px;
    color: rgba(255,255,255,0.55);
    letter-spacing: 0.04em;
    text-transform: uppercase;
    margin-top: 1px;
  }

  /* Progress bar */
  .progress-bar {
    display: flex;
    padding: 0 20px 14px;
    gap: 5px;
  }
  .pb-seg {
    flex: 1;
    height: 2px;
    border-radius: 2px;
    background: rgba(255,255,255,0.2);
    transition: background 0.3s;
  }
  .pb-seg.done { background: var(--green-light); }
  .pb-seg.active { background: rgba(255,255,255,0.7); }

  /* Main content */
  .content {
    flex: 1;
    padding: 24px 20px 100px;
    max-width: 520px;
    margin: 0 auto;
    width: 100%;
  }

  /* Steps */
  .step { display: none; animation: fadeUp 0.25s ease; }
  .step.active { display: block; }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(10px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .step-label {
    font-size: 11px;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 6px;
  }
  .step-title {
    font-family: 'DM Serif Display', serif;
    font-size: 26px;
    font-weight: 400;
    color: var(--green-deep);
    margin-bottom: 24px;
    line-height: 1.2;
  }

  /* Fields */
  .field { margin-bottom: 18px; }
  .field > label {
    display: block;
    font-size: 12px;
    font-weight: 500;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    margin-bottom: 7px;
  }

  input[type=text], input[type=number], textarea, select {
    width: 100%;
    padding: 13px 14px;
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    font-family: 'DM Sans', sans-serif;
    font-size: 16px;
    color: var(--text);
    background: #fff;
    outline: none;
    transition: border-color 0.15s;
    -webkit-appearance: none;
  }
  input:focus, textarea:focus {
    border-color: var(--green-mid);
    box-shadow: 0 0 0 3px rgba(45,102,73,0.1);
  }
  textarea { min-height: 90px; resize: vertical; line-height: 1.5; }

  /* Photo capture */
  .photo-capture {
    border: 1.5px dashed rgba(45,102,73,0.3);
    border-radius: var(--radius);
    background: #fff;
    overflow: hidden;
    position: relative;
    transition: border-color 0.2s;
  }
  .photo-capture.has-photo { border-style: solid; border-color: var(--green-mid); }
  .photo-capture input[type=file] {
    position: absolute; inset: 0; opacity: 0; width: 100%; height: 100%; cursor: pointer; z-index: 2;
  }
  .photo-placeholder {
    padding: 28px 20px;
    text-align: center;
  }
  .photo-icon { font-size: 36px; margin-bottom: 8px; display: block; }
  .photo-label { font-size: 15px; color: var(--green-mid); font-weight: 500; }
  .photo-sub { font-size: 12px; color: var(--text-muted); margin-top: 3px; }
  .photo-preview {
    width: 100%; max-height: 220px; object-fit: cover; display: none;
  }
  .photo-retake {
    position: absolute; bottom: 10px; right: 10px; z-index: 3;
    background: rgba(26,58,42,0.82); color: #fff; border: none;
    padding: 6px 12px; border-radius: 20px; font-size: 12px;
    font-family: 'DM Sans', sans-serif; cursor: pointer; display: none;
  }

  /* Stems */
  .stem-row {
    display: flex; gap: 8px; align-items: center; margin-bottom: 8px;
  }
  .stem-row input[type=text] { flex: 2; }
  .stem-row input[type=number] { flex: 0.85; }
  .stem-remove {
    background: none; border: none; color: var(--text-muted);
    font-size: 20px; cursor: pointer; padding: 0 4px; line-height: 1;
    flex-shrink: 0;
  }
  .add-stem-btn {
    display: flex; align-items: center; gap: 6px;
    background: var(--green-pale); border: 1px solid rgba(45,102,73,0.2);
    color: var(--green-mid); font-family: 'DM Sans', sans-serif;
    font-size: 14px; font-weight: 500; padding: 9px 14px;
    border-radius: var(--radius-sm); cursor: pointer; margin-top: 4px;
    width: 100%;
  }

  /* Bottom nav */
  .bottom-nav {
    position: fixed;
    bottom: 0; left: 0; right: 0;
    background: rgba(250,248,244,0.95);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    padding: 12px 20px env(safe-area-inset-bottom, 12px);
    border-top: 1px solid var(--border);
    display: flex; gap: 10px;
    max-width: 520px; margin: 0 auto;
  }

  .btn {
    flex: 1; padding: 14px;
    border-radius: var(--radius-sm);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px; font-weight: 500;
    cursor: pointer; border: 1px solid var(--border);
    background: #fff; color: var(--text);
    transition: all 0.15s;
  }
  .btn:active { transform: scale(0.97); }
  .btn.primary {
    background: var(--green-deep); color: #fff; border-color: var(--green-deep);
  }
  .btn.primary:active { background: var(--green-mid); }
  .btn:disabled { opacity: 0.4; cursor: not-allowed; }

  /* Status */
  .status-msg {
    font-size: 13px; text-align: center; color: var(--text-muted);
    margin-top: 10px; min-height: 18px; padding: 0 10px;
  }
  .status-msg.error { color: #c0392b; }

  /* Success */
  .success-screen {
    text-align: center; padding: 40px 20px;
  }
  .success-icon { font-size: 64px; margin-bottom: 20px; display: block; }
  .success-screen h2 {
    font-family: 'DM Serif Display', serif;
    font-size: 28px; font-weight: 400; color: var(--green-deep); margin-bottom: 10px;
  }
  .success-screen p { font-size: 15px; color: var(--text-muted); line-height: 1.6; }
  .success-meta {
    background: var(--green-pale); border-radius: var(--radius);
    padding: 14px 18px; margin: 20px 0; text-align: left;
  }
  .success-meta p { font-size: 13px; color: var(--green-mid); margin-bottom: 4px; }
  .success-meta strong { color: var(--green-deep); }

  /* Divider */
  .divider {
    display: flex; align-items: center; gap: 10px; margin: 20px 0;
  }
  .divider span { font-size: 11px; color: var(--text-muted); white-space: nowrap; text-transform: uppercase; letter-spacing: 0.06em; }
  .divider::before, .divider::after { content:''; flex:1; height:1px; background: var(--border); }
</style>
</head>
<body>
<div class="app">

  <div class="header">
    <div class="header-inner">
      <span class="header-logo">🌸</span>
      <div class="header-text">
        <h1>Floral Image</h1>
        <p>Revamp Log</p>
      </div>
    </div>
    <div class="progress-bar" id="progress-bar">
      <div class="pb-seg active" id="pb0"></div>
      <div class="pb-seg" id="pb1"></div>
      <div class="pb-seg" id="pb2"></div>
      <div class="pb-seg" id="pb3"></div>
    </div>
  </div>

  <div class="content">

    <!-- Step 0: Vase Details -->
    <div class="step active" id="step-0">
      <div class="step-label">Step 1 of 4</div>
      <div class="step-title">Vase details</div>

      <div class="field">
        <label>Your name</label>
        <input type="text" id="staff-name" placeholder="e.g. Sarah" autocomplete="name">
      </div>

      <div class="field">
        <label>Location / client</label>
        <input type="text" id="location" placeholder="e.g. NAB Canberra — Reception">
      </div>

      <div class="field">
        <label>Serial number photo</label>
        <div class="photo-capture" id="box-serial">
          <input type="file" accept="image/*" capture="environment" id="file-serial"
            onchange="handlePhoto(this,'img-serial','box-serial','retake-serial','ph-serial')">
          <div class="photo-placeholder" id="ph-serial">
            <span class="photo-icon">🏷️</span>
            <div class="photo-label">Photograph serial number</div>
            <div class="photo-sub">Tap to open camera</div>
          </div>
          <img class="photo-preview" id="img-serial">
          <button class="photo-retake" id="retake-serial" onclick="retakePhoto('file-serial',event)">Retake</button>
        </div>
      </div>

      <div class="divider"><span>or type it</span></div>

      <div class="field">
        <label>Serial number (manual)</label>
        <input type="text" id="serial-text" placeholder="e.g. FI-0042" autocomplete="off">
      </div>
    </div>

    <!-- Step 1: Before Photo -->
    <div class="step" id="step-1">
      <div class="step-label">Step 2 of 4</div>
      <div class="step-title">Before photo</div>

      <div class="field">
        <label>Current arrangement</label>
        <div class="photo-capture" id="box-before">
          <input type="file" accept="image/*" capture="environment" id="file-before"
            onchange="handlePhoto(this,'img-before','box-before','retake-before','ph-before')">
          <div class="photo-placeholder" id="ph-before">
            <span class="photo-icon">📸</span>
            <div class="photo-label">Photograph before revamp</div>
            <div class="photo-sub">Show the full arrangement clearly</div>
          </div>
          <img class="photo-preview" id="img-before">
          <button class="photo-retake" id="retake-before" onclick="retakePhoto('file-before',event)">Retake</button>
        </div>
      </div>
    </div>

    <!-- Step 2: Stems -->
    <div class="step" id="step-2">
      <div class="step-label">Step 3 of 4</div>
      <div class="step-title">Stems used</div>

      <div class="field">
        <label>Stem types &amp; quantities</label>
        <div id="stems-list"></div>
        <button class="add-stem-btn" onclick="addStem()">＋ Add stem type</button>
      </div>

      <div class="field">
        <label>Notes</label>
        <textarea id="notes" placeholder="Vase condition, special requests, anything worth logging…"></textarea>
      </div>
    </div>

    <!-- Step 3: After Photo -->
    <div class="step" id="step-3">
      <div class="step-label">Step 4 of 4</div>
      <div class="step-title">After photo</div>

      <div class="field">
        <label>Finished arrangement</label>
        <div class="photo-capture" id="box-after">
          <input type="file" accept="image/*" capture="environment" id="file-after"
            onchange="handlePhoto(this,'img-after','box-after','retake-after','ph-after')">
          <div class="photo-placeholder" id="ph-after">
            <span class="photo-icon">💐</span>
            <div class="photo-label">Photograph finished revamp</div>
            <div class="photo-sub">Show the full arrangement clearly</div>
          </div>
          <img class="photo-preview" id="img-after">
          <button class="photo-retake" id="retake-after" onclick="retakePhoto('file-after',event)">Retake</button>
        </div>
      </div>
      <div class="status-msg" id="status-msg"></div>
    </div>

    <!-- Success -->
    <div class="step" id="step-done">
      <div class="success-screen">
        <span class="success-icon">✅</span>
        <h2>Record saved!</h2>
        <p>Photos uploaded to Google Drive and logged to your Revamp Sheet.</p>
        <div class="success-meta" id="success-meta"></div>
      </div>
    </div>

  </div><!-- /content -->

  <div class="bottom-nav" id="bottom-nav">
    <button class="btn" id="btn-back" onclick="goBack()" style="display:none">← Back</button>
    <button class="btn primary" id="btn-next" onclick="goNext()">Next →</button>
  </div>

</div><!-- /app -->

<script>
// =============================================
// CONFIGURATION — paste your Apps Script URL here
// =============================================
const APPS_SCRIPT_URL = 'YOUR_APPS_SCRIPT_URL_HERE';
// =============================================

let currentStep = 0;
const totalSteps = 4;

function updateNav() {
  const back = document.getElementById('btn-back');
  const next = document.getElementById('btn-next');
  const nav  = document.getElementById('bottom-nav');

  if (currentStep === totalSteps) {
    nav.style.display = 'none';
    document.getElementById('progress-bar').style.display = 'none';
    return;
  }

  back.style.display = currentStep > 0 ? 'block' : 'none';
  next.textContent = currentStep === totalSteps - 1 ? 'Submit record ✓' : 'Next →';
  next.disabled = false;

  for (let i = 0; i < totalSteps; i++) {
    const seg = document.getElementById('pb' + i);
    seg.className = 'pb-seg';
    if (i < currentStep) seg.classList.add('done');
    else if (i === currentStep) seg.classList.add('active');
  }
}

function showStep(n) {
  document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
  const id = n === totalSteps ? 'step-done' : 'step-' + n;
  document.getElementById(id).classList.add('active');
  currentStep = n;
  updateNav();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function goBack() { if (currentStep > 0) showStep(currentStep - 1); }

function goNext() {
  if (currentStep === totalSteps - 1) {
    submitForm();
  } else {
    showStep(currentStep + 1);
  }
}

// Photo handling
function handlePhoto(input, imgId, boxId, retakeId, phId) {
  const file = input.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = e => {
    const img = document.getElementById(imgId);
    img.src = e.target.result;
    img.style.display = 'block';
    document.getElementById(phId).style.display = 'none';
    document.getElementById(retakeId).style.display = 'block';
    document.getElementById(boxId).classList.add('has-photo');
    // make the retake button not trigger the file input
    img.style.zIndex = '1';
  };
  reader.readAsDataURL(file);
}

function retakePhoto(fileId, event) {
  event.stopPropagation();
  document.getElementById(fileId).click();
}

// Stems
function addStem() {
  const list = document.getElementById('stems-list');
  const row = document.createElement('div');
  row.className = 'stem-row';
  row.innerHTML = `
    <input type="text" placeholder="Stem type (e.g. White rose)">
    <input type="number" placeholder="Qty" min="1" style="max-width:80px">
    <button class="stem-remove" onclick="this.parentElement.remove()">×</button>
  `;
  list.appendChild(row);
  row.querySelector('input').focus();
}

function getStems() {
  return Array.from(document.querySelectorAll('.stem-row'))
    .map(row => {
      const inputs = row.querySelectorAll('input');
      const type = inputs[0].value.trim();
      const qty  = inputs[1].value.trim();
      return type ? (qty ? qty + '× ' + type : type) : null;
    })
    .filter(Boolean)
    .join(', ');
}

// File to base64
function toB64(file) {
  return new Promise((res, rej) => {
    if (!file) return res(null);
    const r = new FileReader();
    r.onload = e => res(e.target.result.split(',')[1]);
    r.onerror = rej;
    r.readAsDataURL(file);
  });
}

// Submit
async function submitForm() {
  const btn = document.getElementById('btn-next');
  const status = document.getElementById('status-msg');
  btn.disabled = true;
  btn.textContent = 'Uploading…';
  status.className = 'status-msg';
  status.textContent = 'Uploading photos and saving record…';

  const serialFile = document.getElementById('file-serial').files[0];
  const beforeFile = document.getElementById('file-before').files[0];
  const afterFile  = document.getElementById('file-after').files[0];

  const [s64, b64, a64] = await Promise.all([
    toB64(serialFile), toB64(beforeFile), toB64(afterFile)
  ]);

  const ts = Date.now();
  const payload = {
    staffName:   document.getElementById('staff-name').value.trim(),
    location:    document.getElementById('location').value.trim(),
    serialText:  document.getElementById('serial-text').value.trim(),
    stems:       getStems(),
    notes:       document.getElementById('notes').value.trim(),
    timestamp:   new Date().toISOString(),
    serialImage: s64 ? { data: s64, mimeType: serialFile.type, name: 'serial_' + ts + '.jpg' } : null,
    beforeImage: b64 ? { data: b64, mimeType: beforeFile.type, name: 'before_' + ts + '.jpg' } : null,
    afterImage:  a64 ? { data: a64, mimeType: afterFile.type,  name: 'after_'  + ts + '.jpg' } : null,
  };

  try {
    const res = await fetch(APPS_SCRIPT_URL, {
      method: 'POST',
      body: JSON.stringify(payload)
    });
    const json = await res.json();
    if (json.status === 'ok') {
      // Populate success summary
      const meta = document.getElementById('success-meta');
      meta.innerHTML = `
        <p><strong>${payload.staffName || 'Staff'}</strong> — ${payload.location || 'No location'}</p>
        <p>Serial: <strong>${payload.serialText || '(photo only)'}</strong></p>
        ${payload.stems ? '<p>Stems: <strong>' + payload.stems + '</strong></p>' : ''}
        <p style="margin-top:8px;font-size:12px;color:var(--text-muted)">${new Date().toLocaleString('en-AU')}</p>
      `;
      showStep(totalSteps);
    } else {
      throw new Error(json.message || 'Unknown error from server');
    }
  } catch (err) {
    status.className = 'status-msg error';
    status.textContent = '⚠ ' + err.message;
    btn.disabled = false;
    btn.textContent = 'Submit record ✓';
  }
}

// Reset for next vase
function resetForm() {
  ['staff-name','location','serial-text','notes'].forEach(id => document.getElementById(id).value = '');
  ['serial','before','after'].forEach(key => {
    document.getElementById('file-' + key).value = '';
    const img = document.getElementById('img-' + key);
    img.src = ''; img.style.display = 'none';
    document.getElementById('ph-' + key).style.display = '';
    document.getElementById('retake-' + key).style.display = 'none';
    document.getElementById('box-' + key).classList.remove('has-photo');
  });
  document.getElementById('stems-list').innerHTML = '';
  document.getElementById('status-msg').textContent = '';
  document.getElementById('btn-next').disabled = false;
  document.getElementById('progress-bar').style.display = 'flex';
  document.getElementById('bottom-nav').style.display = 'flex';
  showStep(0);
  addStem();
}

// Init
addStem();
updateNav();

// Make the reset button in success screen work
document.getElementById('step-done').innerHTML += `
  <button onclick="resetForm()" class="btn primary" style="margin-top:10px;width:100%;max-width:300px">Log another vase</button>
`;
</script>
</body>
</html>
