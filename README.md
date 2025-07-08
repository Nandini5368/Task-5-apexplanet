<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>ShopSwift – Mini E-Commerce</title>
  <style>
    body { margin:0; font-family:Arial,sans-serif; background:#fafafa; color:#333; }
    header { background:#111; color:#fff; padding:1rem; text-align:center; }
    nav a { color:#fff; margin:0 10px; text-decoration:none; }
    .container { max-width:1200px; margin:auto; padding:1rem; }
    .products { display:grid; grid-template-columns:repeat(auto-fit, minmax(250px, 1fr)); gap:1rem; }
    .card { background:#fff; padding:1rem; border-radius:8px; box-shadow:0 0 10px rgba(0,0,0,0.1); }
    .card img { width:100%; height:200px; object-fit:cover; border-radius:8px; loading:lazy; }
    .card h4 { margin:10px 0 5px; }
    .card button { background:#28a745; color:#fff; border:none; padding:0.5rem 1rem; cursor:pointer; border-radius:4px; }
    .cart { margin-top:2rem; padding:1rem; background:#fff; border-radius:8px; box-shadow:0 0 10px rgba(0,0,0,0.1); }
    footer { background:#111; color:#fff; text-align:center; padding:1rem; margin-top:2rem; }

    @media (max-width:600px) {
      header, footer { font-size:14px; }
      .card img { height:150px; }
    }
  </style>
</head>
<body>

<header>
  <h1>ShopSwift</h1>
  <nav>
    <a href="#products">Products</a>
    <a href="#cart">Cart</a>
  </nav>
</header>

<div class="container" id="products">
  <h2>Our Products</h2>
  <div class="products" id="product-list"></div>
</div>

<div class="container cart" id="cart">
  <h2>Your Cart</h2>
  <ul id="cart-items"></ul>
  <p><strong>Total: $<span id="cart-total">0.00</span></strong></p>
</div>

<footer>
  <p>© 2025 ShopSwift | Built with HTML, CSS & JS</p>
</footer>

<script>
  const products = [
    { id: 1, name: 'Wireless Headphones', price: 59.99, image: 'https://via.placeholder.com/300x200?text=Headphones' },
    { id: 2, name: 'Smart Watch', price: 89.99, image: 'https://via.placeholder.com/300x200?text=Smart+Watch' },
    { id: 3, name: 'Backpack', price: 39.99, image: 'https://via.placeholder.com/300x200?text=Backpack' },
    { id: 4, name: 'Sneakers', price: 69.99, image: 'https://via.placeholder.com/300x200?text=Sneakers' }
  ];

  const productList = document.getElementById("product-list");
  const cartItems = document.getElementById("cart-items");
  const cartTotal = document.getElementById("cart-total");
  const cart = [];

  function renderProducts() {
    productList.innerHTML = '';
    products.forEach(product => {
      productList.innerHTML += `
        <div class="card">
          <img src="${product.image}" alt="${product.name}" loading="lazy">
          <h4>${product.name}</h4>
          <p>$${product.price.toFixed(2)}</p>
          <button onclick="addToCart(${product.id})">Add to Cart</button>
        </div>`;
    });
  }

  function addToCart(productId) {
    const product = products.find(p => p.id === productId);
    cart.push(product);
    updateCart();
  }

  function updateCart() {
    cartItems.innerHTML = '';
    let total = 0;
    cart.forEach((item, index) => {
      total += item.price;
      cartItems.innerHTML += `
        <li>${item.name} - $${item.price.toFixed(2)} 
        <button onclick="removeItem(${index})" style="margin-left:10px;">❌</button></li>`;
    });
    cartTotal.textContent = total.toFixed(2);
  }

  function removeItem(index) {
    cart.splice(index, 1);
    updateCart();
  }

  renderProducts();
</script>

</body>
</html>
