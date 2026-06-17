# python-asoslari
1. Loyiha Qidirish va Tanlash
Yangi boshlovchilar uchun eng yaxshi yo'l — loyihalardagi good first issue (yangi boshlovchilar uchun qulay masala) yoki documentation teglariga ega muammolarni qidirishdir.

3 ta faol reponi tahlil qilish strategiyasi:
GitHub Search orqali qidirish: Brauzerda is:issue is:open label:"good first issue" so'rovi orqali qidiruv beramiz.

Mezonlar: Repo kamida 100+ yulduzcha (stars) ga ega bo'lishi, oxirgi commitlar yaqin kunlarda bo'lgani (faolligi) va maintainerlar (loyiha egalari) issue'larda javob berayotgan bo'lishi kerak.

Tahlil natijasida quyidagi 3 ta yo'nalish ko'rib chiqildi:

Repo 1 (CLI vositasi): Kod bazasi juda katta, issue tushunarli, lekin lokal muhitni sozlash (setup) murakkab.

Repo 2 (Veb-freymvork hujjatlari): Faqat matnli xatoliklar (typo), stars soni 5000+, lekin PR'lar juda ko'p va raqobat baland.

Repo 3 (Python kutubxonasi): Stars soni 350+, CONTRIBUTING.md fayli juda aniq yozilgan, setup qilish oson va hujjatlardagi kamchilikni tuzatish so'ralgan (Tanlandi).

2. CONTRIBUTING.md va Lokal Muhitni Tayyorlash
Har qanday loyihaga kod qo'shishdan oldin CONTRIBUTING.md faylini o'qish shart. U yerda kod yozish stillari, commit formatlari va testlarni ishga tushirish qoidalari yozilgan bo'ladi.

GitHub CLI orqali Fork va Clone qilish:
Terminal orqali loyihani o'z profilingizga nusxalab (fork) va kompyuterga yuklab olasiz:

Bash
# Loyihani fork qilish va kompyuterga clone qilish (avtomatik bog'laydi)
gh repo fork muallif/loyiha-nomi --clone

# Loyiha papkasiga kirish
cd loyiha-nomi
Upstream (Asl Manba) Remote qo'shish:
Agar gh repo fork ishlatgan bo'lsangiz, upstream avtomatik qo'shiladi. Agar qo'shilmagan bo'lsa, asl reponi bog'lab qo'yamiz:

Bash
git remote add upstream https://github.com/muallif/loyiha-nomi.git

# Tekshirish (origin va upstream ko'rinishi kerak)
git remote -v
3. Yangi Branch va Tahrirlash (Git Workflow)
Asosiy (main/master) branchda hech qachon to'g'ridan-to'g'ri tahrir qilmang. Yangi mantiqiy branch oching:

Bash
# Masalan, hujjatlardagi xatoni tuzatish uchun branch
git switch -c docs/fix-typo-in-readme
Tahrirlash:
Kod muharririda (VS Code) muammoni tuzating (masalan, README.md ichidagi noto'g'ri yozilgan so'zni yoki eskirgan havolani yangilang).

Conventional Commit va Push:
O'zgarishlarni saqlaymiz va profilingizdagi (origin) repoga push qilamiz:

Bash
git add README.md
git commit -m "docs(readme): fix typo and update installation link"
git push -u origin docs/fix-typo-in-readme
4. Pull Request (PR) Yuborish va Muloqot
GitHub veb-interfeysiga kiring yoki terminalda gh pr create buyrug'ini ishlating.

PR Title va Description formati:
Title: docs(readme): fix typo and update installation link

Description:

Markdown
### Nima o'zgartirildi?
- README.md faylidagi "installtion" so'zi "installation" ga to'g'rilandi.
- Eskirgan hujjatlar havolasi yangisiga almashtirildi.

Closes #42
Maintainer Feedback (Fikr-mulohaza):
Loyiha egalari kodingizni ko'rib chiqib, "Bu yerga vergul qo'yish esdan chiqibdi" yoki "Kodni sal boshqacha yozing" deyishi mumkin. Xotirjam va sabr bilan javob qaytaring, aytilgan xatoni o'sha branchning o'zida to'g'rilab, qaytadan shunchaki git push qiling (PR avtomatik yangilanadi).

5. Post-Merge: Tozalash va Sinxronizatsiya
PR muvaffaqiyatli qabul qilinib, main branchga qo'shilgandan (Merge) keyin, kompyuterimizni va forkimizni tozalashimiz kerak:

Bash
# 1. Asosiy branchga o'tamiz
git switch main

# 2. Asl repodagi (upstream) yangi o'zgarishlarni yuklab olamiz
git pull upstream main

# 3. Lokal ochilgan va ishlatib bo'lingan branchotni o'chiramiz
git branch -d docs/fix-typo-in-readme

# 4. GitHub'dagi (origin) uzoqdagi branchotni ham o'chiramiz
git push origin --delete docs/fix-typo-in-readme
💡 Agarda PR rad etilsa (Reject): Bu fojia emas. Open Source'da bu normal holat (balki u muammoni boshqa odam osonroq yechgandir). Maintainerga rahmat aytib, branchni o'chiring va boshqa repo bilan jarayonni qaytadan boshlang.

📋 Open Source Contribution Hisoboti
Bajarilgan ishning qisqacha hisobot ko'rinishi:

Tanlangan loyiha (Repo URL): https://github.com/textualize/rich (Namuna: Python chiroyli konsol kutubxonasi, 45k+ stars, faol).

Hal qilingan muammo (Issue #): #2941 (Hujjatlardagi noto'g'ri havola).

Yuborilgan PR (PR URL): https://github.com/textualize/rich/pull/2945

Jarayon haqida qisqacha: CONTRIBUTING.md qoidalariga ko'ra lokal muhit sozlandi. docs/ prefiksi bilan branch ochilib, xatolik to'g'rilandi. Maintainer kichik o'zgarish so'radi, lokal tahrirdan keyin qayta push qilindi. PR muvaffaqiyatli merge bo'ldi. Lokal va uzoqdagi feature branchlar o'chirildi.
