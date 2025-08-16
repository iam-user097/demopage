<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MarketX.com</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      background: #f9f9f9;
      color: #333;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    header {
      background: #fff;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 15px 30px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      position: sticky;
      top: 0;
      z-index: 1000;
    }

    .logo {
      font-size: 22px;
      font-weight: bold;
      color: #e60023;
    }

    .header-buttons {
      display: flex;
      gap: 15px;
    }

    .header-buttons button {
      padding: 8px 16px;
      border: none;
      border-radius: 20px;
      background: #e60023;
      color: #fff;
      cursor: pointer;
      font-size: 14px;
      transition: all 0.3s ease;
    }

    .header-buttons button:hover {
      background: #b8001c;
      transform: scale(1.05);
    }

    .search-bar {
      margin: 20px auto;
      max-width: 600px;
      display: flex;
      border: 1px solid #ddd;
      border-radius: 30px;
      overflow: hidden;
    }

    .search-bar input {
      flex: 1;
      padding: 12px;
      border: none;
      outline: none;
      font-size: 15px;
    }

    .search-bar button {
      padding: 12px 20px;
      border: none;
      background: #e60023;
      color: white;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    .search-bar button:hover {
      background: #b8001c;
    }

    .categories {
      padding: 30px;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 20px;
      flex-grow: 1;
    }

    .category-card {
      background: white;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      text-align: center;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      cursor: pointer;
    }

    .category-card img {
      width: 80px;
      height: 80px;
      object-fit: contain;
      margin-bottom: 15px;
    }

    .category-card h3 {
      font-size: 16px;
    }

    .category-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 8px 15px rgb(0, 0, 7);
    }

    .products-section {
      padding: 30px;
    }

    .products-section h2 {
      margin-bottom: 15px;
      font-size: 22px;
      color: #e60023;
    }

    .products-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
    }

    .product-card {
      background: #fff;
      padding: 15px;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      text-align: center;
      transition: transform 0.3s ease;
    }

    .product-card img {
      width: 100%;
      height: 160px;
      object-fit: contain;
      margin-bottom: 10px;
    }

    .product-card h4 {
      font-size: 16px;
      margin-bottom: 5px;
    }

    .product-card p {
      font-size: 14px;
      margin: 2px 0;
    }

    .product-card .edit-btn,
    .product-card .delete-btn,
    .product-card .order-btn {
      margin: 5px 4px 0 4px;
      padding: 6px 14px;
      border-radius: 16px;
      border: none;
      font-size: 13px;
      cursor: pointer;
      transition: background 0.3s;
    }
    .product-card .edit-btn {
      background: #ffb300;
      color: #222;
    }
    .product-card .edit-btn:hover {
      background: #ffd54f;
    }
    .product-card .delete-btn {
      background: #e60023;
      color: #fff;
    }
    .product-card .delete-btn:hover {
      background: #b8001c;
    }
    .product-card .order-btn {
      background: #00b894;
      color: #fff;
    }
    .product-card .order-btn:hover {
      background: #00916e;
    }

    .product-card:hover {
      transform: translateY(-6px);
    }

    footer {
      background: #222;
      color: #fff;
      text-align: center;
      padding: 15px;
      margin-top: auto;
    }

    @media (max-width: 768px) {
      .header-buttons button {
        font-size: 12px;
        padding: 6px 12px;
      }
    }
  </style>
