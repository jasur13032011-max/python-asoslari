# python-asoslari
Python
# Dastur tavsifi: Ushbu dastur terminal konsolida maxsus belgilar yordamida 
# chiroyli bezatilgan va turli parametrlardan (sep, end) foydalanilgan 
# vizual "Git Cheat Sheet" (Git bo'yicha qisqa eslatma) xabarini chiqaradi.

# 1. Bosh sarlavha (Katta bezak bilan)
print("=" * 45)
print("*" * 12, "GIT CHEAT SHEET", "*" * 12)
print("=" * 45)

# 2. Alohida bo'lim ko'rsatish (sep parametri bilan)
print("1", "Lokal sozlamalar", sep=" -> ")
print("-" * 30)

# 3. end parametri yordamida ma'lumotlarni ketma-ket chiqarish
print("Repository yaratish: ", end="")
print("git init")

# 4. Yana bir nechta foydali buyruqlar va yakuniy bezak
print("Statusni tekshirish: git status")
print("O'zgarishlarni saqlash: git commit -m 'xabar'")
print("=" * 45)
