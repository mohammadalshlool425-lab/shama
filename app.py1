from flask import Flask, render_template, request, jsonify

app = Flask(__name__)

# بيانات أولية تحاكي قاعدة بيانات Firebase (إعلانات حية في إربد وجامعة اليرموك)
SAMPLE_LISTINGS = [
    {
        "id": 1,
        "title": "لابتوب Lenovo IdeaPad 3 - رام 8 جيجا نظيف جداً",
        "category": "إلكترونيات ولابتوبات",
        "price_jod": 165,
        "ai_fair_price": "160 - 180",
        "price_status": "سعر ممتاز",
        "status_color": "green",
        "condition": "مستعمل - بحالة الوكالة (البطارية تدوم 4 ساعات، بدون أي خدوش)",
        "seller_name": "محمد الشلول",
        "seller_badge": "طالب جامعي موثق - اليرموك 🎓",
        "meetup_spot": "جامعة اليرموك - قرب كلية الاقتصاد",
        "image": "https://images.unsplash.com/photo-1588872657578-7efd1f1555ed?auto=format&fit=crop&w=600&q=80"
    },
    {
        "id": 2,
        "title": "مجموعة كتب تخصص الاقتصاد والمصارف الإسلامية + ملخصات شاملة",
        "category": "كتب ومستلزمات جامعية",
        "price_jod": 12,
        "ai_fair_price": "10 - 15",
        "price_status": "سعر عادل",
        "status_color": "blue",
        "condition": "مستعملة نظيفة جداً مع تحديد النقاط المهمة",
        "seller_name": "أحمد العلي",
        "seller_badge": "طالب جامعي موثق - اليرموك 🎓",
        "meetup_spot": "البوابة الشمالية - شارع الجامعة",
        "image": "https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?auto=format&fit=crop&w=600&q=80"
    },
    {
        "id": 3,
        "title": "هاتف Huawei Y7 Prime 2019 مع الشاحن الأصلي",
        "category": "هواتف ذكية",
        "price_jod": 45,
        "ai_fair_price": "40 - 50",
        "price_status": "سعر عادل",
        "status_color": "blue",
        "condition": "يعمل بكفاءة، يوجد خدش بسيط على الإطار الجانبي (موضح للأمانة)",
        "seller_name": "متجر النور للهواتف",
        "seller_badge": "تاجر محلي موثق - إربد ✅",
        "meetup_spot": "وسط البلد - شارع الهاشمي",
        "image": "https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?auto=format&fit=crop&w=600&q=80"
    }
]

@app.route('/')
def home():
    return render_template('index.html', listings=SAMPLE_LISTINGS)

# نقطة اتصال المحرك الذكي (AI Auto-Fill & Fair Pricing)
@app.route('/api/ai-analyze', methods=['POST'])
def ai_analyze():
    data = request.json
    item_Hint = data.get('item_hint', '').strip()
    condition = data.get('condition', 'مستعمل نظيف')
    
    # هنا يتم ربط Gemini API لاحقاً، وهذه محاكاة ذكية فورية للتجربة:
    if "لابتوب" in item_Hint or "حاسوب" in item_Hint:
        result = {
            "title": f"جهاز {item_Hint} عملي للدراسة والبرمجة",
            "category": "إلكترونيات ولابتوبات",
            "suggested_price": 175,
            "fair_range": "165 - 190",
            "description": f"جهاز {item_Hint} بحالة ({condition}). مناسب جداً لطلاب الجامعات والبرمجة. البيع على الفحص الكامل في مكان عام لضمان حق المشتري وخلوه من أي عيوب خفية."
        }
    elif "كتاب" in item_Hint or "كتب" in item_Hint:
        result = {
            "title": f"{item_Hint} - نسخة أصلية مع الملاحظات",
            "category": "كتب ومستلزمات جامعية",
            "suggested_price": 8,
            "fair_range": "6 - 10",
            "description": f"{item_Hint} بحالة ({condition})، جميع الصفحات كاملة وواضحة. التسليم يداً بيد داخل الحرم الجامعي."
        }
    else:
        result = {
            "title": f"{item_Hint} بحالة ممتازة للبيع في إربد",
            "category": "أقسام متنوعة",
            "suggested_price": 35,
            "fair_range": "30 - 45",
            "description": f"سلعة ({item_Hint}) بحالة ({condition}). تم تحديد السعر بناءً على متوسط أسعار السوق المحلي في الأردن مع بيان كافة التفاصيل بشفافية تامة."
        }
    return jsonify(result)

@app.route('/api/add-listing', methods=['POST'])
def add_listing():
    data = request.json
    new_item = {
        "id": len(SAMPLE_LISTINGS) + 1,
        "title": data['title'],
        "category": data['category'],
        "price_jod": int(data['price_jod']),
        "ai_fair_price": data.get('ai_fair_price', 'حسب الفحص'),
        "price_status": "سعر عادل (مفحوص بالـ AI)",
        "status_color": "green",
        "condition": data['condition'],
        "seller_name": data.get('seller_name', 'مستخدم موثق'),
        "seller_badge": "طالب جامعي موثق - اليرموك 🎓",
        "meetup_spot": data['meetup_spot'],
        "image": "https://images.unsplash.com/photo-1526738549149-8e07eca6c147?auto=format&fit=crop&w=600&q=80"
    }
    SAMPLE_LISTINGS.insert(0, new_item)
    return jsonify({"status": "success", "item": new_item})

if __name__ == '__main__':
    app.run(debug=True, port=5000)
