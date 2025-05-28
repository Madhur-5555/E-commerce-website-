<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>MKS Wonders - Premium E-Commerce</title>
<style>
/* === CSS Start === */
* {
  margin: 0; padding: 0; box-sizing: border-box;
}
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: #fafafa;
  color: #333;
  line-height: 1.6;
}
/* Header */
.header {
  background: #222;
  color: white;
  padding: 1rem 0;
}
.nav-container {
  width: 90%;
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.logo {
  font-size: 2rem;
  font-weight: 700;
}
nav a {
  color: white;
  text-decoration: none;
  margin-left: 1rem;
  font-weight: 600;
}
nav a:hover {
  text-decoration: underline;
}

/* Product Grid */
.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(240px,1fr));
  gap: 1rem;
  padding: 2rem;
  max-width: 1100px;
  margin: auto;
}
.product-card {
  background: white;
  padding: 1rem;
  border-radius: 16px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.1);
  transition: box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.product-card:hover {
  box-shadow: 0 12px 30px rgba(0,0,0,0.2);
}
.product-card img {
  max-width: 100%;
  border-radius: 12px;
  object-fit: cover;
  height: 180px;
}
.btn-buy {
  background: #00c851;
  border: none;
  padding: 0.7rem 1.2rem;
  color: white;
  border-radius: 30px;
  cursor: pointer;
  font-weight: 700;
  margin-top: auto;
  transition: background 0.3s ease;
}
.btn-buy:hover {
  background: #007e33;
}

/* Reviews */
.reviews {
  margin-top: 1rem;
  padding: 1rem;
  background: #f9f9f9;
  border-radius: 12px;
  box-shadow: inset 0 0 8px rgba(0, 0, 0, 0.05);
  width: 100%;
}
.review p {
  margin: 0.2rem 0;
  font-size: 0.95rem;
}

/* Sections */
.section-title {
  text-align: center;
  margin: 2rem 0 1rem 0;
  font-size: 2rem;
  color: #222;
}
.cart-section, .checkout-section, .payment-section, .thankyou-section {
  max-width: 600px;
  margin: 3rem auto;
  padding: 2rem;
  background: white;
  border-radius: 20px;
  box-shadow: 0 8px 30px rgba(0,0,0,0.1);
  text-align: center;
}
.cart-section h2, .checkout-section h2, .payment-section h2, .thankyou-section h2 {
  margin-bottom: 1rem;
  color: #00c851;
}
.cart-section button, .checkout-section button, .payment-section button {
  background: #00c851;
  border: none;
  padding: 0.7rem 1.2rem;
  color: white;
  border-radius: 30px;
  cursor: pointer;
  font-weight: 700;
  transition: background 0.3s ease;
}
.cart-section button:hover, .checkout-section button:hover, .payment-section button:hover {
  background: #007e33;
}
label {
  display: block;
  margin: 0.8rem 0 0.2rem 0;
  font-weight: 600;
  text-align: left;
}
input, textarea {
  width: 100%;
  padding: 0.5rem;
  border-radius: 12px;
  border: 1px solid #ccc;
  font-size: 1rem;
  resize: vertical;
}
input[type=number]::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
input[type=number] {
  -moz-appearance: textfield;
}

/* Navigation Buttons for Sections */
.nav-btn {
  background: #00c851;
  border: none;
  padding: 0.6rem 1rem;
  color: white;
  border-radius: 30px;
  cursor: pointer;
  font-weight: 700;
  margin: 0.5rem;
  transition: background 0.3s ease;
}
.nav-btn:hover {
  background: #007e33;
}

/* Hide all sections except home on load */
.section {
  display: none;
}
.section.active {
  display: block;
}
</style>
</head>
<body>

<!-- Header -->
<header class="header">
  <div class="nav-container">
    <div class="logo">MKS Wonders</div>
    <nav>
      <a href="#" class="nav-link" data-target="home">Home</a>
      <a href="#" class="nav-link" data-target="cart">Cart</a>
      <a href="#" class="nav-link" data-target="checkout">Checkout</a>
      <a href="#" class="nav-link" data-target="payment">Payment</a>
      <a href="#" class="nav-link" data-target="thankyou">Thank You</a>
    </nav>
  </div>
</header>

<!-- Sections -->

<!-- Home Section (Products) -->
<section id="home" class="section active">
  <h1 class="section-title">Welcome to MKS Wonders</h1>
  <div class="product-grid" id="productGrid">
    <!-- Products loaded by JS -->
  </div>
</section>

<!-- Cart Section -->
<section id="cart" class="section cart-section">
  <h2>Your Cart</h2>
  <div id="cart-items"></div>
  <div id="cart-total"></div>
  <button class="nav-btn" id="checkoutBtn">Proceed to Checkout</button>
