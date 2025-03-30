#<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sweet Delight Bakery</title>
    <script src="https://checkout.razorpay.com/v1/checkout.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f8e8d9;
            margin: 0;
            padding: 0;
        }
        header {
            background-color: #d2691e;
            color: white;
            padding: 20px;
            font-size: 24px;
        }
        .menu {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 20px;
        }
        .menu-item {
            background: white;
            margin: 15px;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            width: 200px;
        }
        .order-form {
            margin-top: 20px;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            width: 50%;
            margin-left: auto;
            margin-right: auto;
        }
        footer {
            margin-top: 20px;
            padding: 10px;
            background-color: #d2691e;
            color: white;
        }
    </style>
</head>
<body>
    <header>
        Welcome to Sweet Delight Bakery
    </header>
    
    <h2>Our Specialties</h2>
    <div class="menu">
        <div class="menu-item">
            <h3>Chocolate Cupcake</h3>
            <p>$3.00</p>
        </div>
        <div class="menu-item">
            <h3>Strawberry Cake</h3>
            <p>$5.00</p>
        </div>
        <div class="menu-item">
            <h3>Blueberry Muffin</h3>
            <p>$2.50</p>
        </div>
    </div>
    
    <h2>Place Your Order</h2>
    <form class="order-form" onsubmit="return makePayment(event)">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required><br><br>
        
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required><br><br>
        
        <label for="item">Select Item:</label>
        <select id="item" name="item">
            <option value="3">Chocolate Cupcake - $3.00</option>
            <option value="5">Strawberry Cake - $5.00</option>
            <option value="2.5">Blueberry Muffin - $2.50</option>
        </select><br><br>
        
        <label for="quantity">Quantity:</label>
        <input type="number" id="quantity" name="quantity" min="1" required><br><br>
        
        <button type="submit">Pay with Razorpay</button>
    </form>
    
    <script>
        function makePayment(event) {
            event.preventDefault();
            
            let name = document.getElementById("name").value;
            let email = document.getElementById("email").value;
            let itemPrice = parseFloat(document.getElementById("item").value);
            let quantity = parseInt(document.getElementById("quantity").value);
            let amount = itemPrice * quantity * 100; // Convert to paise (Razorpay uses INR in paise)
            
            var options = {
                "key": "YOUR_RAZORPAY_KEY_HERE", // Replace with your Razorpay key
                "amount": amount,
                "currency": "INR",
                "name": "Sweet Delight Bakery",
                "description": "Order Payment",
                "prefill": {
                    "name": name,
                    "email": email
                },
                "theme": {
                    "color": "#d2691e"
                }
            };
            
            var rzp = new Razorpay(options);
            rzp.open();
        }
    </script>
    
    <footer>
        Contact us: sweetdelight@example.com | 123-456-7890
    </footer>
</body>
</html>

