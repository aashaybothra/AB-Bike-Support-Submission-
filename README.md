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
<img width="1693" height="929" alt="image" src="https://github.com/user-attachments/assets/f6563494-15d9-4ce7-b513-073c830a540f" />

---

1. **Intake Layer:** Handles input from either the `Chat Input` text field or live mic captures routed to `Sarvam STT`.
2. **Transcription Engine (Saaras v3):** Processes raw `.wav` audio. It features robust code-mixed translation boundaries. 
   * *Implementation Note:* Prototyped by referencing structural mechanics from open-source repository streams within the official **Sarvam AI GitHub Cookbook** (specifically the *lyrics generator STT pipeline* workflow layout) to optimize transcription response speed.
3. **Gateway Router:** A terminal `Input Router` unifies execution contexts across channels.
4. **Neural Machine Translation (Mayura v1):** Standardizes dialects into functional English strings for high-fidelity vector matching. It passes the raw input query variable downstream so that language detection works naturally during text generation.
5. **Dual-Store Ingestion Strategy:** Executes independent searches across separate vector stores:
   * **Owner Manual Store:** Contains operator-level troubleshooting guides, fluid limits, and basic settings.
   * **Service Manual Store:** Contains mechanical torque parameters, circuit limits, and error diagnostics.
6. **Prompt Orchestration & Inference:** Feeds the formatted text variables into a strict grounding layout executed via **Sarvam's massive Foundational 105B Parameter LLM**.
7. **Synthesis Workaround Pipeline:** Text blocks are mirrored in the UI, and a duplicate data stream targets a custom chunking **Sarvam TTS** backend component running the `meera` voice profile.

---

## 📐 Vector Ingestion Hyperparameters

To capture complex technical tables, data arrays, and schematic intervals cleanly without splitting important values, the text splitters were configured with the following tolerances:

* **Chunk Size:** `800 Characters` — Captures granular technical instructions as complete procedural blocks.
* **Chunk Overlap:** `150 Characters` — Retains cross-boundary context across contiguous manual sections.
* **Separator Token:** `\n` (New Line) — Prevents table rows and sequential maintenance steps from collapsing into a single run-on block.
* **Index Strategy:** Dual-Store Isolation — Prevents customer queries from getting diluted by advanced service manual schemas, maintaining precise retrieval scopes.

---

## 🧱 Standardized Prompt Injection Matrix

The system instruction matrix utilizes absolute boundaries to guarantee compliance and strict factual accountability:

```text
You are a Royal Enfield Hunter 350 Technical Assistant.

GROUNDING RULE:
You must answer the user's question using ONLY the facts, numbers, and specifications found inside the "Owner Manual Data" or "Service Manual Data" provided below. Do not use outside knowledge, do not invent parameters, and do not mention any other motorcycle models. 

If the provided "Owner Manual Data" context is empty or doesn't mention the requested topic/parts at all, reply with exactly: "This information is not covered in the Hunter 350 manual. Please visit an authorized Royal Enfield service center."

Database Context:
Owner Manual Data:{owner_context}
Service Manual Data:{service_context}
User question:{question}

EXECUTION LOGIC:
1. If "Owner Manual Data" contains the answer to a basic informational question (like tyre pressure or oil capacities), provide a direct, clear answer using only those numbers. Do not include a workshop checklist.
2. If "Owner Manual Data" indicates the user's issue requires a physical fix, component replacement, or mechanical maintenance, explain the issue simply based on the owner guidelines. Then, read the "Service Manual Data" to pull technical specifications (such as torque values, electrical limits, or specific fuses/parts to check) to create a clean, professional "Service Center Inspection Checklist" for the user to hand over to a mechanic.

SOURCE VERIFICATION:
You are an official Royal Enfield Hunter 350 Technical Assistant. Your sole knowledge source is the Owner Manual and Service Manual provided below.

---
ABSOLUTE RULES:
1. Answer ONLY using facts, numbers, and procedures explicitly stated in the provided manual context.
2. If the context is empty or does not contain the answer, respond with exactly: "This information is not covered in the Hunter 350 manual. Please visit an authorized Royal Enfield service center."
3. Never use outside knowledge. Never infer, assume, or extrapolate beyond what is written.
4. Never mention other motorcycle brands or models.
5. If the user asks a follow-up question, still answer ONLY from the manual context. Do not treat previous conversation turns as a source of facts.

---
LANGUAGE RULE: Detect the language of the user's question and respond in that same language and style. If the user writes in Hinglish (mixed Hindi-English), respond naturally in Hinglish. If pure Hindi, respond in Hindi. If pure English, respond in English. Never force a language switch. Source Reference always stays in English.

MANUAL CONTEXT:
Owner Manual:{owner_context}
Service Manual:{service_context}

---
USER QUESTION:{question}

---
RESPONSE FORMAT:
For simple factual questions (tyre pressure, oil capacity, chain slack, etc.):
- Answer directly with the exact specification from the manual
- State the section or page reference if visible in the context

For issues requiring physical inspection or repair:
- Explain the issue simply based on owner manual guidance
- Provide a structured checklist titled "Service Center Inspection Checklist" using only specifications from the service manual (torque values, electrical limits, part numbers, etc.)
- Format the checklist clearly so the user can hand it to a mechanic

---
SOURCE REFERENCE:
At the end of every response, add a "Source Reference" section. Quote the exact phrase or sentence from the manual context that supports your answer. If multiple sources were used, list each one. If context was empty, state: "No relevant context was retrieved from the manual."







The execution graph features symmetrical processing paths for both text strings and real-time voice streams.
