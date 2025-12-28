# Yemek Tarifleri Chatbot

**Retrieval-Augmented Generation (RAG) Tabanlı Türkçe Yemek Tarifi Asistanı**

## Proje Tanımı

**Yemek Tarifleri Chatbot**, Türkçe yemek tarifleri alanında çalışan, **RAG (Retrieval-Augmented Generation)** mimarisiyle geliştirilmiş bir sohbet botudur.
Sistem, büyük dil modelinin (LLM) doğrudan uydurma yapmasını engelleyerek, **yalnızca tarif veri setinde bulunan bilgilerle** cevap üretir.

Bu yaklaşım sayesinde chatbot:

* Güvenilir
* Tekrarlanabilir
* Akademik olarak savunulabilir
  bir yapı sunar.

---

## Amaç ve Motivasyon

Klasik LLM tabanlı chatbot’lar:

* Olmayan tarifleri uydurabilir
* Yanlış malzeme veya süre bilgisi verebilir
* Kaynaksız ve doğrulanamaz cevaplar üretebilir

Bu proje, bu sorunları çözmek için:

* **Vektör tabanlı bilgi getirme (FAISS)**
* **Katı kural tabanlı guardrail mekanizmaları**
* **Deterministik cevaplama stratejisi**
  kullanır.

Amaç, **“mutfakta gerçekten kullanılabilir”** bir yapay zeka sistemi oluşturmaktır.

---

##  Kullanılan Teknolojiler

| Bileşen                  | Açıklama                       |
| ------------------------ | ------------------------------ |
| **RAG**                  | Retrieval-Augmented Generation |
| **FAISS**                | Vektör tabanlı benzerlik arama |
| **SentenceTransformers** | Metin embedding                |
| **Qwen2.5-3B-Instruct**  | Büyük dil modeli (LLM)         |
| **Regex Guardrails**     | Güvenli sorgu kontrolü         |
| **Python**               | Ana geliştirme dili            |
| **HuggingFace Datasets** | Tarif veri seti                |

---

##  Sistem Mimarisi

```
Kullanıcı Sorusu
      │
      ▼
Regex Guardrails (niyet analizi)
      │
      ▼
Tarif Adı Ayrıştırma & Normalize
      │
      ▼
Embedding (SentenceTransformers)
      │
      ▼
FAISS Vektör Arama
      │
      ▼
Skor & Belirsizlik Kontrolü
      │
      ├── Tarif Yok → “Bu tarif veri setimde bulunmuyor. & Benzer tarifler üzerinden ilerlenebilir.”
      │
      └── Tarif Var
             │
             ▼
     (Gerekirse) LLM ile Açıklama
             │
             ▼
          Cevap
```

---

##  Güvenlik ve Guardrail Mantığı

Sistem, LLM’i **her zaman kullanmaz**.

Aşağıdaki durumlarda LLM **bilerek devre dışı bırakılır**:

*   **Pişirme süresi / derece soruları**
*   **Kaç kişilik / porsiyon soruları**
*   **Veri setinde olmayan tarifler**
*   **Belirsiz eşleşmeler**

Bu gibi durumlarda chatbot:

* Sabit, deterministik mesajlar döner
* Tahmin yapmaz
* Kullanıcıyı yanlış yönlendirmez

##  Güçlü Yönler

 Halüsinasyon yok
 Akademik olarak savunulabilir
 Deterministik cevaplar
 Türkçe odaklı
 RAG mimarisi doğru uygulanmış

---

##  Sınırlılıklar

* Veri seti kapsamı ile sınırlı
* Porsiyon / derece gibi yapılandırılmış alanlar yok
* Şu an çoklu seçim (interactive suggestion) yok

---

## Lisans

Bu proje akademik ve eğitim amaçlı geliştirilmiştir.
Veri seti ve model lisansları ilgili sağlayıcılara aittir.

---

## Yazar

**Yemek Tarifleri Chatbot**
RAG tabanlı güvenli NLP projesi Burak AVCI tarafından yapılmıştır. (burakavci0206@gmail.com)

---
