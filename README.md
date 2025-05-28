<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>MKS Wonders - Full E-Commerce Site</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; background: #f2f2f2; }
    header { background: #4CAF50; color: white; padding: 1rem; text-align: center; font-size: 1.8rem; font-weight: bold; }
    nav { display: flex; justify-content: space-around; background: #333; padding: 0.5rem; }
    nav button { background: none; border: none; color: white; font-size: 1rem; cursor: pointer; }
    nav button:hover { text-decoration: underline; }
    .products, .cart-section, .checkout, .credits-info { padding: 1rem; display: none; }
    .products.active, .cart-section.active, .checkout.active, .credits-info.active { display: block; }
    .product-card { background: white; border-radius: 10px; box-shadow: 0 0 5px rgba(0,0,0,0.2); margin: 1rem 0; padding: 1rem; }
    .product-card h3 { margin-top: 0; }
    .product-card button { background: #4CAF50; color: white; border: none; padding: 0.5rem 1rem; cursor: pointer; border-radius: 5px; }
    .cart-items, .review-box { margin-top: 1rem; }
    .checkout input, .checkout textarea { display: block; width: 100%; margin: 0.5rem 0; padding: 0.5rem; }
    .whatsapp-button { background: #25D366; color: white; padding: 0.5rem 1rem; text-decoration: none; display: inline-block; margin-top: 1rem; border-radius: 5px; }
  </style>
</head>
<body>
  <header>MKS Wonders 🛍️</header>
  <nav>
    <button onclick="showSection('products')">Home</button>
    <button onclick="showSection('cart-section')">Cart 🛒</button>
    <button onclick="showSection('checkout')">Checkout</button>
    <button onclick="showSection('credits-info')">Credits</button>
  </nav>  <section class="products active" id="products"></section>  <section class="cart-section" id="cart-section">
    <h2>Your Cart</h2>
    <div class="cart-items" id="cart-items"></div>
    <p>Total: ₹<span id="total-price">0</span></p>
  </section>  <section class="checkout" id="checkout">
    <h2>Checkout</h2>
    <input type="text" id="name" placeholder="Your Name" required />
    <input type="email" id="email" placeholder="Email" required />
    <input type="tel" id="phone" placeholder="Phone" required />
    <textarea id="address" placeholder="Address"></textarea>
    <button onclick="completePurchase()">Place Order</button>
    <a class="whatsapp-button" id="whatsapp-link" target="_blank">WhatsApp Order 📲</a>
  </section>  <section class="credits-info" id="credits-info">
    <h2>Your Wallet</h2>
    <p>You have <strong id="credits">10000</strong> credits.</p>
    <p>Use credits to purchase your favorite items 🎮</p>
  </section>  <script>
    const products = [
      { id: 1, name: "Magic Notebook", price: 250, review: "Amazing quality!", shipping: "2-3 days" },
      { id: 2, name: "Puzzle Box", price: 499, review: "Very creative toy.", shipping: "3-5 days" },
      { id: 3, name: "Color Pens Set", price: 199, review: "Loved the vibrant colors.", shipping: "1-2 days" },
      { id: 4, name: "Educational Game", price: 799, review: "Fun and learning.", shipping: "4-5 days" },
      { id: 5, name: "Birthday Decoration Kit", price: 599, review: "Made the party awesome!", shipping: "2 days" },
      { id: 6, name: "LED Study Lamp", price: 899, review: "Perfect lighting for study.", shipping: "1-3 days" },
      { id: 7, name: "Gift Box Surprise", price: 299, review: "Best gift ever!", shipping: "2-4 days" },
      { id: 8, name: "Science Experiment Kit", price: 999, review: "Very educational.", shipping: "3-6 days" },
      { id: 9, name: "Cartoon Pencil Pouch", price: 149, review: "Kids loved it!", shipping: "2 days" },
      { id: 10, name: "Handmade Diary", price: 349, review: "Looks premium.", shipping: "2-3 days" },
      { id: 11, name: "Crayons Mega Pack", price: 199, review: "So many shades!", shipping: "2 days" },
      { id: 12, name: "Glow in Dark Stickers", price: 179, review: "Glows nicely at night.", shipping: "1 day" },
      { id: 13, name: "Origami Set", price: 129, review: "Fun time pass.", shipping: "2-3 days" },
      { id: 14, name: "Board Game Combo", price: 1099, review: "Family fun!", shipping: "4 days" },
      { id: 15, name: "Teddy Keychain", price: 89, review: "Cute and soft.", shipping: "2 days" },
      { id: 16, name: "Scented Gel Pens", price: 159, review: "Smells great!", shipping: "2-3 days" },
      { id: 17, name: "Motivational Posters", price: 349, review: "Boosts mindset.", shipping: "2 days" },
      { id: 18, name: "Cartoon Books Set", price: 699, review: "Great collection.", shipping: "3-5 days" },
      { id: 19, name: "Kids Watch", price: 499, review: "Stylish and cool.", shipping: "3 days" },
      { id: 20, name: "Stationery Kit", price: 599, review: "All-in-one set.", shipping: "1-2 days" }
    ];

    let cart = [];
    let credits = 10000;

    const productsContainer = document.getElementById("products");
    const cartItems = document.getElementById("cart-items");
    const totalPrice = document.getElementById("total-price");
    const creditsDisplay = document.getElementById("credits");

    function showSection(id) {
      document.querySelectorAll("section").forEach(s => s.classList.remove("active"));
      document.getElementById(id).classList.add("active");
    }

    function renderProducts() {
      products.forEach(product => {
        const card = document.createElement("div");
        card.className = "product-card";
        card.innerHTML = `
          <h3>${product.name}</h3>
          <p>₹${product.price}</p>
          <p>Review: "${product.review}"</p>
          <p>Shipping: ${product.shipping}</p>
          <button onclick='addToCart(${JSON.stringify(product)})'>Add to Cart</button>
        `;
        productsContainer.appendChild(card);
      });
    }

    function addToCart(product) {
      if (credits >= product.price) {
        cart.push(product);
        credits -= product.price;
        creditsDisplay.textContent = credits;
        updateCart();
      } else {
        alert("Not enough credits!");
      }
    }

    function updateCart() {
      cartItems.innerHTML = "";
      let total = 0;
      cart.forEach(item => {
        total += item.price;
        const div = document.createElement("div");
        div.textContent = `${item.name} - ₹${item.price}`;
        cartItems.appendChild(div);
      });
      totalPrice.textContent = total;
    }

    function completePurchase() {
      const name = document.getElementById("name").value;
      const phone = document.getElementById("phone").value;
      const address = document.getElementById("address").value;
      const items = cart.map(item => item.name).join(", ");
      
      let orderMsg = `New Order from MKS Wonders%0A%0AName: ${name}%0APhone: ${phone}%0AAddress: ${address}%0AItems:`;
      let total = 0;
      cart.forEach(item => {
        orderMsg += `%0A- ${item.name} (₹${item.price})`;
        total += item.price;
      });
      orderMsg += `%0A%0ATotal: ₹${total}`;
document.getElementById("whatsapp-link").href =`https://wa.me/8433076349?text=${msg}`;
      alert("Order placed! Click WhatsApp to confirm.");
    }

    renderProducts();
  </script></body>
</html>
