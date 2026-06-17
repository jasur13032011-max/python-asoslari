# python-asoslari
Mana, barcha talablarga toʻliq javob beradigan, modulli va xatoliklar boshqarilgan Python dasturi. Bu dasturda har bir amal alohida funksiyaga ajratilgan va sozlik.json fayli bilan ishlaydi.

Python Dastur Kodi
Python
import json
import os

FAYL_NOMI = "sozlik.json"

# Boshlang'ich 20 ta so'z (agar fayl mavjud bo'lmasa ishlatiladi)
BOSHLANGICH_SOZLAR = {
    "apple": "olma", "banana": "banan", "cherry": "gilos", "date": "xurmo",
    "elderberry": "marjon meva", "fig": "anjir", "grape": "uzum", "honeydew": "qovun",
    "ice cream": "muzqaymoq", "juice": "sharbat", "kiwi": "kivi", "lemon": "limon",
    "mango": "mango", "nectarine": "nektarin", "orange": "apelsin", "papaya": "papaya",
    "quince": "behi", "raspberry": "morush", "strawberry": "qulupnay", "tangerine": "mandarin"
}

def yuklash():
    """Fayldan lug'at ma'lumotlarini yuklash funksiyasi"""
    try:
        if os.path.exists(FAYL_NOMI):
            with open(FAYL_NOMI, "r", encoding="utf-8") as fayl:
                return json.load(fayl)
        else:
            # Fayl bo'lmasa, boshlang'ich 20 ta so'z bilan yangi lug'at yaratiladi
            saqlash(BOSHLANGICH_SOZLAR)
            return BOSHLANGICH_SOZLAR
    except (json.JSONDecodeError, IOError) as e:
        print(f"⚠️ Faylni yuklashda xatolik yuz berdi: {e}")
        return {}

def saqlash(lugat):
    """Lug'at ma'lumotlarini faylga saqlash funksiyasi"""
    try:
        with open(FAYL_NOMI, "w", encoding="utf-8") as fayl:
            json.dump(lugat, fayl, ensure_ascii=False, indent=4)
    except IOError as e:
        print(f"⚠️ Ma'lumotlarni saqlashda xatolik yuz berdi: {e}")

def qoshish(lugat):
    """Yangi so'z qo'shish funksiyasi"""
    inglizcha = input("Inglizcha so'zni kiriting: ").strip().lower()
    if not inglizcha:
        print("❌ So'z bo'sh bo'lishi mumkin emas!")
        return
    
    if inglizcha in lugat:
        print(f"⚠️ '{inglizcha}' so'zi lug'atda allaqachon bor ({lugat[inglizcha]}).")
        yangilash = input("Uni yangilashni xohlaysizmi? (ha/yo'q): ").strip().lower()
        if yangilash != 'ha':
            return

    ozbekcha = input("O'zbekcha tarjimasini kiriting: ").strip().lower()
    if ozbekcha:
        lugat[inglizcha] = ozbekcha
        saqlash(lugat)
        print("✅ So'z muvaffaqiyatli saqlandi!")
    else:
        print("❌ Tarjima bo'sh bo'lishi mumkin emas!")

def qidirish(lugat):
    """Kalit (inglizcha) yoki qiymat (o'zbekcha) bo'yicha qidirish funksiyasi"""
    soz = input("Qidirilayotgan so'zni kiriting (inglizcha yoki o'zbekcha): ").strip().lower()
    topildi = False

    # Kalit bo'yicha qidirish (Inglizcha)
    if soz in lugat:
        print(f"🔍 Topildi (Inglizcha): {soz} -> {lugat[soz]}")
        topildi = True

    # Qiymat bo'yicha qidirish (O'zbekcha)
    for kalit, qiymat in lugat.items():
        if qiymat == soz:
            print(f"🔍 Topildi (O'zbekcha): {qiymat} -> {kalit}")
            topildi = True

    if not topildi:
        print("❌ Afsuski, bunday so'z lug'atdan topilmadi.")

def ochirish(lugat):
    """Lug'atdan so'z o'chirish funksiyasi"""
    inglizcha = input("O'chiriladigan inglizcha so'zni kiriting: ").strip().lower()
    if inglizcha in lugat:
        del lugat[inglizcha]
        saqlash(lugat)
        print(f"🗑️ '{inglizcha}' so'zi lug'atdan o'chirildi.")
    else:
        print("❌ Bunday so'z lug'atda mavjud emas.")

def statistika(lugat):
    """Bonus: Lug'at statistikasini ko'rsatish funksiyasi"""
    jami_sozlar = len(lugat)
    print("\n--- 📊 LUG'AT STATISTIKASI ---")
    print(f"Jami saqlangan so'zlar soni: {jami_sozlar} ta")
    if jami_sozlar > 0:
        # Eng uzun inglizcha so'zni topish uchun namuna statistika
        eng_uzun = max(lugat.keys(), key=len)
        print(f"Eng uzun inglizcha so'z: '{eng_uzun}' ({len(eng_uzun)} ta harf)")
    print("------------------------------")

def menu():
    """Ilova boshqaruv menyusi (Menu Pattern)"""
    lugat = yuklash()
    
    while True:
        print("\n=== LUG'AT ILOVASI EN-UZ ===")
        print("1. So'z qidirish")
        print("2. Yangi so'z qo'shish")
        print("3. So'zni o'chirish")
        print("4. Statistika ko'rish")
        print("5. Chiqish")
        
        tanlov = input("Amalni tanlang (1-5): ").strip()
        
        if tanlov == "1":
            qidirish(lugat)
        elif tanlov == "2":
            qoshish(lugat)
        elif tanlov == "3":
            ochirish(lugat)
        elif tanlov == "4":
            statistika(lugat)
        elif tanlov == "5":
            print("👋 Dastur tugatildi. Xayr!")
            break
        else:
            print("❌ Noto'g'ri buyruq! Iltimos, 1 dan 5 gacha bo'lgan raqamlardan birini kiriting.")

# Dasturni ishga tushirish
if __name__ == "__main__":
    menu()
Kodning oʻziga xos imkoniyatlari va talablar ijrosi:
Modullik: yuklash, saqlash, qoshish, qidirish, ochirish va statistika amallari toʻliq alohida funksiyalarga ajratilgan.

JSON bilan ishlash: Ma'lumotlar sozlik.json faylida chiroyli formatda (indent=4) saqlanadi va yuklanadi.

Avtomatik yuklash va Boshlangʻich baza: Dastur ilk bor ishga tushganda fayl bo'lmasa, kod ichidagi 20 ta meva nomlaridan iborat tayyor lug'atni avtomatik ravishda faylga yozib oladi.

Ikki tomonlama qidiruv: Qidiruv tizimi ham inglizcha kalit so'zni, ham o'zbekcha tarjimani birdek qidira oladi.

Xatoliklar nazorati (try/except): Fayl o'qish yoki yozishda yuzaga kelishi mumkin bo'lgan har qanday kutilmagan tizim xatolari dasturni to'xtatib qo'ymaydi, balki ogohlantirish beradi.

Statistika (Bonus): Lug'atdagi jami so'zlar soni va eng uzun so'z kabi foydali ma'lumotlarni chiqaradi.
