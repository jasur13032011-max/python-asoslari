# python-asoslari
Mana, berilgan barcha talablarga to'liq javob beradigan, xatoliklarni oldindan aniqlaydigan va hisob-kitoblarni 2 xonagacha yaxlitlab ko'rsatadigan konsol kalkulyatori:

Python
# Foydalanuvchiga mavjud amallar ro'yxatini ko'rsatish
print("=" * 50)
print("           MUKAMMAL KONSOL KALKULYATORI           ")
print("=" * 50)
print("Mavjud amallar:")
print(" +  -> Qo'shish          |  -  -> Ayirish")
print(" * -> Ko'paytirish      |  /  -> Bo'lish (O'nli)")
print(" // -> Butunli bo'lish   |  %  -> Qoldikli bo'lish")
print(" ** -> Darajaga ko'tarish |  v  -> Kvadrat ildiz (Faqat 1-son)")
print(" f  -> Foiz hisoblash (1-sonning 2-son foizi)")
print("=" * 50)

# 1. Kiritilgan ma'lumotlarni tekshirish va casting qilish
son1_input = input("Birinchi sonni kiriting: ")

# Kiritilgan qiymat haqiqatan ham son ekanligini tekshirish
# (Nuqta va minus belgilarini hisobga olgan holda)
if not son1_input.replace('.', '', 1).replace('-', '', 1).isdigit():
    print("\n[XATOLIK]: Birinchi qiymat o'rniga son kiritmadingiz!")
else:
    son1 = float(son1_input)
    amal = input("Amalni kiriting (+, -, *, /, //, %, **, v, f): ").strip()

    # Kvadrat ildiz amali faqat bitta son bilan ishlagani uchun uni alohida tekshiramiz
    if amal == 'v':
        if son1 < 0:
            print("\n[XATOLIK]: Manfiy sonning kvadrat ildizini hisoblab bo'lmaydi!")
        else:
            natija = son1 ** 0.5
            print("-" * 50)
            print(f"Natija: √{son1} = {natija:.2f}")
            print("-" * 50)
            
    # Boshqa barcha amallar uchun ikkinchi sonni ham so'raymiz
    elif amal in ['+', '-', '*', '/', '//', '%', '**', 'f']:
        son2_input = input("Ikkinchi sonni kiriting: ")
        
        if not son2_input.replace('.', '', 1).replace('-', '', 1).isdigit():
            print("\n[XATOLIK]: Ikkinchi qiymat o'rniga son kiritmadingiz!")
        else:
            son2 = float(son2_input)
            print("-" * 50)

            # 2. Amallarni bajarish va 0 ga bo'lishni tekshirish
            if amal == '+':
                natija = son1 + son2
                print(f"Natija: {son1} + {son2} = {natija:.2f}")
                
            elif amal == '-':
                natija = son1 - son2
                print(f"Natija: {son1} - {son2} = {natija:.2f}")
                
            elif amal == '*':
                natija = son1 * son2
                print(f"Natija: {son1} * {son2} = {natija:.2f}")
                
            elif amal == '/':
                if son2 == 0:
                    print("[XATOLIK]: Sonni 0 ga bo'lish mumkin emas!")
                else:
                    natija = son1 / son2
                    print(f"Natija: {son1} / {son2} = {natija:.2f}")
                    
            elif amal == '//':
                if son2 == 0:
                    print("[XATOLIK]: 0 ga butunli bo'lish mumkin emas!")
                else:
                    natija = son1 // son2
                    print(f"Natija: {son1} // {son2} = {natija:.2f}")
                    
            elif amal == '%':
                if son2 == 0:
                    print("[XATOLIK]: 0 ga bo'lgandagi qoldiqni hisoblab bo'lmaydi!")
                else:
                    natija = son1 % son2
                    print(f"Natija: {son1} % {son2} = {natija:.2f}")
                    
            elif amal == '**':
                natija = son1 ** son2
                print(f"Natija: {son1} ^ {son2} = {natija:.2f}")
                
            elif amal == 'f':
                # a dan b foizni topish formulasi: (a * b) / 100
                natija = (son1 * son2) / 100
                print(f"Natija: {son1} sonining {son2}% foizi = {natija:.2f}")
            
            print("-" * 50)
    else:
        print("\n[XATOLIK]: Noto'g'ri amal kiritdingiz!")
💡 Kodning muhim qismlari tushuntirishi:
Xavfsiz kiritish: isdigit() tekshiruvi orqali foydalanuvchi tasodifan harf yoki belgi kiritib yuborsa, dastur xatolik bilan o'chib qolmaydi, balki tushunarli ogohlantirish beradi.

0 ga bo'lish himoyasi: /, //, va % amallarining barchasida if son2 == 0: sharti orqali dasturning ZeroDivisionError berishini oldi olindi.

Kvadrat ildiz (math'siz): Matematika qoidasiga ko'ra sonning 0.5 darajasi uning kvadrat ildiziga teng ( 
x

​
 =x 
0.5
 ), dasturda aynan shu mantiq ishlatildi.

Formatlash (:.2f): Har qanday uzun kasr son chiqadigan natija f-string ichida nuqtadan keyin 2 ta raqamgacha yaxlitlab ko'rsatiladi.
