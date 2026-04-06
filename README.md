<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="ImmoSaison">
<title>ImmoSaison Dashboard</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
:root{
--primary:#1a73e8;--secondary:#34a853;--danger:#ea4335;
--warning:#fbbc04;--bg:#f0f4f8;--card:#ffffff;
--text:#1a1a2e;--text-light:#6b7280;--border:#e5e7eb;
--shadow:0 4px 20px rgba(0,0,0,0.08);--radius:16px;--nav:70px
}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;
background:var(--bg);color:var(--text);min-height:100vh;
padding-bottom:calc(var(--nav) + 20px)}

/* HEADER */
.header{background:linear-gradient(135deg,#1a73e8,#0d47a1);
padding:50px 20px 25px;color:white;position:relative;overflow:hidden}
.header::before{content:'';position:absolute;top:-50%;right:-20%;
width:300px;height:300px;background:rgba(255,255,255,0.05);border-radius:50%}
.header-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:15px}
.agency-name{font-size:22px;font-weight:700}
.agency-sub{font-size:12px;opacity:0.8;margin-top:2px}
.header-avatar{width:44px;height:44px;background:rgba(255,255,255,0.2);
border-radius:50%;display:flex;align-items:center;justify-content:center;
font-size:20px;cursor:pointer}
.header-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-top:10px}
.hstat{background:rgba(255,255,255,0.15);border-radius:12px;padding:12px;text-align:center}
.hstat-val{font-size:24px;font-weight:700}
.hstat-lab{font-size:10px;opacity:0.8;margin-top:2px}

/* NAV */
.bottom-nav{position:fixed;bottom:0;left:0;right:0;height:var(--nav);
background:white;border-top:1px solid var(--border);
display:flex;align-items:center;justify-content:space-around;
padding-bottom:env(safe-area-inset-bottom);z-index:1000;
box-shadow:0 -4px 20px rgba(0,0,0,0.08)}
.nav-item{display:flex;flex-direction:column;align-items:center;gap:4px;
padding:8px 16px;border-radius:12px;cursor:pointer;
color:var(--text-light);border:none;background:none;font-family:inherit}
.nav-item.active{color:var(--primary)}
.nav-icon{width:36px;height:36px;border-radius:10px;
display:flex;align-items:center;justify-content:center;font-size:20px}
.nav-item.active .nav-icon{background:rgba(26,115,232,0.1)}
.nav-label{font-size:10px;font-weight:600}

/* PAGES */
.page{display:none;padding:20px;animation:fadeIn 0.3s ease}
.page.active{display:block}
@keyframes fadeIn{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}

/* CARDS */
.card{background:white;border-radius:var(--radius);padding:18px;
box-shadow:var(--shadow);margin-bottom:15px}
.card-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:15px}
.card-title{font-size:16px;font-weight:700}
.section-title{font-size:18px;font-weight:700;margin-bottom:15px}

/* BUTTONS */
.btn{padding:12px 20px;border-radius:12px;border:none;font-size:14px;
font-weight:600;cursor:pointer;font-family:inherit;
display:inline-flex;align-items:center;gap:8px;transition:all 0.2s}
.btn-primary{background:var(--primary);color:white}
.btn-success{background:var(--secondary);color:white}
.btn-danger{background:var(--danger);color:white}
.btn-warning{background:var(--warning);color:white}
.btn-outline{background:transparent;border:2px solid var(--primary);color:var(--primary)}
.btn-sm{padding:8px 14px;font-size:12px;border-radius:8px}
.btn-full{width:100%;justify-content:center}
.btn-icon{padding:8px;border-radius:8px;border:none;cursor:pointer;
font-size:16px;background:var(--bg)}

.fab{position:fixed;bottom:calc(var(--nav) + 20px);right:20px;
width:56px;height:56px;border-radius:50%;background:var(--primary);
color:white;border:none;font-size:24px;cursor:pointer;
box-shadow:0 4px 20px rgba(26,115,232,0.4);
display:flex;align-items:center;justify-content:center;z-index:999}

/* FORMS */
.form-group{margin-bottom:16px}
.form-label{display:block;font-size:13px;font-weight:600;
color:var(--text-light);margin-bottom:6px;text-transform:uppercase;letter-spacing:0.5px}
.form-control{width:100%;padding:13px 16px;border:2px solid var(--border);
border-radius:12px;font-size:15px;font-family:inherit;color:var(--text);
background:white;-webkit-appearance:none}
.form-control:focus{outline:none;border-color:var(--primary)}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:12px}

/* MODAL */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.5);
z-index:2000;display:none;align-items:flex-end;backdrop-filter:blur(4px)}
.modal-overlay.active{display:flex}
.modal{background:white;border-radius:24px 24px 0 0;width:100%;
max-height:90vh;overflow-y:auto;padding:20px;
padding-bottom:calc(env(safe-area-inset-bottom) + 20px);
animation:slideUp 0.3s ease}
@keyframes slideUp{from{transform:translateY(100%)}to{transform:translateY(0)}}
.modal-handle{width:40px;height:4px;background:var(--border);
border-radius:2px;margin:0 auto 20px}
.modal-title{font-size:20px;font-weight:700;margin-bottom:20px;text-align:center}

