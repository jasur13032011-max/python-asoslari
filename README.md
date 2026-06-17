# python-asoslari
Python
# Boshlang'ich ro'yxatlar
bajarilmagan_vazifalar = []  # Ichida lug'atlar (dict) saqlanadi
bajarilgan_vazifalar = []

# Muhimlik darajalarini tartiblash uchun yordamchi lug'at
MUHIMLIK_DARAJA = {"high": 1, "medium": 2, "low": 3}

while True:
    print("\n" + "=" * 15 + " VAZIFALAR MЕNЕJЕRI " + "=" * 15)
    print("1. Yangi vazifa qo'shish")
    print("2. Vazifalar ro'yxatini ko'rish (Saralangan)")
    print("3. Vazifani bajarilgan deb belgilash")
    print("4. Vazifani o'chirish")
    print("5. Statistikani ko'rish")
    print("6. Chiqish")
    print("=" * 50)
    
    tanlov = input("Amalni tanlang (1-6): ").strip()
    
    # 1. Vazifa qo'shish
    if tanlov == "1":
        matn = input("Vazifa matnini kiriting: ").strip()
        if not matn:
            print("❌ Vazifa matni bo'sh bo'lishi mumkin emas!")
            continue
            
        muhimlik = input("Muhimlik darajasi (low, medium, high): ").strip().lower()
        if muhimlik not in MUHIMLIK_DARAJA:
            print("⚠️ Noto'g'ri daraja! Standart 'low' deb belgilandi.")
            muhimlik = "low"
            
        yangi_vazifa = {"matn": matn, "muhimlik": muhimlik}
        bajarilmagan_vazifalar.append(yangi_vazifa)
        print(f"✅ Vazifa muvaffaqiyatli qo'shildi!")
        
    # 2. Vazifalarni ko'rish va saralash
    elif tanlov == "2":
        if not bajarilmagan_vazifalar and not bajarilgan_vazifalar:
            print("📭 Vazifalar ro'yxati butunlay bo'sh.")
            continue
            
        # Saralash: high -> medium -> low ketma-ketligida
        # lambda funksiyasi har bir vazifaning muhimlik sonini aniqlab beradi
        bajarilmagan_vazifalar.sort(key=lambda x: MUHIMLIK_DARAJA[x["muhimlik"]])
        
        print("\n📋 BAJARILMAGAN VAZIFALAR:")
        if not bajarilmagan_vazifalar:
            print("   Barcha vazifalar bajarilgan! 🎉")
        else:
            for indeks, vazifa in enumerate(bajarilmagan_vazifalar, 1):
                # Vizual chiroyli ko'rsatish uchun muhimlikka qarab belgi qo'yamiz
                belgi = "🔴" if vazifa["muhimlik"] == "high" else "🟡" if vazifa["muhimlik"] == "medium" else "🟢"
                print(f"  {indeks}. {belgi} [{vazifa['muhimlik'].upper()}] {vazifa['matn']}")
                
        print("\n✅ BAJARILGAN VAZIFALAR:")
        if not bajarilgan_vazifalar:
            print("   Hozircha bajarilgan vazifalar yo'q.")
        else:
            for indeks, vazifa in enumerate(bajarilgan_vazifalar, 1):
                print(f"  [✓] {vazifa['matn']}")
                
    # 3. Bajarilganini belgilash
    elif tanlov == "3":
        if not bajarilmagan_vazifalar:
            print("⚠️ Bajarilmagan vazifalar mavjud emas.")
            continue
            
        # Avval ro'yxatni ko'rsatamiz
        for indeks, vazifa in enumerate(bajarilmagan_vazifalar, 1):
            print(f"  {indeks}. {vazifa['matn']}")
            
        raqam_input = input("Bajarilgan vazifa raqamini kiriting: ").strip()
        if raqam_input.isdigit():
            raqam = int(raqam_input)
            if 1 <= raqam <= len(bajarilmagan_vazifalar):
                # Vazifani bajarilmaganlar ro'yxatidan sug'urib olib, bajarilganlarga qo'shamiz
                bajarilgan = bajarilmagan_vazifalar.pop(raqam - 1)
                bajarilgan_vazifalar.append(bajarilgan)
                print("🎉 Barakalla! Vazifa bajarilganlar ro'yxatiga ko'chirildi.")
            else:
                print("❌ Bunday raqamdagi vazifa yo'q!")
        else:
            print("❌ Iltimos, faqat son kiriting!")
            
    # 4. O'chirish
    elif tanlov == "4":
        if not bajarilmagan_vazifalar:
            print("⚠️ O'chirish uchun vazifa yo'q.")
            continue
            
        for indeks, vazifa in enumerate(bajarilmagan_vazifalar, 1):
            print(f"  {indeks}. {vazifa['matn']}")
            
        raqam_input = input("O'chirmoqchi bo'lgan vazifa raqamini kiriting: ").strip()
        if raqam_input.isdigit():
            raqam = int(raqam_input)
            if 1 <= raqam <= len(bajarilmagan_vazifalar):
                ochirilgan = bajarilmagan_vazifalar.pop(raqam - 1)
                print(f"🗑 '{ochirilgan['matn']}' o'chirib tashlandi.")
            else:
                print("❌ Bunday raqamdagi vazifa yo'q!")
        else:
            print("❌ Iltimos, faqat son kiriting!")
            
    # 5. Statistika
    elif tanlov == "5":
        qolgan_soni = len(bajarilmagan_vazifalar)
        bajarilgan_soni = len(bajarilgan_vazifalar)
        jami_soni = qolgan_soni + bajarilgan_soni
        
        # Bajarish foizini xavfsiz hisoblash (0 ga bo'linish xavfisiz)
        foiz = (bajarilgan_soni / jami_soni) * 100 if jami_soni > 0 else 0
        
        print("\n" + "-"*15 + " STATISTIKA " + "-"*15)
        print(f"📊 Jami vazifalar:       {jami_soni} ta")
        print(f"✅ Bajarilganlar:       {bajarilgan_soni} ta")
        print(f"⏳ Qolgan vazifalar:    {qolgan_soni} ta")
        print(f"📈 Bajarish unumdorligi: {foiz:.1f}%")
        print("-" * 42)
        
    # 6. Chiqish
    elif tanlov == "6":
        print("👋 Dastur tugatildi. Kuningiz xayrli o'tsin!")
        break
    else:
        print("❌ Noto'g'ri buyruq! Iltimos, 1 dan 6 gacha bo'lgan son kiriting.")
💡 Kod arxitekturasi va funksionalligi:
Lug'atlar ro'yxati (List of Dicts): Har bir vazifa bitta matndan iborat bo'lmay, o'zida ham matnni, ham unga tegishli muhimlik holatini ({"matn": ..., "muhimlik": ...}) jamlaydi.

Saralash algoritmi (sort + lambda): bajarilmagan_vazifalar.sort(key=lambda x: MUHIMLIK_DARAJA[x["muhimlik"]]) qatori vazifalarni alifbo bo'yicha emas, aynan biz belgilagan tartibda (avval high, keyin medium, keyin low) chiroyli tartiblab beradi.

Ma'lumotlar migratsiyasi: pop() metodi orqali bajarilgan vazifa bir listdan o'chib, parallel ravishda ikkinchisiga ko'chadi, bu esa xotirani toza saqlashga xizmat qiladi.
