# python-asoslari
Mana, ma'lumotlar strukturasi (ichma-ich lug'atlar, to'plamlar) va mukammal qidiruv/filtr tizimiga ega bo'lgan Kontaktlar kitobi (Telefon ma'lumotnomasi) dasturi:

Python
# Boshlang'ich kontaktlar ma'lumotlar bazasi
# Struktura: {ism: {tel: str, manzil: str, email: str}}
kontaktlar = {
    "Ali Valiyev": {"tel": "+998901234567", "manzil": "Toshkent", "email": "ali@mail.com"},
    "Zuhra Karimova": {"tel": "+998939876543", "manzil": "Samarqand", "email": "zuhra@gmail.com"},
    "Olim Nabiyev": {"tel": "+998914445566", "manzil": "Toshkent", "email": "olim@it.uz"},
    "Asal Shokirova": {"tel": "+998997778899", "manzil": "Farg'ona", "email": "asal@design.com"}
}

def tel_va_ism_validatsiya(ism: str, tel: str) -> bool:
    """Ism bo'sh emasligi va telefon raqami to'g'ri formatdaligini tekshiradi."""
    if not ism.strip():
        print("❌ Xatolik: Ism bo'sh bo'lishi mumkin emas!")
        return False
    # Telefon raqami kamida 9 ta raqam bo'lishi va + belgisi bilan boshlanishi mumkin
    tozalangan_tel = tel.replace("+", "").strip()
    if not tozalangan_tel.isdigit() or len(tozalangan_tel) < 9:
        print("❌ Xatolik: Telefon raqami formati noto'g'ri! (Faqat raqamlar yoki + belgisi)")
        return False
    return True

while True:
    print("\n" + "=" * 15 + " KONTAKTLAR DASTURI " + "=" * 15)
    print("1. Yangi kontakt qo'shish")
    print("2. Kontakt qidirish (Ism yoki Tel bo'yicha)")
    print("3. Kontaktni o'chirish")
    print("4. Barcha kontaktlarni ko'rish (Alifbo tartibida)")
    print("5. Shaharlar bo'yicha filtrlash (Dict Comprehension)")
    print("6. Tizim statistikasi (Set va Tahlil)")
    print("7. Chiqish")
    print("=" * 50)
    
    tanlov = input("Amalni tanlang (1-7): ").strip()
    
    # 1. Yangi kontakt qo'shish
    if tanlov == "1":
        ism = input("Kontakt ismini kiriting: ").strip()
        tel = input("Telefon raqamini kiriting (Masalan: +998901234567): ").strip()
        manzil = input("Yashash shahrini kiriting: ").strip().capitalize()
        email = input("Email manzilini kiriting: ").strip()
        
        if tel_va_ism_validatsiya(ism, tel):
            if ism in kontaktlar:
                print(f"⚠️ {ism} ismli kontakt allaqachon mavjud! Ma'lumotlar yangilandi.")
            
            # Ichma-ich dict yaratish qismi
            kontaktlar[ism] = {
                "tel": tel,
                "manzil": manzil if manzil else "Noma'lum",
                "email": email if email else "Noma'lum"
            }
            print(f"✅ {ism} muvaffaqiyatli saqlandi.")
            
    # 2. Qidirish (Ism yoki Tel bo'yicha)
    elif tanlov == "2":
        kalit = input("Qidirilayotgan ism yoki telefon raqamini kiriting: ").strip().lower()
        topildi = False
        
        for ism, info in kontaktlar.items():
            # Ism yoki telefon mos kelsa (qisman qidiruv ham ishlaydi)
            if kalit in ism.lower() or kalit in info["tel"]:
                print(f"\n👤 {ism}:")
                print(f"  📞 Tel:    {info['tel']}")
                print(f"  📍 Manzil: {info['manzil']}")
                print(f"  📧 Email:  {info['email']}")
                topildi = True
                
        if not topildi:
            print("🔍 Afsuski, hech qanday kontakt topilmadi.")
            
    # 3. O'chirish
    elif tanlov == "3":
        ism = input("O'chirmoqchi bo'lgan kontakt ismini kiriting: ").strip()
        if ism in kontaktlar:
            # Lug'atdan kalit so'z bo'yicha butunlay o'chirish
            del kontaktlar[ism]
            print(f"🗑️ '{ism}' kontaktlar ro'yxatidan o'chirildi.")
        else:
            print("❌ Bunday ismli kontakt topilmadi.")
            
    # 4. Hammasini ko'rsatish (Alifbo tartibida)
    elif tanlov == "4":
        if not kontaktlar:
            print("📭 Kontaktlar kitobi bo'sh.")
            continue
            
        print("\n🗂️ BARCHA KONTAKTLAR (ALIFBO TARTIBIDA):")
        # Kalitlar bo'yicha saralangan ro'yxat olish
        for ism in sorted(kontaktlar.keys()):
            info = kontaktlar[ism]
            print(f" ▫️ {ism} -> 📞 {info['tel']} | 📍 {info['manzil']}")
            
    # 5. Dict Comprehension bilan filtrlash
    elif tanlov == "5":
        shahar = input("Qaysi shahardagi kontaktlarni filtrlamoqchisiz?: ").strip().capitalize()
        
        # Dict comprehension yordamida yangi lug'at hosil qilish
        filtr_kontaktlar = {k: v for k, v in kontaktlar.items() if v["manzil"] == shahar}
        
        print(f"\n📍 {shahar} shahridagi kontaktlar:")
        if not filtr_kontaktlar:
            print("   Bu shahardan hech kim topilmadi.")
        else:
            for ism, info in filtr_kontaktlar.items():
                print(f"  👤 {ism} | 📞 {info['tel']}")
                
    # 6. Statistika va Set (Unique shaharlar)
    elif tanlov == "6":
        if not kontaktlar:
            print("⚠️ Statistika uchun ma'lumot yetarli emas.")
            continue
            
        jami_kontakt = len(kontaktlar)
        
        # Set comprehension yordamida faqat unikal shaharlarni ajratib olish
        unikal_shaharlar = {info["manzil"] for info in kontaktlar.values()}
        
        # Eng uzun ismni topish
        eng_uzun_ism = max(kontaktlar.keys(), key=len)
        
        print("\n" + "-"*15 + " TIZIM STATISTIKASI " + "-"*15)
        print(f"📊 Jami kontaktlar soni:  {jami_kontakt} ta")
        print(f"🔤 Eng uzun kontakt ismi: {eng_uzun_ism} ({len(eng_uzun_ism)} ta belgi)")
        print(f"🗺️ Unikal shaharlar ({len(unikal_shaharlar)} ta): {', '.join(unikal_shaharlar)}")
        print("-" * 50)
        
    # 7. Chiqish
    elif tanlov == "7":
        print("👋 Dastur tugatildi. Kontaktlar xavfsiz saqlandi!")
        break
    else:
        print("❌ Noto'g'ri buyruq! 1 dan 7 gacha bo'lgan raqam kiriting.")
💡 Kodning kuchli tomonlari:
Murakkab ma'lumotlar arxitekturasi: Har bir insonning ismi asosiy kalit (key), uning ichidagi ma'lumotlar esa ikkinchi kichik lug'at (sub-dictionary) hisoblanadi.

Dict va Set Comprehension:

{k: v for k, v in kontaktlar.items() if ...} kodi bitta qatorda butun boshli lug'atni filtrlaydi.

{info["manzil"] for info in kontaktlar.values()} to'plam (set) yaratadi, to'plamlar esa o'z ichida bir xil elementlarni takrorlamaydi va unikal ro'yxat hosil qilib beradi.

Professional Validatsiya: Ism bo'sh qolishi yoki telefon o'rniga harf kiritilishining oldi mustahkam olingan.
