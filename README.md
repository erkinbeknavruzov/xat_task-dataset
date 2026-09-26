# Xat-Task Dataset

O'zbekistondagi rasmiy xat-hujjatlardan topshiriqlarni aniqlash, ularning mazmuni, ijrochisi va muddatini ajratib olish bo'yicha test dataset.

## Maqsad

Dataset quyidagi vazifalarni ishlab chiqish va baholash uchun mo'ljallangan:

- hujjatda topshiriq mavjud yoki mavjud emasligini aniqlash;
- topshiriqning hujjatdagi manba bandi yoki ilovasini topish;
- topshiriq mazmunini ajratish;
- ijrochi va hamijrochini aniqlash;
- muddatni aniqlash va normallashtirish;
- band, kichik band va ilovalar orasidagi bog'lanishlarni aniqlash;
- scan PDF hujjatlarda OCR asosida matn olish.

Dataset rivojlantirib boriladi va yangi hujjatlar hamda annotatsiyalar bilan muntazam to'ldiriladi.

## Fayllar tuzilishi

Har bir hujjat imkon qadar bir xil ID bilan juftlanadi:

```text
Xat_<ID>.pdf
Task_<ID>.txt
```

Misol:

```text
Xat_4501.pdf
Task_4501.txt
```

Tavsiya etilgan katalog:

```text
data/
├── Xat_1.pdf
├── Task_1.txt
├── Xat_2.pdf
├── Task_2.txt
└── ...
```

## Task annotatsiyasi

Task fayllari quyidagi ko'rinishda saqlanadi:

```text
1-topshiriq:
topshiriq: <hujjatdagi band/ilova/reference>
mazmuni: <topshiriqning mazmuni>
ijrochi: <ijrochi yoki null>
muddati: <muddat yoki null>
```

Bir hujjatda bir nechta topshiriq bo'lishi mumkin.

Agar hujjatda topshiriq mavjud bo'lmasa:

```text
no tasks
```

## Maydonlar

| Maydon | Tavsif |
|---|---|
| `topshiriq` | Topshiriq joylashgan band, kichik band, ilova yoki boshqa reference |
| `mazmuni` | Topshiriqning asosiy matni |
| `ijrochi` | Asosiy ijrochi yoki ijrochilar |
| `muddati` | Topshiriq bajarilish muddati |

## Hujjat turlari

Datasetda turli ko'rinishdagi hujjatlar bo'lishi mumkin:

- text-layer PDF;
- scan PDF;
- mixed PDF;
- jadval va ilovali hujjatlar.

Scan PDFlar uchun OCR talab qilinadi. Loyihada asosiy OCR vositasi sifatida Tesseractdan foydalanish ko'zda tutilgan.

## Tillar

Hujjatlarda quyidagi tillar va yozuvlar uchrashi mumkin:

- o'zbek tili — lotin yozuvi;
- o'zbek tili — kirill yozuvi;
- rus tili;
- aralash matn.

## Kutilayotgan ishlov berish pipeline'i

```text
PDF
 ↓
Page analysis
 ↓
Native text / Tesseract OCR
 ↓
Normalization
 ↓
Document structure recovery
 ↓
Reference detection & resolution
 ↓
Relevance classification
 ↓
Task detection
 ↓
Executor extraction
 ↓
Deadline extraction
 ↓
Structured result
```

## Reference holatlari

Topshiriq mazmuni va unga tegishli metadata turli bloklarda joylashishi mumkin.

Misollar:

```text
1-ilovaning 6-bandida nazarda tutilgan vazifalar
4-bandining 2-xatboshisida
13-bandining (v) kichik bandida
yuqorida ko'rsatilgan topshiriqlar
```

Shuning uchun topshiriqlar faqat alohida abzats bo'yicha emas, hujjat strukturasi va bloklar orasidagi bog'lanishlar bilan birga tahlil qilinadi.

## Dataset holati

Dataset hozircha test va prototiplash bosqichida.

Joriy versiyada:

- positive va `no tasks` hujjatlar mavjud;
- scan PDFlar salmoqli ulushni tashkil qiladi;
- task va deadline annotatsiyalari mavjud;
- executor annotatsiyalari hali barcha yozuvlarda to'liq emas;
- dataset kengaytirib boriladi.

## Yangi ma'lumot qo'shish

Yangi hujjat qo'shilganda mos juftlik yaratiladi:

```text
Xat_5001.pdf
Task_5001.txt
```

So'ng:

```bash
git add .
git commit -m "Add document 5001"
git push
```

## Ma'lumotlar xavfsizligi

Public repositoryga fayl joylashtirishdan oldin hujjatlarda tarqatilishi cheklangan, maxfiy yoki shaxsiy ma'lumotlar mavjud emasligini tekshirish kerak.

## Status

Work in progress. Dataset yangi real hujjatlar va ekspert annotatsiyalari bilan bosqichma-bosqich kengaytiriladi.
