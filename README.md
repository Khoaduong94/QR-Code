<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QR Code Generator Nâng Cao</title>
    <script src="https://cdn.jsdelivr.net/npm/qrcodejs/qrcode.min.js"></script>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin: 30px; background-color: #f4f4f4; }
        .container { background-color: #fff; padding: 30px; border-radius: 8px; box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); margin: 20px auto; max-width: 600px; }
        h1 { color: #333; margin-bottom: 20px; }
        .input-group { margin-bottom: 20px; }
        label { display: block; margin-bottom: 5px; color: #555; }
        input[type="text"], input[type="color"] { padding: 10px; width: calc(100% - 22px); margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box; }
        .controls { display: flex; gap: 10px; margin-bottom: 20px; justify-content: center; }
        button { padding: 10px 20px; border: none; border-radius: 4px; cursor: pointer; font-weight: bold; color: #fff; background-color: #007bff; transition: background-color 0.3s ease; }
        button:hover { background-color: #0056b3; }
        #qrcode-container { margin-top: 20px; border: 1px solid #eee; padding: 15px; border-radius: 4px; display: inline-block; }
        #qrcode { display: inline-block; }
        #downloadBtn { display: none; background-color: #28a745; }
        #downloadBtn:hover { background-color: #1e7e34; }
        .error-message { color: red; margin-top: 10px; }
    </style>
</head>
<body>
    <div class="container">
        <h1> Tạo Mã QR Code</h1>

        <div class="input-group">
            <label for="linkInput">Nhập Liên Kết:</label>
            <input type="text" id="linkInput" placeholder="Ví dụ: https://www.example.com" oninput="generateQRCode()">
            <p id="linkError" class="error-message"></p>
        </div>

        <div class="controls">
            <div>
                <label for="colorLight">Màu Nền:</label>
                <input type="color" id="colorLight" value="#ffffff" oninput="generateQRCode()">
            </div>
            <div>
                <label for="colorDark">Màu Mã QR:</label>
                <input type="color" id="colorDark" value="#000000" oninput="generateQRCode()">
            </div>
        </div>

        <div id="qrcode-container" style="display: none;">
            <div id="qrcode"></div>
        </div>

        <button id="downloadBtn" onclick="downloadQRCode()" style="display: none;">Tải Xuống Mã QR</button>
    </div>

    <script>
        let qrcode;
        const qrcodeContainer = document.getElementById("qrcode-container");
        const downloadBtn = document.getElementById("downloadBtn");
        const linkError = document.getElementById("linkError");
        const qrcodeDiv = document.getElementById("qrcode");

        function isValidURL(str) {
            try {
                new URL(str);
                return true;
            } catch (_) {
                return false;
            }
        }

        function generateQRCode() {
            let link = document.getElementById("linkInput").value;
            let colorLight = document.getElementById("colorLight").value;
            let colorDark = document.getElementById("colorDark").value;

            linkError.textContent = "";
            qrcodeContainer.style.display = "none";
            downloadBtn.style.display = "none";
            qrcodeDiv.innerHTML = "";

            if (!link) {
                return;
            }

            // Optional: Basic URL validation
            // if (!isValidURL(link)) {
            //     linkError.textContent = "Vui lòng nhập một liên kết hợp lệ.";
            //     return;
            // }

            qrcode = new QRCode(qrcodeDiv, {
                text: link,
                width: 200,
                height: 200,
                colorDark: colorDark,
                colorLight: colorLight,
                correctLevel: QRCode.CorrectLevel.H
            });

            setTimeout(() => {
                const canvas = qrcodeDiv.querySelector('canvas');
                if (canvas) {
                    qrcodeContainer.style.display = "inline-block";
                    downloadBtn.style.display = "block";
                } else {
                    qrcodeContainer.style.display = "none";
                    downloadBtn.style.display = "none";
                }
            }, 200);
        }

        function downloadQRCode() {
            const canvas = qrcodeDiv.querySelector('canvas');
            if (canvas) {
                const link = document.createElement('a');
                link.href = canvas.toDataURL("image/png");
                link.download = 'qrcode.png';
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            } else {
                alert("Chưa có mã QR nào để tải xuống.");
            }
        }

        if (document.getElementById("linkInput").value) {
            generateQRCode();
        }
    </script>
</body>
</html>