/* APARTMENT */
.apt-card{background:white;border-radius:var(--radius);
overflow:hidden;box-shadow:var(--shadow);margin-bottom:15px}
.apt-header{background:linear-gradient(135deg,#1a73e8,#0d47a1);
padding:20px;color:white;position:relative}
.apt-emoji{font-size:36px;margin-bottom:8px}
.apt-name{font-size:18px;font-weight:700}
.apt-address{font-size:12px;opacity:0.8;margin-top:4px}
.apt-badge{position:absolute;top:15px;right:15px;padding:5px 12px;
border-radius:20px;font-size:11px;font-weight:700}
.badge-available{background:rgba(52,168,83,0.2);color:#34a853;border:1px solid rgba(52,168,83,0.3)}
.badge-occupied{background:rgba(234,67,53,0.2);color:#ea4335;border:1px solid rgba(234,67,53,0.3)}
.badge-checkin{background:rgba(251,188,4,0.2);color:#f57c00;border:1px solid rgba(251,188,4,0.3)}
.apt-body{padding:15px}
.apt-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:15px}
.apt-info{text-align:center;padding:10px;background:var(--bg);border-radius:10px}
.apt-info-val{font-size:18px;font-weight:700;color:var(--primary)}
.apt-info-lab{font-size:10px;color:var(--text-light);margin-top:2px}
.apt-actions{display:flex;gap:8px}

/* RESERVATION */
.res-card{background:white;border-radius:var(--radius);padding:16px;
box-shadow:var(--shadow);margin-bottom:12px;border-left:4px solid var(--primary)}
.res-card.checkout{border-left-color:var(--danger)}
.res-card.checkin{border-left-color:var(--secondary)}
.res-card.pending{border-left-color:var(--warning)}
.res-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:10px}
.res-name{font-size:16px;font-weight:700}
.res-apt{font-size:13px;color:var(--text-light);margin-top:2px}
.res-dates{display:flex;gap:15px;margin-bottom:10px}
.res-date{display:flex;align-items:center;gap:6px;font-size:13px}
.res-date-icon{font-size:16px}
.res-actions{display:flex;gap:8px;flex-wrap:wrap}
.badge{padding:4px 10px;border-radius:20px;font-size:11px;font-weight:700}
.badge-blue{background:rgba(26,115,232,0.1);color:var(--primary)}
.badge-green{background:rgba(52,168,83,0.1);color:var(--secondary)}
.badge-red{background:rgba(234,67,53,0.1);color:var(--danger)}
.badge-yellow{background:rgba(251,188,4,0.1);color:#f57c00}

/* CLIENT */
.client-card{background:white;border-radius:var(--radius);padding:16px;
box-shadow:var(--shadow);margin-bottom:12px;
display:flex;align-items:center;gap:15px}
.client-avatar{width:50px;height:50px;border-radius:50%;
background:linear-gradient(135deg,var(--primary),#0d47a1);
display:flex;align-items:center;justify-content:center;
color:white;font-size:20px;font-weight:700;flex-shrink:0}
.client-info{flex:1}
.client-name{font-size:16px;font-weight:700}
.client-phone{font-size:13px;color:var(--text-light);margin-top:2px}
.client-actions{display:flex;gap:8px}

/* SETTINGS */
.settings-item{background:white;border-radius:var(--radius);padding:16px;
box-shadow:var(--shadow);margin-bottom:10px;
display:flex;align-items:center;gap:15px;cursor:pointer}
.settings-icon{width:44px;height:44px;border-radius:12px;
display:flex;align-items:center;justify-content:center;font-size:22px}
.settings-text{flex:1}
.settings-title{font-size:15px;font-weight:600}
.settings-sub{font-size:12px;color:var(--text-light);margin-top:2px}

/* ALERT */
.alert{padding:12px 16px;border-radius:12px;margin-bottom:15px;
display:flex;align-items:center;gap:10px;font-size:14px}
.alert-info{background:rgba(26,115,232,0.1);color:var(--primary)}
.alert-success{background:rgba(52,168,83,0.1);color:var(--secondary)}
.alert-danger{background:rgba(234,67,53,0.1);color:var(--danger)}
.alert-warning{background:rgba(251,188,4,0.1);color:#f57c00}

/* SEARCH */
.search-box{background:white;border-radius:12px;padding:12px 16px;
box-shadow:var(--shadow);margin-bottom:15px;
display:flex;align-items:center;gap:10px}
.search-box input{border:none;outline:none;flex:1;font-size:15px;font-family:inherit}
.search-icon{font-size:18px;color:var(--text-light)}

/* TOAST */
.toast{position:fixed;top:20px;left:50%;transform:translateX(-50%);
background:#1a1a2e;color:white;padding:12px 24px;border-radius:12px;
font-size:14px;font-weight:600;z-index:9999;
animation:toastIn 0.3s ease;display:none;white-space:nowrap}
.toast.show{display:block}
@keyframes toastIn{from{opacity:0;transform:translateX(-50%) translateY(-20px)}
to{opacity:1;transform:translateX(-50%) translateY(0)}}

/* EMPTY STATE */
.empty{text-align:center;padding:40px 20px;color:var(--text-light)}
.empty-icon{font-size:60px;margin-bottom:15px}
.empty-text{font-size:16px;font-weight:600;margin-bottom:8px;color:var(--text)}
.empty-sub{font-size:14px}

/* REVENUE */
.revenue-card{background:linear-gradient(135deg,#34a853,#1e7e34);
border-radius:var(--radius);padding:20px;color:white;margin-bottom:15px}
.revenue-amount{font-size:36px;font-weight:700;margin:8px 0}
.revenue-label{font-size:13px;opacity:0.8}

/* CALENDAR */
.calendar-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:4px;margin-top:10px}
.cal-day-name{text-align:center;font-size:11px;font-weight:600;
color:var(--text-light);padding:5px 0}
.cal-day{text-align:center;padding:8px 4
