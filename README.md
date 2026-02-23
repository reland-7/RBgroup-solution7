[Inventari_v10 (7) (1).html](https://github.com/user-attachments/files/25484946/Inventari_v10.7.1.html)
<!DOCTYPE html>
<html lang="sq">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Inventari v5 — Firmë Ndërtimi</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.0/chart.umd.min.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0d1117;
  --s1:#161c26;
  --s2:#1e2736;
  --s3:#242f42;
  --border:rgba(255,255,255,0.07);
  --text:#e8edf5;
  --muted:#7a8ba8;
  --orange:#f97316;
  --yellow:#eab308;
  --green:#22c55e;
  --red:#ef4444;
  --blue:#3b82f6;
  --cyan:#06b6d4;
}
body{background:var(--bg);color:var(--text);font-family:'DM Sans',sans-serif;min-height:100vh;overflow-x:hidden}

/* SIDEBAR */
.sidebar{position:fixed;left:0;top:0;bottom:0;width:220px;background:var(--s1);border-right:1px solid var(--border);z-index:100;display:flex;flex-direction:column;padding:0}
.logo{padding:24px 20px 20px;border-bottom:1px solid var(--border)}
.logo-title{font-family:'Bebas Neue',sans-serif;font-size:1.5rem;letter-spacing:0.08em;color:var(--orange);line-height:1}
.logo-sub{font-size:0.65rem;color:var(--muted);letter-spacing:0.12em;text-transform:uppercase;margin-top:2px}
.nav{flex:1;padding:16px 12px;display:flex;flex-direction:column;gap:4px}
.nav-item{display:flex;align-items:center;gap:10px;padding:10px 12px;border-radius:10px;cursor:pointer;font-size:0.82rem;font-weight:500;color:var(--muted);transition:all 0.2s;border:none;background:none;width:100%;text-align:left}
.nav-item:hover{background:var(--s2);color:var(--text)}
.nav-item.active{background:rgba(249,115,22,0.12);color:var(--orange);border:1px solid rgba(249,115,22,0.2)}
.nav-icon{font-size:1rem;width:20px;text-align:center}
.nav-badge{margin-left:auto;background:var(--orange);color:#fff;font-size:0.6rem;font-weight:700;padding:2px 6px;border-radius:99px}

/* MAIN */
.main{margin-left:220px;min-height:100vh;display:flex;flex-direction:column}
.topbar{background:var(--s1);border-bottom:1px solid var(--border);padding:16px 28px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:50}
.page-title{font-family:'Bebas Neue',sans-serif;font-size:1.6rem;letter-spacing:0.06em;color:var(--text)}
.topbar-actions{display:flex;gap:10px;align-items:center}
.btn{padding:8px 18px;border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.8rem;font-weight:600;cursor:pointer;border:none;transition:all 0.2s;letter-spacing:0.02em}
.btn-primary{background:var(--orange);color:#fff}
.btn-primary:hover{background:#ea6c0a;transform:translateY(-1px)}
.btn-ghost{background:var(--s2);color:var(--muted);border:1px solid var(--border)}
.btn-ghost:hover{color:var(--text);border-color:rgba(255,255,255,0.15)}

.content{padding:24px 28px;flex:1}

/* PANELS */
.panel{display:none}
.panel.active{display:block}

/* STATS ROW */
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;margin-bottom:24px}
.stat-card{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:20px;position:relative;overflow:hidden;animation:fadeUp 0.4s ease both}
.stat-card::after{content:'';position:absolute;bottom:0;left:0;right:0;height:3px}
.stat-card.orange::after{background:var(--orange)}
.stat-card.green::after{background:var(--green)}
.stat-card.yellow::after{background:var(--yellow)}
.stat-card.red::after{background:var(--red)}
.stat-card.blue::after{background:var(--blue)}
.stat-label{font-size:0.68rem;font-weight:600;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:8px}
.stat-value{font-family:'JetBrains Mono',monospace;font-size:1.5rem;font-weight:600;color:var(--text)}
.stat-sub{font-size:0.72rem;color:var(--muted);margin-top:4px}
.stat-icon{position:absolute;top:16px;right:16px;font-size:1.5rem;opacity:0.15}

/* TABLE */
.table-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px}
.table-title{font-size:0.9rem;font-weight:700;color:var(--text)}
.search-box{display:flex;align-items:center;gap:8px;background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:7px 12px}
.search-box input{background:none;border:none;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.8rem;outline:none;width:180px}
.search-box input::placeholder{color:var(--muted)}

.table-wrap{background:var(--s1);border:1px solid var(--border);border-radius:14px;overflow:hidden}
table{width:100%;border-collapse:collapse}
thead th{background:var(--s2);padding:11px 16px;text-align:left;font-size:0.68rem;font-weight:700;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;border-bottom:1px solid var(--border)}
tbody tr{border-bottom:1px solid var(--border);transition:background 0.15s;animation:fadeUp 0.3s ease both}
tbody tr:last-child{border-bottom:none}
tbody tr:hover{background:var(--s2)}
tbody td{padding:12px 16px;font-size:0.82rem;color:var(--text)}
.mono{font-family:'JetBrains Mono',monospace;font-size:0.78rem}
.badge{display:inline-block;padding:3px 9px;border-radius:99px;font-size:0.65rem;font-weight:700;letter-spacing:0.06em}
.badge-green{background:rgba(34,197,94,0.12);color:var(--green);border:1px solid rgba(34,197,94,0.2)}
.badge-yellow{background:rgba(234,179,8,0.12);color:var(--yellow);border:1px solid rgba(234,179,8,0.2)}
.badge-red{background:rgba(239,68,68,0.12);color:var(--red);border:1px solid rgba(239,68,68,0.2)}
.badge-blue{background:rgba(59,130,246,0.12);color:var(--blue);border:1px solid rgba(59,130,246,0.2)}
.badge-orange{background:rgba(249,115,22,0.12);color:var(--orange);border:1px solid rgba(249,115,22,0.2)}

.action-btn{background:none;border:1px solid var(--border);color:var(--muted);padding:4px 10px;border-radius:6px;font-size:0.72rem;cursor:pointer;transition:all 0.15s;font-family:'DM Sans',sans-serif}
.action-btn:hover{border-color:var(--orange);color:var(--orange)}
.action-btn.del:hover{border-color:var(--red);color:var(--red)}

/* MODAL */
.modal-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.7);z-index:200;align-items:center;justify-content:center;backdrop-filter:blur(4px)}
.modal-overlay.open{display:flex}
.modal{background:var(--s1);border:1px solid var(--border);border-radius:18px;width:560px;max-width:96vw;max-height:90vh;overflow-y:auto;padding:28px;animation:modalIn 0.25s ease}
.modal-title{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:0.06em;margin-bottom:20px;color:var(--orange)}
.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px}
.form-grid.full{grid-template-columns:1fr}
.field{display:flex;flex-direction:column;gap:6px}
.field label{font-size:0.7rem;font-weight:700;color:var(--muted);letter-spacing:0.08em;text-transform:uppercase}
.field input,.field select,.field textarea{background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:9px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.82rem;outline:none;transition:border-color 0.2s;width:100%}
.field input:focus,.field select:focus,.field textarea:focus{border-color:var(--orange)}
.field select option{background:var(--s2)}
.modal-actions{display:flex;gap:10px;justify-content:flex-end;margin-top:20px}

/* BIBLIOTEKA */
.bib-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:16px;margin-top:16px}
.bib-card{background:var(--s2);border:1px solid var(--border);border-radius:14px;padding:18px;cursor:pointer;transition:all 0.2s;position:relative}
.bib-card:hover{border-color:var(--orange);transform:translateY(-2px);box-shadow:0 8px 24px rgba(0,0,0,0.3)}
.bib-card-icon{font-size:2rem;margin-bottom:10px}
.bib-card-title{font-weight:700;font-size:0.9rem;margin-bottom:4px}
.bib-card-sub{font-size:0.7rem;color:var(--muted)}
.bib-card-type{position:absolute;top:12px;right:12px;font-size:0.6rem;font-weight:700;letter-spacing:0.08em;text-transform:uppercase;background:var(--s1);border:1px solid var(--border);border-radius:6px;padding:2px 7px;color:var(--muted)}
.bib-upload-zone{border:2px dashed var(--border);border-radius:14px;padding:40px;text-align:center;cursor:pointer;transition:all 0.2s;background:var(--s2);position:relative}
.bib-upload-zone:hover,.bib-upload-zone.drag{border-color:var(--orange);background:rgba(249,115,22,0.05)}
.bib-upload-zone input{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.bib-fill-row{display:grid;grid-template-columns:1fr 2fr;gap:10px;align-items:center;padding:8px 0;border-bottom:1px solid var(--border)}
.bib-fill-row:last-child{border-bottom:none}
.bib-field-label{font-size:0.72rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:0.06em}
.bib-field-auto{font-size:0.65rem;color:var(--green);margin-top:2px}
.bib-section{background:var(--s2);border:1px solid var(--border);border-radius:12px;padding:16px 20px;margin-bottom:14px}
.bib-section-title{font-size:0.7rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:0.1em;margin-bottom:12px;display:flex;align-items:center;gap:6px}
/* PROGRESS BAR */
.prog-track{background:rgba(255,255,255,0.06);border-radius:99px;height:5px;margin-top:4px;overflow:hidden}
.prog-fill{height:100%;border-radius:99px;transition:width 0.8s cubic-bezier(0.4,0,0.2,1)}

/* ALERT ROWS */
.alert-list{display:flex;flex-direction:column;gap:10px;margin-bottom:24px}
.alert-item{display:flex;align-items:center;gap:14px;background:rgba(239,68,68,0.06);border:1px solid rgba(239,68,68,0.15);border-radius:12px;padding:14px 18px}
.alert-item.warn{background:rgba(234,179,8,0.06);border-color:rgba(234,179,8,0.15)}
.alert-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.alert-dot.red{background:var(--red)}
.alert-dot.warn{background:var(--yellow)}
.alert-text{font-size:0.82rem;flex:1}
.alert-name{font-weight:700;color:var(--text)}
.alert-sub{color:var(--muted);font-size:0.75rem}

/* SECTION DIVIDER */
.section-label{font-size:0.68rem;font-weight:700;color:var(--muted);letter-spacing:0.12em;text-transform:uppercase;margin:24px 0 12px;display:flex;align-items:center;gap:8px}
.section-label::after{content:'';flex:1;height:1px;background:var(--border)}

/* FURNITOR CARDS */
.furnitor-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:16px;margin-bottom:24px}
.furnitor-card{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:20px;position:relative;overflow:hidden;animation:fadeUp 0.4s ease both}
.furnitor-card::before{content:'';position:absolute;top:0;left:0;right:0;height:3px}
.f0::before{background:linear-gradient(90deg,#f97316,#eab308)}
.f1::before{background:linear-gradient(90deg,#3b82f6,#06b6d4)}
.f2::before{background:linear-gradient(90deg,#22c55e,#06b6d4)}
.f3::before{background:linear-gradient(90deg,#a855f7,#ec4899)}
.f4::before{background:linear-gradient(90deg,#ef4444,#f97316)}
.f-name{font-weight:700;font-size:0.92rem;margin-bottom:2px}
.f-nid{font-family:'JetBrains Mono',monospace;font-size:0.68rem;color:var(--muted);margin-bottom:12px}
.f-row{display:flex;justify-content:space-between;align-items:center;font-size:0.76rem;margin-bottom:6px}
.f-row-label{color:var(--muted)}
.f-row-val{font-family:'JetBrains Mono',monospace;font-weight:600}

/* TABS */
.tabs{display:flex;gap:4px;background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:4px;width:fit-content;margin-bottom:20px}
.tab{padding:7px 16px;border-radius:7px;font-size:0.78rem;font-weight:600;cursor:pointer;border:none;background:none;color:var(--muted);transition:all 0.2s;font-family:'DM Sans',sans-serif}
.tab.active{background:var(--orange);color:#fff}

/* EMPTY */
.empty{text-align:center;padding:48px 20px;color:var(--muted)}
.empty-icon{font-size:2.5rem;margin-bottom:10px;opacity:0.4}

/* BACKUP AREA */
.backup-area{padding:10px 12px 16px;border-top:1px solid var(--border)}

/* BILANCI */
.bil-tatim-box{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:4px}
.bil-tatim-card{background:var(--s1);border:1px solid var(--border);border-radius:12px;padding:16px;position:relative}
.bil-tatim-card::after{content:'';position:absolute;bottom:0;left:0;right:0;height:3px;border-radius:0 0 12px 12px;background:var(--orange)}
.bil-tatim-card.green::after{background:var(--green)}
.bil-tatim-card.red::after{background:var(--red)}
.bil-tc-label{font-size:0.65rem;font-weight:700;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:6px}
.bil-tc-val{font-family:'JetBrains Mono',monospace;font-size:1.2rem;font-weight:600;color:var(--text)}
.bil-tc-sub{font-size:0.68rem;color:var(--muted);margin-top:4px}
.backup-status{font-size:0.65rem;color:var(--green);margin-bottom:8px;padding:0 4px;opacity:0.8}
.backup-status.saving{color:var(--yellow)}
.backup-btn{display:flex;align-items:center;gap:7px;padding:7px 10px;border-radius:8px;cursor:pointer;font-size:0.75rem;font-weight:500;color:var(--muted);border:1px solid var(--border);background:var(--s2);width:100%;text-align:left;margin-bottom:4px;transition:all 0.2s;font-family:'DM Sans',sans-serif}
.backup-btn:hover{border-color:var(--orange);color:var(--orange)}
.backup-btn-subj{border-style:dashed;color:var(--cyan)}
.backup-btn-subj:hover{border-color:var(--cyan) !important;color:var(--cyan) !important}
.toast{position:fixed;bottom:24px;right:24px;background:var(--s2);border:1px solid var(--border);border-radius:12px;padding:12px 20px;font-size:0.82rem;color:var(--text);z-index:999;display:flex;align-items:center;gap:8px;box-shadow:0 8px 32px rgba(0,0,0,0.4);animation:toastIn 0.3s ease;pointer-events:none}
@keyframes toastIn{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
@keyframes modalIn{from{opacity:0;transform:scale(0.95)}to{opacity:1;transform:scale(1)}}

/* INVENTAR LIVE CARDS */
.inv-card{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:18px;position:relative;overflow:hidden;animation:fadeUp 0.3s ease both;transition:transform 0.15s,box-shadow 0.15s}
.inv-card:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(0,0,0,0.3)}
.inv-card::before{content:'';position:absolute;top:0;left:0;right:0;height:4px}
.inv-card.normal::before{background:var(--green)}
.inv-card.ulet::before{background:var(--yellow)}
.inv-card.kritik::before{background:var(--red)}
.inv-card-header{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:12px}
.inv-card-name{font-weight:700;font-size:0.9rem;color:var(--text);line-height:1.3}
.inv-card-cat{font-size:0.65rem;color:var(--muted);margin-top:2px;letter-spacing:0.06em;text-transform:uppercase}
.inv-sasia-big{font-family:'JetBrains Mono',monospace;font-size:2rem;font-weight:700;line-height:1;margin-bottom:2px}
.inv-sasia-big.normal{color:var(--green)}
.inv-sasia-big.ulet{color:var(--yellow)}
.inv-sasia-big.kritik{color:var(--red)}
.inv-njesia{font-size:0.7rem;color:var(--muted)}
.inv-prog-wrap{margin:10px 0}
.inv-prog-label{display:flex;justify-content:space-between;font-size:0.68rem;color:var(--muted);margin-bottom:4px}
.inv-meta{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-top:10px;padding-top:10px;border-top:1px solid var(--border)}
.inv-meta-item{font-size:0.72rem}
.inv-meta-label{color:var(--muted);font-size:0.62rem;text-transform:uppercase;letter-spacing:0.06em}
.inv-meta-val{font-family:'JetBrains Mono',monospace;font-weight:600;color:var(--text)}
.inv-card-actions{display:flex;gap:6px;margin-top:12px;padding-top:10px;border-top:1px solid var(--border)}
.inv-btn{flex:1;padding:7px 10px;border-radius:7px;font-size:0.74rem;font-weight:600;cursor:pointer;border:none;font-family:'DM Sans',sans-serif;transition:all 0.15s;text-align:center}
.inv-btn-add{background:rgba(249,115,22,0.12);color:var(--orange);border:1px solid rgba(249,115,22,0.2)}
.inv-btn-add:hover{background:rgba(249,115,22,0.22)}
.inv-btn-sell{background:rgba(34,197,94,0.12);color:var(--green);border:1px solid rgba(34,197,94,0.2)}
.inv-btn-sell:hover{background:rgba(34,197,94,0.22)}
.inv-btn-edit{background:var(--s2);color:var(--muted);border:1px solid var(--border)}
.inv-btn-edit:hover{color:var(--text)}
.subject-area{padding:10px 12px;border-bottom:1px solid var(--border)}
.subject-section-label{font-size:0.6rem;font-weight:700;color:var(--muted);letter-spacing:0.12em;text-transform:uppercase;margin-bottom:6px;padding:0 4px}
.subject-list{display:flex;flex-direction:column;gap:2px}
.subject-btn{display:flex;align-items:center;gap:8px;padding:8px 10px;border-radius:8px;cursor:pointer;font-size:0.78rem;font-weight:600;color:var(--muted);transition:all 0.2s;border:1px solid transparent;background:none;width:100%;text-align:left}
.subject-btn:hover{background:var(--s2);color:var(--text)}
.subject-btn.active{background:rgba(249,115,22,0.1);color:var(--orange);border-color:rgba(249,115,22,0.25)}
.subject-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.subject-name{flex:1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.subject-del{opacity:0;font-size:0.7rem;padding:1px 4px;border-radius:4px;background:rgba(239,68,68,0.15);color:var(--red);border:none;cursor:pointer;transition:opacity 0.2s}
.subject-btn:hover .subject-del{opacity:1}
.subject-btn:hover .subj-edit-btn{opacity:1!important}
.subject-add-btn{display:flex;align-items:center;gap:6px;padding:7px 10px;border-radius:8px;cursor:pointer;font-size:0.75rem;color:var(--muted);border:1px dashed var(--border);background:none;width:100%;text-align:left;margin-top:4px;transition:all 0.2s;font-family:'DM Sans',sans-serif}
.subject-add-btn:hover{border-color:var(--orange);color:var(--orange)}

/* SUBJECT TOPBAR INDICATOR */
.subject-indicator{display:flex;align-items:center;gap:8px;background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:6px 12px;font-size:0.78rem;font-weight:600;color:var(--text)}
.subject-indicator-dot{width:8px;height:8px;border-radius:50%}

/* COLOR PICKER */
.color-picker{display:flex;gap:6px;flex-wrap:wrap;margin-top:4px}
.color-opt{width:26px;height:26px;border-radius:50%;cursor:pointer;border:2px solid transparent;transition:all 0.15s}
.color-opt:hover{transform:scale(1.1)}
.color-opt.sel{border-color:#fff;transform:scale(1.15)}

/* ═══ PROJEKTET ═══ */
.proj-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(320px,1fr));gap:16px;margin-bottom:24px}
.proj-card{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:20px;position:relative;overflow:hidden;animation:fadeUp 0.3s ease both;transition:transform 0.15s,box-shadow 0.15s}
.proj-card:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(0,0,0,0.3)}
.proj-card::before{content:'';position:absolute;top:0;left:0;right:0;height:4px}
.proj-card.aktiv::before{background:linear-gradient(90deg,var(--orange),var(--yellow))}
.proj-card.perfunduar::before{background:var(--green)}
.proj-card.pauzuar::before{background:var(--muted)}
.proj-card.vonuar::before{background:var(--red)}
.proj-card-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:10px}
.proj-name{font-weight:700;font-size:0.95rem;color:var(--text);line-height:1.3}
.proj-klienti{font-size:0.72rem;color:var(--muted);margin-top:2px}
.proj-meta-row{display:flex;justify-content:space-between;font-size:0.75rem;margin-bottom:5px}
.proj-meta-row .lbl{color:var(--muted)}
.proj-meta-row .val{font-family:'JetBrains Mono',monospace;font-weight:600}
.proj-prog-wrap{margin:10px 0 6px}
.proj-prog-label{display:flex;justify-content:space-between;font-size:0.68rem;color:var(--muted);margin-bottom:4px}
.proj-actions{display:flex;gap:6px;margin-top:12px;padding-top:10px;border-top:1px solid var(--border)}
.faza-list{display:flex;flex-direction:column;gap:6px;margin:10px 0}
.faza-item{display:flex;align-items:center;gap:8px;font-size:0.78rem;background:var(--s2);border-radius:8px;padding:7px 12px;border:1px solid var(--border)}
.faza-check{width:16px;height:16px;border-radius:4px;border:2px solid var(--border);cursor:pointer;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:0.7rem}
.faza-check.done{background:var(--green);border-color:var(--green)}
.faza-name{flex:1;color:var(--text)}
.faza-name.done{text-decoration:line-through;color:var(--muted)}
.proj-detail-box{background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:14px;margin-bottom:14px;font-size:0.82rem}

/* ═══ FATURAT ═══ */
.fat-card{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:18px;animation:fadeUp 0.3s ease both;transition:transform 0.15s}
.fat-card:hover{transform:translateY(-2px);box-shadow:0 6px 20px rgba(0,0,0,0.25)}
.fat-nr{font-family:'JetBrains Mono',monospace;font-size:0.72rem;color:var(--muted);margin-bottom:4px}
.fat-klienti{font-weight:700;font-size:0.92rem;margin-bottom:6px}
.fat-total{font-family:'JetBrains Mono',monospace;font-size:1.4rem;font-weight:700;color:var(--orange);margin:8px 0 4px}
.fat-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:14px;margin-bottom:24px}
.fat-lines{width:100%;border-collapse:collapse;font-size:0.8rem}
.fat-lines th{background:var(--s2);padding:8px 12px;text-align:left;font-size:0.65rem;font-weight:700;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase}
.fat-lines td{padding:8px 12px;border-bottom:1px solid var(--border)}
.fat-lines tr:last-child td{border-bottom:none}
.fat-total-box{background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:14px;text-align:right;margin-top:10px}
.fat-print-area{display:none}
@media print{
  .sidebar,.topbar,.topbar-actions,.btn,.nav,.backup-area,.subject-area,.fat-print-area{display:none!important}
  .fat-print-area{display:block!important}
  body{background:#fff;color:#000}
}

/* ═══ RAPORTI MUJOR ═══ */
.rap-selector{display:flex;align-items:center;gap:12px;margin-bottom:24px;flex-wrap:wrap;background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:16px 20px}
.rap-selector select{background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:8px 14px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.85rem;outline:none;cursor:pointer}
.rap-selector select:focus{border-color:var(--orange)}
.rap-month-nav{display:flex;align-items:center;gap:8px}
.rap-nav-btn{background:var(--s2);border:1px solid var(--border);color:var(--muted);width:32px;height:32px;border-radius:8px;cursor:pointer;font-size:1rem;display:flex;align-items:center;justify-content:center;transition:all 0.15s}
.rap-nav-btn:hover{border-color:var(--orange);color:var(--orange)}
.rap-period-label{font-family:'Bebas Neue',sans-serif;font-size:1.3rem;letter-spacing:0.06em;color:var(--orange);min-width:160px;text-align:center}
.rap-lock-btn{margin-left:auto;display:flex;align-items:center;gap:6px;padding:8px 16px;border-radius:8px;font-size:0.78rem;font-weight:700;cursor:pointer;border:none;font-family:'DM Sans',sans-serif;transition:all 0.2s}
.rap-lock-btn.open{background:rgba(249,115,22,0.12);color:var(--orange);border:1px solid rgba(249,115,22,0.25)}
.rap-lock-btn.locked{background:rgba(34,197,94,0.12);color:var(--green);border:1px solid rgba(34,197,94,0.25)}

.rap-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:20px}
.rap-grid.full{grid-template-columns:1fr}
.rap-section{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:20px;position:relative}
.rap-section-title{font-size:0.72rem;font-weight:700;color:var(--muted);letter-spacing:0.12em;text-transform:uppercase;margin-bottom:14px;display:flex;align-items:center;gap:8px}
.rap-section-title::after{content:'';flex:1;height:1px;background:var(--border)}
.rap-field{display:flex;flex-direction:column;gap:5px;margin-bottom:10px}
.rap-field label{font-size:0.68rem;font-weight:700;color:var(--muted);letter-spacing:0.08em;text-transform:uppercase}
.rap-field input,.rap-field select,.rap-field textarea{background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:8px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.82rem;outline:none;transition:border-color 0.2s;width:100%}
.rap-field input:focus,.rap-field select:focus,.rap-field textarea:focus{border-color:var(--orange)}
.rap-field input:disabled,.rap-field select:disabled,.rap-field textarea:disabled{opacity:0.55;cursor:not-allowed}
.rap-2col{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.rap-3col{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px}
.rap-result-box{background:var(--s2);border-radius:10px;padding:14px;margin-top:10px}
.rap-result-row{display:flex;justify-content:space-between;align-items:center;padding:5px 0;font-size:0.82rem;border-bottom:1px solid var(--border)}
.rap-result-row:last-child{border-bottom:none}
.rap-result-total{display:flex;justify-content:space-between;align-items:center;padding:10px 0 0;margin-top:4px;font-weight:700;font-size:0.95rem}
.rap-kpi-row{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:20px}
.rap-kpi{background:var(--s1);border:1px solid var(--border);border-radius:12px;padding:16px;text-align:center;position:relative;overflow:hidden}
.rap-kpi::after{content:'';position:absolute;bottom:0;left:0;right:0;height:3px}
.rap-kpi.pos::after{background:var(--green)}
.rap-kpi.neg::after{background:var(--red)}
.rap-kpi.neu::after{background:var(--orange)}
.rap-kpi.info::after{background:var(--blue)}
.rap-kpi-label{font-size:0.62rem;font-weight:700;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:6px}
.rap-kpi-val{font-family:'JetBrains Mono',monospace;font-size:1.2rem;font-weight:700}
.rap-kpi-delta{font-size:0.68rem;margin-top:3px}
.rap-punator-row{display:grid;grid-template-columns:2fr 1fr 1fr 1fr;gap:8px;align-items:center;background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:8px 12px;margin-bottom:6px;font-size:0.8rem}
.rap-punator-row input{background:var(--s3);border:1px solid var(--border);border-radius:6px;padding:5px 8px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.78rem;outline:none;width:100%}
.rap-punator-row input:focus{border-color:var(--orange)}
.rap-punator-row input:disabled{opacity:0.5;cursor:not-allowed}
.rap-add-row-btn{background:none;border:1px dashed var(--border);color:var(--muted);padding:7px 14px;border-radius:8px;cursor:pointer;font-size:0.75rem;width:100%;margin-top:4px;font-family:'DM Sans',sans-serif;transition:all 0.2s}
.rap-add-row-btn:hover{border-color:var(--orange);color:var(--orange)}
.rap-del-btn{background:rgba(239,68,68,0.1);color:var(--red);border:1px solid rgba(239,68,68,0.2);padding:4px 8px;border-radius:6px;cursor:pointer;font-size:0.7rem}
.rap-history-strip{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:10px;margin-bottom:20px}
.rap-hist-card{background:var(--s1);border:1px solid var(--border);border-radius:10px;padding:12px 14px;cursor:pointer;transition:all 0.15s}
.rap-hist-card:hover{border-color:var(--orange)}
.rap-hist-card.active{border-color:var(--orange);background:rgba(249,115,22,0.07)}
.rap-hist-month{font-family:'Bebas Neue',sans-serif;font-size:1rem;letter-spacing:0.06em;color:var(--text)}
.rap-hist-val{font-family:'JetBrains Mono',monospace;font-size:0.72rem;margin-top:3px}
.rap-hist-badge{font-size:0.6rem;margin-top:4px}
.rap-chart-wrap{background:var(--s1);border:1px solid var(--border);border-radius:14px;padding:20px;margin-bottom:20px}
.rap-save-bar{position:sticky;bottom:16px;background:var(--s1);border:1px solid var(--border);border-radius:12px;padding:12px 20px;display:flex;align-items:center;justify-content:space-between;gap:12px;box-shadow:0 8px 32px rgba(0,0,0,0.4);z-index:10;margin-top:16px}
.rap-autosave-hint{font-size:0.72rem;color:var(--muted)}

/* ═══ GLOBAL SEARCH ═══ */
.gs-group-lbl{font-size:0.6rem;font-weight:700;color:var(--muted);letter-spacing:0.14em;text-transform:uppercase;padding:10px 12px 4px}
.gs-item{display:flex;align-items:center;gap:10px;padding:9px 12px;border-radius:9px;cursor:pointer;transition:background 0.1s}
.gs-item:hover,.gs-item.sel{background:var(--s2)}
.gs-item.sel{outline:1px solid rgba(249,115,22,0.3)}
.gs-icon{width:30px;height:30px;border-radius:7px;display:flex;align-items:center;justify-content:center;font-size:0.9rem;flex-shrink:0}
.gs-main{flex:1;min-width:0}
.gs-title{font-size:0.83rem;font-weight:600;color:var(--text);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.gs-sub{font-size:0.7rem;color:var(--muted);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.gs-badge{font-size:0.62rem;font-weight:700;padding:2px 8px;border-radius:99px;flex-shrink:0}
.gs-badge.green{background:rgba(34,197,94,0.1);color:var(--green)}
.gs-badge.orange{background:rgba(249,115,22,0.1);color:var(--orange)}
.gs-badge.red{background:rgba(239,68,68,0.1);color:var(--red)}
.gs-badge.blue{background:rgba(59,130,246,0.1);color:var(--blue)}
.gs-badge.yellow{background:rgba(234,179,8,0.1);color:var(--yellow)}
.gs-empty{padding:28px;text-align:center;color:var(--muted);font-size:0.82rem}

/* ═══ EXCEL IMPORT ═══ */
.imp-modal{background:var(--s1);border:1px solid var(--border);border-radius:18px;width:700px;max-width:96vw;max-height:90vh;overflow-y:auto;padding:28px;animation:modalIn 0.25s ease}
.imp-drop{border:2px dashed var(--border);border-radius:14px;padding:32px 24px;text-align:center;cursor:pointer;transition:all 0.2s;position:relative;margin-bottom:16px}
.imp-drop:hover,.imp-drop.dragover{border-color:var(--orange);background:rgba(249,115,22,0.05)}
.imp-drop-icon{font-size:2.2rem;margin-bottom:8px;opacity:0.6}
.imp-drop-text{font-size:0.82rem;color:var(--muted);line-height:1.6}
.imp-drop input[type=file]{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.imp-tabs{display:flex;gap:4px;margin:0 0 14px;background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:4px;width:fit-content}
.imp-tab{padding:6px 14px;border-radius:7px;font-size:0.74rem;font-weight:600;cursor:pointer;border:none;background:none;color:var(--muted);transition:all 0.15s;font-family:'DM Sans',sans-serif}
.imp-tab.active{background:var(--orange);color:#fff}
.imp-table-wrap{overflow-x:auto;border:1px solid var(--border);border-radius:10px;max-height:220px;overflow-y:auto;margin-bottom:14px}
.imp-table{width:100%;border-collapse:collapse;font-size:0.74rem}
.imp-table th{background:var(--s2);padding:7px 10px;text-align:left;font-size:0.62rem;font-weight:700;color:var(--muted);letter-spacing:0.08em;text-transform:uppercase;border-bottom:1px solid var(--border);position:sticky;top:0;z-index:1}
.imp-table td{padding:6px 10px;border-bottom:1px solid var(--border)}
.imp-table tr:last-child td{border-bottom:none}
.imp-table tr:hover td{background:var(--s2)}
.imp-map-row{display:grid;grid-template-columns:1fr 24px 1fr;gap:8px;align-items:center;margin-bottom:6px}
.imp-map-row select{background:var(--s2);border:1px solid var(--border);border-radius:7px;padding:7px 10px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.76rem;outline:none;width:100%}
.imp-map-row select:focus{border-color:var(--orange)}
.imp-arrow{color:var(--orange);text-align:center;font-size:1.1rem}
.imp-col-label{color:var(--muted);font-size:0.72rem;background:var(--s2);border:1px solid var(--border);border-radius:7px;padding:7px 10px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.imp-sheet-sel{display:flex;gap:6px;margin-bottom:12px;flex-wrap:wrap}
.imp-sheet-btn{padding:5px 12px;border-radius:6px;font-size:0.73rem;font-weight:600;cursor:pointer;border:1px solid var(--border);background:var(--s2);color:var(--muted);font-family:'DM Sans',sans-serif;transition:all 0.15s}
.imp-sheet-btn.active{background:var(--orange);color:#fff;border-color:var(--orange)}
.imp-result-box{background:var(--s2);border-radius:10px;padding:12px 14px;margin-top:12px;font-size:0.8rem;display:flex;flex-direction:column;gap:5px}
.imp-stat{display:flex;align-items:center;gap:8px}
.imp-stat .ok{color:var(--green)} .imp-stat .warn{color:var(--yellow)} .imp-stat .err{color:var(--red)}
.imp-section-lbl{font-size:0.68rem;font-weight:700;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;margin:14px 0 8px;display:flex;align-items:center;gap:8px}
.imp-section-lbl::after{content:'';flex:1;height:1px;background:var(--border)}
</style>
</head>
<body>

<!-- SIDEBAR -->
<div class="sidebar">
  <div class="logo">
    <div class="logo-title">🏗️ BuildTrack</div>
    <div class="logo-sub">Sistem Inventari v5</div>
  </div>

  <!-- SUBJECT SWITCHER -->
  <div class="subject-area">
    <div class="subject-section-label">📁 Subjektet</div>
    <div class="subject-list" id="subject-list"></div>
    <button class="subject-add-btn" onclick="openSubjectModal()">＋ Shto Subjekt</button>
  </div>

  <nav class="nav">
    <button class="nav-item active" onclick="showPanel('dashboard',this)"><span class="nav-icon">📊</span> Dashboard</button>
    <button class="nav-item" onclick="showPanel('inventar',this)"><span class="nav-icon">📦</span> Inventar Live <span class="nav-badge" id="badge-inv-low" style="display:none">!</span></button>
    <button class="nav-item" onclick="showPanel('materiale',this)"><span class="nav-icon">🧱</span> Materiale <span class="nav-badge" id="badge-mat">0</span></button>
    <button class="nav-item" onclick="showPanel('pajisje',this)"><span class="nav-icon">⚙️</span> Pajisje & Mjete</button>
    <button class="nav-item" onclick="showPanel('shitje',this)"><span class="nav-icon">💰</span> Shitje & Stok</button>
    <button class="nav-item" onclick="showPanel('furnitoret',this)"><span class="nav-icon">🚛</span> Furnitorët</button>
    <button class="nav-item" onclick="showPanel('bilanci',this)"><span class="nav-icon">📑</span> Bilanci & Tatimi <span class="nav-badge" id="badge-bil" style="display:none">!</span></button>
    <button class="nav-item" onclick="showPanel('hr',this)"><span class="nav-icon">👷</span> Paga & HR</button>
    <button class="nav-item" onclick="showPanel('projektet',this)"><span class="nav-icon">📋</span> Kontratat & Proj. <span class="nav-badge" id="badge-proj" style="display:none">!</span></button>
    <button class="nav-item" onclick="showPanel('faturat',this)"><span class="nav-icon">🧾</span> Fatura & Oferta <span class="nav-badge" id="badge-fat" style="display:none">!</span></button>
    <button class="nav-item" onclick="showPanel('raporti',this)"><span class="nav-icon">🗓️</span> Raporti Mujor</button>
    <div style="height:1px;background:var(--border);margin:8px 0"></div>
    <button class="nav-item" onclick="showPanel('biblioteka',this)"><span class="nav-icon">📚</span> Biblioteka Formatesh</button>
  </nav>

  <!-- BACKUP AREA -->
  <div class="backup-area">
    <div class="subject-section-label">💾 Ruajtja & Backup</div>
    <div class="backup-status" id="backup-status">✅ Ruajtur automatikisht</div>
    <button class="backup-btn" onclick="exportBackup()">📤 Shkarko Të Gjitha</button>
    <button class="backup-btn" onclick="document.getElementById('import-file').click()">📥 Ngarko Backup</button>
    <input type="file" id="import-file" accept=".json" style="display:none" onchange="importBackup(event)">
    <button class="backup-btn backup-btn-subj" onclick="exportCurrentSubject()">📋 Shkarko Subjektin Aktual</button>
    <button class="backup-btn" style="border-color:rgba(34,197,94,0.3);color:var(--green);margin-top:6px" onclick="openExcelImport()">📊 Importo nga Excel</button>
  </div>
</div>

<!-- MAIN -->
<div class="main">
  <div class="topbar">
    <div class="page-title" id="topbar-title">Dashboard</div>
    <div class="topbar-actions">
      <button class="btn btn-ghost" onclick="openGlobalSearch()" style="display:flex;align-items:center;gap:7px;color:var(--muted);border-color:var(--border)">
        <span>🔍</span><span>Kërko</span>
        <span style="font-size:0.62rem;background:var(--s3);padding:2px 6px;border-radius:5px;color:var(--muted);margin-left:2px">Ctrl+K</span>
      </button>
      <div class="subject-indicator"><div class="subject-indicator-dot" id="subj-dot"></div><span id="subj-name-top">—</span></div>
      <button class="btn btn-ghost" onclick="exportCSV()">📥 Eksporto CSV</button>
      <button class="btn btn-primary" id="btn-add" onclick="openModal()">＋ Shto të Re</button>
    </div>
  </div>

  <div class="content">

    <!-- ═══ DASHBOARD ═══ -->
    <div class="panel active" id="panel-dashboard">
      <div class="stats-row">
        <div class="stat-card orange" style="animation-delay:0s">
          <div class="stat-icon">🧱</div>
          <div class="stat-label">Artikuj Aktiv</div>
          <div class="stat-value" id="d-artikuj">0</div>
          <div class="stat-sub">Materiale + Pajisje</div>
        </div>
        <div class="stat-card green" style="animation-delay:0.05s">
          <div class="stat-icon">💰</div>
          <div class="stat-label">Vlera Totale Stokut</div>
          <div class="stat-value" id="d-vlera">0 L</div>
          <div class="stat-sub">Çmimi blerje × sasia</div>
        </div>
        <div class="stat-card yellow" style="animation-delay:0.1s">
          <div class="stat-icon">⚠️</div>
          <div class="stat-label">Stok i Ulët</div>
          <div class="stat-value" id="d-ulët">0</div>
          <div class="stat-sub">Nën nivelin minimal</div>
        </div>
        <div class="stat-card red" style="animation-delay:0.15s">
          <div class="stat-icon">🚛</div>
          <div class="stat-label">Furnitorë Aktiv</div>
          <div class="stat-value" id="d-furnitorë">0</div>
          <div class="stat-sub">Partner aktualë</div>
        </div>
      </div>

      <div class="stats-row" style="grid-template-columns:repeat(3,1fr);margin-bottom:16px">
        <div class="stat-card blue" style="animation-delay:0.2s">
          <div class="stat-icon">🔗</div>
          <div class="stat-label">Shitje → Inventar</div>
          <div class="stat-value" id="d-shitje-cnt" style="font-size:1.1rem">Auto</div>
          <div class="stat-sub">Stoku ulet/rritet automatikisht</div>
        </div>
        <div class="stat-card green" style="animation-delay:0.25s">
          <div class="stat-icon">📑</div>
          <div class="stat-label">Blerje → Bilanci</div>
          <div class="stat-value" id="d-blerje-cnt" style="font-size:1.1rem">Auto</div>
          <div class="stat-sub">Regjistrohet si shpenzim direkt</div>
        </div>
        <div class="stat-card yellow" style="animation-delay:0.3s">
          <div class="stat-icon">💼</div>
          <div class="stat-label">Paga → Bilanci</div>
          <div class="stat-value" id="d-paga-cnt" style="font-size:1.1rem">Auto</div>
          <div class="stat-sub">HR merr llogaritë automatikisht</div>
        </div>
      </div>

      <div class="section-label">⚠️ Alarme Stoku</div>
      <div id="alert-list" class="alert-list"></div>

      <div class="section-label">📋 Lëvizjet e Fundit</div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Artikull</th><th>Kategori</th><th>Sasia</th><th>Vlera</th><th>Statusi</th></tr></thead>
          <tbody id="dash-table"></tbody>
        </table>
      </div>
    </div>

    <!-- ═══ INVENTAR LIVE ═══ -->
    <div class="panel" id="panel-inventar">
      <!-- Stats row -->
      <div class="stats-row" style="margin-bottom:20px">
        <div class="stat-card orange"><div class="stat-icon">📦</div><div class="stat-label">Total Artikuj</div><div class="stat-value" id="inv-total-art">0</div><div class="stat-sub">Materiale në inventar</div></div>
        <div class="stat-card green"><div class="stat-icon">💰</div><div class="stat-label">Vlera Stokut</div><div class="stat-value" id="inv-vlera">0 L</div><div class="stat-sub">Çmim blerje × sasi</div></div>
        <div class="stat-card yellow"><div class="stat-icon">⚠️</div><div class="stat-label">Stok i Ulët</div><div class="stat-value" id="inv-ulet">0</div><div class="stat-sub">Nën nivelin minimal</div></div>
        <div class="stat-card red"><div class="stat-icon">🚨</div><div class="stat-label">Stok Kritik</div><div class="stat-value" id="inv-kritik">0</div><div class="stat-sub">Duhet urgjentisht blerje</div></div>
      </div>

      <!-- Filter + Search -->
      <div class="table-header" style="margin-bottom:16px">
        <div style="display:flex;gap:6px;flex-wrap:wrap" id="inv-filter-tabs">
          <button class="tab active" onclick="filterInv('all',this)">Të Gjitha</button>
          <button class="tab" onclick="filterInv('normal',this)" style="background:rgba(34,197,94,0.15);color:var(--green)">✅ Normal</button>
          <button class="tab" onclick="filterInv('ulet',this)" style="background:rgba(234,179,8,0.15);color:var(--yellow)">⚠️ I Ulët</button>
          <button class="tab" onclick="filterInv('kritik',this)" style="background:rgba(239,68,68,0.15);color:var(--red)">🚨 Kritik</button>
        </div>
        <div class="search-box">🔍 <input type="text" placeholder="Kërko artikull..." oninput="searchInv(this.value)"></div>
      </div>

      <!-- Kartat e inventarit -->
      <div id="inv-cards-grid" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:14px"></div>
    </div>

    <!-- ═══ MATERIALE ═══ -->
    <div class="panel" id="panel-materiale">
      <div class="tabs">
        <button class="tab active" onclick="filterMat('all',this)">Të Gjitha</button>
        <button class="tab" onclick="filterMat('Betoni & Strukturë',this)">Betoni</button>
        <button class="tab" onclick="filterMat('Çelik & Metal',this)">Çelik</button>
        <button class="tab" onclick="filterMat('Elektrik',this)">Elektrik</button>
        <button class="tab" onclick="filterMat('Hidraulikë',this)">Hidraulikë</button>
        <button class="tab" onclick="filterMat('Tjetër',this)">Tjetër</button>
      </div>
      <div class="table-header">
        <span class="table-title">📦 Lista e Materialeve</span>
        <div class="search-box">🔍 <input type="text" placeholder="Kërko material..." oninput="searchTable('mat-tbody',this.value)"></div>
      </div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>#</th><th>Emri Materialit</th><th>Kategori</th><th>Njësia</th><th>Sasia</th><th>Min</th><th>Çmimi Blerje</th><th>Çmimi Shitje</th><th>Furnitori</th><th>Statusi</th><th>Veprime</th></tr></thead>
          <tbody id="mat-tbody"></tbody>
        </table>
      </div>
    </div>

    <!-- ═══ PAJISJE ═══ -->
    <div class="panel" id="panel-pajisje">
      <div class="table-header">
        <span class="table-title">⚙️ Pajisje & Mjete</span>
        <div class="search-box">🔍 <input type="text" placeholder="Kërko pajisje..." oninput="searchTable('paj-tbody',this.value)"></div>
      </div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>#</th><th>Emri</th><th>Kategori</th><th>Seria/Kodi</th><th>Gjendja</th><th>Vlera Blerjes</th><th>Mirëmbajtja Radhës</th><th>Lokacioni</th><th>Statusi</th><th>Veprime</th></tr></thead>
          <tbody id="paj-tbody"></tbody>
        </table>
      </div>
    </div>

    <!-- ═══ SHITJE ═══ -->
    <div class="panel" id="panel-shitje">
      <div class="stats-row" style="grid-template-columns:repeat(3,1fr)">
        <div class="stat-card green"><div class="stat-icon">📈</div><div class="stat-label">Shitje Totale</div><div class="stat-value" id="sh-total">0 L</div><div class="stat-sub">Gjithsej</div></div>
        <div class="stat-card blue"><div class="stat-icon">🔄</div><div class="stat-label">Transaksione</div><div class="stat-value" id="sh-count">0</div><div class="stat-sub">Regjistrime</div></div>
        <div class="stat-card orange"><div class="stat-icon">💹</div><div class="stat-label">Fitimi Mesatar</div><div class="stat-value" id="sh-profit">0%</div><div class="stat-sub">Marzhi</div></div>
      </div>
      <div class="table-header">
        <span class="table-title">💰 Regjistri i Shitjeve & Stokut</span>
        <div class="search-box">🔍 <input type="text" placeholder="Kërko..." oninput="searchTable('sh-tbody',this.value)"></div>
      </div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>#</th><th>Data</th><th>Artikull</th><th>Lloji</th><th>Sasia</th><th>Çmimi Unit</th><th>Vlera Totale</th><th>Klienti/Shënim</th><th>Veprime</th></tr></thead>
          <tbody id="sh-tbody"></tbody>
        </table>
      </div>
    </div>

    <!-- ═══ FURNITORET ═══ -->
    <div class="panel" id="panel-furnitoret">
      <div class="furnitor-grid" id="furnitor-grid"></div>
      <div class="section-label">📋 Lista e Furnitorëve</div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>#</th><th>Emri</th><th>NID</th><th>Kontakti</th><th>Adresa</th><th>Materialet</th><th>Afati Pageses</th><th>Statusi</th><th>Veprime</th></tr></thead>
          <tbody id="fur-tbody"></tbody>
        </table>
      </div>
    </div>

    <!-- ═══ BILANCI & TATIMI ═══ -->
    <div class="panel" id="panel-bilanci">

      <!-- YEAR/MONTH FILTER -->
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:20px;flex-wrap:wrap">
        <div class="tabs" style="margin-bottom:0">
          <button class="tab active" onclick="setBilPeriod('vit',this)">Vjetor</button>
          <button class="tab" onclick="setBilPeriod('muaj',this)">Mujor</button>
        </div>
        <select id="bil-year" onchange="renderBilanci()" style="background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:7px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.8rem;outline:none"></select>
        <select id="bil-month" onchange="renderBilanci()" style="background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:7px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.8rem;outline:none;display:none">
          <option value="01">Janar</option><option value="02">Shkurt</option><option value="03">Mars</option>
          <option value="04">Prill</option><option value="05">Maj</option><option value="06">Qershor</option>
          <option value="07">Korrik</option><option value="08">Gusht</option><option value="09">Shtator</option>
          <option value="10">Tetor</option><option value="11">Nëntor</option><option value="12">Dhjetor</option>
        </select>
        <button class="btn btn-ghost" onclick="exportBilanciPDF()" style="margin-left:auto">📄 Eksporto Raport</button>
        <button class="btn btn-primary" onclick="openModal('shpenzim')">＋ Shto Shpenzim</button>
      </div>

      <!-- STATS ROW -->
      <div class="stats-row" style="grid-template-columns:repeat(4,1fr)">
        <div class="stat-card green"><div class="stat-icon">📈</div><div class="stat-label">Të Ardhura Bruto</div><div class="stat-value" id="bil-ardhura">0 L</div><div class="stat-sub">Nga shitjet</div></div>
        <div class="stat-card red"><div class="stat-icon">📉</div><div class="stat-label">Shpenzime Totale</div><div class="stat-value" id="bil-shpenzime">0 L</div><div class="stat-sub">Blerje + Operative</div></div>
        <div class="stat-card orange"><div class="stat-icon">💹</div><div class="stat-label">Fitimi Para Tatimit</div><div class="stat-value" id="bil-fitim-para">0 L</div><div class="stat-sub">Bruto - Shpenzime</div></div>
        <div class="stat-card blue"><div class="stat-icon">🏦</div><div class="stat-label">Fitimi Neto</div><div class="stat-value" id="bil-fitim-neto">0 L</div><div class="stat-sub">Pas tatimit</div></div>
      </div>

      <!-- TATIMI ROW -->
      <div class="stats-row" style="grid-template-columns:repeat(3,1fr);margin-top:0">
        <div class="stat-card yellow"><div class="stat-icon">🧾</div><div class="stat-label">TVSH e Mbledhur (20%)</div><div class="stat-value" id="bil-tvsh-mbj">0 L</div><div class="stat-sub">Nga shitjet me TVSH</div></div>
        <div class="stat-card yellow"><div class="stat-icon">🔄</div><div class="stat-label">TVSH e Zbritshme</div><div class="stat-value" id="bil-tvsh-zbr">0 L</div><div class="stat-sub">Nga blerjet me TVSH</div></div>
        <div class="stat-card red"><div class="stat-icon">💸</div><div class="stat-label">TVSH për Pagesë</div><div class="stat-value" id="bil-tvsh-net">0 L</div><div class="stat-sub">Detyrim ndaj tatimit</div></div>
      </div>

      <!-- TATIM FITIMI -->
      <div class="section-label">🏛️ Detyrimet Tatimore</div>
      <div id="bil-tatim-box" class="bil-tatim-box"></div>

      <!-- GRAFIKU MUJOR -->
      <div class="section-label">📊 Grafiku i Të Ardhurave & Shpenzimeve</div>
      <div class="table-wrap" style="padding:20px 24px">
        <canvas id="bil-chart" height="80"></canvas>
      </div>

      <!-- SHPENZIME OPERATIVE -->
      <div class="section-label" style="margin-top:24px">📋 Shpenzime Operative</div>
      <div class="table-header">
        <span class="table-title">Lista e Shpenzimeve</span>
        <div class="search-box">🔍 <input type="text" placeholder="Kërko..." oninput="searchTable('shp-tbody',this.value)"></div>
      </div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>#</th><th>Data</th><th>Përshkrimi</th><th>Kategoria</th><th>Vlera</th><th>TVSH</th><th>Total me TVSH</th><th>Veprime</th></tr></thead>
          <tbody id="shp-tbody"></tbody>
        </table>
      </div>

    </div>

    <!-- ═══ PAGA & HR ═══ -->
    <div class="panel" id="panel-hr">

      <!-- FILTER ROW -->
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:20px;flex-wrap:wrap">
        <div class="tabs" style="margin-bottom:0">
          <button class="tab active" onclick="setHrView('punonjes',this)">Punonjësit</button>
          <button class="tab" onclick="setHrView('paga',this)">Rregjistri Pagave</button>
          <button class="tab" onclick="setHrView('shpenzime',this)">Shpenzime të Tjera</button>
        </div>
        <select id="hr-year" onchange="renderHR()" style="background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:7px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.8rem;outline:none"></select>
        <select id="hr-month" onchange="renderHR()" style="background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:7px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.8rem;outline:none">
          <option value="all">Të gjitha muajt</option>
          <option value="01">Janar</option><option value="02">Shkurt</option><option value="03">Mars</option>
          <option value="04">Prill</option><option value="05">Maj</option><option value="06">Qershor</option>
          <option value="07">Korrik</option><option value="08">Gusht</option><option value="09">Shtator</option>
          <option value="10">Tetor</option><option value="11">Nëntor</option><option value="12">Dhjetor</option>
        </select>
        <button class="btn btn-primary" id="hr-btn-add" onclick="openHRModal()" style="margin-left:auto">＋ Shto</button>
      </div>

      <!-- STATS -->
      <div class="stats-row" style="grid-template-columns:repeat(4,1fr)" id="hr-stats-row">
        <div class="stat-card blue"><div class="stat-icon">👷</div><div class="stat-label">Punonjës Aktiv</div><div class="stat-value" id="hr-total-pun">0</div><div class="stat-sub">Stafi aktual</div></div>
        <div class="stat-card red"><div class="stat-icon">💵</div><div class="stat-label">Paga Totale (Muaji)</div><div class="stat-value" id="hr-total-paga">0 L</div><div class="stat-sub">Bruto + Kontribute</div></div>
        <div class="stat-card orange"><div class="stat-icon">🏛️</div><div class="stat-label">Kontribute Shoq.</div><div class="stat-value" id="hr-kontribute">0 L</div><div class="stat-sub">Punëdhënës (16.7%)</div></div>
        <div class="stat-card yellow"><div class="stat-icon">📋</div><div class="stat-label">Shp. të Tjera</div><div class="stat-value" id="hr-shp-tjera">0 L</div><div class="stat-sub">Periudha e zgjedhur</div></div>
      </div>

      <!-- PUNONJESIT VIEW -->
      <div id="hr-view-punonjes">
        <div class="section-label">👷 Lista e Punonjësve</div>
        <div class="table-wrap">
          <table>
            <thead><tr><th>#</th><th>Emri & Mbiemri</th><th>Pozicioni</th><th>Data Fillimit</th><th>Paga Bruto</th><th>Kontribute (16.7%)</th><th>Paga Neto</th><th>Statusi</th><th>Veprime</th></tr></thead>
            <tbody id="hr-pun-tbody"></tbody>
          </table>
        </div>
      </div>

      <!-- PAGA VIEW -->
      <div id="hr-view-paga" style="display:none">
        <div class="section-label">💵 Regjistri i Pagave</div>
        <div class="table-wrap">
          <table>
            <thead><tr><th>#</th><th>Muaji</th><th>Punonjësi</th><th>Paga Bruto</th><th>Tatim Mbi të Ardhura</th><th>Kontribute</th><th>Paga Neto</th><th>Statusi</th><th>Veprime</th></tr></thead>
            <tbody id="hr-paga-tbody"></tbody>
          </table>
        </div>
      </div>

      <!-- SHPENZIME TË TJERA VIEW -->
      <div id="hr-view-shpenzime" style="display:none">
        <div class="section-label">📋 Shpenzime të Tjera Operative</div>
        <div class="table-wrap">
          <table>
            <thead><tr><th>#</th><th>Data</th><th>Përshkrimi</th><th>Kategoria</th><th>Vlera</th><th>TVSH (20%)</th><th>Total</th><th>Veprime</th></tr></thead>
            <tbody id="hr-shp-tbody"></tbody>
          </table>
        </div>
      </div>

    </div>

    <!-- ═══ PANEL: KONTRATAT & PROJEKTET ═══ -->
    <div class="panel" id="panel-projektet">
      <div class="stats-row">
        <div class="stat-card orange"><div class="stat-icon">📋</div><div class="stat-label">Projekte Aktive</div><div class="stat-value" id="prj-aktive">0</div><div class="stat-sub">Në zhvillim</div></div>
        <div class="stat-card green"><div class="stat-icon">✅</div><div class="stat-label">Të Përfunduara</div><div class="stat-value" id="prj-perfunduar">0</div><div class="stat-sub">Këtë vit</div></div>
        <div class="stat-card red"><div class="stat-icon">⚠️</div><div class="stat-label">Të Vonuara</div><div class="stat-value" id="prj-vonuara">0</div><div class="stat-sub">Mbi afatin</div></div>
        <div class="stat-card blue"><div class="stat-icon">💰</div><div class="stat-label">Vlera Totale</div><div class="stat-value" id="prj-vlera">0 L</div><div class="stat-sub">Të gjitha projektet</div></div>
      </div>
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:20px;flex-wrap:wrap">
        <div class="tabs" style="margin-bottom:0" id="proj-filter-tabs">
          <button class="tab active" onclick="filterProj('all',this)">Të Gjitha</button>
          <button class="tab" onclick="filterProj('Aktiv',this)">Aktive</button>
          <button class="tab" onclick="filterProj('Vonuar',this)">Vonuara</button>
          <button class="tab" onclick="filterProj('Përfunduar',this)">Përfunduara</button>
        </div>
        <div class="search-box" style="margin-left:auto">🔍 <input type="text" placeholder="Kërko projekt..." oninput="searchProj(this.value)"></div>
      </div>
      <div class="proj-grid" id="proj-grid"></div>
      <div class="section-label">📊 Lista Tabelare</div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>#</th><th>Projekti</th><th>Klienti</th><th>Fillimi</th><th>Afati</th><th>Buxheti</th><th>Realizuar %</th><th>Progresi</th><th>Statusi</th><th>Veprime</th></tr></thead>
          <tbody id="proj-tbody"></tbody>
        </table>
      </div>
    </div>

    <!-- ═══ PANEL: FATURA & OFERTA ═══ -->
    <div class="panel" id="panel-faturat">
      <div class="stats-row">
        <div class="stat-card green"><div class="stat-icon">✅</div><div class="stat-label">Fatura të Paguara</div><div class="stat-value" id="fat-paguar">0</div><div class="stat-sub">Të arketuara</div></div>
        <div class="stat-card yellow"><div class="stat-icon">⏳</div><div class="stat-label">Në Pritje</div><div class="stat-value" id="fat-pritje">0</div><div class="stat-sub">Pa paguar ende</div></div>
        <div class="stat-card red"><div class="stat-icon">❌</div><div class="stat-label">Të Vonuara</div><div class="stat-value" id="fat-vonuar">0</div><div class="stat-sub">Mbi datën e skadimit</div></div>
        <div class="stat-card orange"><div class="stat-icon">💵</div><div class="stat-label">Totali i Faturave</div><div class="stat-value" id="fat-total-stat">0 L</div><div class="stat-sub">Të gjitha llojet</div></div>
      </div>
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:20px;flex-wrap:wrap">
        <div class="tabs" style="margin-bottom:0">
          <button class="tab active" onclick="setFatView('faturat',this)">🧾 Fatura</button>
          <button class="tab" onclick="setFatView('ofertat',this)">📄 Oferta</button>
        </div>
        <div class="search-box" style="margin-left:auto">🔍 <input type="text" placeholder="Kërko..." oninput="searchFat(this.value)"></div>
      </div>
      <!-- FATURA -->
      <div id="fat-view-faturat">
        <div class="fat-grid" id="fat-cards-grid"></div>
        <div class="section-label">📋 Të Gjitha Faturat</div>
        <div class="table-wrap"><table>
          <thead><tr><th>#</th><th>Nr. Faturës</th><th>Data</th><th>Klienti</th><th>Projekti</th><th>Subtotal</th><th>TVSH 20%</th><th>Total</th><th>Statusi</th><th>Skadon</th><th>Veprime</th></tr></thead>
          <tbody id="fat-tbody"></tbody>
        </table></div>
      </div>
      <!-- OFERTA -->
      <div id="fat-view-ofertat" style="display:none">
        <div class="section-label">📄 Ofertat e Dërguara</div>
        <div class="table-wrap"><table>
          <thead><tr><th>#</th><th>Nr.</th><th>Data</th><th>Klienti</th><th>Shërbimi/Projekti</th><th>Vlera</th><th>Vlefshmëria</th><th>Statusi</th><th>Veprime</th></tr></thead>
          <tbody id="ofe-tbody"></tbody>
        </table></div>
      </div>
    </div>

    <!-- ═══ PANEL: RAPORTI MUJOR ═══ -->
    <div class="panel" id="panel-raporti">

      <!-- SELECTOR BAR -->
      <div class="rap-selector">
        <div class="rap-month-nav">
          <button class="rap-nav-btn" onclick="rapNavMonth(-1)">‹</button>
          <div class="rap-period-label" id="rap-period-lbl">— — —</div>
          <button class="rap-nav-btn" onclick="rapNavMonth(1)">›</button>
        </div>
        <select id="rap-year-sel" onchange="renderRaporti()" style="font-family:'Bebas Neue',sans-serif;font-size:1rem;letter-spacing:0.06em"></select>
        <select id="rap-month-sel" onchange="renderRaporti()">
          <option value="01">Janar</option><option value="02">Shkurt</option><option value="03">Mars</option>
          <option value="04">Prill</option><option value="05">Maj</option><option value="06">Qershor</option>
          <option value="07">Korrik</option><option value="08">Gusht</option><option value="09">Shtator</option>
          <option value="10">Tetor</option><option value="11">Nëntor</option><option value="12">Dhjetor</option>
        </select>
        <button class="rap-lock-btn open" id="rap-lock-btn" onclick="toggleRapLock()">🔓 Modifikim i Hapur</button>
        <button class="btn btn-ghost" onclick="exportRapCSV()" style="font-size:0.75rem">📥 Eksporto CSV</button>
        <button class="btn btn-primary" onclick="printRaport()" style="font-size:0.75rem">🖨️ Printo Raportin</button>
      </div>

      <!-- HISTORY STRIP -->
      <div class="section-label">📅 Historia Mujore</div>
      <div class="rap-history-strip" id="rap-history-strip"></div>

      <!-- KPI ROW -->
      <div class="rap-kpi-row" id="rap-kpi-row">
        <div class="rap-kpi pos"><div class="rap-kpi-label">Të Ardhura</div><div class="rap-kpi-val" id="rkpi-ardhura">— L</div><div class="rap-kpi-delta" id="rkpi-ardhura-d"></div></div>
        <div class="rap-kpi neg"><div class="rap-kpi-label">Shpenzime</div><div class="rap-kpi-val" id="rkpi-shp">— L</div><div class="rap-kpi-delta" id="rkpi-shp-d"></div></div>
        <div class="rap-kpi neu"><div class="rap-kpi-label">Fitimi Neto</div><div class="rap-kpi-val" id="rkpi-fitim">— L</div><div class="rap-kpi-delta" id="rkpi-fitim-d"></div></div>
        <div class="rap-kpi info"><div class="rap-kpi-label">Paga Totale</div><div class="rap-kpi-val" id="rkpi-paga">— L</div><div class="rap-kpi-delta" id="rkpi-paga-d"></div></div>
      </div>

      <!-- MAIN FORM GRID -->
      <div class="rap-grid">

        <!-- LEFT: BLERJE & SHITJE -->
        <div style="display:flex;flex-direction:column;gap:16px">

          <!-- SHITJET -->
          <div class="rap-section">
            <div class="rap-section-title">💰 Të Ardhurat e Muajit</div>
            <div class="rap-3col">
              <div class="rap-field"><label>Shitje Materiale (L)</label><input type="number" id="rap-shitje-mat" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Shërbime/Kontr. (L)</label><input type="number" id="rap-shitje-she" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Të Ardhura Tjera (L)</label><input type="number" id="rap-ardhura-tjera" oninput="rapCalc()" placeholder="0"></div>
            </div>
            <div class="rap-result-box">
              <div class="rap-result-row"><span>Subtotal shitje:</span><span id="rap-r-shitje" class="mono" style="color:var(--green)">0 L</span></div>
              <div class="rap-result-row"><span>Shitje me TVSH (20%):</span><span id="rap-r-shitje-tvsh" class="mono" style="color:var(--yellow)">0 L</span></div>
              <div class="rap-result-total"><span>TOTAL TË ARDHURA:</span><span id="rap-r-ardhura-tot" style="color:var(--green);font-family:'JetBrains Mono',monospace">0 L</span></div>
            </div>
          </div>

          <!-- BLERJET -->
          <div class="rap-section">
            <div class="rap-section-title">📦 Blerjet e Muajit</div>
            <div class="rap-3col">
              <div class="rap-field"><label>Materiale (L)</label><input type="number" id="rap-blerje-mat" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Pajisje/Mjete (L)</label><input type="number" id="rap-blerje-paj" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Blerje Tjera (L)</label><input type="number" id="rap-blerje-tjera" oninput="rapCalc()" placeholder="0"></div>
            </div>
            <div class="rap-result-box">
              <div class="rap-result-total"><span>TOTAL BLERJE:</span><span id="rap-r-blerje-tot" style="color:var(--orange);font-family:'JetBrains Mono',monospace">0 L</span></div>
            </div>
          </div>

          <!-- ARKA -->
          <div class="rap-section">
            <div class="rap-section-title">🏦 Gjendja e Arkës</div>
            <div class="rap-2col">
              <div class="rap-field"><label>Arka Fillim Muaji (L)</label><input type="number" id="rap-arka-fillim" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Arka Fund Muaji (L)</label><input type="number" id="rap-arka-fund" oninput="rapCalc()" placeholder="0" style="background:var(--s3)"></div>
            </div>
            <div class="rap-2col">
              <div class="rap-field"><label>Llogari Bankare (L)</label><input type="number" id="rap-banka" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Detyrime/Borxhe (L)</label><input type="number" id="rap-detyrime" oninput="rapCalc()" placeholder="0"></div>
            </div>
            <div class="rap-result-box">
              <div class="rap-result-row"><span>Lëvizja e Arkës:</span><span id="rap-r-levizja" class="mono">0 L</span></div>
              <div class="rap-result-total"><span>GJENDJA TOTALE:</span><span id="rap-r-gjendja" style="font-family:'JetBrains Mono',monospace">0 L</span></div>
            </div>
          </div>

        </div><!-- /left -->

        <!-- RIGHT: DETYRIME + PUNONJËS -->
        <div style="display:flex;flex-direction:column;gap:16px">

          <!-- DETYRIMET -->
          <div class="rap-section">
            <div class="rap-section-title">💳 Detyrimet & Shpenzimet</div>
            <div class="rap-2col">
              <div class="rap-field"><label>Qira Zyrë/Depo (L)</label><input type="number" id="rap-qira" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Karburant/Transport (L)</label><input type="number" id="rap-karb" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Fatura Energji/Ujë (L)</label><input type="number" id="rap-energji" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Mirëmbajtje Makina (L)</label><input type="number" id="rap-mirembajt" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Telefon/Internet (L)</label><input type="number" id="rap-telekom" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Shpenzime Tjera (L)</label><input type="number" id="rap-shp-tjera" oninput="rapCalc()" placeholder="0"></div>
            </div>
            <div class="rap-result-box">
              <div class="rap-result-row"><span>Shpenzime operative:</span><span id="rap-r-shp-op" class="mono" style="color:var(--red)">0 L</span></div>
              <div class="rap-result-row"><span>TVSH e Pagueshme:</span><span id="rap-r-tvsh" class="mono" style="color:var(--yellow)">0 L</span></div>
              <div class="rap-result-total"><span>TOTAL SHPENZIME:</span><span id="rap-r-shp-tot" style="color:var(--red);font-family:'JetBrains Mono',monospace">0 L</span></div>
            </div>
          </div>

          <!-- STOKU -->
          <div class="rap-section">
            <div class="rap-section-title">📊 Gjendja e Stokut</div>
            <div class="rap-2col">
              <div class="rap-field"><label>Vlera Stokut Fillim (L)</label><input type="number" id="rap-stok-fillim" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Vlera Stokut Fund (L)</label><input type="number" id="rap-stok-fund" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Nr. Artikujve Kritik</label><input type="number" id="rap-stok-kritik" oninput="rapCalc()" placeholder="0"></div>
              <div class="rap-field"><label>Nr. Artikujve Total</label><input type="number" id="rap-stok-total-art" oninput="rapCalc()" placeholder="0"></div>
            </div>
            <div class="rap-result-box">
              <div class="rap-result-row"><span>Ndryshim Stoku:</span><span id="rap-r-stok-delta" class="mono">0 L</span></div>
            </div>
          </div>

          <!-- SHËNIME -->
          <div class="rap-section">
            <div class="rap-section-title">📝 Shënime & Vlerësim</div>
            <div class="rap-field"><label>Ngjarjet Kryesore të Muajit</label><textarea id="rap-shenime" rows="3" placeholder="p.sh. U nënshkrua kontrata me Invest Group, u bë blerja e vinçit..."></textarea></div>
            <div class="rap-field"><label>Objektivat për Muajin Tjetër</label><textarea id="rap-objektivat" rows="2" placeholder="p.sh. Të rriten shitjet me 15%, të blihen 200 thes çimento..."></textarea></div>
            <div class="rap-field"><label>Vlerësimi i Muajit</label>
              <select id="rap-vleresim">
                <option value="shkelqyer">⭐⭐⭐ Shkëlqyer — Objektivat u tejkaluan</option>
                <option value="mire" selected>⭐⭐ Mirë — Rezultate pozitive</option>
                <option value="mesatar">⭐ Mesatar — Duhen përmirësime</option>
                <option value="dobet">⚠️ Dobët — Nën pritje</option>
              </select>
            </div>
          </div>

        </div><!-- /right -->
      </div><!-- /rap-grid -->

      <!-- PUNONJESIT SECTION -->
      <div class="rap-section" style="margin-bottom:16px">
        <div class="rap-section-title">👷 Lista e Punonjësve & Pagat Muajore</div>
        <div style="display:grid;grid-template-columns:2fr 1fr 1fr 1fr 1fr;gap:8px;padding:6px 12px;font-size:0.65rem;font-weight:700;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:4px">
          <span>EMRI & POZICIONI</span><span>PAGA BRUTO</span><span>KONTRIBUTE</span><span>PAGA NETO</span><span>STATUSI</span>
        </div>
        <div id="rap-punonjesit-list"></div>
        <button class="rap-add-row-btn" id="rap-add-pun-btn" onclick="rapAddPunator()">＋ Shto Punonjës</button>
        <div class="rap-result-box" style="margin-top:12px">
          <div class="rap-result-row"><span>Paga Bruto Totale:</span><span id="rap-r-paga-bruto" class="mono" style="color:var(--text)">0 L</span></div>
          <div class="rap-result-row"><span>Kontribute Punëdhënës (16.7%):</span><span id="rap-r-kontribute" class="mono" style="color:var(--yellow)">0 L</span></div>
          <div class="rap-result-row"><span>Tatim mbi të Ardhura:</span><span id="rap-r-tatim-pun" class="mono" style="color:var(--red)">0 L</span></div>
          <div class="rap-result-total"><span>KOSTO TOTALE PUNONJËSISH:</span><span id="rap-r-paga-tot" style="color:var(--orange);font-family:'JetBrains Mono',monospace">0 L</span></div>
        </div>
      </div>

      <!-- BOTTOM SUMMARY -->
      <div class="rap-section" style="border-color:rgba(249,115,22,0.3);margin-bottom:16px">
        <div class="rap-section-title" style="color:var(--orange)">📊 Përmbledhja Financiare e Muajit</div>
        <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:16px">
          <div>
            <div style="font-size:0.68rem;color:var(--muted);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:8px">TË ARDHURA</div>
            <div class="rap-result-row"><span>Shitje + Shërbime:</span><span id="rs-ardhura" class="mono" style="color:var(--green)">0 L</span></div>
          </div>
          <div>
            <div style="font-size:0.68rem;color:var(--muted);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:8px">SHPENZIME</div>
            <div class="rap-result-row"><span>Operative:</span><span id="rs-shp-op" class="mono" style="color:var(--red)">0 L</span></div>
            <div class="rap-result-row"><span>Pagat:</span><span id="rs-pagat" class="mono" style="color:var(--red)">0 L</span></div>
            <div class="rap-result-row"><span>Blerje:</span><span id="rs-blerje" class="mono" style="color:var(--orange)">0 L</span></div>
          </div>
          <div style="background:var(--s2);border-radius:10px;padding:14px;display:flex;flex-direction:column;justify-content:center;align-items:center;gap:6px">
            <div style="font-size:0.68rem;color:var(--muted);text-transform:uppercase;letter-spacing:0.08em">FITIMI NETO</div>
            <div id="rs-fitim-neto" style="font-family:'JetBrains Mono',monospace;font-size:1.8rem;font-weight:700">0 L</div>
            <div id="rs-fitim-pct" style="font-size:0.78rem;color:var(--muted)">0% marzh fitimi</div>
          </div>
        </div>
      </div>

      <!-- CHARTS -->
      <div class="rap-chart-wrap">
        <div class="section-label" style="margin-bottom:16px">📈 Krahasimi Muaj-me-Muaj (12 muajt e fundit)</div>
        <canvas id="rap-chart-main" height="70"></canvas>
      </div>
      <div class="rap-grid" style="margin-bottom:16px">
        <div class="rap-chart-wrap" style="margin-bottom:0">
          <div class="section-label" style="margin-bottom:16px">💰 Shpërndarja e Shpenzimeve</div>
          <canvas id="rap-chart-shp" height="120"></canvas>
        </div>
        <div class="rap-chart-wrap" style="margin-bottom:0">
          <div class="section-label" style="margin-bottom:16px">📊 Trendi i Fitimit</div>
          <canvas id="rap-chart-trend" height="120"></canvas>
        </div>
      </div>

      <!-- SAVE BAR -->
      <div class="rap-save-bar">
        <span class="rap-autosave-hint" id="rap-save-hint">💡 Ndryshimet ruhen automatikisht</span>
        <div style="display:flex;gap:10px">
          <button class="btn btn-ghost" onclick="rapAutoFill()">🔄 Plotëso nga të Dhënat Aktuale</button>
          <button class="btn btn-primary" onclick="saveRaport()">💾 Ruaj Raportin</button>
        </div>
      </div>

    </div><!-- /panel-raporti -->


    <!-- ═══ PANEL: BIBLIOTEKA ═══ -->
    <div class="panel" id="panel-biblioteka">
      <div class="topbar">
        <div>
          <div style="font-size:1.1rem;font-weight:800;color:var(--text)">📚 Biblioteka e Formateve</div>
          <div style="font-size:0.72rem;color:var(--muted);margin-top:2px">Ngarko template · Plotëso të dhënat · Gjenero dokument</div>
        </div>
        <div style="display:flex;gap:8px">
          <button class="btn btn-ghost" onclick="bibShowTab('templates')" id="bib-tab-templates" style="font-size:0.75rem">📋 Template-t</button>
          <button class="btn btn-ghost" onclick="bibShowTab('builtins')" id="bib-tab-builtins" style="font-size:0.75rem">⭐ Të Gatshme</button>
        </div>
      </div>

      <!-- TAB: TEMPLATES (upload) -->
      <div id="bib-pane-templates" style="padding:24px">
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-bottom:24px">

          <!-- Upload zone -->
          <div>
            <div style="font-size:0.7rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:10px">📤 Ngarko Template të Ri</div>
            <div class="bib-upload-zone" id="bib-drop-zone" ondragover="event.preventDefault();this.classList.add('drag')" ondragleave="this.classList.remove('drag')" ondrop="bibHandleDrop(event)">
              <input type="file" accept=".xlsx,.xls,.pdf,.docx,.csv" onchange="bibHandleFile(this.files[0])">
              <div style="font-size:2rem;margin-bottom:10px">📎</div>
              <div style="font-weight:700;margin-bottom:4px">Tërhiq skedarin këtu</div>
              <div style="font-size:0.75rem;color:var(--muted)">ose kliko për të zgjedhur</div>
              <div style="font-size:0.65rem;color:var(--muted);margin-top:8px">Excel (.xlsx), PDF, Word (.docx), CSV</div>
            </div>
          </div>

          <!-- Template info after upload -->
          <div id="bib-template-info" style="display:none">
            <div style="font-size:0.7rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:10px">📄 Template i Ngarkuar</div>
            <div class="bib-section">
              <div id="bib-tpl-name" style="font-weight:700;font-size:1rem;margin-bottom:4px"></div>
              <div id="bib-tpl-meta" style="font-size:0.72rem;color:var(--muted)"></div>
              <div id="bib-tpl-fields" style="margin-top:12px"></div>
            </div>
            <button class="btn btn-primary" onclick="bibProceedToFill()" style="width:100%;margin-top:8px">▶ Vazhdo me Plotësimin</button>
          </div>

        </div>

        <!-- Fill fields step -->
        <div id="bib-fill-step" style="display:none">
          <div style="font-size:0.7rem;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:12px">✏️ Plotëso Fushat</div>
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:20px">
            <div>
              <div class="bib-section">
                <div class="bib-section-title">🤖 Auto-fill nga BuildTrack <span style="background:rgba(34,197,94,0.15);color:var(--green);border-radius:6px;padding:2px 8px">Aktiv</span></div>
                <div id="bib-auto-fields"></div>
              </div>
            </div>
            <div>
              <div class="bib-section">
                <div class="bib-section-title">✍️ Fushat Manuale</div>
                <div id="bib-manual-fields"></div>
              </div>
            </div>
          </div>
          <div style="display:flex;gap:10px;margin-top:16px">
            <button class="btn btn-ghost" onclick="bibBackToUpload()">← Prapa</button>
            <button class="btn btn-primary" onclick="bibGenerate()" style="flex:1">⚡ Gjenero Dokumentin</button>
          </div>
        </div>
      </div>

      <!-- TAB: BUILTINS -->
      <div id="bib-pane-builtins" style="display:none;padding:24px">
        <div style="font-size:0.75rem;color:var(--muted);margin-bottom:16px">Formate të gatshme profesionale — plotëso vetëm të dhënat specifike</div>
        <div class="bib-grid" id="bib-builtins-grid"></div>

        <!-- Builtin fill form -->
        <div id="bib-builtin-fill" style="display:none;margin-top:20px">
          <div style="display:flex;align-items:center;gap:10px;margin-bottom:16px">
            <button class="btn btn-ghost" onclick="bibBuiltinBack()" style="font-size:0.75rem">← Prapa</button>
            <div style="font-weight:700" id="bib-builtin-title"></div>
          </div>
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:20px">
            <div>
              <div class="bib-section">
                <div class="bib-section-title">🤖 Nga BuildTrack (auto)</div>
                <div id="bib-builtin-auto"></div>
              </div>
            </div>
            <div>
              <div class="bib-section">
                <div class="bib-section-title">✍️ Plotëso Manualisht</div>
                <div id="bib-builtin-manual"></div>
              </div>
            </div>
          </div>
          <button class="btn btn-primary" onclick="bibBuiltinGenerate()" style="width:100%;margin-top:16px">⚡ Gjenero Tani</button>
        </div>
      </div>

    </div><!-- /panel-biblioteka -->
  </div><!-- /content -->
</div><!-- /main -->

<!-- ═══ MODAL ═══ -->
<div class="modal-overlay" id="modal-overlay" onclick="if(event.target===this)closeModal()">
  <div class="modal" id="modal-box">
    <div class="modal-title" id="modal-title">Shto Material</div>
    <div id="modal-body"></div>
    <div class="modal-actions" id="modal-actions">
      <button class="btn btn-ghost" onclick="closeModal()">Anulo</button>
      <button class="btn btn-primary" onclick="saveItem()">💾 Ruaj</button>
    </div>
  </div>
</div>

<!-- ═══ SUBJECT MODAL ═══ -->
<div class="modal-overlay" id="subj-modal-overlay" onclick="if(event.target===this)closeSubjectModal()">
  <div class="modal" style="width:520px;max-height:90vh;overflow-y:auto">
    <div class="modal-title" id="subj-modal-title">➕ Shto Subjekt</div>

    <div style="font-size:0.65rem;font-weight:700;color:var(--muted);letter-spacing:0.12em;text-transform:uppercase;margin-bottom:10px">🏢 Informacion Bazë</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px">
      <div class="field" style="grid-column:1/-1">
        <label>Emri Kompanisë / Subjektit *</label>
        <input id="subj-emri" placeholder="p.sh. AlbBuild SHPK...">
      </div>
      <div class="field">
        <label>NIPT / NID</label>
        <input id="subj-nipt" placeholder="L12345678A">
      </div>
      <div class="field">
        <label>Tel. Kontakti</label>
        <input id="subj-tel" placeholder="+355 69 123 4567">
      </div>
      <div class="field" style="grid-column:1/-1">
        <label>Adresa</label>
        <input id="subj-adresa" placeholder="Rruga, Qyteti, Shqipëri">
      </div>
      <div class="field">
        <label>Email</label>
        <input id="subj-email" placeholder="info@kompania.al" type="email">
      </div>
      <div class="field">
        <label>Website</label>
        <input id="subj-web" placeholder="www.kompania.al">
      </div>
    </div>

    <div style="font-size:0.65rem;font-weight:700;color:var(--muted);letter-spacing:0.12em;text-transform:uppercase;margin-bottom:10px">🎨 Pamja</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px">
      <div class="field">
        <label>Ngjyra e Brandimit</label>
        <div class="color-picker" id="color-picker"></div>
      </div>
      <div class="field">
        <label>Logo (URL ose Base64)</label>
        <input id="subj-logo" placeholder="https://... ose ngarko më poshtë">
        <div style="margin-top:6px;display:flex;gap:6px;align-items:center">
          <input type="file" id="subj-logo-file" accept="image/*" style="display:none" onchange="loadLogoFile(event)">
          <button onclick="document.getElementById('subj-logo-file').click()" style="background:var(--s2);border:1px solid var(--border);color:var(--muted);padding:5px 10px;border-radius:7px;cursor:pointer;font-size:0.7rem;font-family:'DM Sans',sans-serif">📎 Ngarko Logo</button>
          <div id="subj-logo-preview" style="width:36px;height:36px;border:1px solid var(--border);border-radius:6px;overflow:hidden;display:none"><img id="subj-logo-img" style="width:100%;height:100%;object-fit:contain"></div>
        </div>
      </div>
    </div>

    <div style="font-size:0.65rem;font-weight:700;color:var(--muted);letter-spacing:0.12em;text-transform:uppercase;margin-bottom:10px">📄 Tekst në Fatura</div>
    <div class="field" style="margin-bottom:14px">
      <label>Shënim Fundi Faturës (opsional)</label>
      <textarea id="subj-shenimFature" rows="2" style="background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:8px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.82rem;outline:none;resize:vertical;width:100%" placeholder="p.sh. Faleminderit për besimin! Pagesa brenda 30 ditësh."></textarea>
    </div>

    <div class="modal-actions">
      <button class="btn btn-ghost" onclick="closeSubjectModal()">Anulo</button>
      <button class="btn btn-primary" onclick="saveSubject()">💾 Ruaj</button>
    </div>
  </div>
</div>

<!-- ═══ GLOBAL SEARCH MODAL ═══ -->
<div class="modal-overlay" id="gsearch-overlay" onclick="if(event.target===this)closeGlobalSearch()" style="align-items:flex-start;padding-top:80px">
  <div style="background:var(--s1);border:1px solid var(--border);border-radius:16px;width:620px;max-width:96vw;overflow:hidden;animation:modalIn 0.2s ease">
    <div style="padding:14px 16px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:10px">
      <span style="font-size:1.1rem;opacity:0.5">🔍</span>
      <input id="gsearch-input" placeholder="Kërko materiale, fatura, punonjës, shitje..." autofocus
        style="flex:1;background:none;border:none;outline:none;font-size:0.95rem;color:var(--text);font-family:'DM Sans',sans-serif"
        oninput="runGlobalSearch(this.value)" onkeydown="gsearchKeydown(event)">
      <span style="font-size:0.68rem;color:var(--muted);background:var(--s2);padding:3px 8px;border-radius:5px">ESC</span>
    </div>
    <div id="gsearch-results" style="max-height:420px;overflow-y:auto;padding:8px">
      <div style="padding:24px;text-align:center;color:var(--muted);font-size:0.82rem">
        Shkruaj për të kërkuar në të gjitha modulet...
      </div>
    </div>
    <div style="padding:8px 16px;border-top:1px solid var(--border);display:flex;gap:16px;font-size:0.65rem;color:var(--muted)">
      <span>↑↓ navigim</span><span>↵ hap</span><span>ESC mbyll</span>
    </div>
  </div>
</div>
<div class="modal-overlay" id="excel-modal-overlay" onclick="if(event.target===this)closeExcelImport()">
  <div class="imp-modal">
    <div class="modal-title" style="margin-bottom:16px">📊 Importo nga Excel / CSV</div>

    <!-- STEP 1: DROP ZONE -->
    <div id="imp-step1">
      <div class="imp-drop" id="imp-drop-zone">
        <div class="imp-drop-icon">📂</div>
        <div class="imp-drop-text">
          <strong style="color:var(--text);font-size:0.9rem">Tërhiq & Lësho skedarin këtu</strong><br>
          ose kliko për të zgjedhur<br>
          <span style="font-size:0.72rem;opacity:0.7;margin-top:4px;display:block">Suporton: .xlsx, .xls, .csv</span>
        </div>
        <input type="file" id="excel-file-input" accept=".xlsx,.xls,.csv" onchange="handleExcelFile(event)">
      </div>
      <div style="background:rgba(249,115,22,0.06);border:1px solid rgba(249,115,22,0.2);border-radius:10px;padding:12px 14px;font-size:0.78rem;color:var(--muted);line-height:1.7">
        <strong style="color:var(--orange)">💡 Si funksionon:</strong> Ngarko Excel-in tuaj → sistemi lexon kolonat automatikisht → ju vendosni cila kolonë i përket cilit fushë → konfirmoni importin. Të dhënat shtohen mbi ato ekzistuese.
      </div>
    </div>

    <!-- STEP 2: SHEET SELECTION + MAPPING -->
    <div id="imp-step2" style="display:none">
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:14px">
        <div id="imp-file-info" style="flex:1;font-size:0.82rem;color:var(--text)"></div>
        <button onclick="resetExcelImport()" style="background:none;border:1px solid var(--border);color:var(--muted);padding:5px 10px;border-radius:7px;cursor:pointer;font-size:0.72rem;font-family:'DM Sans',sans-serif">✕ Ndrysho skedarin</button>
      </div>

      <!-- Sheet selector -->
      <div id="imp-sheets-wrap" style="display:none">
        <div class="imp-section-lbl">📋 Zgjidhni Sheet-in</div>
        <div class="imp-sheet-sel" id="imp-sheet-sel"></div>
      </div>

      <!-- Data type tabs -->
      <div class="imp-section-lbl">🎯 Çfarë po importoni?</div>
      <div class="imp-tabs" id="imp-type-tabs">
        <button class="imp-tab active" onclick="setImpType('materiale',this)">📦 Materiale</button>
        <button class="imp-tab" onclick="setImpType('shitje',this)">💰 Shitje/Blerje</button>
        <button class="imp-tab" onclick="setImpType('shpenzime',this)">💳 Shpenzime</button>
        <button class="imp-tab" onclick="setImpType('faturat',this)">🧾 Fatura</button>
      </div>

      <!-- Preview table -->
      <div class="imp-section-lbl">👁️ Preview (5 rreshtat e parë)</div>
      <div class="imp-table-wrap">
        <table class="imp-table">
          <thead id="imp-preview-head"></thead>
          <tbody id="imp-preview-body"></tbody>
        </table>
      </div>

      <!-- Column mapping -->
      <div class="imp-section-lbl">🔗 Lidhja e Kolonave</div>
      <div style="background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:14px">
        <div style="display:grid;grid-template-columns:1fr 24px 1fr;gap:8px;margin-bottom:8px">
          <div style="font-size:0.62rem;font-weight:700;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase">KOLONA NGA EXCEL</div>
          <div></div>
          <div style="font-size:0.62rem;font-weight:700;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase">FUSHA NË SISTEM</div>
        </div>
        <div id="imp-mapping-rows"></div>
      </div>

      <!-- Result preview -->
      <div id="imp-result-preview" style="display:none" class="imp-result-box"></div>

      <!-- Actions -->
      <div style="display:flex;gap:10px;margin-top:18px;justify-content:flex-end">
        <button class="btn btn-ghost" onclick="closeExcelImport()">Anulo</button>
        <button class="btn" onclick="previewImport()" style="background:var(--s2);border:1px solid var(--border);color:var(--text)">👁️ Preview Importit</button>
        <button class="btn btn-primary" id="imp-confirm-btn" onclick="confirmImport()" style="display:none">✅ Konfirmo Importin</button>
      </div>
    </div>
  </div>
</div>

<script>
// ═══════════════════════════════════════════════
// MULTI-SUBJECT SYSTEM
// ═══════════════════════════════════════════════
const COLORS = ['#f97316','#3b82f6','#22c55e','#a855f7','#ef4444','#06b6d4','#eab308','#ec4899'];
let selectedColor = COLORS[0];

const defaultData = () => ({
  materiale: [
    {id:1,emri:"Çimento Portland 42.5N",kategori:"Betoni & Strukturë",njesia:"Thes (50kg)",sasia:320,min:50,cmBlerje:850,cmShitje:1050,furnitori:"TITAN Cement Albania",status:"Stok Normal"},
    {id:2,emri:"Zhavorr 0-4mm",kategori:"Betoni & Strukturë",njesia:"Ton",sasia:45,min:20,cmBlerje:3200,cmShitje:4000,furnitori:"Guri Alb SHPK",status:"Stok Normal"},
    {id:3,emri:"Hekur Armature Ø12",kategori:"Çelik & Metal",njesia:"Ton",sasia:8.5,min:5,cmBlerje:92000,cmShitje:110000,furnitori:"KROMAÇEL SHPK",status:"Stok i Ulët"},
    {id:4,emri:"Hekur Armature Ø16",kategori:"Çelik & Metal",njesia:"Ton",sasia:3.2,min:4,cmBlerje:95000,cmShitje:115000,furnitori:"KROMAÇEL SHPK",status:"Stok Kritik"},
    {id:5,emri:"Tulla e zakonshme 25x12x6",kategori:"Muratim",njesia:"Copë (1000)",sasia:180,min:50,cmBlerje:28000,cmShitje:35000,furnitori:"Tullat Tirana",status:"Stok Normal"},
    {id:6,emri:"Kabllo NYY 3x2.5",kategori:"Elektrik",njesia:"Metër",sasia:1200,min:500,cmBlerje:320,cmShitje:420,furnitori:"Electro Alba",status:"Stok Normal"},
    {id:7,emri:"Kabllo NYY 3x6",kategori:"Elektrik",njesia:"Metër",sasia:380,min:300,cmBlerje:580,cmShitje:750,furnitori:"Electro Alba",status:"Stok i Ulët"},
    {id:8,emri:"Tub PVC Ø110 (zjarrëzike)",kategori:"Hidraulikë",njesia:"Metër",sasia:250,min:100,cmBlerje:480,cmShitje:620,furnitori:"Hidro System",status:"Stok Normal"},
    {id:9,emri:"Tub PPR Ø32",kategori:"Hidraulikë",njesia:"Metër",sasia:90,min:100,cmBlerje:220,cmShitje:290,furnitori:"Hidro System",status:"Stok Kritik"},
    {id:10,emri:"Gëlqere hidraulike",kategori:"Betoni & Strukturë",njesia:"Thes (25kg)",sasia:220,min:60,cmBlerje:450,cmShitje:580,furnitori:"TITAN Cement Albania",status:"Stok Normal"},
    {id:11,emri:"Izolim termik EPS 5cm",kategori:"Izolim",njesia:"m²",sasia:650,min:200,cmBlerje:380,cmShitje:500,furnitori:"IzoAlb SHPK",status:"Stok Normal"},
    {id:12,emri:"Shina gipsi 60/27",kategori:"Tjetër",njesia:"Metër",sasia:800,min:400,cmBlerje:180,cmShitje:240,furnitori:"Gyproc Albania",status:"Stok Normal"},
  ],
  pajisje: [
    {id:1,emri:"Betonierë 350L",kategori:"Makina",seria:"BET-350-2022",gjendja:"Shumë Mirë",vlera:850000,mirembajtja:"2025-06-01",lokacioni:"Kantieri Qendër",status:"Aktive"},
    {id:2,emri:"Grilë Këndi 115mm",kategori:"Mjete Dore",seria:"GK-115-A",gjendja:"Mirë",vlera:18000,mirembajtja:"2025-03-15",lokacioni:"Depo Kryesore",status:"Aktive"},
    {id:3,emri:"Vinç Torre 5t",kategori:"Makina të Rënda",seria:"VT-500-2020",gjendja:"Mirë",vlera:12500000,mirembajtja:"2025-04-20",lokacioni:"Kantieri Liqeni",status:"Aktive"},
    {id:4,emri:"Gjenerator 15KVA",kategori:"Elektrike",seria:"GEN-15K-21",gjendja:"Mirë",vlera:950000,mirembajtja:"2025-05-10",lokacioni:"Depo Kryesore",status:"Aktive"},
    {id:5,emri:"Dhëmb elektrik Bosch",kategori:"Mjete Dore",seria:"GSB-21-2RE",gjendja:"Mirë",vlera:32000,mirembajtja:"—",lokacioni:"Depo Kryesore",status:"Aktive"},
    {id:6,emri:"Pompë uji 3' ",kategori:"Elektrike",seria:"PU-3IN-19",gjendja:"Nevojitet Riparim",vlera:65000,mirembajtja:"2025-02-28",lokacioni:"Kantieri Qendër",status:"Riparim"},
    {id:7,emri:"Rrafshues betoni Wacker",kategori:"Makina",seria:"WK-BS45-23",gjendja:"Shumë Mirë",vlera:420000,mirembajtja:"2025-07-01",lokacioni:"Kantieri Liqeni",status:"Aktive"},
    {id:8,emri:"Skela metalike 200m²",kategori:"Skela",seria:"SK-META-18",gjendja:"Mirë",vlera:1800000,mirembajtja:"—",lokacioni:"Kantieri Qendër",status:"Aktive"},
  ],
  shitje: [
    {id:1,data:"2025-01-15",artikull:"Çimento Portland 42.5N",lloji:"Shitje",sasia:50,cmUnit:1050,total:52500,klienti:"Konstruksion Alba SHPK"},
    {id:2,data:"2025-01-18",artikull:"Hekur Armature Ø12",lloji:"Shitje",sasia:2,cmUnit:110000,total:220000,klienti:"Bejko & Associatë"},
    {id:3,data:"2025-01-20",artikull:"Tulla e zakonshme",lloji:"Blerje",sasia:100,cmUnit:28000,total:2800000,klienti:"Tullat Tirana"},
    {id:4,data:"2025-01-22",artikull:"Kabllo NYY 3x2.5",lloji:"Shitje",sasia:300,cmUnit:420,total:126000,klienti:"Elektro Marin"},
    {id:5,data:"2025-02-03",artikull:"Izolim termik EPS",lloji:"Shitje",sasia:120,cmUnit:500,total:60000,klienti:"Ndert Progres"},
    {id:6,data:"2025-02-08",artikull:"Hekur Armature Ø16",lloji:"Blerje",sasia:5,cmUnit:95000,total:475000,klienti:"KROMAÇEL SHPK"},
    {id:7,data:"2025-02-10",artikull:"Gëlqere hidraulike",lloji:"Shitje",sasia:80,cmUnit:580,total:46400,klienti:"Bardhi Konstruksion"},
    {id:8,data:"2025-02-14",artikull:"Tub PVC Ø110",lloji:"Shitje",sasia:50,cmUnit:620,total:31000,klienti:"Hidro Marin SHPK"},
  ],
  furnitoret: [
    {id:1,emri:"TITAN Cement Albania",nid:"L12345678A",kontakti:"+355 4 222 1234",adresa:"Rruga Nacionale, Shkodër",materialet:"Çimento, Gëlqere",afati:"30 ditë",status:"Aktiv"},
    {id:2,emri:"KROMAÇEL SHPK",nid:"K98765432B",kontakti:"+355 69 333 4444",adresa:"Autostrada Tiranë-Durrës km12",materialet:"Hekur, Çelik",afati:"15 ditë",status:"Aktiv"},
    {id:3,emri:"Electro Alba",nid:"M11223344C",kontakti:"+355 68 555 6666",adresa:"Rruga Kavajës, Tiranë",materialet:"Kabllo, Material Elektrik",afati:"45 ditë",status:"Aktiv"},
    {id:4,emri:"Hidro System",nid:"J55667788D",kontakti:"+355 67 777 8888",adresa:"Zona Industriale, Durrës",materialet:"Tuba, Fitting Hidraulikë",afati:"30 ditë",status:"Aktiv"},
    {id:5,emri:"Guri Alb SHPK",nid:"L33445566E",kontakti:"+355 52 111 2222",adresa:"Elbasan",materialet:"Zhavorr, Rëra, Gurë",afati:"Cash",status:"Aktiv"},
  ],
  shpenzime: [
    {id:1,data:"2025-01-05",pershkrimi:"Qira zyrë + depo",kategoria:"Qira",vlera:150000,tvsh:true},
    {id:2,data:"2025-01-10",pershkrimi:"Paga punëtorë Janar",kategoria:"Paga",vlera:420000,tvsh:false},
    {id:3,data:"2025-01-15",pershkrimi:"Karburant makinash",kategoria:"Transport",vlera:45000,tvsh:true},
    {id:4,data:"2025-02-05",pershkrimi:"Qira zyrë + depo",kategoria:"Qira",vlera:150000,tvsh:true},
    {id:5,data:"2025-02-10",pershkrimi:"Paga punëtorë Shkurt",kategoria:"Paga",vlera:420000,tvsh:false},
    {id:6,data:"2025-02-12",pershkrimi:"Mirëmbajtje makina",kategoria:"Mirëmbajtje",vlera:28000,tvsh:true},
    {id:7,data:"2025-02-14",pershkrimi:"Telefon + Internet",kategoria:"Komunikim",vlera:8500,tvsh:true},
  ],
  tatimi: {
    nipt: '',
    emri_tatimpagues: '',
    regjim: 'Normal', // Normal / Bизnes i Vogël
    tvsh_regjistruar: true,
    tatim_fitimi_norme: 15,
  },
  projektet: [
    {id:1,emri:'Pallati Rezidencial "Panorama"',klienti:'Konstruksion Alba SHPK',nipt_klienti:'K12345678L',fillimi:'2025-01-10',afati:'2025-09-30',buxheti:45000000,realizuar:32,statusi:'Aktiv',adresa:'Rruga e Kavajës, Tiranë',pershkrimi:'Ndërtim pallati 8 katësh, 32 apartamente',fazat:[{emri:'Themelet & Gërmimi',done:true},{emri:'Skelet Beton',done:true},{emri:'Muratura',done:false},{emri:'Fasada & Çatia',done:false},{emri:'Instalime',done:false},{emri:'Mbarimi i brendshëm',done:false}]},
    {id:2,emri:'Vila "Bregdeti" Durrës',klienti:'Bejko & Associatë',nipt_klienti:'L98765432B',fillimi:'2025-02-01',afati:'2025-07-15',buxheti:18000000,realizuar:68,statusi:'Vonuar',adresa:'Rruga Taulantia, Durrës',pershkrimi:'Ndërtim vilë private 2 katësh me pishinë',fazat:[{emri:'Themelet',done:true},{emri:'Skelet',done:true},{emri:'Çati',done:true},{emri:'Fasada',done:false},{emri:'Pishinë & Oborr',done:false}]},
    {id:3,emri:'Ndërtesa Komerciale "Alba Center"',klienti:'Invest Group SHPK',nipt_klienti:'M11122233N',fillimi:'2024-06-01',afati:'2025-01-31',buxheti:92000000,realizuar:100,statusi:'Përfunduar',adresa:'Blloku, Tiranë',pershkrimi:'Qendër tregtare 5 katësh me parking nëntokësor',fazat:[{emri:'Themelet',done:true},{emri:'Struktura',done:true},{emri:'Instalime',done:true},{emri:'Mbarimi',done:true}]},
  ],
  faturat: [
    {id:1,nr:'FAT-2025-001',data:'2025-01-20',klienti:'Konstruksion Alba SHPK',nipt:'K12345678L',projekti:'Pallati Rezidencial "Panorama"',zerat:[{pershkrimi:'Punë Betonierë — Themel',sasia:1,cmUnit:2500000,tvsh:true},{pershkrimi:'Material Çimento 320 thes',sasia:1,cmUnit:336000,tvsh:true}],statusi:'Paguar',skadon:'2025-02-20',shenime:''},
    {id:2,nr:'FAT-2025-002',data:'2025-02-05',klienti:'Bejko & Associatë',nipt:'L98765432B',projekti:'Vila "Bregdeti" Durrës',zerat:[{pershkrimi:'Punë Skelet Beton',sasia:1,cmUnit:4800000,tvsh:true},{pershkrimi:'Hekur Armature Ø12 — 2 ton',sasia:2,cmUnit:110000,tvsh:true}],statusi:'Në Pritje',skadon:'2025-03-05',shenime:''},
    {id:3,nr:'FAT-2025-003',data:'2025-02-15',klienti:'Invest Group SHPK',nipt:'M11122233N',projekti:'Alba Center',zerat:[{pershkrimi:'Punë Mbarimi Final',sasia:1,cmUnit:8500000,tvsh:true}],statusi:'Vonuar',skadon:'2025-02-28',shenime:'Klienti ka kërkuar shtyrje'},
  ],
  ofertat: [
    {id:1,nr:'OFE-2025-001',data:'2025-01-05',klienti:'Ndert Progres SHPK',sherbimi:'Ndërtim Magazinë 500m²',vlera:12500000,vlefshmeria:'2025-02-05',statusi:'Pranuar'},
    {id:2,nr:'OFE-2025-002',data:'2025-02-10',klienti:'Bardhi Konstruksion',sherbimi:'Rinovim Zyra 3 Kati',vlera:3800000,vlefshmeria:'2025-03-10',statusi:'Në Shqyrtim'},
    {id:3,nr:'OFE-2025-003',data:'2025-02-18',klienti:'Hotel Adriatik SHPK',sherbimi:'Ndërtim Pishinë Olimpike',vlera:22000000,vlefshmeria:'2025-03-18',statusi:'Dërguar'},
  ],
  raportet: {
    '2025-01': {
      shitje_mat:52500, shitje_she:220000, ardhura_tjera:0,
      blerje_mat:2800000, blerje_paj:0, blerje_tjera:475000,
      qira:150000, karb:45000, energji:18000, mirembajt:0, telekom:8500, shp_tjera:0,
      arka_fillim:1500000, banka:3200000, detyrime:0,
      stok_fillim:12000000, stok_fund:12400000, stok_kritik:2, stok_total_art:12,
      shenime:'Muaj i mirë. U nënshkrua kontrata me Invest Group.', objektivat:'Rritje shitjesh me 10%.', vleresim:'mire',
      punonjesit:[
        {emri:'Artan Hoxha',pozicioni:'Inxhinier',bruto:120000,statusi:'Paguar'},
        {emri:'Blerina Muça',pozicioni:'Kontabiliste',bruto:90000,statusi:'Paguar'},
        {emri:'Genti Kola',pozicioni:'Punëtor',bruto:55000,statusi:'Paguar'},
        {emri:'Dorjan Shehu',pozicioni:'Shofer',bruto:60000,statusi:'Paguar'},
      ], locked:true
    },
    '2025-02': {
      shitje_mat:46400, shitje_she:475000, ardhura_tjera:31000,
      blerje_mat:475000, blerje_paj:0, blerje_tjera:0,
      qira:150000, karb:45000, energji:18000, mirembajt:28000, telekom:8500, shp_tjera:0,
      arka_fillim:2100000, banka:4200000, detyrime:200000,
      stok_fillim:12400000, stok_fund:11850000, stok_kritik:3, stok_total_art:12,
      shenime:'U realizuan 3 shitje të mëdha. Pompë uji shkoi në riparim.', objektivat:'Të blihet pompa e re. Të hapen negociatat me hotelin.', vleresim:'mire',
      punonjesit:[
        {emri:'Artan Hoxha',pozicioni:'Inxhinier',bruto:120000,statusi:'Paguar'},
        {emri:'Blerina Muça',pozicioni:'Kontabiliste',bruto:90000,statusi:'Paguar'},
        {emri:'Genti Kola',pozicioni:'Punëtor',bruto:55000,statusi:'Pending'},
        {emri:'Dorjan Shehu',pozicioni:'Shofer',bruto:60000,statusi:'Pending'},
      ], locked:false
    },
  },
  punonjesit: [
    {id:1,emri:'Artan Hoxha',pozicioni:'Inxhinier Ndërtimi',fillimi:'2023-01-10',pagaBruto:120000,status:'Aktiv'},
    {id:2,emri:'Blerina Muça',pozicioni:'Kontabiliste',fillimi:'2022-06-01',pagaBruto:90000,status:'Aktiv'},
    {id:3,emri:'Genti Kola',pozicioni:'Punëtor Kantieri',fillimi:'2024-03-15',pagaBruto:55000,status:'Aktiv'},
    {id:4,emri:'Dorjan Shehu',pozicioni:'Shofer',fillimi:'2023-09-01',pagaBruto:60000,status:'Aktiv'},
  ],
  pagat: [
    {id:1,muaji:'2025-01',punonjesiId:1,pagaBruto:120000,status:'Paguar'},
    {id:2,muaji:'2025-01',punonjesiId:2,pagaBruto:90000,status:'Paguar'},
    {id:3,muaji:'2025-01',punonjesiId:3,pagaBruto:55000,status:'Paguar'},
    {id:4,muaji:'2025-01',punonjesiId:4,pagaBruto:60000,status:'Paguar'},
    {id:5,muaji:'2025-02',punonjesiId:1,pagaBruto:120000,status:'Paguar'},
    {id:6,muaji:'2025-02',punonjesiId:2,pagaBruto:90000,status:'Paguar'},
    {id:7,muaji:'2025-02',punonjesiId:3,pagaBruto:55000,status:'Pending'},
    {id:8,muaji:'2025-02',punonjesiId:4,pagaBruto:60000,status:'Pending'},
  ],
});

// ── SUBJECTS ──
function loadSubjects(){
  try{ return JSON.parse(localStorage.getItem('bt_subjects')||'null'); }catch(e){return null;}
}
function saveSubjects(){
  try{
    localStorage.setItem('bt_subjects', JSON.stringify(subjects));
    const el = document.getElementById('backup-status');
    if(el){ el.textContent='💾 Duke ruajtur...'; el.className='backup-status saving'; setTimeout(()=>{ const now=new Date(); el.textContent='✅ Ruajtur '+now.toLocaleTimeString('sq-AL',{hour:'2-digit',minute:'2-digit'}); el.className='backup-status'; },600); }
  }catch(e){ console.error(e); }
}
function loadCurrentSubjId(){
  return localStorage.getItem('bt_current_subj')||null;
}
function saveCurrentSubjId(id){
  localStorage.setItem('bt_current_subj', id);
}

let subjects = loadSubjects();
if(!subjects){
  subjects = [{id:'s1', emri:'Subjekti 1', ngjyra:'#f97316', data: defaultData()}];
  saveSubjects();
}

let currentSubjId = loadCurrentSubjId() || subjects[0].id;
// make sure saved id still exists
if(!subjects.find(s=>s.id===currentSubjId)) currentSubjId = subjects[0].id;

function getCurrentSubj(){
  return subjects.find(s=>s.id===currentSubjId);
}

// state is always a live reference to current subject data
let state = getCurrentSubj().data;

// ── MIGRATE old subjects to have new fields ──
function migrateState(s){
  if(!s.projektet) s.projektet=[];
  if(!s.faturat) s.faturat=[];
  if(!s.ofertat) s.ofertat=[];
  if(!s.raportet) s.raportet={};
}
subjects.forEach(subj=>migrateState(subj.data));
migrateState(state);

function switchSubject(id){
  // save current state back
  getCurrentSubj().data = state;
  saveSubjects();
  currentSubjId = id;
  saveCurrentSubjId(id);
  state = getCurrentSubj().data;
  migrateState(state);
  renderSubjectList();
  updateSubjTopbar();
  render();
}

function renderSubjectList(){
  const list = document.getElementById('subject-list');
  list.innerHTML = subjects.map(s=>`
    <button class="subject-btn ${s.id===currentSubjId?'active':''}" onclick="switchSubject('${s.id}')">
      <div class="subject-dot" style="background:${s.ngjyra}"></div>
      <span class="subject-name">${s.emri}</span>
      ${subjects.length>1?`<span class="subject-del" onclick="event.stopPropagation();deleteSubject('${s.id}')">✕</span>`:''}
      <span style="opacity:0;font-size:0.62rem;padding:1px 5px;border-radius:4px;background:rgba(249,115,22,0.12);color:var(--orange);border:none;cursor:pointer;transition:opacity 0.2s;margin-left:2px" class="subj-edit-btn" onclick="event.stopPropagation();openSubjectModal('${s.id}')">✏️</span>
    </button>
  `).join('');
}

function updateSubjTopbar(){
  const s = getCurrentSubj();
  document.getElementById('subj-name-top').textContent = s.emri;
  document.getElementById('subj-dot').style.background = s.ngjyra;
}

function deleteSubject(id){
  if(subjects.length<=1){alert('Nuk mund të fshish subjektin e vetëm!');return;}
  if(!confirm('Fshi këtë subjekt dhe të gjitha të dhënat e tij?')) return;
  subjects = subjects.filter(s=>s.id!==id);
  if(currentSubjId===id) currentSubjId = subjects[0].id;
  saveSubjects();
  saveCurrentSubjId(currentSubjId);
  state = getCurrentSubj().data;
  renderSubjectList();
  updateSubjTopbar();
  render();
}

// ── SUBJECT MODAL ──
let editingSubjId = null;
function openSubjectModal(id){
  editingSubjId = id||null;
  const s = id ? subjects.find(x=>x.id===id) : null;
  selectedColor = s ? s.ngjyra : COLORS[subjects.length % COLORS.length];
  document.getElementById('subj-modal-title').textContent = id ? 'Modifiko Subjektin' : '➕ Shto Subjekt';
  document.getElementById('subj-emri').value    = s?.emri||'';
  document.getElementById('subj-nipt').value    = s?.nipt||'';
  document.getElementById('subj-tel').value     = s?.tel||'';
  document.getElementById('subj-adresa').value  = s?.adresa||'';
  document.getElementById('subj-email').value   = s?.email||'';
  document.getElementById('subj-web').value     = s?.website||'';
  document.getElementById('subj-logo').value    = s?.logo||'';
  document.getElementById('subj-shenimFature').value = s?.shenimFature||'';
  // Logo preview
  updateLogoPreview(s?.logo||'');
  // Color picker
  document.getElementById('color-picker').innerHTML = COLORS.map(c=>
    `<div class="color-opt ${c===selectedColor?'sel':''}" style="background:${c}" onclick="selectColor('${c}',this)"></div>`
  ).join('');
  document.getElementById('subj-modal-overlay').classList.add('open');
}
function closeSubjectModal(){
  document.getElementById('subj-modal-overlay').classList.remove('open');
}
function selectColor(c, el){
  selectedColor = c;
  document.querySelectorAll('.color-opt').forEach(x=>x.classList.remove('sel'));
  el.classList.add('sel');
}
function loadLogoFile(e){
  const file=e.target.files[0]; if(!file) return;
  const reader=new FileReader();
  reader.onload=ev=>{
    document.getElementById('subj-logo').value=ev.target.result;
    updateLogoPreview(ev.target.result);
  };
  reader.readAsDataURL(file);
}
function updateLogoPreview(src){
  const wrap=document.getElementById('subj-logo-preview');
  const img=document.getElementById('subj-logo-img');
  if(src&&wrap&&img){ wrap.style.display=''; img.src=src; }
  else if(wrap){ wrap.style.display='none'; }
}
function saveSubject(){
  const emri = document.getElementById('subj-emri').value.trim();
  if(!emri){alert('Shkruaj emrin e subjektit!');return;}
  const info={
    emri, ngjyra:selectedColor,
    nipt:   document.getElementById('subj-nipt').value.trim(),
    tel:    document.getElementById('subj-tel').value.trim(),
    adresa: document.getElementById('subj-adresa').value.trim(),
    email:  document.getElementById('subj-email').value.trim(),
    website:document.getElementById('subj-web').value.trim(),
    logo:   document.getElementById('subj-logo').value.trim(),
    shenimFature: document.getElementById('subj-shenimFature').value.trim(),
  };
  if(editingSubjId){
    const s = subjects.find(x=>x.id===editingSubjId);
    Object.assign(s, info);
  } else {
    if(subjects.length>=4){alert('Maksimumi 4 subjekte!');return;}
    subjects.push({id:'s'+Date.now(), ...info, data: defaultData()});
  }
  saveSubjects(); renderSubjectList(); updateSubjTopbar(); closeSubjectModal();
  showToast('✅ Informacioni i kompanisë u ruajt!','🏢');
}

let currentPanel = 'dashboard';
let editingId = null;
let currentMat = 'all';

// ═══════════════════════════════════════════════
// NAVIGATION
// ═══════════════════════════════════════════════
function showPanel(name, el){
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.getElementById('panel-'+name).classList.add('active');
  if(el) el.classList.add('active');
  currentPanel = name;
  const titles={dashboard:'Dashboard',inventar:'📦 Inventar Live',materiale:'Materiale',pajisje:'Pajisje & Mjete',shitje:'Shitje & Stok',furnitoret:'Furnitorët',bilanci:'Bilanci & Tatimi',hr:'Paga & HR',projektet:'📋 Kontratat & Projektet',faturat:'🧾 Fatura & Oferta',raporti:'🗓️ Raporti Mujor i Biznesit'};
  document.getElementById('topbar-title').textContent = titles[name]||name;
  render();
}

// ═══════════════════════════════════════════════
// RENDER
// ═══════════════════════════════════════════════
function render(){
  renderDashboard();
  renderMateriale();
  renderPajisje();
  renderShitje();
  renderFurnitoret();
  renderBilanci();
  renderHR();
  renderInvenLive();
  renderProjektet();
  renderFaturat();
  renderRaporti();
  updateBadges();
}

function fmt(n){return Number(n).toLocaleString('sq-AL',{minimumFractionDigits:0,maximumFractionDigits:0})+' L'}
function statusBadge(s){
  const map={'Stok Normal':'badge-green','Stok i Ulët':'badge-yellow','Stok Kritik':'badge-red',
    'Aktive':'badge-green','Riparim':'badge-yellow','Joaktive':'badge-red',
    'Shitje':'badge-green','Blerje':'badge-blue','Aktiv':'badge-green'};
  return `<span class="badge ${map[s]||'badge-blue'}">${s}</span>`;
}

function renderDashboard(){
  const totArtikuj = state.materiale.length + state.pajisje.length;
  const totVlera = state.materiale.reduce((s,m)=>s+m.sasia*m.cmBlerje,0)+state.pajisje.reduce((s,p)=>s+p.vlera,0);
  const ulët = state.materiale.filter(m=>m.status==='Stok i Ulët'||m.status==='Stok Kritik').length;
  document.getElementById('d-artikuj').textContent = totArtikuj;
  document.getElementById('d-vlera').textContent = fmt(totVlera);
  document.getElementById('d-ulët').textContent = ulët;
  document.getElementById('d-furnitorë').textContent = state.furnitoret.length;

  // Stats lidhje
  const shitjeCnt = state.shitje.filter(s=>s.lloji==='Shitje').length;
  const blerjetCnt = state.shitje.filter(s=>s.lloji==='Blerje').length;
  const pagaCnt = (state.pagat||[]).length;
  const dShitje = document.getElementById('d-shitje-cnt');
  const dBlerje = document.getElementById('d-blerje-cnt');
  const dPaga = document.getElementById('d-paga-cnt');
  if(dShitje) dShitje.textContent = shitjeCnt>0 ? shitjeCnt+' tx' : 'Auto';
  if(dBlerje) dBlerje.textContent = blerjetCnt>0 ? blerjetCnt+' tx' : 'Auto';
  if(dPaga) dPaga.textContent = pagaCnt>0 ? pagaCnt+' reg' : 'Auto';

  // Alerts
  const alerts = state.materiale.filter(m=>m.status!=='Stok Normal');
  const al = document.getElementById('alert-list');
  if(alerts.length===0){al.innerHTML=`<div class="empty"><div class="empty-icon">✅</div>Nuk ka alarme stoku!</div>`;return;}
  al.innerHTML = alerts.map(m=>`
    <div class="alert-item ${m.status==='Stok Kritik'?'':'warn'}">
      <div class="alert-dot ${m.status==='Stok Kritik'?'red':'warn'}"></div>
      <div class="alert-text">
        <div class="alert-name">${m.emri}</div>
        <div class="alert-sub">Sasia: ${m.sasia} ${m.njesia} — Minimumi: ${m.min} — Furnitori: ${m.furnitori}</div>
      </div>
      ${statusBadge(m.status)}
    </div>`).join('');

  // Dash table — last 8 materiale
  document.getElementById('dash-table').innerHTML = state.materiale.slice(0,8).map(m=>`
    <tr>
      <td>${m.emri}</td><td>${m.kategori}</td>
      <td class="mono">${m.sasia} ${m.njesia}</td>
      <td class="mono">${fmt(m.sasia*m.cmBlerje)}</td>
      <td>${statusBadge(m.status)}</td>
    </tr>`).join('');
}

function renderMateriale(){
  const filtered = currentMat==='all'?state.materiale:state.materiale.filter(m=>m.kategori===currentMat);
  document.getElementById('mat-tbody').innerHTML = filtered.map((m,i)=>`
    <tr>
      <td class="mono">${i+1}</td>
      <td><strong>${m.emri}</strong></td>
      <td>${m.kategori}</td>
      <td class="mono">${m.njesia}</td>
      <td class="mono">
        ${m.sasia}
        <div class="prog-track"><div class="prog-fill" style="width:${Math.min(100,m.sasia/m.min*100)}%;background:${m.sasia<m.min?'#ef4444':m.sasia<m.min*1.5?'#eab308':'#22c55e'}"></div></div>
      </td>
      <td class="mono">${m.min}</td>
      <td class="mono">${fmt(m.cmBlerje)}</td>
      <td class="mono">${fmt(m.cmShitje)}</td>
      <td style="font-size:0.75rem">${m.furnitori}</td>
      <td>${statusBadge(m.status)}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="editItem('mat',${m.id})">✏️</button>
        <button class="action-btn del" onclick="deleteItem('mat',${m.id})">🗑️</button>
      </td>
    </tr>`).join('') || `<tr><td colspan="11" style="text-align:center;padding:32px;color:var(--muted)">Nuk ka materiale</td></tr>`;
}

function renderPajisje(){
  document.getElementById('paj-tbody').innerHTML = state.pajisje.map((p,i)=>`
    <tr>
      <td class="mono">${i+1}</td>
      <td><strong>${p.emri}</strong></td>
      <td>${p.kategori}</td>
      <td class="mono">${p.seria}</td>
      <td>${p.gjendja}</td>
      <td class="mono">${fmt(p.vlera)}</td>
      <td class="mono" style="color:var(--yellow)">${p.mirembajtja}</td>
      <td style="font-size:0.75rem">${p.lokacioni}</td>
      <td>${statusBadge(p.status)}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="editItem('paj',${p.id})">✏️</button>
        <button class="action-btn del" onclick="deleteItem('paj',${p.id})">🗑️</button>
      </td>
    </tr>`).join('');
}

function renderShitje(){
  const shitjet = state.shitje.filter(s=>s.lloji==='Shitje');
  const totSh = shitjet.reduce((s,x)=>s+x.total,0);
  document.getElementById('sh-total').textContent = fmt(totSh);
  document.getElementById('sh-count').textContent = state.shitje.length;
  // avg margin
  let margin = 0;
  shitjet.forEach(sh=>{
    const mat = state.materiale.find(m=>sh.artikull.includes(m.emri.split(' ')[0]));
    if(mat) margin += (sh.cmUnit - mat.cmBlerje)/sh.cmUnit*100;
  });
  document.getElementById('sh-profit').textContent = shitjet.length?(margin/shitjet.length).toFixed(1)+'%':'—';

  document.getElementById('sh-tbody').innerHTML = [...state.shitje].reverse().map((s,i)=>`
    <tr>
      <td class="mono">${state.shitje.length-i}</td>
      <td class="mono">${s.data}</td>
      <td><strong>${s.artikull}</strong></td>
      <td>${statusBadge(s.lloji)}</td>
      <td class="mono">${s.sasia}</td>
      <td class="mono">${fmt(s.cmUnit)}</td>
      <td class="mono" style="color:${s.lloji==='Shitje'?'var(--green)':'var(--orange)'}">${fmt(s.total)}</td>
      <td style="font-size:0.75rem">${s.klienti}</td>
      <td>
        <button class="action-btn del" onclick="deleteItem('sh',${s.id})">🗑️</button>
      </td>
    </tr>`).join('');
}

function renderFurnitoret(){
  const colors=['f0','f1','f2','f3','f4'];
  document.getElementById('furnitor-grid').innerHTML = state.furnitoret.map((f,i)=>`
    <div class="furnitor-card ${colors[i%5]}" style="animation-delay:${i*0.06}s">
      <div class="f-name">🚛 ${f.emri}</div>
      <div class="f-nid">${f.nid}</div>
      <div class="f-row"><span class="f-row-label">Kontakt</span><span class="f-row-val">${f.kontakti}</span></div>
      <div class="f-row"><span class="f-row-label">Afati</span><span class="f-row-val" style="color:var(--yellow)">${f.afati}</span></div>
      <div class="f-row"><span class="f-row-label">Materialet</span></div>
      <div style="font-size:0.72rem;color:var(--muted);margin-top:2px">${f.materialet}</div>
    </div>`).join('');

  document.getElementById('fur-tbody').innerHTML = state.furnitoret.map((f,i)=>`
    <tr>
      <td class="mono">${i+1}</td>
      <td><strong>${f.emri}</strong></td>
      <td class="mono">${f.nid}</td>
      <td>${f.kontakti}</td>
      <td style="font-size:0.75rem">${f.adresa}</td>
      <td style="font-size:0.75rem">${f.materialet}</td>
      <td class="mono" style="color:var(--yellow)">${f.afati}</td>
      <td>${statusBadge(f.status)}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="editItem('fur',${f.id})">✏️</button>
        <button class="action-btn del" onclick="deleteItem('fur',${f.id})">🗑️</button>
      </td>
    </tr>`).join('');
}

// ═══════════════════════════════════════════════
// INVENTAR LIVE
// ═══════════════════════════════════════════════
let invFilter = 'all';
let invSearch = '';

function filterInv(f, el){
  invFilter = f;
  document.querySelectorAll('#inv-filter-tabs .tab').forEach(t=>t.classList.remove('active'));
  if(el) el.classList.add('active');
  renderInvenLive();
}

function searchInv(q){
  invSearch = q.toLowerCase();
  renderInvenLive();
}

function renderInvenLive(){
  const grid = document.getElementById('inv-cards-grid');
  if(!grid) return;

  let list = [...state.materiale];

  // Filter sipas statusit
  if(invFilter==='normal') list = list.filter(m=>m.status==='Stok Normal');
  else if(invFilter==='ulet') list = list.filter(m=>m.status==='Stok i Ulët');
  else if(invFilter==='kritik') list = list.filter(m=>m.status==='Stok Kritik');

  // Search
  if(invSearch) list = list.filter(m=>m.emri.toLowerCase().includes(invSearch)||m.kategori.toLowerCase().includes(invSearch)||m.furnitori.toLowerCase().includes(invSearch));

  // Stats
  const totalArt = state.materiale.length;
  const vlera = state.materiale.reduce((s,m)=>s+m.sasia*m.cmBlerje,0);
  const ulet = state.materiale.filter(m=>m.status==='Stok i Ulët').length;
  const kritik = state.materiale.filter(m=>m.status==='Stok Kritik').length;
  const el1=document.getElementById('inv-total-art'); if(el1) el1.textContent=totalArt;
  const el2=document.getElementById('inv-vlera'); if(el2) el2.textContent=fmt(vlera);
  const el3=document.getElementById('inv-ulet'); if(el3) el3.textContent=ulet;
  const el4=document.getElementById('inv-kritik'); if(el4) el4.textContent=kritik;

  if(list.length===0){
    grid.innerHTML=`<div class="empty" style="grid-column:1/-1"><div class="empty-icon">📦</div>Nuk ka artikuj për këtë filtër</div>`;
    return;
  }

  // Rendero kartat — kritik/ulët sipër
  list.sort((a,b)=>{
    const order={'Stok Kritik':0,'Stok i Ulët':1,'Stok Normal':2};
    return (order[a.status]||2)-(order[b.status]||2);
  });

  const cls = {
    'Stok Normal':'normal',
    'Stok i Ulët':'ulet',
    'Stok Kritik':'kritik'
  };

  const pct = m => m.min>0 ? Math.min(100, Math.round(m.sasia/m.min*100)) : 100;
  const barColor = m => m.status==='Stok Kritik'?'var(--red)':m.status==='Stok i Ulët'?'var(--yellow)':'var(--green)';
  const badgeCls = m => m.status==='Stok Normal'?'badge-green':m.status==='Stok i Ulët'?'badge-yellow':'badge-red';
  const cardCls = m => cls[m.status]||'normal';

  grid.innerHTML = list.map((m,i)=>{
    const cc = cardCls(m);
    const bc = badgeCls(m);
    const bar = barColor(m);
    const p = pct(m);
    return '<div class="inv-card '+cc+'" style="animation-delay:'+( i*0.04)+'s" id="inv-card-'+m.id+'">'
      +'<div class="inv-card-header">'
      +'<div>'
      +'<div class="inv-card-name">'+m.emri+'</div>'
      +'<div class="inv-card-cat">'+m.kategori+'</div>'
      +'</div>'
      +'<span class="badge '+bc+'">'+m.status+'</span>'
      +'</div>'
      +'<div style="display:flex;align-items:baseline;gap:6px">'
      +'<div class="inv-sasia-big '+cc+'">'+m.sasia+'</div>'
      +'<div class="inv-njesia">'+m.njesia+'</div>'
      +'<div style="margin-left:auto;font-size:0.7rem;color:var(--muted)">min: <strong>'+m.min+'</strong></div>'
      +'</div>'
      +'<div class="inv-prog-wrap">'
      +'<div class="inv-prog-label"><span>Stoku</span><span style="color:'+bar+'">'+p+'%</span></div>'
      +'<div class="prog-track"><div class="prog-fill" style="width:'+p+'%;background:'+bar+'"></div></div>'
      +'</div>'
      +'<div class="inv-meta">'
      +'<div class="inv-meta-item"><div class="inv-meta-label">Çmimi Blerje</div><div class="inv-meta-val">'+fmt(m.cmBlerje)+'</div></div>'
      +'<div class="inv-meta-item"><div class="inv-meta-label">Çmimi Shitje</div><div class="inv-meta-val">'+fmt(m.cmShitje)+'</div></div>'
      +'<div class="inv-meta-item"><div class="inv-meta-label">Vlera Stokut</div><div class="inv-meta-val" style="color:var(--cyan)">'+fmt(m.sasia*m.cmBlerje)+'</div></div>'
      +'<div class="inv-meta-item"><div class="inv-meta-label">Furnitori</div><div class="inv-meta-val" style="font-size:0.68rem;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">'+(m.furnitori||'—')+'</div></div>'
      +'</div>'
      +'<div class="inv-card-actions">'
      +'<button class="inv-btn inv-btn-sell" onclick="quickShitje('+m.id+')">💰 Shito</button>'
      +'<button class="inv-btn inv-btn-add" onclick="quickBlerje('+m.id+')">📦 Shto Stok</button>'
      +'<button class="inv-btn inv-btn-edit" onclick="editItem(\'mat\','+m.id+')">✏️</button>'
      +'</div>'
      +'</div>';
  }).join('');
}

function quickShitje(matId){
  // Hap modalin e shitjes me materialin të para-zgjedhur
  currentPanel='shitje';
  openModal();
  setTimeout(()=>{
    const sel=document.getElementById('f-art-sel');
    if(sel){
      sel.value=matId;
      onArtikullChange();
    }
  },80);
}

function quickBlerje(matId){
  // Hap modalin e shitjes në modalitetin Blerje me materialin të para-zgjedhur
  currentPanel='shitje';
  openModal();
  setTimeout(()=>{
    const sel=document.getElementById('f-art-sel');
    const lloji=document.getElementById('f-llj');
    if(sel&&lloji){
      lloji.value='Blerje';
      sel.value=matId;
      onLlojiChange();
      onArtikullChange();
    }
  },80);
}


// updateBadges defined below (unified version)

// ═══════════════════════════════════════════════
// FILTER & SEARCH
// ═══════════════════════════════════════════════
function filterMat(cat, el){
  currentMat = cat;
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  renderMateriale();
}

function searchTable(tbodyId, q){
  const rows = document.getElementById(tbodyId).querySelectorAll('tr');
  rows.forEach(row=>{
    row.style.display = row.textContent.toLowerCase().includes(q.toLowerCase())?'':'none';
  });
}

// ═══════════════════════════════════════════════
// MODAL (openModal defined below — unified version)
// ═══════════════════════════════════════════════

function closeModal(){
  document.getElementById('modal-overlay').classList.remove('open');
  editingId=null;
  const a=document.getElementById('modal-actions');
  if(a) a.innerHTML='<button class="btn btn-ghost" onclick="closeModal()">Anulo</button><button class="btn btn-primary" onclick="saveItem()">💾 Ruaj</button>';
}

function g(id){const el=document.getElementById(id);return el?el.value:''}

function editItem(type, id){
  document._saveType=type;
  const panelMap={mat:'materiale',paj:'pajisje',sh:'shitje',fur:'furnitoret',shp:'bilanci'};
  currentPanel=panelMap[type];
  openModal(type, id);
}

function deleteItem(type, id){
  if(!confirm('Fshi këtë artikull?')) return;
  if(type==='mat') state.materiale=state.materiale.filter(m=>m.id!==id);
  else if(type==='paj') state.pajisje=state.pajisje.filter(p=>p.id!==id);
  else if(type==='sh') state.shitje=state.shitje.filter(s=>s.id!==id);
  else if(type==='fur') state.furnitoret=state.furnitoret.filter(f=>f.id!==id);
  else if(type==='shp') state.shpenzime=state.shpenzime.filter(s=>s.id!==id);
  getCurrentSubj().data = state;
  saveSubjects();
  render();
}

// ═══════════════════════════════════════════════
// EXPORT CSV
// ═══════════════════════════════════════════════
function exportCSV(){
  const p = currentPanel;
  let csv='', filename='inventar';
  if(p==='materiale'||p==='dashboard'){
    csv='Emri,Kategori,Njesia,Sasia,Min,Cmimi Blerje,Cmimi Shitje,Furnitori,Status\n';
    state.materiale.forEach(m=>csv+=`"${m.emri}","${m.kategori}","${m.njesia}",${m.sasia},${m.min},${m.cmBlerje},${m.cmShitje},"${m.furnitori}","${m.status}"\n`);
    filename='materiale';
  } else if(p==='pajisje'){
    csv='Emri,Kategori,Seria,Gjendja,Vlera,Mirembajtja,Lokacioni,Status\n';
    state.pajisje.forEach(p=>csv+=`"${p.emri}","${p.kategori}","${p.seria}","${p.gjendja}",${p.vlera},"${p.mirembajtja}","${p.lokacioni}","${p.status}"\n`);
    filename='pajisje';
  } else if(p==='shitje'){
    csv='Data,Artikull,Lloji,Sasia,Cmimi Unit,Total,Klienti\n';
    state.shitje.forEach(s=>csv+=`"${s.data}","${s.artikull}","${s.lloji}",${s.sasia},${s.cmUnit},${s.total},"${s.klienti}"\n`);
    filename='shitje';
  } else if(p==='furnitoret'){
    csv='Emri,NID,Kontakti,Adresa,Materialet,Afati,Status\n';
    state.furnitoret.forEach(f=>csv+=`"${f.emri}","${f.nid}","${f.kontakti}","${f.adresa}","${f.materialet}","${f.afati}","${f.status}"\n`);
    filename='furnitoret';
  }
  const blob=new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8'});
  const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download=filename+'.csv';a.click();
}

// ═══════════════════════════════════════════════
// BILANCI & TATIMI
// ═══════════════════════════════════════════════
let bilPeriod = 'vit';
let bilChart = null;

function setBilPeriod(p, el){
  bilPeriod = p;
  document.querySelectorAll('#panel-bilanci .tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  const mSel = document.getElementById('bil-month');
  if(mSel) mSel.style.display = p==='muaj'?'':'none';
  renderBilanci();
}

function getBilFilter(){
  const yearSel = document.getElementById('bil-year');
  const monthSel = document.getElementById('bil-month');
  if(!yearSel) return {year:null,month:null};
  const year = yearSel.value;
  const month = monthSel?monthSel.value:null;
  return {year, month};
}

function filterByPeriod(arr, dateField){
  const {year, month} = getBilFilter();
  return arr.filter(x=>{
    if(!x[dateField]) return false;
    const d = x[dateField];
    if(bilPeriod==='vit') return d.startsWith(year);
    return d.startsWith(year+'-'+month);
  });
}

function initBilYears(){
  const yearSel = document.getElementById('bil-year');
  if(!yearSel) return;
  const allDates = [
    ...state.shitje.map(s=>s.data),
    ...(state.shpenzime||[]).map(s=>s.data)
  ].filter(Boolean).map(d=>d.slice(0,4));
  const years = [...new Set(allDates)].sort().reverse();
  if(!years.length) years.push(new Date().getFullYear().toString());
  const curYear = yearSel.value || years[0];
  yearSel.innerHTML = years.map(y=>`<option value="${y}" ${y===curYear?'selected':''}>${y}</option>`).join('');
}

function renderBilanci(){
  if(!document.getElementById('bil-ardhura')) return;
  if(!state.shpenzime) state.shpenzime = [];
  if(!state.tatimi) state.tatimi = {nipt:'',emri_tatimpagues:'',regjim:'Normal',tvsh_regjistruar:true,tatim_fitimi_norme:15};

  initBilYears();

  const shitjet = filterByPeriod(state.shitje, 'data').filter(s=>s.lloji==='Shitje');
  const blerjet = filterByPeriod(state.shitje, 'data').filter(s=>s.lloji==='Blerje');
  const shpenzime = filterByPeriod(state.shpenzime, 'data');

  // Paga & HR — merged into bilanci
  const {year:bilYear, month:bilMonth} = getBilFilter();
  const pagat = (state.pagat||[]).filter(p=>{
    if(bilPeriod==='vit') return p.muaji && p.muaji.startsWith(bilYear);
    return p.muaji === bilYear+'-'+bilMonth;
  });
  const KONTRIBUTE_PUNEDH = 0.167;
  const TATIM_ARDHURA = 0.13;
  const totalPaga = pagat.reduce((s,p)=>{
    const bruto = p.pagaBruto||0;
    const kontribute = bruto * KONTRIBUTE_PUNEDH;
    return s + bruto + kontribute;
  }, 0);

  // Financials
  const ardhura = shitjet.reduce((s,x)=>s+x.total,0);
  const kostoB  = blerjet.reduce((s,x)=>s+x.total,0);
  const shpOp   = shpenzime.reduce((s,x)=>s+x.vlera,0);
  const totalShp = kostoB + shpOp + totalPaga;
  const fitimPara = ardhura - totalShp;

  // TVSH
  const TVSH = 0.20;
  const tvshMbj = shitjet.reduce((s,x)=>s + x.total*TVSH/(1+TVSH), 0); // assume prices incl. TVSH
  const tvshZbr = [...blerjet, ...shpenzime.filter(s=>s.tvsh)].reduce((s,x)=>{
    const v = x.total||x.vlera||0;
    return s + v*TVSH;
  },0);
  const tvshNet = Math.max(0, tvshMbj - tvshZbr);

  // Tatim fitimi
  const norme = (state.tatimi.tatim_fitimi_norme||15)/100;
  const tatimFitimi = fitimPara>0 ? fitimPara*norme : 0;
  const fitimNeto = fitimPara - tatimFitimi;

  // Update cards
  document.getElementById('bil-ardhura').textContent = fmt(ardhura);
  document.getElementById('bil-shpenzime').textContent = fmt(totalShp);
  document.getElementById('bil-fitim-para').textContent = fmt(fitimPara);
  document.getElementById('bil-fitim-neto').textContent = fmt(fitimNeto);
  document.getElementById('bil-tvsh-mbj').textContent = fmt(tvshMbj);
  document.getElementById('bil-tvsh-zbr').textContent = fmt(tvshZbr);
  document.getElementById('bil-tvsh-net').textContent = fmt(tvshNet);

  // Color fitim
  const fpEl = document.getElementById('bil-fitim-para');
  const fnEl = document.getElementById('bil-fitim-neto');
  fpEl.style.color = fitimPara>=0?'var(--green)':'var(--red)';
  fnEl.style.color = fitimNeto>=0?'var(--green)':'var(--red)';

  // Tatim box
  const marzhi = ardhura>0?(fitimPara/ardhura*100).toFixed(1):0;
  document.getElementById('bil-tatim-box').innerHTML = `
    <div class="bil-tatim-card"><div class="bil-tc-label">Tatim Fitimi (${state.tatimi.tatim_fitimi_norme||15}%)</div><div class="bil-tc-val" style="color:var(--red)">${fmt(tatimFitimi)}</div><div class="bil-tc-sub">Norma: ${state.tatimi.regjim||'Normal'}</div></div>
    <div class="bil-tatim-card green"><div class="bil-tc-label">TVSH për Pagesë</div><div class="bil-tc-val" style="color:var(--yellow)">${fmt(tvshNet)}</div><div class="bil-tc-sub">Deklaratë mujore</div></div>
    <div class="bil-tatim-card red"><div class="bil-tc-label">Marzhi i Fitimit</div><div class="bil-tc-val" style="color:${marzhi>=0?'var(--green)':'var(--red)'}">${marzhi}%</div><div class="bil-tc-sub">Fitim / Të ardhura</div></div>
  `;

  // Chart — monthly breakdown for the year
  renderBilChart();

  // Shpenzime table
  document.getElementById('shp-tbody').innerHTML = [...shpenzime].reverse().map((s,i)=>{
    const tvshAmt = s.tvsh?(s.vlera*TVSH):0;
    return `<tr>
      <td class="mono">${shpenzime.length-i}</td>
      <td class="mono">${s.data}</td>
      <td><strong>${s.pershkrimi}</strong></td>
      <td><span class="badge badge-blue">${s.kategoria}</span></td>
      <td class="mono">${fmt(s.vlera)}</td>
      <td class="mono" style="color:var(--yellow)">${s.tvsh?fmt(tvshAmt):'—'}</td>
      <td class="mono" style="color:var(--red)">${fmt(s.vlera+tvshAmt)}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="editItem('shp',${s.id})">✏️</button>
        <button class="action-btn del" onclick="deleteItem('shp',${s.id})">🗑️</button>
      </td>
    </tr>`;
  }).join('') || `<tr><td colspan="8" style="text-align:center;padding:32px;color:var(--muted)">Nuk ka shpenzime të regjistruara</td></tr>`;
}

function renderBilChart(){
  const canvas = document.getElementById('bil-chart');
  if(!canvas) return;
  const {year} = getBilFilter();
  const months = ['Jan','Shk','Mar','Pri','Maj','Qer','Kor','Gus','Sht','Tet','Nën','Dhj'];

  const ardhM = Array(12).fill(0);
  const shpM  = Array(12).fill(0);

  state.shitje.filter(s=>s.data&&s.data.startsWith(year)&&s.lloji==='Shitje').forEach(s=>{
    const m = parseInt(s.data.slice(5,7))-1;
    ardhM[m] += s.total;
  });
  state.shitje.filter(s=>s.data&&s.data.startsWith(year)&&s.lloji==='Blerje').forEach(s=>{
    const m = parseInt(s.data.slice(5,7))-1;
    shpM[m] += s.total;
  });
  (state.shpenzime||[]).filter(s=>s.data&&s.data.startsWith(year)).forEach(s=>{
    const m = parseInt(s.data.slice(5,7))-1;
    shpM[m] += s.vlera;
  });

  const maxVal = Math.max(...ardhM,...shpM,1);
  const W = canvas.offsetWidth||600, H = canvas.offsetHeight||200;
  canvas.width = W; canvas.height = H;
  const ctx = canvas.getContext('2d');
  ctx.clearRect(0,0,W,H);

  const padL=40, padR=16, padT=16, padB=36;
  const barW = (W-padL-padR)/(12*2+12*0.5);
  const gap = barW*0.5;

  months.forEach((m,i)=>{
    const x = padL + i*(barW*2+gap);
    const hA = (ardhM[i]/maxVal)*(H-padT-padB);
    const hS = (shpM[i]/maxVal)*(H-padT-padB);

    // Ardhura bar
    ctx.fillStyle='rgba(34,197,94,0.7)';
    ctx.beginPath();
    ctx.roundRect(x, H-padB-hA, barW, hA, [3,3,0,0]);
    ctx.fill();

    // Shpenzime bar
    ctx.fillStyle='rgba(239,68,68,0.7)';
    ctx.beginPath();
    ctx.roundRect(x+barW+2, H-padB-hS, barW, hS, [3,3,0,0]);
    ctx.fill();

    // Month label
    ctx.fillStyle='#7a8ba8';
    ctx.font='10px DM Sans,sans-serif';
    ctx.textAlign='center';
    ctx.fillText(m, x+barW, H-padB+14);
  });

  // Y axis hint
  ctx.fillStyle='#7a8ba8';
  ctx.font='9px DM Sans,sans-serif';
  ctx.textAlign='right';
  [0,0.5,1].forEach(f=>{
    const y = H-padB - f*(H-padT-padB);
    ctx.fillText((maxVal*f/1000).toFixed(0)+'k', padL-4, y+3);
    ctx.strokeStyle='rgba(255,255,255,0.04)';
    ctx.beginPath(); ctx.moveTo(padL,y); ctx.lineTo(W-padR,y); ctx.stroke();
  });

  // Legend
  ctx.fillStyle='rgba(34,197,94,0.8)'; ctx.fillRect(padL,4,10,8);
  ctx.fillStyle='#e8edf5'; ctx.font='10px DM Sans'; ctx.textAlign='left';
  ctx.fillText('Të Ardhura', padL+14, 11);
  ctx.fillStyle='rgba(239,68,68,0.8)'; ctx.fillRect(padL+90,4,10,8);
  ctx.fillStyle='#e8edf5'; ctx.fillText('Shpenzime', padL+104, 11);
}

function exportBilanciPDF(){
  const subj = getCurrentSubj();
  const {year} = getBilFilter();
  const shitjet = filterByPeriod(state.shitje,'data').filter(s=>s.lloji==='Shitje');
  const blerjet = filterByPeriod(state.shitje,'data').filter(s=>s.lloji==='Blerje');
  const shpenzime = filterByPeriod(state.shpenzime,'data');
  const ardhura = shitjet.reduce((s,x)=>s+x.total,0);
  const totalShp = blerjet.reduce((s,x)=>s+x.total,0)+shpenzime.reduce((s,x)=>s+x.vlera,0);
  const fitim = ardhura - totalShp;
  const norme = (state.tatimi?.tatim_fitimi_norme||15)/100;
  const tatim = fitim>0?fitim*norme:0;

  const html=`<!DOCTYPE html><html><head><meta charset="UTF-8">
  <title>Raport Financiar — ${subj.emri}</title>
  <style>
    body{font-family:Arial,sans-serif;color:#1a1a1a;padding:40px;max-width:800px;margin:0 auto}
    h1{font-size:22px;margin-bottom:4px} .sub{color:#666;font-size:13px;margin-bottom:32px}
    .row{display:flex;justify-content:space-between;padding:10px 0;border-bottom:1px solid #eee;font-size:14px}
    .row.total{font-weight:bold;font-size:16px;border-top:2px solid #333;border-bottom:none;margin-top:8px}
    .green{color:#16a34a} .red{color:#dc2626} .blue{color:#2563eb}
    .section{margin-top:28px} h2{font-size:15px;color:#444;border-bottom:2px solid #f97316;padding-bottom:6px}
    table{width:100%;border-collapse:collapse;margin-top:8px;font-size:13px}
    th{text-align:left;padding:8px;background:#f5f5f5;font-size:11px;text-transform:uppercase}
    td{padding:8px;border-bottom:1px solid #eee}
    .footer{margin-top:40px;font-size:11px;color:#999;text-align:center}
  </style></head><body>
  <h1>📑 Raport Financiar — ${subj.emri}</h1>
  <div class="sub">Periudha: ${bilPeriod==='vit'?'Viti '+year:'Muaji '+year} &nbsp;|&nbsp; Gjeneruar: ${new Date().toLocaleString('sq-AL')}</div>
  <div class="section"><h2>PASQYRA E TË ARDHURAVE</h2>
    <div class="row"><span>Të Ardhura nga Shitjet</span><span class="green">${fmt(ardhura)}</span></div>
    <div class="row"><span>Kosto Blerje Mallrash</span><span class="red">- ${fmt(blerjet.reduce((s,x)=>s+x.total,0))}</span></div>
    <div class="row"><span>Shpenzime Operative</span><span class="red">- ${fmt(shpenzime.reduce((s,x)=>s+x.vlera,0))}</span></div>
    <div class="row total"><span>FITIMI PARA TATIMIT</span><span class="${fitim>=0?'green':'red'}">${fmt(fitim)}</span></div>
    <div class="row"><span>Tatim Fitimi (${(norme*100).toFixed(0)}%)</span><span class="red">- ${fmt(tatim)}</span></div>
    <div class="row total"><span>FITIMI NETO</span><span class="${(fitim-tatim)>=0?'green':'red'}">${fmt(fitim-tatim)}</span></div>
  </div>
  <div class="section"><h2>SHPENZIME OPERATIVE</h2>
  <table><thead><tr><th>Data</th><th>Përshkrimi</th><th>Kategoria</th><th>Vlera</th></tr></thead><tbody>
  ${shpenzime.map(s=>`<tr><td>${s.data}</td><td>${s.pershkrimi}</td><td>${s.kategoria}</td><td>${fmt(s.vlera)}</td></tr>`).join('')}
  </tbody></table></div>
  <div class="footer">BuildTrack — Raport i gjeneruar automatikisht • ${new Date().toLocaleDateString('sq-AL')}</div>
  </body></html>`;

  const blob = new Blob([html],{type:'text/html'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = `raport_financiar_${subj.emri.replace(/\s/g,'_')}_${year}.html`;
  a.click();
  showToast('Raporti u shkarkua!','📄');
}

// ═══════════════════════════════════════════════
// PAGA & HR
// ═══════════════════════════════════════════════
let hrView = 'punonjes';

function setHrView(v, el){
  hrView = v;
  document.querySelectorAll('#panel-hr .tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  // show/hide sub-views
  document.getElementById('hr-view-punonjes').style.display  = v==='punonjes'?'':'none';
  document.getElementById('hr-view-paga').style.display      = v==='paga'?'':'none';
  document.getElementById('hr-view-shpenzime').style.display = v==='shpenzime'?'':'none';
  // change add button label
  const labels={punonjes:'＋ Shto Punonjës',paga:'＋ Regjistro Pagë',shpenzime:'＋ Shto Shpenzim'};
  document.getElementById('hr-btn-add').textContent = labels[v];
  renderHR();
}

function initHRYears(){
  const sel = document.getElementById('hr-year');
  if(!sel) return;
  const all = [
    ...(state.pagat||[]).map(p=>p.muaji?.slice(0,4)),
    ...(state.shpenzime||[]).map(s=>s.data?.slice(0,4)),
  ].filter(Boolean);
  const years = [...new Set(all)].sort().reverse();
  if(!years.length) years.push(new Date().getFullYear().toString());
  const cur = sel.value||years[0];
  sel.innerHTML = years.map(y=>`<option value="${y}" ${y===cur?'selected':''}>${y}</option>`).join('');
}

function getHRFilter(){
  const y = document.getElementById('hr-year')?.value||'2025';
  const m = document.getElementById('hr-month')?.value||'all';
  return {year:y, month:m};
}

function calcPaga(bruto){
  const KONTRIBUTE_PUNEDH = 0.167;
  const KONTRIBUTE_PUNET  = 0.114;
  const TATIM_MIN = 40000; // prag tatimi
  const kontPunedh = bruto * KONTRIBUTE_PUNEDH;
  const kontPunet  = bruto * KONTRIBUTE_PUNET;
  const bazaTatimit = Math.max(0, bruto - kontPunet - TATIM_MIN);
  const tatim = bazaTatimit > 0 ? bazaTatimit * 0.13 : 0;
  const neto  = bruto - kontPunet - tatim;
  return {kontPunedh, kontPunet, tatim, neto, kostoTotale: bruto + kontPunedh};
}

function renderHR(){
  if(!document.getElementById('hr-total-pun')) return;
  if(!state.punonjesit) state.punonjesit = [];
  if(!state.pagat) state.pagat = [];

  initHRYears();
  const {year, month} = getHRFilter();

  const aktiv = state.punonjesit.filter(p=>p.status==='Aktiv');
  const pagaKuMuajit = aktiv.reduce((s,p)=>{
    const c = calcPaga(p.pagaBruto||0);
    return s + c.kostoTotale;
  }, 0);
  const kontributeTotal = aktiv.reduce((s,p)=>s+calcPaga(p.pagaBruto||0).kontPunedh,0);

  // Filter pagat
  const pagat = (state.pagat||[]).filter(p=>{
    if(!p.muaji) return false;
    if(month!=='all') return p.muaji===year+'-'+month;
    return p.muaji.startsWith(year);
  });

  // Filter shpenzime
  const shpenzime = (state.shpenzime||[]).filter(s=>{
    if(!s.data) return false;
    if(month!=='all') return s.data.startsWith(year+'-'+month);
    return s.data.startsWith(year);
  });
  const totShp = shpenzime.reduce((s,x)=>s+x.vlera,0);

  document.getElementById('hr-total-pun').textContent = aktiv.length;
  document.getElementById('hr-total-paga').textContent = fmt(pagaKuMuajit);
  document.getElementById('hr-kontribute').textContent = fmt(kontributeTotal);
  document.getElementById('hr-shp-tjera').textContent = fmt(totShp);

  // PUNONJËSIT TABLE
  document.getElementById('hr-pun-tbody').innerHTML = state.punonjesit.map((p,i)=>{
    const c = calcPaga(p.pagaBruto||0);
    return `<tr>
      <td class="mono">${i+1}</td>
      <td><strong>${p.emri}</strong></td>
      <td>${p.pozicioni}</td>
      <td class="mono">${p.fillimi||'—'}</td>
      <td class="mono">${fmt(p.pagaBruto)}</td>
      <td class="mono" style="color:var(--yellow)">${fmt(c.kontPunedh)}</td>
      <td class="mono" style="color:var(--green)">${fmt(c.neto)}</td>
      <td>${p.status==='Aktiv'?'<span class="badge badge-green">Aktiv</span>':'<span class="badge badge-red">Joaktiv</span>'}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="editHRItem('pun',${p.id})">✏️</button>
        <button class="action-btn del" onclick="deleteHRItem('pun',${p.id})">🗑️</button>
      </td>
    </tr>`;
  }).join('') || `<tr><td colspan="9" style="text-align:center;padding:32px;color:var(--muted)">Nuk ka punonjës</td></tr>`;

  // PAGAT TABLE
  document.getElementById('hr-paga-tbody').innerHTML = pagat.map((p,i)=>{
    const pun = state.punonjesit.find(x=>x.id===p.punonjesiId);
    const c = calcPaga(p.pagaBruto||0);
    return `<tr>
      <td class="mono">${i+1}</td>
      <td class="mono">${p.muaji}</td>
      <td><strong>${pun?pun.emri:'—'}</strong></td>
      <td class="mono">${fmt(p.pagaBruto)}</td>
      <td class="mono" style="color:var(--red)">${fmt(c.tatim)}</td>
      <td class="mono" style="color:var(--yellow)">${fmt(c.kontPunedh+c.kontPunet)}</td>
      <td class="mono" style="color:var(--green)">${fmt(c.neto)}</td>
      <td>${p.status==='Paguar'?'<span class="badge badge-green">Paguar</span>':'<span class="badge badge-yellow">Pending</span>'}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="togglePagaStatus(${p.id})">✅</button>
        <button class="action-btn del" onclick="deleteHRItem('pag',${p.id})">🗑️</button>
      </td>
    </tr>`;
  }).join('') || `<tr><td colspan="9" style="text-align:center;padding:32px;color:var(--muted)">Nuk ka pagesa të regjistruara</td></tr>`;

  // SHPENZIME TABLE
  const TVSH=0.20;
  document.getElementById('hr-shp-tbody').innerHTML = shpenzime.map((s,i)=>{
    const tvshAmt = s.tvsh?(s.vlera*TVSH):0;
    return `<tr>
      <td class="mono">${i+1}</td>
      <td class="mono">${s.data}</td>
      <td><strong>${s.pershkrimi}</strong></td>
      <td><span class="badge badge-blue">${s.kategoria}</span></td>
      <td class="mono">${fmt(s.vlera)}</td>
      <td class="mono" style="color:var(--yellow)">${s.tvsh?fmt(tvshAmt):'—'}</td>
      <td class="mono" style="color:var(--red)">${fmt(s.vlera+tvshAmt)}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="editItem('shp',${s.id})">✏️</button>
        <button class="action-btn del" onclick="deleteItem('shp',${s.id})">🗑️</button>
      </td>
    </tr>`;
  }).join('') || `<tr><td colspan="8" style="text-align:center;padding:32px;color:var(--muted)">Nuk ka shpenzime</td></tr>`;
}

function togglePagaStatus(id){
  const p = state.pagat.find(x=>x.id===id);
  if(!p) return;
  p.status = p.status==='Paguar'?'Pending':'Paguar';
  getCurrentSubj().data = state; saveSubjects(); renderHR();
}

function deleteHRItem(type, id){
  if(!confirm('Fshi këtë rekord?')) return;
  if(type==='pun') state.punonjesit = state.punonjesit.filter(x=>x.id!==id);
  else if(type==='pag') state.pagat = state.pagat.filter(x=>x.id!==id);
  getCurrentSubj().data = state; saveSubjects(); renderHR();
}

function editHRItem(type, id){
  openHRModal(type, id);
}

// HR MODAL
function openHRModal(type, id){
  const view = type||hrView;
  editingId = id||null;
  let title, body;

  if(view==='punonjes'||view==='pun'){
    const item = id ? state.punonjesit.find(x=>x.id===id) : {};
    title = id?'✏️ Modifiko Punonjës':'➕ Shto Punonjës të Ri';
    body=`<div class="form-grid">
      <div class="field form-grid full"><label>Emri & Mbiemri</label><input id="f-emri" value="${item.emri||''}" placeholder="Artan Hoxha..."></div>
      <div class="field"><label>Pozicioni</label><input id="f-poz" value="${item.pozicioni||''}" placeholder="Inxhinier, Punëtor..."></div>
      <div class="field"><label>Data Fillimit</label><input id="f-fil" type="date" value="${item.fillimi||''}"></div>
      <div class="field"><label>Paga Bruto (L/muaj)</label><input id="f-paga" type="number" value="${item.pagaBruto||0}"></div>
      <div class="field"><label>Statusi</label><select id="f-sts">
        <option ${item.status==='Aktiv'?'selected':''}>Aktiv</option>
        <option ${item.status==='Joaktiv'?'selected':''}>Joaktiv</option>
      </select></div>
    </div>`;
    document._saveType='pun';

  } else if(view==='paga'||view==='pag'){
    title = '➕ Regjistro Pagë Mujore';
    const muajAktual = new Date().toISOString().slice(0,7);
    body=`<div class="form-grid">
      <div class="field"><label>Muaji</label><input id="f-muaj" type="month" value="${muajAktual}"></div>
      <div class="field"><label>Punonjësi</label><select id="f-pun">
        ${state.punonjesit.filter(p=>p.status==='Aktiv').map(p=>`<option value="${p.id}">${p.emri} — ${fmt(p.pagaBruto)}</option>`).join('')}
      </select></div>
      <div class="field form-grid full"><label>Paga Bruto (L) — mund të ndryshohet</label><input id="f-paga" type="number" value="0" oninput="updatePagaCalc()"></div>
      <div class="field form-grid full" id="paga-calc-box" style="background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:12px;font-size:0.78rem;color:var(--muted)">
        Zgjidh punonjësin për të parë llogaritjen...
      </div>
      <div class="field"><label>Statusi</label><select id="f-sts"><option>Paguar</option><option>Pending</option></select></div>
    </div>`;
    document._saveType='pag';
    setTimeout(()=>{
      const sel=document.getElementById('f-pun');
      if(sel){
        const pun=state.punonjesit.find(p=>p.id==sel.value);
        if(pun){document.getElementById('f-paga').value=pun.pagaBruto; updatePagaCalc();}
        sel.onchange=()=>{
          const p2=state.punonjesit.find(x=>x.id==sel.value);
          if(p2){document.getElementById('f-paga').value=p2.pagaBruto; updatePagaCalc();}
        };
      }
    },50);

  } else if(view==='shpenzime'){
    // reuse existing shpenzim modal logic
    currentPanel='bilanci';
    openModal('shpenzim');
    return;
  }

  document.getElementById('modal-title').textContent = title;
  document.getElementById('modal-body').innerHTML = body;
  document.getElementById('modal-overlay').classList.add('open');
}

function updatePagaCalc(){
  const bruto = parseFloat(document.getElementById('f-paga')?.value)||0;
  const c = calcPaga(bruto);
  const box = document.getElementById('paga-calc-box');
  if(!box) return;
  box.innerHTML=`
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:6px;font-size:0.78rem">
      <div>Paga Bruto: <strong style="color:var(--text)">${fmt(bruto)}</strong></div>
      <div>Kontribute Punëtor (11.4%): <strong style="color:var(--yellow)">- ${fmt(c.kontPunet)}</strong></div>
      <div>Tatim Mbi të Ardhura (13%): <strong style="color:var(--red)">- ${fmt(c.tatim)}</strong></div>
      <div>Kontribute Punëdhënës (16.7%): <strong style="color:var(--orange)">+ ${fmt(c.kontPunedh)}</strong></div>
      <div style="grid-column:1/-1;border-top:1px solid var(--border);padding-top:6px;margin-top:2px">
        Paga Neto (merr punëtori): <strong style="color:var(--green)">${fmt(c.neto)}</strong> &nbsp;|&nbsp;
        Kosto Totale Firmës: <strong style="color:var(--red)">${fmt(c.kostoTotale)}</strong>
      </div>
    </div>`;
}

// ═══════════════════════════════════════════════
// LIDHJA SHITJE ↔ INVENTAR
// ═══════════════════════════════════════════════
function onLlojiChange(){
  const lloji = document.getElementById('f-llj')?.value;
  const sel = document.getElementById('f-art-sel');
  if(!sel) return;
  onArtikullChange();
  updateShitjeModalActions();
}

function updateShitjeModalActions(){
  if(document._saveType !== 'sh') return;
  const lloji = document.getElementById('f-llj')?.value;
  const actEl = document.getElementById('modal-actions');
  if(!actEl) return;
  if(lloji === 'Shitje'){
    actEl.innerHTML = '<button class="btn btn-ghost" onclick="closeModal()">Anulo</button>' +
      '<button class="btn btn-primary" onclick="saveItem()" style="background:var(--green);border-color:var(--green)">\u{1F4B0} Ruaj Shitjen</button>' +
      '<button class="btn btn-primary" onclick="saveItemAndCreateFature()" style="background:#3b82f6;border-color:#3b82f6">\u{1F9FE} Ruaj + Krijo Fatur\u00EB</button>';
  } else {
    actEl.innerHTML = '<button class="btn btn-ghost" onclick="closeModal()">Anulo</button>' +
      '<button class="btn btn-primary" onclick="saveItem()">\u{1F4BE} Ruaj Blerjen</button>';
  }
}

function saveItemAndCreateFature(){
  if(document._saveType !== 'sh') return;
  const dat = document.getElementById('f-dat')?.value || '';
  const sas = parseFloat(document.getElementById('f-sas')?.value)||0;
  const cm  = parseFloat(document.getElementById('f-cmu')?.value)||0;
  const kli = document.getElementById('f-kli')?.value || '';
  const artSel = document.getElementById('f-art-sel');
  let artikullEmri = document.getElementById('f-art')?.value || '';
  if(artSel && artSel.value){
    const opt = artSel.options[artSel.selectedIndex];
    artikullEmri = opt.text.split(' [')[0];
    const stokAv = parseFloat(opt.dataset.sasia)||0;
    if(sas > stokAv){ showToast('Stok i pamjaftueshëm! Keni vetëm '+stokAv+' në stok.','⛔'); return; }
  }
  saveItem();
  setTimeout(function(){
    const fatBtn = Array.from(document.querySelectorAll('.nav-item')).find(function(b){ return b.getAttribute('onclick') && b.getAttribute('onclick').includes("'faturat'"); });
    if(fatBtn) showPanel('faturat', fatBtn);
    setTimeout(function(){
      openFatModal(null);
      setTimeout(function(){
        const nrNew = 'FAT-'+new Date().getFullYear()+'-'+String((state.faturat||[]).length).padStart(3,'0');
        const ska = new Date(dat); ska.setDate(ska.getDate()+30);
        const nrEl=document.getElementById('f-nr');
        const datEl=document.getElementById('f-dat');
        const kliEl=document.getElementById('f-kli');
        const skaEl=document.getElementById('f-ska');
        const perEl=document.getElementById('fz-per-0');
        const sasEl=document.getElementById('fz-sas-0');
        const cmuEl=document.getElementById('fz-cmu-0');
        if(nrEl)  nrEl.value  = nrNew;
        if(datEl) datEl.value = dat;
        if(kliEl) kliEl.value = kli;
        if(skaEl) skaEl.value = ska.toISOString().split('T')[0];
        if(perEl) perEl.value = artikullEmri;
        if(sasEl) sasEl.value = sas;
        if(cmuEl) cmuEl.value = cm;
        if(typeof updateFatTotalPreview === 'function') updateFatTotalPreview();
        showToast('Fatura u hap e plotësuar automatikisht!','🧾');
      }, 200);
    }, 300);
  }, 200);
}

function onArtikullChange(){
  const sel = document.getElementById('f-art-sel');
  if(!sel) return;
  const opt = sel.options[sel.selectedIndex];
  const lloji = document.getElementById('f-llj')?.value;
  const alertBox = document.getElementById('stok-alert-box');
  const availEl = document.getElementById('stok-available');
  const cmuEl = document.getElementById('f-cmu');

  if(!opt.value){
    if(alertBox) alertBox.style.display='none';
    if(availEl) availEl.textContent='';
    return;
  }

  const cmShitje = parseFloat(opt.dataset.cmShitje)||0;
  const cmBlerje = parseFloat(opt.dataset.cmBlerje)||0;
  const sasia = parseFloat(opt.dataset.sasia)||0;
  const njesia = opt.dataset.njesia||'';
  const status = opt.dataset.status||'';

  // Vendos çmimin automatik
  if(lloji==='Shitje') cmuEl.value = cmShitje;
  else cmuEl.value = cmBlerje;

  // Trego stokun e disponueshëm
  if(availEl) availEl.textContent = `Disponueshëm: ${sasia} ${njesia}`;

  // Alert nëse stok kritik ose i ulët
  if(alertBox){
    if(status==='Stok Kritik'){
      alertBox.style.display='block';
      alertBox.innerHTML='⛔ <strong>STOK KRITIK!</strong> Ky material ka stok shumë të ulët. Konsideroni blerje para shitjes.';
      alertBox.style.color='var(--red)';
      alertBox.style.borderColor='rgba(239,68,68,0.3)';
    } else if(status==='Stok i Ulët'){
      alertBox.style.display='block';
      alertBox.innerHTML='⚠️ <strong>Stok i Ulët!</strong> Ky material është nën nivelin minimal të rekomanduar.';
      alertBox.style.color='var(--yellow)';
      alertBox.style.borderColor='rgba(234,179,8,0.3)';
      alertBox.style.background='rgba(234,179,8,0.08)';
    } else {
      alertBox.style.display='none';
    }
  }

  onSasiaChange();
}

function onSasiaChange(){
  const sel = document.getElementById('f-art-sel');
  const sasiaEl = document.getElementById('f-sas');
  const cmuEl = document.getElementById('f-cmu');
  const previewBox = document.getElementById('total-preview-box');
  const lloji = document.getElementById('f-llj')?.value;
  if(!sel||!sasiaEl||!previewBox) return;

  const opt = sel.options[sel.selectedIndex];
  if(!opt.value){ previewBox.innerHTML='Zgjidh artikullin dhe sasinë...'; return; }

  const sasia = parseFloat(sasiaEl.value)||0;
  const sasiaNëStok = parseFloat(opt.dataset.sasia)||0;
  const cmUnit = parseFloat(cmuEl?.value)||0;
  const total = sasia * cmUnit;
  const njesia = opt.dataset.njesia||'';
  const alertBox = document.getElementById('stok-alert-box');

  // Nëse shitje dhe sasia > stok → blloko
  if(lloji==='Shitje' && sasia > sasiaNëStok){
    if(alertBox){
      alertBox.style.display='block';
      alertBox.innerHTML=`⛔ <strong>STOK I PAMJAFTUESHËM!</strong> Keni vetëm <strong>${sasiaNëStok} ${njesia}</strong> në stok, por po tentoni të shisni <strong>${sasia} ${njesia}</strong>.`;
      alertBox.style.color='var(--red)';
      alertBox.style.background='rgba(239,68,68,0.1)';
      alertBox.style.borderColor='rgba(239,68,68,0.3)';
    }
    previewBox.innerHTML=`<span style="color:var(--red)">⛔ Nuk mund të realizohet shitja — stok i pamjaftueshëm!</span>`;
    return;
  }

  // Preview normal
  const cmBlerje = parseFloat(opt.dataset.cmBlerje)||0;
  let marginHtml = '';
  if(lloji==='Shitje' && cmBlerje>0 && cmUnit>0){
    const margin = ((cmUnit-cmBlerje)/cmUnit*100).toFixed(1);
    const fitim = (cmUnit-cmBlerje)*sasia;
    marginHtml = `&nbsp;|&nbsp; Marzhi: <strong style="color:var(--green)">${margin}%</strong> &nbsp;|&nbsp; Fitim: <strong style="color:var(--green)">${fmt(fitim)}</strong>`;
  }

  previewBox.innerHTML=`📊 Total: <strong style="color:var(--text)">${fmt(total)}</strong> &nbsp;|&nbsp; ${sasia} × ${fmt(cmUnit)}${marginHtml}`;
}

// ── SAVE ITEM: ALL TYPES UNIFIED ──
function saveItem(){
  const t=document._saveType;
  // ── HR types ──
  if(t==='pun'){
    const item={emri:g('f-emri'),pozicioni:g('f-poz'),fillimi:g('f-fil'),pagaBruto:parseFloat(g('f-paga'))||0,status:g('f-sts')};
    if(editingId){const i=state.punonjesit.findIndex(x=>x.id===editingId);item.id=editingId;state.punonjesit[i]=item;}
    else{item.id=Date.now();state.punonjesit.push(item);}
    closeModal(); getCurrentSubj().data=state; saveSubjects(); renderHR(); return;
  }
  if(t==='pag'){
    const punId=parseInt(document.getElementById('f-pun')?.value)||0;
    const muaji=g('f-muaj'), bruto=parseFloat(g('f-paga'))||0;
    state.pagat.push({id:Date.now(),muaji,punonjesiId:punId,pagaBruto:bruto,status:g('f-sts')});
    closeModal(); getCurrentSubj().data=state; saveSubjects(); renderHR(); renderBilanci(); return;
  }
  // ── Projektet ──
  if(t==='proj'){
    const fazatRaw=(document.getElementById('f-fazat')?.value||'').split('\n').map(s=>s.trim()).filter(Boolean);
    const fazat=fazatRaw.map(emri=>({emri,done:false}));
    if(editingId){
      const old=state.projektet.find(x=>x.id===editingId);
      if(old&&old.fazat) fazat.forEach((f,i)=>{const match=old.fazat.find(of=>of.emri===f.emri);if(match)fazat[i].done=match.done;});
    }
    const item={emri:g('f-emri'),klienti:g('f-kli'),nipt_klienti:g('f-nipt')||'',fillimi:g('f-fil'),afati:g('f-afa'),buxheti:parseFloat(g('f-bux'))||0,statusi:g('f-sts'),adresa:g('f-adr')||'',pershkrimi:g('f-per')||'',fazat};
    if(editingId){const i=state.projektet.findIndex(x=>x.id===editingId);item.id=editingId;state.projektet[i]=item;}
    else{item.id=Date.now();state.projektet.push(item);}
    closeModal(); getCurrentSubj().data=state; saveSubjects(); renderProjektet();
    showToast(`Projekti "${item.emri}" u ruajt!`,'📋'); return;
  }
  // ── Faturat ──
  if(t==='fat'){
    const zerat=getFatZerat();
    const item={nr:g('f-nr'),data:g('f-dat'),klienti:g('f-kli'),nipt:g('f-nipt')||'',projekti:document.getElementById('f-proj')?.value||'',skadon:g('f-ska')||'',statusi:g('f-sts'),shenime:g('f-she')||'',zerat};
    if(editingId){const i=state.faturat.findIndex(x=>x.id===editingId);item.id=editingId;state.faturat[i]=item;}
    else{item.id=Date.now();state.faturat.push(item);}
    closeModal(); getCurrentSubj().data=state; saveSubjects(); renderFaturat();
    showToast(`Fatura ${item.nr} u ruajt!`,'🧾'); return;
  }
  // ── Ofertat ──
  if(t==='ofe'){
    const item={nr:g('f-nr'),data:g('f-dat'),klienti:g('f-kli'),sherbimi:g('f-she'),vlera:parseFloat(g('f-vlr'))||0,vlefshmeria:g('f-vlf')||'',statusi:g('f-sts')};
    if(editingId){const i=state.ofertat.findIndex(x=>x.id===editingId);item.id=editingId;state.ofertat[i]=item;}
    else{item.id=Date.now();state.ofertat.push(item);}
    closeModal(); getCurrentSubj().data=state; saveSubjects(); renderFaturat();
    showToast(`Oferta ${item.nr} u ruajt!`,'📄'); return;
  }
  // ── Core types: mat, paj, sh, fur, shp ──
  const sas=parseFloat(g('f-sas'))||0, min=parseFloat(g('f-min'))||0;
  if(t==='mat'){
    const status=sas===0?'Stok Kritik':sas<min?'Stok Kritik':sas<min*1.5?'Stok i Ulët':'Stok Normal';
    const item={emri:g('f-emri'),kategori:g('f-kat'),njesia:g('f-nje'),sasia:sas,min,cmBlerje:parseFloat(g('f-cmb'))||0,cmShitje:parseFloat(g('f-cms'))||0,furnitori:g('f-fur'),status};
    if(editingId){const i=state.materiale.findIndex(m=>m.id===editingId);item.id=editingId;state.materiale[i]=item;}
    else{item.id=Date.now();state.materiale.push(item);}
  } else if(t==='paj'){
    const item={emri:g('f-emri'),kategori:g('f-kat'),seria:g('f-ser'),gjendja:g('f-gje'),vlera:parseFloat(g('f-vlr'))||0,mirembajtja:g('f-mir')||'—',lokacioni:g('f-lok'),status:g('f-sts')};
    if(editingId){const i=state.pajisje.findIndex(p=>p.id===editingId);item.id=editingId;state.pajisje[i]=item;}
    else{item.id=Date.now();state.pajisje.push(item);}
  } else if(t==='sh'){
    const cm=parseFloat(g('f-cmu'))||0, lloji=g('f-llj');
    const artSel=document.getElementById('f-art-sel');
    let artikullEmri='', matId=null;
    if(artSel&&artSel.value){
      matId=parseInt(artSel.value);
      const opt=artSel.options[artSel.selectedIndex];
      artikullEmri=opt.text.split(' [')[0];
      const sasiaNëStok=parseFloat(opt.dataset.sasia)||0;
      if(lloji==='Shitje'&&sas>sasiaNëStok){showToast(`⛔ Stok i pamjaftueshëm! Keni vetëm ${sasiaNëStok} në stok.`,'⛔');return;}
      const mat=state.materiale.find(m=>m.id===matId);
      if(mat){
        if(lloji==='Shitje') mat.sasia=Math.max(0,mat.sasia-sas);
        else if(lloji==='Blerje') mat.sasia=mat.sasia+sas;
        mat.status=mat.sasia===0?'Stok Kritik':mat.sasia<mat.min?'Stok Kritik':mat.sasia<mat.min*1.5?'Stok i Ulët':'Stok Normal';
        if(lloji==='Blerje'){
          if(!state.shpenzime) state.shpenzime=[];
          state.shpenzime.push({id:Date.now()+1,pershkrimi:'Blerje: '+artikullEmri,kategoria:'Blerje Mallrash',data:g('f-dat'),vlera:sas*cm,tvsh:false});
          showToast(`📦 "${artikullEmri}" u shtua në inventar (+${sas}) dhe u regjistrua në Bilanci!`,'✅');
        } else {
          showToast(`💰 Shitje regjistruar! Stoku i "${artikullEmri}" u ul me ${sas}.`,'✅');
        }
        if(mat.status!=='Stok Normal') setTimeout(()=>showToast(`⚠️ "${mat.emri}" ka rënë nën stokun minimal (${mat.sasia}/${mat.min})!`,'⚠️'),1200);
      }
    } else { artikullEmri=g('f-art'); }
    state.shitje.push({id:Date.now(),data:g('f-dat'),artikull:artikullEmri||g('f-art'),lloji,sasia:sas,cmUnit:cm,total:sas*cm,klienti:g('f-kli'),matId});
  } else if(t==='fur'){
    const item={emri:g('f-emri'),nid:g('f-nid'),kontakti:g('f-kon'),adresa:g('f-adr'),materialet:g('f-mat'),afati:g('f-afa'),status:'Aktiv'};
    if(editingId){const i=state.furnitoret.findIndex(f=>f.id===editingId);item.id=editingId;state.furnitoret[i]=item;}
    else{item.id=Date.now();state.furnitoret.push(item);}
  } else if(t==='shp'){
    const vlera=parseFloat(g('f-vlr'))||0, tvsh=g('f-tvsh')==='true';
    const item={pershkrimi:g('f-emri'),kategoria:g('f-kat'),data:g('f-dat'),vlera,tvsh};
    if(editingId){const i=state.shpenzime.findIndex(s=>s.id===editingId);item.id=editingId;state.shpenzime[i]=item;}
    else{item.id=Date.now();state.shpenzime.push(item);}
  }
  closeModal();
  getCurrentSubj().data=state; saveSubjects(); render();
}

// ═══════════════════════════════════════════════
// TOAST
// ═══════════════════════════════════════════════
function showToast(msg, icon='✅'){
  const old = document.getElementById('toast-el');
  if(old) old.remove();
  const t = document.createElement('div');
  t.id='toast-el';
  t.className='toast';
  t.innerHTML=`<span>${icon}</span><span>${msg}</span>`;
  document.body.appendChild(t);
  setTimeout(()=>{t.style.opacity='0';t.style.transition='opacity 0.4s';setTimeout(()=>t.remove(),400);},2800);
}

// ═══════════════════════════════════════════════
// BACKUP & RESTORE
// ═══════════════════════════════════════════════

// saveSubjects me indicator është tashmë e definuar më sipër

// saveSubjects me indicator është tashmë e definuar më sipër

// Export ALL subjects as JSON file
function exportBackup(){
  const now = new Date();
  const dateStr = now.toISOString().split('T')[0];
  const timeStr = now.toTimeString().slice(0,5).replace(':','-');
  const payload = {
    version: 1,
    exported: now.toISOString(),
    app: 'BuildTrack',
    subjects: subjects
  };
  const blob = new Blob([JSON.stringify(payload, null, 2)], {type:'application/json'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = `buildtrack_backup_${dateStr}_${timeStr}.json`;
  a.click();
  showToast('Backup u shkarkua me sukses! 🎉','📤');
}

// Export only current subject
function exportCurrentSubject(){
  const subj = getCurrentSubj();
  const now = new Date();
  const dateStr = now.toISOString().split('T')[0];
  const safeName = subj.emri.replace(/[^a-zA-Z0-9_]/g,'_');
  const payload = {
    version: 1,
    exported: now.toISOString(),
    app: 'BuildTrack',
    single_subject: true,
    subject: subj
  };
  const blob = new Blob([JSON.stringify(payload, null, 2)], {type:'application/json'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = `buildtrack_${safeName}_${dateStr}.json`;
  a.click();
  showToast(`"${subj.emri}" u shkarkua!`,'📋');
}

// Import backup from file
function importBackup(event){
  const file = event.target.files[0];
  if(!file) return;
  const reader = new FileReader();
  reader.onload = function(e){
    try{
      const payload = JSON.parse(e.target.result);
      if(payload.app !== 'BuildTrack') throw new Error('Jo file BuildTrack');

      if(payload.single_subject){
        // Import single subject
        const incoming = payload.subject;
        const exists = subjects.find(s=>s.id===incoming.id);
        if(exists){
          if(!confirm(`Subjekti "${incoming.emri}" ekziston. E zëvendësojmë?`)) return;
          const idx = subjects.findIndex(s=>s.id===incoming.id);
          subjects[idx] = incoming;
        } else {
          if(subjects.length>=4){alert('Maksimumi 4 subjekte! Fshi njërin para importit.');return;}
          subjects.push(incoming);
        }
        showToast(`"${incoming.emri}" u importua!`,'📥');
      } else {
        // Import all
        if(!confirm(`Do të zëvendësohen TË GJITHA ${payload.subjects.length} subjektet. Vazhdo?`)) return;
        subjects = payload.subjects;
        currentSubjId = subjects[0].id;
        saveCurrentSubjId(currentSubjId);
        state = getCurrentSubj().data;
        showToast(`${subjects.length} subjekte u importuan!`,'📥');
      }

      saveSubjects();
      renderSubjectList();
      updateSubjTopbar();
      render();
    } catch(err){
      alert('Gabim: File i pavlefshëm ose i dëmtuar!\n'+err.message);
    }
    // reset input
    event.target.value='';
  };
  reader.readAsText(file);
}

// ═══════════════════════════════════════════════
// PROJEKTET & KONTRATAT
// ═══════════════════════════════════════════════
let projFilter = 'all';
let projSearch = '';
let fatView = 'faturat';

function filterProj(f, el){
  projFilter = f;
  document.querySelectorAll('#proj-filter-tabs .tab').forEach(t=>t.classList.remove('active'));
  if(el) el.classList.add('active');
  renderProjektet();
}
function searchProj(q){ projSearch = q.toLowerCase(); renderProjektet(); }

function renderProjektet(){
  if(!document.getElementById('proj-grid')) return;
  if(!state.projektet) state.projektet = [];
  // auto-update vonuar status
  const sot = new Date().toISOString().split('T')[0];
  state.projektet.forEach(p=>{
    if(p.statusi==='Aktiv' && p.afati < sot) p.statusi='Vonuar';
  });

  const aktive = state.projektet.filter(p=>p.statusi==='Aktiv').length;
  const perf   = state.projektet.filter(p=>p.statusi==='Përfunduar').length;
  const vonuar = state.projektet.filter(p=>p.statusi==='Vonuar').length;
  const vlera  = state.projektet.reduce((s,p)=>s+(p.buxheti||0),0);
  document.getElementById('prj-aktive').textContent = aktive;
  document.getElementById('prj-perfunduar').textContent = perf;
  document.getElementById('prj-vonuara').textContent = vonuar;
  document.getElementById('prj-vlera').textContent = fmt(vlera);

  let list = [...state.projektet];
  if(projFilter!=='all') list = list.filter(p=>p.statusi===projFilter);
  if(projSearch) list = list.filter(p=>(p.emri+p.klienti).toLowerCase().includes(projSearch));

  // Badge
  const badgePrj = document.getElementById('badge-proj');
  if(badgePrj){ if(vonuar>0){badgePrj.style.display='';badgePrj.textContent=vonuar;}else badgePrj.style.display='none'; }

  // CARDS
  document.getElementById('proj-grid').innerHTML = list.map((p,i)=>{
    const cls = p.statusi==='Aktiv'?'aktiv':p.statusi==='Përfunduar'?'perfunduar':p.statusi==='Vonuar'?'vonuar':'pauzuar';
    const fazatDone = (p.fazat||[]).filter(f=>f.done).length;
    const fazatTotal = (p.fazat||[]).length;
    const progPct = fazatTotal>0 ? Math.round(fazatDone/fazatTotal*100) : (p.realizuar||0);
    const progColor = progPct>=80?'var(--green)':progPct>=40?'var(--yellow)':'var(--orange)';
    const diteLeft = p.afati ? Math.ceil((new Date(p.afati)-new Date())/(1000*60*60*24)) : null;
    const diteHtml = diteLeft!==null ? (diteLeft<0?`<span style="color:var(--red)">⚠️ ${Math.abs(diteLeft)} ditë vonesë</span>`:`<span style="color:${diteLeft<14?'var(--yellow)':'var(--muted)'}">${diteLeft} ditë mbetur</span>`) : '';
    return `<div class="proj-card ${cls}" style="animation-delay:${i*0.05}s">
      <div class="proj-card-header">
        <div>
          <div class="proj-name">${p.emri}</div>
          <div class="proj-klienti">👤 ${p.klienti}</div>
        </div>
        ${projStatusBadge(p.statusi)}
      </div>
      <div class="proj-meta-row"><span class="lbl">📅 Afati:</span><span class="val">${p.afati||'—'}</span></div>
      <div class="proj-meta-row"><span class="lbl">💰 Buxheti:</span><span class="val" style="color:var(--orange)">${fmt(p.buxheti||0)}</span></div>
      <div class="proj-meta-row"><span class="lbl">📍 Adresa:</span><span class="val" style="font-family:'DM Sans',sans-serif;font-size:0.72rem">${p.adresa||'—'}</span></div>
      <div class="proj-meta-row" style="margin-top:4px"><span class="lbl">${diteHtml}</span></div>
      <div class="proj-prog-wrap">
        <div class="proj-prog-label"><span>Progresi</span><span style="color:${progColor};font-weight:700">${progPct}%</span></div>
        <div class="prog-track"><div class="prog-fill" style="width:${progPct}%;background:${progColor}"></div></div>
      </div>
      <div class="faza-list">
        ${(p.fazat||[]).map((f,fi)=>`
          <div class="faza-item">
            <div class="faza-check ${f.done?'done':''}" onclick="toggleFaza(${p.id},${fi})">${f.done?'✓':''}</div>
            <span class="faza-name ${f.done?'done':''}">${f.emri}</span>
          </div>`).join('')}
      </div>
      <div class="proj-actions">
        <button class="inv-btn inv-btn-add" onclick="openProjModal(${p.id})">✏️ Modifiko</button>
        <button class="inv-btn inv-btn-sell" onclick="openFaturaFromProj(${p.id})">🧾 Faturë</button>
        <button class="inv-btn inv-btn-edit" onclick="deleteProj(${p.id})">🗑️</button>
      </div>
    </div>`;
  }).join('') || `<div class="empty" style="grid-column:1/-1"><div class="empty-icon">📋</div>Nuk ka projekte. Shto projektin e parë!</div>`;

  // TABLE
  document.getElementById('proj-tbody').innerHTML = list.map((p,i)=>{
    const progPct = p.fazat ? Math.round(p.fazat.filter(f=>f.done).length/p.fazat.length*100)||0 : (p.realizuar||0);
    return `<tr>
      <td class="mono">${i+1}</td>
      <td><strong>${p.emri}</strong><div style="font-size:0.7rem;color:var(--muted)">${p.pershkrimi||''}</div></td>
      <td>${p.klienti}</td>
      <td class="mono">${p.fillimi||'—'}</td>
      <td class="mono" style="color:var(--yellow)">${p.afati||'—'}</td>
      <td class="mono" style="color:var(--orange)">${fmt(p.buxheti||0)}</td>
      <td class="mono">${progPct}%</td>
      <td style="min-width:100px"><div class="prog-track"><div class="prog-fill" style="width:${progPct}%;background:${progPct>=80?'var(--green)':progPct>=40?'var(--yellow)':'var(--orange)'}"></div></div></td>
      <td>${projStatusBadge(p.statusi)}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="openProjModal(${p.id})">✏️</button>
        <button class="action-btn del" onclick="deleteProj(${p.id})">🗑️</button>
      </td>
    </tr>`;
  }).join('') || `<tr><td colspan="10" style="text-align:center;padding:32px;color:var(--muted)">Nuk ka projekte</td></tr>`;
}

function projStatusBadge(s){
  const map={'Aktiv':'badge-orange','Vonuar':'badge-red','Përfunduar':'badge-green','Pauzuar':'badge-yellow'};
  return `<span class="badge ${map[s]||'badge-blue'}">${s}</span>`;
}

function toggleFaza(projId, fazaIdx){
  if(!state.projektet) return;
  const p = state.projektet.find(x=>x.id===projId);
  if(!p||!p.fazat) return;
  p.fazat[fazaIdx].done = !p.fazat[fazaIdx].done;
  // auto set perfunduar
  if(p.fazat.every(f=>f.done)) p.statusi='Përfunduar';
  else if(p.statusi==='Përfunduar') p.statusi='Aktiv';
  getCurrentSubj().data=state; saveSubjects(); renderProjektet();
}

function deleteProj(id){
  if(!confirm('Fshi projektin?')) return;
  state.projektet = state.projektet.filter(p=>p.id!==id);
  getCurrentSubj().data=state; saveSubjects(); renderProjektet();
}

function openFaturaFromProj(projId){
  const p = state.projektet.find(x=>x.id===projId);
  if(!p) return;
  showPanel('faturat', document.querySelectorAll('.nav-item')[9]);
  setTimeout(()=>openFatModal(null, p), 200);
}

// PROJEKT MODAL
function openProjModal(id){
  editingId = id||null;
  const p = id ? state.projektet.find(x=>x.id===id) : {};
  const fazatVal = p.fazat ? p.fazat.map(f=>f.emri).join('\n') : 'Themelet & Gërmimi\nSkelet Beton\nMuratura\nFasada & Çatia\nInstalime\nMbarimi i brendshëm';
  document.getElementById('modal-title').textContent = id?'✏️ Modifiko Projekt':'📋 Shto Projekt të Ri';
  document.getElementById('modal-body').innerHTML = `
    <div class="form-grid">
      <div class="field form-grid full"><label>Emri Projektit</label><input id="f-emri" value="${p.emri||''}" placeholder="p.sh. Pallati Rezidencial..."></div>
      <div class="field"><label>Klienti</label><input id="f-kli" value="${p.klienti||''}" placeholder="Emri i klientit..."></div>
      <div class="field"><label>NIPT Klienti</label><input id="f-nipt" value="${p.nipt_klienti||''}" placeholder="K12345678L"></div>
      <div class="field"><label>Data Fillimit</label><input id="f-fil" type="date" value="${p.fillimi||new Date().toISOString().split('T')[0]}"></div>
      <div class="field"><label>Afati i Dorëzimit</label><input id="f-afa" type="date" value="${p.afati||''}"></div>
      <div class="field"><label>Buxheti (L)</label><input id="f-bux" type="number" value="${p.buxheti||0}" placeholder="0"></div>
      <div class="field"><label>Statusi</label><select id="f-sts">
        <option ${(p.statusi||'Aktiv')==='Aktiv'?'selected':''}>Aktiv</option>
        <option ${p.statusi==='Vonuar'?'selected':''}>Vonuar</option>
        <option ${p.statusi==='Përfunduar'?'selected':''}>Përfunduar</option>
        <option ${p.statusi==='Pauzuar'?'selected':''}>Pauzuar</option>
      </select></div>
      <div class="field"><label>Adresa / Lokacioni</label><input id="f-adr" value="${p.adresa||''}" placeholder="Rruga, Qyteti..."></div>
      <div class="field form-grid full"><label>Përshkrim i Shkurtër</label><input id="f-per" value="${p.pershkrimi||''}" placeholder="Përshkruaj projektin..."></div>
      <div class="field form-grid full"><label>Fazat e Projektit (një fazë për rresht)</label><textarea id="f-fazat" rows="5" style="resize:vertical">${fazatVal}</textarea></div>
    </div>`;
  document._saveType='proj';
  document.getElementById('modal-overlay').classList.add('open');
}

// ═══════════════════════════════════════════════
// FATURAT & OFERTAT
// ═══════════════════════════════════════════════
function setFatView(v, el){
  fatView = v;
  document.querySelectorAll('#fat-view-faturat,#fat-view-ofertat').forEach(x=>x.style.display='none');
  document.getElementById('fat-view-'+v).style.display='';
  document.querySelectorAll('.tabs .tab').forEach(t=>t.classList.remove('active'));
  if(el) el.classList.add('active');
  renderFaturat();
}
let fatSearch = '';
function searchFat(q){ fatSearch=q.toLowerCase(); renderFaturat(); }

function calcFatura(f){
  const sub = (f.zerat||[]).reduce((s,z)=>s+(z.sasia||1)*(z.cmUnit||0),0);
  const tvshAmt = (f.zerat||[]).reduce((s,z)=>z.tvsh?s+(z.sasia||1)*(z.cmUnit||0)*0.20:s,0);
  return {sub, tvsh:tvshAmt, total:sub+tvshAmt};
}

function renderFaturat(){
  if(!document.getElementById('fat-tbody')) return;
  if(!state.faturat) state.faturat=[];
  if(!state.ofertat) state.ofertat=[];

  const sot = new Date().toISOString().split('T')[0];
  // auto-set vonuar
  state.faturat.forEach(f=>{ if(f.statusi==='Në Pritje'&&f.skadon&&f.skadon<sot) f.statusi='Vonuar'; });

  const paguar = state.faturat.filter(f=>f.statusi==='Paguar').length;
  const pritje = state.faturat.filter(f=>f.statusi==='Në Pritje').length;
  const vonuar = state.faturat.filter(f=>f.statusi==='Vonuar').length;
  const total  = state.faturat.reduce((s,f)=>s+calcFatura(f).total,0);
  document.getElementById('fat-paguar').textContent=paguar;
  document.getElementById('fat-pritje').textContent=pritje;
  document.getElementById('fat-vonuar').textContent=vonuar;
  document.getElementById('fat-total-stat').textContent=fmt(total);

  // Badge
  const badgeFat = document.getElementById('badge-fat');
  if(badgeFat){if(vonuar>0||pritje>0){badgeFat.style.display='';badgeFat.textContent=vonuar+pritje;}else badgeFat.style.display='none';}

  let fatList = [...state.faturat];
  if(fatSearch) fatList=fatList.filter(f=>(f.nr+f.klienti+f.projekti).toLowerCase().includes(fatSearch));

  // CARDS (top 4)
  const cardColors=['var(--green)','var(--yellow)','var(--red)','var(--orange)'];
  document.getElementById('fat-cards-grid').innerHTML = fatList.slice(0,4).map((f,i)=>{
    const c=calcFatura(f);
    const clr=f.statusi==='Paguar'?'var(--green)':f.statusi==='Vonuar'?'var(--red)':'var(--yellow)';
    return `<div class="fat-card" style="border-top:3px solid ${clr}">
      <div class="fat-nr">${f.nr}</div>
      <div class="fat-klienti">${f.klienti}</div>
      <div style="font-size:0.72rem;color:var(--muted);margin-bottom:4px">📋 ${f.projekti||'—'}</div>
      <div class="fat-total">${fmt(c.total)}</div>
      <div style="display:flex;justify-content:space-between;align-items:center">
        <span style="font-size:0.72rem;color:var(--muted)">📅 ${f.data} → ⏰ ${f.skadon||'—'}</span>
        ${fatStatusBadge(f.statusi)}
      </div>
      <div class="proj-actions" style="margin-top:10px;padding-top:10px;border-top:1px solid var(--border)">
        <button class="inv-btn inv-btn-add" onclick="openFatModal(${f.id})">✏️</button>
        <button class="inv-btn inv-btn-sell" onclick="printFatura(${f.id})">🖨️ Print</button>
        <button class="inv-btn inv-btn-edit" onclick="toggleFatStatus(${f.id})">✅</button>
      </div>
    </div>`;
  }).join('');

  // TABLE
  document.getElementById('fat-tbody').innerHTML = fatList.map((f,i)=>{
    const c=calcFatura(f);
    return `<tr>
      <td class="mono">${i+1}</td>
      <td class="mono" style="color:var(--cyan)">${f.nr}</td>
      <td class="mono">${f.data}</td>
      <td><strong>${f.klienti}</strong><div style="font-size:0.68rem;color:var(--muted)">${f.nipt||''}</div></td>
      <td style="font-size:0.75rem">${f.projekti||'—'}</td>
      <td class="mono">${fmt(c.sub)}</td>
      <td class="mono" style="color:var(--yellow)">${fmt(c.tvsh)}</td>
      <td class="mono" style="color:var(--orange);font-weight:700">${fmt(c.total)}</td>
      <td>${fatStatusBadge(f.statusi)}</td>
      <td class="mono" style="color:${f.skadon&&f.skadon<new Date().toISOString().split('T')[0]&&f.statusi!=='Paguar'?'var(--red)':'var(--muted)'}">${f.skadon||'—'}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="openFatModal(${f.id})">✏️</button>
        <button class="action-btn" onclick="printFatura(${f.id})">🖨️</button>
        <button class="action-btn" onclick="toggleFatStatus(${f.id})">✅</button>
        <button class="action-btn del" onclick="deleteFatura(${f.id})">🗑️</button>
      </td>
    </tr>`;
  }).join('') || `<tr><td colspan="12" style="text-align:center;padding:32px;color:var(--muted)">Nuk ka fatura. Shto faturën e parë!</td></tr>`;

  // OFERTAT TABLE
  let ofeList = [...state.ofertat];
  if(fatSearch) ofeList=ofeList.filter(o=>(o.nr+o.klienti+o.sherbimi).toLowerCase().includes(fatSearch));
  document.getElementById('ofe-tbody').innerHTML = ofeList.map((o,i)=>`
    <tr>
      <td class="mono">${i+1}</td>
      <td class="mono" style="color:var(--cyan)">${o.nr}</td>
      <td class="mono">${o.data}</td>
      <td><strong>${o.klienti}</strong></td>
      <td>${o.sherbimi||'—'}</td>
      <td class="mono" style="color:var(--orange)">${fmt(o.vlera||0)}</td>
      <td class="mono">${o.vlefshmeria||'—'}</td>
      <td>${ofeStatusBadge(o.statusi)}</td>
      <td style="white-space:nowrap">
        <button class="action-btn" onclick="openOfeModal(${o.id})">✏️</button>
        <button class="action-btn" onclick="convertOfertaToFatura(${o.id})">→ Faturë</button>
        <button class="action-btn del" onclick="deleteOferta(${o.id})">🗑️</button>
      </td>
    </tr>`).join('') || `<tr><td colspan="9" style="text-align:center;padding:32px;color:var(--muted)">Nuk ka oferta</td></tr>`;
}

function fatStatusBadge(s){
  const m={'Paguar':'badge-green','Në Pritje':'badge-yellow','Vonuar':'badge-red'};
  return `<span class="badge ${m[s]||'badge-blue'}">${s}</span>`;
}
function ofeStatusBadge(s){
  const m={'Pranuar':'badge-green','Dërguar':'badge-blue','Në Shqyrtim':'badge-yellow','Refuzuar':'badge-red'};
  return `<span class="badge ${m[s]||'badge-blue'}">${s}</span>`;
}

function toggleFatStatus(id){
  const f=state.faturat.find(x=>x.id===id);
  if(!f) return;
  f.statusi=f.statusi==='Paguar'?'Në Pritje':'Paguar';
  getCurrentSubj().data=state; saveSubjects(); renderFaturat();
  showToast(`Fatura ${f.nr} u shënua si "${f.statusi}"!`,'✅');
}
function deleteFatura(id){
  if(!confirm('Fshi faturën?')) return;
  state.faturat=state.faturat.filter(f=>f.id!==id);
  getCurrentSubj().data=state; saveSubjects(); renderFaturat();
}
function deleteOferta(id){
  if(!confirm('Fshi ofertën?')) return;
  state.ofertat=state.ofertat.filter(o=>o.id!==id);
  getCurrentSubj().data=state; saveSubjects(); renderFaturat();
}
function convertOfertaToFatura(id){
  const o=state.ofertat.find(x=>x.id===id);
  if(!o||!confirm(`Konverto ofertën "${o.nr}" në faturë?`)) return;
  if(!state.faturat) state.faturat=[];
  const nr='FAT-'+new Date().getFullYear()+'-'+String(state.faturat.length+1).padStart(3,'0');
  const skadon=new Date(Date.now()+30*24*3600*1000).toISOString().split('T')[0];
  state.faturat.push({id:Date.now(),nr,data:new Date().toISOString().split('T')[0],
    klienti:o.klienti,nipt:'',projekti:o.sherbimi,
    zerat:[{pershkrimi:o.sherbimi,sasia:1,cmUnit:o.vlera,tvsh:true}],
    statusi:'Në Pritje',skadon,shenime:`Konvertuar nga oferta ${o.nr}`});
  o.statusi='Pranuar';
  getCurrentSubj().data=state; saveSubjects(); renderFaturat();
  showToast(`Oferta u konvertua në faturë ${nr}!`,'🧾');
}

// ── FATURA MODAL ──
function openFatModal(id, projPreset){
  editingId=id||null;
  if(!state.faturat) state.faturat=[];
  const f=id?state.faturat.find(x=>x.id===id):{};
  const nr=id?(f.nr||''):('FAT-'+new Date().getFullYear()+'-'+String(state.faturat.length+1).padStart(3,'0'));
  const projOptions=(state.projektet||[]).map(p=>`<option value="${p.emri}" ${(f.projekti||projPreset?.emri)===p.emri?'selected':''}>${p.emri}</option>`).join('');
  const zerat=f.zerat||[{pershkrimi:'',sasia:1,cmUnit:0,tvsh:true}];

  document.getElementById('modal-title').textContent=id?'✏️ Modifiko Faturë':'🧾 Shto Faturë të Re';
  document.getElementById('modal-body').innerHTML=`
    <div class="form-grid">
      <div class="field"><label>Nr. Faturës</label><input id="f-nr" value="${nr}"></div>
      <div class="field"><label>Data</label><input id="f-dat" type="date" value="${f.data||new Date().toISOString().split('T')[0]}"></div>
      <div class="field"><label>Klienti</label><input id="f-kli" value="${f.klienti||projPreset?.klienti||''}" placeholder="Emri i klientit..."></div>
      <div class="field"><label>NIPT Klienti</label><input id="f-nipt" value="${f.nipt||''}" placeholder="K12345678L"></div>
      <div class="field"><label>Projekti (opsional)</label><select id="f-proj"><option value="">— Pa projekt —</option>${projOptions}</select></div>
      <div class="field"><label>Data e Skadimit</label><input id="f-ska" type="date" value="${f.skadon||''}"></div>
      <div class="field"><label>Statusi</label><select id="f-sts">
        <option ${(f.statusi||'Në Pritje')==='Në Pritje'?'selected':''}>Në Pritje</option>
        <option ${f.statusi==='Paguar'?'selected':''}>Paguar</option>
        <option ${f.statusi==='Vonuar'?'selected':''}>Vonuar</option>
      </select></div>
      <div class="field"><label>Shënime</label><input id="f-she" value="${f.shenime||''}" placeholder="Shënime shtesë..."></div>
    </div>
    <div class="section-label" style="margin:14px 0 10px">📦 Zërat e Faturës</div>
    <div id="fat-zerat-list">
      ${zerat.map((z,zi)=>fatZeraRow(z,zi)).join('')}
    </div>
    <button onclick="addFatZera()" style="margin-top:8px;background:rgba(249,115,22,0.1);color:var(--orange);border:1px dashed rgba(249,115,22,0.3);padding:7px 14px;border-radius:8px;cursor:pointer;font-size:0.78rem;font-family:'DM Sans',sans-serif;width:100%">＋ Shto Zë të Ri</button>
    <div id="fat-total-preview" style="background:var(--s2);border:1px solid var(--border);border-radius:10px;padding:12px;margin-top:12px;font-size:0.82rem;text-align:right"></div>`;
  document._saveType='fat';
  updateFatTotalPreview();
  document.getElementById('modal-overlay').classList.add('open');
}

function fatZeraRow(z,zi){
  return `<div class="form-grid" style="margin-bottom:8px;background:var(--s2);padding:10px;border-radius:8px;border:1px solid var(--border)" id="fat-zera-${zi}">
    <div class="field form-grid full"><label>Përshkrimi</label><input id="fz-per-${zi}" value="${z.pershkrimi||''}" placeholder="Shërbimi ose materiali..." oninput="updateFatTotalPreview()"></div>
    <div class="field"><label>Sasia</label><input id="fz-sas-${zi}" type="number" value="${z.sasia||1}" min="0.01" step="0.01" oninput="updateFatTotalPreview()"></div>
    <div class="field"><label>Çmimi/Njësi (L)</label><input id="fz-cmu-${zi}" type="number" value="${z.cmUnit||0}" oninput="updateFatTotalPreview()"></div>
    <div class="field" style="flex-direction:row;align-items:center;gap:8px;padding-top:20px">
      <input type="checkbox" id="fz-tvs-${zi}" ${z.tvsh?'checked':''} onchange="updateFatTotalPreview()" style="width:16px;height:16px;cursor:pointer">
      <label for="fz-tvs-${zi}" style="font-size:0.78rem;color:var(--text);cursor:pointer">TVSH 20%</label>
      <button onclick="removeFatZera(${zi})" style="margin-left:auto;background:rgba(239,68,68,0.1);color:var(--red);border:1px solid rgba(239,68,68,0.2);padding:4px 10px;border-radius:6px;font-size:0.72rem;cursor:pointer">🗑️</button>
    </div>
  </div>`;
}

let fatZeraCount = 0;
function addFatZera(){
  const list=document.getElementById('fat-zerat-list');
  const zi=list.children.length;
  const div=document.createElement('div');
  div.innerHTML=fatZeraRow({pershkrimi:'',sasia:1,cmUnit:0,tvsh:true},zi);
  list.appendChild(div.firstChild);
  updateFatTotalPreview();
}
function removeFatZera(zi){
  const el=document.getElementById('fat-zera-'+zi);
  if(el) el.remove();
  updateFatTotalPreview();
}
function getFatZerat(){
  const list=document.getElementById('fat-zerat-list');
  if(!list) return [];
  return [...list.querySelectorAll('[id^="fz-per-"]')].map((el,i)=>{
    const zi=el.id.split('-')[2];
    return {
      pershkrimi:el.value,
      sasia:parseFloat(document.getElementById('fz-sas-'+zi)?.value)||1,
      cmUnit:parseFloat(document.getElementById('fz-cmu-'+zi)?.value)||0,
      tvsh:document.getElementById('fz-tvs-'+zi)?.checked||false
    };
  }).filter(z=>z.pershkrimi);
}
function updateFatTotalPreview(){
  const zerat=getFatZerat();
  const sub=zerat.reduce((s,z)=>s+z.sasia*z.cmUnit,0);
  const tvsh=zerat.reduce((s,z)=>z.tvsh?s+z.sasia*z.cmUnit*0.20:s,0);
  const total=sub+tvsh;
  const prev=document.getElementById('fat-total-preview');
  if(prev) prev.innerHTML=`<div style="display:flex;justify-content:flex-end;gap:24px;flex-wrap:wrap">
    <span style="color:var(--muted)">Subtotal: <strong style="color:var(--text)">${fmt(sub)}</strong></span>
    <span style="color:var(--muted)">TVSH: <strong style="color:var(--yellow)">${fmt(tvsh)}</strong></span>
    <span style="color:var(--muted)">TOTAL: <strong style="color:var(--orange);font-size:1.1rem">${fmt(total)}</strong></span>
  </div>`;
}

// ── OFERTA MODAL ──
function openOfeModal(id){
  editingId=id||null;
  if(!state.ofertat) state.ofertat=[];
  const o=id?state.ofertat.find(x=>x.id===id):{};
  const nr=id?(o.nr||''):('OFE-'+new Date().getFullYear()+'-'+String(state.ofertat.length+1).padStart(3,'0'));
  document.getElementById('modal-title').textContent=id?'✏️ Modifiko Ofertë':'📄 Shto Ofertë të Re';
  document.getElementById('modal-body').innerHTML=`
    <div class="form-grid">
      <div class="field"><label>Nr. Ofertës</label><input id="f-nr" value="${nr}"></div>
      <div class="field"><label>Data</label><input id="f-dat" type="date" value="${o.data||new Date().toISOString().split('T')[0]}"></div>
      <div class="field form-grid full"><label>Klienti</label><input id="f-kli" value="${o.klienti||''}" placeholder="Emri i klientit..."></div>
      <div class="field form-grid full"><label>Shërbimi / Përshkrimi i Ofertës</label><input id="f-she" value="${o.sherbimi||''}" placeholder="p.sh. Ndërtim Magazinë 500m²..."></div>
      <div class="field"><label>Vlera (L)</label><input id="f-vlr" type="number" value="${o.vlera||0}"></div>
      <div class="field"><label>Vlefshmëria (data)</label><input id="f-vlf" type="date" value="${o.vlefshmeria||''}"></div>
      <div class="field"><label>Statusi</label><select id="f-sts">
        <option ${(o.statusi||'Dërguar')==='Dërguar'?'selected':''}>Dërguar</option>
        <option ${o.statusi==='Në Shqyrtim'?'selected':''}>Në Shqyrtim</option>
        <option ${o.statusi==='Pranuar'?'selected':''}>Pranuar</option>
        <option ${o.statusi==='Refuzuar'?'selected':''}>Refuzuar</option>
      </select></div>
    </div>`;
  document._saveType='ofe';
  document.getElementById('modal-overlay').classList.add('open');
}

// PRINT FATURA
function printFatura(id){
  const f=state.faturat.find(x=>x.id===id);
  if(!f) return;
  const c=calcFatura(f);
  const subj=getCurrentSubj();
  const color=subj.ngjyra||'#f97316';
  const colorLight=color+'18';

  // Build logo HTML
  const logoHtml = subj.logo
    ? `<img src="${subj.logo}" style="height:60px;max-width:180px;object-fit:contain;display:block">`
    : `<div style="font-size:1.6rem;font-weight:800;color:${color};letter-spacing:-0.02em">🏗️ ${subj.emri}</div>`;

  const statusColor = f.statusi==='Paguar'?'#22c55e': f.statusi==='Vonuar'?'#ef4444':'#eab308';

  // Generate barcode SVG inline (CODE128 - no external script needed)
  const barcodeNr = f.nr.replace(/[^A-Z0-9\-\.\/ ]/gi,'').substring(0,20);
  function bc128(text){
    const C128=[
      [2,1,2,2,2,2],[2,2,2,1,2,2],[2,2,2,2,2,1],[1,2,1,2,2,3],[1,2,1,3,2,2],[1,3,1,2,2,2],[1,2,2,2,1,3],[1,2,2,3,1,2],[1,3,2,2,1,2],[2,2,1,2,1,3],
      [2,2,1,3,1,2],[2,3,1,2,1,2],[1,1,2,2,3,2],[1,2,2,1,3,2],[1,2,2,2,3,1],[1,1,3,2,2,2],[1,2,3,1,2,2],[1,2,3,2,2,1],[2,2,3,2,1,1],[2,2,1,1,3,2],
      [2,2,1,2,3,1],[2,1,3,2,1,2],[2,2,3,1,1,2],[3,1,2,1,3,1],[3,1,1,2,2,2],[3,2,1,1,2,2],[3,2,1,2,2,1],[3,1,2,2,1,2],[3,2,2,1,1,2],[3,2,2,2,1,1],
      [2,1,2,1,2,3],[2,1,2,3,2,1],[2,3,2,1,2,1],[1,1,1,3,2,3],[1,3,1,1,2,3],[1,3,1,3,2,1],[1,1,2,3,1,3],[1,3,2,1,1,3],[1,3,2,3,1,1],[2,1,1,3,1,3],
      [2,1,3,1,1,3],[2,3,1,1,1,3],[1,1,2,1,3,3],[1,1,3,1,2,3],[3,1,1,1,2,3],[1,2,2,3,3,1],[1,3,3,1,1,2],[1,1,1,1,4,2],[1,2,1,1,4,1],[1,2,1,4,1,1],
      [1,4,1,1,2,1],[1,1,3,3,1,2],[4,1,1,1,1,3],[4,1,1,3,1,1],[1,1,4,1,1,3],[1,1,4,3,1,1],[4,1,1,1,3,1],[4,1,3,1,1,1],[1,1,2,1,4,2],[1,1,3,1,4,1],
      [1,2,4,1,1,2],[1,2,2,1,4,1],[1,4,2,1,1,2],[1,4,2,2,1,1],[1,1,1,3,4,1],[1,1,1,4,3,1],[1,3,1,1,4,1],[1,4,1,1,3,1],[2,1,1,1,4,2],[2,1,1,4,1,2],
      [2,1,1,4,2,1],[2,1,4,1,1,2],[2,1,4,2,1,1],[2,4,1,1,1,2],[2,4,1,2,1,1],[2,4,2,1,1,1],[1,2,3,1,3,1],[1,1,4,2,1,2],[3,3,1,1,2,1],[3,1,4,1,1,2],
      [3,2,1,4,1,1],[3,4,1,1,1,2],[3,1,1,4,2,1],[3,4,1,2,1,1],[3,1,4,2,1,1],[3,2,4,1,1,1],[1,4,1,3,1,1],[2,1,2,3,3,1],[1,1,4,1,3,1],[2,4,1,1,3,1],
      [1,2,1,1,4,2],[1,3,2,1,1,2],[2,2,1,1,1,4],[2,1,1,2,1,4],[3,3,1,1,1,2],[2,1,1,4,1,2],[1,3,1,2,1,2],[1,2,1,3,1,2],[3,2,1,1,1,2]
    ];
    const START_B=104,STOP=106;
    const chars=text.split('').map(c=>c.charCodeAt(0)-32);
    let chk=START_B; chars.forEach((c,i)=>chk+=(i+1)*c); chk%=103;
    const codes=[START_B,...chars,chk,STOP];
    const W=240,H=50;
    let total=codes.reduce((s,c)=>{const p=C128[c]||[1,1,1,1,1,1];return s+p.reduce((a,b)=>a+b,0);},0)+2;
    const mod=W/total;
    let rects='',x=mod;
    codes.forEach(c=>{
      const p=C128[c]||[1,1,1,1,1,1];
      let bar=true;
      p.forEach(w=>{
        if(bar) rects+=`<rect x="${x.toFixed(2)}" y="0" width="${Math.max(0.8,(w*mod-0.4)).toFixed(2)}" height="${H}"/>`;
        x+=w*mod; bar=!bar;
      });
    });
    return `<svg xmlns="http://www.w3.org/2000/svg" width="${W}" height="${H}" viewBox="0 0 ${W} ${H}"><rect width="${W}" height="${H}" fill="white"/><g fill="#374151">${rects}</g></svg>`;
  }
  const barcodeHtml = bc128(barcodeNr);

  const html = `<!DOCTYPE html>
<html lang="sq"><head>
<meta charset="UTF-8">
<title>Faturë ${f.nr} — ${subj.emri}</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  body{font-family:'Inter',sans-serif;background:#fff;color:#111827;font-size:13px;line-height:1.5}
  .page{max-width:820px;margin:0 auto;padding:40px 48px}
  /* HEADER */
  .hdr{display:flex;justify-content:space-between;align-items:flex-start;padding-bottom:24px;border-bottom:3px solid ${color};margin-bottom:30px}
  .hdr-left{}
  .company-sub{font-size:11px;color:#9ca3af;margin-top:4px}
  .hdr-right{text-align:right}
  .fat-label{font-size:10px;font-weight:700;letter-spacing:0.15em;text-transform:uppercase;color:#9ca3af;margin-bottom:4px}
  .fat-nr{font-size:1.8rem;font-weight:800;color:#111827;letter-spacing:-0.02em}
  .fat-date{font-size:12px;color:#6b7280;margin-top:4px}
  /* STATUS BADGE */
  .status-badge{display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:99px;font-size:11px;font-weight:700;margin-top:6px;background:${statusColor}18;color:${statusColor};border:1px solid ${statusColor}40}
  /* PARTIES */
  .parties{display:grid;grid-template-columns:1fr 1fr 1fr;gap:0;margin-bottom:28px;border:1px solid #e5e7eb;border-radius:12px;overflow:hidden}
  .party{padding:16px 18px}
  .party+.party{border-left:1px solid #e5e7eb}
  .party-lbl{font-size:9px;font-weight:700;letter-spacing:0.15em;text-transform:uppercase;color:#9ca3af;margin-bottom:8px}
  .party-name{font-size:14px;font-weight:700;color:#111827;margin-bottom:3px}
  .party-detail{font-size:11px;color:#6b7280;margin-bottom:1px}
  /* ITEMS TABLE */
  .tbl-wrap{border:1px solid #e5e7eb;border-radius:12px;overflow:hidden;margin-bottom:24px}
  table{width:100%;border-collapse:collapse}
  thead{background:${color};color:#fff}
  th{padding:11px 14px;text-align:left;font-size:10px;font-weight:700;letter-spacing:0.1em;text-transform:uppercase}
  th.num{text-align:right}
  td{padding:11px 14px;border-bottom:1px solid #f3f4f6;font-size:13px}
  td.num{text-align:right;font-family:'SF Mono','Fira Mono',monospace;font-size:12px}
  tr:last-child td{border-bottom:none}
  tr:nth-child(even) td{background:#fafafa}
  tfoot td{background:#f9fafb;font-weight:600}
  /* TOTALS */
  .totals{display:flex;justify-content:flex-end;margin-bottom:24px}
  .totals-box{width:300px;border:1px solid #e5e7eb;border-radius:12px;overflow:hidden}
  .tot-row{display:flex;justify-content:space-between;padding:9px 16px;font-size:12px;border-bottom:1px solid #f3f4f6}
  .tot-row:last-child{border-bottom:none}
  .tot-final{background:${color};color:#fff;padding:12px 16px;display:flex;justify-content:space-between;align-items:center;font-weight:700;font-size:14px}
  /* FOOTER */
  .note-box{background:#fffbeb;border:1px solid #fcd34d;border-radius:10px;padding:14px 16px;margin-bottom:24px;font-size:12px;color:#92400e;line-height:1.6}
  .footer{display:flex;justify-content:space-between;align-items:flex-end;padding-top:20px;border-top:1px solid #e5e7eb;margin-top:8px}
  .footer-brand{font-size:10px;color:#d1d5db}
  .sign-box{border-top:1px solid #9ca3af;padding-top:6px;font-size:10px;color:#9ca3af;text-align:center;width:160px}
  /* QR placeholder */
  .qr-hint{width:56px;height:56px;border:1px solid #e5e7eb;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:20px;color:#d1d5db}
  @media print{
    body{-webkit-print-color-adjust:exact;print-color-adjust:exact}
    .page{padding:20px 28px}
    .no-print{display:none}
  }
</style>
</head><body>
<div class="page">

  <!-- PRINT TOOLBAR -->
  <div class="no-print" style="display:flex;gap:8px;margin-bottom:20px;padding:10px 14px;background:#f9fafb;border:1px solid #e5e7eb;border-radius:10px">
    <button onclick="window.print()" style="background:${color};color:#fff;border:none;padding:8px 18px;border-radius:7px;cursor:pointer;font-size:13px;font-weight:600;font-family:'Inter',sans-serif">🖨️ Printo / Ruaj PDF</button>
    <button onclick="window.close()" style="background:#fff;color:#6b7280;border:1px solid #e5e7eb;padding:8px 14px;border-radius:7px;cursor:pointer;font-size:13px;font-family:'Inter',sans-serif">✕ Mbyll</button>
    <span style="margin-left:auto;font-size:11px;color:#9ca3af;align-self:center">💡 Për PDF: Printo → "Ruaj si PDF"</span>
  </div>

  <!-- HEADER -->
  <div class="hdr">
    <div class="hdr-left">
      ${logoHtml}
      ${subj.logo?`<div style="font-size:13px;font-weight:600;color:#374151;margin-top:8px">${subj.emri}</div>`:''}
      ${subj.nipt?`<div class="company-sub">NIPT: ${subj.nipt}</div>`:''}
      ${subj.adresa?`<div class="company-sub">📍 ${subj.adresa}</div>`:''}
      ${subj.tel?`<div class="company-sub">📞 ${subj.tel}</div>`:''}
      ${subj.email?`<div class="company-sub">✉️ ${subj.email}</div>`:''}
    </div>
    <div class="hdr-right">
      <div class="fat-label">Faturë Tatimore</div>
      <div class="fat-nr">${f.nr}</div>
      <div class="fat-date">Data: <strong>${f.data}</strong></div>
      ${f.skadon?`<div class="fat-date">Skadon: <strong>${f.skadon}</strong></div>`:''}
      <div><span class="status-badge">● ${f.statusi}</span></div>
    </div>
  </div>

  <!-- PARTIES -->
  <div class="parties">
    <div class="party">
      <div class="party-lbl">Nga (Shitësi)</div>
      <div class="party-name">${subj.emri}</div>
      ${subj.nipt?`<div class="party-detail">NIPT: ${subj.nipt}</div>`:''}
      ${subj.adresa?`<div class="party-detail">${subj.adresa}</div>`:''}
      ${subj.website?`<div class="party-detail">${subj.website}</div>`:''}
    </div>
    <div class="party">
      <div class="party-lbl">Për (Blerësi)</div>
      <div class="party-name">${f.klienti}</div>
      ${f.nipt?`<div class="party-detail">NIPT: ${f.nipt}</div>`:''}
      ${f.projekti?`<div class="party-detail">📋 ${f.projekti}</div>`:''}
    </div>
    <div class="party">
      <div class="party-lbl">Detaje Pagese</div>
      <div class="party-detail" style="margin-bottom:6px">Metoda: Transfer Bankar</div>
      ${f.skadon?`<div class="party-detail">Afati: <strong>${f.skadon}</strong></div>`:''}
      <div class="party-detail" style="margin-top:8px">Referenca:</div>
      <div class="party-name" style="font-size:12px">${f.nr}</div>
    </div>
  </div>

  <!-- ITEMS TABLE -->
  <div class="tbl-wrap">
    <table>
      <thead>
        <tr>
          <th style="width:36px">#</th>
          <th>Përshkrimi i Shërbimit / Mallrave</th>
          <th class="num" style="width:70px">Sasia</th>
          <th class="num" style="width:110px">Çmimi/Njësi</th>
          <th class="num" style="width:60px">TVSH</th>
          <th class="num" style="width:120px">Total</th>
        </tr>
      </thead>
      <tbody>
        ${(f.zerat||[]).map((z,i)=>{
          const row_total = z.sasia * z.cmUnit * (z.tvsh ? 1.20 : 1);
          return `<tr>
            <td style="color:#9ca3af">${i+1}</td>
            <td>${z.pershkrimi}</td>
            <td class="num">${Number(z.sasia).toLocaleString('sq-AL')}</td>
            <td class="num">${Number(z.cmUnit).toLocaleString('sq-AL')} L</td>
            <td class="num">${z.tvsh?'<span style="color:#f97316;font-weight:600">20%</span>':'—'}</td>
            <td class="num" style="font-weight:600">${Number(row_total).toLocaleString('sq-AL')} L</td>
          </tr>`;
        }).join('')}
      </tbody>
    </table>
  </div>

  <!-- TOTALS -->
  <div class="totals">
    <div class="totals-box">
      <div class="tot-row"><span style="color:#6b7280">Subtotal (pa TVSH)</span><span>${Number(c.sub).toLocaleString('sq-AL')} L</span></div>
      <div class="tot-row"><span style="color:#6b7280">TVSH (20%)</span><span>${Number(c.tvsh).toLocaleString('sq-AL')} L</span></div>
      <div class="tot-final"><span>TOTAL PËR PAGESË</span><span>${Number(c.total).toLocaleString('sq-AL')} L</span></div>
    </div>
  </div>

  <!-- NOTE -->
  ${(f.shenime||subj.shenimFature)?`<div class="note-box">
    📝 ${f.shenime||''} ${f.shenime&&subj.shenimFature?'<br>':''} ${subj.shenimFature||''}
  </div>`:''}

  <!-- FOOTER -->
  <div class="footer">
    <div style="display:flex;flex-direction:column;align-items:center;gap:3px">
      \${barcodeHtml}
      <div style="font-size:8px;color:#9ca3af;font-family:monospace;letter-spacing:0.05em;margin-top:3px">\${f.nr}</div>
    </div>
    <div style="text-align:center">
      <div class="sign-box">Firmë & Vulë</div>
    </div>
    <div style="text-align:right">
      <div class="footer-brand">Gjeneruar me BuildTrack</div>
      <div class="footer-brand">${new Date().toLocaleDateString('sq-AL',{day:'2-digit',month:'long',year:'numeric'})}</div>
      ${subj.website?`<div class="footer-brand" style="color:${color}">${subj.website}</div>`:''}
    </div>
  </div>

</div>
</body></html>`;
  const _blob1 = new Blob([html], {type:'text/html;charset=utf-8'});
  const _url1 = URL.createObjectURL(_blob1);
  const _win1 = window.open(_url1, '_blank');
  if(!_win1){ const _a=document.createElement('a'); _a.href=_url1; _a.target='_blank'; document.body.appendChild(_a); _a.click(); _a.remove(); }
  setTimeout(()=>URL.revokeObjectURL(_url1), 15000);
}

// ── OPEN MODAL: ALL PANELS UNIFIED ──
function openModal(type, id){
  // New panel types
  if(currentPanel==='projektet'){openProjModal(id);return;}
  if(currentPanel==='faturat'){
    if(fatView==='ofertat'){openOfeModal(id);return;}
    openFatModal(id);return;
  }
  editingId = id||null;
  const p = currentPanel;
  let title, body;
  if(p==='materiale'||p==='dashboard'){
    title = id?'Modifiko Material':'➕ Shto Material të Ri';
    const item = id?state.materiale.find(m=>m.id===id):{};
    body=`<div class="form-grid">
      <div class="field form-grid full"><label>Emri Materialit</label><input id="f-emri" value="${item.emri||''}" placeholder="Çimento Portland..."></div>
      <div class="field"><label>Kategori</label><select id="f-kat">
        ${['Betoni & Strukturë','Çelik & Metal','Muratim','Elektrik','Hidraulikë','Izolim','Tjetër'].map(c=>`<option ${item.kategori===c?'selected':''}>${c}</option>`).join('')}
      </select></div>
      <div class="field"><label>Njësia</label><input id="f-nje" value="${item.njesia||''}" placeholder="Ton / Metër / Copë"></div>
      <div class="field"><label>Sasia Aktuale</label><input id="f-sas" type="number" value="${item.sasia||0}"></div>
      <div class="field"><label>Sasia Minimale</label><input id="f-min" type="number" value="${item.min||0}"></div>
      <div class="field"><label>Çmimi Blerje (L)</label><input id="f-cmb" type="number" value="${item.cmBlerje||0}"></div>
      <div class="field"><label>Çmimi Shitje (L)</label><input id="f-cms" type="number" value="${item.cmShitje||0}"></div>
      <div class="field"><label>Furnitori</label><select id="f-fur">
        ${state.furnitoret.map(f=>`<option ${item.furnitori===f.emri?'selected':''}>${f.emri}</option>`).join('')}
      </select></div>
    </div>`;
    document._saveType='mat';
  } else if(p==='pajisje'){
    title = id?'Modifiko Pajisje':'➕ Shto Pajisje të Re';
    const item = id?state.pajisje.find(p=>p.id===id):{};
    body=`<div class="form-grid">
      <div class="field form-grid full"><label>Emri Pajisjes</label><input id="f-emri" value="${item.emri||''}" placeholder="Betonierë, Grilë..."></div>
      <div class="field"><label>Kategori</label><select id="f-kat">
        ${['Makina','Mjete Dore','Makina të Rënda','Elektrike','Skela','Tjetër'].map(c=>`<option ${item.kategori===c?'selected':''}>${c}</option>`).join('')}
      </select></div>
      <div class="field"><label>Seria / Kodi</label><input id="f-ser" value="${item.seria||''}"></div>
      <div class="field"><label>Gjendja</label><select id="f-gje">
        ${['Shumë Mirë','Mirë','Nevojitet Riparim','Jashtë Funksionit'].map(c=>`<option ${item.gjendja===c?'selected':''}>${c}</option>`).join('')}
      </select></div>
      <div class="field"><label>Vlera Blerjes (L)</label><input id="f-vlr" type="number" value="${item.vlera||0}"></div>
      <div class="field"><label>Mirëmbajtja Radhës</label><input id="f-mir" type="date" value="${item.mirembajtja&&item.mirembajtja!=='—'?item.mirembajtja:''}"></div>
      <div class="field"><label>Lokacioni</label><input id="f-lok" value="${item.lokacioni||''}" placeholder="Kantieri, Depo..."></div>
      <div class="field"><label>Statusi</label><select id="f-sts">
        ${['Aktive','Riparim','Joaktive'].map(c=>`<option ${item.status===c?'selected':''}>${c}</option>`).join('')}
      </select></div>
    </div>`;
    document._saveType='paj';
  } else if(p==='shitje'){
    title = '➕ Regjistro Lëvizje';
    const matOptions = state.materiale.map(m=>
      `<option value="${m.id}" data-cm-shitje="${m.cmShitje}" data-cm-blerje="${m.cmBlerje}" data-sasia="${m.sasia}" data-njesia="${m.njesia}" data-status="${m.status}">${m.emri} [Stok: ${m.sasia} ${m.njesia}]</option>`
    ).join('');
    body=`<div class="form-grid">
      <div class="field"><label>Data</label><input id="f-dat" type="date" value="${new Date().toISOString().split('T')[0]}"></div>
      <div class="field"><label>Lloji</label><select id="f-llj" onchange="onLlojiChange()"><option>Shitje</option><option>Blerje</option></select></div>
      <div class="field form-grid full">
        <label>Artikulli (nga Inventari)</label>
        <select id="f-art-sel" onchange="onArtikullChange()">
          <option value="">— Zgjidh Material —</option>${matOptions}
        </select>
        <input id="f-art" style="display:none">
      </div>
      <div id="stok-alert-box" style="display:none;background:rgba(239,68,68,0.1);border:1px solid rgba(239,68,68,0.3);border-radius:8px;padding:10px 14px;font-size:0.8rem;color:var(--red);grid-column:1/-1"></div>
      <div class="field"><label>Sasia</label><input id="f-sas" type="number" value="1" oninput="onSasiaChange()"><span id="stok-available" style="font-size:0.7rem;color:var(--muted);margin-top:2px"></span></div>
      <div class="field"><label>Çmimi për Njësi (L)</label><input id="f-cmu" type="number" value="0" oninput="onSasiaChange()"></div>
      <div class="field form-grid full" id="total-preview-box" style="background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:10px 14px;font-size:0.8rem;color:var(--muted)">Zgjidh artikullin dhe sasinë...</div>
      <div class="field form-grid full"><label>Klienti / Furnitori / Shënim</label><input id="f-kli" placeholder="Emri klientit ose furnitorit..."></div>
    </div>`;
    document._saveType='sh';
    setTimeout(function(){ onLlojiChange(); updateShitjeModalActions(); }, 50);
  } else if(p==='furnitoret'){
    title = id?'Modifiko Furnitor':'➕ Shto Furnitor të Ri';
    const item = id?state.furnitoret.find(f=>f.id===id):{};
    body=`<div class="form-grid">
      <div class="field"><label>Emri Firmës</label><input id="f-emri" value="${item.emri||''}"></div>
      <div class="field"><label>NID / NIPT</label><input id="f-nid" value="${item.nid||''}"></div>
      <div class="field"><label>Kontakti</label><input id="f-kon" value="${item.kontakti||''}"></div>
      <div class="field"><label>Afati Pageses</label><input id="f-afa" value="${item.afati||'30 ditë'}"></div>
      <div class="field form-grid full"><label>Adresa</label><input id="f-adr" value="${item.adresa||''}"></div>
      <div class="field form-grid full"><label>Materialet e Furnizimit</label><input id="f-mat" value="${item.materialet||''}"></div>
    </div>`;
    document._saveType='fur';
  } else if(type==='shpenzim'||p==='bilanci'){
    const item = id?state.shpenzime.find(s=>s.id===id):{};
    title = id?'Modifiko Shpenzim':'➕ Shto Shpenzim';
    body=`<div class="form-grid">
      <div class="field"><label>Data</label><input id="f-dat" type="date" value="${item.data||new Date().toISOString().split('T')[0]}"></div>
      <div class="field"><label>Kategoria</label><select id="f-kat">
        ${['Qira','Paga','Transport','Mirëmbajtje','Komunikim','Utilities','Marketing','Tatim & Tarifë','Tjetër'].map(c=>`<option ${item.kategoria===c?'selected':''}>${c}</option>`).join('')}
      </select></div>
      <div class="field form-grid full"><label>Përshkrimi</label><input id="f-emri" value="${item.pershkrimi||''}" placeholder="Qira, paga, karburant..."></div>
      <div class="field"><label>Vlera (pa TVSH) L</label><input id="f-vlr" type="number" value="${item.vlera||0}"></div>
      <div class="field"><label>Me TVSH 20%?</label><select id="f-tvsh">
        <option value="true" ${item.tvsh?'selected':''}>Po — me TVSH</option>
        <option value="false" ${!item.tvsh&&item.tvsh!==undefined?'selected':''}>Jo — pa TVSH</option>
      </select></div>
    </div>`;
    document._saveType='shp';
  }
  if(title&&body){
    document.getElementById('modal-title').textContent = title;
    document.getElementById('modal-body').innerHTML = body;
    document.getElementById('modal-overlay').classList.add('open');
  }
}

// ── UPDATEBADGES: ALL BADGES UNIFIED ──
function updateBadges(){
  // Inventar badge
  const low=state.materiale.filter(m=>m.status!=='Stok Normal').length;
  const bInv=document.getElementById('badge-inv-low');
  if(bInv){if(low>0){bInv.style.display='';bInv.textContent=low;}else bInv.style.display='none';}
  // Materiale badge
  const bMat=document.getElementById('badge-mat');
  if(bMat) bMat.textContent=state.materiale.length;
  // Bilanci badge
  const bBil=document.getElementById('badge-bil');
  if(bBil) bBil.style.display='none';
  // Projektet badge
  if(state.projektet){
    const v=state.projektet.filter(p=>p.statusi==='Vonuar').length;
    const b=document.getElementById('badge-proj');
    if(b){if(v>0){b.style.display='';b.textContent=v;}else b.style.display='none';}
  }
  // Faturat badge
  if(state.faturat){
    const v=state.faturat.filter(f=>f.statusi==='Vonuar'||f.statusi==='Në Pritje').length;
    const b=document.getElementById('badge-fat');
    if(b){if(v>0){b.style.display='';b.textContent=v;}else b.style.display='none';}
  }
}

// ═══════════════════════════════════════════════
// RAPORTI MUJOR I BIZNESIT
// ═══════════════════════════════════════════════
const MUAJT = ['Janar','Shkurt','Mars','Prill','Maj','Qershor','Korrik','Gusht','Shtator','Tetor','Nëntor','Dhjetor'];
let rapYear = new Date().getFullYear().toString();
let rapMonth = String(new Date().getMonth()+1).padStart(2,'0');
let rapLocked = false;
let rapChartMain = null, rapChartShp = null, rapChartTrend = null;
let rapPunCount = 0;

function getRapKey(){ return rapYear+'-'+rapMonth; }
function getRap(){ return (state.raportet||{})[getRapKey()] || {}; }

function renderRaporti(){
  if(!document.getElementById('rap-period-lbl')) return;
  if(!state.raportet) state.raportet={};

  // Sync selects
  const ySel = document.getElementById('rap-year-sel');
  const mSel = document.getElementById('rap-month-sel');
  if(ySel){
    const years=[...new Set([2024,2025,2026,parseInt(rapYear)])].sort();
    ySel.innerHTML=years.map(y=>`<option value="${y}" ${y==rapYear?'selected':''}>${y}</option>`).join('');
    rapYear=ySel.value||rapYear;
  }
  if(mSel) mSel.value=rapMonth;

  document.getElementById('rap-period-lbl').textContent = MUAJT[parseInt(rapMonth)-1].toUpperCase()+' '+rapYear;

  const r = getRap();
  rapLocked = r.locked||false;
  updateRapLockUI();

  // Fill form fields
  const fields = ['shitje-mat','shitje-she','ardhura-tjera','blerje-mat','blerje-paj','blerje-tjera',
    'qira','karb','energji','mirembajt','telekom','shp-tjera',
    'arka-fillim','arka-fund','banka','detyrime',
    'stok-fillim','stok-fund','stok-kritik','stok-total-art','shenime','objektivat'];
  fields.forEach(f=>{
    const el=document.getElementById('rap-'+f);
    if(!el) return;
    const key=f.replace(/-/g,'_');
    el.value=r[key]||'';
  });
  if(document.getElementById('rap-vleresim')) document.getElementById('rap-vleresim').value=r.vleresim||'mire';

  // Render punonjesit
  renderRapPunonjesit(r.punonjesit||[]);

  rapCalc();
  renderRapHistory();
  renderRapCharts();
}

function updateRapLockUI(){
  const btn=document.getElementById('rap-lock-btn');
  if(!btn) return;
  if(rapLocked){
    btn.textContent='🔒 Raporti i Mbyllur';
    btn.className='rap-lock-btn locked';
  } else {
    btn.textContent='🔓 Modifikim i Hapur';
    btn.className='rap-lock-btn open';
  }
  // Disable/enable all inputs
  document.querySelectorAll('#panel-raporti input, #panel-raporti select, #panel-raporti textarea').forEach(el=>{
    if(el.id==='rap-year-sel'||el.id==='rap-month-sel'||el.id==='rap-lock-btn') return;
    el.disabled=rapLocked;
  });
  const addBtn=document.getElementById('rap-add-pun-btn');
  if(addBtn) addBtn.style.display=rapLocked?'none':'';
}

function toggleRapLock(){
  rapLocked=!rapLocked;
  const r=getRap();
  r.locked=rapLocked;
  state.raportet[getRapKey()]=r;
  getCurrentSubj().data=state; saveSubjects();
  updateRapLockUI();
  showToast(rapLocked?'🔒 Raporti u mbyll dhe u ruajt!':'🔓 Raporti u hap për modifikim!',rapLocked?'🔒':'🔓');
}

function rapNavMonth(dir){
  let m=parseInt(rapMonth)+dir;
  let y=parseInt(rapYear);
  if(m>12){m=1;y++;}
  if(m<1){m=12;y--;}
  rapMonth=String(m).padStart(2,'0');
  rapYear=String(y);
  renderRaporti();
}

function n(id){ return parseFloat(document.getElementById(id)?.value)||0; }

function rapCalc(){
  // Të ardhura
  const shitjeMat=n('rap-shitje-mat'), shitjeShe=n('rap-shitje-she'), ardhuratTjera=n('rap-ardhura-tjera');
  const totArdhura=shitjeMat+shitjeShe+ardhuratTjera;
  const tvshArdhura=totArdhura*0.20;
  document.getElementById('rap-r-shitje').textContent=fmt(totArdhura);
  document.getElementById('rap-r-shitje-tvsh').textContent=fmt(tvshArdhura);
  document.getElementById('rap-r-ardhura-tot').textContent=fmt(totArdhura+tvshArdhura);

  // Blerje
  const blerjeM=n('rap-blerje-mat'),blerjeP=n('rap-blerje-paj'),blerjeT=n('rap-blerje-tjera');
  const totBlerje=blerjeM+blerjeP+blerjeT;
  document.getElementById('rap-r-blerje-tot').textContent=fmt(totBlerje);

  // Shpenzime
  const qira=n('rap-qira'),karb=n('rap-karb'),energji=n('rap-energji'),
        mirembajt=n('rap-mirembajt'),telekom=n('rap-telekom'),shpT=n('rap-shp-tjera');
  const totShpOp=qira+karb+energji+mirembajt+telekom+shpT;
  const tvshShp=totShpOp*0.20;
  document.getElementById('rap-r-shp-op').textContent=fmt(totShpOp);
  document.getElementById('rap-r-tvsh').textContent=fmt(tvshShp);
  document.getElementById('rap-r-shp-tot').textContent=fmt(totShpOp+tvshShp);

  // Arka
  const arkaF=n('rap-arka-fillim'),banka=n('rap-banka'),detyrime=n('rap-detyrime');
  const arkaFund=totArdhura-totShpOp-totBlerje+arkaF;
  const arkaFundEl=document.getElementById('rap-arka-fund');
  if(arkaFundEl&&!arkaFundEl.value) arkaFundEl.value=Math.max(0,Math.round(arkaFund));
  const levizja=arkaFund-arkaF;
  const gjendja=arkaFund+banka-detyrime;
  document.getElementById('rap-r-levizja').textContent=(levizja>=0?'+':'')+fmt(levizja);
  document.getElementById('rap-r-levizja').style.color=levizja>=0?'var(--green)':'var(--red)';
  document.getElementById('rap-r-gjendja').textContent=fmt(gjendja);
  document.getElementById('rap-r-gjendja').style.color=gjendja>=0?'var(--green)':'var(--red)';

  // Stok
  const stokF=n('rap-stok-fillim'),stokFund=n('rap-stok-fund');
  const stokDelta=stokFund-stokF;
  document.getElementById('rap-r-stok-delta').textContent=(stokDelta>=0?'+':'')+fmt(stokDelta);
  document.getElementById('rap-r-stok-delta').style.color=stokDelta>=0?'var(--green)':'var(--orange)';

  // Punonjesit calc
  const punRows=document.querySelectorAll('[data-rap-pun]');
  let totBruto=0,totKont=0,totTatim=0,totNeto=0,totKosto=0;
  punRows.forEach(row=>{
    const bruto=parseFloat(row.querySelector('.pun-bruto')?.value)||0;
    const c=calcPaga(bruto);
    totBruto+=bruto; totKont+=c.kontPunedh; totTatim+=c.tatim; totNeto+=c.neto; totKosto+=c.kostoTotale;
  });
  document.getElementById('rap-r-paga-bruto').textContent=fmt(totBruto);
  document.getElementById('rap-r-kontribute').textContent=fmt(totKont);
  document.getElementById('rap-r-tatim-pun').textContent=fmt(totTatim);
  document.getElementById('rap-r-paga-tot').textContent=fmt(totKosto);

  // Fitimi neto
  const fitim=totArdhura-totShpOp-totKosto-totBlerje;
  const pct=totArdhura>0?((fitim/totArdhura)*100).toFixed(1):0;
  document.getElementById('rs-ardhura').textContent=fmt(totArdhura);
  document.getElementById('rs-shp-op').textContent=fmt(totShpOp);
  document.getElementById('rs-pagat').textContent=fmt(totKosto);
  document.getElementById('rs-blerje').textContent=fmt(totBlerje);
  document.getElementById('rs-fitim-neto').textContent=fmt(fitim);
  document.getElementById('rs-fitim-neto').style.color=fitim>=0?'var(--green)':'var(--red)';
  document.getElementById('rs-fitim-pct').textContent=pct+'% marzh fitimi';

  // KPI row
  const prevKey=getPrevMonthKey();
  const prev=(state.raportet||{})[prevKey]||{};
  const prevArdhura=(prev.shitje_mat||0)+(prev.shitje_she||0)+(prev.ardhura_tjera||0);
  const prevShp=(prev.qira||0)+(prev.karb||0)+(prev.energji||0)+(prev.mirembajt||0)+(prev.telekom||0)+(prev.shp_tjera||0);
  const prevPagat=(prev.punonjesit||[]).reduce((s,p)=>s+calcPaga(p.bruto||0).kostoTotale,0);
  const prevFitim=prevArdhura-prevShp-prevPagat;

  setKpi('rkpi-ardhura','rkpi-ardhura-d',totArdhura,prevArdhura,'L');
  setKpi('rkpi-shp','rkpi-shp-d',totShpOp,prevShp,'L',true);
  setKpi('rkpi-fitim','rkpi-fitim-d',fitim,prevFitim,'L');
  setKpi('rkpi-paga','rkpi-paga-d',totKosto,prevPagat,'L',true);

  // Auto-save hint
  const hint=document.getElementById('rap-save-hint');
  if(hint&&!rapLocked) hint.textContent='✏️ Ndryshim i paruajtur — kliko Ruaj';
}

function setKpi(valId,deltaId,cur,prev,unit,reverseColor){
  const el=document.getElementById(valId);
  const del=document.getElementById(deltaId);
  if(el) el.textContent=fmt(cur);
  if(del&&prev){
    const diff=cur-prev;
    const pct=prev>0?((Math.abs(diff)/prev)*100).toFixed(1):0;
    const up=diff>=0;
    const good=reverseColor?!up:up;
    del.textContent=(up?'▲':'▼')+' '+pct+'% vs muaji i kaluar';
    del.style.color=good?'var(--green)':'var(--red)';
  }
}

function getPrevMonthKey(){
  let m=parseInt(rapMonth)-1, y=parseInt(rapYear);
  if(m<1){m=12;y--;}
  return y+'-'+String(m).padStart(2,'0');
}

function renderRapPunonjesit(list){
  const container=document.getElementById('rap-punonjesit-list');
  if(!container) return;
  rapPunCount=list.length;
  container.innerHTML='';
  list.forEach((p,i)=>rapAddPunatorRow(p,i));
  if(list.length===0 && !rapLocked){
    // Auto-load from state.punonjesit if available
    if((state.punonjesit||[]).length>0){
      state.punonjesit.filter(p=>p.status==='Aktiv').forEach((p,i)=>{
        rapAddPunatorRow({emri:p.emri,pozicioni:p.pozicioni,bruto:p.pagaBruto,statusi:'Paguar'},i);
      });
    }
  }
}

function rapAddPunatorRow(p, i){
  const container=document.getElementById('rap-punonjesit-list');
  if(!container) return;
  const idx=container.children.length;
  const c=p?calcPaga(p.bruto||0):{neto:0};
  const dis=rapLocked?'disabled':'';
  const div=document.createElement('div');
  div.className='rap-punator-row';
  div.setAttribute('data-rap-pun',idx);
  div.style.gridTemplateColumns='2fr 1fr 1fr 1fr auto';
  div.innerHTML=`
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:6px">
      <input class="pun-emri" value="${p?.emri||''}" placeholder="Emri Mbiemri" ${dis} oninput="rapCalc()">
      <input class="pun-poz" value="${p?.pozicioni||''}" placeholder="Pozicioni" ${dis} oninput="rapCalc()">
    </div>
    <input class="pun-bruto" type="number" value="${p?.bruto||0}" placeholder="Bruto" ${dis} oninput="rapCalcPunRow(this,${idx})">
    <input class="pun-kontribute" type="number" value="${Math.round((p?.bruto||0)*0.167)}" placeholder="—" disabled style="opacity:0.6">
    <div style="display:flex;align-items:center;gap:6px">
      <select class="pun-statusi" ${dis} style="background:var(--s3);border:1px solid var(--border);border-radius:6px;padding:5px 8px;color:var(--text);font-size:0.72rem;outline:none;flex:1">
        <option ${(p?.statusi||'Paguar')==='Paguar'?'selected':''}>Paguar</option>
        <option ${p?.statusi==='Pending'?'selected':''}>Pending</option>
      </select>
    </div>
    ${!rapLocked?`<button class="rap-del-btn" onclick="this.closest('[data-rap-pun]').remove();rapCalc()">✕</button>`:'<span></span>'}`;
  container.appendChild(div);
}

function rapAddPunator(){
  if(rapLocked) return;
  rapAddPunatorRow({emri:'',pozicioni:'',bruto:0,statusi:'Paguar'}, rapPunCount++);
}

function rapCalcPunRow(input, idx){
  const row=input.closest('[data-rap-pun]');
  if(!row) return;
  const bruto=parseFloat(input.value)||0;
  const c=calcPaga(bruto);
  const kontEl=row.querySelector('.pun-kontribute');
  if(kontEl) kontEl.value=Math.round(c.kontPunedh);
  rapCalc();
}

function rapGetPunonjesit(){
  const rows=document.querySelectorAll('[data-rap-pun]');
  return [...rows].map(row=>({
    emri:row.querySelector('.pun-emri')?.value||'',
    pozicioni:row.querySelector('.pun-poz')?.value||'',
    bruto:parseFloat(row.querySelector('.pun-bruto')?.value)||0,
    statusi:row.querySelector('.pun-statusi')?.value||'Paguar',
  })).filter(p=>p.emri);
}

function saveRaport(){
  if(rapLocked){showToast('⚠️ Raporti është i mbyllur! Hap për modifikim.','⚠️');return;}
  const r={
    shitje_mat:n('rap-shitje-mat'), shitje_she:n('rap-shitje-she'), ardhura_tjera:n('rap-ardhura-tjera'),
    blerje_mat:n('rap-blerje-mat'), blerje_paj:n('rap-blerje-paj'), blerje_tjera:n('rap-blerje-tjera'),
    qira:n('rap-qira'), karb:n('rap-karb'), energji:n('rap-energji'),
    mirembajt:n('rap-mirembajt'), telekom:n('rap-telekom'), shp_tjera:n('rap-shp-tjera'),
    arka_fillim:n('rap-arka-fillim'), arka_fund:n('rap-arka-fund'),
    banka:n('rap-banka'), detyrime:n('rap-detyrime'),
    stok_fillim:n('rap-stok-fillim'), stok_fund:n('rap-stok-fund'),
    stok_kritik:n('rap-stok-kritik'), stok_total_art:n('rap-stok-total-art'),
    shenime:document.getElementById('rap-shenime')?.value||'',
    objektivat:document.getElementById('rap-objektivat')?.value||'',
    vleresim:document.getElementById('rap-vleresim')?.value||'mire',
    punonjesit:rapGetPunonjesit(),
    locked:false, savedAt:new Date().toISOString()
  };
  if(!state.raportet) state.raportet={};
  state.raportet[getRapKey()]=r;
  getCurrentSubj().data=state; saveSubjects();
  showToast(`✅ Raporti ${MUAJT[parseInt(rapMonth)-1]} ${rapYear} u ruajt!`,'🗓️');
  const hint=document.getElementById('rap-save-hint');
  if(hint) hint.textContent='✅ Ruajtur — '+new Date().toLocaleTimeString('sq-AL',{hour:'2-digit',minute:'2-digit'});
  renderRapHistory();
  renderRapCharts();
}

function rapAutoFill(){
  if(rapLocked){showToast('⚠️ Hap raportin për modifikim!','⚠️');return;}
  // Pull from current state data for this month
  const prefix=rapYear+'-'+rapMonth;
  const shitjet=(state.shitje||[]).filter(s=>s.data&&s.data.startsWith(prefix));
  const shitjeVal=shitjet.filter(s=>s.lloji==='Shitje').reduce((a,s)=>a+s.total,0);
  const blerjeVal=shitjet.filter(s=>s.lloji==='Blerje').reduce((a,s)=>a+s.total,0);
  const shp=(state.shpenzime||[]).filter(s=>s.data&&s.data.startsWith(prefix));
  const qira=shp.filter(s=>s.kategoria==='Qira').reduce((a,s)=>a+s.vlera,0);
  const karb=shp.filter(s=>s.kategoria==='Transport').reduce((a,s)=>a+s.vlera,0);
  const tele=shp.filter(s=>s.kategoria==='Komunikim').reduce((a,s)=>a+s.vlera,0);
  const tjera=shp.filter(s=>!['Qira','Transport','Komunikim','Paga','Blerje Mallrash'].includes(s.kategoria)).reduce((a,s)=>a+s.vlera,0);
  const stokVlera=state.materiale.reduce((s,m)=>s+m.sasia*m.cmBlerje,0)+state.pajisje.reduce((s,p)=>s+p.vlera,0);
  const stokKritik=state.materiale.filter(m=>m.status==='Stok Kritik').length;
  const punAktiv=(state.punonjesit||[]).filter(p=>p.status==='Aktiv');

  const set=(id,v)=>{const el=document.getElementById(id);if(el)el.value=v||0;};
  set('rap-shitje-mat',shitjeVal);
  set('rap-blerje-mat',blerjeVal);
  set('rap-qira',qira);
  set('rap-karb',karb);
  set('rap-telekom',tele);
  set('rap-shp-tjera',tjera);
  set('rap-stok-fund',stokVlera);
  set('rap-stok-kritik',stokKritik);
  set('rap-stok-total-art',state.materiale.length);

  // Auto-load punonjesit
  if(punAktiv.length>0){
    const container=document.getElementById('rap-punonjesit-list');
    if(container){
      container.innerHTML='';
      punAktiv.forEach((p,i)=>rapAddPunatorRow({emri:p.emri,pozicioni:p.pozicioni,bruto:p.pagaBruto,statusi:'Paguar'},i));
    }
  }
  rapCalc();
  showToast('🔄 U plotësua automatikisht nga të dhënat aktuale!','✅');
}

function renderRapHistory(){
  const strip=document.getElementById('rap-history-strip');
  if(!strip||!state.raportet) return;
  const keys=Object.keys(state.raportet).sort().reverse().slice(0,12);
  if(keys.length===0){strip.innerHTML=`<div style="color:var(--muted);font-size:0.8rem;grid-column:1/-1">Nuk ka raporte të ruajtura ende. Plotëso dhe ruaj raportin e muajit!</div>`;return;}
  strip.innerHTML=keys.map(key=>{
    const r=state.raportet[key];
    const [y,m]=key.split('-');
    const ardhura=(r.shitje_mat||0)+(r.shitje_she||0)+(r.ardhura_tjera||0);
    const shp=(r.qira||0)+(r.karb||0)+(r.energji||0)+(r.mirembajt||0)+(r.telekom||0)+(r.shp_tjera||0);
    const pagat=(r.punonjesit||[]).reduce((s,p)=>s+calcPaga(p.bruto||0).kostoTotale,0);
    const fitim=ardhura-shp-pagat;
    const vmap={'shkelqyer':'⭐⭐⭐','mire':'⭐⭐','mesatar':'⭐','dobet':'⚠️'};
    const isActive=key===getRapKey();
    return `<div class="rap-hist-card ${isActive?'active':''}" onclick="rapYear='${y}';rapMonth='${m}';renderRaporti()">
      <div class="rap-hist-month">${MUAJT[parseInt(m)-1].substring(0,3).toUpperCase()} ${y}</div>
      <div class="rap-hist-val" style="color:${fitim>=0?'var(--green)':'var(--red)'}">${fitim>=0?'+':''}${fmt(fitim)}</div>
      <div style="display:flex;justify-content:space-between;align-items:center;margin-top:4px">
        <span style="font-size:0.62rem;color:var(--muted)">${vmap[r.vleresim]||'—'}</span>
        ${r.locked?'<span style="font-size:0.6rem;color:var(--green)">🔒</span>':'<span style="font-size:0.6rem;color:var(--orange)">✏️</span>'}
      </div>
    </div>`;
  }).join('');
}

function renderRapCharts(){
  if(!window.Chart||!state.raportet) return;
  const keys=Object.keys(state.raportet).sort().slice(-12);
  const labels=keys.map(k=>{const[y,m]=k.split('-');return MUAJT[parseInt(m)-1].substring(0,3)+' '+y.slice(2);});
  const ardhurat=keys.map(k=>{const r=state.raportet[k];return (r.shitje_mat||0)+(r.shitje_she||0)+(r.ardhura_tjera||0);});
  const shpenzimet=keys.map(k=>{const r=state.raportet[k];const pagat=(r.punonjesit||[]).reduce((s,p)=>s+calcPaga(p.bruto||0).kostoTotale,0);return (r.qira||0)+(r.karb||0)+(r.energji||0)+(r.mirembajt||0)+(r.telekom||0)+(r.shp_tjera||0)+pagat;});
  const fitimi=keys.map((k,i)=>ardhurat[i]-shpenzimet[i]);

  const copt={responsive:true,plugins:{legend:{labels:{color:'#7a8ba8',font:{size:11}}}},scales:{x:{grid:{color:'rgba(255,255,255,0.04)'},ticks:{color:'#7a8ba8',font:{size:10}}},y:{grid:{color:'rgba(255,255,255,0.04)'},ticks:{color:'#7a8ba8',font:{size:10},callback:v=>v>=1000000?(v/1000000).toFixed(1)+'M':v>=1000?(v/1000).toFixed(0)+'K':v}}}};

  // Main chart
  const ctxM=document.getElementById('rap-chart-main');
  if(ctxM){
    if(rapChartMain) rapChartMain.destroy();
    rapChartMain=new Chart(ctxM,{type:'bar',data:{labels,datasets:[
      {label:'Të Ardhura',data:ardhurat,backgroundColor:'rgba(34,197,94,0.25)',borderColor:'#22c55e',borderWidth:2,borderRadius:4},
      {label:'Shpenzime',data:shpenzimet,backgroundColor:'rgba(239,68,68,0.25)',borderColor:'#ef4444',borderWidth:2,borderRadius:4},
      {label:'Fitimi Neto',data:fitimi,type:'line',borderColor:'#f97316',backgroundColor:'rgba(249,115,22,0.1)',borderWidth:2.5,pointRadius:4,tension:0.3,fill:true},
    ]},options:{...copt,plugins:{...copt.plugins,title:{display:false}}}});
  }

  // Shpenzime pie (last month)
  const ctxS=document.getElementById('rap-chart-shp');
  const r=getRap();
  if(ctxS&&r){
    const pagat2=(r.punonjesit||[]).reduce((s,p)=>s+calcPaga(p.bruto||0).kostoTotale,0);
    const shpData=[r.qira||0,r.karb||0,r.energji||0,r.mirembajt||0,r.telekom||0,r.shp_tjera||0,pagat2];
    const shpLabels=['Qira','Karburant','Energji','Mirëmbajtje','Telekom','Të tjera','Pagat'];
    const shpColors=['#f97316','#3b82f6','#eab308','#a855f7','#06b6d4','#7a8ba8','#ef4444'];
    if(rapChartShp) rapChartShp.destroy();
    rapChartShp=new Chart(ctxS,{type:'doughnut',data:{labels:shpLabels,datasets:[{data:shpData,backgroundColor:shpColors.map(c=>c+'55'),borderColor:shpColors,borderWidth:2}]},options:{responsive:true,plugins:{legend:{position:'right',labels:{color:'#7a8ba8',font:{size:10},boxWidth:12}}}}});
  }

  // Trend line
  const ctxT=document.getElementById('rap-chart-trend');
  if(ctxT){
    if(rapChartTrend) rapChartTrend.destroy();
    rapChartTrend=new Chart(ctxT,{type:'line',data:{labels,datasets:[
      {label:'Fitimi Neto',data:fitimi,borderColor:'#f97316',backgroundColor:'rgba(249,115,22,0.08)',borderWidth:2.5,pointRadius:5,pointBackgroundColor:fitimi.map(v=>v>=0?'#22c55e':'#ef4444'),tension:0.35,fill:true},
    ]},options:{...copt,plugins:{...copt.plugins}}});
  }
}

function exportRapCSV(){
  const r=getRap();
  if(!r||Object.keys(r).length===0){showToast('Nuk ka të dhëna për eksportim!','⚠️');return;}
  const muaji=MUAJT[parseInt(rapMonth)-1]+' '+rapYear;
  const ardhura=(r.shitje_mat||0)+(r.shitje_she||0)+(r.ardhura_tjera||0);
  const shp=(r.qira||0)+(r.karb||0)+(r.energji||0)+(r.mirembajt||0)+(r.telekom||0)+(r.shp_tjera||0);
  const pagat=(r.punonjesit||[]).reduce((s,p)=>s+calcPaga(p.bruto||0).kostoTotale,0);
  const fitim=ardhura-shp-pagat;
  let csv=`Raporti Mujor — ${muaji}\n\nKATEGORIA,VLERA (L)\n`;
  csv+=`Shitje Materiale,${r.shitje_mat||0}\n`;
  csv+=`Shitje Shërbime,${r.shitje_she||0}\n`;
  csv+=`Të Ardhura Tjera,${r.ardhura_tjera||0}\n`;
  csv+=`TOTAL TË ARDHURA,${ardhura}\n\n`;
  csv+=`Blerje Materiale,${r.blerje_mat||0}\n`;
  csv+=`Blerje Pajisje,${r.blerje_paj||0}\n`;
  csv+=`Qira,${r.qira||0}\n`;
  csv+=`Karburant,${r.karb||0}\n`;
  csv+=`Pagat (kosto totale),${pagat}\n`;
  csv+=`TOTAL SHPENZIME,${shp+pagat}\n\n`;
  csv+=`FITIMI NETO,${fitim}\n\n`;
  csv+=`\nPUNONJËSIT\nEMRI,POZICIONI,PAGA BRUTO,STATUSI\n`;
  (r.punonjesit||[]).forEach(p=>{ csv+=`${p.emri},${p.pozicioni},${p.bruto||0},${p.statusi}\n`; });
  const blob=new Blob([csv],{type:'text/csv;charset=utf-8'});
  const a=document.createElement('a');
  a.href=URL.createObjectURL(blob);
  a.download=`raport_${rapYear}_${rapMonth}.csv`;
  a.click();
  showToast('📥 CSV u shkarkua!','📥');
}

function printRaport(){
  const r=getRap();
  const muaji=MUAJT[parseInt(rapMonth)-1]+' '+rapYear;
  const ardhura=(r.shitje_mat||0)+(r.shitje_she||0)+(r.ardhura_tjera||0);
  const shp=(r.qira||0)+(r.karb||0)+(r.energji||0)+(r.mirembajt||0)+(r.telekom||0)+(r.shp_tjera||0);
  const pagat=(r.punonjesit||[]).reduce((s,p)=>s+calcPaga(p.bruto||0).kostoTotale,0);
  const fitim=ardhura-shp-pagat;
  const blerje=(r.blerje_mat||0)+(r.blerje_paj||0)+(r.blerje_tjera||0);
  const subj=getCurrentSubj();
  const vmap={'shkelqyer':'⭐⭐⭐ Shkëlqyer','mire':'⭐⭐ Mirë','mesatar':'⭐ Mesatar','dobet':'⚠️ Dobët'};
  const html = `<!DOCTYPE html><html><head><meta charset="UTF-8"><title>Raport Mujor ${muaji}</title>
  <style>
    body{font-family:'Segoe UI',sans-serif;color:#1a1a1a;padding:40px;max-width:900px;margin:0 auto;font-size:0.9rem}
    h1{font-size:1.8rem;color:#f97316;margin:0}h2{font-size:1rem;color:#6b7280;margin:4px 0 20px;font-weight:400}
    .grid2{display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-bottom:20px}
    .box{background:#f9fafb;border:1px solid #e5e7eb;border-radius:10px;padding:16px}
    .box-title{font-size:0.7rem;text-transform:uppercase;letter-spacing:0.1em;color:#9ca3af;margin-bottom:10px;font-weight:700}
    .row{display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid #e5e7eb;font-size:0.85rem}
    .row:last-child{border:none}
    .total{display:flex;justify-content:space-between;padding:8px 0;font-weight:700;font-size:0.95rem;margin-top:4px}
    .fitim-box{background:#fff7ed;border:2px solid #f97316;border-radius:10px;padding:20px;text-align:center;margin:20px 0}
    .fitim-val{font-size:2.5rem;font-weight:700;color:${fitim>=0?'#22c55e':'#ef4444'}}
    table{width:100%;border-collapse:collapse;font-size:0.85rem}
    th{background:#f97316;color:#fff;padding:8px 12px;text-align:left;font-size:0.75rem}
    td{padding:8px 12px;border-bottom:1px solid #e5e7eb}
    @media print{body{padding:20px}}
  </style></head><body>
  <h1>🏗️ ${subj.emri}</h1>
  <h2>Raport Mujor i Biznesit — ${muaji} &nbsp;|&nbsp; ${vmap[r.vleresim]||'—'}</h2>
  <div class="fitim-box">
    <div style="font-size:0.75rem;text-transform:uppercase;color:#9ca3af;margin-bottom:6px">FITIMI NETO I MUAJIT</div>
    <div class="fitim-val">${Number(fitim).toLocaleString()} L</div>
    <div style="color:#6b7280;font-size:0.85rem;margin-top:6px">Të Ardhura: ${Number(ardhura).toLocaleString()} L &nbsp;|&nbsp; Shpenzime: ${Number(shp+pagat).toLocaleString()} L</div>
  </div>
  <div class="grid2">
    <div class="box">
      <div class="box-title">💰 Të Ardhurat</div>
      <div class="row"><span>Shitje Materiale</span><span>${Number(r.shitje_mat||0).toLocaleString()} L</span></div>
      <div class="row"><span>Shitje Shërbime/Kontrata</span><span>${Number(r.shitje_she||0).toLocaleString()} L</span></div>
      <div class="row"><span>Të Ardhura Tjera</span><span>${Number(r.ardhura_tjera||0).toLocaleString()} L</span></div>
      <div class="total"><span>TOTAL</span><span style="color:#22c55e">${Number(ardhura).toLocaleString()} L</span></div>
    </div>
    <div class="box">
      <div class="box-title">💳 Shpenzimet Operative</div>
      <div class="row"><span>Qira</span><span>${Number(r.qira||0).toLocaleString()} L</span></div>
      <div class="row"><span>Karburant/Transport</span><span>${Number(r.karb||0).toLocaleString()} L</span></div>
      <div class="row"><span>Energji/Ujë</span><span>${Number(r.energji||0).toLocaleString()} L</span></div>
      <div class="row"><span>Mirëmbajtje</span><span>${Number(r.mirembajt||0).toLocaleString()} L</span></div>
      <div class="row"><span>Telefon/Internet</span><span>${Number(r.telekom||0).toLocaleString()} L</span></div>
      <div class="total"><span>TOTAL</span><span style="color:#ef4444">${Number(shp).toLocaleString()} L</span></div>
    </div>
  </div>
  <div class="box" style="margin-bottom:20px">
    <div class="box-title">👷 Punonjësit & Pagat — ${muaji}</div>
    <table><thead><tr><th>#</th><th>Emri & Mbiemri</th><th>Pozicioni</th><th>Paga Bruto</th><th>Kontribute</th><th>Paga Neto</th><th>Statusi</th></tr></thead>
    <tbody>${(r.punonjesit||[]).map((p,i)=>{const c=calcPaga(p.bruto||0);return `<tr><td>${i+1}</td><td>${p.emri}</td><td>${p.pozicioni}</td><td>${Number(p.bruto||0).toLocaleString()} L</td><td>${Number(c.kontPunedh).toLocaleString()} L</td><td>${Number(c.neto).toLocaleString()} L</td><td>${p.statusi}</td></tr>`;}).join('')}</tbody>
    <tfoot><tr><td colspan="3"><strong>Kosto Totale Pagave</strong></td><td colspan="4"><strong>${Number(pagat).toLocaleString()} L</strong></td></tr></tfoot>
    </table>
  </div>
  ${r.shenime?`<div class="box" style="margin-bottom:20px"><div class="box-title">📝 Shënime</div><p style="margin:0;color:#374151">${r.shenime}</p></div>`:''}
  ${r.objektivat?`<div class="box"><div class="box-title">🎯 Objektivat për Muajin Tjetër</div><p style="margin:0;color:#374151">${r.objektivat}</p></div>`:''}
  <div style="margin-top:30px;text-align:center;color:#9ca3af;font-size:0.75rem;border-top:1px solid #e5e7eb;padding-top:12px">Gjeneruar nga BuildTrack v10 — ${new Date().toLocaleDateString('sq-AL')}</div>
  </body></html>`;
  const _blob2 = new Blob([html], {type:'text/html;charset=utf-8'});
  const _url2 = URL.createObjectURL(_blob2);
  const _win2 = window.open(_url2, '_blank');
  if(!_win2){ const _a=document.createElement('a'); _a.href=_url2; _a.target='_blank'; document.body.appendChild(_a); _a.click(); _a.remove(); }
  setTimeout(()=>URL.revokeObjectURL(_url2), 15000);
}

// ═══════════════════════════════════════════════
// EXCEL IMPORT SYSTEM
// ═══════════════════════════════════════════════
let impWorkbook = null;
let impSheetName = null;
let impRows = [];
let impHeaders = [];
let impType = 'materiale';
let impMappedData = [];

// Fushat e kërkuara për çdo tip
const IMP_FIELDS = {
  materiale: [
    {key:'emri',     label:'Emri Materialit',    req:true},
    {key:'kategori', label:'Kategoria',           req:false},
    {key:'njesia',   label:'Njësia (kg/m/copë)',  req:false},
    {key:'sasia',    label:'Sasia',               req:false},
    {key:'min',      label:'Sasia Minimale',      req:false},
    {key:'cmBlerje', label:'Çmimi Blerje (L)',    req:false},
    {key:'cmShitje', label:'Çmimi Shitje (L)',    req:false},
    {key:'furnitori',label:'Furnitori',           req:false},
  ],
  shitje: [
    {key:'data',     label:'Data',                req:true},
    {key:'artikull', label:'Artikulli/Materiali', req:true},
    {key:'lloji',    label:'Lloji (Shitje/Blerje)',req:false},
    {key:'sasia',    label:'Sasia',               req:false},
    {key:'cmUnit',   label:'Çmimi/Njësi (L)',     req:false},
    {key:'total',    label:'Total (L)',            req:false},
    {key:'klienti',  label:'Klienti/Furnitori',   req:false},
  ],
  shpenzime: [
    {key:'data',        label:'Data',             req:true},
    {key:'pershkrimi',  label:'Përshkrimi',       req:true},
    {key:'kategoria',   label:'Kategoria',        req:false},
    {key:'vlera',       label:'Vlera (L)',         req:true},
    {key:'tvsh',        label:'Me TVSH? (po/jo)', req:false},
  ],
  faturat: [
    {key:'nr',       label:'Nr. Faturës',          req:false},
    {key:'data',     label:'Data',                 req:true},
    {key:'klienti',  label:'Klienti',              req:true},
    {key:'nipt',     label:'NIPT Klienti',         req:false},
    {key:'projekti', label:'Projekti',             req:false},
    {key:'total',    label:'Total (L)',             req:false},
    {key:'statusi',  label:'Statusi',              req:false},
    {key:'skadon',   label:'Data Skadimit',        req:false},
  ],
};

// Sugjerime automatike — emra të zakonshëm të kolonave
const IMP_AUTO = {
  emri:       ['emri','name','emër','artikull','material','pershkrimi','description','produkt','mallra'],
  kategori:   ['kategori','kategoria','category','tip','type','lloji'],
  njesia:     ['njesia','njësia','unit','një','um','masë'],
  sasia:      ['sasia','qty','quantity','sasi','amount','shuma','stok','stock'],
  min:        ['min','minimum','min stok','stok min','minimale'],
  cmBlerje:   ['çmimi blerje','cmimi blerje','çmim blerje','blerje','cost','purchase price','çmim bleje','price in','çmimi'],
  cmShitje:   ['çmimi shitje','cmimi shitje','çmim shitje','shitje price','sale price','çmim shes','selling price'],
  furnitori:  ['furnitori','supplier','furnizuesi','vendor'],
  data:       ['data','date','dt','datë','tarikhu'],
  artikull:   ['artikull','item','produkt','mall','material','emri','name','description'],
  lloji:      ['lloji','type','tip','kategoria','lloj'],
  cmUnit:     ['çmim','çmimi','cmimi','unit price','çmim/njësi','price','vlera','cmim'],
  total:      ['total','shuma','totali','vlera totale','grand total','sum'],
  klienti:    ['klienti','client','customer','furnitori','vendor','partner'],
  pershkrimi: ['pershkrimi','përshkrimi','description','emri','name','shpenzim','shënim'],
  kategoria:  ['kategoria','category','tip','lloji','type'],
  vlera:      ['vlera','value','amount','shuma','total','çmimi','price','vlera(l)','vlera (l)'],
  tvsh:       ['tvsh','vat','tax','tatim','taksë'],
  nr:         ['nr','number','numri','fatura nr','invoice no','nr fature'],
  nipt:       ['nipt','nid','tax id','id'],
  projekti:   ['projekti','project','kantieri','punë'],
  statusi:    ['statusi','status','gjendja','state'],
  skadon:     ['skadon','due date','afati','expiry','skadenca'],
};

function openExcelImport(){
  document.getElementById('excel-modal-overlay').classList.add('open');
  resetExcelImport();
}
function closeExcelImport(){
  document.getElementById('excel-modal-overlay').classList.remove('open');
}

function resetExcelImport(){
  impWorkbook=null; impSheetName=null; impRows=[]; impHeaders=[]; impMappedData=[];
  document.getElementById('imp-step1').style.display='';
  document.getElementById('imp-step2').style.display='none';
  document.getElementById('imp-confirm-btn').style.display='none';
  document.getElementById('imp-result-preview').style.display='none';
  document.getElementById('excel-file-input').value='';
  // Reset drag state
  const dz=document.getElementById('imp-drop-zone');
  if(dz) dz.classList.remove('dragover');
}

// Drag & drop
document.addEventListener('DOMContentLoaded',()=>{
  const dz=document.getElementById('imp-drop-zone');
  if(!dz) return;
  dz.addEventListener('dragover',e=>{e.preventDefault();dz.classList.add('dragover');});
  dz.addEventListener('dragleave',()=>dz.classList.remove('dragover'));
  dz.addEventListener('drop',e=>{
    e.preventDefault(); dz.classList.remove('dragover');
    const f=e.dataTransfer?.files[0];
    if(f) processExcelFile(f);
  });
});

function handleExcelFile(e){
  const f=e.target.files[0];
  if(f) processExcelFile(f);
}

function processExcelFile(file){
  const ext=file.name.split('.').pop().toLowerCase();
  const reader=new FileReader();
  reader.onload=e=>{
    try{
      let wb;
      if(ext==='csv'){
        // CSV: parse manually
        const text=e.target.result;
        wb=XLSX.read(text,{type:'string'});
      } else {
        wb=XLSX.read(e.target.result,{type:'array'});
      }
      impWorkbook=wb;
      showStep2(file.name, wb);
    }catch(err){
      showToast('⛔ Gabim në leximin e skedarit: '+err.message,'⛔');
    }
  };
  if(ext==='csv') reader.readAsText(file);
  else reader.readAsArrayBuffer(file);
}

function showStep2(filename, wb){
  document.getElementById('imp-step1').style.display='none';
  document.getElementById('imp-step2').style.display='';
  document.getElementById('imp-file-info').innerHTML=`📄 <strong style="color:var(--text)">${filename}</strong> &nbsp;·&nbsp; <span style="color:var(--muted)">${wb.SheetNames.length} sheet(s)</span>`;

  // Sheet selector
  const wrap=document.getElementById('imp-sheets-wrap');
  const sel=document.getElementById('imp-sheet-sel');
  if(wb.SheetNames.length>1){
    wrap.style.display='';
    sel.innerHTML=wb.SheetNames.map((n,i)=>
      `<button class="imp-sheet-btn ${i===0?'active':''}" onclick="selectSheet('${n}',this)">${n}</button>`
    ).join('');
  } else {
    wrap.style.display='none';
  }
  impSheetName=wb.SheetNames[0];
  loadSheetData();
}

function selectSheet(name, el){
  impSheetName=name;
  document.querySelectorAll('.imp-sheet-btn').forEach(b=>b.classList.remove('active'));
  el.classList.add('active');
  loadSheetData();
}

function loadSheetData(){
  if(!impWorkbook||!impSheetName) return;
  const ws=impWorkbook.Sheets[impSheetName];
  const data=XLSX.utils.sheet_to_json(ws,{header:1,defval:''});
  if(!data||data.length<2){showToast('⚠️ Sheet-i është bosh ose ka vetëm header!','⚠️');return;}

  // First non-empty row = headers
  let hdrIdx=0;
  for(let i=0;i<Math.min(5,data.length);i++){
    if(data[i].some(c=>c!=='')){ hdrIdx=i; break; }
  }
  impHeaders=data[hdrIdx].map((h,i)=>h!==''?String(h).trim():`Kolona ${i+1}`);
  impRows=data.slice(hdrIdx+1).filter(r=>r.some(c=>c!=='')).map(r=>{
    const obj={};
    impHeaders.forEach((h,i)=>obj[h]=r[i]!==undefined?String(r[i]).trim():'');
    return obj;
  });

  renderPreview();
  renderMapping();
}

function renderPreview(){
  const head=document.getElementById('imp-preview-head');
  const body=document.getElementById('imp-preview-body');
  if(!head||!body) return;
  head.innerHTML=`<tr>${impHeaders.map(h=>`<th>${h}</th>`).join('')}</tr>`;
  const rows=impRows.slice(0,5);
  body.innerHTML=rows.map(r=>`<tr>${impHeaders.map(h=>`<td>${r[h]||''}</td>`).join('')}</tr>`).join('');
}

function autoMatch(header){
  const h=header.toLowerCase().trim();
  for(const [field,hints] of Object.entries(IMP_AUTO)){
    if(hints.some(hint=>h===hint||h.includes(hint)||hint.includes(h))) return field;
  }
  return '';
}

function setImpType(type, el){
  impType=type;
  document.querySelectorAll('.imp-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  renderMapping();
  document.getElementById('imp-result-preview').style.display='none';
  document.getElementById('imp-confirm-btn').style.display='none';
}

function renderMapping(){
  const fields=IMP_FIELDS[impType]||[];
  const cont=document.getElementById('imp-mapping-rows');
  if(!cont) return;
  cont.innerHTML=fields.map(f=>{
    const auto=impHeaders.find(h=>autoMatch(h)===f.key)||'';
    const opts=`<option value="">— Mos importo —</option>`+
      impHeaders.map(h=>`<option value="${h}" ${h===auto?'selected':''}>${h}</option>`).join('');
    return `<div class="imp-map-row">
      <div class="imp-col-label" title="${auto||'pa selektim'}">${auto||'<span style="opacity:0.4">— zgjidh kolonën —</span>'}</div>
      <div class="imp-arrow">→</div>
      <select id="imp-map-${f.key}" onchange="updateMapLabel(this,'${f.key}')">
        ${opts}
      </select>
    </div>
    <div style="font-size:0.65rem;color:var(--muted);text-align:right;margin-bottom:8px;margin-top:-4px">
      ${f.label} ${f.req?'<span style="color:var(--orange)">*</span>':''}
    </div>`;
  }).join('');
}

function updateMapLabel(sel, key){
  const row=sel.closest('.imp-map-row');
  const lbl=row?.querySelector('.imp-col-label');
  if(lbl) lbl.innerHTML=sel.value||'<span style="opacity:0.4">— zgjidh kolonën —</span>';
}

function getMapping(){
  const fields=IMP_FIELDS[impType]||[];
  const map={};
  fields.forEach(f=>{
    const sel=document.getElementById('imp-map-'+f.key);
    if(sel&&sel.value) map[f.key]=sel.value;
  });
  return map;
}

function parseVal(v){
  if(v===undefined||v===null||v==='') return '';
  const s=String(v).replace(/[,\s]/g,'').replace(/L$/,'').trim();
  const n=parseFloat(s);
  return isNaN(n)?s:n;
}
function parseNum(v){ const n=parseVal(v); return typeof n==='number'?n:parseFloat(n)||0; }
function parseBool(v){ return /po|yes|true|1|check/i.test(String(v)); }
function parseDate(v){
  if(!v) return '';
  // Try ISO first
  if(/^\d{4}-\d{2}-\d{2}/.test(String(v))) return String(v).slice(0,10);
  // Excel serial number
  if(typeof v==='number'||/^\d+$/.test(String(v))){
    const d=XLSX.SSF.parse_date_code(Number(v));
    if(d) return `${d.y}-${String(d.m).padStart(2,'0')}-${String(d.d).padStart(2,'0')}`;
  }
  // Try parse
  const d=new Date(String(v));
  if(!isNaN(d)) return d.toISOString().slice(0,10);
  return String(v);
}

function previewImport(){
  const map=getMapping();
  const fields=IMP_FIELDS[impType]||[];
  const reqFields=fields.filter(f=>f.req);
  const missing=reqFields.filter(f=>!map[f.key]).map(f=>f.label);
  const box=document.getElementById('imp-result-preview');

  if(missing.length>0){
    box.style.display='';
    box.innerHTML=`<div class="imp-stat"><span class="err">⛔</span> Mungojnë fushat e detyrueshme: <strong style="color:var(--red)">${missing.join(', ')}</strong></div>`;
    document.getElementById('imp-confirm-btn').style.display='none';
    return;
  }

  // Build preview data
  impMappedData=[];
  let skipped=0;

  impRows.forEach((row,ri)=>{
    try{
      let item={id:Date.now()+ri+Math.random()};
      if(impType==='materiale'){
        const emri=String(row[map.emri]||'').trim();
        if(!emri){skipped++;return;}
        const sas=parseNum(row[map.sasia]);
        const min=parseNum(row[map.min]);
        const cmB=parseNum(row[map.cmBlerje]);
        item={...item, emri,
          kategori:row[map.kategori]||'Tjetër',
          njesia:row[map.njesia]||'copë',
          sasia:sas, min:min||0,
          cmBlerje:cmB, cmShitje:parseNum(row[map.cmShitje])||cmB*1.2,
          furnitori:row[map.furnitori]||'—',
          status:sas===0?'Stok Kritik':sas<min?'Stok Kritik':sas<min*1.5?'Stok i Ulët':'Stok Normal'};
      } else if(impType==='shitje'){
        const art=String(row[map.artikull]||'').trim();
        if(!art){skipped++;return;}
        const sas=parseNum(row[map.sasia])||1;
        const cm=parseNum(row[map.cmUnit]);
        const tot=parseNum(row[map.total])||sas*cm;
        const lloji=String(row[map.lloji]||'Shitje').trim();
        item={...item, data:parseDate(row[map.data])||new Date().toISOString().slice(0,10),
          artikull:art,
          lloji:/blerje|purchase|buy/i.test(lloji)?'Blerje':'Shitje',
          sasia:sas, cmUnit:cm, total:tot,
          klienti:row[map.klienti]||'—', matId:null};
      } else if(impType==='shpenzime'){
        const per=String(row[map.pershkrimi]||'').trim();
        const vlera=parseNum(row[map.vlera]);
        if(!per||!vlera){skipped++;return;}
        item={...item, data:parseDate(row[map.data])||new Date().toISOString().slice(0,10),
          pershkrimi:per,
          kategoria:row[map.kategoria]||'Tjetër',
          vlera, tvsh:map.tvsh?parseBool(row[map.tvsh]):false};
      } else if(impType==='faturat'){
        const kli=String(row[map.klienti]||'').trim();
        if(!kli){skipped++;return;}
        const tot=parseNum(row[map.total]);
        const sub=Math.round(tot/1.2*100)/100;
        const nr=row[map.nr]||('FAT-IMP-'+String(state.faturat.length+impMappedData.length+1).padStart(3,'0'));
        item={...item, nr:String(nr),
          data:parseDate(row[map.data])||new Date().toISOString().slice(0,10),
          klienti:kli, nipt:row[map.nipt]||'',
          projekti:row[map.projekti]||'',
          statusi:row[map.statusi]||'Në Pritje',
          skadon:parseDate(row[map.skadon])||'',
          shenime:'',
          zerat:[{pershkrimi:'Importuar nga Excel',sasia:1,cmUnit:sub||tot,tvsh:!!tot&&tot>sub}]};
      }
      impMappedData.push(item);
    }catch(e){skipped++;}
  });

  // Show result
  box.style.display='';
  const dupCheck = impType==='materiale'?
    impMappedData.filter(m=>state.materiale.some(x=>x.emri.toLowerCase()===m.emri.toLowerCase())).length : 0;

  box.innerHTML=`
    <div class="imp-stat"><span class="ok">✅</span> <strong>${impMappedData.length}</strong> rreshta gati për import</div>
    ${skipped>0?`<div class="imp-stat"><span class="warn">⚠️</span> <strong>${skipped}</strong> rreshta u kapërcyen (të dhëna jo të plota)</div>`:''}
    ${dupCheck>0?`<div class="imp-stat"><span class="warn">⚠️</span> <strong>${dupCheck}</strong> materiale me emër identik ekzistojnë tashmë (do të shtohen sërish)</div>`:''}
    <div class="imp-stat" style="margin-top:4px;padding-top:8px;border-top:1px solid var(--border)">
      <span style="color:var(--muted)">Tip:</span> <strong>${{materiale:'📦 Materiale',shitje:'💰 Shitje & Blerje',shpenzime:'💳 Shpenzime',faturat:'🧾 Fatura'}[impType]}</strong>
      &nbsp;·&nbsp; <span style="color:var(--muted)">Do të shtohen mbi të dhënat ekzistuese</span>
    </div>`;

  if(impMappedData.length>0){
    document.getElementById('imp-confirm-btn').style.display='';
  }
}

function confirmImport(){
  if(!impMappedData.length){showToast('Nuk ka të dhëna për import!','⚠️');return;}
  migrateState(state);
  let count=0;
  if(impType==='materiale'){
    impMappedData.forEach(m=>{state.materiale.push(m);count++;});
  } else if(impType==='shitje'){
    impMappedData.forEach(s=>{state.shitje.push(s);count++;});
  } else if(impType==='shpenzime'){
    if(!state.shpenzime) state.shpenzime=[];
    impMappedData.forEach(s=>{state.shpenzime.push(s);count++;});
  } else if(impType==='faturat'){
    if(!state.faturat) state.faturat=[];
    impMappedData.forEach(f=>{state.faturat.push(f);count++;});
  }
  getCurrentSubj().data=state; saveSubjects(); render();
  closeExcelImport();
  showToast(`✅ ${count} rekorde u importuan me sukses nga Excel!`,'📊');

  // Navigate to relevant panel
  const panelMap={materiale:'materiale',shitje:'shitje',shpenzime:'bilanci',faturat:'faturat'};
  const target=panelMap[impType];
  if(target){
    const navBtns=document.querySelectorAll('.nav-item');
    navBtns.forEach(btn=>{
      if(btn.getAttribute('onclick')?.includes(`'${target}'`)){
        showPanel(target, btn);
      }
    });
  }
}

// ═══════════════════════════════════════════════
// GLOBAL SEARCH
// ═══════════════════════════════════════════════
let gsResults = [];
let gsSelected = -1;

function openGlobalSearch(){
  document.getElementById('gsearch-overlay').classList.add('open');
  setTimeout(()=>{ const inp=document.getElementById('gsearch-input'); inp.value=''; inp.focus(); },50);
  document.getElementById('gsearch-results').innerHTML=`<div class="gs-empty">Shkruaj për të kërkuar në të gjitha modulet...</div>`;
  gsResults=[]; gsSelected=-1;
}
function closeGlobalSearch(){
  document.getElementById('gsearch-overlay').classList.remove('open');
}
// Keyboard shortcut
document.addEventListener('keydown',e=>{
  if((e.ctrlKey||e.metaKey)&&e.key==='k'){ e.preventDefault(); openGlobalSearch(); }
  if(e.key==='Escape') closeGlobalSearch();
});
function gsearchKeydown(e){
  if(e.key==='ArrowDown'){ e.preventDefault(); gsMove(1); }
  else if(e.key==='ArrowUp'){ e.preventDefault(); gsMove(-1); }
  else if(e.key==='Enter'){ e.preventDefault(); gsOpen(); }
  else if(e.key==='Escape'){ closeGlobalSearch(); }
}
function gsMove(dir){
  const items=document.querySelectorAll('.gs-item');
  items.forEach(i=>i.classList.remove('sel'));
  gsSelected=Math.max(0,Math.min(items.length-1,gsSelected+dir));
  items[gsSelected]?.classList.add('sel');
  items[gsSelected]?.scrollIntoView({block:'nearest'});
}
function gsOpen(){
  const items=document.querySelectorAll('.gs-item');
  const sel=items[gsSelected]||items[0];
  if(sel) sel.click();
}

function highlight(text, q){
  if(!q||!text) return String(text||'');
  const re=new RegExp('('+q.replace(/[.*+?^${}()|[\]\\]/g,'\\$&')+')','gi');
  return String(text).replace(re,'<mark style="background:rgba(249,115,22,0.25);color:var(--orange);border-radius:2px">$1</mark>');
}

function runGlobalSearch(q){
  q=(q||'').trim();
  gsSelected=-1;
  const box=document.getElementById('gsearch-results');
  if(q.length<2){
    box.innerHTML=`<div class="gs-empty">Shkruaj të paktën 2 shkronja...</div>`;
    return;
  }
  const ql=q.toLowerCase();
  const results=[];

  // MATERIALE
  (state.materiale||[]).forEach(m=>{
    if([m.emri,m.kategori,m.furnitori,m.njesia].some(v=>String(v||'').toLowerCase().includes(ql))){
      results.push({type:'mat',icon:'📦',color:'#f97316',
        title:m.emri, sub:`${m.kategori} · Stok: ${m.sasia} ${m.njesia} · ${Number(m.cmShitje).toLocaleString()} L`,
        badge:m.status, badgeClass:m.status==='Stok Normal'?'green':m.status==='Stok i Ulët'?'yellow':'red',
        panel:'materiale', obj:m});
    }
  });

  // SHITJE
  (state.shitje||[]).forEach(s=>{
    if([s.artikull,s.klienti,s.lloji,s.data].some(v=>String(v||'').toLowerCase().includes(ql))){
      results.push({type:'sh',icon:'💰',color:'#22c55e',
        title:s.artikull||'—', sub:`${s.lloji} · ${s.data} · ${s.klienti||''} · ${Number(s.total).toLocaleString()} L`,
        badge:s.lloji, badgeClass:s.lloji==='Shitje'?'green':'blue',
        panel:'shitje', obj:s});
    }
  });

  // FATURAT
  (state.faturat||[]).forEach(f=>{
    if([f.nr,f.klienti,f.statusi,f.data,f.projekti].some(v=>String(v||'').toLowerCase().includes(ql))){
      const c=calcFatura(f);
      results.push({type:'fat',icon:'🧾',color:'#3b82f6',
        title:`${f.nr} — ${f.klienti}`, sub:`${f.data} · ${Number(c.total).toLocaleString()} L · ${f.statusi}`,
        badge:f.statusi, badgeClass:f.statusi==='Paguar'?'green':f.statusi==='Vonuar'?'red':'yellow',
        panel:'faturat', obj:f});
    }
  });

  // PUNONJESIT
  (state.punonjesit||[]).forEach(p=>{
    if([p.emri,p.pozicioni,p.status].some(v=>String(v||'').toLowerCase().includes(ql))){
      results.push({type:'pun',icon:'👷',color:'#a855f7',
        title:p.emri, sub:`${p.pozicioni} · Paga: ${Number(p.pagaBruto).toLocaleString()} L · ${p.status}`,
        badge:p.status, badgeClass:p.status==='Aktiv'?'green':'red',
        panel:'hr', obj:p});
    }
  });

  // SHPENZIME
  (state.shpenzime||[]).forEach(s=>{
    if([s.pershkrimi,s.kategoria,s.data].some(v=>String(v||'').toLowerCase().includes(ql))){
      results.push({type:'shp',icon:'💳',color:'#ef4444',
        title:s.pershkrimi||'—', sub:`${s.kategoria||''} · ${s.data} · ${Number(s.vlera).toLocaleString()} L`,
        badge:s.kategoria||'Shpenzim', badgeClass:'red',
        panel:'bilanci', obj:s});
    }
  });

  // OFERTAT
  (state.ofertat||[]).forEach(o=>{
    if([o.nr,o.klienti,o.sherbimi,o.statusi].some(v=>String(v||'').toLowerCase().includes(ql))){
      results.push({type:'ofe',icon:'📄',color:'#06b6d4',
        title:`${o.nr||'Ofertë'} — ${o.klienti}`, sub:`${o.sherbimi||''} · ${Number(o.vlera).toLocaleString()} L`,
        badge:o.statusi, badgeClass:o.statusi==='Pranuar'?'green':o.statusi==='Refuzuar'?'red':'blue',
        panel:'faturat', obj:o});
    }
  });

  gsResults=results;

  if(!results.length){
    box.innerHTML=`<div class="gs-empty">🔍 Nuk u gjet asgjë për "<strong>${q}</strong>"</div>`;
    return;
  }

  // Group by panel
  const groups={};
  const panelNames={mat:'📦 Materiale',sh:'💰 Shitje & Stok',fat:'🧾 Fatura',pun:'👷 Paga & HR',shp:'💳 Bilanci',ofe:'📄 Oferta'};
  results.forEach(r=>{ if(!groups[r.type]) groups[r.type]=[]; groups[r.type].push(r); });

  let html='';
  Object.entries(groups).forEach(([type,items])=>{
    html+=`<div class="gs-group-lbl">${panelNames[type]||type} (${items.length})</div>`;
    items.slice(0,6).forEach((r,i)=>{
      html+=`<div class="gs-item" onclick="gsNavigateTo('${r.panel}')">
        <div class="gs-icon" style="background:${r.color}18;color:${r.color}">${r.icon}</div>
        <div class="gs-main">
          <div class="gs-title">${highlight(r.title,q)}</div>
          <div class="gs-sub">${highlight(r.sub,q)}</div>
        </div>
        <span class="gs-badge ${r.badgeClass}">${r.badge}</span>
      </div>`;
    });
    if(items.length>6) html+=`<div style="padding:4px 12px 8px;font-size:0.7rem;color:var(--muted)">+ ${items.length-6} të tjera...</div>`;
  });

  html+=`<div style="padding:8px 12px;font-size:0.68rem;color:var(--muted);border-top:1px solid var(--border);margin-top:6px">
    ${results.length} rezultate totale
  </div>`;
  box.innerHTML=html;
}

function gsNavigateTo(panel){
  closeGlobalSearch();
  const navBtns=document.querySelectorAll('.nav-item');
  navBtns.forEach(btn=>{
    if(btn.getAttribute('onclick')?.includes(`'${panel}'`)) showPanel(panel, btn);
  });
}

// ── COMPANY INFO helper ──
function getSubjInfo(){
  return getCurrentSubj();
}

// ═══════════════════════════════════════════════════════
// BIBLIOTEKA E FORMATEVE
// ═══════════════════════════════════════════════════════

const BIB_BUILTINS = [
  {
    id:'bilanc_kontabel', icon:'📊', title:'Bilanc Kontabël', sub:'Aktiv · Pasiv · Kapitali',
    type:'XLSX', color:'#22c55e',
    autoFields:[
      {key:'emri_kompanise', label:'Emri Kompanisë', fn: ()=> getCurrentSubj().emri||''},
      {key:'nipt', label:'NIPT', fn: ()=> getCurrentSubj().nipt||''},
      {key:'totali_aktiv', label:'Vlera Stokut (Aktiv)', fn: ()=> (state.materiale||[]).reduce((a,m)=>a+(m.sasia*(m.cmBlerje||0)),0)},
      {key:'arketimet', label:'Arkëtimet nga Shitjet', fn: ()=> (state.shitje||[]).reduce((a,x)=>a+x.total,0)},
      {key:'shpenzimet', label:'Shpenzime Operative', fn: ()=> (state.shpenzime||[]).reduce((a,x)=>a+x.vlera,0)},
      {key:'pagat_totale', label:'Kosto Pagave', fn: ()=> (state.punonjesit||[]).reduce((a,p)=>{const c=calcPaga(p.bruto||0);return a+c.kostoTotale;},0)},
    ],
    manualFields:[
      {key:'periudha', label:'Periudha Raportuese', placeholder:'p.sh. Janar - Dhjetor 2024', type:'text'},
      {key:'data_raportit', label:'Data e Raportit', placeholder:'', type:'date'},
      {key:'kapitali_fillestar', label:'Kapitali Fillestar (L)', placeholder:'0', type:'number'},
      {key:'detyrimet_afatgjata', label:'Detyrimet Afatgjata (L)', placeholder:'0', type:'number'},
      {key:'huate_bankare', label:'Huatë Bankare (L)', placeholder:'0', type:'number'},
      {key:'kontabilist', label:'Kontabilist', placeholder:'Emri dhe mbiemri', type:'text'},
    ],
    generate: 'bilanc_kontabel'
  },
  {
    id:'raport_tatimor', icon:'🏛️', title:'Deklaratë Tatimore', sub:'TVSH · Tatim Fitimi · Kontribute',
    type:'XLSX', color:'#3b82f6',
    autoFields:[
      {key:'emri_kompanise', label:'Emri Kompanisë', fn: ()=> getCurrentSubj().emri||''},
      {key:'nipt', label:'NIPT', fn: ()=> getCurrentSubj().nipt||''},
      {key:'totali_shitjeve', label:'Totali Shitjeve (pa TVSH)', fn: ()=> (state.shitje||[]).reduce((a,x)=>a+x.total,0)},
      {key:'tvsh_mbledhur', label:'TVSH e Mbledhur (20%)', fn: ()=> (state.faturat||[]).reduce((a,f)=>{const c=calcFatura(f);return a+c.tvsh;},0)},
      {key:'tvsh_paguar', label:'TVSH e Paguar (Blerje)', fn: ()=> (state.shpenzime||[]).filter(x=>x.tvsh).reduce((a,x)=>a+x.vlera*0.20,0)},
      {key:'tatim_fitimi', label:'Tatim Fitimi (15%)', fn: ()=>{ const f=(state.shitje||[]).reduce((a,x)=>a+x.total,0)-(state.shpenzime||[]).reduce((a,x)=>a+x.vlera,0); return f>0?f*0.15:0; }},
      {key:'kontribute_total', label:'Kontribute Totale', fn: ()=> (state.punonjesit||[]).reduce((a,p)=>{const c=calcPaga(p.bruto||0);return a+c.kontPunetor+c.kontPunedh;},0)},
    ],
    manualFields:[
      {key:'periudha', label:'Periudha', placeholder:'T1 2024 / Janar 2024', type:'text'},
      {key:'data_dorezimit', label:'Data e Dorëzimit', placeholder:'', type:'date'},
      {key:'tvsh_import', label:'TVSH nga Importi (L)', placeholder:'0', type:'number'},
      {key:'perfaqesuesi', label:'Përfaqësuesi Ligjor', placeholder:'Emri', type:'text'},
    ],
    generate: 'raport_tatimor'
  },
  {
    id:'cash_flow', icon:'💵', title:'Cash Flow', sub:'Hyrje · Dalje · Pozicion Cash',
    type:'XLSX', color:'#f97316',
    autoFields:[
      {key:'emri_kompanise', label:'Emri Kompanisë', fn: ()=> getCurrentSubj().emri||''},
      {key:'hyrjet_shitje', label:'Hyrjet nga Shitjet', fn: ()=> (state.shitje||[]).filter(x=>x.lloji==='Shitje').reduce((a,x)=>a+x.total,0)},
      {key:'daljet_blerje', label:'Daljet për Blerje', fn: ()=> (state.shitje||[]).filter(x=>x.lloji==='Blerje').reduce((a,x)=>a+x.total,0)},
      {key:'daljet_shpenzime', label:'Daljet Shpenzime', fn: ()=> (state.shpenzime||[]).reduce((a,x)=>a+x.vlera,0)},
      {key:'daljet_paga', label:'Daljet Paga', fn: ()=> (state.punonjesit||[]).reduce((a,p)=>a+(p.bruto||0),0)},
      {key:'faturat_papaguara', label:'Arkëtime të Pritshme', fn: ()=> (state.faturat||[]).filter(f=>f.statusi!=='Paguar').reduce((a,f)=>{const c=calcFatura(f);return a+c.total;},0)},
    ],
    manualFields:[
      {key:'periudha', label:'Periudha', placeholder:'Q1 2024', type:'text'},
      {key:'data_raportit', label:'Data', placeholder:'', type:'date'},
      {key:'cash_fillestar', label:'Cash Fillestar (L)', placeholder:'0', type:'number'},
      {key:'investimet', label:'Investimet (L)', placeholder:'0', type:'number'},
      {key:'huate_marra', label:'Hua të Marra (L)', placeholder:'0', type:'number'},
    ],
    generate: 'cash_flow'
  },
  {
    id:'listepagese', icon:'👷', title:'Listë-Pagese', sub:'HR · Pagat · Kontributet Shqipëri',
    type:'XLSX', color:'#a855f7',
    autoFields:[
      {key:'emri_kompanise', label:'Emri Kompanisë', fn: ()=> getCurrentSubj().emri||''},
      {key:'nipt', label:'NIPT', fn: ()=> getCurrentSubj().nipt||''},
      {key:'nr_punonjesve', label:'Nr. Punonjësve', fn: ()=> (state.punonjesit||[]).length},
      {key:'paga_bruto_total', label:'Paga Bruto Totale', fn: ()=> (state.punonjesit||[]).reduce((a,p)=>a+(p.bruto||0),0)},
      {key:'kontribute_punetore', label:'Kontribute Punëtore (11.4%)', fn: ()=> (state.punonjesit||[]).reduce((a,p)=>a+calcPaga(p.bruto||0).kontPunetor,0)},
      {key:'kontribute_punedhenesit', label:'Kontribute Punëdhënës (16.7%)', fn: ()=> (state.punonjesit||[]).reduce((a,p)=>a+calcPaga(p.bruto||0).kontPunedh,0)},
      {key:'paga_neto_total', label:'Paga Neto Totale', fn: ()=> (state.punonjesit||[]).reduce((a,p)=>a+calcPaga(p.bruto||0).neto,0)},
      {key:'kosto_totale', label:'Kosto Totale e Punës', fn: ()=> (state.punonjesit||[]).reduce((a,p)=>a+calcPaga(p.bruto||0).kostoTotale,0)},
    ],
    manualFields:[
      {key:'muaji', label:'Muaji', placeholder:'p.sh. Janar 2025', type:'text'},
      {key:'data_pageses', label:'Data e Pagesës', placeholder:'', type:'date'},
      {key:'nr_konto', label:'Nr. Konto Bankare', placeholder:'AL...', type:'text'},
    ],
    generate: 'listepagese'
  },
  {
    id:'inventar_fizik', icon:'📦', title:'Inventar Fizik', sub:'Stok · Vlera · Statusi',
    type:'XLSX', color:'#eab308',
    autoFields:[
      {key:'emri_kompanise', label:'Emri Kompanisë', fn: ()=> getCurrentSubj().emri||''},
      {key:'nr_artikujve', label:'Nr. Artikujve', fn: ()=> (state.materiale||[]).length},
      {key:'vlera_stokut', label:'Vlera Totale Stokut', fn: ()=> (state.materiale||[]).reduce((a,m)=>a+(m.sasia*(m.cmBlerje||0)),0)},
      {key:'stok_kritik', label:'Artikuj Stok Kritik', fn: ()=> (state.materiale||[]).filter(m=>m.status==='Stok Kritik').length},
    ],
    manualFields:[
      {key:'data_inventarit', label:'Data e Inventarit', placeholder:'', type:'date'},
      {key:'kryer_nga', label:'Kryer nga', placeholder:'Emri dhe mbiemri', type:'text'},
      {key:'vendndodhja', label:'Vendndodhja / Magazina', placeholder:'p.sh. Magazina Kryesore', type:'text'},
    ],
    generate: 'inventar_fizik'
  },
  {
    id:'raport_projekti', icon:'📋', title:'Raport Projektesh', sub:'Kostos · Progresi · Faturimi',
    type:'XLSX', color:'#06b6d4',
    autoFields:[
      {key:'emri_kompanise', label:'Emri Kompanisë', fn: ()=> getCurrentSubj().emri||''},
      {key:'nr_projekteve', label:'Nr. Projekteve Aktive', fn: ()=> (state.projektet||[]).filter(p=>p.statusi==='Në Progres'||p.statusi==='Aktiv').length},
      {key:'vlera_totale_projekteve', label:'Vlera Totale Projekteve', fn: ()=> (state.projektet||[]).reduce((a,p)=>a+(parseFloat(p.vlera)||0),0)},
      {key:'faturat_projektet', label:'Faturuar Total', fn: ()=> (state.faturat||[]).reduce((a,f)=>{const c=calcFatura(f);return a+c.total;},0)},
    ],
    manualFields:[
      {key:'projekti_specific', label:'Emri Projektit', placeholder:'ose lër bosh për të gjitha', type:'text'},
      {key:'periudha', label:'Periudha', placeholder:'2024', type:'text'},
      {key:'data_raportit', label:'Data', placeholder:'', type:'date'},
      {key:'pergjegjesi', label:'Përgjegjësi', placeholder:'Emri', type:'text'},
    ],
    generate: 'raport_projekti'
  }
];

let bibCurrentBuiltin = null;
let bibUploadedFile   = null;
let bibUploadedFields = [];

function bibShowTab(tab){
  document.getElementById('bib-pane-templates').style.display = tab==='templates' ? '' : 'none';
  document.getElementById('bib-pane-builtins').style.display  = tab==='builtins'  ? '' : 'none';
  const tBtn=document.getElementById('bib-tab-templates');
  const bBtn=document.getElementById('bib-tab-builtins');
  if(tBtn){ tBtn.style.borderColor=tab==='templates'?'var(--orange)':''; tBtn.style.color=tab==='templates'?'var(--orange)':''; }
  if(bBtn){ bBtn.style.borderColor=tab==='builtins'?'var(--orange)':'';  bBtn.style.color=tab==='builtins'?'var(--orange)':''; }
  if(tab==='builtins') bibRenderBuiltins();
}

function bibRenderBuiltins(){
  const grid = document.getElementById('bib-builtins-grid');
  if(!grid) return;
  grid.innerHTML = BIB_BUILTINS.map(t=>`
    <div class="bib-card" onclick="bibSelectBuiltin('${t.id}')">
      <span class="bib-card-type">${t.type}</span>
      <div class="bib-card-icon">${t.icon}</div>
      <div class="bib-card-title">${t.title}</div>
      <div class="bib-card-sub">${t.sub}</div>
      <div style="margin-top:10px;height:3px;border-radius:99px;background:${t.color};opacity:0.7"></div>
    </div>`).join('');
}

function bibSelectBuiltin(id){
  const tpl = BIB_BUILTINS.find(t=>t.id===id);
  if(!tpl) return;
  bibCurrentBuiltin = tpl;
  document.getElementById('bib-builtins-grid').style.display='none';
  const fill = document.getElementById('bib-builtin-fill');
  fill.style.display='';
  document.getElementById('bib-builtin-title').textContent = tpl.icon+' '+tpl.title;

  const autoEl = document.getElementById('bib-builtin-auto');
  autoEl.innerHTML = tpl.autoFields.map(f=>{
    let val; try{ val=f.fn(); }catch(e){ val='—'; }
    const disp = typeof val==='number' ? fmt(val) : val;
    return `<div class="bib-fill-row">
      <div><div class="bib-field-label">${f.label}</div><div class="bib-field-auto">✓ Auto nga BuildTrack</div></div>
      <div style="font-size:0.82rem;font-weight:600;color:var(--text);text-align:right">${disp}</div>
    </div>`;
  }).join('');

  const manEl = document.getElementById('bib-builtin-manual');
  manEl.innerHTML = tpl.manualFields.map(f=>`
    <div class="bib-fill-row">
      <div class="bib-field-label">${f.label}</div>
      <input id="bib-m-${f.key}" type="${f.type||'text'}" placeholder="${f.placeholder||''}"
        style="background:var(--s1);border:1px solid var(--border);border-radius:7px;padding:7px 10px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.8rem;width:100%;outline:none;transition:border-color 0.2s"
        onfocus="this.style.borderColor='var(--orange)'" onblur="this.style.borderColor='var(--border)'">
    </div>`).join('');
}

function bibBuiltinBack(){
  document.getElementById('bib-builtins-grid').style.display='';
  document.getElementById('bib-builtin-fill').style.display='none';
  bibCurrentBuiltin=null;
}

function bibBuiltinGenerate(){
  if(!bibCurrentBuiltin) return;
  const tpl = bibCurrentBuiltin;
  const data = {};
  tpl.autoFields.forEach(f=>{ try{ data[f.key]=f.fn(); }catch(e){ data[f.key]=0; } });
  tpl.manualFields.forEach(f=>{
    const el=document.getElementById('bib-m-'+f.key);
    data[f.key] = el ? (f.type==='number'?parseFloat(el.value)||0 : el.value) : '';
  });
  bibGenerateXLSX(tpl, data);
}

function bibGenerateXLSX(tpl, data){
  let wb;
  if(tpl.generate==='bilanc_kontabel')   wb=bibBuildBilanc(data,getCurrentSubj());
  else if(tpl.generate==='raport_tatimor') wb=bibBuildTatimor(data,getCurrentSubj());
  else if(tpl.generate==='cash_flow')    wb=bibBuildCashFlow(data,getCurrentSubj());
  else if(tpl.generate==='listepagese')  wb=bibBuildListePagese(data,getCurrentSubj());
  else if(tpl.generate==='inventar_fizik') wb=bibBuildInventar(data,getCurrentSubj());
  else if(tpl.generate==='raport_projekti') wb=bibBuildProjekt(data,getCurrentSubj());
  else { showToast('Template i panjohur','❌'); return; }

  const out  = XLSX.write(wb,{bookType:'xlsx',type:'array'});
  const blob = new Blob([out],{type:'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = tpl.title.replace(/\s+/g,'_')+'_'+new Date().toISOString().split('T')[0]+'.xlsx';
  document.body.appendChild(a); a.click(); a.remove();
  showToast('✅ '+tpl.title+' u gjenerua!','📊');
}

function bibBuildBilanc(d,subj){
  const wb=XLSX.utils.book_new();
  const fitimi=(d.arketimet||0)-(d.shpenzimet||0)-(d.pagat_totale||0);
  const kapitali=(d.kapitali_fillestar||0)+fitimi;
  const aktiv_total=(d.totali_aktiv||0)+(d.arketimet||0);
  const pasiv_total=(d.detyrimet_afatgjata||0)+(d.huate_bankare||0)+kapitali;
  const rows=[
    [subj.emri||'','','',''],
    ['NIPT: '+(subj.nipt||''),'','Periudha: '+(d.periudha||''),''],
    ['BILANC KONTABËL','','','Data: '+(d.data_raportit||new Date().toLocaleDateString('sq-AL'))],
    ['','','',''],
    ['AKTIVI','Shuma (L)','PASIVI & KAPITALI','Shuma (L)'],
    ['Inventari / Stoku',d.totali_aktiv||0,'Detyrime Afatgjata',d.detyrimet_afatgjata||0],
    ['Arkëtime nga Shitjet',d.arketimet||0,'Hua Bankare',d.huate_bankare||0],
    ['','','Kapitali Fillestar',d.kapitali_fillestar||0],
    ['','','Fitimi i Periudhës',fitimi],
    ['TOTALI AKTIV',aktiv_total,'TOTALI PASIV + KAPITAL',pasiv_total],
    ['','','',''],
    ['PASQYRA E TË ARDHURAVE','','',''],
    ['Të Ardhura nga Shitjet',d.arketimet||0,'',''],
    ['(-) Shpenzime Operative',d.shpenzimet||0,'',''],
    ['(-) Kosto Pagave',d.pagat_totale||0,'',''],
    ['FITIMI NETO',fitimi,'',''],
    ['','','',''],
    ['Kontabilist: '+(d.kontabilist||'___________________'),'','Drejtori: ___________________',''],
  ];
  const ws=XLSX.utils.aoa_to_sheet(rows);
  ws['!cols']=[{wch:34},{wch:16},{wch:34},{wch:16}];
  XLSX.utils.book_append_sheet(wb,ws,'Bilanc Kontabël');
  return wb;
}

function bibBuildTatimor(d,subj){
  const wb=XLSX.utils.book_new();
  const tvsh_neto=(d.tvsh_mbledhur||0)-(d.tvsh_paguar||0)-(d.tvsh_import||0);
  const rows=[
    [subj.emri||'',''],
    ['NIPT: '+(subj.nipt||''),''],
    ['DEKLARATË TATIMORE','Periudha: '+(d.periudha||'')],
    ['Data Dorëzimit: '+(d.data_dorezimit||''),''],
    ['',''],
    ['ZËRI','Shuma (L)'],
    ['Totali Shitjeve (pa TVSH)',d.totali_shitjeve||0],
    ['TVSH e Mbledhur (20%)',d.tvsh_mbledhur||0],
    ['(-) TVSH e Paguar për Blerje',d.tvsh_paguar||0],
    ['(-) TVSH nga Importi',d.tvsh_import||0],
    ['TVSH NETO PËR PAGESË',tvsh_neto],
    ['',''],
    ['Tatim Fitimi (15%)',d.tatim_fitimi||0],
    ['Kontribute Totale',d.kontribute_total||0],
    ['',''],
    ['Përfaqësuesi Ligjor: '+(d.perfaqesuesi||'___________________'),''],
  ];
  const ws=XLSX.utils.aoa_to_sheet(rows);
  ws['!cols']=[{wch:40},{wch:18}];
  XLSX.utils.book_append_sheet(wb,ws,'Deklaratë Tatimore');
  return wb;
}

function bibBuildCashFlow(d,subj){
  const wb=XLSX.utils.book_new();
  const hyrje=(d.hyrjet_shitje||0)+(d.huate_marra||0);
  const dalje=(d.daljet_blerje||0)+(d.daljet_shpenzime||0)+(d.daljet_paga||0)+(d.investimet||0);
  const fund=(d.cash_fillestar||0)+hyrje-dalje;
  const rows=[
    [subj.emri||'',''],
    ['PASQYRA E RRJEDHJES SË PARASË','Periudha: '+(d.periudha||'')],
    ['Data: '+(d.data_raportit||''),''],
    ['',''],
    ['HYRJET','Shuma (L)'],
    ['Arkëtime nga Shitjet',d.hyrjet_shitje||0],
    ['Hua të Marra',d.huate_marra||0],
    ['TOTALI HYRJEVE',hyrje],
    ['',''],
    ['DALJET',''],
    ['Pagesa për Blerje',d.daljet_blerje||0],
    ['Shpenzime Operative',d.daljet_shpenzime||0],
    ['Pagesa Pagash',d.daljet_paga||0],
    ['Investime',d.investimet||0],
    ['TOTALI DALJEVE',dalje],
    ['',''],
    ['Cash Fillestar',d.cash_fillestar||0],
    ['(+/-) Ndryshimi Neto',hyrje-dalje],
    ['CASH FUNDI PERIUDHËS',fund],
    ['',''],
    ['Arkëtime të Pritshme (Fatura Hapur)',d.faturat_papaguara||0],
  ];
  const ws=XLSX.utils.aoa_to_sheet(rows);
  ws['!cols']=[{wch:40},{wch:20}];
  XLSX.utils.book_append_sheet(wb,ws,'Cash Flow');
  return wb;
}

function bibBuildListePagese(d,subj){
  const wb=XLSX.utils.book_new();
  const pun=state.punonjesit||[];
  const hdr=['#','Emri & Mbiemri','Pozicioni','Paga Bruto (L)','Kont. Punëtori (L)','Kont. Punëdhënësi (L)','Tatim (L)','Paga Neto (L)','Kosto Totale (L)','Statusi'];
  const prows=pun.map((p,i)=>{
    const c=calcPaga(p.bruto||0);
    return [i+1,p.emri,p.pozicioni,p.bruto||0,c.kontPunetor,c.kontPunedh,c.tatim,c.neto,c.kostoTotale,p.statusi||'Aktiv'];
  });
  const allRows=[
    [subj.emri||''],['NIPT: '+(subj.nipt||'')],
    ['Listë-Pagese — '+(d.muaji||''),'','','Data Pagesës: '+(d.data_pageses||'')],
    ['Konto: '+(d.nr_konto||'')],[''],
    hdr,...prows,
    [''],
    ['','TOTALI','',d.paga_bruto_total||0,d.kontribute_punetore||0,d.kontribute_punedhenesit||0,'',d.paga_neto_total||0,d.kosto_totale||0,''],
  ];
  const ws=XLSX.utils.aoa_to_sheet(allRows);
  ws['!cols']=[{wch:4},{wch:22},{wch:16},{wch:14},{wch:16},{wch:18},{wch:12},{wch:14},{wch:14},{wch:10}];
  XLSX.utils.book_append_sheet(wb,ws,'Listë-Pagese');
  return wb;
}

function bibBuildInventar(d,subj){
  const wb=XLSX.utils.book_new();
  const mat=state.materiale||[];
  const hdr=['#','Emri Materialit','Kategoria','Njësia','Sasia','Çm. Blerje (L)','Çm. Shitje (L)','Vlera (L)','Statusi','Furnitori'];
  const mrows=mat.map((m,i)=>[i+1,m.emri,m.kategori,m.njesia,m.sasia,m.cmBlerje||0,m.cmShitje||0,(m.sasia*(m.cmBlerje||0)),m.status||'',m.furnitori||'']);
  const allRows=[
    [subj.emri||''],
    ['INVENTAR FIZIK','','Data: '+(d.data_inventarit||'')],
    ['Vendndodhja: '+(d.vendndodhja||''),'','Kryer nga: '+(d.kryer_nga||'')],
    [''],hdr,...mrows,[''],
    ['','','','','','','VLERA TOTALE:',mat.reduce((a,m)=>a+(m.sasia*(m.cmBlerje||0)),0),'',''],
  ];
  const ws=XLSX.utils.aoa_to_sheet(allRows);
  ws['!cols']=[{wch:4},{wch:26},{wch:14},{wch:8},{wch:8},{wch:14},{wch:14},{wch:14},{wch:12},{wch:16}];
  XLSX.utils.book_append_sheet(wb,ws,'Inventar');
  return wb;
}

function bibBuildProjekt(d,subj){
  const wb=XLSX.utils.book_new();
  const proj=state.projektet||[];
  const fat=state.faturat||[];
  const hdr=['#','Emri Projektit','Klienti','Vlera (L)','Fillimi','Mbarimi','Statusi','Faturuar (L)'];
  const prows=proj.map((p,i)=>{
    const fatP=fat.filter(f=>f.projekti===p.emri).reduce((a,f)=>{const c=calcFatura(f);return a+c.total;},0);
    return [i+1,p.emri,p.klienti||'',p.vlera||0,p.fillimi||'',p.mbarimi||'',p.statusi||'',fatP];
  });
  const allRows=[
    [subj.emri||''],
    ['RAPORT PROJEKTESH','Periudha: '+(d.periudha||'')],
    ['Data: '+(d.data_raportit||''),'Përgjegjësi: '+(d.pergjegjesi||'')],
    [''],hdr,...prows,[''],
    ['','','TOTALI:',proj.reduce((a,p)=>a+(parseFloat(p.vlera)||0),0),'','','',''],
  ];
  const ws=XLSX.utils.aoa_to_sheet(allRows);
  ws['!cols']=[{wch:4},{wch:28},{wch:18},{wch:14},{wch:10},{wch:10},{wch:12},{wch:14}];
  XLSX.utils.book_append_sheet(wb,ws,'Projekte');
  return wb;
}

// ── File upload handler
function bibHandleDrop(e){
  e.preventDefault();
  document.getElementById('bib-drop-zone').classList.remove('drag');
  const file=e.dataTransfer.files[0];
  if(file) bibHandleFile(file);
}

function bibHandleFile(file){
  if(!file) return;
  bibUploadedFile=file;
  const ext=file.name.split('.').pop().toLowerCase();
  const typeMap={xlsx:'Excel',xls:'Excel',csv:'CSV',pdf:'PDF',docx:'Word'};
  const type=typeMap[ext]||ext.toUpperCase();
  document.getElementById('bib-template-info').style.display='';
  document.getElementById('bib-tpl-name').textContent=file.name;
  document.getElementById('bib-tpl-meta').textContent=type+' · '+(file.size/1024).toFixed(1)+' KB · Ngarkuar '+new Date().toLocaleTimeString('sq-AL');
  if(ext==='xlsx'||ext==='xls'||ext==='csv'){
    const reader=new FileReader();
    reader.onload=ev=>{
      try{
        const wb=XLSX.read(ev.target.result,{type:'array'});
        const ws=wb.Sheets[wb.SheetNames[0]];
        const txt=XLSX.utils.sheet_to_csv(ws);
        const matches=[...new Set((txt.match(/\{\{[\w_]+\}\}/g)||[]))];
        bibUploadedFields=matches;
        const fEl=document.getElementById('bib-tpl-fields');
        if(matches.length){
          fEl.innerHTML='<div style="font-size:0.7rem;color:var(--muted);margin-bottom:6px">Fushat e zbuluara ({{placeholder}}):</div>'+
            matches.map(m=>`<span style="display:inline-block;background:rgba(249,115,22,0.1);color:var(--orange);border:1px solid rgba(249,115,22,0.2);border-radius:6px;padding:2px 8px;font-size:0.7rem;margin:2px">${m}</span>`).join('');
        } else {
          bibUploadedFields=['{{emri_kompanise}}','{{nipt}}','{{data_sot}}','{{periudha}}','{{totali}}'];
          fEl.innerHTML='<div style="font-size:0.72rem;color:var(--muted)">Nuk u zbuluan fusha {{placeholder}}. Mund të përdorësh fushat standarde.</div>';
        }
      }catch(err){ document.getElementById('bib-tpl-fields').textContent='Gabim gjatë leximit të skedarit.'; }
    };
    reader.readAsArrayBuffer(file);
  } else {
    bibUploadedFields=['{{emri_kompanise}}','{{nipt}}','{{data_sot}}','{{periudha}}'];
    document.getElementById('bib-tpl-fields').innerHTML='<div style="font-size:0.72rem;color:var(--muted)">'+type+' · Plotëso fushat manuale më poshtë.</div>';
  }
}

function bibProceedToFill(){
  if(!bibUploadedFile){ showToast('Ngarko një skedar fillimisht!','⚠️'); return; }
  document.getElementById('bib-fill-step').style.display='';
  document.getElementById('bib-template-info').style.display='none';
  document.getElementById('bib-drop-zone').style.display='none';
  const subj=getCurrentSubj();
  const autoMap={
    '{{emri_kompanise}}':subj.emri||'','{{nipt}}':subj.nipt||'','{{adresa}}':subj.adresa||'',
    '{{tel}}':subj.tel||'','{{data_sot}}':new Date().toLocaleDateString('sq-AL'),
    '{{totali_shitjeve}}':fmt((state.shitje||[]).reduce((a,x)=>a+x.total,0)),
    '{{totali_shpenzimeve}}':fmt((state.shpenzime||[]).reduce((a,x)=>a+x.vlera,0)),
    '{{nr_punonjesve}}':(state.punonjesit||[]).length,
    '{{vlera_stokut}}':fmt((state.materiale||[]).reduce((a,m)=>a+(m.sasia*(m.cmBlerje||0)),0)),
    '{{nr_faturave}}':(state.faturat||[]).length,
    '{{fitimi}}':fmt((state.shitje||[]).reduce((a,x)=>a+x.total,0)-(state.shpenzime||[]).reduce((a,x)=>a+x.vlera,0)),
  };
  const autoMatched=[],manualLeft=[];
  bibUploadedFields.forEach(f=>{ if(autoMap[f]!==undefined) autoMatched.push({key:f,val:autoMap[f]}); else manualLeft.push(f); });
  document.getElementById('bib-auto-fields').innerHTML=autoMatched.length
    ? autoMatched.map(x=>`<div class="bib-fill-row"><div><div class="bib-field-label">${x.key.replace(/[{}]/g,'')}</div><div class="bib-field-auto">✓ Auto</div></div><div style="font-size:0.82rem;font-weight:600;color:var(--text);text-align:right">${x.val}</div></div>`).join('')
    : '<div style="font-size:0.72rem;color:var(--muted)">Asnjë fushë automatike e zbuluar.</div>';
  document.getElementById('bib-manual-fields').innerHTML=manualLeft.length
    ? manualLeft.map(f=>`<div class="bib-fill-row"><div class="bib-field-label">${f.replace(/[{}]/g,'')}</div><input id="bibf-${f.replace(/[{}]/g,'')}" type="text" placeholder="Shkruaj vlerën..." style="background:var(--s1);border:1px solid var(--border);border-radius:7px;padding:6px 10px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.8rem;width:100%;outline:none"></div>`).join('')
    : '<div style="font-size:0.72rem;color:var(--green)">✅ Të gjitha fushat plotësohen automatikisht!</div>';
}

function bibBackToUpload(){
  document.getElementById('bib-fill-step').style.display='none';
  document.getElementById('bib-template-info').style.display='';
  document.getElementById('bib-drop-zone').style.display='';
}

function bibGenerate(){
  if(!bibUploadedFile){ showToast('Ngarko një skedar fillimisht!','⚠️'); return; }
  const ext=bibUploadedFile.name.split('.').pop().toLowerCase();
  const subj=getCurrentSubj();
  const autoMap={
    '{{emri_kompanise}}':subj.emri||'','{{nipt}}':subj.nipt||'','{{adresa}}':subj.adresa||'',
    '{{tel}}':subj.tel||'','{{data_sot}}':new Date().toLocaleDateString('sq-AL'),
    '{{totali_shitjeve}}':(state.shitje||[]).reduce((a,x)=>a+x.total,0),
    '{{totali_shpenzimeve}}':(state.shpenzime||[]).reduce((a,x)=>a+x.vlera,0),
    '{{nr_punonjesve}}':(state.punonjesit||[]).length,
    '{{vlera_stokut}}':(state.materiale||[]).reduce((a,m)=>a+(m.sasia*(m.cmBlerje||0)),0),
    '{{nr_faturave}}':(state.faturat||[]).length,
    '{{fitimi}}':(state.shitje||[]).reduce((a,x)=>a+x.total,0)-(state.shpenzime||[]).reduce((a,x)=>a+x.vlera,0),
  };
  bibUploadedFields.forEach(f=>{
    if(autoMap[f]===undefined){ const el=document.getElementById('bibf-'+f.replace(/[{}]/g,'')); if(el) autoMap[f]=el.value; }
  });
  if(ext==='xlsx'||ext==='xls'){
    const reader=new FileReader();
    reader.onload=ev=>{
      try{
        const wb=XLSX.read(ev.target.result,{type:'array'});
        wb.SheetNames.forEach(sn=>{
          const ws=wb.Sheets[sn];
          Object.keys(ws).filter(k=>k[0]!=='!').forEach(addr=>{
            const cell=ws[addr];
            if(cell&&cell.t==='s'){ let v=cell.v; Object.entries(autoMap).forEach(([ph,val])=>{v=v.split(ph).join(String(val));}); cell.v=v; }
          });
        });
        const out=XLSX.write(wb,{bookType:'xlsx',type:'array'});
        const blob=new Blob([out],{type:'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet'});
        const a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='plotesuar_'+bibUploadedFile.name;
        document.body.appendChild(a); a.click(); a.remove();
        showToast('✅ Excel u plotësua dhe u shkarkua!','📊');
      }catch(e){ showToast('Gabim: '+e.message,'❌'); }
    };
    reader.readAsArrayBuffer(bibUploadedFile);
  } else if(ext==='csv'){
    const reader=new FileReader();
    reader.onload=ev=>{
      let txt=ev.target.result;
      Object.entries(autoMap).forEach(([ph,val])=>{txt=txt.split(ph).join(String(val));});
      const blob=new Blob([txt],{type:'text/csv;charset=utf-8'});
      const a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='plotesuar_'+bibUploadedFile.name;
      document.body.appendChild(a); a.click(); a.remove();
      showToast('✅ CSV u plotësua!','📄');
    };
    reader.readAsText(bibUploadedFile,'utf-8');
  } else {
    showToast('Tipi '+ext.toUpperCase()+' nuk mbështet zëvendësim automatik. Shkarkohet origjinali.','⚠️');
  }
}


// INIT
renderSubjectList();
updateSubjTopbar();
render();
</script>
</body>
</html>
