# index.html
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ตลาดนัด — ร้านค้าออนไลน์</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Mitr:wght@400;500;600&family=Sarabun:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --paper:#FBF9F4;
    --ink:#1A2238;
    --cobalt:#1F4FD8;
    --marigold:#F5A623;
    --leaf:#1E7F5C;
    --tag:#FFF3D6;
    --radius:14px;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  body{
    font-family:'Sarabun',sans-serif;
    background:var(--paper);
    color:var(--ink);
    line-height:1.6;
  }
  h1,h2,h3,.btn{font-family:'Mitr',sans-serif}

  /* ===== Header ===== */
  header{
    position:sticky;top:0;z-index:50;
    background:var(--cobalt);color:#fff;
    display:flex;align-items:center;justify-content:space-between;
    padding:14px 20px;
    box-shadow:0 2px 12px rgba(31,79,216,.25);
  }
  header h1{font-size:1.3rem;font-weight:600;letter-spacing:.5px}
  header h1 span{color:var(--marigold)}
  #cartBtn{
    background:var(--marigold);color:var(--ink);
    border:none;border-radius:999px;
    padding:8px 18px;font-size:1rem;font-weight:500;
    cursor:pointer;font-family:'Mitr',sans-serif;
    transition:transform .15s;
  }
  #cartBtn:hover{transform:scale(1.05)}
  #cartBtn:focus-visible{outline:3px solid #fff;outline-offset:2px}

  /* ===== Hero ===== */
  .hero{
    text-align:center;
    padding:56px 20px 40px;
  }
  .hero h2{
    font-size:clamp(1.8rem,5vw,3rem);
    font-weight:600;
  }
  .hero h2 em{
    font-style:normal;color:var(--cobalt);
    border-bottom:6px solid var(--marigold);
  }
  .hero p{margin-top:12px;color:#555;max-width:520px;margin-inline:auto}

  /* ===== Product grid ===== */
  .grid{
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
    gap:22px;
    max-width:1000px;margin:0 auto;padding:0 20px 60px;
  }
  .card{
    background:#fff;border-radius:var(--radius);
    border:1.5px solid #E8E4DA;
    overflow:hidden;
    display:flex;flex-direction:column;
    transition:transform .18s, box-shadow .18s;
  }
  .card:hover{transform:translateY(-4px);box-shadow:0 10px 24px rgba(26,34,56,.10)}
  .thumb{
    height:150px;display:flex;align-items:center;justify-content:center;
    font-size:3.4rem;
  }
  .card-body{padding:16px;flex:1;display:flex;flex-direction:column;gap:6px}
  .card-body h3{font-size:1.05rem;font-weight:500}
  .card-body p{font-size:.86rem;color:#666;flex:1}

  /* ป้ายราคาแบบแท็กกระดาษ — ลายเซ็นของหน้า */
  .price-tag{
    align-self:flex-start;
    background:var(--tag);
    border:1.5px dashed var(--marigold);
    border-radius:4px 12px 12px 4px;
    padding:3px 12px 3px 18px;
    font-family:'Mitr',sans-serif;font-weight:600;
    position:relative;
  }
  .price-tag::before{
    content:'';position:absolute;left:6px;top:50%;
    width:6px;height:6px;border-radius:50%;
    background:var(--paper);border:1.5px solid var(--marigold);
    transform:translateY(-50%);
  }
  .btn{
    border:none;border-radius:10px;cursor:pointer;
    padding:10px 14px;font-size:.95rem;font-weight:500;
    background:var(--cobalt);color:#fff;
    transition:background .15s;
  }
  .btn:hover{background:#173FB0}
  .btn:focus-visible{outline:3px solid var(--marigold);outline-offset:2px}
  .btn.ghost{background:transparent;color:var(--cobalt);border:1.5px solid var(--cobalt)}
  .btn.ghost:hover{background:rgba(31,79,216,.08)}

  /* ===== Cart drawer ===== */
  #overlay{
    position:fixed;inset:0;background:rgba(26,34,56,.45);
    opacity:0;pointer-events:none;transition:opacity .25s;z-index:90;
  }
  #overlay.show{opacity:1;pointer-events:auto}
  #drawer{
    position:fixed;top:0;right:-360px;width:min(360px,92vw);height:100%;
    background:#fff;z-index:100;
    display:flex;flex-direction:column;
    transition:right .28s ease;
    box-shadow:-8px 0 30px rgba(0,0,0,.15);
  }
  #drawer.show{right:0}
  #drawer header{
    background:var(--ink);position:static;
  }
  #cartItems{flex:1;overflow-y:auto;padding:16px}
  .cart-row{
    display:flex;align-items:center;gap:12px;
    padding:10px 0;border-bottom:1px dashed #DDD;
  }
  .cart-row .emoji{font-size:1.8rem}
  .cart-row .info{flex:1}
  .cart-row .info b{font-family:'Mitr',sans-serif;font-weight:500;font-size:.95rem}
  .qty{display:flex;align-items:center;gap:8px}
  .qty button{
    width:26px;height:26px;border-radius:50%;
    border:1.5px solid var(--cobalt);background:#fff;color:var(--cobalt);
    font-weight:700;cursor:pointer;
  }
  .empty{color:#999;text-align:center;margin-top:40px}
  #drawer footer{padding:16px;border-top:2px solid var(--ink)}
  .total-line{
    display:flex;justify-content:space-between;
    font-family:'Mitr',sans-serif;font-weight:600;font-size:1.15rem;
    margin-bottom:12px;
  }
  #checkoutBtn{width:100%;background:var(--leaf)}
  #checkoutBtn:hover{background:#166647}

  /* ===== Toast ===== */
  #toast{
    position:fixed;bottom:24px;left:50%;transform:translate(-50%,80px);
    background:var(--ink);color:#fff;padding:10px 22px;border-radius:999px;
    font-size:.9rem;transition:transform .3s;z-index:120;
  }
  #toast.show{transform:translate(-50%,0)}

  footer.site{
    text-align:center;padding:24px;color:#888;font-size:.85rem;
    border-top:1.5px solid #E8E4DA;
  }
  @media (prefers-reduced-motion: reduce){
    *{transition:none!important}
  }
