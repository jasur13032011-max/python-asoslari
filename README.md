# python-asoslari
Geometrik figuralarning yuzasi va perimetrini hisoblab beradigan, toza kod yozish qoidalariga (docstring, default argumentlar, return) mos ravishda tayyorlangan Python dasturi:

Python
import math

# ==========================================
# 1. DOIRA (CIRCLE) FUNKSIYALARI
# ==========================================

def doira_maydoni(radius: float, pi: float = 3.14159) -> float:
    """Doira radiusiga ko'ra uning yuzasini hisoblaydi.
    
    Formula: S = pi * r^2
    """
    if radius < 0:
        raise ValueError("Radius manfiy bo'lishi mumkin emas!")
    return pi * (radius ** 2)

def doira_perimetri(radius: float, pi: float = 3.14159) -> float:
    """Doira radiusiga ko'ra uning uzunligini (perimetrini) hisoblaydi.
    
    Formula: P = 2 * pi * r
    """
    if radius < 0:
        raise ValueError("Radius manfiy bo'lishi mumkin emas!")
    return 2 * pi * radius


# ==========================================
# 2. TO'G'RI TO'RTLIK (RECTANGLE) FUNKSIYALARI
# ==========================================

def tortlik_maydoni(boyi: float, eni: float = 1.0) -> float:
    """To'g'ri to'rtburchakning bo'yi va eniga ko'ra yuzasini hisoblaydi.
    
    Formula: S = a * b
    """
    if boyi < 0 or eni < 0:
        raise ValueError("O'lchamlar manfiy bo'lishi mumkin emas!")
    return boyi * eni

def tortlik_perimetri(boyi: float, eni: float = 1.0) -> float:
    """To'g'ri to'rtburchakning bo'yi va eniga ko'ra perimetrini hisoblaydi.
    
    Formula: P = 2 * (a + b)
    """
    if boyi < 0 or eni < 0:
        raise ValueError("O'lchamlar manfiy bo'lishi mumkin emas!")
    return 2 * (boyi + eni)


# ==========================================
# 3. UCHBURCHAK (TRIANGLE) FUNKSIYALARI
# ==========================================

def uchburchak_maydoni(asos: float, balandlik: float) -> float:
    """Uchburchakning asosi va balandligiga ko'ra yuzasini hisoblaydi.
    
    Formula: S = 0.5 * a * h
    """
    if asos < 0 or balandlik < 0:
        raise ValueError("Asos yoki balandlik manfiy bo'lishi mumkin emas!")
    return 0.5 * asos * balandlik

def uchburchak_perimetri(a: float, b: float, c: float) -> float:
    """Uchburchakning uchta tomoniga ko'ra perimetrini hisoblaydi.
    
    Formula: P = a + b + c
    """
    if a < 0 or b < 0 or c < 0:
        raise ValueError("Tomonlar manfiy bo'lishi mumkin emas!")
    # Uchburchak qoidasini tekshirish (ixtiyoriy, lekin foydali validatsiya)
    if not (a + b > c and a + c > b and b + c > a):
        raise ValueError("Bunday tomonlar bilan uchburchak yasab bo'lmaydi!")
    return a + b + c


# ==========================================
# ASOSIY MENU FUNKSIYASI
# ==========================================

def main_menu():
    while True:
        print("\n" + "=" * 15 + " GEOMETRIK KALKULYATOR " + "=" * 15)
        print("1. Doira (Yuzasi va Uzunligi)")
        print("2. To'g'ri to'rtburchak (Yuzasi va Perimetri)")
        print("3. Uchburchak (Yuzasi va Perimetri)")
        print("4. Chiqish")
        print("=" * 53)
        
        tanlov = input("Figurani tanlang (1-4): ").strip()
        
        try:
            if tanlov == "1":
                r = float(input("Doira radiusini kiriting: "))
                S = doira_maydoni(r)
                P = doira_perimetri(r)
                print(f"\n🟢 Doira Natijalari:")
                print(f"  - Yuzasi:    {S:.4f}")
                print(f"  - Perimetri: {P:.4f}")
                
            elif tanlov == "2":
                a = float(input("To'rtburchak bo'yini kiriting: "))
                b_input = input("To'rtburchak enini kiriting (standart 1.0 uchun Enter bosing): ").strip()
                
                # Default qiymatdan foydalanish mantiqi
                if b_input == "":
                    S = tortlik_maydoni(a)
                    P = tortlik_perimetri(a)
                else:
                    b = float(b_input)
                    S = tortlik_maydoni(a, b)
                    P = tortlik_perimetri(a, b)
                    
                print(f"\n🟦 To'g'ri to'rtburchak Natijalari:")
                print(f"  - Yuzasi:    {S:.2f}")
                print(f"  - Perimetri: {P:.2f}")
                
            elif tanlov == "3":
                print("--- Yuza hisoblash uchun ---")
                asos = float(input("Uchburchak asosini kiriting: "))
                balandlik = float(input("Uchburchak balandligini kiriting: "))
                S = uchburchak_maydoni(asos, balandlik)
                
                print("--- Perimetr hisoblash uchun ---")
                tomon1 = float(input("1-tomonni kiriting: "))
                tomon2 = float(input("2-tomonni kiriting: "))
                tomon3 = float(input("3-tomonni kiriting: "))
                P = uchburchak_perimetri(tomon1, tomon2, tomon3)
                
                print(f"\n🔺 Uchburchak Natijalari:")
                print(f"  - Yuzasi:    {S:.2f}")
                print(f"  - Perimetri: {P:.2f}")
                
            elif tanlov == "4":
                print("👋 Matematika darsimiz tugadi. Salomat bo'ling!")
                break
            else:
                print("❌ Noto'g'ri buyruq! 1 dan 4 gacha son kiriting.")
                
        except ValueError as xato:
            # Manfiy son yoki noto'g'ri ma'lumot kiritilganda dastur o'chib ketmaydi
            print(f"\n⚠️ [XATOLIK]: {xato}")
            print("Iltimos, qiymatlarni qaytadan to'g'ri kiriting.")

# Dasturni faqat to'g'ridan-to'g'ri ishga tushganda bajarish
if __name__ == "__main__":
    main_menu()
💡 Kodning arxitektura jihatdan afzalliklari:
Toza funksiyalar (Single Responsibility): Har bir funksiya faqat bitta matematik amalni bajaradi va natijani return orqali qaytaradi. Bu ulardan loyihaning boshqa joylarida ham qayta foydalanish imkonini beradi.

Docstring ("""..."""): Har bir funksiya tepasida uning nima ish qilishi va qaysi formula asosida ishlashi aniq yozilgan.

Default Argumentlar: pi=3.14159 va eni=1.0 parametrlari agar ikkinchi argument berilmasa, avtomatik ravishda tayyor qiymatdan foydalanadi.

raise ValueError: Kod ichida manfiy o'lchovlar kiritilishi qat'iy nazorat qilingan. Xato aniqlansa, maxsus xabar bilan tizimga signal uzatiladi va bu xato main_menu ichidagi try/except bloki orqali xavfsiz ushlab qolinadi.