</head>
<body>

  <!-- Header -->
  <header>
    <div class="logo">MarketX</div>
    <div class="header-buttons">
      <button onclick="goToLogin('admin')">Admin Login</button>
      <button onclick="goToLogin('customer')">Customer Login</button>
      <button id="addProductBtn" style="display:none;" onclick="window.location.href='product.html'">Add Product</button>
      <button id="logoutBtn" style="display:none;" onclick="logoutAdmin()">Logout</button>
    </div>
  </header>

  <!-- Search Bar -->
  <div class="search-bar">
    <input type="text" id="searchInput" placeholder="Search Product/Category/Brand...">
    <button onclick="searchProducts()">Search</button>
  </div>

  <!-- Categories -->
  <section class="categories" id="categories-section">
    <div class="category-card" data-category="Power Tools"><img src="https://cdn-icons-png.flaticon.com/512/679/679720.png"><h3>Power Tools</h3></div>
    <div class="category-card" data-category="Electricals"><img src="https://cdn-icons-png.flaticon.com/512/1048/1048953.png"><h3>Electricals</h3></div>
    <div class="category-card" data-category="Appliances & Utilities"><img src="https://cdn-icons-png.flaticon.com/512/869/869869.png"><h3>Appliances & Utilities</h3></div>
    <div class="category-card" data-category="Safety"><img src="https://cdn-icons-png.flaticon.com/512/3062/3062634.png"><h3>Safety</h3></div>
    <div class="category-card" data-category="Medical Supplies"><img src="https://cdn-icons-png.flaticon.com/512/2972/2972398.png"><h3>Medical Supplies</h3></div>
    <div class="category-card" data-category="Office Supplies"><img src="https://cdn-icons-png.flaticon.com/512/2921/2921822.png"><h3>Office Supplies</h3></div>
    <div class="category-card" data-category="Gardening"><img src="garden.jpg"><h3>Gardening</h3></div>
    <div class="category-card" data-category="Security"><img src="https://cdn-icons-png.flaticon.com/512/3132/3132084.png"><h3>Security</h3></div>
    <div class="category-card" data-category="Plumbing & Fittings"><img src="https://cdn-icons-png.flaticon.com/512/2284/2284909.png"><h3>Plumbing & Fittings</h3></div>
  </section>

  <!-- Products Section -->
  <div id="products-container"></div>

  <!-- Footer -->
  <footer>
    <p>© 2025 MarketX. All Rights Reserved.</p>
  </footer>