</style>
</head>
<body>

<header>
  <h1>ตลาด<span>นัด</span> ONLINE</h1>
  <button id="cartBtn" onclick="toggleCart(true)">🛒 ตะกร้า (<span id="cartCount">0</span>)</button>
</header>

<section class="hero">
  <h2>ของดี <em>ส่งตรงถึงบ้าน</em></h2>
  <p>ร้านค้าออนไลน์ตัวอย่าง — กดเพิ่มสินค้าลงตะกร้า ปรับจำนวน แล้วลองสั่งซื้อได้เลย</p>
</section>

<main class="grid" id="productGrid"></main>

<footer class="site">© 2026 ตลาดนัด ONLINE — เว็บตัวอย่างเพื่อการเรียนรู้</footer>

<!-- Cart drawer -->
<div id="overlay" onclick="toggleCart(false)"></div>
<aside id="drawer" aria-label="ตะกร้าสินค้า">
  <header>
    <h1>ตะกร้าของฉัน</h1>
    <button id="cartBtn" onclick="toggleCart(false)">ปิด ✕</button>
  </header>
  <div id="cartItems"></div>
  <footer>
    <div class="total-line"><span>รวมทั้งหมด</span><span id="totalPrice">฿0</span></div>
    <button class="btn" id="checkoutBtn" onclick="checkout()">สั่งซื้อสินค้า</button>
  </footer>
</aside>

<div id="toast"></div>

