# python-asoslari
Mana, foydalanuvchidan ma'lumot oluvchi, kiritilgan qiymatlar turini tekshiruvchi va barcha arifmetik amallarni xavfsiz bajariuvchi Python dasturi:

Python
# Foydalanuvchidan sonlarni kiritishni so'rash va turini float'ga o'tkazish (casting)
son1_input = input("Birinchi sonni kiriting: ")
son2_input = input("Ikkinchi sonni kiriting: ")

son1 = float(son1_input)
son2 = float(son2_input)

# O'zgaruvchilarning turini type() yordamida tekshirish va chiqarish
print("-" * 40)
print(f"son1 o'zgaruvchisi turi: {type(son1)}")
print(f"son2 o'zgaruvchisi turi: {type(son2)}")
print("-" * 40)

# 4 ta asosiy arifmetik amalni bajarish va f-string orqali formatlash
# (:.2f) yordamida natijalar nuqtadan keyin 2 ta raqamgacha yaxlitlanadi

qo_shish = son1 + son2
ayirish = son1 - son2
ko_paytirish = son1 * son2

print(f"Qo'shish natijasi: {son1} + {son2} = {qo_shish:.2f}")
print(f"Ayirish natijasi: {son1} - {son2} = {ayirish:.2f}")
print(f"Ko'paytirish natijasi: {son1} * {son2} = {ko_paytirish:.2f}")

# 0 ga bo'lish xatoligini oldini olish (Xavfsiz bo'lish)
if son2 != 0:
    bo_lish = son1 / son2
    print(f"Bo'lish natijasi: {son1} / {son2} = {bo_lish:.2f}")
else:
    print("Xatolik: Sonni 0 ga bo'lish mumkin emas!")

print("-" * 40)
