# crypto-api
//A simple web application that allows users to check live cryptocurrency prices using the CoinGecko API. Enter the cryptocurrency symbol, and get real-time price updates in USD. Built with HTML, CSS, and JavaScript.

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cryptocurrency Checker</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color:black;
        }

        .crypto-container {
            text-align: center;
            padding: 30px;
            background-color: green;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
            width: 350px;
        }

        h1 {
            font-size: 24px;
            color: #333;
        }

        #crypto-info {
            margin-top: 20px;
            font-size: 16px;
        }

        input, button {
            padding: 10px;
            font-size: 16px;
            border-radius: 5px;
            border: 1px solid #ccc;
            margin-top: 10px;
        }

        button {
            background-color: gray;
            color: white;
            border: none;
            cursor: pointer;
        }

        button:hover {
            background-color: #5a9bd3;
        }

        input {
            width: 80%;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="crypto-container">
        <h1>Check Cryptocurrency Price</h1>
        <form id="crypto-form">
            <input type="text" id="crypto-input" placeholder="Enter cryptocurrency symbol (e.g., bitcoin)" required />
            <button type="submit">Get Price</button>
        </form>
        <div id="crypto-info">
           
        </div>
    </div>z

    <script>
       
        document.getElementById('crypto-form').addEventListener('submit', function(event) {
            event.preventDefault();
            const cryptoSymbol = document.getElementById('crypto-input').value.toLowerCase().trim(); 
            fetchCryptoData(cryptoSymbol); 
        });

    
        function fetchCryptoData(cryptoSymbol) {
            const apiUrl = `https://api.coingecko.com/api/v3/simple/price?ids=${cryptoSymbol}&vs_currencies=usd`
            fetch(apiUrl)
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Cryptocurrency not found or API error');
                    }
                    return response.json(); 
                })
                .then(data => {
                  
                    console.log(data);

               
                    if (data[cryptoSymbol]) {
                        displayCryptoInfo(data, cryptoSymbol);
                    } else {
                        throw new Error('Cryptocurrency not found');
                    }
                })
                .catch(error => {
                    
                    document.getElementById('crypto-info').innerHTML = `<p>Error: ${error.message}</p>`;
                });
        }

       
        function displayCryptoInfo(data, cryptoSymbol) {
            const cryptoDetails = `
                <h2>${cryptoSymbol.toUpperCase()}</h2>
                <p><strong>Price:</strong> $${data[cryptoSymbol].usd}</p>
                <p><strong>Currency:</strong> USD</p>
            `;
            
  
            document.getElementById('crypto-info').innerHTML = cryptoDetails;
        }
    </script>
</body>
</html>
