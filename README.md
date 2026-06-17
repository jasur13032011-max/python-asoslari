# python-asoslari
    Mana, berilgan barcha talablarga javob beradigan, kiritilgan matnni tahlil qilib beruvchi mukammal Python dasturi:

Python
# Foydalanuvchidan matn qabul qilish
matn = input("Iltimos, tahlil qilish uchun matn kiriting: ")

# Bo'sh matn holatini tekshirish
# .strip() metodi matn boshidagi va oxiridagi ortiqcha bo'shliqlarni olib tashlaydi
if not matn.strip():
    print("\n[Xatolik]: Siz hech qanday matn kiritmadingiz yoki faqat bo'shliqlar kiritdingiz!")
else:
    # 1. Matn uzunligi va so'zlar sonini aniqlash
    # .split() metodi matnni bo'shliqlar bo'yicha bo'laklarga (so'zlarga) ajratadi va ro'yxat qaytaradi
    sozlar_royxati = matn.split()
    matn_uzunligi = len(matn)
    sozlar_soni = len(sozlar_royxati)

    # 2. String metodlarini qo'llash
    katta_harf = matn.upper()                         # 1-metod: Hamma harflarni katta qiladi
    kichik_harf = matn.lower()                       # 2-metod: Hamma harflarni kichik qiladi
    tozalangan_matn = matn.strip()                   # 3-metod: Chetki bo'shliqlarni tozalaydi
    almashtirilgan = matn.replace(" ", "_")          # 4-metod: Bo'shliqlarni pastki chiziqqa almashtiradi
    # .split() yuqorida ishlatildi va bu 5-metod hisoblanadi

    # 3. Slicing (Kesib olish) orqali matnning bir qismini chiqarish
    # Matnning dastlabki 10 ta belgisini kesib olamiz
    birinchi_10_belgi = matn[:10]

    # 4. Natijalarni f-string yordamida chiroyli ko'rinishda chiqarish
    print("\n" + "="*20 + " MATN TAHLILI " + "="*20)
    print(f"📝 Kiritilgan matn: '{tozalangan_matn}'")
    print(f"📊 Belgilar soni (uzunligi): {matn_uzunligi} ta")
    print(f"🔤 So'zlar soni: {sozlar_soni} ta")
    print("-" * 54)
    print(f"🔺 Katta harflarda: {katta_harf}")
    print(f"🔻 Kichik harflarda: {kichik_harf}")
    print(f"🔗 Bo'shliqlar almashtirilganda: {almashtirilgan}")
    print(f"✂️ Slicing (Dastlabki 10 ta belgi): '{birinchi_10_belgi}'")
    print("=" * 54)
💡 Dastur qanday ishlaydi va metodlar tushuntirishi:
strip(): Agar foydalanuvchi adashib matn boshiga yoki oxiriga ko'p bo'shliq qo'yib yuborsa, ularni o'chirib, toza matn bilan ishlashga yordam beradi.

split(): Matn ichidagi so'zlarni bir-biridan ajratib oladi va len() funksiyasi orqali matnda jami nechta so'z borligini aniqlashga xizmat qiladi.

[:10]: Agar kiritilgan matn uzun bo'lsa, indekslash qoidasiga ko'ra 0-indeksdan to 10-indeksgaacha bo'lgan qismini qirqib ko'rsatadi.
