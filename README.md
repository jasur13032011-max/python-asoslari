# python-asoslari
Ochiq manbali (Open Source) loyihalarga hissa qo'shish — dasturchi sifatida o'sishning eng samarali usullaridan biri. Quyida siz keltirgan reja asosida jarayonni bosqichma-bosqich qanday amalga oshirish bo'yicha batafsil qo'llanma va yakuniy hisobot topshirish uchun shablon tayyorlab berdim.

1-bosqich: Repozitoriyani qidirish va tanlash
"Good first issue" yorlig'iga ega, 100 dan ortiq yulduzcha (star) yig'gan va faol loyihalarni topish uchun GitHub qidiruv tizimidan foydalanamiz.

Tavsiya etilgan 3 ta repo turi (Tahlil):
Kutubxonalar (Libraries): Masalan, mashhur dasturlash tillaridagi utilitlar. Ularda hujjatlar (documentation) juda ko'p bo'ladi.

CLI vositalari (Command Line Tools): Kod strukturasi odatda tushunarli bo'ladi.

O'quv loyihalari (Awesome lists / Tutorials): Dastlabki tajriba uchun juda qulay.

Qidiruv filtri (GitHub qidiruv satriga yozish uchun):
is:issue is:open label:"good first issue" stars:>100

2-bosqich: Texnik jarayon (Git va GitHub)
Loyiha tanlangandan so'ng, quyidagi buyruqlar ketma-ketligi orqali ishni boshlaymiz. O'zgarish kiritishdan oldin CONTRIBUTING.md faylini albatta o'qib chiqing!

1. Fork va Clone qilish
Loyiha sahifasida "Fork" tugmasini bosing yoki GitHub CLI orqali bajaring:

Bash
gh repo fork <original-repo-url> --clone
2. Upstream bog'lash (Sinxronizatsiya uchun)
Loyiha papkasiga kirib, asl repozitoriyani upstream sifatida qo'shing:

Bash
git remote add upstream <original-repo-url>
# Tekshirish uchun:
git remote -v
3. Yangi Branch ochish
Asosiy (main yoki master) branchda kod yozmang. Doim yangi branch oching:

Bash
# Hujjatlardagi xatolik (typo) uchun:
git checkout -b docs/fix-typo-in-readme

# Kichik kod tuzatish uchun:
git checkout -b fix/resolve-null-pointer
4. Kodni o'zgartirish va Commit (Conventional Commits)
O'zgarishlarni kiritgach, tushunarli commit xabari yozing:

Bash
git add .
git commit -m "docs(readme): fix typo in installation guide"
Format: <type>(<scope>): <short description>

5. Push va Pull Request (PR)
O'zgarishni o'zingizning fork qilingan repongizga yuklang:

Bash
git push origin docs/fix-typo-in-readme
GitHub sahifangizga kiring va "Compare & pull request" tugmasini bosing.

PR sarlavhasi va tavsifi:

Title: docs(readme): fix typo in installation guide

Description: This PR fixes a small typo in the installation section of the README.md.

Closes: Closes #123 (Agar muayyan issue'ga tegishli bo'lsa)

3-bosqich: PR'dan keyingi jarayon
Feedback (Fikr-mulohaza): Maintainer loyihaga qarab kodni o'zgartirishni so'rashi mumkin. Sabr bilan, muloyimlik bilan javob bering va so'ralgan tuzatishlarni o'sha branchning o'zida qilib, qayta push qiling.

Merge bo'lgandan keyin (Tozalash):

Bash
git checkout main
git fetch upstream
git merge upstream/main
git push origin main
git branch -d docs/fix-typo-in-readme
Agar rad etilsa (Reject): Xafa bo'lish yo'q! Bu normal holat. Sababini tushunishga harakat qiling va boshqa loyihada qaytadan urinib ko'ring.

4-bosqich: Hisobot (Shablon)
Vazifani topshirish yoki o'zingiz uchun qayd etib borish uchun quyidagi tayyor shablondan foydalanishingiz mumkin:

Open Source Contribution Hisoboti
Tanlangan loyiha (Repo URL): https://github.com/owner/repository_name

Yuborilgan PR (PR URL): https://github.com/owner/repository_name/pull/X

Jarayon haqida qisqacha hisobot (O'z-o'zini baholash):
Mezon	Berilgan ball	Izoh / Sabab
1. Repo tanlash va tahlil	20 / 20	100+ star bo'lgan, faol va good first issue tegiga ega loyiha to'g'ri tanlandi.
2. Qoidalarga rioya qilish	20 / 20	CONTRIBUTING.md to'liq o'qildi, loyiha formatlash qoidalariga rioya qilindi.
3. Git va Branch boshqaruvi	20 / 20	Fork qilindi, upstream ulandi, nomlanish qoidasiga mos alohida branch ochildi.
4. Commit va PR sifati	20 / 20	Conventional Commits ishlatildi. PR tavsifi aniq yozilib, tegishli Issue'ga bog'landi (Closes #N).
5. Kommunikatsiya va Yakun	20 / 20	Maintainer feedback'iga to'g'ri javob berildi / branchlar o'z vaqtida tozalandi.
YAKUNIY NATIJA	100 / 100	Jarayon muvaffaqiyatli yakunlandi!
