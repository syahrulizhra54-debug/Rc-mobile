# Rc-mobile
Jual RC berkualitas 
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy RC Toys - Mainan RC Seru</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      background-color: #fff8f0;
      color: #333;
    }
    header {
      background-color: #ffcc00;
      text-align: center;
      padding: 20px;
    }
    header h1 {
      margin: 0;
      color: #fff;
      font-size: 2rem;
    }
    .hero {
      text-align: center;
      padding: 20px;
    }
    .hero img {
      width: 300px;
      border-radius: 10px;
    }
    .products {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
      padding: 20px;
    }
    .product-card {
      background-color: #fff;
      border: 2px solid #ffcc00;
      border-radius: 10px;
      width: 220px;
      text-align: center;
      padding: 15px;
      transition: transform 0.2s;
    }
    .product-card:hover {
      transform: scale(1.05);
    }
    .product-card img {
      width: 100%;
      border-radius: 8px;
    }
    .product-card h3 {
      margin: 10px 0 5px;
    }
    .product-card p {
      margin: 5px 0;
    }
    .product-card button {
      padding: 10px 15px;
      background-color: #ff6600;
      color: white;
      border: none;
      border-radius: 5px;
      font-weight: bold;
      cursor: pointer;
    }
    .cart {
      position: fixed;
      top: 50%;
      right: 0;
      background-color: #ffcc00;
      padding: 15px;
      border-radius: 10px 0 0 10px;
      width: 250px;
      transform: translateY(-50%);
      box-shadow: -2px 2px 10px rgba(0,0,0,0.2);
    }
    .cart h3 {
      margin-top: 0;
    }
    .cart-items {
      max-height: 300px;
      overflow-y: auto;
      margin-bottom: 10px;
    }
    .cart-item {
      display: flex;
      justify-content: space-between;
      margin-bottom: 5px;
    }
    .cart-item span {
      font-size: 0.9rem;
    }
    .checkout-btn {
      display: block;
      width: 100%;
      text-align: center;
      background-color: #ff6600;
      color: white;
      padding: 10px;
      border-radius: 5px;
      text-decoration: none;
      font-weight: bold;
    }
    footer {
      background-color: #ffcc00;
      text-align: center;
      padding: 15px;
      color: #fff;
      margin-top: 20px;
    }
  </style>
</head>
<body>

<header>
  <h1>Happy RC Toys</h1>
  <p>🚗 Mobil • ✈️ Pesawat • 🚁 Helikopter RC Seru & Berkualitas!</p>
</header>

<section class="hero">
  <img src="https://i.ibb.co/4p8H6Rv/happy-rc-toys-hero.png" alt="Happy RC Toys Banner">
</section>

<section class="products">
  <!-- Product 1 -->
  <div class="product-card" data-name="Mobil RC Turbo" data-price="150000">
    <img src="https://i.ibb.co/7YZ6W3k/rc-car.png" alt="Mobil RC">
    <h3>Mobil RC Turbo</h3>
    <p>Harga: Rp150.000</p>
    <button onclick="addToCart(this)">Tambah ke Keranjang</button>
  </div>

  <!-- Product 2 -->
  <div class="product-card" data-name="Helikopter RC Terbang" data-price="200000">
    <img src="https://i.ibb.co/0Yw6j6K/rc-helicopter.png" alt="Helikopter RC">
    <h3>Helikopter RC Terbang</h3>
    <p>Harga: Rp200.000</p>
    <button onclick="addToCart(this)">Tambah ke Keranjang</button>
  </div>

  <!-- Product 3 -->
  <div class="product-card" data-name="Pesawat RC Mini" data-price="180000">
    <img src="https://i.ibb.co/6WtJtXc/rc-plane.png" alt="Pesawat RC">
    <h3>Pesawat RC Mini</h3>
    <p>Harga: Rp180.000</p>
    <button onclick="addToCart(this)">Tambah ke Keranjang</button>
  </div>
</section>

<div class="cart" id="cart">
  <h3>Keranjang Belanja</h3>
  <div class="cart-items" id="cart-items">
    <p>Belum ada produk</p>
  </div>
  <p>Total: Rp<span id="cart-total">0</span></p>
  <a href="#" target="_blank" id="checkout-btn" class="checkout-btn">Checkout via WhatsApp</a>
</div>

<footer>
  <p>Happy RC Toys | Siap Kirim ke Seluruh Indonesia 🚚</p>
  <p>Hubungi Kami: <a href="https://wa.me/628123456789" style="color:white; font-weight:bold;">WhatsApp</a></p>
</footer>

<script>
let cart = [];

function addToCart(button) {
  const card = button.parentElement;
  const name = card.getAttribute('data-name');
  const price = parseInt(card.getAttribute('data-price'));

  // Tambahkan ke cart
  cart.push({name, price});
  updateCart();
}

function updateCart() {
  const cartItemsDiv = document.getElementById('cart-items');
  const cartTotal = document.getElementById('cart-total');
  const checkoutBtn = document.getElementById('checkout-btn');

  cartItemsDiv.innerHTML = '';
  let total = 0;
  cart.forEach((item, index) => {
    total += item.price;
    const div = document.createElement('div');
    div.className = 'cart-item';
    div.innerHTML = `<span>${item.name}</span> <span>Rp${item.price.toLocaleString()}</span>`;
    cartItemsDiv.appendChild(div);
  });

  if(cart.length === 0) {
    cartItemsDiv.innerHTML = '<p>Belum ada produk</p>';
  }

  cartTotal.innerText = total.toLocaleString();

  // Buat link WhatsApp
  let waMessage = 'Halo Happy RC Toys! Saya ingin memesan:\n';
  cart.forEach(item => {
    waMessage += `- ${item.name} (Rp${item.price.toLocaleString()})\n`;
  });
  waMessage += `Total: Rp${total.toLocaleString()}`;

  const waLink = `https://wa.me/628123456789?text=${encodeURIComponent(waMessage)}`;
  checkoutBtn.setAttribute('href', waLink);
}
</script>

</body>
</html>
