[U
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Order System with Invoice</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 0; background-color: #f8f8f8; }
        header { background-color: #007bff; color: white; padding: 10px; text-align: center; }
        .container { padding: 20px; }
        .category button { width: 100%; padding: 10px; margin: 5px 0; border: none; border-radius: 5px; background-color: #007bff; color: white; font-size: 16px; cursor: pointer; }
        .popup { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.7); justify-content: center; align-items: center; }
        .popup-content { background: white; padding: 20px; border-radius: 5px; width: 90%; max-width: 500px; position: relative; }
        .popup-content h2 { margin: 0 0 10px 0; }
        .menu-item { border: 1px solid #ddd; padding: 10px; border-radius: 5px; background: white; display: flex; justify-content: space-between; align-items: center; margin: 10px 0; }
        .menu-item img { width: 100px; height: 100px; object-fit: cover; border-radius: 5px; }
        .order-form, .cart-summary, #invoice { background: white; padding: 15px; margin-top: 20px; border: 1px solid #ddd; border-radius: 5px; }
        #invoice { display: none; }
    </style>
</head>
<body>
    <header><h1>Order Your Meal</h1></header>
    <div class="container">
        <div class="category"><button onclick="showPopup('main-dishes')">Món Chính</button></div>
        <div class="category"><button onclick="showPopup('soups')">Món Nước</button></div>
        <div class="category"><button onclick="showPopup('drinks')">Nước Ngọt</button></div>
        <div class="category"><button onclick="showPopup('must-try')">Món Mới</button></div>
        <div class="category"><button onclick="showPopup('others')">Món Khác</button></div>

        <!-- Popups for Categories -->
        <div class="popup" id="main-dishes">
            <div class="popup-content">
                <button class="close-popup" onclick="hidePopup('main-dishes')">&times;</button>
                <h2>Món Chính</h2>
                <div class="menu-item">
                    <img src="https://via.placeholder.com/100" alt="Dish A">
                    <div>
                        <h3>Dish A</h3>
                        <p>Price: 50,000 VND</p>
                        <input type="number" id="qty-dish-a" value="0" min="0">
                        <button onclick="addToCart('Dish A', 50000, 'qty-dish-a')">Add</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Order Form -->
        <div class="order-form">
            <h2>Place Your Order</h2>
            <label>Name: <input type="text" id="name"></label>
            <label>Phone: <input type="text" id="phone"></label>
            <label>Pick-up Time: <input type="time" id="time"></label>
            <button onclick="submitOrder()">Submit</button>
        </div>

        <!-- Cart Summary -->
        <div class="cart-summary">
            <h2>Cart</h2>
            <div id="cart-items"></div>
            <p>Total: <span id="total-amount">0</span> VND</p>
        </div>

        <!-- Invoice -->
        <div id="invoice">
            <h2>Invoice</h2>
            <p>Name: <span id="invoice-name"></span></p>
            <p>Phone: <span id="invoice-phone"></span></p>
            <p>Time: <span id="invoice-time"></span></p>
            <div id="invoice-items"></div>
            <p>Total: <span id="invoice-total"></span> VND</p>
            <button onclick="printInvoice()">Print</button>
        </div>
    </div>

    <script>
        let cart = [];

        function addToCart(name, price, qtyId) {
            const quantity = parseInt(document.getElementById(qtyId).value);
            if (quantity <= 0) return alert("Invalid quantity");
            const existing = cart.find(item => item.name === name);
            if (existing) existing.quantity += quantity;
            else cart.push({ name, price, quantity });
            updateCart();
        }

        function updateCart() {
            const cartItems = document.getElementById("cart-items");
            const totalAmount = document.getElementById("total-amount");
            cartItems.innerHTML = "";
            let total = 0;
            cart.forEach(item => {
                cartItems.innerHTML += `<p>${item.name} - ${item.quantity} x ${item.price}</p>`;
                total += item.price * item.quantity;
            });
            totalAmount.textContent = total;
        }

        function submitOrder() {
            const name = document.getElementById("name").value;
            const phone = document.getElementById("phone").value;
            const time = document.getElementById("time").value;
            if (!name || !phone || !time || cart.length === 0) return alert("Complete all fields and cart");
            document.getElementById("invoice-name").textContent = name;
            document.getElementById("invoice-phone").textContent = phone;
            document.getElementById("invoice-time").textContent = time;
            const invoiceItems = document.getElementById("invoice-items");
            const invoiceTotal = document.getElementById("invoice-total");
            invoiceItems.innerHTML = "";
            let total = 0;
            cart.forEach(item => {
                invoiceItems.innerHTML += `<p>${item.name} - ${item.quantity} x ${item.price}</p>`;
                total += item.price * item.quantity;
            });
            invoiceTotal.textContent = total;
            document.getElementById("invoice").style.display = "block";
            cart = [];
            updateCart();
        }

        function printInvoice() {
            window.print();
        }

        function showPopup(id) {
            document.getElementById(id).style.display = "flex";
        }

        function hidePopup(id) {
            document.getElementById(id).style.display = "none";
        }
    </script>
</body>
</html>
ploading index (1).html…]()
