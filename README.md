# Royal Enfield Hunter 350 Multilingual Voice RAG Assistant

An intelligent, hands-free voice-to-voice Voice RAG application designed specifically for field mechanics and motorcycle operators. The system accepts messy voice inputs in local code-mixed dialects, standardizes queries, searches isolated vector manual indices, applies strict grounding guardrails, and reads out detailed technical specifications with automated streaming chunk workarounds.

---

## 🚀 Live Sandbox Validation Cases

The assistant acts as a zero-hallucination data mirror. Below are two verified live sandbox interactions demonstrating conversational Hinglish grounding and automated out-of-bounds rejection layers:

### Sandbox Test Case 1: Code-Mixed Technical Query
* **User Input:** *"check engine light kyun aati hai"*
* **Grounded System Output:**
  > Royal Enfield Hunter 350 mein check engine light (MIL) isliye aati hai kyunki:
  > 
  > 1. **Startup Self-Check**: Jab aap motorcycle start karte hain, toh check engine light 2-3 seconds ke liye glow karti hai aur phir OFF ho jaati hai. Ye normal hai aur dikhaata hai ki EFI system correctly kaam kar raha hai.
  > 2. **Malfunction Indication**: Agar start karne ke baad bhi check engine light continuously ON rehti hai, toh iska matlab hai ki electronic fuel injection (EFI) system mein koi fault hai.
  > 3. **Common Causes**: Manual ke according, check engine light in wajahon se aa sakti hai:
  >    - Engine oil temperature sensor circuit fault (P0650 DTC code)
  >    - MIL circuit malfunction
  >    - EFI system mein koi bhi malfunction
  > 
  > **Important**: Agar start karne ke baad check engine light OFF nahi hoti, toh aapko motorcycle Royal Enfield Authorized Service Centre mein check karwani chahiye. Isse ignore karne se engine damage ho sakta hai.
  > 
  > Service manual mein mention hai ki MIL (Malfunction Indicator Lamp) ko hi check engine light kehte hain, aur agar ismein koi loose connection ya pin deformation hai, toh usse bhi check engine light aati hai.
  > 
  > **Source Reference**: 
  > - *"After the vehicle is started, the MIL will glow for a few seconds and turns 'OFF', this indicates that all the function of the electronic fuel injection (EFI) system is functioning normally. In the event of any malfunction in the EFI system the MIL will glow continuously."*
  > - *"Malfunction indicator lamp (MIL) is also called as Check engine light"*
  > - *"TROUBLE CODE: DTC CODE: P0650, type of error: MIL circuit malfunction"*

### Sandbox Test Case 2: Out-of-Bounds Adversarial Rejection
* **User Input:** *"meri gf meri bike par kyun naahi baith ti hai"*
* **Grounded System Output:**
  > यह जानकारी Hunter 350 मैनुअल में कवर नहीं की गई है। कृपया एक अधिकृत Royal Enfield सर्विस सेंटर पर जाएँ।
  > 
  > **Source Reference**:
  > *"This information is not covered in the Hunter 350 manual. Please visit an authorized Royal Enfield service center."*

---

## 🛠️ System Architecture & Data Telemetry Flow

The execution graph features symmetrical processing paths for both text strings and real-time voice streams.
