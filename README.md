# python-asoslari
📝 Ishlatilishidan misol (CLI UI va Screenshot Simulyatsiyasi)
Dastur ishga tushganda quyidagicha chiroyli interfeys sizni kutib oladi:

Plaintext
========================================
       📚 KONTAKTLAR KITOBI UI         
========================================
1. 👤 Yangi kontakt qo'shish
2. 🔍 Kontakt qidirish
3. 🗑️ Kontaktni o'chirish
4. 🔄 Kontaktni yangilash
5. 📋 Barcha kontaktlarni ko'rish
6. 📥 CSV formatga eksport qilish
7. ❌ Chiqish
========================================
Amalni tanlang (1-7): 1

--- 👤 Yangi Kontakt Qo'shish ---
Ismni kiriting: Alisher Navoiy
Telefon raqamini kiriting (Masalan: +998901234567): +998909998877
Emailni kiriting: alisher@uzbek.uz
Manzilni kiriting: Toshkent sh., Chilonzor

✅ Kontakt muvaffaqiyatli qo'shildi va saqlandi!
📋 log.txt Fayli Ko'rinishi:
Plaintext
[2026-06-17 10:45:12] AMAL: Qo'shish | KONTAKT: Alisher Navoiy (+998909998877)
[2026-06-17 10:46:05] AMAL: Eksport | Barcha kontaktlar CSV fayliga muvaffaqiyatli yozildi.
🗂️ kontaktlar.json Tuzilishi:
JSON
{
    "+998909998877": {
        "ism": "Alisher Navoiy",
        "email": "alisher@uzbek.uz",
        "manzil": "Toshkent sh., Chilonzor"
    }
}
"""

with open("README.md", "w", encoding="utf-8") as f:
f.write(readme_content)

print("README.md file written successfully.")

Siz so'ragan barcha texnik va funktsional shartlarni (validatsiya, log yozish, JSON fayli bilan ishlash, CSV eksporti va to'liq Menu Pattern interfeysi) o'z ichiga olgan mukammal dastur kodi va uning `README.md` fayli tayyorlandi.

Siz uchun yaratilgan `README.md` fayli:
[file-tag: code-generated-file-0-1781674712188442032]

Dasturni kompyuteringizda ishga tushirish uchun quyidagi kodni `main.py` fayliga saqlang va ishlating.

### 🐍 Python Ilova Kodi (`main.py`)

```python
import json
import csv
import os
import re
from datetime import datetime

JSON_FAYL = "kontaktlar.json"
LOG_FAYL = "log.txt"

class Contact:
    """Kontakt ma'lumotlarini saqlash uchun klass"""
    def __init__(self, ism: str, telefon: str, email: str = "", manzil: str = ""):
        self.validate(ism, telefon)
        self.ism = ism.strip()
        self.telefon = telefon.strip()
        self.email = email.strip()
        self.manzil = manzil.strip()

    @staticmethod
    def validate(ism: str, telefon: str):
        """Ism va telefon raqamini qat'iy tekshirish (Validatsiya)"""
        if not ism or not ism.strip():
            raise ValueError("Xatolik: Ism bo'sh bo'lishi mumkin emas!")
        
        # Telefon raqami formati: faqat raqamlar yoki + belgisi bilan boshlanishi kerak (kamida 7 ta belgi)
        tel_pattern = r"^\+?[0-9]{7,15}$"
        if not re.match(tel_pattern, telefon.strip()):
            raise ValueError("Xatolik: Telefon raqami formati noto'g'ri! (Faqat raqamlar yoki + bilan boshlanishi kerak)")

    def to_dict(self) -> dict:
        """Kontaktni lug'at ko'rinishiga o'tkazish"""
        return {
            "ism": self.ism,
            "email": self.email,
            "manzil": self.manzil
        }

    def __str__(self) -> str:
        return f"👤 {self.ism} | 📞 {self.telefon} | 📧 {self.email or 'Kiritilmagan'} | 📍 {self.manzil or 'Kiritilmagan'}"


