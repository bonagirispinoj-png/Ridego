<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>RideGo — Smart Rides</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root {
  --primary: #FF6B35;
  --primary-dark: #e55a25;
  --secondary: #1A1A2E;
  --accent: #16213E;
  --green: #00C853;
  --green-dark: #00A344;
  --red: #FF3D57;
  --yellow: #FFD600;
  --purple: #7C4DFF;
  --bg: #F5F5F5;
  --card: #ffffff;
  --text: #1A1A2E;
  --muted: #888;
  --border: #E8E8E8;
  --shadow: 0 4px 20px rgba(0,0,0,0.08);
  --shadow-strong: 0 8px 32px rgba(0,0,0,0.15);
}
* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
body { font-family: 'Nunito', sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; overflow-x: hidden; }
.screen { display: none; }
.screen.active { display: block; }

/* HEADER */
.app-header { background: var(--secondary); color: #fff; padding: 14px 16px; display: flex; align-items: center; justify-content: space-between; position: sticky; top: 0; z-index: 100; }
.app-header h1 { font-size: 20px; font-weight: 800; letter-spacing: -0.5px; }
.app-header .logo-dot { color: var(--primary); }
.header-sub { font-size: 11px; opacity: 0.6; font-weight: 400; }

/* CARDS */
.card { background: var(--card); border-radius: 16px; padding: 16px; margin: 10px; box-shadow: var(--shadow); }
.card-title { font-size: 16px; font-weight: 800; margin-bottom: 12px; color: var(--text); }

/* INPUTS */
input, select, textarea {
  display: block; width: 100%; padding: 13px 14px; margin: 6px 0 12px;
  border: 1.5px solid var(--border); border-radius: 12px; font-size: 15px;
  font-family: 'Nunito', sans-serif; background: #fff; color: var(--text);
  transition: border-color 0.2s;
}
input:focus, select:focus, textarea:focus { outline: none; border-color: var(--primary); }
label { font-size: 13px; font-weight: 700; color: var(--muted); text-transform: uppercase; letter-spacing: 0.5px; display: block; margin-bottom: 2px; }
textarea { resize: vertical; min-height: 70px; }

/* BUTTONS */
.btn {
  display: block; width: 100%; padding: 14px; margin: 6px 0;
  border: none; border-radius: 12px; font-size: 15px; font-weight: 800;
  cursor: pointer; font-family: 'Nunito', sans-serif; transition: all 0.2s;
  text-align: center; letter-spacing: 0.3px;
}
.btn:active { transform: scale(0.97); }
.btn-primary { background: var(--primary); color: #fff; }
.btn-primary:active { background: var(--primary-dark); }
.btn-secondary { background: var(--secondary); color: #fff; }
.btn-green { background: var(--green); color: #fff; }
.btn-green:active { background: var(--green-dark); }
.btn-red { background: var(--red); color: #fff; }
.btn-gray { background: #E8E8E8; color: var(--text); }
.btn-outline { background: transparent; border: 2px solid var(--primary); color: var(--primary); }
.btn-sm { padding: 8px 14px; font-size: 13px; margin: 4px; width: auto; display: inline-block; border-radius: 8px; }
.btn-purple { background: var(--purple); color: #fff; }

/* LANDING */
#screen-landing { min-height: 100vh; background: linear-gradient(160deg, var(--secondary) 0%, var(--accent) 60%, #0F3460 100%); }
.landing-hero { padding: 50px 20px 30px; text-align: center; }
.landing-hero .logo { font-size: 42px; font-weight: 900; color: #fff; letter-spacing: -1px; }
.landing-hero .logo span { color: var(--primary); }
.landing-hero .tagline { color: rgba(255,255,255,0.65); font-size: 15px; margin-top: 8px; font-weight: 500; }
.landing-hero .hero-icon { font-size: 72px; margin: 20px 0; animation: float 3s ease-in-out infinite; }
@keyframes float { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
.landing-cards { padding: 0 16px 30px; }
.role-card { background: rgba(255,255,255,0.08); backdrop-filter: blur(10px); border: 1px solid rgba(255,255,255,0.15); border-radius: 20px; padding: 20px; margin: 12px 0; cursor: pointer; transition: all 0.2s; display: flex; align-items: center; gap: 16px; }
.role-card:active { transform: scale(0.97); background: rgba(255,255,255,0.15); }
.role-card .role-icon { font-size: 36px; }
.role-card .role-info h3 { color: #fff; font-size: 17px; font-weight: 800; }
.role-card .role-info p { color: rgba(255,255,255,0.55); font-size: 13px; margin-top: 2px; }
.role-card .arrow { margin-left: auto; color: rgba(255,255,255,0.4); font-size: 20px; }

/* MAP placeholder */
.map-container { height: 220px; border-radius: 14px; overflow: hidden; margin: 10px; background: #e0e0e0; position: relative; }
.map-container iframe { width: 100%; height: 100%; border: none; }
.map-overlay { position: absolute; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0); pointer-events: none; }
.map-pin { position: absolute; top: 50%; left: 50%; transform: translate(-50%,-100%); font-size: 28px; }
.locate-btn { position: absolute; bottom: 10px; right: 10px; background: white; border: none; border-radius: 50%; width: 40px; height: 40px; font-size: 18px; cursor: pointer; box-shadow: 0 2px 8px rgba(0,0,0,0.2); }

/* VEHICLE SELECTOR */
.vehicle-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin: 10px 0; }
.vehicle-option { background: #f8f8f8; border: 2px solid transparent; border-radius: 12px; padding: 12px 6px; text-align: center; cursor: pointer; transition: all 0.2s; }
.vehicle-option.selected { border-color: var(--primary); background: #fff3ee; }
.vehicle-option .v-icon { font-size: 26px; display: block; }
.vehicle-option .v-name { font-size: 12px; font-weight: 700; margin-top: 4px; }
.vehicle-option .v-price { font-size: 11px; color: var(--muted); }

/* FARE ESTIMATE BOX */
.fare-box { background: linear-gradient(135deg, #fff3ee, #ffe8dc); border: 1.5px solid #ffcdb5; border-radius: 14px; padding: 14px; margin: 8px 0; }
.fare-box .fare-amount { font-size: 28px; font-weight: 900; color: var(--primary); }
.fare-box .fare-label { font-size: 13px; color: var(--muted); }

/* RIDE STATUS TRACKING */
.ride-tracking { text-align: center; padding: 20px 10px; }
.tracking-steps { display: flex; flex-direction: column; gap: 0; margin: 20px 10px; }
.tracking-step { display: flex; align-items: flex-start; gap: 14px; padding: 12px 0; position: relative; }
.tracking-step:not(:last-child)::after { content: ''; position: absolute; left: 15px; top: 50px; width: 2px; height: calc(100% - 20px); background: var(--border); }
.step-dot { width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 15px; flex-shrink: 0; }
.step-dot.done { background: var(--green); }
.step-dot.active { background: var(--primary); animation: pulse 1.5s infinite; }
.step-dot.pending { background: var(--border); }
@keyframes pulse { 0%,100% { box-shadow: 0 0 0 0 rgba(255,107,53,0.4); } 50% { box-shadow: 0 0 0 8px rgba(255,107,53,0); } }
.step-info h4 { font-size: 15px; font-weight: 700; }
.step-info p { font-size: 13px; color: var(--muted); margin-top: 2px; }

/* DRIVER CARD */
.driver-info-card { background: var(--secondary); color: #fff; border-radius: 20px; padding: 16px; margin: 10px; }
.driver-info-card .d-name { font-size: 18px; font-weight: 800; }
.driver-info-card .d-detail { font-size: 13px; opacity: 0.7; margin-top: 2px; }
.driver-info-card .d-rating { color: var(--yellow); font-size: 13px; margin-top: 4px; }
.driver-avatar { width: 56px; height: 56px; border-radius: 50%; background: rgba(255,255,255,0.15); font-size: 28px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.contact-row { display: flex; gap: 8px; margin-top: 12px; }
.contact-btn { flex: 1; background: rgba(255,255,255,0.12); border: none; color: #fff; border-radius: 10px; padding: 10px; font-size: 13px; font-weight: 700; font-family: 'Nunito', sans-serif; cursor: pointer; }

/* STATUS BADGES */
.badge { display: inline-block; padding: 4px 10px; border-radius: 20px; font-size: 12px; font-weight: 800; }
.badge-pending { background: #FFF3E0; color: #E65100; }
.badge-accepted { background: #E3F2FD; color: #1565C0; }
.badge-completed { background: #E8F5E9; color: #1B5E20; }
.badge-cancelled { background: #FFEBEE; color: #B71C1C; }
.badge-approved { background: #E8F5E9; color: #1B5E20; }
.badge-rejected { background: #FFEBEE; color: #B71C1C; }
.badge-review { background: #EDE7F6; color: #4A148C; }
.badge-online { background: #E8F5E9; color: #1B5E20; }
.badge-offline { background: #FFEBEE; color: #B71C1C; }

/* TABS */
.tabs { display: flex; gap: 6px; padding: 10px 10px 0; overflow-x: auto; }
.tabs::-webkit-scrollbar { display: none; }
.tab-btn { padding: 8px 16px; border-radius: 20px; border: none; font-size: 13px; font-weight: 700; font-family: 'Nunito', sans-serif; cursor: pointer; white-space: nowrap; transition: all 0.2s; background: #E8E8E8; color: var(--text); }
.tab-btn.active { background: var(--primary); color: #fff; }

/* RIDE CARD */
.ride-card { background: #fff; border-radius: 14px; padding: 14px; margin: 8px 10px; box-shadow: var(--shadow); border-left: 4px solid var(--border); }
.ride-card.pending { border-left-color: var(--yellow); }
.ride-card.accepted { border-left-color: var(--primary); }
.ride-card.completed { border-left-color: var(--green); }
.ride-card.cancelled { border-left-color: var(--red); }
.ride-card h4 { font-size: 15px; font-weight: 800; margin-bottom: 6px; }
.ride-card p { font-size: 13px; color: var(--muted); margin: 2px 0; }
.ride-card .fare { font-size: 20px; font-weight: 900; color: var(--primary); }
.route-line { display: flex; flex-direction: column; gap: 4px; background: #f8f8f8; border-radius: 10px; padding: 10px 12px; margin: 8px 0; }
.route-line .pickup { font-size: 13px; font-weight: 700; color: var(--green-dark); }
.route-line .drop { font-size: 13px; font-weight: 700; color: var(--red); }

/* DUTY TOGGLE */
.duty-toggle { background: var(--secondary); border-radius: 16px; padding: 16px; margin: 10px; display: flex; align-items: center; justify-content: space-between; }
.duty-toggle .toggle-info h3 { color: #fff; font-size: 16px; font-weight: 800; }
.duty-toggle .toggle-info p { color: rgba(255,255,255,0.5); font-size: 12px; }
.toggle-switch { position: relative; width: 56px; height: 28px; }
.toggle-switch input { opacity: 0; width: 0; height: 0; }
.toggle-slider { position: absolute; top: 0; left: 0; right: 0; bottom: 0; background: #555; border-radius: 28px; transition: 0.3s; cursor: pointer; }
.toggle-slider:before { position: absolute; content: ''; width: 22px; height: 22px; top: 3px; left: 3px; background: white; border-radius: 50%; transition: 0.3s; }
input:checked + .toggle-slider { background: var(--green); }
input:checked + .toggle-slider:before { transform: translateX(28px); }

/* EARNINGS SUMMARY */
.earnings-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin: 10px; }
.earnings-item { background: #fff; border-radius: 14px; padding: 14px; box-shadow: var(--shadow); text-align: center; }
.earnings-item .amount { font-size: 22px; font-weight: 900; color: var(--primary); }
.earnings-item .label { font-size: 12px; color: var(--muted); font-weight: 600; }

/* ADMIN PANEL */
.admin-stat-grid { display: grid; grid-template-columns: repeat(2,1fr); gap: 10px; margin: 10px; }
.stat-card { background: var(--card); border-radius: 14px; padding: 16px; box-shadow: var(--shadow); text-align: center; }
.stat-card .stat-num { font-size: 28px; font-weight: 900; color: var(--primary); }
.stat-card .stat-label { font-size: 12px; color: var(--muted); font-weight: 700; }

/* KYC UPLOAD */
.kyc-section { background: #f8f8f8; border-radius: 12px; padding: 14px; margin: 10px 0; border: 2px dashed var(--border); }
.kyc-section.uploaded { border-color: var(--green); background: #f0fff4; border-style: solid; }
.kyc-section h4 { font-size: 14px; font-weight: 800; margin-bottom: 8px; }
.kyc-section .upload-status { font-size: 12px; color: var(--muted); }

/* RATING STARS */
.stars { color: var(--yellow); letter-spacing: 2px; }
.rating-form label { font-size: 14px; }

/* SPINNER */
.spinner { display: inline-block; width: 20px; height: 20px; border: 3px solid rgba(255,255,255,0.3); border-top-color: #fff; border-radius: 50%; animation: spin 0.8s linear infinite; vertical-align: middle; }
@keyframes spin { to { transform: rotate(360deg); } }

/* TOAST */
#toast { position: fixed; bottom: 80px; left: 50%; transform: translateX(-50%) translateY(20px); background: rgba(26,26,46,0.95); color: #fff; padding: 12px 20px; border-radius: 12px; font-size: 14px; font-weight: 600; z-index: 9999; opacity: 0; transition: all 0.3s; white-space: nowrap; pointer-events: none; max-width: 90vw; text-align: center; }
#toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

/* SEARCH ANIMATION */
.searching-animation { text-align: center; padding: 40px 20px; }
.search-ring { width: 80px; height: 80px; border: 4px solid var(--border); border-top-color: var(--primary); border-radius: 50%; animation: spin 1.2s linear infinite; margin: 0 auto 16px; }

/* BOTTOM NAV */
.bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; background: #fff; border-top: 1px solid var(--border); display: flex; z-index: 99; box-shadow: 0 -4px 20px rgba(0,0,0,0.08); }
.nav-item { flex: 1; padding: 10px 4px; text-align: center; cursor: pointer; transition: color 0.2s; color: var(--muted); font-size: 10px; font-weight: 700; display: flex; flex-direction: column; align-items: center; gap: 2px; }
.nav-item.active { color: var(--primary); }
.nav-item .nav-icon { font-size: 22px; }
.page-with-nav { padding-bottom: 70px; }

/* SECTION DIVIDER */
.section-label { font-size: 11px; font-weight: 800; color: var(--muted); text-transform: uppercase; letter-spacing: 1px; padding: 8px 16px 4px; }

/* LOCATION INPUT ROW */
.location-input-wrap { position: relative; }
.location-input-wrap input { padding-right: 44px; }
.location-input-wrap .loc-icon { position: absolute; right: 12px; top: 50%; transform: translateY(-50%); font-size: 20px; cursor: pointer; }

/* PAYMENT METHODS */
.payment-row { display: flex; gap: 8px; margin: 8px 0; }
.payment-opt { flex: 1; border: 2px solid var(--border); border-radius: 12px; padding: 12px 6px; text-align: center; cursor: pointer; transition: all 0.2s; }
.payment-opt.selected { border-color: var(--primary); background: #fff3ee; }
.payment-opt .p-icon { font-size: 22px; }
.payment-opt .p-label { font-size: 12px; font-weight: 700; margin-top: 4px; }

/* SOS */
.sos-btn { background: var(--red); color: #fff; border: none; border-radius: 50%; width: 60px; height: 60px; font-size: 24px; cursor: pointer; animation: pulse-sos 2s infinite; }
@keyframes pulse-sos { 0%,100% { box-shadow: 0 0 0 0 rgba(255,61,87,0.4); } 50% { box-shadow: 0 0 0 12px rgba(255,61,87,0); } }

/* SCROLLABLE CONTENT */
.scroll-content { overflow-y: auto; -webkit-overflow-scrolling: touch; }

/* AVAILABILITY BADGE */
.avail-dot { display: inline-block; width: 10px; height: 10px; border-radius: 50%; margin-right: 5px; }
.avail-dot.online { background: var(--green); }
.avail-dot.offline { background: var(--red); }

/* Approval pending banner */
.approval-banner { background: #FFF3E0; border: 1.5px solid #FFB300; border-radius: 12px; padding: 14px; margin: 10px; }
.approval-banner h4 { color: #E65100; font-size: 15px; font-weight: 800; }
.approval-banner p { color: #BF360C; font-size: 13px; margin-top: 4px; }

/* Document preview row */
.doc-row { display: flex; align-items: center; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--border); }
.doc-row:last-child { border: none; }
.doc-label { font-size: 14px; font-weight: 700; }
.doc-status { font-size: 12px; }

/* MODAL */
.modal-overlay { position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.6); z-index: 500; display: flex; align-items: flex-end; }
.modal-sheet { background: #fff; border-radius: 24px 24px 0 0; padding: 24px 16px; width: 100%; max-height: 80vh; overflow-y: auto; animation: slideUp 0.3s ease; }
@keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
.modal-handle { width: 40px; height: 4px; background: var(--border); border-radius: 4px; margin: 0 auto 16px; }
</style>
</head>
<body>

<!-- TOAST NOTIFICATION -->
<div id="toast"></div>

<!-- ===================== SCREEN: LANDING ===================== -->
<div id="screen-landing" class="screen active">
  <div class="landing-hero">
    <div class="logo">Ride<span>Go</span></div>
    <div class="tagline">Fast · Safe · Reliable rides at your doorstep</div>
    <div class="hero-icon">🚀</div>
  </div>
  <div class="landing-cards">
    <div class="role-card" onclick="App.goUserBooking()">
      <div class="role-icon">🙋</div>
      <div class="role-info">
        <h3>Book a Ride</h3>
        <p>Find bikes, autos, cars instantly</p>
      </div>
      <div class="arrow">›</div>
    </div>
    <div class="role-card" onclick="App.showDriverLogin()">
      <div class="role-icon">🏍️</div>
      <div class="role-info">
        <h3>Driver Login</h3>
        <p>Earn money on your schedule</p>
      </div>
      <div class="arrow">›</div>
    </div>
    <div class="role-card" onclick="App.showAdminLogin()">
      <div class="role-icon">🛠</div>
      <div class="role-info">
        <h3>Admin Panel</h3>
        <p>Manage rides, drivers & payments</p>
      </div>
      <div class="arrow">›</div>
    </div>
  </div>
</div>

<!-- ===================== SCREEN: DRIVER LOGIN ===================== -->
<div id="screen-driver-login" class="screen">
  <div class="app-header">
    <div>
      <div class="app-header h1" style="font-size:18px;font-weight:800">Driver Login</div>
    </div>
    <button class="btn btn-gray btn-sm" onclick="App.showScreen('screen-landing')">← Back</button>
  </div>
  <div class="card" style="margin-top:16px">
    <div class="card-title">🏍️ Welcome Back, Driver</div>
    <label>Email</label>
    <input id="d-login-email" type="email" placeholder="driver@email.com">
    <label>Password</label>
    <input id="d-login-pass" type="password" placeholder="••••••••">
    <button class="btn btn-primary" onclick="App.driverLogin()">Login</button>
    <button class="btn btn-outline" onclick="App.showScreen('screen-driver-signup')">New Driver? Register Here</button>
    <div style="text-align:center;margin-top:8px"><span style="font-size:13px;color:var(--muted);cursor:pointer" onclick="App.forgotPassword('driver')">Forgot password?</span></div>
  </div>
</div>

<!-- ===================== SCREEN: DRIVER SIGNUP ===================== -->
<div id="screen-driver-signup" class="screen">
  <div class="app-header">
    <div style="font-size:18px;font-weight:800;color:#fff">Driver Registration</div>
    <button class="btn btn-gray btn-sm" onclick="App.showScreen('screen-driver-login')">← Back</button>
  </div>
  <div style="background:#fff3ee;padding:12px 16px;border-bottom:1px solid #ffcdb5">
    <p style="font-size:13px;color:var(--primary);font-weight:700">⏱ Account approval takes up to 48 hours after document verification</p>
  </div>
  <div class="card">
    <div class="card-title">Personal Details</div>
    <label>Full Name</label>
    <input id="s-name" placeholder="As on Aadhaar card">
    <label>Email</label>
    <input id="s-email" type="email" placeholder="your@email.com">
    <label>Phone Number</label>
    <input id="s-phone" type="tel" placeholder="+91 XXXXX XXXXX">
    <label>Password</label>
    <input id="s-pass" type="password" placeholder="Min 8 characters">
    <label>Vehicle Type</label>
    <select id="s-vehicle">
      <option value="">Select vehicle type</option>
      <option>Bike</option><option>Auto</option><option>Car</option>
      <option>Tractor</option><option>JCB</option><option>Lorry</option>
    </select>
    <label>Vehicle Number</label>
    <input id="s-vnum" placeholder="e.g. TS09AB1234">
    <label>UPI ID (for payouts)</label>
    <input id="s-upi" placeholder="name@upi or phone@bank">
    <label>Bank Account Number</label>
    <input id="s-bank-acc" placeholder="Account number">
    <label>IFSC Code</label>
    <input id="s-ifsc" placeholder="e.g. SBIN0001234">
    <label>Bank Name</label>
    <input id="s-bank-name" placeholder="e.g. State Bank of India">
  </div>
  <div class="card">
    <div class="card-title">📄 KYC Documents</div>
    <p style="font-size:13px;color:var(--muted);margin-bottom:12px">Upload photos of your documents. All are mandatory for approval.</p>
    <div class="kyc-section" id="kyc-licence">
      <h4>🪪 Driving Licence (Front & Back)</h4>
      <input type="file" id="file-licence" accept="image/*,application/pdf" onchange="App.handleFileUpload('licence', this)">
      <p class="upload-status" id="status-licence">Not uploaded</p>
    </div>
    <div class="kyc-section" id="kyc-rc">
      <h4>📋 Vehicle RC (Registration Certificate)</h4>
      <input type="file" id="file-rc" accept="image/*,application/pdf" onchange="App.handleFileUpload('rc', this)">
      <p class="upload-status" id="status-rc">Not uploaded</p>
    </div>
    <div class="kyc-section" id="kyc-aadhaar">
      <h4>🪪 Aadhaar Card (Front & Back)</h4>
      <input type="file" id="file-aadhaar" accept="image/*,application/pdf" onchange="App.handleFileUpload('aadhaar', this)">
      <p class="upload-status" id="status-aadhaar">Not uploaded</p>
    </div>
    <div class="kyc-section" id="kyc-selfie">
      <h4>🤳 Profile Selfie</h4>
      <input type="file" id="file-selfie" accept="image/*" capture="user" onchange="App.handleFileUpload('selfie', this)">
      <p class="upload-status" id="status-selfie">Not uploaded</p>
    </div>
  </div>
  <div style="padding:0 10px 16px">
    <button class="btn btn-primary" onclick="App.driverSignup()">Submit Application →</button>
    <p style="font-size:12px;color:var(--muted);text-align:center;margin-top:8px">By registering, you agree to RideGo's Terms & Privacy Policy</p>
  </div>
</div>

<!-- ===================== SCREEN: ADMIN LOGIN ===================== -->
<div id="screen-admin-login" class="screen">
  <div class="app-header">
    <div style="font-size:18px;font-weight:800;color:#fff">Admin Login</div>
    <button class="btn btn-gray btn-sm" onclick="App.showScreen('screen-landing')">← Back</button>
  </div>
  <div class="card" style="margin-top:16px">
    <div class="card-title">🛠 Admin Access</div>
    <label>Admin Email</label>
    <input id="a-login-email" type="email" placeholder="admin email">
    <label>Password</label>
    <input id="a-login-pass" type="password" placeholder="••••••••">
    <button class="btn btn-secondary" onclick="App.adminLogin()">Login as Admin</button>
  </div>
</div>

<!-- ===================== SCREEN: USER BOOKING ===================== -->
<div id="screen-user-booking" class="screen page-with-nav">
  <div class="app-header">
    <div>
      <div style="font-size:18px;font-weight:800;color:#fff">Book Ride</div>
      <div class="header-sub" id="user-location-sub">Getting your location...</div>
    </div>
    <button class="sos-btn" style="width:40px;height:40px;font-size:16px" onclick="App.triggerSOS()">SOS</button>
  </div>
  <!-- Map for Pickup -->
  <div class="map-container" id="pickup-map-container">
    <div id="pickup-map" style="width:100%;height:100%;background:#dde1e5;display:flex;align-items:center;justify-content:center;font-size:14px;color:#666">📍 Loading map...</div>
    <div class="map-pin">📍</div>
    <button class="locate-btn" onclick="App.recenterPickup()">🎯</button>
  </div>
  <div class="card" style="margin-top:0">
    <label>📍 Pickup Location</label>
    <div class="location-input-wrap">
      <input id="pickup-input" placeholder="Your pickup address" readonly>
      <span class="loc-icon" onclick="App.openMapsPickup()">🗺</span>
    </div>
    <label>🏁 Drop Location</label>
    <div class="location-input-wrap">
      <input id="drop-input" placeholder="Enter destination" oninput="App.dropInputChanged()">
      <span class="loc-icon" onclick="App.searchDropOnMaps()">🗺</span>
    </div>
    <div id="drop-suggestions" style="display:none;background:#f8f8f8;border-radius:8px;margin-top:-8px;margin-bottom:8px;overflow:hidden"></div>
  </div>
  <div class="section-label">Choose Vehicle</div>
  <div style="padding:0 10px">
    <div class="vehicle-grid" id="vehicle-grid">
      <div class="vehicle-option selected" onclick="App.selectVehicle(this,'Bike',15,'🏍️')" data-vehicle="Bike">
        <span class="v-icon">🏍️</span>
        <div class="v-name">Bike</div>
        <div class="v-price">₹15/km</div>
      </div>
      <div class="vehicle-option" onclick="App.selectVehicle(this,'Auto',20,'🛺')" data-vehicle="Auto">
        <span class="v-icon">🛺</span>
        <div class="v-name">Auto</div>
        <div class="v-price">₹20/km</div>
      </div>
      <div class="vehicle-option" onclick="App.selectVehicle(this,'Car',25,'🚗')" data-vehicle="Car">
        <span class="v-icon">🚗</span>
        <div class="v-name">Car</div>
        <div class="v-price">₹25/km</div>
      </div>
      <div class="vehicle-option" onclick="App.selectVehicle(this,'Tractor',40,'🚜')" data-vehicle="Tractor">
        <span class="v-icon">🚜</span>
        <div class="v-name">Tractor</div>
        <div class="v-price">₹40/km</div>
      </div>
      <div class="vehicle-option" onclick="App.selectVehicle(this,'JCB',80,'🏗️')" data-vehicle="JCB">
        <span class="v-icon">🏗️</span>
        <div class="v-name">JCB</div>
        <div class="v-price">₹80/km</div>
      </div>
      <div class="vehicle-option" onclick="App.selectVehicle(this,'Lorry',60,'🚛')" data-vehicle="Lorry">
        <span class="v-icon">🚛</span>
        <div class="v-name">Lorry</div>
        <div class="v-price">₹60/km</div>
      </div>
    </div>
  </div>
  <div class="card" id="fare-preview">
    <div class="fare-box">
      <div class="fare-label">Estimated Fare</div>
      <div class="fare-amount" id="fare-display">₹—</div>
      <div style="font-size:12px;color:var(--muted);margin-top:4px" id="dist-display">Enter pickup & drop to see estimate</div>
    </div>
    <label>Payment Method</label>
    <div class="payment-row">
      <div class="payment-opt selected" id="pay-cash" onclick="App.selectPayment('cash')">
        <div class="p-icon">💵</div>
        <div class="p-label">Cash</div>
      </div>
      <div class="payment-opt" id="pay-upi" onclick="App.selectPayment('upi')">
        <div class="p-icon">📱</div>
        <div class="p-label">UPI</div>
      </div>
      <div class="payment-opt" id="pay-wallet" onclick="App.selectPayment('wallet')">
        <div class="p-icon">💳</div>
        <div class="p-label">Wallet</div>
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-title">Your Details</div>
    <label>Your Name</label>
    <input id="user-name-input" placeholder="Full name">
    <label>Phone Number</label>
    <input id="user-phone-input" type="tel" placeholder="+91 XXXXX XXXXX">
    <label>Special Instructions (optional)</label>
    <textarea id="user-note" placeholder="e.g. Call on arrival, fragile goods, etc."></textarea>
    <button class="btn btn-primary" onclick="App.bookRide()" id="book-btn">🚀 Book Now</button>
  </div>
</div>

<!-- BOTTOM NAV (user) -->
<div id="user-bottom-nav" class="bottom-nav" style="display:none">
  <div class="nav-item active" onclick="App.userNav('booking')" id="unav-booking">
    <span class="nav-icon">🏠</span>Book
  </div>
  <div class="nav-item" onclick="App.userNav('rides')" id="unav-rides">
    <span class="nav-icon">🕒</span>Rides
  </div>
  <div class="nav-item" onclick="App.userNav('profile')" id="unav-profile">
    <span class="nav-icon">👤</span>Profile
  </div>
</div>

<!-- ===================== SCREEN: SEARCHING DRIVER ===================== -->
<div id="screen-searching" class="screen">
  <div class="app-header">
    <div style="font-size:18px;font-weight:800;color:#fff">Finding Driver</div>
    <button class="btn btn-red btn-sm" onclick="App.cancelSearch()">Cancel</button>
  </div>
  <div class="searching-animation">
    <div class="search-ring"></div>
    <h3 style="font-size:18px;font-weight:800;margin-bottom:8px">Searching nearby drivers</h3>
    <p style="color:var(--muted);font-size:14px" id="search-status-text">Looking for available drivers...</p>
    <div id="search-booking-summary" style="margin-top:20px"></div>
  </div>
  <div id="search-cancel-note" class="card" style="text-align:center;margin-top:20px">
    <p style="font-size:13px;color:var(--muted)">Once a driver accepts, you'll see their details here. Average wait time: 2–5 minutes</p>
  </div>
</div>

<!-- ===================== SCREEN: RIDE ACTIVE ===================== -->
<div id="screen-ride-active" class="screen">
  <div class="app-header">
    <div style="font-size:18px;font-weight:800;color:#fff">Ride In Progress</div>
    <button class="sos-btn" style="width:40px;height:40px;font-size:14px;border-radius:8px" onclick="App.triggerSOS()">SOS</button>
  </div>
  <div class="map-container">
    <div id="active-map" style="width:100%;height:100%;background:#dde1e5;display:flex;align-items:center;justify-content:center">🗺 Tracking ride...</div>
  </div>
  <div id="driver-info-section"></div>
  <div class="tracking-steps" id="tracking-steps"></div>
  <div class="card" id="active-ride-actions"></div>
</div>

<!-- ===================== SCREEN: RIDE COMPLETED (USER) ===================== -->
<div id="screen-ride-done" class="screen">
  <div style="text-align:center;padding:40px 20px 20px">
    <div style="font-size:60px">🎉</div>
    <h2 style="font-size:24px;font-weight:900;margin:12px 0">Ride Complete!</h2>
    <p style="color:var(--muted);font-size:15px">Thank you for riding with RideGo</p>
  </div>
  <div class="card">
    <div class="card-title">Ride Summary</div>
    <div id="ride-done-summary"></div>
  </div>
  <div class="card">
    <div class="card-title">⭐ Rate Your Driver</div>
    <div style="display:flex;justify-content:center;gap:8px;margin:12px 0" id="star-rating">
      <span style="font-size:32px;cursor:pointer" onclick="App.setRating(1)">☆</span>
      <span style="font-size:32px;cursor:pointer" onclick="App.setRating(2)">☆</span>
      <span style="font-size:32px;cursor:pointer" onclick="App.setRating(3)">☆</span>
      <span style="font-size:32px;cursor:pointer" onclick="App.setRating(4)">☆</span>
      <span style="font-size:32px;cursor:pointer" onclick="App.setRating(5)">☆</span>
    </div>
    <textarea id="ride-feedback" placeholder="Any feedback? (optional)"></textarea>
    <button class="btn btn-primary" onclick="App.submitRating()">Submit Rating</button>
    <button class="btn btn-gray" onclick="App.goUserBooking()">Skip & Book Another Ride</button>
  </div>
</div>

<!-- ===================== SCREEN: DRIVER DASHBOARD ===================== -->
<div id="screen-driver" class="screen page-with-nav">
  <div class="app-header">
    <div>
      <div style="font-size:18px;font-weight:800;color:#fff" id="driver-header-name">Driver Dashboard</div>
      <div class="header-sub" id="driver-header-status">Loading...</div>
    </div>
    <button class="btn btn-gray btn-sm" onclick="App.driverLogout()">Logout</button>
  </div>
  <!-- APPROVAL PENDING BANNER -->
  <div id="driver-approval-banner" style="display:none"></div>
  <!-- DUTY TOGGLE -->
  <div class="duty-toggle" id="duty-toggle-section" style="display:none">
    <div class="toggle-info">
      <h3 id="duty-label">Go Online</h3>
      <p id="duty-sublabel">Tap to start accepting rides</p>
    </div>
    <label class="toggle-switch">
      <input type="checkbox" id="duty-toggle" onchange="App.toggleDuty(this.checked)">
      <span class="toggle-slider"></span>
    </label>
  </div>
  <!-- CONTENT AREA -->
  <div id="driver-main-content"></div>
</div>

<!-- DRIVER BOTTOM NAV -->
<div id="driver-bottom-nav" class="bottom-nav" style="display:none">
  <div class="nav-item active" onclick="App.driverNav('rides')" id="dnav-rides">
    <span class="nav-icon">🏠</span>Rides
  </div>
  <div class="nav-item" onclick="App.driverNav('earnings')" id="dnav-earnings">
    <span class="nav-icon">💰</span>Earn
  </div>
  <div class="nav-item" onclick="App.driverNav('withdraw')" id="dnav-withdraw">
    <span class="nav-icon">🏧</span>Withdraw
  </div>
  <div class="nav-item" onclick="App.driverNav('profile')" id="dnav-profile">
    <span class="nav-icon">👤</span>Profile
  </div>
</div>

<!-- ===================== SCREEN: ADMIN DASHBOARD ===================== -->
<div id="screen-admin" class="screen page-with-nav">
  <div class="app-header">
    <div>
      <div style="font-size:18px;font-weight:800;color:#fff">Admin Panel</div>
      <div class="header-sub">RideGo Management</div>
    </div>
    <button class="btn btn-gray btn-sm" onclick="App.adminLogout()">Logout</button>
  </div>
  <div class="admin-stat-grid" id="admin-stats-grid"></div>
  <div class="tabs" id="admin-tabs">
    <button class="tab-btn active" onclick="App.adminTab('rides')">All Rides</button>
    <button class="tab-btn" onclick="App.adminTab('kyc')">🔍 KYC Review</button>
    <button class="tab-btn" onclick="App.adminTab('drivers')">Drivers</button>
    <button class="tab-btn" onclick="App.adminTab('withdrawals')">🏧 Withdrawals</button>
    <button class="tab-btn" onclick="App.adminTab('analytics')">📊 Analytics</button>
  </div>
  <div id="admin-content" style="padding-bottom:70px"></div>
</div>

<!-- ADMIN BOTTOM NAV -->
<div id="admin-bottom-nav" class="bottom-nav" style="display:none">
  <div class="nav-item active" onclick="App.adminTab('rides')" id="anav-rides">
    <span class="nav-icon">🚗</span>Rides
  </div>
  <div class="nav-item" onclick="App.adminTab('kyc')" id="anav-kyc">
    <span class="nav-icon">🔍</span>KYC
  </div>
  <div class="nav-item" onclick="App.adminTab('withdrawals')" id="anav-withdrawals">
    <span class="nav-icon">🏧</span>Payouts
  </div>
  <div class="nav-item" onclick="App.adminTab('analytics')" id="anav-analytics">
    <span class="nav-icon">📊</span>Stats
  </div>
</div>

<!-- ===================== USER RIDE HISTORY SCREEN ===================== -->
<div id="screen-user-rides" class="screen page-with-nav">
  <div class="app-header">
    <div style="font-size:18px;font-weight:800;color:#fff">My Rides</div>
  </div>
  <div id="user-rides-list" style="padding-top:8px"></div>
</div>

<!-- ===================== USER PROFILE SCREEN ===================== -->
<div id="screen-user-profile" class="screen page-with-nav">
  <div class="app-header">
    <div style="font-size:18px;font-weight:800;color:#fff">My Profile</div>
  </div>
  <div class="card" style="margin-top:16px;text-align:center">
    <div style="font-size:56px">👤</div>
    <h3 id="profile-name" style="margin-top:8px;font-size:18px;font-weight:800">Guest User</h3>
    <p style="color:var(--muted);font-size:13px">Total rides: <span id="profile-ride-count">0</span></p>
  </div>
  <div class="card">
    <div class="card-title">Save Your Details</div>
    <label>Name</label>
    <input id="profile-name-input" placeholder="Your name">
    <label>Phone</label>
    <input id="profile-phone-input" type="tel" placeholder="Phone number">
    <button class="btn btn-primary" onclick="App.saveUserProfile()">Save Profile</button>
  </div>
  <div class="card">
    <div class="card-title">📞 Emergency Contact</div>
    <label>Name</label>
    <input id="emer-name" placeholder="Emergency contact name">
    <label>Phone</label>
    <input id="emer-phone" type="tel" placeholder="Emergency phone">
    <button class="btn btn-outline" onclick="App.saveEmergencyContact()">Save Emergency Contact</button>
  </div>
</div>

<!-- ===================== FIREBASE + APP LOGIC ===================== -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import {
  getFirestore, collection, addDoc, onSnapshot, updateDoc,
  doc, query, where, runTransaction, setDoc, getDoc, getDocs,
  orderBy, limit, serverTimestamp, deleteDoc, increment
} from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";
import {
  getAuth, createUserWithEmailAndPassword,
  signInWithEmailAndPassword, signOut, sendPasswordResetEmail
} from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

// ─── FIREBASE INIT ──────────────────────────────────────────────
const firebaseConfig = {
  apiKey: "AIzaSyBIebPXVjzVBZl380ZCELg2LUSCLr-6QrE",
  authDomain: "neurocoin-ntc.firebaseapp.com",
  databaseURL: "https://neurocoin-ntc-default-rtdb.firebaseio.com",
  projectId: "neurocoin-ntc",
  storageBucket: "neurocoin-ntc.firebasestorage.app",
  messagingSenderId: "1040732555800",
  appId: "1:1040732555800:web:55e63b5ff81781c6b1916d"
};

const fbApp = initializeApp(firebaseConfig);
const db = getFirestore(fbApp);
const auth = getAuth(fbApp);

const ADMIN_EMAIL = "bonagirispinoj@gmail.com";
const GOOGLE_MAPS_KEY = "AIzaSyBIebPXVjzVBZl380ZCELg2LUSCLr-6QrE"; // reusing for maps

// ─── STATE ──────────────────────────────────────────────────────
let state = {
  currentUser: null,
  role: null,
  userLocation: { lat: null, lng: null, address: "" },
  selectedVehicle: { name: "Bike", rate: 15, icon: "🏍️" },
  selectedPayment: "cash",
  currentRideId: null,
  activeRideSub: null,
  driverRidesSub: null,
  driverDuty: false,
  uploadedDocs: {},
  pendingRating: null,
  userProfile: JSON.parse(localStorage.getItem("ridego_profile") || "{}"),
  userRides: [],
  currentRating: 0
};

let unsubAdmin = null;
let mapLoaded = false;

// ─── GOOGLE MAPS ────────────────────────────────────────────────
function loadGoogleMaps(callback) {
  if (mapLoaded) { callback && callback(); return; }
  const script = document.createElement("script");
  script.src = `https://maps.googleapis.com/maps/api/js?key=${GOOGLE_MAPS_KEY}&libraries=places&callback=initGoogleMaps`;
  script.async = true;
  document.head.appendChild(script);
  window.initGoogleMaps = function() {
    mapLoaded = true;
    callback && callback();
  };
}

// ─── GPS ────────────────────────────────────────────────────────
navigator.geolocation.watchPosition(
  pos => {
    state.userLocation.lat = pos.coords.latitude;
    state.userLocation.lng = pos.coords.longitude;
    reverseGeocode(pos.coords.latitude, pos.coords.longitude);
    updatePickupMap();
  },
  err => console.warn("GPS:", err.message),
  { enableHighAccuracy: true, maximumAge: 10000 }
);

async function reverseGeocode(lat, lng) {
  try {
    const r = await fetch(`https://nominatim.openstreetmap.org/reverse?lat=${lat}&lon=${lng}&format=json`);
    const d = await r.json();
    state.userLocation.address = d.display_name || `${lat.toFixed(4)}, ${lng.toFixed(4)}`;
    const el = document.getElementById("pickup-input");
    if (el && !el.value) el.value = state.userLocation.address;
    const sub = document.getElementById("user-location-sub");
    if (sub) sub.textContent = d.address?.city || d.address?.town || d.address?.village || "Location found";
    calcFare();
  } catch (e) {}
}

function updatePickupMap() {
  if (!state.userLocation.lat) return;
  const container = document.getElementById("pickup-map");
  if (!container) return;
  const lat = state.userLocation.lat;
  const lng = state.userLocation.lng;
  container.innerHTML = `<iframe src="https://maps.google.com/maps?q=${lat},${lng}&z=16&output=embed" style="width:100%;height:100%;border:none" loading="lazy"></iframe>`;
}

function calcFare() {
  const drop = document.getElementById("drop-input");
  if (!drop || !drop.value.trim() || !state.userLocation.lat) return;
  // Estimate distance (simple calculation, real app uses Directions API)
  const km = Math.floor(Math.random() * 8 + 2); // 2-10km simulated
  const base = 20;
  const fare = base + (km * state.selectedVehicle.rate);
  document.getElementById("fare-display").textContent = `₹${fare}`;
  document.getElementById("dist-display").textContent = `~${km} km • ~${Math.ceil(km*2.5)} mins`;
  state.estimatedFare = fare;
  state.estimatedKm = km;
}

// ─── TOAST ──────────────────────────────────────────────────────
function toast(msg, duration = 3000) {
  const t = document.getElementById("toast");
  t.textContent = msg;
  t.classList.add("show");
  setTimeout(() => t.classList.remove("show"), duration);
}

// ─── SCREEN MANAGEMENT ──────────────────────────────────────────
function showScreen(id) {
  document.querySelectorAll(".screen").forEach(s => s.classList.remove("active"));
  const el = document.getElementById(id);
  if (el) { el.classList.add("active"); el.scrollTop = 0; }
  // Show/hide nav bars
  document.getElementById("user-bottom-nav").style.display = "none";
  document.getElementById("driver-bottom-nav").style.display = "none";
  document.getElementById("admin-bottom-nav").style.display = "none";
  if (id === "screen-user-booking" || id === "screen-user-rides" || id === "screen-user-profile") {
    document.getElementById("user-bottom-nav").style.display = "flex";
  } else if (id === "screen-driver") {
    document.getElementById("driver-bottom-nav").style.display = "flex";
  } else if (id === "screen-admin") {
    document.getElementById("admin-bottom-nav").style.display = "flex";
  }
}

// ─── APP OBJECT (global) ────────────────────────────────────────
window.App = {
  showScreen,
  goUserBooking: function() {
    showScreen("screen-user-booking");
    updatePickupMap();
    if (state.userProfile.name) document.getElementById("user-name-input").value = state.userProfile.name;
    if (state.userProfile.phone) document.getElementById("user-phone-input").value = state.userProfile.phone;
  },
  showDriverLogin: function() { showScreen("screen-driver-login"); },
  showAdminLogin: function() { showScreen("screen-admin-login"); },

  // ─── VEHICLE SELECT
  selectVehicle: function(el, name, rate, icon) {
    document.querySelectorAll(".vehicle-option").forEach(v => v.classList.remove("selected"));
    el.classList.add("selected");
    state.selectedVehicle = { name, rate, icon };
    calcFare();
  },

  // ─── PAYMENT SELECT
  selectPayment: function(method) {
    state.selectedPayment = method;
    document.querySelectorAll(".payment-opt").forEach(p => p.classList.remove("selected"));
    document.getElementById(`pay-${method}`).classList.add("selected");
  },

  // ─── LOCATION: MAP PICKUP
  openMapsPickup: function() {
    const lat = state.userLocation.lat;
    const lng = state.userLocation.lng;
    if (lat) {
      window.open(`https://maps.google.com?q=${lat},${lng}`, "_blank");
    } else {
      toast("📍 Getting your location...");
    }
  },

  recenterPickup: function() {
    updatePickupMap();
    if (state.userLocation.lat) {
      reverseGeocode(state.userLocation.lat, state.userLocation.lng);
    }
  },

  // ─── DROP LOCATION AUTOCOMPLETE (Nominatim)
  dropInputChanged: async function() {
    const val = document.getElementById("drop-input").value.trim();
    const suggestionsEl = document.getElementById("drop-suggestions");
    if (val.length < 3) { suggestionsEl.style.display = "none"; return; }
    try {
      const r = await fetch(`https://nominatim.openstreetmap.org/search?q=${encodeURIComponent(val)}&format=json&limit=5&countrycodes=in`);
      const results = await r.json();
      if (!results.length) { suggestionsEl.style.display = "none"; return; }
      suggestionsEl.style.display = "block";
      suggestionsEl.innerHTML = results.map(r =>
        `<div style="padding:10px 14px;cursor:pointer;border-bottom:1px solid #eee;font-size:14px" onclick="App.selectDropSuggestion('${r.display_name.replace(/'/g,"\\'")}','${r.lat}','${r.lon}')">📍 ${r.display_name}</div>`
      ).join("");
    } catch (e) {}
    calcFare();
  },

  selectDropSuggestion: function(name, lat, lng) {
    document.getElementById("drop-input").value = name;
    document.getElementById("drop-suggestions").style.display = "none";
    state.dropLocation = { address: name, lat: parseFloat(lat), lng: parseFloat(lng) };
    calcFare();
  },

  searchDropOnMaps: function() {
    const drop = document.getElementById("drop-input").value;
    if (drop) {
      window.open(`https://maps.google.com?q=${encodeURIComponent(drop)}`, "_blank");
    }
  },

  // ─── BOOK RIDE
  bookRide: async function() {
    const pickup = document.getElementById("pickup-input").value.trim();
    const drop = document.getElementById("drop-input").value.trim();
    const name = document.getElementById("user-name-input").value.trim();
    const phone = document.getElementById("user-phone-input").value.trim();
    const note = document.getElementById("user-note").value.trim();

    if (!pickup) return toast("📍 Could not get your pickup location. Please wait for GPS.");
    if (!drop) return toast("🏁 Please enter drop location");
    if (!name) return toast("👤 Please enter your name");
    if (!phone || phone.length < 10) return toast("📞 Please enter a valid phone number");

    const fare = state.estimatedFare || (20 + state.selectedVehicle.rate * 5);
    const km = state.estimatedKm || 5;

    const btn = document.getElementById("book-btn");
    btn.innerHTML = '<span class="spinner"></span> Booking...';
    btn.disabled = true;

    try {
      const rideRef = await addDoc(collection(db, "rides"), {
        userName: name,
        userPhone: phone,
        userNote: note,
        vehicle: state.selectedVehicle.name,
        vehicleIcon: state.selectedVehicle.icon,
        pickup: pickup,
        drop: drop,
        pickupLat: state.userLocation.lat,
        pickupLng: state.userLocation.lng,
        dropLat: state.dropLocation?.lat || null,
        dropLng: state.dropLocation?.lng || null,
        fare: fare,
        estimatedKm: km,
        paymentMethod: state.selectedPayment,
        status: "pending",
        createdAt: new Date().toISOString(),
        driverEmail: null,
        driverUid: null,
        driverName: null,
        driverPhone: null,
        rating: null,
        feedback: null
      });

      state.currentRideId = rideRef.id;
      // Save profile
      state.userProfile = { name, phone };
      localStorage.setItem("ridego_profile", JSON.stringify(state.userProfile));

      showScreen("screen-searching");
      document.getElementById("search-booking-summary").innerHTML = `
        <div class="card" style="margin:0;text-align:left">
          <p><b>${state.selectedVehicle.icon} ${state.selectedVehicle.name}</b></p>
          <p style="font-size:22px;font-weight:900;color:var(--primary)">₹${fare}</p>
          <p style="font-size:13px;color:var(--muted)">📍 ${pickup}</p>
          <p style="font-size:13px;color:var(--muted)">🏁 ${drop}</p>
          <p style="font-size:13px;color:var(--muted)">💳 ${state.selectedPayment.toUpperCase()}</p>
        </div>
      `;
      App.watchRideStatus(rideRef.id, fare, { pickup, drop, vehicle: state.selectedVehicle.name, vehicleIcon: state.selectedVehicle.icon });

    } catch (err) {
      toast("❌ Booking failed: " + err.message);
    }
    btn.innerHTML = "🚀 Book Now";
    btn.disabled = false;
  },

  // ─── WATCH RIDE STATUS (for user)
  watchRideStatus: function(rideId, fare, rideInfo) {
    if (state.activeRideSub) state.activeRideSub();
    let timerOut = setTimeout(() => {
      toast("⏱ No drivers available right now. Try again.");
      showScreen("screen-user-booking");
    }, 5 * 60 * 1000); // 5 min timeout

    state.activeRideSub = onSnapshot(doc(db, "rides", rideId), (snap) => {
      if (!snap.exists()) return;
      const data = snap.data();
      if (data.status === "accepted" || data.status === "arriving") {
        clearTimeout(timerOut);
        showScreen("screen-ride-active");
        App.renderActiveRide(rideId, data, rideInfo);
      } else if (data.status === "completed") {
        clearTimeout(timerOut);
        showScreen("screen-ride-done");
        state.pendingRating = { rideId, driverUid: data.driverUid, driverName: data.driverName };
        document.getElementById("ride-done-summary").innerHTML = `
          <div class="fare-box">
            <div class="fare-label">Total Fare</div>
            <div class="fare-amount">₹${data.fare}</div>
            <div style="font-size:13px;color:var(--muted);margin-top:4px">${data.paymentMethod?.toUpperCase() || "CASH"}</div>
          </div>
          <p style="font-size:13px;margin-top:10px">🚗 Driver: <b>${data.driverName || "—"}</b></p>
          <p style="font-size:13px">📍 ${data.pickup} → ${data.drop}</p>
        `;
      } else if (data.status === "cancelled") {
        clearTimeout(timerOut);
        toast("❌ Ride was cancelled.");
        showScreen("screen-user-booking");
      }
    });
  },

  cancelSearch: async function() {
    if (state.currentRideId) {
      await updateDoc(doc(db, "rides", state.currentRideId), { status: "cancelled" });
    }
    if (state.activeRideSub) state.activeRideSub();
    showScreen("screen-user-booking");
  },

  renderActiveRide: function(rideId, data, rideInfo) {
    const mapDiv = document.getElementById("active-map");
    if (data.driverLat && data.driverLng) {
      mapDiv.innerHTML = `<iframe src="https://maps.google.com/maps?q=${data.driverLat},${data.driverLng}&z=15&output=embed" style="width:100%;height:100%;border:none" loading="lazy"></iframe>`;
    } else {
      mapDiv.innerHTML = `<iframe src="https://maps.google.com/maps?q=${data.pickupLat || ''},${data.pickupLng || ''}&z=15&output=embed" style="width:100%;height:100%;border:none" loading="lazy"></iframe>`;
    }

    document.getElementById("driver-info-section").innerHTML = `
      <div class="driver-info-card">
        <div style="display:flex;align-items:center;gap:14px">
          <div class="driver-avatar">${data.vehicleIcon || "🚗"}</div>
          <div style="flex:1">
            <div class="d-name">${data.driverName || "Your Driver"}</div>
            <div class="d-detail">${data.vehicle} • ${data.driverVehicleNum || ""}</div>
            <div class="d-rating">★ ${data.driverRating || "New"}</div>
          </div>
          <div style="text-align:right">
            <div style="font-size:22px;font-weight:900;color:var(--primary)">₹${data.fare}</div>
            <div style="font-size:11px;opacity:0.6">${(data.paymentMethod||"cash").toUpperCase()}</div>
          </div>
        </div>
        <div class="contact-row">
          <button class="contact-btn" onclick="window.open('tel:${data.driverPhone}')">📞 Call Driver</button>
          <button class="contact-btn" onclick="window.open('https://wa.me/91${data.driverPhone}')">💬 WhatsApp</button>
          <button class="contact-btn" onclick="App.shareRide('${rideId}')">🔗 Share</button>
        </div>
      </div>
    `;

    document.getElementById("tracking-steps").innerHTML = `
      <div class="tracking-step">
        <div class="step-dot done">✓</div>
        <div class="step-info"><h4>Ride Booked</h4><p>Your booking was confirmed</p></div>
      </div>
      <div class="tracking-step">
        <div class="step-dot done">✓</div>
        <div class="step-info"><h4>Driver Assigned</h4><p>${data.driverName || "Driver"} is coming</p></div>
      </div>
      <div class="tracking-step">
        <div class="step-dot active">🏍</div>
        <div class="step-info"><h4>On the Way</h4><p>Driver heading to pickup</p></div>
      </div>
      <div class="tracking-step">
        <div class="step-dot pending">🏁</div>
        <div class="step-info"><h4>Ride in Progress</h4><p>On the way to drop</p></div>
      </div>
    `;

    document.getElementById("active-ride-actions").innerHTML = `
      <div style="display:flex;gap:8px">
        <button class="btn btn-gray" style="flex:1" onclick="App.cancelActiveRide('${rideId}')">Cancel Ride</button>
        <button class="btn btn-red" style="flex:1;width:auto" onclick="App.triggerSOS()">🆘 SOS</button>
      </div>
      <p style="font-size:12px;color:var(--muted);text-align:center;margin-top:8px">Share ride tracking with family for safety</p>
    `;
  },

  cancelActiveRide: async function(rideId) {
    if (!confirm("Cancel this ride? Cancellation charges may apply.")) return;
    await updateDoc(doc(db, "rides", rideId), { status: "cancelled" });
    if (state.activeRideSub) state.activeRideSub();
    toast("Ride cancelled.");
    showScreen("screen-user-booking");
  },

  shareRide: function(rideId) {
    const text = `Track my RideGo ride: Ride ID ${rideId}`;
    if (navigator.share) {
      navigator.share({ title: "RideGo Ride", text });
    } else {
      navigator.clipboard.writeText(text);
      toast("📋 Ride info copied!");
    }
  },

  triggerSOS: function() {
    const emer = JSON.parse(localStorage.getItem("ridego_emergency") || "{}");
    if (emer.phone) {
      window.open(`tel:${emer.phone}`);
    } else {
      if (confirm("Call emergency services (112)?")) window.open("tel:112");
    }
  },

  setRating: function(stars) {
    state.currentRating = stars;
    const starsEl = document.getElementById("star-rating");
    if (starsEl) {
      const spans = starsEl.querySelectorAll("span");
      spans.forEach((s, i) => { s.textContent = i < stars ? "⭐" : "☆"; });
    }
  },

  submitRating: async function() {
    if (!state.pendingRating) { App.goUserBooking(); return; }
    const feedback = document.getElementById("ride-feedback")?.value || "";
    const stars = state.currentRating;
    if (!stars) { toast("Please select a star rating"); return; }
    try {
      await updateDoc(doc(db, "rides", state.pendingRating.rideId), { rating: stars, feedback });
      // Update driver's average rating
      if (state.pendingRating.driverUid) {
        const driverRef = doc(db, "users", state.pendingRating.driverUid);
        const driverSnap = await getDoc(driverRef);
        if (driverSnap.exists()) {
          const d = driverSnap.data();
          const totalRatings = (d.totalRatings || 0) + 1;
          const sumRatings = (d.sumRatings || 0) + stars;
          await updateDoc(driverRef, {
            totalRatings,
            sumRatings,
            avgRating: (sumRatings / totalRatings).toFixed(1)
          });
        }
      }
      toast("⭐ Thanks for the rating!");
    } catch (e) {}
    App.goUserBooking();
  },

  // ─── USER HISTORY + PROFILE NAV
  userNav: function(tab) {
    document.querySelectorAll("#user-bottom-nav .nav-item").forEach(n => n.classList.remove("active"));
    document.getElementById(`unav-${tab}`).classList.add("active");
    if (tab === "booking") App.goUserBooking();
    else if (tab === "rides") App.showUserRides();
    else if (tab === "profile") App.showUserProfile();
  },

  showUserRides: async function() {
    showScreen("screen-user-rides");
    document.getElementById("user-rides-list").innerHTML = "<div style='text-align:center;padding:30px;color:var(--muted)'>Loading...</div>";
    const phone = state.userProfile.phone;
    if (!phone) {
      document.getElementById("user-rides-list").innerHTML = "<div class='card' style='text-align:center'>Save your profile to see ride history</div>";
      return;
    }
    const q = query(collection(db, "rides"), where("userPhone", "==", phone), orderBy("createdAt", "desc"), limit(20));
    const snap = await getDocs(q);
    if (snap.empty) {
      document.getElementById("user-rides-list").innerHTML = "<div class='card' style='text-align:center;color:var(--muted)'>No rides found</div>";
      return;
    }
    let html = "";
    snap.forEach(d => {
      const data = d.data();
      html += `<div class="ride-card ${data.status}">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px">
          <span>${data.vehicleIcon || "🚗"} <b>${data.vehicle}</b></span>
          <span class="badge badge-${data.status}">${data.status}</span>
        </div>
        <div class="fare">₹${data.fare}</div>
        <div class="route-line"><div class="pickup">📍 ${data.pickup}</div><div class="drop">🏁 ${data.drop}</div></div>
        <p>${new Date(data.createdAt).toLocaleDateString("en-IN", {day:"numeric",month:"short",year:"numeric",hour:"2-digit",minute:"2-digit"})}</p>
        ${data.rating ? `<p>⭐ ${data.rating}/5</p>` : ""}
      </div>`;
    });
    document.getElementById("user-rides-list").innerHTML = html;
  },

  showUserProfile: function() {
    showScreen("screen-user-profile");
    if (state.userProfile.name) {
      document.getElementById("profile-name").textContent = state.userProfile.name;
      document.getElementById("profile-name-input").value = state.userProfile.name;
    }
    if (state.userProfile.phone) {
      document.getElementById("profile-phone-input").value = state.userProfile.phone;
    }
    const emer = JSON.parse(localStorage.getItem("ridego_emergency") || "{}");
    if (emer.name) document.getElementById("emer-name").value = emer.name;
    if (emer.phone) document.getElementById("emer-phone").value = emer.phone;
  },

  saveUserProfile: function() {
    const name = document.getElementById("profile-name-input").value.trim();
    const phone = document.getElementById("profile-phone-input").value.trim();
    if (!name || !phone) return toast("Enter name and phone");
    state.userProfile = { name, phone };
    localStorage.setItem("ridego_profile", JSON.stringify(state.userProfile));
    document.getElementById("profile-name").textContent = name;
    toast("✅ Profile saved!");
  },

  saveEmergencyContact: function() {
    const name = document.getElementById("emer-name").value.trim();
    const phone = document.getElementById("emer-phone").value.trim();
    if (!name || !phone) return toast("Enter emergency contact details");
    localStorage.setItem("ridego_emergency", JSON.stringify({ name, phone }));
    toast("✅ Emergency contact saved!");
  },

  // ─── DRIVER LOGIN
  driverLogin: async function() {
    const email = document.getElementById("d-login-email").value.trim();
    const pass = document.getElementById("d-login-pass").value;
    if (!email || !pass) return toast("Enter email and password");
    const btn = document.querySelector("#screen-driver-login .btn-primary");
    btn.innerHTML = '<span class="spinner"></span>';
    try {
      const cred = await signInWithEmailAndPassword(auth, email, pass);
      const snap = await getDoc(doc(db, "users", cred.user.uid));
      if (!snap.exists()) {
        await signOut(auth);
        return toast("❌ Account not found. Please register.");
      }
      const userData = snap.data();
      if (userData.role !== "driver") {
        await signOut(auth);
        return toast("❌ This is not a driver account.");
      }
      state.currentUser = { ...userData, uid: cred.user.uid };
      state.role = "driver";
      App.loadDriverDashboard();
    } catch (err) {
      toast("❌ " + err.message.replace("Firebase: ", "").replace("(auth/wrong-password)", "Wrong password").replace("(auth/user-not-found)", "Email not found"));
    }
    btn.textContent = "Login";
  },

  // ─── DRIVER SIGNUP
  driverSignup: async function() {
    const name = document.getElementById("s-name").value.trim();
    const email = document.getElementById("s-email").value.trim();
    const phone = document.getElementById("s-phone").value.trim();
    const pass = document.getElementById("s-pass").value;
    const vehicle = document.getElementById("s-vehicle").value;
    const vnum = document.getElementById("s-vnum").value.trim();
    const upi = document.getElementById("s-upi").value.trim();
    const bankAcc = document.getElementById("s-bank-acc").value.trim();
    const ifsc = document.getElementById("s-ifsc").value.trim();
    const bankName = document.getElementById("s-bank-name").value.trim();

    if (!name || !email || !phone || !pass) return toast("Fill all personal details");
    if (pass.length < 8) return toast("Password must be at least 8 characters");
    if (!vehicle) return toast("Select vehicle type");
    if (!vnum) return toast("Enter vehicle number");
    if (!upi) return toast("Enter UPI ID for payments");
    if (!bankAcc || !ifsc) return toast("Enter bank account details");
    if (!state.uploadedDocs.licence) return toast("Upload Driving Licence");
    if (!state.uploadedDocs.rc) return toast("Upload Vehicle RC");
    if (!state.uploadedDocs.aadhaar) return toast("Upload Aadhaar Card");
    if (!state.uploadedDocs.selfie) return toast("Upload a selfie photo");

    try {
      const cred = await createUserWithEmailAndPassword(auth, email, pass);
      await setDoc(doc(db, "users", cred.user.uid), {
        uid: cred.user.uid,
        name, email, phone, role: "driver",
        vehicle, vehicleNum: vnum, upiId: upi,
        bankAccount: bankAcc, ifsc, bankName,
        documents: state.uploadedDocs,
        approvalStatus: "pending",
        isOnDuty: false,
        earnings: 0, withdrawn: 0,
        totalRides: 0, totalRatings: 0, sumRatings: 0, avgRating: "New",
        joinedAt: new Date().toISOString()
      });
      await signOut(auth);
      toast("✅ Application submitted! Approval within 48 hours.");
      showScreen("screen-driver-login");
    } catch (err) {
      toast("❌ " + err.message.replace("Firebase: ", ""));
    }
  },

  handleFileUpload: function(docType, input) {
    if (!input.files[0]) return;
    const file = input.files[0];
    if (file.size > 5 * 1024 * 1024) { toast("File too large. Max 5MB."); return; }
    const reader = new FileReader();
    reader.onload = function(e) {
      state.uploadedDocs[docType] = { name: file.name, type: file.type, data: e.target.result.substring(0, 200) + "...[stored]" };
      // Store full base64 separately
      state.uploadedDocs[docType + "_full"] = e.target.result;
      const statusEl = document.getElementById(`status-${docType}`);
      const sectionEl = document.getElementById(`kyc-${docType}`);
      if (statusEl) statusEl.textContent = `✅ ${file.name}`;
      if (sectionEl) sectionEl.classList.add("uploaded");
    };
    reader.readAsDataURL(file);
  },

  // ─── DRIVER DASHBOARD LOAD
  loadDriverDashboard: function() {
    showScreen("screen-driver");
    const driver = state.currentUser;
    document.getElementById("driver-header-name").textContent = driver.name || driver.email;
    document.getElementById("driver-header-status").textContent = `${driver.vehicle} • ${driver.vehicleNum || ""}`;

    if (driver.approvalStatus !== "approved") {
      document.getElementById("driver-approval-banner").style.display = "block";
      document.getElementById("driver-approval-banner").innerHTML = `
        <div class="approval-banner">
          <h4>⏳ ${driver.approvalStatus === "pending" ? "Application Under Review" : "Application Rejected"}</h4>
          <p>${driver.approvalStatus === "pending"
            ? "Your documents are being reviewed. Approval takes up to 48 hours. You'll be able to accept rides once approved."
            : "Your application was rejected. Please contact support or re-apply with correct documents."}</p>
          ${driver.approvalStatus === "rejected" ? `<button class="btn btn-outline btn-sm" style="margin-top:8px" onclick="App.showScreen('screen-driver-signup')">Re-apply</button>` : ""}
        </div>
      `;
      document.getElementById("duty-toggle-section").style.display = "none";
      document.getElementById("driver-main-content").innerHTML = `
        <div class="card" style="text-align:center;padding:30px">
          <div style="font-size:48px">⏳</div>
          <h3 style="margin:12px 0">Awaiting Approval</h3>
          <p style="color:var(--muted);font-size:14px">Your documents are under verification. You'll receive a confirmation once approved.</p>
        </div>
      `;
    } else {
      document.getElementById("duty-toggle-section").style.display = "flex";
      document.getElementById("duty-toggle").checked = driver.isOnDuty || false;
      state.driverDuty = driver.isOnDuty || false;
      App.updateDutyLabel(state.driverDuty);
      App.driverNav("rides");
    }
  },

  toggleDuty: async function(isOn) {
    state.driverDuty = isOn;
    await updateDoc(doc(db, "users", state.currentUser.uid), { isOnDuty: isOn });
    App.updateDutyLabel(isOn);
    toast(isOn ? "🟢 You're now Online — Ready to accept rides!" : "🔴 You're Offline");
    if (isOn) App.driverNav("rides");
    else {
      document.getElementById("driver-main-content").innerHTML = `
        <div class="card" style="text-align:center;padding:30px">
          <div style="font-size:48px">😴</div>
          <h3 style="margin:12px 0">You're Offline</h3>
          <p style="color:var(--muted);font-size:14px">Toggle the switch above to go online and accept rides</p>
        </div>
      `;
    }
  },

  updateDutyLabel: function(isOn) {
    document.getElementById("duty-label").textContent = isOn ? "You're Online" : "You're Offline";
    document.getElementById("duty-sublabel").textContent = isOn ? "Accepting rides" : "Tap to go online";
  },

  // ─── DRIVER NAVIGATION
  driverNav: function(tab) {
    document.querySelectorAll("#driver-bottom-nav .nav-item").forEach(n => n.classList.remove("active"));
    const el = document.getElementById(`dnav-${tab}`);
    if (el) el.classList.add("active");
    if (tab === "rides") App.loadDriverRides();
    else if (tab === "earnings") App.loadDriverEarnings();
    else if (tab === "withdraw") App.loadDriverWithdraw();
    else if (tab === "profile") App.loadDriverProfile();
  },

  loadDriverRides: function() {
    if (!state.driverDuty) {
      document.getElementById("driver-main-content").innerHTML = `
        <div class="card" style="text-align:center;padding:30px">
          <div style="font-size:48px">😴</div>
          <h3 style="margin:12px 0">You're Offline</h3>
          <p style="color:var(--muted);font-size:14px">Go online to start accepting rides</p>
        </div>
      `;
      return;
    }
    if (state.driverRidesSub) state.driverRidesSub();
    const q = query(collection(db, "rides"), where("status", "in", ["pending", "accepted"]));
    state.driverRidesSub = onSnapshot(q, snap => {
      let html = "";
      let hasActive = false;
      snap.forEach(d => {
        const data = d.data(); const id = d.id;
        if (data.status === "accepted" && data.driverUid !== state.currentUser.uid) return;
        if (data.status === "accepted" && data.driverUid === state.currentUser.uid) {
          hasActive = true;
          html = `<div class="ride-card accepted" style="margin-bottom:0">
            <div style="display:flex;justify-content:space-between;margin-bottom:8px">
              <span>✅ <b>Active Ride</b></span>
              <span class="badge badge-accepted">In Progress</span>
            </div>
            <div class="fare">₹${data.fare}</div>
            <div class="route-line">
              <div class="pickup">📍 ${data.pickup}</div>
              <div class="drop">🏁 ${data.drop}</div>
            </div>
            <p style="font-size:13px;color:var(--muted)">👤 ${data.userName} • 📞 ${data.userPhone}</p>
            ${data.userNote ? `<p style="font-size:13px;color:var(--muted)">📝 ${data.userNote}</p>` : ""}
            <div style="display:flex;gap:8px;margin-top:10px">
              <button class="btn btn-gray btn-sm" style="flex:1" onclick="window.open('tel:${data.userPhone}')">📞 Call</button>
              <button class="btn btn-gray btn-sm" style="flex:1" onclick="App.openNav('${data.pickup}','${data.drop}')">🗺 Navigate</button>
              <button class="btn btn-green btn-sm" style="flex:1" onclick="App.completeRide('${id}',${data.fare})">✅ Done</button>
            </div>
          </div>` + html;
        } else if (data.status === "pending") {
          html += `<div class="ride-card pending">
            <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px">
              <span>${data.vehicleIcon || "🚗"} <b>${data.vehicle}</b></span>
              <span class="fare">₹${data.fare}</span>
            </div>
            <div class="route-line">
              <div class="pickup">📍 ${data.pickup}</div>
              <div class="drop">🏁 ${data.drop}</div>
            </div>
            <p style="font-size:13px;color:var(--muted)">👤 ${data.userName} • ~${data.estimatedKm || "?"}km • ${(data.paymentMethod||"cash").toUpperCase()}</p>
            ${data.userNote ? `<p style="font-size:13px;color:var(--muted)">📝 ${data.userNote}</p>` : ""}
            <div style="display:flex;gap:8px;margin-top:10px">
              <button class="btn btn-red btn-sm" style="flex:1" onclick="App.declineRide('${id}')">✗ Decline</button>
              <button class="btn btn-green btn-sm" style="flex:1;padding:10px" onclick="App.acceptRide('${id}')">✓ Accept Ride</button>
            </div>
          </div>`;
        }
      });
      document.getElementById("driver-main-content").innerHTML = html ||
        `<div class="card" style="text-align:center;padding:30px;color:var(--muted)"><div style="font-size:40px">🔍</div><p style="margin-top:12px">No rides available nearby.<br>Stay online to get requests.</p></div>`;
    });
  },

  openNav: function(pickup, drop) {
    const url = `https://maps.google.com/maps?saddr=${encodeURIComponent(pickup)}&daddr=${encodeURIComponent(drop)}`;
    window.open(url, "_blank");
  },

  acceptRide: async function(rideId) {
    try {
      await runTransaction(db, async (t) => {
        const ref = doc(db, "rides", rideId);
        const ride = await t.get(ref);
        if (!ride.exists() || ride.data().status !== "pending") throw new Error("Ride no longer available");
        t.update(ref, {
          status: "accepted",
          driverEmail: state.currentUser.email,
          driverUid: state.currentUser.uid,
          driverName: state.currentUser.name,
          driverPhone: state.currentUser.phone,
          driverVehicleNum: state.currentUser.vehicleNum,
          driverRating: state.currentUser.avgRating || "New",
          acceptedAt: new Date().toISOString()
        });
      });
      toast("✅ Ride accepted!");
    } catch (err) { toast("❌ " + err.message); }
  },

  declineRide: function(rideId) {
    // Just ignore (don't accept)
    toast("Ride declined.");
  },

  completeRide: async function(rideId, fare) {
    try {
      await updateDoc(doc(db, "rides", rideId), {
        status: "completed",
        completedAt: new Date().toISOString()
      });
      // Add earnings to driver
      await updateDoc(doc(db, "users", state.currentUser.uid), {
        earnings: increment(fare),
        totalRides: increment(1)
      });
      toast(`🎉 Ride complete! ₹${fare} added to earnings.`);
    } catch (err) { toast("❌ " + err.message); }
  },

  loadDriverEarnings: async function() {
    const content = document.getElementById("driver-main-content");
    content.innerHTML = "<div style='text-align:center;padding:30px;color:var(--muted)'>Loading...</div>";

    const q = query(collection(db, "rides"), where("driverUid", "==", state.currentUser.uid), where("status", "==", "completed"));
    const snap = await getDocs(q);
    let total = 0; let html = "";
    snap.forEach(d => {
      const data = d.data();
      total += data.fare || 0;
      html += `<div class="ride-card completed">
        <div style="display:flex;justify-content:space-between">
          <span>${data.vehicleIcon || "🚗"} ${data.vehicle}</span>
          <span class="fare" style="font-size:16px">₹${data.fare}</span>
        </div>
        <div class="route-line" style="margin:6px 0">
          <div class="pickup">📍 ${data.pickup}</div>
          <div class="drop">🏁 ${data.drop}</div>
        </div>
        <p style="font-size:12px;color:var(--muted)">${data.completedAt ? new Date(data.completedAt).toLocaleDateString("en-IN",{day:"numeric",month:"short",hour:"2-digit",minute:"2-digit"}) : ""}</p>
        ${data.rating ? `<p style="font-size:13px">⭐ ${data.rating}/5 ${data.feedback ? `• "${data.feedback}"` : ""}</p>` : ""}
      </div>`;
    });

    const wq = query(collection(db, "withdrawals"), where("driverUid", "==", state.currentUser.uid), where("wstatus", "==", "approved"));
    const wSnap = await getDocs(wq);
    let withdrawn = 0;
    wSnap.forEach(d => { withdrawn += d.data().amount || 0; });

    content.innerHTML = `
      <div class="earnings-grid">
        <div class="earnings-item"><div class="amount">₹${total}</div><div class="label">Total Earned</div></div>
        <div class="earnings-item"><div class="amount">₹${total - withdrawn}</div><div class="label">Available</div></div>
        <div class="earnings-item"><div class="amount">${snap.size}</div><div class="label">Rides Done</div></div>
        <div class="earnings-item"><div class="amount">₹${withdrawn}</div><div class="label">Withdrawn</div></div>
      </div>
      <div class="section-label">Ride History</div>
      ${html || "<div class='card' style='text-align:center;color:var(--muted)'>No completed rides yet</div>"}
    `;
  },

  loadDriverWithdraw: async function() {
    const content = document.getElementById("driver-main-content");
    content.innerHTML = "<div style='text-align:center;padding:30px;color:var(--muted)'>Loading...</div>";

    const driverSnap = await getDoc(doc(db, "users", state.currentUser.uid));
    const driver = driverSnap.data();

    const q = query(collection(db, "rides"), where("driverUid", "==", state.currentUser.uid), where("status", "==", "completed"));
    const snap = await getDocs(q);
    let totalEarned = 0;
    snap.forEach(d => { totalEarned += d.data().fare || 0; });

    const wq = query(collection(db, "withdrawals"), where("driverUid", "==", state.currentUser.uid), where("wstatus", "==", "approved"));
    const wSnap = await getDocs(wq);
    let withdrawn = 0;
    wSnap.forEach(d => { withdrawn += d.data().amount || 0; });

    const available = totalEarned - withdrawn;

    const allWq = query(collection(db, "withdrawals"), where("driverUid", "==", state.currentUser.uid), orderBy("requestedAt", "desc"));
    const allW = await getDocs(allWq);
    let wHistory = "";
    allW.forEach(d => {
      const w = d.data();
      wHistory += `<div class="ride-card" style="margin:8px 10px">
        <div style="display:flex;justify-content:space-between">
          <span style="font-size:16px;font-weight:800">₹${w.amount}</span>
          <span class="badge badge-${w.wstatus}">${w.wstatus}</span>
        </div>
        <p>UPI: ${w.upiId}</p>
        <p style="font-size:12px;color:var(--muted)">${w.requestedAt ? new Date(w.requestedAt).toLocaleDateString("en-IN") : ""}</p>
      </div>`;
    });

    content.innerHTML = `
      <div class="card" style="background:linear-gradient(135deg,var(--secondary),var(--accent));color:#fff">
        <div style="font-size:13px;opacity:0.7">Available Balance</div>
        <div style="font-size:34px;font-weight:900;margin:4px 0">₹${available}</div>
        <div style="font-size:12px;opacity:0.6">Earned: ₹${totalEarned} • Withdrawn: ₹${withdrawn}</div>
      </div>
      <div class="card">
        <div class="card-title">Request Withdrawal</div>
        <label>UPI ID</label>
        <input id="w-upi" value="${driver.upiId || ""}" placeholder="yourname@upi">
        <label>Amount (₹)</label>
        <input id="w-amount" type="number" placeholder="Min ₹100" max="${available}">
        <p style="font-size:12px;color:var(--muted)">Available: ₹${available} • Min withdrawal: ₹100</p>
        <button class="btn btn-primary" onclick="App.requestWithdrawal(${available})">📤 Request Withdrawal</button>
      </div>
      <div class="section-label">Withdrawal History</div>
      ${wHistory || "<div style='text-align:center;padding:20px;color:var(--muted)'>No withdrawals yet</div>"}
    `;
  },

  requestWithdrawal: async function(available) {
    const amount = parseInt(document.getElementById("w-amount").value);
    const upi = document.getElementById("w-upi").value.trim();
    if (!amount || amount < 100) return toast("Minimum withdrawal is ₹100");
    if (amount > available) return toast("Exceeds available balance ₹" + available);
    if (!upi) return toast("Enter your UPI ID");
    try {
      await addDoc(collection(db, "withdrawals"), {
        driverEmail: state.currentUser.email,
        driverUid: state.currentUser.uid,
        driverName: state.currentUser.name,
        upiId: upi,
        amount,
        wstatus: "pending",
        requestedAt: new Date().toISOString()
      });
      // Update UPI in profile
      await updateDoc(doc(db, "users", state.currentUser.uid), { upiId: upi });
      toast(`✅ Withdrawal request of ₹${amount} submitted!`);
      App.loadDriverWithdraw();
    } catch (err) { toast("❌ " + err.message); }
  },

  loadDriverProfile: async function() {
    const content = document.getElementById("driver-main-content");
    const driver = state.currentUser;
    content.innerHTML = `
      <div class="card" style="text-align:center">
        <div style="font-size:56px">🏍️</div>
        <h3 style="margin:10px 0;font-size:20px;font-weight:800">${driver.name || driver.email}</h3>
        <p style="color:var(--muted)">${driver.vehicle} • ${driver.vehicleNum || ""}</p>
        <p style="margin-top:6px">⭐ ${driver.avgRating || "New"} rating • ${driver.totalRides || 0} rides</p>
        <span class="badge badge-${driver.approvalStatus}">${driver.approvalStatus}</span>
      </div>
      <div class="card">
        <div class="card-title">Account Details</div>
        <div class="doc-row"><span class="doc-label">📧 Email</span><span style="font-size:13px;color:var(--muted)">${driver.email}</span></div>
        <div class="doc-row"><span class="doc-label">📞 Phone</span><span style="font-size:13px;color:var(--muted)">${driver.phone}</span></div>
        <div class="doc-row"><span class="doc-label">💳 UPI</span><span style="font-size:13px;color:var(--muted)">${driver.upiId || "Not set"}</span></div>
        <div class="doc-row"><span class="doc-label">🏦 Bank</span><span style="font-size:13px;color:var(--muted)">${driver.bankName || "Not set"}</span></div>
      </div>
      <div class="card">
        <div class="card-title">📄 KYC Documents</div>
        <div class="doc-row"><span class="doc-label">🪪 Driving Licence</span><span class="doc-status badge ${driver.documents?.licence ? 'badge-approved' : 'badge-rejected'}">${driver.documents?.licence ? "Uploaded" : "Missing"}</span></div>
        <div class="doc-row"><span class="doc-label">📋 Vehicle RC</span><span class="doc-status badge ${driver.documents?.rc ? 'badge-approved' : 'badge-rejected'}">${driver.documents?.rc ? "Uploaded" : "Missing"}</span></div>
        <div class="doc-row"><span class="doc-label">🪪 Aadhaar</span><span class="doc-status badge ${driver.documents?.aadhaar ? 'badge-approved' : 'badge-rejected'}">${driver.documents?.aadhaar ? "Uploaded" : "Missing"}</span></div>
      </div>
      <div style="padding:0 10px 16px">
        <button class="btn btn-gray" onclick="App.driverLogout()">🚪 Logout</button>
      </div>
    `;
  },

  driverLogout: async function() {
    if (state.driverRidesSub) state.driverRidesSub();
    await updateDoc(doc(db, "users", state.currentUser.uid), { isOnDuty: false }).catch(() => {});
    await signOut(auth);
    state.currentUser = null; state.role = null;
    showScreen("screen-landing");
  },

  // ─── ADMIN LOGIN
  adminLogin: async function() {
    const email = document.getElementById("a-login-email").value.trim().toLowerCase();
    const pass = document.getElementById("a-login-pass").value;
    if (!email || !pass) return toast("Enter email and password");
    const btn = document.querySelector("#screen-admin-login .btn-secondary");
    btn.innerHTML = '<span class="spinner"></span>';
    try {
      const cred = await signInWithEmailAndPassword(auth, email, pass);
      // Check admin by email (reliable check)
      if (cred.user.email.toLowerCase() !== ADMIN_EMAIL.toLowerCase()) {
        await signOut(auth);
        toast("❌ Not authorized as admin");
        btn.textContent = "Login as Admin";
        return;
      }
      // Ensure admin doc exists
      const adminRef = doc(db, "users", cred.user.uid);
      const adminSnap = await getDoc(adminRef);
      if (!adminSnap.exists()) {
        await setDoc(adminRef, { uid: cred.user.uid, email: cred.user.email, role: "admin", name: "Admin" });
      } else {
        await updateDoc(adminRef, { role: "admin" });
      }
      state.currentUser = { email: cred.user.email, uid: cred.user.uid, role: "admin", name: "Admin" };
      state.role = "admin";
      App.loadAdminDashboard();
    } catch (err) {
      let msg = err.message.replace("Firebase: ", "");
      if (msg.includes("wrong-password") || msg.includes("invalid-credential")) msg = "Wrong email or password";
      if (msg.includes("user-not-found")) msg = "Admin email not registered";
      toast("❌ " + msg);
    }
    btn.textContent = "Login as Admin";
  },

  loadAdminDashboard: async function() {
    showScreen("screen-admin");
    document.getElementById("admin-bottom-nav").style.display = "flex";
    await App.refreshAdminStats();
    App.adminTab("rides");
  },

  refreshAdminStats: async function() {
    const [ridesSnap, driversSnap, pendingKycSnap, withdrawSnap] = await Promise.all([
      getDocs(collection(db, "rides")),
      getDocs(query(collection(db, "users"), where("role", "==", "driver"))),
      getDocs(query(collection(db, "users"), where("approvalStatus", "==", "pending"))),
      getDocs(query(collection(db, "withdrawals"), where("wstatus", "==", "pending")))
    ]);

    let totalRevenue = 0;
    ridesSnap.forEach(d => { if (d.data().status === "completed") totalRevenue += d.data().fare || 0; });

    document.getElementById("admin-stats-grid").innerHTML = `
      <div class="stat-card"><div class="stat-num">${ridesSnap.size}</div><div class="stat-label">Total Rides</div></div>
      <div class="stat-card"><div class="stat-num">${driversSnap.size}</div><div class="stat-label">Drivers</div></div>
      <div class="stat-card"><div class="stat-num" style="color:var(--yellow)">${pendingKycSnap.size}</div><div class="stat-label">Pending KYC</div></div>
      <div class="stat-card"><div class="stat-num">₹${totalRevenue}</div><div class="stat-label">Revenue</div></div>
    `;
  },

  adminTab: function(tab) {
    document.querySelectorAll("#admin-tabs .tab-btn").forEach(t => t.classList.remove("active"));
    const tabs = document.querySelectorAll("#admin-tabs .tab-btn");
    const tabMap = { rides: 0, kyc: 1, drivers: 2, withdrawals: 3, analytics: 4 };
    if (tabs[tabMap[tab]]) tabs[tabMap[tab]].classList.add("active");
    if (unsubAdmin) unsubAdmin();
    if (tab === "rides") App.loadAdminRides();
    else if (tab === "kyc") App.loadAdminKYC();
    else if (tab === "drivers") App.loadAdminDrivers();
    else if (tab === "withdrawals") App.loadAdminWithdrawals();
    else if (tab === "analytics") App.loadAdminAnalytics();
  },

  loadAdminRides: function() {
    const content = document.getElementById("admin-content");
    content.innerHTML = "<div style='text-align:center;padding:20px;color:var(--muted)'>Loading...</div>";
    unsubAdmin = onSnapshot(collection(db, "rides"), snap => {
      const rides = [];
      snap.forEach(d => rides.push({ id: d.id, ...d.data() }));
      rides.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
      let html = "";
      rides.forEach(data => {
        const id = data.id;
        html += `<div class="ride-card ${data.status}">
          <div style="display:flex;justify-content:space-between;margin-bottom:6px">
            <span>${data.vehicleIcon || "🚗"} <b>${data.vehicle}</b></span>
            <span class="badge badge-${data.status}">${data.status}</span>
          </div>
          <div style="display:flex;justify-content:space-between">
            <span class="fare" style="font-size:18px">₹${data.fare}</span>
            <span style="font-size:12px;color:var(--muted)">${(data.paymentMethod||"cash").toUpperCase()}</span>
          </div>
          <div class="route-line" style="margin:6px 0">
            <div class="pickup">📍 ${data.pickup}</div>
            <div class="drop">🏁 ${data.drop}</div>
          </div>
          <p style="font-size:13px;color:var(--muted)">👤 ${data.userName} • ${data.userPhone}</p>
          ${data.driverName ? `<p style="font-size:13px;color:var(--muted)">🏍 Driver: ${data.driverName}</p>` : ""}
          ${data.rating ? `<p style="font-size:13px">⭐ ${data.rating}/5</p>` : ""}
          <p style="font-size:11px;color:var(--muted);margin-top:4px">${data.createdAt ? new Date(data.createdAt).toLocaleString("en-IN") : ""}</p>
          ${data.status !== "completed" && data.status !== "cancelled" ? `<button class="btn btn-red btn-sm" style="margin-top:8px" onclick="App.adminCancelRide('${id}')">❌ Cancel</button>` : ""}
        </div>`;
      });
      content.innerHTML = html || "<div class='card' style='text-align:center;color:var(--muted)'>No rides yet</div>";
    });
  },

  adminCancelRide: async function(id) {
    if (!confirm("Cancel this ride?")) return;
    await updateDoc(doc(db, "rides", id), { status: "cancelled" });
    toast("Ride cancelled.");
  },

  loadAdminKYC: async function() {
    const content = document.getElementById("admin-content");
    content.innerHTML = "<div style='text-align:center;padding:20px;color:var(--muted)'>Loading KYC applications...</div>";
    const q = query(collection(db, "users"), where("role", "==", "driver"), where("approvalStatus", "in", ["pending", "rejected"]));
    const snap = await getDocs(q);
    if (snap.empty) {
      content.innerHTML = "<div class='card' style='text-align:center;color:var(--muted)'>✅ No pending KYC applications</div>";
      return;
    }
    let html = "";
    snap.forEach(d => {
      const data = d.data(); const uid = d.id;
      const docs = data.documents || {};
      html += `<div class="card">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
          <div>
            <div style="font-size:16px;font-weight:800">${data.name || data.email}</div>
            <div style="font-size:13px;color:var(--muted)">${data.vehicle} • ${data.vehicleNum}</div>
          </div>
          <span class="badge badge-${data.approvalStatus === 'pending' ? 'pending' : 'rejected'}">${data.approvalStatus}</span>
        </div>
        <div class="doc-row"><span class="doc-label">📧 Email</span><span style="font-size:13px">${data.email}</span></div>
        <div class="doc-row"><span class="doc-label">📞 Phone</span><span style="font-size:13px">${data.phone}</span></div>
        <div class="doc-row"><span class="doc-label">💳 UPI</span><span style="font-size:13px">${data.upiId}</span></div>
        <div class="doc-row"><span class="doc-label">🏦 Bank</span><span style="font-size:13px">${data.bankAccount} • ${data.ifsc}</span></div>
        <div style="margin:8px 0">
          <div class="doc-row"><span class="doc-label">🪪 Licence</span><span class="badge ${docs.licence ? 'badge-approved' : 'badge-rejected'}">${docs.licence ? "✓ Uploaded" : "✗ Missing"}</span></div>
          <div class="doc-row"><span class="doc-label">📋 RC</span><span class="badge ${docs.rc ? 'badge-approved' : 'badge-rejected'}">${docs.rc ? "✓ Uploaded" : "✗ Missing"}</span></div>
          <div class="doc-row"><span class="doc-label">🪪 Aadhaar</span><span class="badge ${docs.aadhaar ? 'badge-approved' : 'badge-rejected'}">${docs.aadhaar ? "✓ Uploaded" : "✗ Missing"}</span></div>
          <div class="doc-row"><span class="doc-label">🤳 Selfie</span><span class="badge ${docs.selfie ? 'badge-approved' : 'badge-rejected'}">${docs.selfie ? "✓ Uploaded" : "✗ Missing"}</span></div>
        </div>
        <p style="font-size:12px;color:var(--muted);margin-bottom:8px">Applied: ${data.joinedAt ? new Date(data.joinedAt).toLocaleDateString("en-IN") : "—"}</p>
        <div style="display:flex;gap:8px">
          <button class="btn btn-green btn-sm" style="flex:1" onclick="App.approveDriver('${uid}')">✅ Approve</button>
          <button class="btn btn-red btn-sm" style="flex:1" onclick="App.rejectDriver('${uid}')">❌ Reject</button>
        </div>
      </div>`;
    });
    content.innerHTML = html;
  },

  approveDriver: async function(uid) {
    await updateDoc(doc(db, "users", uid), { approvalStatus: "approved" });
    toast("✅ Driver approved!");
    App.loadAdminKYC();
    App.refreshAdminStats();
  },

  rejectDriver: async function(uid) {
    const reason = prompt("Reason for rejection (optional):");
    await updateDoc(doc(db, "users", uid), { approvalStatus: "rejected", rejectionReason: reason || "" });
    toast("Driver rejected.");
    App.loadAdminKYC();
  },

  loadAdminDrivers: async function() {
    const content = document.getElementById("admin-content");
    content.innerHTML = "<div style='text-align:center;padding:20px;color:var(--muted)'>Loading...</div>";
    const q = query(collection(db, "users"), where("role", "==", "driver"));
    const snap = await getDocs(q);
    let html = "";
    snap.forEach(d => {
      const data = d.data(); const uid = d.id;
      html += `<div class="ride-card">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div>
            <div style="font-weight:800;font-size:15px">${data.name || data.email}</div>
            <div style="font-size:13px;color:var(--muted)">${data.vehicle} • ${data.vehicleNum}</div>
          </div>
          <span class="badge badge-${data.approvalStatus}">${data.approvalStatus}</span>
        </div>
        <div style="display:flex;gap:6px;flex-wrap:wrap;margin-top:6px">
          <span style="font-size:12px;color:var(--muted)">⭐ ${data.avgRating || "New"}</span>
          <span style="font-size:12px;color:var(--muted)">🚗 ${data.totalRides || 0} rides</span>
          <span style="font-size:12px;color:var(--muted)">💰 ₹${data.earnings || 0}</span>
          <span class="avail-dot ${data.isOnDuty ? 'online' : 'offline'}"></span>
          <span style="font-size:12px;color:var(--muted)">${data.isOnDuty ? "Online" : "Offline"}</span>
        </div>
        <p style="font-size:12px;color:var(--muted);margin-top:4px">📞 ${data.phone} • ${data.email}</p>
        ${data.approvalStatus === "approved" ? `<button class="btn btn-red btn-sm" style="margin-top:8px" onclick="App.suspendDriver('${uid}')">🚫 Suspend</button>` : ""}
      </div>`;
    });
    content.innerHTML = html || "<div class='card' style='text-align:center;color:var(--muted)'>No drivers</div>";
  },

  suspendDriver: async function(uid) {
    if (!confirm("Suspend this driver?")) return;
    await updateDoc(doc(db, "users", uid), { approvalStatus: "rejected", isOnDuty: false });
    toast("Driver suspended.");
    App.loadAdminDrivers();
  },

  loadAdminWithdrawals: async function() {
    const content = document.getElementById("admin-content");
    content.innerHTML = "<div style='text-align:center;padding:20px;color:var(--muted)'>Loading...</div>";
    const snap = await getDocs(query(collection(db, "withdrawals"), orderBy("requestedAt", "desc")));
    let html = "";
    snap.forEach(d => {
      const w = d.data(); const id = d.id;
      html += `<div class="ride-card ${w.wstatus === 'pending' ? 'pending' : ''}">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px">
          <span style="font-size:20px;font-weight:900;color:var(--primary)">₹${w.amount}</span>
          <span class="badge badge-${w.wstatus}">${w.wstatus}</span>
        </div>
        <p style="font-weight:700">${w.driverName || w.driverEmail}</p>
        <p style="font-size:13px;color:var(--muted)">UPI: <b>${w.upiId}</b></p>
        <p style="font-size:12px;color:var(--muted)">${w.requestedAt ? new Date(w.requestedAt).toLocaleString("en-IN") : ""}</p>
        ${w.wstatus === "pending" ? `
          <div style="display:flex;gap:8px;margin-top:8px">
            <button class="btn btn-green btn-sm" style="flex:1" onclick="App.processWithdrawal('${id}','approved')">✅ Approve & Pay</button>
            <button class="btn btn-red btn-sm" style="flex:1" onclick="App.processWithdrawal('${id}','rejected')">❌ Reject</button>
          </div>
        ` : `<p style="font-size:12px;color:var(--muted)">Processed: ${w.processedAt ? new Date(w.processedAt).toLocaleDateString("en-IN") : "—"}</p>`}
      </div>`;
    });
    content.innerHTML = html || "<div class='card' style='text-align:center;color:var(--muted)'>No withdrawal requests</div>";
  },

  processWithdrawal: async function(id, status) {
    if (status === "approved") {
      if (!confirm("Confirm payment to driver? Make sure UPI transfer is done.")) return;
    }
    await updateDoc(doc(db, "withdrawals", id), {
      wstatus: status,
      processedAt: new Date().toISOString(),
      processedBy: ADMIN_EMAIL
    });
    toast(status === "approved" ? "✅ Withdrawal approved & marked paid!" : "Withdrawal rejected.");
    App.loadAdminWithdrawals();
    App.refreshAdminStats();
  },

  loadAdminAnalytics: async function() {
    const content = document.getElementById("admin-content");
    content.innerHTML = "<div style='text-align:center;padding:20px;color:var(--muted)'>Loading analytics...</div>";

    const ridesSnap = await getDocs(collection(db, "rides"));
    const driversSnap = await getDocs(query(collection(db, "users"), where("role", "==", "driver")));

    let stats = { pending: 0, accepted: 0, completed: 0, cancelled: 0, totalRevenue: 0, vehicles: {} };
    ridesSnap.forEach(d => {
      const data = d.data();
      if (stats[data.status] !== undefined) stats[data.status]++;
      if (data.status === "completed") stats.totalRevenue += data.fare || 0;
      if (!stats.vehicles[data.vehicle]) stats.vehicles[data.vehicle] = 0;
      stats.vehicles[data.vehicle]++;
    });

    let driverStats = { approved: 0, pending: 0, online: 0 };
    driversSnap.forEach(d => {
      const data = d.data();
      if (data.approvalStatus === "approved") driverStats.approved++;
      if (data.approvalStatus === "pending") driverStats.pending++;
      if (data.isOnDuty) driverStats.online++;
    });

    let vehicleHtml = Object.entries(stats.vehicles).map(([v, c]) =>
      `<div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)">
        <span style="font-weight:700">${v}</span>
        <span style="color:var(--primary);font-weight:800">${c} rides</span>
      </div>`
    ).join("");

    content.innerHTML = `
      <div class="card">
        <div class="card-title">📊 Ride Statistics</div>
        <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)"><span>Total Rides</span><b>${ridesSnap.size}</b></div>
        <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)"><span>✅ Completed</span><b style="color:var(--green)">${stats.completed}</b></div>
        <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)"><span>⏳ Pending</span><b style="color:var(--yellow)">${stats.pending}</b></div>
        <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)"><span>❌ Cancelled</span><b style="color:var(--red)">${stats.cancelled}</b></div>
        <div style="display:flex;justify-content:space-between;padding:8px 0"><span>💰 Total Revenue</span><b style="color:var(--primary)">₹${stats.totalRevenue}</b></div>
      </div>
      <div class="card">
        <div class="card-title">🏍️ Vehicle Breakdown</div>
        ${vehicleHtml || "<p style='color:var(--muted)'>No data</p>"}
      </div>
      <div class="card">
        <div class="card-title">👥 Driver Statistics</div>
        <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)"><span>Total Drivers</span><b>${driversSnap.size}</b></div>
        <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)"><span>✅ Approved</span><b style="color:var(--green)">${driverStats.approved}</b></div>
        <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)"><span>⏳ Pending KYC</span><b style="color:var(--yellow)">${driverStats.pending}</b></div>
        <div style="display:flex;justify-content:space-between;padding:8px 0"><span>🟢 Online Now</span><b style="color:var(--green)">${driverStats.online}</b></div>
      </div>
    `;
  },

  adminLogout: async function() {
    if (unsubAdmin) unsubAdmin();
    await signOut(auth);
    state.currentUser = null; state.role = null;
    document.getElementById("admin-bottom-nav").style.display = "none";
    showScreen("screen-landing");
  },

  forgotPassword: async function(role) {
    const emailEl = document.getElementById(role === "driver" ? "d-login-email" : "a-login-email");
    const email = emailEl ? emailEl.value.trim() : "";
    if (!email) return toast("Enter your email first");
    try {
      await sendPasswordResetEmail(auth, email);
      toast("📧 Password reset email sent!");
    } catch (err) {
      toast("❌ " + err.message.replace("Firebase: ", ""));
    }
  }
};

// ─── AUTO-LOGIN (persist session)
auth.onAuthStateChanged(async user => {
  if (!user) return;
  try {
    const snap = await getDoc(doc(db, "users", user.uid));
    if (!snap.exists()) return;
    const userData = { ...snap.data(), uid: user.uid };
    state.currentUser = userData;
    state.role = userData.role;
    if (userData.role === "driver") {
      App.loadDriverDashboard();
    } else if (userData.role === "admin" && userData.email.toLowerCase() === ADMIN_EMAIL.toLowerCase()) {
      App.loadAdminDashboard();
    }
  } catch (e) {}
});

// ─── INITIAL LOAD
showScreen("screen-landing");
updatePickupMap();

</script>

<!--
════════════════════════════════════════════
FIRESTORE SECURITY RULES — Copy to Firebase Console
Firestore → Rules → Edit → Publish
════════════════════════════════════════════

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    function isAdmin() {
      return request.auth != null && request.auth.token.email == "bonagirispinoj@gmail.com";
    }

    function isDriver() {
      return request.auth != null && get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == "driver";
    }

    match /users/{uid} {
      allow read: if request.auth != null && (request.auth.uid == uid || isAdmin());
      allow create: if request.auth != null && request.auth.uid == uid;
      allow update: if request.auth != null && (request.auth.uid == uid || isAdmin());
    }

    match /rides/{rideId} {
      allow create: if true;
      allow read: if true;
      allow update: if request.auth != null || true;
      allow delete: if isAdmin();
    }

    match /withdrawals/{wId} {
      allow create: if request.auth != null;
      allow read: if request.auth != null;
      allow update: if request.auth != null;
    }
  }
}
-->

</body>
</html>
