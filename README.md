# python-asoslari
Mana, berilgan barcha shartlar va OOP (Obyektga Yoʻnaltirilgan Dasturlash) qoidalari asosida yozilgan BankAccount va PremiumAccount klasslari kodi.

Bu yerda har bir amal tarixga yozib boriladi, salbiy qoldiqqa yo'l qo'yilmaydi (ValueError orqali) va vorislik (inheritance) xususiyatidan to'g'ri foydalanilgan.

Python Dastur Kodi
Python
from datetime import datetime

class BankAccount:
    def __init__(self, ism: str, qoldiq: float = 0.0):
        self.ism = ism
        self.qoldiq = qoldiq
        self.tarix = []  # Har bir amalni dict ko'rinishida saqlaymiz
        
        # Hisob ochilganini tarixga yozib qo'yamiz
        self._tarixga_yoz(amal="Hisob ochildi", miqdor=qoldiq)

    def _tarixga_yoz(self, amal: str, miqdor: float, qoshimcha: str = ""):
        """Ichki metod: Har bir amalni vaqt bilan birga tarixga yozadi"""
        vaqt = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        self.tarix.append({
            "vaqt": vaqt,
            "amal": amal,
            "miqdor": miqdor,
            "qoldiq": self.qoldiq,
            "izoh": qoshimcha
        })

    def pul_qoyish(self, miqdor: float):
        """Hisobga pul kirim qilish"""
        if miqdor <= 0:
            raise ValueError("Kiritilayotgan pul miqdori noldan katta bo'lishi kerak!")
        
        self.qoldiq += miqdor
        self._tarixga_yoz(amal="Kirim", miqdor=miqdor)
        print(f"✅ {self.ism}: Hisobga {miqdor} so'm qo'shildi.")

    def pul_chiqarish(self, miqdor: float) -> bool:
        """Hisobdan pul yechish (Salbiy qoldiq tekshiruvi bilan)"""
        if miqdor <= 0:
            raise ValueError("Yechilayotgan pul miqdori noldan katta bo'lishi kerak!")
        
        if self.qoldiq < miqdor:
            raise ValueError(f"❌ {self.ism}: Hisobda mablag' yetarli emas! Qoldiq: {self.qoldiq} so'm.")
        
        self.qoldiq -= miqdor
        self._tarixga_yoz(amal="Chiqim", miqdor=miqdor)
        print(f"💸 {self.ism}: Hisobdan {miqdor} so'm yechildi.")
        return True

    def qoldiq_korish(self):
        """Joriy qoldiq va qisqacha tarixni chiqarish"""
        print(f"\n=== {self.ism} kontenti qoldig'i: {self.qoldiq} so'm ===")
        print("Oxirgi amallar tarixi:")
        for odim in self.tarix[-3:]:  # Oxirgi 3 ta amalni ko'rsatadi
            print(f" [{odim['vaqt']}] {odim['amal']}: {odim['miqdor']} so'm (Qoldiq: {odim['qoldiq']}) {odim['izoh']}")

    def transfer(self, qabul_qiluvchi: 'BankAccount', miqdor: float):
        """Boshqa hisob raqamiga pul o'tkazish"""
        if miqdor <= 0:
            raise ValueError("O'tkatma miqdori noldan katta bo'lishi kerak!")
        
        # Pulni yechishga urinib ko'ramiz (agar mablag' yetmasa, avtomatik ValueError otiladi)
        self.pul_chiqarish(miqdor)
        
        # Qabul qiluvchining hisobiga qo'shamiz
        qabul_qiluvchi.qoldiq += miqdor
        qabul_qiluvchi._tarixga_yoz(amal="O'tkatma (Kirim)", miqdor=miqdor, qoshimcha=f"Yuboruvchi: {self.ism}")
        
        # Yuboruvchining tarixini yangilaymiz (oxirgi Chiqim amalini o'tkatmaga o'zgartirib qo'yamiz)
        self.tarix[-1]['amal'] = "O'tkatma (Chiqim)"
        self.tarix[-1]['izoh'] = f"Qabul qiluvchi: {qabul_qiluvchi.ism}"
        
        print(f"🔄 {self.ism} -> {qabul_qiluvchi.ism} hisobiga {miqdor} so'm muvaffaqiyatli o'tkazildi.")

    def __str__(self) -> str:
        """Obyekt haqida chiroyli ma'lumot"""
        return f"🏦 BankAccount | Ega: {self.ism} | Qoldiq: {self.qoldiq} so'm"