class ContactBook:
    """Kontaktlar kitobini boshqarish klassi"""
    def __init__(self):
        self.kontaktlar = {}  # Kalit: telefon raqami, Qiymat: {ism, email, manzil}
        self.yuklash()

    def _log_yoz(self, amal: str, xabar: str):
        """Amallarni vaqt bilan birga log.txt fayliga qayd etish"""
        vaqt = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        try:
            with open(LOG_FAYL, "a", encoding="utf-8") as f:
                f.write(f"[{vaqt}] AMAL: {amal} | {xabar}\n")
        except IOError:
            print("⚠️ Log fayliga yozishda muammo yuz berdi.")

    def yuklash(self):
        """Fayldan ma'lumotlarni try/except orqali xavfsiz yuklash"""
        try:
            if os.path.exists(JSON_FAYL):
                with open(JSON_FAYL, "r", encoding="utf-8") as f:
                    self.kontaktlar = json.load(f)
            else:
                self.kontaktlar = {}
        except (json.JSONDecodeError, IOError) as e:
            print(f"⚠️ Faylni yuklashda xatolik yuz berdi ({e}). Bo'sh kontaktlar kitobi yaratildi.")
            self.kontaktlar = {}

    def saqlash(self):
        """Ma'lumotlarni JSON faylga saqlash"""
        try:
            with open(JSON_FAYL, "w", encoding="utf-8") as f:
                json.dump(self.kontaktlar, f, ensure_ascii=False, indent=4)
        except IOError as e:
            print(f"⚠️ Ma'lumotlarni saqlashda xatolik yuz berdi: {e}")

    def qoshish(self, kontakt: Contact) -> bool:
        """Yangi kontakt qo'shish"""
        if kontakt.telefon in self.kontaktlar:
            print(f"⚠️ '{kontakt.telefon}' raqami allaqachon '{self.kontaktlar[kontakt.telefon]['ism']}' nomi bilan ro'yxatda bor.")
            return False
        
        self.kontaktlar[kontakt.telefon] = kontakt.to_dict()
        self.saqlash()
        self._log_yoz("Qo'shish", f"KONTAKT: {kontakt.ism} ({kontakt.telefon}) muvaffaqiyatli qo'shildi.")
        return True

    def ochirish(self, telefon: str) -> bool:
        """Kontaktni telefon raqami bo'yicha o'chirish"""
        if telefon in self.kontaktlar:
            ism = self.kontaktlar[telefon]['ism']
            del self.kontaktlar[telefon]
            self.saqlash()
            self._log_yoz("O'chirish", f"KONTAKT: {ism} ({telefon}) o'chirildi.")
            return True
        return False

    def qidirish(self, kalit_soz: str) -> list:
        """Ism, telefon yoki email bo'yicha qidirish"""
        kalit_soz = kalit_soz.lower().strip()
        natijalar = []
        
        for tel, info in self.kontaktlar.items():
            if (kalit_soz in tel) or (kalit_soz in info['ism'].lower()) or (kalit_soz in info['email'].lower()):
                obj = Contact(info['ism'], tel, info['email'], info['manzil'])
                natijalar.append(obj)
        return natijalar

    def yangilash(self, telefon: str, yangi_ism: str, yangi_email: str, yangi_manzil: str) -> bool:
        """Mavjud kontakt ma'lumotlarini yangilash"""
        if telefon not in self.kontaktlar:
            return False
        
        # Validatsiyadan o'tkazish
        Contact.validate(yangi_ism, telefon)
        
        self.kontaktlar[telefon] = {
            "ism": yangi_ism.strip(),
            "email": yangi_email.strip(),
            "manzil": yangi_manzil.strip()
        }
        self.saqlash()
        self._log_yoz("Yangilash", f"KONTAKT: {yangi_ism} ({telefon}) ma'lumotlari yangilandi.")
        return True

    def list_all(self):
        """Barcha kontaktlarni konsolga chiqarish"""
        if not self.kontaktlar:
            print("📭 Kontaktlar kitobi hozircha bo'sh.")
            return
        
        print(f"\n--- JAMI KONTAKTLAR ({len(self.kontaktlar)} ta) ---")
        for tel, info in self.kontaktlar.items():
            print(f"👤 {info['ism']} | 📞 {tel} | 📧 {info['email'] or '-'} | 📍 {info['manzil'] or '-'}")

    def eksport_csv(self, csv_fayl_nomi="kontaktlar.csv"):
        """Bonus: Barcha ma'lumotlarni CSV faylga eksport qilish"""
        if not self.kontaktlar:
            print("⚠️ Eksport qilish uchun kontaktlar mavjud emas.")
            return
        
        try:
            with open(csv_fayl_nomi, "w", newline="", encoding="utf-8") as f:
                writer = csv.writer(f)
                # Sarlavhalar
                writer.writerow(["Ism", "Telefon", "Email", "Manzil"])
                # Ma'lumotlar
                for tel, info in self.kontaktlar.items():
                    writer.writerow([info['ism'], tel, info['email'], info['manzil']])
            
            print(f"📥 Ma'lumotlar muvaffaqiyatli '{csv_fayl_nomi}' fayliga eksport qilindi!")
            self._log_yoz("Eksport", f"Barcha kontaktlar {csv_fayl_nomi} fayliga eksport qilindi.")
        except IOError as e:
            print(f"⚠️ CSV faylga yozishda xatolik yuz berdi: {e}")


