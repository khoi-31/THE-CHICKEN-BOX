<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>冷冻鸡排在线商店</title>
    <style>
        /* Reset styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f9;
            color: #333;
        }

        header {
            background-color: #ff6f61;
            color: white;
            padding: 20px;
            text-align: center;
        }

        header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        header p {
            font-size: 1.2em;
        }

        nav {
            background-color: #333;
            color: white;
            padding: 10px 0;
            text-align: center;
        }

        nav a {
            color: white;
            text-decoration: none;
            margin: 0 15px;
            font-size: 1.1em;
            transition: color 0.3s;
        }

        nav a:hover {
            color: #ff6f61;
        }

        .container {
            padding: 20px;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
        }

        .product-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            flex: 3;
        }

        .product {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            transition: transform 0.3s ease;
        }

        .product:hover {
            transform: translateY(-10px);
        }

        .product img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }

        .product h3 {
            font-size: 1.5em;
            padding: 10px;
            text-align: center;
        }

        .product p {
            text-align: center;
            font-size: 1.1em;
            margin: 10px 0;
        }

        .add-to-cart {
            background-color: #ff6f61;
            color: white;
            border: none;
            padding: 10px 20px;
            width: 100%;
            font-size: 1.1em;
            cursor: pointer;
            transition: background-color 0.3s;
            border-radius: 0 0 10px 10px;
        }

        .add-to-cart:hover {
            background-color: #e25e54;
        }

        #cart {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
            flex: 1;
            margin-left: 20px;
            display: none; /* Hide cart by default */
        }

        #cart h2 {
            font-size: 1.8em;
            margin-bottom: 20px;
        }

        #cart ul {
            list-style: none;
            padding: 0;
            margin-bottom: 20px;
        }

        #cart li {
            font-size: 1.2em;
            margin: 5px 0;
        }

        #cart button {
            background-color: #ff6f61;
            color: white;
            border: none;
            padding: 12px;
            font-size: 1.3em;
            width: 100%;
            cursor: pointer;
            border-radius: 10px;
            transition: background-color 0.3s;
        }

        #cart button:hover {
            background-color: #e25e54;
        }

        footer {
            text-align: center;
            background-color: #333;
            color: white;
            padding: 10px;
            margin-top: 40px;
        }

        footer a {
            color: white;
            text-decoration: none;
        }

        footer a:hover {
            color: #ff6f61;
        }

        /* 购物车泡泡样式 */
        .cart-bubble {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #ff6f61;
            color: white;
            padding: 10px 20px;
            border-radius: 30px;
            font-size: 1.1em;
            cursor: pointer;
            display: none;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
        }

        .cart-bubble:hover {
            transform: scale(1.1);
        }

        .remove-item {
            font-size: 0.8em;
            background-color: #e25e54;
            color: white;
            border: none;
            padding: 5px 10px;
            cursor: pointer;
            border-radius: 5px;
            margin-left: 10px;
        }

        @media (max-width: 768px) {
            .container {
                flex-direction: column;
                align-items: center;
            }

            .product-list {
                grid-template-columns: 1fr 1fr;
            }

            #cart {
                margin-left: 0;
                margin-top: 20px;
            }
        }

        @media (max-width: 480px) {
            .product-list {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>冷冻鸡排在线商店</h1>
        <p>新鲜、美味、安全的冷冻鸡排，送到您家门口！</p>
    </header>
    <nav>
        <a href="#">🏠 首页</a>
        <a href="#products">📦 产品</a>
        <a href="#about">📖 关于我们</a>
        <a href="#contact">📞 联系我们</a>
        <a href="javascript:void(0);" onclick="toggleCart()">🛒 查看购物车</a>
    </nav>
    <div class="container">
        <div class="product-list" id="products"></div>

        <div id="cart">
            <h2>购物车</h2>
            <ul id="cart-items"></ul>
            <p>总计: <span id="total-price">RM0</span></p>
            <button id="checkout-button" onclick="checkout()" disabled>去结账</button>
        </div>
    </div>

    <footer>
        <p>&copy; 2025 冷冻鸡排在线商店. 版权所有. | <a href="#">隐私政策</a></p>
    </footer>

    <!-- 购物车泡泡 -->
    <div id="cart-bubble" class="cart-bubble" onclick="toggleCart()">购物车 (0)</div>

    <script>
        const products = [
            { name: "经典鸡排", price: 10, image: "https://via.placeholder.com/300x200" },
            { name: "辣味鸡排", price: 12, image: "https://via.placeholder.com/300x200" },
            { name: "芝士鸡排", price: 15, image: "https://via.placeholder.com/300x200" }
        ];

        let cartItems = {};

        function loadProducts() {
            const productList = document.querySelector('.product-list');
            products.forEach(product => {
                const productHTML = `
                    <div class="product">
                        <img src="${product.image}" alt="${product.name}">
                        <h3>${product.name}</h3>
                        <p>价格: RM${product.price}/块</p>
                        <button data-name="${product.name}" data-price="${product.price}" class="add-to-cart">加入购物车</button>
                    </div>
                `;
                productList.innerHTML += productHTML;
            });

            document.querySelectorAll('.add-to-cart').forEach(button => {
                button.addEventListener('click', () => {
                    addToCart(button.dataset.name, parseFloat(button.dataset.price));
                });
            });
        }

        function addToCart(productName, price) {
            if (cartItems[productName]) {
                cartItems[productName].quantity++;
                cartItems[productName].totalPrice += price;
            } else {
                cartItems[productName] = { price: price, quantity: 1, totalPrice: price };
            }
            updateCartBubble();
            renderCart();
        }

        function removeFromCart(productName) {
            if (cartItems[productName].quantity > 1) {
                cartItems[productName].quantity--;
                cartItems[productName].totalPrice -= cartItems[productName].price;
            } else {
                delete cartItems[productName];
            }
            updateCartBubble();
            renderCart();
        }

        function updateCartBubble() {
            const cartBubble = document.getElementById('cart-bubble');
            const itemCount = Object.values(cartItems).reduce((sum, item) => sum + item.quantity, 0);
            cartBubble.textContent = `购物车 (${itemCount})`;
            cartBubble.style.display = itemCount > 0 ? 'block' : 'none';

            // Enable/Disable checkout button based on cart status
            const checkoutButton = document.getElementById('checkout-button');
            checkoutButton.disabled = itemCount === 0;
        }

        function renderCart() {
            const cartItemsList = document.getElementById('cart-items');
            const totalPriceElement = document.getElementById('total-price');
            cartItemsList.innerHTML = '';

            let total = 0;
            for (let [name, item] of Object.entries(cartItems)) {
                const li = document.createElement('li');
                li.textContent = `${name} x${item.quantity} - RM${item.totalPrice.toFixed(2)}`;
                const removeButton = document.createElement('button');
                removeButton.textContent = '移除';
                removeButton.classList.add('remove-item');
                removeButton.onclick = () => removeFromCart(name);
                li.appendChild(removeButton);
                cartItemsList.appendChild(li);
                total += item.totalPrice;
            }

            totalPriceElement.textContent = `RM${total.toFixed(2)}`;
        }

        function toggleCart() {
            const cart = document.getElementById('cart');
            cart.style.display = cart.style.display === 'none' ? 'block' : 'none';
        }

        function checkout() {
            if (Object.keys(cartItems).length === 0) {
                alert('购物车为空，请添加商品后再结账');
            } else {
                alert('感谢您的购物！我们将跳转到付款页面。');
                window.location.href = "https://docs.google.com/forms/d/e/1FAIpQLSeN08EIgJNBawzJdWTKIG2zwNHWIqr8lVOxmi3TIXU3tbi_jw/viewform?usp=pp_url";
            }
        }

        window.onload = loadProducts;
    </script>
</body>
</html>
