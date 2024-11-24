import requests
import time

# رابط لموقع Faucet (يجب أن يدعم API)
faucet_url = "https://api.example-faucet.com/get-reward"

# بيانات المستخدم (مثال)
user_data = {
    "wallet_address": "YOUR_WALLET_ADDRESS",
    "captcha_token": "YOUR_CAPTCHA_TOKEN"  # قد تحتاج إلى حل الكابتشا يدويًا في بعض الأحيان
}

def collect_reward():
    try:
        # إرسال الطلب إلى الموقع
        response = requests.post(faucet_url, data=user_data)
        
        if response.status_code == 200:
            data = response.json()
            if data["success"]:
                print(f"تم استلام المكافأة: {data['reward']} ساتوشي")
            else:
                print(f"خطأ: {data['message']}")
        else:
            print("فشل في الاتصال بالموقع")
    except Exception as e:
        print(f"حدث خطأ: {e}")

# تشغيل الوظيفة بشكل دوري
while True:
    collect_reward()
    # الانتظار لفترة معينة (حسب شروط الموقع)
    time.sleep(3600)  # مرة كل ساعة
