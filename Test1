<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>MemeBuzz MVX Test</title>
    <script src="https://unpkg.com/@multiversx/sdk-core@12.18.0/out/index.js"></script>
    <script src="https://unpkg.com/@multiversx/sdk-wallet@3.0.0/out/wallet.js"></script>
    <style>
        body { font-family: Arial; width: 300px; padding: 10px; border: 1px solid #000; background: #fff; }
        button { width: 100%; margin: 5px 0; font-size: 16px; }
        #status { font-size: 12px; }
    </style>
</head>
<body>
    <h1 style="font-size: 18px;">MemeBuzz MVX Test</h1>
    <button onclick="connectXPortal()">EGLD (xPortal)</button>
    <button onclick="subscribe()">Subscribe ($2)</button>
    <div id="status">Loading...</div>

    <script>
        let account, provider;
        function log(message) {
            console.log(message);
            document.getElementById('status').innerText = message;
        }

        async function connectXPortal() {
            log("Connecting xPortal...");
            const xPortal = window.Maiar || window.xPortal;
            if (xPortal) {
                provider = new window.Maiar.WalletConnectProvider();
                try {
                    await provider.init();
                    await provider.login();
                    account = await provider.getAddress();
                    log(`Connected: ${account.slice(0, 8)}...`);
                } catch (err) {
                    log("Connect failed: " + err.message);
                    alert("Connect failed: " + err.message);
                }
            } else {
                log("xPortal not found!");
                alert("Install xPortal: chrome.google.com/webstore");
                window.open("https://chrome.google.com/webstore/detail/xportal/kmdnhlobepocfnhipclmgbhngbjafbed", "_blank");
            }
        }

        async function subscribe() {
            if (!account || !provider) {
                log("Connect xPortal first!");
                return alert("Connect xPortal first!");
            }
            log("Subscribing...");
            try {
                const tx = {
                    nonce: 0,
                    value: "70000000000000000", // 0.07 EGLD
                    receiver: "erd1f48rayfnkqn48yjkm2macdgl7gpveq2359jayuez6fm2rc2ppekqwx9r4z",
                    sender: account,
                    gasPrice: 1000000000,
                    gasLimit: 50000,
                    chainID: "T"
                };
                const serialized = new multiversxSdk.Transaction(tx).serializeForSigning();
                const signature = await provider.signTransaction(serialized);
                log("Tx signed!");
                alert("Signed 0.07 EGLD tx—broadcast TBD.");
            } catch (err) {
                log("Subscribe failed: " + err.message);
                alert("Subscribe failed: " + err.message);
            }
        }

        log("Script loaded!");
        console.log("Initial xPortal check:", window.Maiar || window.xPortal);
    </script>
</body>
</html>
