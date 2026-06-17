# python-asoslari
Mana, random moduli, while sikli va qiyinlik darajalariga ega bo'lgan, qiziqarli va mukammal "Sonni top" o'yini:

Python
import random

print("=" * 50)
print("          'SONNI TOP' INTЕRAKTIV O'YINI          ")
print("=" * 50)
print("O'yin qoidalari:")
print("- Tanlangan orliqdagi yashirin sonni topishingiz kerak.")
print("- Sizda jami 10 ta urinish bor.")
print("- O'yinni to'xtatish uchun 'q' tugmasini bosing.")
print("=" * 50)

# 1. Qiyinlik darajasini tanlash
print("Qiyinlik darajasini tanlang:")
print("1 -> Oson (1 - 50 oralig'ida)")
print("2 -> O'rta (1 - 100 oralig'ida)")
print("3 -> Qiyin (1 - 200 oralig'ida)")
print("-" * 50)

daraja = input("Daraja raqamini kiriting (1/2/3): ").strip()

# Tanlangan darajaga qarab chegarani belgilash
if daraja == "1":
    chegara = 50
elif daraja == "3":
    chegara = 200
else:
    # Agar foydalanuvchi noto'g'ri kiritsa, standart holatda 2-daraja (100) tanlanadi
    chegara = 100
    print("[Eslatma]: Standart o'rta daraja (1-100) tanlandi.")

# 2. random.randint yordamida tasodifiy sonni tanlash
yashirin_son = random.randint(1, chegares)
print(f"\nMen 1 dan {chegara} gacha bo'lgan sonni o'yladim. Uni topishga urinib ko'ring!")
print("=" * 50)

# O'yin o'zgaruvchilari
urinishlar_soni = 0
MAKS_URINISH = 10
yutdi = False

# 3. while sikli orqali urinishlarni boshqarish
while urinishlar_soni < MAKS_URINISH:
    urinishlar_soni += 1
    tahmin_input = input(f"[{urinishlar_soni}-urinish] Tahminingizni kiriting: ").strip().lower()
    
    # Foydalanuvchi 'q' yozsa o'yinni to'xtatish (break)
    if tahmin_input == 'q':
        print(f"\nO'yin to'xtatildi. Yashirin son {yashirin_son} edi. Keyingi safar ko'rishguncha!")
        break
        
    # Kiritilgan qiymat son ekanligini tekshirish
    if not tahmin_input.isdigit():
        print("[Ogohlantirish]: Iltimos, faqat butun son yoki chiqish uchun 'q' kiriting.")
        urinishlar_soni -= 1 # Noto'g'ri kiritish urinishlar sonini kamaytirmaydi
        continue
        
    tahmin = int(tahmin_input)
    
    # 4. Katta / Kichik / To'g'ri xabarlarini chiqarish
    if tahmin < yashirin_son:
        print("❌ Yo'q, men o'ylagan son bundan KATTA!")
    elif tahmin > yashirin_son:
        print("❌ Yo'q, men o'ylagan son bundan KICHIK!")
    else:
        yutdi = True
        break  # To'g'ri topilsa sikldan chiqiladi

print("=" * 50)

# 5. O'yin yakuniy natijasini chiqarish
if yutdi:
    print(f"🎉 TABRIKLAYMIZ! Siz g'olib bo'ldingiz!")
    print(f"🎯 Men o'ylagan son haqiqatan ham: {yashirin_son}")
    print(f"📊 Siz buni {urinishlar_soni} ta urinishda topdingiz!")
elif tahmin_input != 'q':
    print("😢 Afsuski, urinishlaringiz tugadi.")
    print(f"🔒 Men o'ylagan yashirin son {yashirin_son} edi.")
    print("Yana urinib ko'ring, siz albatta uddalaysiz!")

print("=" * 50)
💡 Kodning muhim qismlari mantiqi:
random.randint(1, chegares): Foydalanuvchi tanlagan qiyinlik darajasiga ko'ra 1 dan 50, 100 yoki 200 gacha bo'lgan butun sonni kompyuter xotirasida tasodifiy yaratadi.

while urinishlar_soni < MAKS_URINISH: Sikl ko'pi bilan 10 marta aylanadi. Har bir noto'g'ri harf kiritilganda continue orqali urinishlar soni bekorga kuyib ketishidan himoyalangan.

break operatori: O'yindagi ikki holatda — foydalanuvchi taslim bo'lish uchun 'q' yozganda yoki sonni to'g'ri topganda siklni darhol to'xtatish uchun xizmat qiladi.
