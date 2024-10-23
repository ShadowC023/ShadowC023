<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Buy Advertising Space with BTCB</title>
    <script src="https://cdn.jsdelivr.net/gh/ethereum/web3.js/dist/web3.min.js"></script>
</head>
<body>
    <h1>Buy Advertising Space</h1>
    <p>Price: 0.25 BTCB</p>
    <button id="payButton">Pay with BTCB</button>

    <script>
        // Your receiving wallet address on Base Mainnet
        const receivingWalletAddress = "0x5879C2450bad890ab19404CbD5436928795d08c4";  // Replace with your receiving wallet address

        // BTCB Contract Address on Base Mainnet
        const BTCBContractAddress = "0x0c41f1fc9022feb69af6dc666abfe73c9ffda7ce";
        
        const priceInBTCB = "250000000000000000"; // 0.25 BTCB in Wei (1 BTCB = 1e18 Wei)

        window.onload = async function() {
            // Check if MetaMask or another wallet is installed
            if (typeof window.ethereum !== 'undefined') {
                console.log('MetaMask is installed!');
                
                // Request connection to the wallet (MetaMask or other Web3 providers)
                await window.ethereum.request({ method: 'eth_requestAccounts' });
                const web3 = new Web3(window.ethereum);

                // Get the user's account (wallet address)
                const accounts = await web3.eth.getAccounts();
                const userAccount = accounts[0];

                document.getElementById('payButton').onclick = async function() {
                    try {
                        // Set up the transaction parameters
                        const transactionParameters = {
                            to: receivingWalletAddress,  // Your wallet that receives the payment
                            from: userAccount,  // Sender's wallet address
                            value: priceInBTCB,  // Amount in Wei (0.001 BTCB)
                            chainId: '8453'  // Base Mainnet Chain ID (8453 for Base Mainnet)
                        };

                        // Trigger the transaction via MetaMask or Web3 provider
                        await web3.eth.sendTransaction(transactionParameters)
                            .on('transactionHash', function(hash) {
                                console.log('Transaction Hash:', hash);
                                alert('Payment Sent! Transaction Hash: ' + hash);
                                // You can unlock the ad space here or notify your server of successful payment
                            });
                    } catch (error) {
                        console.error(error);
                        alert('Payment failed');
                    }
                };
            } else {
                alert('Please install MetaMask or another wallet to continue.');
            }
        };
    </script>
</body>
</html>