<script>
// ====== ข้อมูลสินค้า (แก้ตรงนี้เพื่อเปลี่ยนสินค้า) ======
const products = [
  {id:1, name:"เสื้อยืดคอตตอน",   desc:"ผ้านุ่ม ใส่สบาย มีทุกไซซ์",        price:259, emoji:"👕", bg:"#EAF0FF"},
  {id:2, name:"กระเป๋าผ้าลดโลกร้อน", desc:"ผ้าแคนวาสหนา สกรีนลายน่ารัก",   price:159, emoji:"👜", bg:"#FFF3D6"},
  {id:3, name:"แก้วเก็บความเย็น",  desc:"เก็บเย็น 12 ชม. ขนาด 750ml",       price:399, emoji:"🥤", bg:"#E4F5EE"},
  {id:4, name:"สติกเกอร์เซ็ต",     desc:"กันน้ำ 20 ชิ้น ติดโน้ตบุ๊กได้",     price:79,  emoji:"✨", bg:"#FDEAEA"},
  {id:5, name:"หมวกแก๊ป",         desc:"ปรับขนาดได้ ปักลายพรีเมียม",        price:299, emoji:"🧢", bg:"#EAF0FF"},
  {id:6, name:"สมุดโน้ตปกแข็ง",    desc:"กระดาษถนอมสายตา 120 แผ่น",         price:129, emoji:"📓", bg:"#FFF3D6"},
];

const cart = {}; // {id: จำนวน}

// ====== แสดงสินค้า ======
const grid = document.getElementById('productGrid');
grid.innerHTML = products.map(p => `
  <div class="card">
    <div class="thumb" style="background:${p.bg}">${p.emoji}</div>
    <div class="card-body">
      <h3>${p.name}</h3>
      <p>${p.desc}</p>
      <span class="price-tag">฿${p.price}</span>
      <button class="btn" onclick="addToCart(${p.id})">เพิ่มลงตะกร้า</button>
    </div>
  </div>
`).join('');

// ====== ตะกร้า ======
function addToCart(id){
  cart[id] = (cart[id]||0) + 1;
  renderCart();
  showToast('เพิ่มลงตะกร้าแล้ว ✔');
}
function changeQty(id, delta){
  cart[id] += delta;
  if(cart[id] <= 0) delete cart[id];
  renderCart();
}
function renderCart(){
  const box = document.getElementById('cartItems');
  const ids = Object.keys(cart);
  let total = 0, count = 0;
  if(ids.length === 0){
    box.innerHTML = '<p class="empty">ตะกร้ายังว่างอยู่<br>เลือกของถูกใจได้เลย 🛍️</p>';
  } else {
    box.innerHTML = ids.map(id => {
      const p = products.find(x => x.id == id);
      const qty = cart[id];
      total += p.price * qty; count += qty;
      return `
        <div class="cart-row">
          <span class="emoji">${p.emoji}</span>
          <div class="info"><b>${p.name}</b><br><small>฿${p.price} × ${qty} = ฿${p.price*qty}</small></div>
          <div class="qty">
            <button onclick="changeQty(${id},-1)" aria-label="ลดจำนวน">−</button>
            <span>${qty}</span>
            <button onclick="changeQty(${id},1)" aria-label="เพิ่มจำนวน">+</button>
          </div>
        </div>`;
    }).join('');
  }
  document.getElementById('totalPrice').textContent = '฿' + total.toLocaleString();
  document.getElementById('cartCount').textContent = count;
}
function toggleCart(open){
  document.getElementById('drawer').classList.toggle('show', open);
  document.getElementById('overlay').classList.toggle('show', open);
}
function checkout(){
  const ids = Object.keys(cart);
  if(ids.length === 0){ showToast('ตะกร้ายังว่างอยู่นะ'); return; }
  let total = 0;
  ids.forEach(id => { const p = products.find(x=>x.id==id); total += p.price*cart[id]; });
  alert('✅ สั่งซื้อสำเร็จ! ยอดรวม ฿' + total.toLocaleString() + '\n(เว็บตัวอย่าง — ยังไม่ตัดเงินจริง)');
  ids.forEach(id => delete cart[id]);
  renderCart();
  toggleCart(false);
}
function showToast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'), 1600);
}
renderCart();
</script>
</body>
</html>