</section>

<!-- Checkout Section -->
<section id="checkout" class="section checkout-section">
  <h2>Checkout - Enter Details</h2>
  <form id="checkoutForm">
    <label for="name">Name:</label>
    <input type="text" id="name" required />

    <label for="email">Email:</label>
    <input type="email" id="email" required />

    <label for="phone">Phone Number:</label>
    <input type="tel" id="phone" required />

    <label for="address">Shipping Address:</label>
    <textarea id="address" rows="3" required></textarea>

    <label for="delivery">Estimated Shipping Time (days):</label>
    <input type="number" id="delivery" min="1" required />

    <button type="submit" class="nav-btn">Continue to Payment</button>
  </form>
</section>

<!-- Payment Section -->
<section id="payment" class="section payment-section">
  <h2>Payment (Using Credits)</h2>
  <p>You have <strong id="creditsCount"></strong> credits.</p>
  <button class="nav-btn" id="finalPayBtn">Pay Now</button>
</section>

<!-- Thank You Section -->
<section id="thankyou" class="section thankyou-section">
  <h2>Thank you for your order!</h2>
  <p>Your order has been placed successfully.</p>
  <button class="nav-btn" id="backToHomeBtn">Back to Home</button>
</section>

<script>
/* === JS Start === */

const products = [
  {id:1, name:"Premium Notebook", price:299, img:"https://images.unsplash.com/photo-1515377905703-c4788e51af15?auto=format&fit=crop&w=400&q=80", reviews: [
    "Very good quality paper.",
    "Perfect for school and office.",
    "Highly recommended!"
  ]},
  {id:2, name:"Toy Car", price:599, img:"https://images.unsplash.com/photo-1508898578281-774ac4893b59?auto=format&fit=crop&w=400&q=80", reviews: [
    "My kid loves it!",
    "Durable and fun.",
    "Great value for money."
  ]},
  {id:3, name:"Colorful Pens Set", price:199, img:"https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?auto=format&fit=crop&w=400&q=80", reviews: [
    "Smooth ink flow.",
    "Bright colors, long-lasting.",
    "Excellent for artists."
  ]},
  {id:4, name:"Birthday Gift Box", price:899, img:"https://images.unsplash.com/photo-1512436991641-6745cdb1723f?auto=format&fit=crop&w=400&q=80", reviews: [
    "Lovely presentation.",
    "Great surprise gift.",
    "Loved the variety inside."
  ]},
  {id:5, name:"Classic Diary", price:399, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews: [
    "Beautiful cover design.",
    "Perfect size to carry around.",
    "Pages are smooth and thick."
  ]},
  {id:6, name:"Puzzle Toy", price:499, img:"https://images.unsplash.com/photo-1532635245-2f1d0f5431ee?auto=format&fit=crop&w=400&q=80", reviews: [
    "Challenging and fun.",
    "Keeps me engaged for hours.",
    "Well made with quality materials."
  ]},
  {id:7, name:"Greeting Cards Set", price:149, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews: [
    "Beautiful designs.",
    "Perfect for any occasion.",
    "Good quality paper."
  ]},
  {id:8, name:"Art Supplies Kit", price:1299, img:"https://images.unsplash.com/photo-1509228627152-4d0f8f1e3168?auto=format&fit=crop&w=400&q=80", reviews: [
    "Complete kit for beginners.",
    "Colors are vibrant.",
    "Great value for money."
  ]},
  {id:9, name:"Desk Organizer", price:799, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews: [
    "Helps keep my desk neat.",
    "Sturdy and stylish.",
    "Easy to assemble."
  ]},
  {id:10, name:"Water Bottle", price:349, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews: [
    "Keeps water cool for hours.",
    "Leak proof design.",
    "Perfect size for gym."
  ]},
  // Add 10 more products similarly
  {id:11, name:"Sketchbook", price:499, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews:["Great paper quality.","Ideal for artists.","Compact size."]},
  {id:12, name:"Stuffed Toy", price:799, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews:["Soft and cuddly.","Perfect gift.","Durable stitching."]},
  {id:13, name:"Birthday Balloons Set", price:299, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews:["Bright colors.","Easy to inflate.","Great decoration."]},
  {id:14, name:"Marker Pens", price:249, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews:["Vibrant colors.","Long-lasting ink.","Smooth writing."]},
  {id:15, name:"Stationery Set", price:699, img:"https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=400&q=80", reviews:["All essentials included.","Good quality.","Compact box."]},
  {id:16, name:"Gift Wrap Paper", price:199, img:"https://images.unsplash.com/photo-1504384308090-c894fd
