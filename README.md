# python-asoslari
Mana, talabalar baholarini qabul qiladigan, ularni qat'iy tekshiruvdan o'tkazadigan (validatsiya) va barcha statistik ko'rsatkichlarni hisoblab beradigan toza va mukammal Python dasturi:

Python
print("=" * 55)
print("         TALABALAR BAHOLARI TAHLILI TIZIMI        ")
print("=" * 55)

baholar = []
baho_soni = 1

# 1. Kamida 5 ta to'g'ri baho kiritishni ta'minlaydigan sikl
while len(baholar) < 5:
    kiritish = input(f"{baho_soni}-bahoni kiriting (yoki tugatish uchun 'ok' deb yozing): ").strip().lower()
    
    # Agar 5 ta baho bo'lgan bo'lsa va 'ok' yozilsa, siklni to'xtatish
    if kiritish == 'ok':
        if len(baholar) >= 5:
            break
        else:
            print(f"[Ogohlantirish]: Kamida 5 ta baho bo'lishi shart! Hozircha {len(baholar)} ta kiritdingiz.")
            continue

    # Kiritilgan qiymat raqam ekanligini tekshirish
    if not kiritish.isdigit():
        print("[Xatolik]: Iltimos, faqat butun son kiriting!")
        continue
        
    baho = int(kiritish)
    
    # Validatsiya: 0-100 oralig'idan tashqaridagi baholarni rad etish
    if baho < 0 or baho > 100:
        print("[Rad etildi]: Baho faqat 0 dan 100 gacha bo'lishi mumkin!")
        continue
        
    baholar.append(baho)
    baho_soni += 1

print("\n" + "="*20 + " TAHLIL NATIJALARI " + "="*20)

# 2. Baholarni oshib boruvchi tartibda saralash
baholar.sort()
print(f"📈 Saralangan baholar (oshib boruvchi): {baholar}")

# 3. Matematik statistikani hisoblash
eng_yuqori = max(baholar)
eng_past = min(baholar)
ortacha = sum(baholar) / len(baholar)

# Mediana hisoblash (Saralangan listning o'rtasidagi qiymat)
n = len(baholar)
if n % 2 == 1:
    mediana = baholar[n // 2]
else:
    mediana = (baholar[(n // 2) - 1] + baholar[n // 2]) / 2

# 4. List comprehension yordamida a'lo baholarni (90+) filtrlash
alo_baholar = [b for b in baholar if b >= 90]

# 5. Qoniqarsiz baholarni (60 dan kam) ajratish
qoniqarsiz_baholar = [b for b in baholar if b < 60]

# Natijalarni chiroyli f-string formatida chiqarish
print("-" * 59)
print(f"📊 Jami kiritilgan baholar soni: {n} ta")
print(f"🧮 O'rtacha ball:               {ortacha:.2f}")
print(f"⭐ Eng yuqori ball:             {eng_yuqori}")
print(f"📉 Eng past ball:               {eng_past}")
print(f"🎯 Mediana ko'rsatkichi:        {mediana:.1f}")
print("-" * 59)
print(f"🥇 A'lo baholar (90+):          {alo_baholar if alo_baholar else 'Yo\'q'}")
print(f"❌ Qoniqarsiz baholar (<60):    {qoniqarsiz_baholar if qoniqarsiz_baholar else 'Yo\'q'}")
print("=" * 59)
💡 Kodning muhim qismlari mantiqi:
Qat'iy Validatsiya: Dastur foydalanuvchi 0 dan kichik yoki 100 dan katta son kiritsa, uni baholar ro'yxatiga qo'shmaydi va qaytadan to'g'ri son kiritishni talab qiladi.

Moslashuvchan soni: while len(baholar) < 5 sharti minimal chegarani belgilaydi, lekin talaba xohlasa 5 tadan ko'p (masalan, 10 ta) baho kiritib, keyin 'ok' yozuvi orqali tahlilni boshlashi mumkin.

List Comprehension: [b for b in baholar if b >= 90] kodi an'anaviy for siklini bir qatorga qisqartirib, tezkor filtr qilish imkonini beradi.

Mediana algoritmi: Agar kiritilgan baholar soni toq bo'lsa, ro'yxatning qo'q o'rtasidagi sonni oladi. Agar juft bo'lsa, o'rtadagi ikkita sonning o'rtacha arifmetigini hisoblab beradi.
