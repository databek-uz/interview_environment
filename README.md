# Spark Interview Environment

Bu repository Apache Spark bilan intervyu savollarini echish uchun tayyor development environment ni taqdim etadi.

## 🚀 Xususiyatlar

- **Apache Spark 3.5.1** - To'liq o'rnatilgan va sozlangan
- **Python 3.11** - Zamonaviy Python versiyasi
- **Jupyter Notebook** - Interaktiv dasturlash uchun
- **PySpark** - Python API for Spark
- **Data Science kutubxonalari**: pandas, numpy, pyarrow, matplotlib
- **VS Code Extensions**: Python, Jupyter, Material Icon Theme

## 📋 Talablar

- GitHub Codespaces yoki
- VS Code + Remote Containers extension
- Docker Desktop (lokal ishlatish uchun)

## 🔧 Ishga tushirish

### GitHub Codespaces orqali (Tavsiya etiladi)

1. Ushbu repository ni oching
2. `Code` tugmasini bosing
3. `Codespaces` tabini tanlang
4. `Create codespace on main` tugmasini bosing
5. **Sabr qiling**: Birinchi build 5-10 daqiqa oladi
   - Apache Spark (~400MB) yuklab olinadi - progress bar ko'rinadi
   - Python packages o'rnatiladi
   - Extensions yuklanadi
   - Keyingi safar cache ishlatiladi va tezroq bo'ladi!

### VS Code Remote Containers orqali

1. Repository ni clone qiling:
   ```bash
   git clone <repository-url>
   cd interview_environment
   ```

2. VS Code da ochish:
   ```bash
   code .
   ```

3. VS Code quyidagi xabarni ko'rsatadi: "Folder contains a Dev Container configuration file"
4. "Reopen in Container" tugmasini bosing
5. Container build bo'lguncha kuting

## 📚 Qanday ishlatiladi

### Spark versiyasini tekshirish

```bash
spark-submit --version
```

### PySpark shell ni ishga tushirish

```bash
pyspark
```

### Python script ni Spark bilan ishlatish

```python
from pyspark.sql import SparkSession

# Spark session yaratish
spark = SparkSession.builder \
    .appName("Interview Practice") \
    .master("local[*]") \
    .getOrCreate()

# Misol: DataFrame yaratish
data = [("Alice", 34), ("Bob", 45), ("Charlie", 23)]
df = spark.createDataFrame(data, ["name", "age"])
df.show()

# Session ni yopish
spark.stop()
```

### Jupyter Notebook ishlatish

1. Terminal ni oching
2. Jupyter ni ishga tushiring:
   ```bash
   jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser
   ```
3. VS Code avtomatik ravishda port forwarding qiladi
4. Notification da ko'rsatilgan URL ni oching

Yoki VS Code ichida:
1. `.ipynb` fayl yarating
2. Kernel sifatida `spark-env` ni tanlang
3. Kod yozishni boshlang!

## 🎯 Interview Mashq Qilish

### Oddiy misollar

```python
# 1. Word Count - Classic Spark misol
text_data = ["hello world", "hello spark", "spark is great"]
rdd = spark.sparkContext.parallelize(text_data)
word_counts = rdd.flatMap(lambda line: line.split()) \
                 .map(lambda word: (word, 1)) \
                 .reduceByKey(lambda a, b: a + b)
word_counts.collect()

# 2. DataFrame operatsiyalari
from pyspark.sql.functions import col, avg, count

df = spark.createDataFrame([
    ("Alice", "Sales", 50000),
    ("Bob", "IT", 60000),
    ("Charlie", "Sales", 55000),
    ("David", "IT", 65000)
], ["name", "department", "salary"])

# Department bo'yicha o'rtacha maosh
df.groupBy("department").agg(avg("salary").alias("avg_salary")).show()
```

## 🛠️ O'rnatilgan kutubxonalar

- `pyspark==3.5.1` - Apache Spark Python API
- `pandas` - Data manipulation
- `numpy` - Numerical computing
- `pyarrow` - Arrow format support
- `jupyter` - Interactive notebooks
- `ipykernel` - Jupyter kernel
- `matplotlib` - Data visualization
- `debugpy` - Python debugging
- `findspark` - Spark initialization helper

## 🐛 Debugging

VS Code debugger ishlatish uchun:

1. `.py` faylda breakpoint qo'ying (F9)
2. Debug panelni oching (Ctrl+Shift+D)
3. "Python: Current File" ni tanlang
4. F5 ni bosing

## ⚙️ Environment Variables

Container quyidagi environment variablelarni o'rnatadi:

- `SPARK_HOME=/opt/spark`
- `JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64`
- `PYSPARK_PYTHON=python3`

## 📝 Maslahatlar

1. **Memory Management**: Lokal rejimda Spark default ravishda barcha CPU core larni ishlatadi (`local[*]`)
2. **Caching**: Bir xil ma'lumotni ko'p marta ishlatayotgan bo'lsangiz `.cache()` yoki `.persist()` dan foydalaning
3. **Lazy Evaluation**: Spark lazy evaluation ishlatadi - action chaqirilguncha hech narsa bajarilmaydi
4. **DataFrame vs RDD**: Zamonaviy Spark loyihalarda DataFrame API tavsiya etiladi

## 🔍 Muammolarni hal qilish

### Container build qolayapti

Agar build stuck bo'lib qolsa:
1. **Sabr qiling** - Spark fayl katta (~400MB), yuklanishi 3-5 daqiqa oladi
2. Progress bar ko'rinishi kerak - agar ko'rinmasa:
   - Container log larini tekshiring
   - Build ni cancel qilib, qayta boshlang
3. Internet connection tekshiring

### Spark session yaratilmayapti
```python
# findspark dan foydalaning
import findspark
findspark.init()

from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[*]").getOrCreate()
```

### Java topilmayapti
```bash
# Java versiyasini tekshiring
java -version
echo $JAVA_HOME
```

### Port band bo'lsa
```bash
# Boshqa port ishlatish
jupyter notebook --ip=0.0.0.0 --port=8889 --no-browser
```

## 📖 Qo'shimcha Resurslar

- [Apache Spark Documentation](https://spark.apache.org/docs/latest/)
- [PySpark API Reference](https://spark.apache.org/docs/latest/api/python/)
- [Spark by Examples](https://sparkbyexamples.com/)

## 🤝 Hissa qo'shish

Agar muammolarni topsangiz yoki yaxshilashlar bo'lsa, issue ochishingiz mumkin.

## 📄 License

MIT License

---

**Muvaffaqiyat tilaymiz interview'da! 🎉**