<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DigiLocker Clone</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{--primary:#1a237e;--primary-light:#3949ab;--accent:#ff6f00;--bg:#f5f5f5;--card:#fff;--text:#333;--text-light:#666;--success:#4caf50;--danger:#f44336;--shadow:0 2px 10px rgba(0,0,0,.1)}
body{font-family:'Poppins',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden}
.screen{display:none}.screen.active{display:block}

/* AUTH */
.auth-container{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:20px;background:linear-gradient(135deg,#1a237e 0%,#3949ab 50%,#1a237e 100%)}
.auth-header{text-align:center;color:#fff;margin-bottom:30px}
.auth-header .logo{width:80px;height:80px;background:#fff;border-radius:20px;display:flex;align-items:center;justify-content:center;margin:0 auto 15px;font-size:35px;color:var(--primary)}
.auth-header h1{font-size:28px}.auth-header p{opacity:.8;font-size:14px}
.auth-form{display:none;width:100%;max-width:400px;background:#fff;padding:30px;border-radius:20px;box-shadow:0 10px 40px rgba(0,0,0,.2)}
.auth-form.active{display:block}
.auth-form h2{text-align:center;margin-bottom:25px;color:var(--primary)}
.input-group{position:relative;margin-bottom:15px}
.input-group i{position:absolute;left:15px;top:50%;transform:translateY(-50%);color:var(--text-light)}
.input-group input,.input-group select{width:100%;padding:12px 15px 12px 45px;border:2px solid #e0e0e0;border-radius:12px;font-size:14px;font-family:'Poppins',sans-serif;outline:none;transition:.3s}
.input-group input:focus,.input-group select:focus{border-color:var(--primary)}
.btn-primary{width:100%;padding:14px;background:linear-gradient(135deg,var(--primary),var(--primary-light));color:#fff;border:none;border-radius:12px;font-size:16px;font-weight:600;cursor:pointer;font-family:'Poppins',sans-serif;margin-top:10px;transition:.2s}
.btn-primary:hover{transform:translateY(-2px);box-shadow:0 5px 20px rgba(26,35,126,.4)}
.switch-auth{text-align:center;margin-top:20px;font-size:14px}
.switch-auth a{color:var(--primary);cursor:pointer;font-weight:600}

/* NAVBAR */
.navbar{background:var(--primary);padding:15px 20px;display:flex;justify-content:space-between;align-items:center;position:sticky;top:0;z-index:100}
.nav-left{display:flex;align-items:center;gap:10px;color:#fff;font-size:20px;font-weight:600}
.nav-left i{font-size:24px}
.nav-right{display:flex;align-items:center;gap:10px;position:relative}
.user-name{color:#fff;font-size:14px}
.profile-icon{color:#fff;font-size:28px;cursor:pointer}
.profile-menu{display:none;position:absolute;top:45px;right:0;background:#fff;border-radius:12px;box-shadow:var(--shadow);width:250px;overflow:hidden;z-index:200}
.profile-menu.active{display:block}
.profile-info{padding:20px;text-align:center;background:linear-gradient(135deg,var(--primary),var(--primary-light));color:#fff}
.profile-info .small-text{font-size:12px;opacity:.8}
.profile-menu a{display:flex;align-items:center;gap:10px;padding:12px 20px;color:var(--text);text-decoration:none;cursor:pointer;transition:.2s}
.profile-menu a:hover{background:#f5f5f5}

/* MAIN */
.main-content{padding:20px;padding-bottom:80px;max-width:800px;margin:0 auto}
.content-section{display:none}.content-section.active{display:block}
.welcome-banner{background:linear-gradient(135deg,var(--primary),var(--primary-light));color:#fff;padding:25px;border-radius:16px;margin-bottom:25px}
.welcome-banner h2{font-size:22px}.welcome-banner p{opacity:.8;font-size:14px}
.stats-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-bottom:25px}
.stat-card{background:#fff;padding:20px;border-radius:16px;text-align:center;box-shadow:var(--shadow);transition:.2s}
.stat-card:hover{transform:translateY(-3px)}
.stat-card i{font-size:28px;color:var(--primary);margin-bottom:10px}
.stat-card h3{font-size:24px;color:var(--primary)}
.stat-card p{font-size:12px;color:var(--text-light)}
.quick-actions h3,.recent-docs h3{margin-bottom:15px;font-size:18px}
.actions-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:25px}
.action-card{background:#fff;padding:20px 10px;border-radius:16px;text-align:center;box-shadow:var(--shadow);cursor:pointer;transition:.2s}
.action-card:hover{transform:translateY(-3px)}
.action-card i{font-size:24px;color:var(--accent);margin-bottom:8px}
.action-card p{font-size:11px;color:var(--text-light)}
.section-header{display:flex;align-items:center;gap:15px;margin-bottom:20px}
.back-btn{width:40px;height:40px;border-radius:12px;border:none;background:#fff;box-shadow:var(--shadow);cursor:pointer;font-size:16px;color:var(--primary)}

/* UPLOAD */
.upload-form{max-width:500px;margin:0 auto}
.upload-area{position:relative;border:2px dashed #ccc;border-radius:16px;padding:40px 20px;text-align:center;margin-bottom:15px;cursor:pointer;transition:.3s;overflow:hidden}
.upload-area:hover{border-color:var(--primary)}
.upload-area input[type="file"]{position:absolute;top:0;left:0;width:100%;height:100%;opacity:0;cursor:pointer}
.upload-placeholder i{color:var(--primary);margin-bottom:10px}
.upload-placeholder p{font-weight:500}
.upload-placeholder span{font-size:12px;color:var(--text-light)}
.upload-preview{position:relative}
.upload-preview img{max-width:100%;max-height:200px;border-radius:8px}
.remove-btn{position:absolute;top:5px;right:5px;width:30px;height:30px;border-radius:50%;border:none;background:var(--danger);color:#fff;cursor:pointer;z-index:5}

/* FILTERS */
.filter-tabs{display:flex;gap:8px;overflow-x:auto;padding-bottom:10px;margin-bottom:20px}
.filter-btn{padding:8px 16px;border:2px solid #e0e0e0;border-radius:25px;background:#fff;font-family:'Poppins',sans-serif;font-size:13px;cursor:pointer;white-space:nowrap;transition:.2s}
.filter-btn.active{background:var(--primary);color:#fff;border-color:var(--primary)}

/* DOCS GRID */
.docs-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:15px}
.doc-card{background:#fff;border-radius:16px;overflow:hidden;box-shadow:var(--shadow);cursor:pointer;transition:.2s}
.doc-card:hover{transform:translateY(-3px)}
.doc-thumb{width:100%;height:120px;background:#e8eaf6;display:flex;align-items:center;justify-content:center;overflow:hidden}
.doc-thumb img{width:100%;height:100%;object-fit:cover}
.doc-thumb i{font-size:40px;color:var(--primary)}
.doc-info{padding:12px}
.doc-info h4{font-size:13px;margin-bottom:4px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.doc-info .doc-cat{font-size:11px;color:var(--primary);background:#e8eaf6;padding:2px 8px;border-radius:10px;display:inline-block}

/* DOCS LIST */
.doc-list-item{display:flex;align-items:center;gap:15px;padding:15px;background:#fff;border-radius:12px;margin-bottom:10px;box-shadow:var(--shadow);cursor:pointer}
.doc-list-icon{width:50px;height:50px;background:#e8eaf6;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:20px;color:var(--primary);flex-shrink:0}
.doc-list-info{flex:1}
.doc-list-info h4{font-size:14px}
.doc-list-info p{font-size:12px;color:var(--text-light)}
.empty-text{text-align:center;color:var(--text-light);padding:40px 20px;font-size:14px}

/* ISSUED */
.issued-card{display:flex;align-items:center;gap:15px;padding:15px;background:#fff;border-radius:12px;margin-bottom:10px;box-shadow:var(--shadow)}
.issued-icon{width:50px;height:50px;background:#e8eaf6;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:20px;color:var(--primary)}
.issued-info{flex:1}
.issued-info h4{font-size:14px}
.issued-info p{font-size:12px;color:var(--text-light)}
.issued-status{font-size:11px;color:var(--success);font-weight:500}
.fetch-btn{padding:8px 16px;background:var(--primary);color:#fff;border:none;border-radius:8px;font-family:'Poppins',sans-serif;cursor:pointer}

/* SHARED */
.shared-empty{text-align:center;padding:60px 20px;color:var(--text-light)}
.shared-empty i{margin-bottom:20px;color:#ccc}

/* PROFILE */
.profile-card{background:#fff;border-radius:16px;overflow:hidden;box-shadow:var(--shadow)}
.profile-avatar{background:linear-gradient(135deg,var(--primary),var(--primary-light));color:#fff;padding:30px;text-align:center}
.profile-details{padding:5px 20px 20px}
.detail-row{display:flex;justify-content:space-between;padding:15px 0;border-bottom:1px solid #f0f0f0}
.detail-row .label{color:var(--text-light);font-size:14px}
.detail-row .value{font-weight:500;font-size:14px}

/* BOTTOM NAV */
.bottom-nav{position:fixed;bottom:0;left:0;right:0;background:#fff;display:flex;justify-content:space-around;align-items:center;padding:8px 0;box-shadow:0 -2px 10px rgba(0,0,0,.1);z-index:100}
.nav-item{display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;padding:5px 15px;color:var(--text-light);font-size:11px;transition:.2s}
