<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QR Code Generator</title>
    <script src="https://cdn.jsdelivr.net/npm/qrcodejs/qrcode.min.js"></script>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin: 50px; }
        input { padding: 10px; width: 80%; margin-bottom: 20px; }
        #qrcode { margin-top: 20px; }
    </style>
</head>
<body>

    <h1>QR Code Generator</h1>
    <input type="text" id="linkInput" placeholder="Nhập link của bạn..." oninput="generateQRCode()">
    <div id="qrcode"></div>

    <script>
        function generateQRCode() {
            let link = document.getElementById("linkInput").value;
            document.getElementById("qrcode").innerHTML = "";
            if (link) {
                new QRCode(document.getElementById("qrcode"), {
                    text: link,
                    width: 200,
                    height: 200
                });
            }
        }
    </script>

</body>
</html>
