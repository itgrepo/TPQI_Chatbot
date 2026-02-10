# E-Workforce Ecosystem (EWE) Intelligent Career & Labor Advisor

ระบบ Chatbot AI อัจฉริยะสำหรับให้คำแนะนำด้านอาชีพและกฎหมายแรงงาน พัฒนาด้วย **Streamlit**, **LangChain**, และ **Firebase Cloud Functions** โดยใช้เทคโนโลยี **RAG (Retrieval-Augmented Generation)** ร่วมกับ **OpenAI GPT-4o**

## สิ่งที่ต้องเตรียม (Prerequisites)

ก่อนรันโปรเจคนี้ คุณต้องมีบัญชีและ API Key จากบริการภายนอกดังนี้:

1.  **OpenAI API Key:** สำหรับใช้งานโมเดล GPT-4o และ Embedding
2.  **Firebase Project:** สำหรับเก็บฐานข้อมูล Vector

---

## การตั้งค่าและเชื่อมต่อ (Configuration)

หากคุณนำโค้ดนี้ไปใช้ **จำเป็นต้องแก้ไขและเชื่อมต่อข้อมูล 3 ส่วนหลัก** ดังนี้:

### 1. ตั้งค่า OpenAI API Key
ระบบถูกตั้งค่าให้ดึง API Key ผ่าน `st.secrets` เพื่อความปลอดภัย (ไม่ฝังในโค้ด)
* สร้างโฟลเดอร์ `.streamlit` ใน root directory
* สร้างไฟล์ `secrets.toml` ข้างในนั้น
* เพิ่มบรรทัดนี้ลงไป:
    ```toml
    OPENAI_API_KEY = "sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    ```

### 2. เชื่อมต่อ Firebase (Database)
ระบบใช้ Firestore ในการเก็บ Vector Embeddings คุณต้องเตรียมไฟล์สิทธิ์การเข้าถึง:
1.  ไปที่ [Firebase Console](https://console.firebase.google.com/) -> Project Settings -> Service accounts
2.  กด **Generate new private key** เพื่อดาวน์โหลดไฟล์ JSON
3.  เปลี่ยนชื่อไฟล์เป็น `serviceAccountKey.json`
4.  **นำไฟล์มาวางไว้ที่ Folder เดียวกับไฟล์ `app.py`**
5.  *หมายเหตุ: ห้ามนำไฟล์ `serviceAccountKey.json` ขึ้น Git เด็ดขาด (ควรใส่ใน .gitignore)*

### 3. ตั้งค่า Firestore Vector Search
เพื่อให้ระบบค้นหาข้อมูลได้ คุณต้องสร้าง **Index** บน Firestore:
* **Collection Name:** ในโค้ดตั้งค่าไว้ที่ `knowledge_base` (แก้ได้ที่ตัวแปร `COLLECTION_NAME`)
* **Field Name:** ข้อมูล Vector ถูกเก็บในฟิลด์ชื่อ `embedding_field`
* **Vector Dimension:** 384 (สำหรับโมเดล `all-MiniLM-L6-v2`)
* *เมื่อรันครั้งแรก หากค้นหาแล้ว Error ให้กด Link ใน Error Log เพื่อสร้าง Index อัตโนมัติใน Google Cloud Console*

---

## วิธีรันโปรเจค (How to Run)

1.  **ติดตั้ง Libraries:**
    ```bash
    pip install -r requirements.txt
    ```
2.  **รันแอปพลิเคชัน:**
    ```bash
    streamlit run app2.py
    ```

## โครงสร้างไฟล์ (File Structure)
- `app2.py`: โค้ดหลักของ Chatbot
- `.streamlit/secrets.toml`: เก็บ OpenAI API Key (ห้ามเอาขึ้น Git)
- `serviceAccountKey.json`: กุญแจเข้า Firebase (ห้ามเอาขึ้น Git)
- `requirements.txt`: รายชื่อ Library ที่ต้องใช้

---
