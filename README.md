# apache-beam---CMPE-255-Assignment

**Goal**  
Demonstrate core Apache Beam features on a small clickstream sample: **pipeline I/O, Map, Filter, ParDo (with side output), composite transform, partition, windowing** (fixed windows, event time).

**Demo video**  
▶️ https://youtu.be/GkJHZx0rGlc

---

## Dataset

**Name:** e-Shop Clickstream “e-shop clothing 2008”  
**Source (Kaggle):** https://www.kaggle.com/datasets/arashnic/e-shop-clickstream-dataset

**Fields used:**  
`year`, `month`, `day`, `order`, `country`, `session ID`, `page 1 (main category)`, `page 2 (clothing model)`, `price`, `price 2`, `page`

**Note:** I create a small JSONL sample with a proper timestamp (`ts`) for event-time windowing.

**Suggested citation (from dataset docs):**  
> Łapczyński M., Białowąs S. (2013). *Discovering Patterns of Users' Behaviour in an E-shop – Comparison of Consumer Buying Behaviours in Poland and Other European Countries*, **Studia Ekonomiczne**, 151.

---

## What this pipeline does

1. **Create sample JSONL** from the CSV with the columns above + derived `ts`.  
2. **Map & Filter:** parse, normalize a couple of fields, keep valid rows.  
3. **ParDo:** custom validator with **side output** for invalid events.  
4. **Composite transform:** bundle parse → normalize → validate.  
5. **Partition:** split by price (**high / low / missing**).  
6. **Windowing:** attach event time and aggregate counts per **category** in **60-second fixed windows**.  
7. **Write outputs:** per-stage results to disk.

---

## How to run (Colab)

1. Open `notebooks/Apache_beam.ipynb` in Google Colab.  
2. Mount Drive and set the CSV path (folder: **e-Shop Click Dataset**).  
3. Run cells in order:
   - **Stage 1:** preview data  
   - **Stage 2:** build JSONL sample  
   - **Stage 4:** Map/Filter  
   - **Stage 5:** ParDo + side output  
   - **Stage 6:** Composite transform  
   - **Stage 7:** Partition  
   - **Stage 8:** Windowing + write outputs

---

## License & acknowledgments

Data belongs to the original authors and Kaggle dataset maintainers—use under their terms.  
This repo is for an academic assignment demonstrating Apache Beam features.
