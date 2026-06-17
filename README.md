# python-asoslari
Mana, kiritilgan yosh, hafta kuni va talabalik maqomiga qarab chipta narxini avtomatik va adolatli hisoblab beradigan mukammal Python dasturi.

Bunda barcha chegirmalar va hafta oxiridagi qo'shimcha narxlar zanjirsimon tartibda hisoblanadi:

Python
# Boshlang'ich chipta narxi (Asosiy narx)
CHIPTA_NARXI = 100000  # 100,000 so'm

print("=" * 50)
print("       CHIPTA NARXINI HISOBLASH TIZIMI        ")
print("=" * 50)

# Foydalanuvchidan ma'lumotlarni so'rash
yosh = int(input("Yoshingizni kiriting: "))
hafta_kuni = input("Hafta kunini kiriting (dushanba-yakshanba): ").strip().lower()
talaba_mi = input("Talabamisiz? (ha/yo'q): ").strip().lower()

# Asosiy narxni yoshga qarab belgilash (4 ta blokli if/elif/else)
if yosh >= 0 and yosh <= 6:
    kodlangan_narx = 0
    chegirma_turi = "0-6 yosh (Bepul)"
    
elif yosh >= 7 and yosh <= 17:
    kodlangan_narx = CHIPTA_NARXI * 0.5  # 50% yarim narx
    chegirma_turi = "7-17 yosh (50% chegirma)"
    
elif yosh >= 60:
    kodlangan_narx = CHIPTA_NARXI * 0.7  # 30% chegirma (ya'ni 70% narxi qoladi)
    chegirma_turi = "60+ yosh (30% chegirma)"
    
else:
    kodlangan_narx = CHIPTA_NARXI  # To'liq narx
    chegirma_turi = "To'liq narx (Chegirmasiz)"

# Hafta oxirini tekshirish (and / or operatorlari ishlatilgan)
# Dam olish kunlari chipta narxi 20% ga qimmatlashadi
if hafta_kuni == "shanba" or hafta_kuni == "yakshanba":
    kodlangan_narx = kodlangan_narx * 1.2
    kun_turi = "Dam olish kuni (+20% qimmatlashish)"
else:
    kun_turi = "Ish kuni (Oddiy tarif)"

# Talabalik chegirmasini qo'llash
# Agar foydalanuvchi talaba bo'lsa va chipta bepul bo'lmasa, yana 15% chegirma beriladi
if talaba_mi == "ha" and kodlangan_narx > 0:
    kodlangan_narx = kodlangan_narx * 0.85  # 15% chegirma
    talaba_status = "Talaba (Qo'shimcha 15% chegirma)"
else:
    talaba_status = "Talaba emas / Tatbiq etilmaydi"

# Yakuniy natijani chiroyli formatda chiqarish
print("\n" + "-"*15 + " CHIPTA CHЕKI " + "-"*15)
print(f"📊 Yosh tarifi:       {chegirma_turi}")
print(f"📅 Hafta turi:       {kun_turi}")
print(f"🎓 Talaba maqomi:     {talaba_status}")
print("-" * 44)
print(f"💵 Yakuniy narx:      {kodlangan_narx:,.2f} so'm")
print("=" * 44)
💡 Tizim qanday ishlaydi?
Yosh filtratsiyasi: yosh >= 0 and yosh <= 6 kabi shartlar orqali foydalanuvchining yosh toifasi aniqlanadi va dastlabki narx shakllantiriladi.

Kun tekshiruvi: or operatori yordamida kiritilgan kun shanba yoki yakshanba ekanligi aniqlanib, narx 1.2 koeffitsiyentiga (20% qimmatlashish) ko'paytiriladi.

Zanjir chegirma: Agar shartlar bajarilsa, talaba chegirmasi avvalgi hisoblangan narx ustiga qo'shimcha ravishda (ko'paytirish mantiqi orqali) qo'llaniladi.

Chiroyli format (:,.2f): Narxni chiqarishda raqamlarni mingliklar bo'yicha ajratadi (masalan, 102,000.00) va tushunarli ko'rinishga keltiradi.