class PremiumAccount(BankAccount):
    def __init__(self, ism: str, qoldiq: float = 0.0, kredit_limiti: float = 0.0):
        # Ota klassning __init__ metodini chaqiramiz
        super().__init__(ism, qoldiq)
        self.kredit_limiti = kredit_limiti

    def pul_chiqarish(self, miqdor: float) -> bool:
        """Kredit limitini hisobga olgan holda pul yechish (Metod override)"""
        if miqdor <= 0:
            raise ValueError("Yechilayotgan pul miqdori noldan katta bo'lishi kerak!")
        
        # Premium foydalanuvchi jami qoldiq + kredit limiti miqdorigacha pul yecha oladi
        jami_ruxsat = self.qoldiq + self.kredit_limiti
        
        if jami_ruxsat < miqdor:
            raise ValueError(f"❌ {self.ism} (Premium): Kredit limiti bilan ham mablag' yetarli emas! Maksimal yechish: {jami_ruxsat} so'm.")
        
        self.qoldiq -= miqdor
        self._tarixga_yoz(amal="Chiqim (Premium)", miqdor=miqdor)
        print(f"💎 {self.ism} (Premium): Hisobdan {miqdor} so'm yechildi (Kredit limiti ishlatilgan bo'lishi mumkin).")
        return True

    def __str__(self) -> str:
        return f"💎 PremiumAccount | Ega: {self.ism} | Qoldiq: {self.qoldiq} so'm | Kredit Limiti: {self.kredit_limiti} so'm"
Ishlatish va Transfer Amallari (Kamida 3 ta obyekt)
Kodni tekshirish uchun 3 ta mijoz yaratamiz: ikkita oddiy va bitta Premium hisob egasi. Ular o'rtasida pul o'tkazmalarini amalga oshiramiz.

Python
# 1. Obyektlarni yaratish
mijoz1 = BankAccount("Anvar", 500_000)
mijoz2 = BankAccount("Zilola", 100_000)
mijoz3 = PremiumAccount("Sardor", 200_000, kredit_limiti=300_000) # Jami 500_000 gacha ishlata oladi

print("\n--- 🟢 BOSH LANG'ICH HOLAT ---")
print(mijoz1)
print(mijoz2)
print(mijoz3)

print("\n--- 🔄 TRANSAKSIYALAR ---")
try:
    # 1-O'tkatma: Anvar Zilolaga 200,000 so'm yuboradi
    mijoz1.transfer(mijoz2, 200_000)
    
    # 2-O'tkatma: Zilola Sardorga 150,000 so'm yuboradi
    mijoz2.transfer(mijoz3, 150_000)
    
    # 3-O'tkatma (Premium imkoniyati): 
    # Sardor hisobida 350,000 bor edi, lekin u Anvarga 600,000 o'tkazmoqchi.
    # Uning 300,000 kredit limiti bor, demak o'tkazma muvaffaqiyatli bo'lishi kerak.
    mijoz3.transfer(mijoz1, 600_000)

except ValueError as e:
    print(e)

print("\n--- 📊 YAKUNIY STATISTIKA VA AMALLAR TARIXI ---")
mijoz1.qoldiq_korish()
mijoz2.qoldiq_korish()
mijoz3.qoldiq_korish()

print("\n--- 🚫 XATOLIKNI TEKSHIRISH (Salbiy qoldiqqa urinish) ---")
try:
    # Zilola endi hisobidan ko'p pul yechishga urunib ko'radi
    mijoz2.pul_chiqarish(500_000)
except ValueError as e:
    print(e)
Kod qanday ishlaydi?
Encapsulation & History: _tarixga_yoz yordamchi metodi har safar pul o'tkazilganda, yechilganda yoki kiritilganda joriy vaqtni olib self.tarix ro'yxatiga dict shaklida qo'shadi.

Polymorphism & Override: PremiumAccount klassi pul_chiqarish metodini o'zgartirgan (override qilgan). Shuning uchun Sardor o'z hisobidagi puldan ko'proq (manfiy balansga kirib) pul o'tkaza oldi, chunki dastur uning kredit_limitini hisobga oldi.

Xavfsizlik: Agar mijoz2 (Zilola) o'zida boridan ortiqcha pul ishlatmoqchi bo'lsa, dastur ValueError beradi va o'tkatmani to'xtatadi.
