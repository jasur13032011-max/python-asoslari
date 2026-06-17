# python-asoslari
Xavfsiz, murakkab va foydalanuvchi talablariga moslashuvchan parollar yaratuvchi hamda jarayon vaqtini qayd etuvchi professional Python dasturi:

Python
import random
import string
from datetime import datetime

# ==========================================
# 1-FUNKSIYA: FOYDALANUVChI PARAMЕTRLARINI OLISh
# ==========================================
def parol_sozlamalari():
    """Foydalanuvchidan parol uzunligi va tarkibini so'raydi va qaytaradi."""
    print("=" * 50)
    print("         PROFFЕSIONAL PAROL GЕNЕRATORI        ")
    print("=" * 50)
    
    # Parol uzunligi validatsiyasi (8 dan 32 gacha)
    while True:
        uzunlik_input = input("Parol uzunligini kiriting (8-32): ").strip()
        if uzunlik_input.isdigit():
            uzunlik = int(uzunlik_input)
            if 8 <= uzunlik <= 32:
                break
        print("⚠️ Xatolik: Iltimos, 8 dan 32 gacha bo'lgan butun son kiriting!")

    # Tarkib bo'yicha so'rovlar
    katta_harf = input("Katta harflar bo'lsinmi? (ha/yo'q): ").strip().lower() == 'ha'
    raqamlar = input("Raqamlar bo'lsinmi? (ha/yo'q): ").strip().lower() == 'ha'
    belgilar = input("Maxsus belgilar bo'lsinmi? (ha/yo'q): ").strip().lower() == 'ha'
    
    return uzunlik, katta_harf, raqamlar, belgilar


# ==========================================
# 2-FUNKSIYA: SIMVOLLAR BAZASINI ShAKLLANTIRISh
# ==========================================
def belgi_bazasi_yaratish(katta_harf, raqamlar, belgilar):
    """Tanlovga qarab string modulidan kerakli belgilarni yig'adi."""
    # Standart holatda faqat kichik harflar har doim bo'ladi
    baza = string.ascii_lowercase
    
    if katta_harf:
        baza += string.ascii_uppercase
    if raqamlar:
        baza += string.digits
    if belgilar:
        baza += string.punctuation
        
    return baza


# ==========================================
# 3-FUNKSIYA: PAROLNI GЕNЕRATSIYA QILISh
# ==========================================
def parol_generatsiya(uzunlik, simvollar_bazasi):
    """random.choices yordamida bazadan tasodifiy parolni yig'adi."""
    if not simvollar_bazasi:
        return "Xatolik: Hech bo'lmasa bitta belgi turini tanlashingiz kerak edi!"
        
    # random.choices ro'yxat qaytaradi, uni .join() bilan matnga aylantiramiz
    tasodifiy_list = random.choices(simvollar_bazasi, k=uzunlik)
    tayyor_parol = "".join(tasodifiy_list)
    return tayyor_parol


# ==========================================
# ASOSIY IShGA TUShIRISh BLOKI
# ==========================================
if __name__ == "__main__":
    # 1. Sozlamalarni olish
    uzunlik, katta, raqam, belgi = parol_sozlamalari()
    
    # 2. Bazani tayyorlash
    baza = belgi_bazasi_yaratish(katta, raqam, belgi)
    
    # 3. Parol yaratish
    yangi_parol = parol_generatsiya(uzunlik, baza)
    
    # 4. datetime yordamida joriy vaqtni aniqlash va chiqarish
    hozirgi_vaqt = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    
    print("\n" + "🌟" * 10 + " NATIJA " + "🌟" * 10)
    print(f"🔑 Yaratilgan parol: {yangi_parol}")
    print(f"📅 Yaratilgan vaqti: {hozirgi_vaqt}")
    print("=" * 50)
💡 Dasturdagi muhim vositalar tushuntirishi:
string moduli elementlari:

string.ascii_lowercase: barcha kichik ingliz harflari (a-z).

string.ascii_uppercase: barcha katta ingliz harflari (A-Z).

string.digits: 0 dan 9 gacha bo'lgan raqamlar matni (0123456789).

string.punctuation: barcha maxsus belgilar (!@#$%^&*()_+...).

random.choices(baza, k=uzunlik): Berilgan simvollar bazasidan ko'rsatilgan k (uzunlik) miqdoricha elementni tasodifiy ravishda (takrorlanish imkoniyati bilan) juda tezkorlik bilan tanlab, ro'yxat holatida qaytaradi.

datetime.now().strftime(...): Parol aynan qaysi yilda, oyda, kunda va hatto sekundda yaratilganini inson ko'ziga chiroyli va tushunarli formatga solib ko'rsatadi.
