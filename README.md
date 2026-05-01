
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Fresha Add-ons Calculator</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Helvetica,Arial,sans-serif;background:#ede9fe;color:#111827;min-height:100vh;padding:2rem 1rem;}
:root{
  --bg:#ffffff;--bg2:#f7f5ff;--bg3:#ede9ff;
  --text:#111827;--text2:#6b7280;--text3:#9ca3af;
  --border:rgba(0,0,0,0.08);--border2:rgba(0,0,0,0.15);
  --rad:8px;--radlg:12px;
  --purple:#7C3AED;--purple-lt:#EDE9FE;--purple-mid:#6D28D9;--purple-dk:#4C1D95;
  --purple-text:#5B21B6;--purple-deep:#1a0a2e;
  --teal-mid:#1D9E75;--green:#0F6E56;
}
.page{max-width:900px;margin:0 auto;}

.topbar{display:flex;align-items:center;justify-content:space-between;margin-bottom:1.5rem;flex-wrap:wrap;gap:10px;}
.topbar-title{font-size:17px;font-weight:600;color:#4C1D95;}
.topbar-sub{font-size:12px;color:#7C3AED;margin-top:3px;}
.fresha-dot{display:inline-block;width:8px;height:8px;background:#7C3AED;border-radius:50%;margin-right:6px;}

.country-tabs{display:flex;gap:6px;}
.ctab{background:rgba(255,255,255,0.5);border:0.5px solid rgba(109,40,217,0.25);border-radius:var(--rad);padding:7px 16px;font-size:12px;font-weight:500;color:#5B21B6;cursor:pointer;transition:all .15s;}
.ctab:hover{background:rgba(255,255,255,0.7);}
.ctab.active{background:#fff;border-color:#fff;color:#4C1D95;font-weight:600;}

.tab-row{display:flex;gap:6px;margin-bottom:1.5rem;}
button{cursor:pointer;font-family:inherit;}
.tab{background:rgba(255,255,255,0.5);border:0.5px solid rgba(109,40,217,0.25);border-radius:var(--rad);padding:8px 18px;font-size:13px;color:#5B21B6;transition:all .15s;}
.tab:hover{background:rgba(255,255,255,0.7);}
.tab.active{background:#fff;border-color:#fff;color:#4C1D95;font-weight:600;}

.view{display:none;}
.view.show{display:block;}

.card{background:var(--bg);border:0.5px solid var(--border);border-radius:var(--radlg);padding:1.25rem 1.5rem;margin-bottom:1.1rem;}
.card-title{font-size:13px;font-weight:600;color:var(--text);margin-bottom:1rem;padding-bottom:10px;border-bottom:0.5px solid var(--border);}

.field-row{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:12px;}
.field{display:flex;flex-direction:column;gap:5px;}
.field label{font-size:11px;font-weight:500;color:var(--text2);}
.field input,.field textarea{border:0.5px solid var(--border2);border-radius:var(--rad);padding:8px 10px;font-size:13px;color:var(--text);background:var(--bg);width:100%;}
.field input:focus,.field textarea:focus{outline:none;border-color:var(--purple);box-shadow:0 0 0 2px rgba(124,58,237,.12);}
.field textarea{resize:vertical;min-height:62px;font-family:inherit;line-height:1.5;}

.feat-admin{width:100%;border-collapse:collapse;font-size:12px;}
.feat-admin th{text-align:left;font-size:11px;font-weight:600;color:var(--text2);padding:7px 8px;border-bottom:0.5px solid var(--border);background:var(--bg2);}
.feat-admin td{padding:8px 8px;border-bottom:0.5px solid var(--border);vertical-align:middle;}
.feat-admin tr:last-child td{border-bottom:none;}
.feat-admin input[type=number],.feat-admin input[type=text]{width:110px;border:0.5px solid var(--border2);border-radius:var(--rad);padding:5px 8px;font-size:12px;color:var(--text);background:var(--bg);}
.feat-admin input[type=number]:focus,.feat-admin input[type=text]:focus{outline:none;border-color:var(--purple);}

.save-btn{background:var(--purple);color:#fff;border:none;border-radius:var(--rad);padding:10px 22px;font-size:13px;font-weight:600;transition:opacity .15s;}
.save-btn:hover{opacity:.88;}
.save-btn:active{transform:scale(.98);}
.toast{display:inline-block;margin-left:12px;font-size:12px;color:#7C3AED;opacity:0;transition:opacity .3s;}
.toast.show{opacity:1;}

/* BANNER */
.banner{background:linear-gradient(135deg,#2d1165 0%,#4C1D95 50%,#6D28D9 100%);border-radius:var(--radlg);padding:0;margin-bottom:1.25rem;overflow:hidden;position:relative;}
.banner-inner{padding:1.5rem 2rem;display:flex;align-items:center;justify-content:space-between;gap:1rem;}
.banner-left{display:flex;align-items:center;gap:1.25rem;flex:1;}
.logo-area{width:72px;height:72px;border-radius:var(--radlg);background:rgba(255,255,255,0.12);border:1px solid rgba(255,255,255,0.2);display:flex;align-items:center;justify-content:center;overflow:hidden;flex-shrink:0;cursor:pointer;position:relative;}
.logo-area img{width:100%;height:100%;object-fit:contain;}
.logo-placeholder{display:flex;flex-direction:column;align-items:center;gap:4px;}
.logo-placeholder svg{opacity:.6;}
.logo-placeholder span{font-size:9px;color:rgba(255,255,255,0.5);text-align:center;line-height:1.3;}
.logo-hover{position:absolute;inset:0;background:rgba(0,0,0,0.45);display:none;align-items:center;justify-content:center;font-size:10px;color:#fff;text-align:center;line-height:1.4;}
.logo-area:hover .logo-hover{display:flex;}
.banner-partner{font-size:13px;color:#c4b5fd;margin-bottom:4px;font-weight:500;}
.banner-t{font-size:20px;font-weight:600;color:#fff;letter-spacing:-.3px;}
.banner-s{font-size:12px;color:#ddd6fe;margin-top:4px;}
.badge-conf{background:rgba(255,255,255,0.15);color:#fff;font-size:10px;font-weight:600;padding:5px 12px;border-radius:20px;white-space:nowrap;border:0.5px solid rgba(255,255,255,0.25);flex-shrink:0;}
.fresha-wordmark{font-size:11px;color:rgba(255,255,255,0.35);font-weight:600;letter-spacing:.05em;text-align:right;padding:0 2rem .75rem;margin-top:-.5rem;}

#logo-upload{display:none;}

.slabel{font-size:10px;font-weight:600;letter-spacing:.09em;text-transform:uppercase;color:var(--text2);margin-bottom:9px;padding-left:2px;}

.fields-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(175px,1fr));gap:12px;}
.cfield{display:flex;flex-direction:column;gap:5px;}
.cfield label{font-size:11px;font-weight:500;color:var(--text2);}
.cfield input{border:0.5px solid var(--border2);border-radius:var(--rad);padding:8px 11px;font-size:13px;color:var(--text);background:var(--bg);width:100%;}
.cfield input:focus{outline:none;border-color:var(--purple);box-shadow:0 0 0 2px rgba(124,58,237,.1);}

/* Addon pricing cards on client view */
.addons-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-bottom:1.25rem;}
.addon-card{background:var(--bg);border:0.5px solid var(--border);border-radius:var(--radlg);padding:1.1rem 1.25rem;}
.addon-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;}
.addon-name{font-size:14px;font-weight:600;color:var(--text);}
.addon-tag{font-size:10px;font-weight:600;padding:3px 8px;border-radius:20px;background:var(--purple-lt);color:var(--purple-dk);}
.price-block{display:flex;align-items:baseline;gap:6px;margin-bottom:4px;}
.price-excl{font-size:22px;font-weight:700;color:var(--purple-mid);}
.price-rrp{font-size:13px;color:var(--text3);text-decoration:line-through;}
.price-basis{font-size:11px;color:var(--text2);}
.saving-pill{display:inline-block;background:#dcfce7;color:#166534;font-size:11px;font-weight:600;padding:3px 9px;border-radius:20px;margin-top:6px;}

/* Summary savings box */
.sbox{background:var(--purple-lt);border:0.5px solid #c4b5fd;border-radius:var(--radlg);padding:1.25rem 1.75rem;display:flex;align-items:center;justify-content:space-between;margin-bottom:1.25rem;gap:1rem;}
.slbl{font-size:14px;font-weight:600;color:var(--purple-dk);}
.ssub{font-size:11px;color:var(--purple-text);margin-top:4px;}
.samt{font-size:28px;font-weight:700;color:var(--purple-dk);white-space:nowrap;}

.cfooter{text-align:center;font-size:11px;color:var(--text3);padding:1rem 0 .5rem;border-top:0.5px solid var(--border);}

/* Admin logo */
.logo-admin-wrap{display:flex;align-items:center;gap:14px;padding:1rem 0;}
.logo-preview-admin{width:64px;height:64px;border-radius:var(--rad);border:0.5px solid var(--border2);background:var(--bg2);display:flex;align-items:center;justify-content:center;overflow:hidden;flex-shrink:0;}
.logo-preview-admin img{width:100%;height:100%;object-fit:contain;}
.upload-btn{background:transparent;border:0.5px solid var(--border2);border-radius:var(--rad);padding:8px 14px;font-size:12px;color:var(--text2);transition:all .15s;}
.upload-btn:hover{background:var(--bg2);border-color:var(--purple);color:var(--purple);}
.remove-btn{background:transparent;border:none;font-size:12px;color:#dc2626;padding:4px 8px;}
.remove-btn:hover{text-decoration:underline;}

/* Country flag pills */
.country-pill{display:inline-flex;align-items:center;gap:5px;background:var(--purple-lt);color:var(--purple-dk);font-size:11px;font-weight:600;padding:4px 10px;border-radius:20px;}

/* Discount slider in admin */
.slider-row{display:flex;align-items:center;gap:10px;}
.slider-row input[type=range]{flex:1;accent-color:var(--purple);}
.slider-val{font-size:13px;font-weight:600;color:var(--purple-mid);min-width:38px;text-align:right;}

@media(max-width:620px){
  .addons-grid{grid-template-columns:1fr;}
  .sbox{flex-direction:column;align-items:flex-start;}
  .banner-inner{flex-direction:column;align-items:flex-start;}
  .field-row{grid-template-columns:1fr;}
}
@media print{
  body{background:#fff;padding:0;}
  .topbar,.tab-row,#view-admin{display:none!important;}
  #view-client{display:block!important;}
  .banner{-webkit-print-color-adjust:exact;print-color-adjust:exact;}
}
</style>
</head>
<body>
<div class="page">

  <div class="topbar">
    <div>
      <div class="topbar-title"><span class="fresha-dot"></span>Fresha Add-ons Calculator</div>
      <div class="topbar-sub">Set pricing in Admin &bull; Present to clients in Client view</div>
    </div>
    <div class="country-tabs">
      <button class="ctab active" onclick="switchCountry('SGD',this)">🇸🇬 Singapore</button>
      <button class="ctab" onclick="switchCountry('HKD',this)">🇭🇰 Hong Kong</button>
      <button class="ctab" onclick="switchCountry('IDR',this)">🇮🇩 Indonesia</button>
      <button class="ctab" onclick="switchCountry('MYR',this)">🇲🇾 Malaysia</button>
      <button class="ctab" onclick="switchCountry('PHP',this)">🇵🇭 Philippines</button>
    </div>
  </div>

  <div class="tab-row">
    <button class="tab active" onclick="switchTab('admin',this)">Admin settings</button>
    <button class="tab" onclick="switchTab('client',this)">Client view</button>
  </div>

  <!-- ADMIN VIEW -->
  <div id="view-admin" class="view show">

    <div class="card">
      <div class="card-title">Partner logo</div>
      <div class="logo-admin-wrap">
        <div class="logo-preview-admin" id="admin-logo-preview">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="#9ca3af" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><path d="M21 15l-5-5L5 21"/></svg>
        </div>
        <div>
          <div style="font-size:13px;font-weight:500;color:var(--text);margin-bottom:4px;">Partner logo</div>
          <div style="font-size:12px;color:var(--text2);margin-bottom:10px;">Appears in the banner on the client view. PNG or JPG recommended.</div>
          <div style="display:flex;align-items:center;gap:8px;">
            <button class="upload-btn" onclick="document.getElementById('logo-upload').click()">Upload logo</button>
            <button class="remove-btn" onclick="removeLogo()" id="remove-logo-btn" style="display:none;">Remove</button>
          </div>
        </div>
      </div>
      <input type="file" id="logo-upload" accept="image/*" onchange="handleLogoUpload(event)">
    </div>

    <div class="card">
      <div class="card-title">Add-on pricing — <span id="admin-country-label">Indonesia (IDR)</span></div>
      <p style="font-size:12px;color:var(--text2);margin-bottom:14px;">Set the RRP and your exclusive discounted price for each add-on. Use the slider or type directly.</p>
      <table class="feat-admin">
        <thead>
          <tr>
            <th style="width:8%">Show</th>
            <th style="width:20%">Add-on</th>
            <th style="width:10%">Type</th>
            <th style="width:16%">RRP</th>
            <th>Discount</th>
            <th style="width:18%">Exclusive price</th>
          </tr>
        </thead>
        <tbody id="admin-feat-body"></tbody>
      </table>
    </div>

    <div class="card">
      <div class="card-title">Subscription — bookable staff calculator</div>

      <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-bottom:14px;">
        <div class="field">
          <label>Price per bookable staff (RRP)</label>
          <input type="number" min="0" step="0.01" id="sub-rrp-display" value="18.95" readonly style="background:var(--bg2);color:var(--text2);cursor:default;">
          <span style="font-size:11px;color:var(--text3);margin-top:4px;display:block;">Auto-filled from RRP above</span>
        </div>
        <div class="field">
          <label>Number of bookable staff</label>
          <input type="number" min="1" step="1" id="bookable-input" value="1" oninput="updateBookable(this.value)">
          <span style="font-size:11px;color:var(--text3);margin-top:4px;display:block;">Used for Subscription &amp; Insights</span>
        </div>
        <div class="field">
          <label>Number of locations</label>
          <input type="number" min="1" step="1" id="locations-input" value="1" oninput="updateLocations(this.value)">
          <span style="font-size:11px;color:var(--text3);margin-top:4px;display:block;">Used for Loyalty &amp; Google Boost</span>
        </div>
      </div>

      <div style="background:var(--bg2);border-radius:var(--rad);padding:12px 14px;margin-bottom:14px;display:flex;align-items:center;gap:8px;flex-wrap:wrap;">
        <span style="font-size:13px;color:var(--text2);">RRP total</span>
        <span style="font-size:13px;font-weight:600;color:var(--text);" id="sub-rrp-calc">—</span>
        <span style="font-size:12px;color:var(--text3);" id="sub-rrp-calc-note">—</span>
      </div>

      <div class="field" style="max-width:220px;margin-bottom:14px;">
        <label>Discount (%)</label>
        <div style="display:flex;align-items:center;gap:10px;">
          <input type="range" min="0" max="60" step="1" id="sub-discount-slider" value="0" style="flex:1;accent-color:var(--purple);" oninput="updateSubDiscount(this.value)">
          <span style="font-size:13px;font-weight:600;color:var(--purple-mid);min-width:38px;text-align:right;" id="sub-discount-val">0%</span>
        </div>
      </div>

      <div style="background:var(--purple-lt);border:0.5px solid #c4b5fd;border-radius:var(--rad);padding:12px 14px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px;">
        <div>
          <div style="font-size:12px;font-weight:600;color:var(--purple-dk);">Exclusive total after discount</div>
          <div style="font-size:11px;color:var(--purple-text);margin-top:2px;" id="sub-excl-note">—</div>
        </div>
        <div style="font-size:20px;font-weight:700;color:var(--purple-dk);" id="sub-excl-total">—</div>
      </div>
    </div>

    <div class="card">
      <div class="card-title">Notes for client view <span style="font-size:11px;font-weight:400;color:var(--text3);">(optional)</span></div>
      <div id="admin-notes-body"></div>
    </div>

    <div style="display:flex;align-items:center;padding-bottom:.5rem;">
      <button class="save-btn" onclick="saveSettings()">Save all changes</button>
      <span class="toast" id="toast">&#10003;&nbsp;Saved</span>
    </div>
  </div>

  <!-- CLIENT VIEW -->
  <div id="view-client" class="view">

    <div class="banner">
      <div class="banner-inner">
        <div class="banner-left">
          <div class="logo-area" id="client-logo-area" onclick="document.getElementById('logo-upload').click()" title="Click to upload logo">
            <div class="logo-placeholder" id="logo-placeholder">
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="rgba(255,255,255,0.5)" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><path d="M21 15l-5-5L5 21"/></svg>
              <span>Add logo</span>
            </div>
            <img id="client-logo-img" src="" style="display:none;">
            <div class="logo-hover">Change<br>logo</div>
          </div>
          <div>
            <div class="banner-partner" id="banner-partner-name">Partner</div>
            <div class="banner-t">Fresha Add-ons Proposal</div>
            <div class="banner-s" id="banner-sub">Exclusive pricing &bull; Indonesia</div>
          </div>
        </div>
        <span class="badge-conf">Confidential</span>
      </div>
      <div class="fresha-wordmark">powered by fresha</div>
    </div>

    <div class="slabel">Client details</div>
    <div class="card">
      <div class="fields-grid">
        <div class="cfield"><label>Partner name</label><input id="c-partner" value="Your Partner" oninput="renderClient()"></div>
        <div class="cfield"><label>Date</label><input id="c-date" value="" oninput="renderClient()"></div>
        <div class="cfield"><label>Prepared by</label><input id="c-preparer" placeholder="Your name" oninput="renderClient()"></div>
      </div>
    </div>

    <div class="slabel">Business inputs</div>
    <div class="card" style="margin-bottom:1.1rem;">
      <div class="fields-grid">
        <div class="cfield">
          <label># of bookable staff</label>
          <input type="number" id="c-bookable-staff" value="1" min="1" step="1" oninput="syncBookable(this.value)">
          <span style="font-size:11px;color:var(--text3);margin-top:4px;display:block;">Used for Subscription &amp; Insights</span>
        </div>
        <div class="cfield">
          <label># of locations</label>
          <input type="number" id="c-locations" value="1" min="1" step="1" oninput="syncLocations(this.value)">
          <span style="font-size:11px;color:var(--text3);margin-top:4px;display:block;">Used for Loyalty &amp; Google Boost</span>
        </div>
      </div>
    </div>

    <div class="slabel">Exclusive add-on pricing</div>
    <div class="addons-grid" id="c-addons"></div>

    <div id="c-savings"></div>

    <div id="c-notes-wrap" style="display:none;">
      <div class="slabel">Key notes</div>
      <div style="display:grid;grid-template-columns:repeat(2,1fr);gap:9px;margin-bottom:1.25rem;" id="c-notes"></div>
    </div>

    <div style="display:flex;justify-content:center;gap:10px;margin-bottom:1rem;">
      <button onclick="exportPDF()" style="background:var(--purple);color:#fff;border:none;border-radius:var(--rad);padding:10px 22px;font-size:13px;font-weight:600;cursor:pointer;display:flex;align-items:center;gap:8px;">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
        Export as PDF
      </button>
      <button onclick="exportPNG()" style="background:transparent;color:var(--purple);border:0.5px solid var(--purple);border-radius:var(--rad);padding:10px 22px;font-size:13px;font-weight:600;cursor:pointer;display:flex;align-items:center;gap:8px;">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><path d="M21 15l-5-5L5 21"/></svg>
        Save as image
      </button>
    </div>
    <div class="cfooter">Confidential &mdash; Prepared for <span id="c-footer-partner">Partner</span> by Fresha</div>
  </div>

</div>

<script>
const COUNTRIES = {
  SGD: { label:'Singapore (SGD)', short:'Singapore', sym:'SGD $', locale:'en-SG', decimals:2 },
  HKD: { label:'Hong Kong (HKD)', short:'Hong Kong', sym:'HKD $', locale:'en-HK', decimals:2 },
  IDR: { label:'Indonesia (IDR)', short:'Indonesia', sym:'Rp', locale:'id-ID', decimals:0 },
  MYR: { label:'Malaysia (MYR)',  short:'Malaysia',  sym:'RM', locale:'en-MY', decimals:2 },
  PHP: { label:'Philippines (PHP)', short:'Philippines', sym:'₱', locale:'en-PH', decimals:0 },
};

const ADDONS_DEF = [
  { id:'subscription',  name:'Subscription',        type:'per_bookable', rrp:{ SGD:18.95, HKD:99.95, IDR:170000, MYR:45,    PHP:600  } },
  { id:'loyalty',       name:'Client Loyalty',      type:'per_location', rrp:{ SGD:79.95, HKD:450,   IDR:760000, MYR:265,   PHP:2750 } },
  { id:'google',        name:'Google Rating Boost', type:'per_location', rrp:{ SGD:14.95, HKD:95.95, IDR:110000, MYR:24.95, PHP:350  } },
  { id:'insights',      name:'Insights',            type:'per_bookable', rrp:{ SGD:13.95, HKD:79,    IDR:110000, MYR:16,    PHP:350  } },
];

const NOTES_DEF = [
  { title:'Bundle value', body:'When taken together, these three add-ons drive retention, visibility, and data — covering the full client lifecycle.' },
  { title:'Loyalty',      body:'Reward repeat clients automatically with points and perks — drives return visits without manual effort.' },
  { title:'Google Boost', body:'Automatically prompts happy clients for Google reviews after appointments, building your online reputation.' },
  { title:'Insights',     body:'Track revenue, staff performance, and client trends in one dashboard — no spreadsheets needed.' },
];

const STORE_KEY = 'fresha-sea-addons-v7';

// State per country
let S = {
  SGD: { discounts:{ subscription:0, loyalty:0, google:0, insights:0 }, enabled:{ subscription:true, loyalty:true, google:true, insights:true }, bookableStaff:1, locations:1, notes: JSON.parse(JSON.stringify(NOTES_DEF)), logoData:null },
  HKD: { discounts:{ subscription:0, loyalty:0, google:0, insights:0 }, enabled:{ subscription:true, loyalty:true, google:true, insights:true }, bookableStaff:1, locations:1, notes: JSON.parse(JSON.stringify(NOTES_DEF)), logoData:null },
  IDR: { discounts:{ subscription:0, loyalty:0, google:0, insights:0 }, enabled:{ subscription:true, loyalty:true, google:true, insights:true }, bookableStaff:1, locations:1, notes: JSON.parse(JSON.stringify(NOTES_DEF)), logoData:null },
  MYR: { discounts:{ subscription:0, loyalty:0, google:0, insights:0 }, enabled:{ subscription:true, loyalty:true, google:true, insights:true }, bookableStaff:1, locations:1, notes: JSON.parse(JSON.stringify(NOTES_DEF)), logoData:null },
  PHP: { discounts:{ subscription:0, loyalty:0, google:0, insights:0 }, enabled:{ subscription:true, loyalty:true, google:true, insights:true }, bookableStaff:1, locations:1, notes: JSON.parse(JSON.stringify(NOTES_DEF)), logoData:null },
};

let currentCountry = 'SGD';

function fmt(n, country) {
  const c = COUNTRIES[country];
  return c.sym + ' ' + parseFloat(n).toLocaleString(c.locale, { minimumFractionDigits:c.decimals, maximumFractionDigits:c.decimals });
}

function getRRP(addonId, country) {
  return ADDONS_DEF.find(a => a.id === addonId).rrp[country];
}

function getExcl(addonId, country) {
  const rrp = getRRP(addonId, country);
  const disc = S[country].discounts[addonId] || 0;
  return rrp * (1 - disc / 100);
}

function loadSettings() {
  try {
    const raw = localStorage.getItem(STORE_KEY);
    if (raw) S = JSON.parse(raw);
  } catch(e) {}
  const today = new Date().toLocaleDateString('en-GB',{day:'numeric',month:'long',year:'numeric'});
  document.getElementById('c-date').value = today;
  renderAdmin();
  renderClient();
  applyLogo(S[currentCountry].logoData);
}

function saveSettings() {
  collectAdmin();
  try { localStorage.setItem(STORE_KEY, JSON.stringify(S)); } catch(e) {}
  const t = document.getElementById('toast');
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2200);
  renderClient();
}

function switchCountry(c, btn) {
  collectAdmin();
  currentCountry = c;
  document.querySelectorAll('.ctab').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderAdmin();
  renderClient();
  applyLogo(S[currentCountry].logoData);
}

function switchTab(t, btn) {
  collectAdmin();
  document.querySelectorAll('.tab').forEach(b => b.classList.remove('active'));
  document.querySelectorAll('.view').forEach(v => v.classList.remove('show'));
  btn.classList.add('active');
  document.getElementById('view-' + t).classList.add('show');
  if (t === 'client') renderClient();
}

function updateBookable(val) {
  const c = currentCountry;
  S[c].bookableStaff = parseInt(val) || 1;
  const clientEl = document.getElementById('c-bookable-staff');
  if (clientEl) clientEl.value = S[c].bookableStaff;
  refreshSubCard();
  renderClient();
}

function syncBookable(val) {
  const c = currentCountry;
  S[c].bookableStaff = parseInt(val) || 1;
  const adminEl = document.getElementById('bookable-input');
  if (adminEl) adminEl.value = S[c].bookableStaff;
  refreshSubCard();
  renderClient();
}

function updateLocations(val) {
  const c = currentCountry;
  S[c].locations = parseInt(val) || 1;
  const clientEl = document.getElementById('c-locations');
  if (clientEl) clientEl.value = S[c].locations;
  renderClient();
}

function syncLocations(val) {
  const c = currentCountry;
  S[c].locations = parseInt(val) || 1;
  const adminEl = document.getElementById('locations-input');
  if (adminEl) adminEl.value = S[c].locations;
  renderClient();
}

function updateSubDiscount(val) {
  const c = currentCountry;
  S[c].discounts['subscription'] = parseFloat(val) || 0;
  document.getElementById('sub-discount-val').textContent = val + '%';
  // also sync the main table slider if visible
  const mainSlider = document.getElementById('aslider-subscription');
  if (mainSlider) mainSlider.value = val;
  const mainVal = document.getElementById('sval-subscription');
  if (mainVal) mainVal.textContent = val + '%';
  refreshSubCard();
  renderClient();
}

function refreshSubCard() {
  const c = currentCountry;
  const cInfo = COUNTRIES[c];
  const staff = S[c].bookableStaff || 1;
  const disc  = S[c].discounts['subscription'] || 0;
  const baseRRP = getBaseRRP('subscription', c);
  const rrpTotal = baseRRP * staff;
  const exclTotal = rrpTotal * (1 - disc / 100);
  const saving = rrpTotal - exclTotal;

  const rrpDisplay = document.getElementById('sub-rrp-display');
  if (rrpDisplay) rrpDisplay.value = baseRRP.toFixed(cInfo.decimals);

  const rrpCalc = document.getElementById('sub-rrp-calc');
  if (rrpCalc) rrpCalc.textContent = fmt(rrpTotal, c);

  const rrpNote = document.getElementById('sub-rrp-calc-note');
  if (rrpNote) rrpNote.textContent = fmt(baseRRP, c) + ' × ' + staff + ' staff';

  const exclNote = document.getElementById('sub-excl-note');
  if (exclNote) exclNote.textContent = disc > 0
    ? fmt(rrpTotal, c) + ' − ' + disc + '% discount = saves ' + fmt(saving, c) + '/mo'
    : 'No discount applied';

  const exclTotal2 = document.getElementById('sub-excl-total');
  if (exclTotal2) exclTotal2.textContent = fmt(exclTotal, c) + '/mo';

  // sync slider
  const slider = document.getElementById('sub-discount-slider');
  if (slider) slider.value = disc;
  const sliderVal = document.getElementById('sub-discount-val');
  if (sliderVal) sliderVal.textContent = disc + '%';

  // sync staff input
  const bookableInput = document.getElementById('bookable-input');
  if (bookableInput) bookableInput.value = staff;
}

function getBaseRRP(addonId, country) {
  return ADDONS_DEF.find(a => a.id === addonId).rrp[country];
}

function collectAdmin() {
  const c = currentCountry;
  const bookEl = document.getElementById('bookable-input');
  if (bookEl) S[c].bookableStaff = parseInt(bookEl.value) || 1;
  const subDisc = document.getElementById('sub-discount-slider');
  if (subDisc) S[c].discounts['subscription'] = parseFloat(subDisc.value) || 0;
  const locsEl = document.getElementById('locations-input');
  if (locsEl) S[c].locations = parseInt(locsEl.value) || 1;
  ADDONS_DEF.forEach(a => {
    const sliderEl = document.getElementById('aslider-' + a.id);
    if (sliderEl) S[c].discounts[a.id] = parseFloat(sliderEl.value) || 0;
    const chkEl = document.getElementById('achk-' + a.id);
    if (chkEl) {
      if (!S[c].enabled) S[c].enabled = {};
      S[c].enabled[a.id] = chkEl.checked;
    }
  });
  S[c].notes.forEach((n, i) => {
    const tEl = document.getElementById('nt-' + i);
    const bEl = document.getElementById('nb-' + i);
    if (tEl) n.title = tEl.value;
    if (bEl) n.body  = bEl.value;
  });
}

function renderAdmin() {
  const c = currentCountry;
  const cInfo = COUNTRIES[c];
  document.getElementById('admin-country-label').textContent = cInfo.label;
  const bookEl = document.getElementById('bookable-input');
  if (bookEl) bookEl.value = S[c].bookableStaff || 1;
  const locsEl2 = document.getElementById('locations-input');
  if (locsEl2) locsEl2.value = S[c].locations || 1;
  refreshSubCard();

  document.getElementById('admin-feat-body').innerHTML = ADDONS_DEF.map(a => {
    const rrp  = getRRP(a.id, c);
    const disc = S[c].discounts[a.id] || 0;
    const excl = rrp * (1 - disc / 100);
    const on   = (S[c].enabled && S[c].enabled[a.id] !== false);
    return `<tr style="opacity:${on?'1':'0.45'}">
      <td style="text-align:center;">
        <input type="checkbox" id="achk-${a.id}" ${on?'checked':''} style="width:16px;height:16px;cursor:pointer;accent-color:var(--purple);" onchange="toggleAddon('${a.id}','${c}',this.checked)">
      </td>
      <td style="font-weight:600;font-size:12px;">${a.name}</td>
      <td style="font-size:11px;color:var(--text3);">${a.type}</td>
      <td style="font-size:13px;font-weight:600;color:var(--text2);">${fmt(rrp, c)}</td>
      <td>
        <div class="slider-row">
          <input type="range" min="0" max="60" step="1" value="${disc}" id="aslider-${a.id}"
            oninput="liveDiscount('${a.id}','${c}',this.value)" ${on?'':'disabled'}>
          <span class="slider-val" id="sval-${a.id}">${disc}%</span>
        </div>
      </td>
      <td style="font-size:14px;font-weight:700;color:var(--purple-mid);" id="excl-${a.id}">${on ? fmt(excl, c) : '—'}</td>
    </tr>`;
  }).join('');

  document.getElementById('admin-notes-body').innerHTML = S[c].notes.map((n, i) => `
    <div class="field-row">
      <div class="field"><label>Note title</label><input type="text" id="nt-${i}" value="${n.title.replace(/"/g,'&quot;')}"></div>
      <div class="field"><label>Note body</label><textarea id="nb-${i}">${n.body}</textarea></div>
    </div>`).join('');
}

function liveDiscount(addonId, country, val) {
  S[country].discounts[addonId] = parseFloat(val) || 0;
  document.getElementById('sval-' + addonId).textContent = val + '%';
  const rrp  = getRRP(addonId, country);
  const excl = rrp * (1 - val / 100);
  document.getElementById('excl-' + addonId).textContent = fmt(excl, country);
}

function toggleAddon(addonId, country, checked) {
  if (!S[country].enabled) S[country].enabled = {};
  S[country].enabled[addonId] = checked;
  renderAdmin();
  renderClient();
}

function renderClient() {
  const c = currentCountry;
  const cInfo = COUNTRIES[c];
  const partner = document.getElementById('c-partner').value || 'Partner';

  document.getElementById('banner-partner-name').textContent = partner;
  document.getElementById('banner-sub').textContent = 'Exclusive pricing \u2022 ' + cInfo.short;
  document.getElementById('c-footer-partner').textContent = partner;

  let totalRRP = 0, totalExcl = 0;

  const bookable = S[c].bookableStaff || 1;
  const locations = S[c].locations || 1;
  const cStaffEl = document.getElementById('c-bookable-staff');
  if (cStaffEl) cStaffEl.value = bookable;
  const cLocsEl = document.getElementById('c-locations');
  if (cLocsEl) cLocsEl.value = locations;
  const adminLocsEl = document.getElementById('locations-input');
  if (adminLocsEl) adminLocsEl.value = locations;

  document.getElementById('c-addons').innerHTML = ADDONS_DEF.filter(a => !S[c].enabled || S[c].enabled[a.id] !== false).map(a => {
    const baseRRP = getRRP(a.id, c);
    const disc = S[c].discounts[a.id] || 0;
    const isPerBookable = a.type === 'per_bookable';
    const isPerLocation = a.type === 'per_location';
    const multiplier = isPerBookable ? bookable : isPerLocation ? locations : 1;
    const rrp  = baseRRP * multiplier;
    const excl = rrp * (1 - disc / 100);
    const saving = rrp - excl;
    totalRRP  += rrp;
    totalExcl += excl;
    const typeLabel = isPerBookable ? `${bookable} staff × ${fmt(baseRRP, c)}` : isPerLocation ? `${locations} location${locations>1?'s':''} × ${fmt(baseRRP, c)}` : 'MRR';
    if (isPerBookable || isPerLocation) {
      const mLabel = isPerBookable
        ? `${bookable} staff × ${fmt(baseRRP, c)} per staff`
        : `${locations} location${locations>1?'s':''} × ${fmt(baseRRP, c)} per location`;
      const tagLabel = isPerBookable ? 'Per bookable staff' : 'Per location';
      return `<div class="addon-card">
        <div class="addon-header">
          <div class="addon-name">${a.name}</div>
          <div class="addon-tag">${tagLabel}</div>
        </div>
        <div style="font-size:11px;color:var(--text3);margin-bottom:8px;">${mLabel}</div>
        <div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:4px;">
          <span style="font-size:12px;color:var(--text2);">RRP total</span>
          <span style="font-size:14px;color:var(--text3);text-decoration:line-through;">${fmt(rrp, c)}</span>
        </div>
        ${disc > 0 ? `<div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:4px;">
          <span style="font-size:12px;color:var(--text2);">Discount</span>
          <span style="font-size:13px;color:#166534;font-weight:500;">−${disc}%</span>
        </div>` : ''}
        <div style="display:flex;justify-content:space-between;align-items:baseline;border-top:0.5px solid var(--border);padding-top:8px;margin-top:4px;">
          <span style="font-size:12px;font-weight:600;color:var(--text);">Your price</span>
          <span style="font-size:20px;font-weight:700;color:var(--purple-mid);">${fmt(excl, c)}<span style="font-size:11px;font-weight:400;color:var(--text2);">/mo</span></span>
        </div>
        ${saving > 0 ? `<div class="saving-pill" style="margin-top:8px;">Save ${fmt(saving, c)}/mo</div>` : ''}
      </div>`;
    }
    return `<div class="addon-card">
      <div class="addon-header">
        <div class="addon-name">${a.name}</div>
        <div class="addon-tag" style="font-size:9px;max-width:150px;text-align:right;line-height:1.4;">${typeLabel}</div>
      </div>
      <div class="price-block">
        <div class="price-excl">${fmt(excl, c)}</div>
        ${disc > 0 ? `<div class="price-rrp">${fmt(rrp, c)}</div>` : ''}
      </div>
      <div class="price-basis">per month</div>
      ${saving > 0 ? `<div class="saving-pill">Save ${fmt(saving, c)}/mo</div>` : ''}
    </div>`;
  }).join('');

  const totalSaving = totalRRP - totalExcl;
  document.getElementById('c-savings').innerHTML = `
    <div class="sbox">
      <div>
        <div class="slbl">Total monthly add-ons — exclusive pricing</div>
        <div class="ssub">vs RRP of ${fmt(totalRRP, c)}/mo &bull; all three add-ons included</div>
      </div>
      <div>
        <div class="samt">${fmt(totalExcl, c)}<span style="font-size:14px;font-weight:400;">/mo</span></div>
        ${totalSaving > 0 ? `<div style="font-size:12px;color:var(--purple-text);text-align:right;margin-top:4px;">You save ${fmt(totalSaving, c)}/mo</div>` : ''}
      </div>
    </div>`;

  const notes = S[c].notes.filter(n => n.title);
  const notesWrap = document.getElementById('c-notes-wrap');
  if (notes.length) {
    notesWrap.style.display = 'block';
    document.getElementById('c-notes').innerHTML = notes.map(n => `
      <div style="background:var(--bg);border:0.5px solid var(--border);border-left:2.5px solid var(--purple);border-radius:0 var(--rad) var(--rad) 0;padding:.8rem 1rem;">
        <div style="font-size:12px;font-weight:600;color:var(--text);margin-bottom:4px;">${n.title}</div>
        <div style="font-size:12px;color:var(--text2);line-height:1.55;">${n.body}</div>
      </div>`).join('');
  } else {
    notesWrap.style.display = 'none';
  }
}

function handleLogoUpload(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    S[currentCountry].logoData = ev.target.result;
    applyLogo(ev.target.result);
    try { localStorage.setItem(STORE_KEY, JSON.stringify(S)); } catch(err) {}
  };
  reader.readAsDataURL(file);
  e.target.value = '';
}

function applyLogo(data) {
  const clientImg   = document.getElementById('client-logo-img');
  const placeholder = document.getElementById('logo-placeholder');
  const adminPrev   = document.getElementById('admin-logo-preview');
  const removeBtn   = document.getElementById('remove-logo-btn');
  if (data) {
    clientImg.src = data; clientImg.style.display = 'block';
    placeholder.style.display = 'none';
    adminPrev.innerHTML = `<img src="${data}" style="width:100%;height:100%;object-fit:contain;">`;
    removeBtn.style.display = 'inline-block';
  } else {
    clientImg.style.display = 'none'; placeholder.style.display = 'flex';
    adminPrev.innerHTML = `<svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="#9ca3af" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><path d="M21 15l-5-5L5 21"/></svg>`;
    removeBtn.style.display = 'none';
  }
}

function removeLogo() {
  S[currentCountry].logoData = null;
  applyLogo(null);
  try { localStorage.setItem(STORE_KEY, JSON.stringify(S)); } catch(e) {}
}

function exportPDF() {
  const partner = document.getElementById('c-partner').value || 'Partner';
  const title = document.title;
  document.title = 'Fresha Add-ons Proposal - ' + partner;
  window.print();
  document.title = title;
}

function exportPNG() {
  const script = document.createElement('script');
  script.src = 'https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js';
  script.onload = function() {
    const clientView = document.getElementById('view-client');
    html2canvas(clientView, {
      scale: 2,
      backgroundColor: '#ede9fe',
      useCORS: true,
      logging: false
    }).then(canvas => {
      const link = document.createElement('a');
      const partner = document.getElementById('c-partner').value || 'Partner';
      link.download = 'Fresha-Addons-' + partner.replace(/\s+/g,'-') + '.png';
      link.href = canvas.toDataURL('image/png');
      link.click();
    });
  };
  document.head.appendChild(script);
}

loadSettings();
</script>
</body>
</html>