def main_menu():
    """Menu Pattern orqali CLI Interfeys (UI)"""
    kitob = ContactBook()
    
    while True:
        print("\n" + "="*40)
        print("       📚 KONTAKTLAR KITOBI UI         ")
        print("="*40)
        print("1. 👤 Yangi kontakt qo'shish")
        print("2. 🔍 Kontakt qidirish")
        print("3. 🗑️ Kontaktni o'chirish")
        print("4. 🔄 Kontaktni yangilash")
        print("5. 📋 Barcha kontaktlarni ko'rish")
        print("6. 📥 CSV formatga eksport qilish")
        print("7. ❌ Chiqish")
        print("="*40)
        
        tanlov = input("Amalni tanlang (1-7): ").strip()
        
        if tanlov == "1":
            print("\n--- 👤 Yangi Kontakt Qo'shish ---")
            ism = input("Ismni kiriting: ")
            tel = input("Telefon raqamini kiriting (Masalan: +998901234567): ")
            email = input("Emailni kiriting (ixtiyoriy): ")
            manzil = input("Manzilni kiriting (ixtiyoriy): ")
            
            try:
                # Validatsiya Contact yaratilayotganda ishlaydi
                yangi_kontakt = Contact(ism, tel, email, manzil)
                if kitob.qoshish(yangi_kontakt):
                    print("✅ Kontakt muvaffaqiyatli qo'shildi!")
            except ValueError as e:
                print(f"❌ {e}")
                kitob._log_yoz("Xatolik", f"Validatsiyadan o'tmadi. Ism: '{ism}', Tel: '{tel}'")

        elif tanlov == "2":
            print("\n--- 🔍 Kontakt Qidirish ---")
            kalit = input("Qidiruv kalit so'zini kiriting (Ism, Tel yoki Email): ")
            natijalar = kitob.qidirish(kalit)
            if natijalar:
                print(f"\n🔍 {len(natijalar)} ta mos kontakt topildi:")
                for k in natijalar:
                    print(k)
            else:
                print("❌ Hech qanday kontakt topilmadi.")

        elif tanlov == "3":
            print("\n--- 🗑️ Kontaktni O'chirish ---")
            tel = input("O'chiriladigan kontaktning telefon raqamini kiriting: ")
            if kitob.ochirish(tel):
                print("🗑️ Kontakt muvaffaqiyatli o'chirildi.")
            else:
                print("❌ Bunday telefon raqamli kontakt topilmadi.")

        elif tanlov == "4":
            print("\n--- 🔄 Kontaktni Yangilash ---")
            tel = input("Yangilanadigan kontaktning telefon raqamini kiriting: ")
            if tel in kitob.kontaktlar:
                print(f"Joriy ma'lumotlar: {kitob.kontaktlar[tel]['ism']}")
                yangi_ism = input("Yangi ism kiriting: ")
                yangi_email = input("Yangi email kiriting: ")
                yangi_manzil = input("Yangi manzil kiriting: ")
                
                try:
                    if kitob.yangilash(tel, yangi_ism, yangi_email, yangi_manzil):
                        print("✅ Kontakt muvaffaqiyatli yangilandi!")
                except ValueError as e:
                    print(f"❌ {e}")
            else:
                print("❌ Bunday telefon raqamli kontakt topilmadi.")

        elif tanlov == "5":
            kitob.list_all()

        elif tanlov == "6":
            kitob.eksport_csv()

        elif tanlov == "7":
            print("👋 Dastur tugatildi. Kuningiz xayrli o'tsin!")
            break
        else:
            print("❌ Noto'g'ri buyruq! 1 dan 7 gacha bo'lgan raqamlardan birini tanlang.")

if __name__ == "__main__":
    main_menu()
Kod qanday talablarni qondirdi?
Validatsiya va istisnolar (raise + except): Agar foydalanuvchi ismni bo'sh qoldirsa yoki telefon raqamiga harflar aralashtirib yuborsa, Contact.validate() buni aniqlab ValueError beradi, Menu interfeysi esa xatolikni tutib olib foydalanuvchiga chiroyli bildirishnoma ko'rsatadi.

Log tizimi (log.txt): Har bir muvaffaqiyatli bajarilgan amal (yoki validatsiya xatosi) vaqt ko'rsatkichi bilan faylga yozib boriladi.

Fayllar xavfsizligi (try/except): kontaktlar.json yuklanayotganda uning formati buzilgan bo'lsa yoki tasodifan fayl o'qilmay qolsa, dastur qulab tushmaydi, balki bo'sh baza bilan ishni xavfsiz davom ettiradi.

Bonus Eksport: csv moduli yordamida barcha kontaktlarni bitta tugma bilan Excel formati (.csv) ko'rinishiga o'tkazish imkoniyati qo'shildi.
