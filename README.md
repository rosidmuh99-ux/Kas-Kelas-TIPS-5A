<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Kas Kelas TIPS 5A</title>
<style>
:root{--bg:#f4f7fc;--card:#fff;--ink:#14213d;--mute:#7a869a;--line:#e3e9f3;--in:#1f7a52;--out:#c0453a;--accent:#2457d6}
body{border-top:4px solid var(--accent)}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;background:var(--bg);color:var(--ink);line-height:1.5;-webkit-font-smoothing:antialiased}
.wrap{max-width:820px;margin:0 auto;padding:44px 18px 60px}
header{margin-bottom:34px}
header small{letter-spacing:.18em;text-transform:uppercase;color:var(--mute);font-size:.7rem}
header h1{font-weight:600;font-size:1.8rem;margin-top:6px;letter-spacing:-.01em}
.saldo{margin-top:22px}
.saldo span{color:var(--mute);font-size:.8rem}
.saldo b{display:block;font-weight:600;font-size:2.6rem;letter-spacing:-.02em;color:var(--accent)}
.sub{display:flex;gap:28px;margin-top:10px;font-size:.9rem}
.sub i{font-style:normal;color:var(--mute);margin-right:6px}
.in{color:var(--in)}.out{color:var(--out)}
.card{background:var(--card);border:1px solid var(--line);border-radius:16px;padding:22px;margin-top:22px}
h2{font-weight:600;font-size:1rem;margin-bottom:14px}
.seg{display:grid;grid-template-columns:1fr 1fr;border:1px solid var(--line);border-radius:10px;padding:3px;margin-bottom:14px;background:var(--bg)}
.seg button{border:0;background:none;padding:9px;border-radius:8px;font-size:.92rem;cursor:pointer;color:var(--mute);font-family:inherit}
.seg button.on{background:var(--card);color:var(--ink);box-shadow:0 1px 3px rgba(0,0,0,.08)}
.seg button.on.m{color:var(--in)}.seg button.on.k{color:var(--out)}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.full{grid-column:1/-1}
label{font-size:.75rem;color:var(--mute);display:block;margin-bottom:4px}
input,select{width:100%;padding:11px 12px;border:1px solid var(--line);border-radius:10px;font-size:.95rem;font-family:inherit;background:#fff;color:var(--ink);outline:none}
input:focus,select:focus{border-color:#7fa0ef}
.grid3{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.act{display:flex;gap:8px;margin-top:14px;align-items:center}
.btn{border:1px solid var(--accent);background:var(--accent);color:#fff;padding:11px 20px;border-radius:10px;font-size:.92rem;cursor:pointer;font-family:inherit}
.btn.ghost{background:none;color:var(--ink);border-color:var(--line)}
.btn:disabled{opacity:.35;cursor:default}
#pesan,#pesan2{font-size:.82rem;color:var(--mute);margin-left:auto}
.tools{display:flex;gap:8px;margin-bottom:10px}
.tools input{flex:1}.tools select{width:150px}
.tw{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:.9rem}
th{font-weight:400;color:var(--mute);font-size:.72rem;letter-spacing:.08em;text-transform:uppercase;text-align:left;padding:8px 8px;border-bottom:1px solid var(--line)}
td{padding:12px 8px;border-bottom:1px solid var(--line);white-space:nowrap}
tr:last-child td{border-bottom:0}
.r{text-align:right}
.x{border:0;background:none;color:var(--mute);cursor:pointer;font-size:.8rem;padding:4px 8px;border-radius:6px;font-family:inherit}
.x:hover{color:var(--out);background:#f7ece9}
.kosong{text-align:center;color:var(--mute);padding:26px 0}
footer{text-align:center;color:var(--mute);font-size:.75rem;margin-top:30px}
@media(max-width:520px){.grid,.grid3{grid-template-columns:1fr}.saldo b{font-size:2.2rem}.sub{flex-direction:column;gap:2px}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <small>Laporan keuangan</small>
    <h1>Kas Kelas TIPS 5A</h1>
    <div class="saldo"><span>Saldo saat ini</span><b id="saldo"></b></div>
    <div class="sub">
      <div><i>Total masuk</i><span class="in" id="tm"></span></div>
      <div><i>Total keluar</i><span class="out" id="tk"></span></div>
    </div>
  </header>

  <div class="card">
    <h2>Catat transaksi</h2>
    <div class="seg">
      <button class="m on" id="bm" type="button">Uang masuk</button>
      <button class="k" id="bk" type="button">Uang keluar</button>
    </div>
    <form id="form" class="grid">
      <div><label for="tgl">Tanggal</label><input type="date" id="tgl" required></div>
      <div><label for="jml">Jumlah (Rp)</label><input type="number" id="jml" min="1" step="500" inputmode="numeric" placeholder="0" required></div>
      <div class="full"><label for="ket">Keterangan</label><input type="text" id="ket" maxlength="60" placeholder="Contoh: Kas minggu ini" required></div>
      <div class="full act">
        <button class="btn" type="submit" id="simpan">Simpan uang masuk</button>
        <button class="btn ghost" type="button" id="undo">Undo</button>
        <span id="pesan"></span>
      </div>
    </form>
  </div>

  <div class="card">
    <h2>Riwayat</h2>
    <div class="tools">
      <input id="cari" placeholder="Cari keterangan">
      <select id="jenis"><option value="semua">Semua</option><option value="masuk">Uang masuk</option><option value="keluar">Uang keluar</option></select>
    </div>
    <div class="tw">
      <table>
        <thead><tr><th>Tanggal</th><th>Keterangan</th><th class="r">Masuk</th><th class="r">Keluar</th><th class="r">Saldo</th><th></th></tr></thead>
        <tbody id="tb"></tbody>
      </table>
    </div>
  </div>
  <div class="card">
    <h2>Ekspor data</h2>
    <div class="grid3">
      <div><label for="edari">Dari tanggal</label><input type="date" id="edari"></div>
      <div><label for="esampai">Sampai tanggal</label><input type="date" id="esampai"></div>
      <div><label for="ejenis">Jenis</label>
        <select id="ejenis"><option value="semua">Semua transaksi</option><option value="masuk">Hanya uang masuk</option><option value="keluar">Hanya uang keluar</option></select>
      </div>
    </div>
    <div class="act">
      <button class="btn" type="button" id="bcsv">Unduh CSV</button>
      <button class="btn ghost" type="button" id="bword">Unduh Word</button>
      <span id="pesan2"></span>
    </div>
    <p style="font-size:.75rem;color:var(--mute);margin-top:10px">Kosongkan tanggal untuk mengekspor semua periode.</p>
  </div>
  <footer>Data tersimpan di browser perangkat ini.</footer>
</div>

<script>
const AWAL = [[1,"10/09/2025","Saldo Semester 2",1350000,0],[2,"10/09/2025","Kas",110000,0],[3,"11/09/2025","Kas",20000,0],[4,"15/09/2025","Kas",135000,0],[5,"22/09/2025","Kas",145000,0],[6,"29/09/2025","Kas",140000,0],[7,"06/10/2025","Kas",135000,0],[8,"06/10/2025","HTM Lomba",0,470000],[9,"07/10/2025","Kas",10000,0],[10,"13/10/2025","Kas",125000,0],[11,"21/10/2025","Sewa Jaz Duta",0,400000],[12,"21/10/2025","Kas",220000,0],[13,"23/10/2025","Kertas Folio",0,10000],[14,"27/10/2025","Kertas Folio",0,7000],[15,"27/10/2025","Kas",210000,0],[16,"03/11/2025","Konsum lomba",0,156000],[17,"03/11/2025","Kertas Folio",0,6000],[18,"03/11/2025","Loundry",0,18000],[19,"03/11/2025","Sewa Jersey",0,50000],[20,"03/11/2025","Kas",154000,0],[21,"10/11/2025","Makeup",0,200000],[22,"10/11/2025","Kas",141000,0],[23,"17/11/2025","Kas",125000,0],[24,"18/11/2025","Kupon Bazar",0,100000],[25,"18/11/2025","Modal Bazar",0,225000],[26,"21/11/2025","Tambah ML",0,10000],[27,"21/11/2025","Bazar",271000,0],[28,"24/11/2025","Kas",155000,0],[29,"01/12/2025","Kas",130000,0],[30,"08/12/2025","Souvernir",0,205000],[31,"08/12/2025","Kas",196000,0],[32,"15/12/2025","Kas",10000,0],[33,"16/12/2025","Kas",44000,0],[34,"23/12/2025","Joki Jurnal Media",0,260000],[35,"05/03/2026","Dana Bansos",0,300000],[36,"11/03/2026","Buka bersama",0,996500],[37,"05/04/2026","Beli Map + Print",0,111500],[38,"06/04/2026","Kas",120000,0],[39,"06/04/2026","Kas",35000,0],[40,"09/04/2026","Beli kabel",0,68500],[41,"13/04/2026","Kas",75000,0],[42,"13/04/2026","Kas",10000,0],[43,"20/04/2026","Kas",140000,0],[44,"27/04/2026","Kertas folio",0,16000],[45,"27/04/2026","Kas",115000,0],[46,"04/05/2026","Kas",215000,0],[47,"04/05/2026","Kas",75000,0],[48,"06/05/2026","Kertas folio",0,9000],[49,"11/05/2026","Kas",45000,0],[50,"14/05/2026","Beli shp rtrw",0,289000],[51,"20/05/2026","Kertas folio",0,16000],[52,"18/05/2026","Kas",40000,0],[53,"24/05/2026","RTRW kls b",145000,0],[54,"01/06/2026","Kas",70000,0],[55,"08/06/2026","Kas",185000,0],[56,"15/06/2026","Kas",240000,0],[57,"18/06/2026","Beli kertas",0,7000],[58,"19/06/2026","Kas",30000,0],[59,"23/06/2026","Kas",20000,0],[60,"25/06/2026","Kas",45000,0],[61,"02/07/2026","Kas",70000,0],[62,"01/07/2026","Kertas",0,7000],[63,"06/07/2026","Kertas",0,7000],[64,"28/07/2026","Kas",50000,0],[65,"28/07/2026","Uang sisa",23000,0],[66,"29/07/2026","Kas",10000,0],[67,"29/07/2026","Fun run",0,1280000],[68,"08/09/2026","Kas",120000,0],[69,"15/09/2026","Kas",150000,0],[70,"21/09/2026","HDMI",0,77000],[71,"21/09/2026","Kas",105000,0],[72,"22/09/2026","Kas",15000,0],[73,"01/10/2026","Kas",125000,0],[74,"01/10/2026","Kas",15000,0],[75,"05/10/2026","Kas",10000,0],[76,"06/10/2026","Kas",140000,0],[77,"16/10/2026","Kas",105000,0],[78,"16/10/2026","ML",0,60000],[79,"18/10/2026","Debat/futsal",0,150000],[80,"18/10/2026","Konsum",0,120000],[81,"20/10/2026","Kas",135000,0],[82,"27/10/2026","Tumpeng",0,15000],[83,"27/10/2026","Konsum debat",0,21000],[84,"29/10/2026","Kas",210000,0]];
const SALDO_AWAL = 500;   // saldo pembuka sebelum transaksi pertama
const KEY = 'kas5a_v1';

const $ = id => document.getElementById(id);
const rp = n => 'Rp ' + n.toLocaleString('id-ID');
const esc = s => s.replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));

let data = [], undoStack = [], mode = 'masuk', nextId = 1000;

function muat(){
  try{ const s = localStorage.getItem(KEY); if(s){ data = JSON.parse(s); return; } }catch(e){}
  data = AWAL.map(r => ({id:r[0], t:r[1], k:r[2], m:r[3], o:r[4]}));
}
function simpanData(){ try{ localStorage.setItem(KEY, JSON.stringify(data)); }catch(e){} }
function idBaru(){ return Math.max(nextId, ...data.map(r=>r.id)) + 1; }

function pesan(t){ $('pesan').textContent = t; clearTimeout(pesan.h); pesan.h = setTimeout(()=>$('pesan').textContent='', 3500); }

function render(){
  let s = SALDO_AWAL, tm = 0, tk = 0;
  const rows = data.map(r => { s += r.m - r.o; tm += r.m; tk += r.o; return {...r, s}; });
  $('saldo').textContent = rp(s);
  $('tm').textContent = rp(tm);
  $('tk').textContent = rp(tk);
  $('undo').disabled = undoStack.length === 0;

  const q = $('cari').value.trim().toLowerCase(), j = $('jenis').value;
  const out = rows.filter(r => (!q || r.k.toLowerCase().includes(q)) && !(j==='masuk' && !r.m) && !(j==='keluar' && !r.o)).reverse();
  $('tb').innerHTML = out.map(r =>
    `<tr><td>${r.t}</td><td>${esc(r.k)}</td>` +
    `<td class="r in">${r.m ? rp(r.m) : ''}</td><td class="r out">${r.o ? rp(r.o) : ''}</td>` +
    `<td class="r">${rp(r.s)}</td><td class="r"><button class="x" data-id="${r.id}">Hapus</button></td></tr>`
  ).join('') || '<tr><td colspan="6" class="kosong">Belum ada transaksi.</td></tr>';
}

function saldoSekarang(){ return SALDO_AWAL + data.reduce((a,r)=>a+r.m-r.o, 0); }

function setMode(m){
  mode = m;
  $('bm').classList.toggle('on', m==='masuk'); $('bk').classList.toggle('on', m==='keluar');
  $('simpan').textContent = m==='masuk' ? 'Simpan uang masuk' : 'Simpan uang keluar';
}
$('bm').onclick = () => setMode('masuk');
$('bk').onclick = () => setMode('keluar');

$('form').addEventListener('submit', e => {
  e.preventDefault();
  const jml = parseInt($('jml').value, 10), ket = $('ket').value.trim(), tg = $('tgl').value;
  if(!jml || jml < 1 || !ket || !tg) return;
  if(mode==='keluar' && jml > saldoSekarang()){ pesan('Saldo tidak cukup untuk pengeluaran ini.'); return; }
  const [y,m,d] = tg.split('-');
  const trx = {id:idBaru(), t:`${d}/${m}/${y}`, k:ket, m: mode==='masuk'?jml:0, o: mode==='keluar'?jml:0};
  data.push(trx);
  undoStack.push({type:'tambah', trx});
  simpanData(); render();
  $('jml').value = ''; $('ket').value = '';
  pesan(mode==='masuk' ? 'Uang masuk tercatat.' : 'Pengeluaran tercatat.');
});

$('tb').addEventListener('click', e => {
  const b = e.target.closest('.x'); if(!b) return;
  const id = +b.dataset.id, i = data.findIndex(r => r.id === id);
  if(i < 0) return;
  if(!confirm(`Hapus transaksi "${data[i].k}" tanggal ${data[i].t}?`)) return;
  const [trx] = data.splice(i, 1);
  undoStack.push({type:'hapus', trx, index:i});
  simpanData(); render(); pesan('Transaksi dihapus. Tekan Undo untuk membatalkan.');
});

$('undo').onclick = () => {
  const a = undoStack.pop(); if(!a) return;
  if(a.type === 'tambah'){ data = data.filter(r => r.id !== a.trx.id); pesan('Transaksi terakhir dibatalkan.'); }
  else { data.splice(a.index, 0, a.trx); pesan('Transaksi dikembalikan.'); }
  simpanData(); render();
};

/* ===== Ekspor ===== */
const iso2id = s => { const [y,m,d] = s.split('-'); return `${d}/${m}/${y}`; };
function pesan2(t){ $('pesan2').textContent = t; clearTimeout(pesan2.h); pesan2.h = setTimeout(()=>$('pesan2').textContent='', 4000); }
function ambilEkspor(){
  const dari = $('edari').value, sampai = $('esampai').value, j = $('ejenis').value;
  if(dari && sampai && dari > sampai){ pesan2('Tanggal awal lebih besar dari tanggal akhir.'); return null; }
  let s = SALDO_AWAL;
  const rows = data.map(r => { s += r.m - r.o; const [d,m,y] = r.t.split('/'); return {...r, s, iso:`${y}-${m}-${d}`}; })
    .filter(r => (!dari || r.iso >= dari) && (!sampai || r.iso <= sampai) && !(j==='masuk' && !r.m) && !(j==='keluar' && !r.o));
  if(!rows.length){ pesan2('Tidak ada transaksi pada pilihan ini.'); return null; }
  return rows;
}
function labelEkspor(){
  const dari = $('edari').value, sampai = $('esampai').value, j = $('ejenis').value;
  const per = (!dari && !sampai) ? 'Semua periode' : `${dari ? iso2id(dari) : 'awal'} - ${sampai ? iso2id(sampai) : 'sekarang'}`;
  const jn = {semua:'Semua transaksi', masuk:'Hanya uang masuk', keluar:'Hanya uang keluar'}[j];
  return {per, jn};
}
function unduh(nama, isi, tipe){
  const a = document.createElement('a');
  a.href = URL.createObjectURL(new Blob([isi], {type:tipe}));
  a.download = nama; document.body.appendChild(a); a.click(); a.remove();
  setTimeout(()=>URL.revokeObjectURL(a.href), 1500);
}
$('bcsv').onclick = () => {
  const rows = ambilEkspor(); if(!rows) return;
  const q = v => '"' + String(v).replace(/"/g,'""') + '"';
  const baris = [['Tanggal','Keterangan','Masuk','Keluar','Saldo'].join(';')]
    .concat(rows.map(r => [r.t, q(r.k), r.m||'', r.o||'', r.s].join(';')));
  unduh('kas-tips-5a.csv', '\ufeff' + baris.join('\r\n'), 'text/csv;charset=utf-8');
  pesan2('CSV diunduh.');
};
$('bword').onclick = () => {
  const rows = ambilEkspor(); if(!rows) return;
  const tm = rows.reduce((a,r)=>a+r.m,0), tk = rows.reduce((a,r)=>a+r.o,0), {per, jn} = labelEkspor();
  const td = 'style="border:1px solid #c9d3e6;padding:5px 8px;font-size:10pt"';
  const th = 'style="border:1px solid #c9d3e6;padding:6px 8px;font-size:10pt;background:#2457d6;color:#fff;text-align:left"';
  const html = `<html xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:w="urn:schemas-microsoft-com:office:word" xmlns="http://www.w3.org/TR/REC-html40"><head><meta charset="utf-8"><title>Kas Kelas TIPS 5A</title></head>
<body style="font-family:Arial,sans-serif;color:#14213d">
<h2 style="color:#2457d6;margin-bottom:2px">Laporan Kas Kelas TIPS 5A</h2>
<p style="font-size:10pt;margin:0">Periode: ${per} &nbsp;|&nbsp; ${jn}</p>
<p style="font-size:10pt;margin:8px 0 12px">Total masuk: <b>${rp(tm)}</b> &nbsp;|&nbsp; Total keluar: <b>${rp(tk)}</b> &nbsp;|&nbsp; Selisih: <b>${rp(tm-tk)}</b></p>
<table style="border-collapse:collapse;width:100%">
<tr><th ${th}>Tanggal</th><th ${th}>Keterangan</th><th ${th}>Masuk</th><th ${th}>Keluar</th><th ${th}>Saldo</th></tr>
${rows.map(r=>`<tr><td ${td}>${r.t}</td><td ${td}>${esc(r.k)}</td><td ${td} align="right">${r.m?rp(r.m):''}</td><td ${td} align="right">${r.o?rp(r.o):''}</td><td ${td} align="right">${rp(r.s)}</td></tr>`).join('')}
</table></body></html>`;
  unduh('kas-tips-5a.doc', '\ufeff' + html, 'application/msword');
  pesan2('Word diunduh.');
};

$('cari').addEventListener('input', render);
$('jenis').addEventListener('change', render);

const h = new Date();
$('tgl').value = `${h.getFullYear()}-${String(h.getMonth()+1).padStart(2,'0')}-${String(h.getDate()).padStart(2,'0')}`;
muat(); render();
</script>
</body>
</html>