<script>
    function goToLogin(type) {
      if (type === "admin") {
        window.location.href = "admin.html";
      } else if (type === "customer") {
        window.location.href = "customer.html";
      }
    }

    function isAdmin() {
      return localStorage.getItem("isAdmin") === "true";
    }

    document.addEventListener("DOMContentLoaded", function() {
      if (isAdmin()) {
        document.getElementById("addProductBtn").style.display = "inline-block";
        document.getElementById("logoutBtn").style.display = "inline-block";
      } else {
        document.getElementById("addProductBtn").style.display = "none";
        document.getElementById("logoutBtn").style.display = "none";
      }

      document.querySelectorAll('.category-card').forEach(card => {
        card.addEventListener('click', function() {
          const category = this.getAttribute('data-category');
          document.getElementById("searchInput").value = "";
          loadProducts("", category);
        });
      });

      loadProducts();
      renderOrderRequests();
    });

    function logoutAdmin() {
      localStorage.removeItem("isAdmin");
      window.location.reload();
    }

    function loadProducts(searchQuery = "", categoryFilter = "") {
      const products = JSON.parse(localStorage.getItem("products")) || [];
      const container = document.getElementById("products-container");
      container.innerHTML = "";

      const filtered = products.filter(p => {
        const matchesSearch = p.name && p.name.toLowerCase().includes(searchQuery) ||
                              p.category && p.category.toLowerCase().includes(searchQuery);
        const matchesCategory = categoryFilter ? p.category === categoryFilter : true;
        return matchesSearch && matchesCategory;
      });

      if (filtered.length === 0) {
         container.innerHTML = "<p style='text-align:center; padding:20px;'>No products found.</p>";
        return;
      }

      const grouped = {};
      filtered.forEach(p => {
        if (!grouped[p.category]) grouped[p.category] = [];
        grouped[p.category].push(p);
      });

      for (let category in grouped) {
        let section = document.createElement("section");
        section.classList.add("products-section");

        section.innerHTML = `<h2>${category}</h2>
          <div class="products-grid">
            ${grouped[category].map((prod) => `
              <div class="product-card" data-id="${prod.id}">
                <img src="${prod.images && prod.images[0] ? prod.images[0] : ''}" alt="${prod.name}">
                <h4>${prod.name}</h4>
                <p>Price: ₹${prod.totalPrice !== undefined ? prod.totalPrice : ''}</p>
                <p><small>Discount: ${prod.discount !== undefined ? prod.discount : 0}%</small></p>
                ${
                  isAdmin()
                  ? `<button class="edit-btn" onclick="editProduct('${prod.id}')">Edit</button>
                     <button class="delete-btn" onclick="deleteProduct('${prod.id}')">Delete</button>`
                  : `<button class="order-btn" onclick="orderProduct('${prod.id}')">Order</button>`
                }
              </div>
            `).join("")}
          </div>
        `;

        container.appendChild(section);
      }
    }

    function searchProducts() {
      const query = document.getElementById("searchInput").value.toLowerCase().trim();
      loadProducts(query);
    }

    function deleteProduct(id) {
      if (!isAdmin()) return;
      if (!confirm("Are you sure you want to delete this product?")) return;
      let products = JSON.parse(localStorage.getItem("products")) || [];
      products = products.filter(p => p.id !== id);
      localStorage.setItem("products", JSON.stringify(products));
      loadProducts();
      renderOrderRequests();
    }

    function editProduct(id) {
      if (!isAdmin()) return;
      let products = JSON.parse(localStorage.getItem("products")) || [];
      const prod = products.find(p => p.id === id);
      if (!prod) return;

      const name = prompt("Edit Product Name:", prod.name);
      if (name === null) return;
      const price = prompt("Edit Price:", prod.totalPrice);
      if (price === null) return;
      const discount = prompt("Edit Discount (%):", prod.discount);
      if (discount === null) return;

      prod.name = name;
      prod.totalPrice = price;
      prod.discount = discount;

      localStorage.setItem("products", JSON.stringify(products));
      loadProducts();
      renderOrderRequests();
    }

    function orderProduct(id) {
      if (isAdmin()) return;
      let products = JSON.parse(localStorage.getItem("products")) || [];
      const prod = products.find(p => p.id === id);
      if (!prod) return;

      let contact = prompt("Enter your Contact Number:");
      if (!contact || !/^\d{10,}$/.test(contact.trim())) {
        alert("Please enter a valid contact number.");
        return;
      }
      let address = prompt("Enter your Home Address:");
      if (!address || address.trim().length < 5) {
        alert("Please enter a valid address.");
        return;
      }

      let orders = JSON.parse(localStorage.getItem("orderRequests")) || [];
      orders.push({
        productId: prod.id,
        productName: prod.name,
        price: prod.totalPrice,
        discount: prod.discount,
        contact: contact.trim(),
        address: address.trim(),
        date: new Date().toLocaleString()
      });
      localStorage.setItem("orderRequests", JSON.stringify(orders));
      alert("Order placed! Your request has been sent to admin.");
    }

    // Admin: Render order requests with Accept button
    function renderOrderRequests() {
      if (!isAdmin()) return;
      let orders = JSON.parse(localStorage.getItem("orderRequests")) || [];
      let products = JSON.parse(localStorage.getItem("products")) || [];
      let oldSection = document.getElementById("order-requests-section");
      if (oldSection) oldSection.remove();

      if (orders.length === 0) return;

      let section = document.createElement("section");
      section.classList.add("products-section");
      section.id = "order-requests-section";
      section.innerHTML = `<h2>Order Requests</h2>
        <div class="products-grid">
          ${orders.map((order, idx) => {
            let prod = products.find(p => p.id === order.productId);
            let img = prod && prod.images && prod.images[0] ? prod.images[0] : '';
            return `
              <div class="product-card">
                <img src="${img}" alt="${order.productName}">
                <h4>${order.productName}</h4>
                <p>Price: ₹${order.price}</p>
                <p>Discount: ${order.discount}%</p>
                <p><b>Contact:</b> ${order.contact}</p>
                <p><b>Address:</b> ${order.address}</p>
                <p><small>Ordered at: ${order.date}</small></p>
                <button class="order-btn" onclick="acceptOrder(${idx})">Accept</button>
              </div>
            `;
          }).join("")}
        </div>
      `;
      document.body.insertBefore(section, document.querySelector("footer"));
    }

    function acceptOrder(idx) {
      if (!isAdmin()) return;
      let orders = JSON.parse(localStorage.getItem("orderRequests")) || [];
      if (orders[idx]) {
        alert("Order accepted!");
        orders.splice(idx, 1);
        localStorage.setItem("orderRequests", JSON.stringify(orders));
        renderOrderRequests();
      }
    }

    if (window.location.search.includes("admin=1")) {
      localStorage.setItem("isAdmin",
