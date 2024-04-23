#### 二维码生成：
``` html
<script src="https://cdn.bootcdn.net/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<script type="text/javascript">
new QRCode(document.getElementById('qrcode'),
                {
                    text: qrcodeUrl,
                    width: 152,
                    height: 152,
                    colorDark: '#000000',
                    colorLight: '#ffffff',
                    correctLevel: QRCode.CorrectLevel.H
                }
            );
</script>
```
