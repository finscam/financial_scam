# 🚨 FINSCAM: Diagnosing Financial Scam Detection under Multilinguality, Multimodality, and Obfuscation

## 📌 Overview

Financial scam detection in practice operates under conditions standard benchmarks rarely reflect: communication is multilingual, deliberately obfuscated, and evidence arrives in isolated modalities rather than aligned pairs. A further structural problem undermines existing evaluations as most datasets contain only scam instances, making a trivial majority classifier competitive on accuracy while learning nothing about scam intent.

We introduce **FINSCAM**, a balanced benchmark of:

- 10,000 SMS messages (50% scam)  
- 700 videos (71% scam)  

spanning English, Hindi, Bengali, and code-mixed variants, with naturally preserved obfuscation.

Alongside the dataset, we propose the **Intent Consistency Score (ICS)** — a behavioral metric measuring prediction stability under six formally specified, intent-preserving perturbation types, human-validated by independent annotators (κ = 0.82, n = 120).

Evaluating seven models (including instruction-tuned LLMs, an Indic-specialized system, and multimodal video-language architectures) against interpretable baselines reveals:

> High accuracy often coexists with low intent consistency.

A keyword classifier achieves **71.2% accuracy** but only **24.8 ICS**, confirming reliance on surface cues.

A modality ablation shows video robustness comes from visual signals, not just transcripts.

🔗 Repository: https://github.com/finscam/finscam

---

## 📊 Table 7: English SMS Examples

| Message | Type | Obfusc. | Flip? |
|--------|------|---------|-------|
| [Phishing, URL frag.] Your KYC is expiring! Verify NOW at sbi-secure-kyc.in/update or your account will be BLOCKED!!! Click: bit.ly/3xRTv2k | SCAM | P4, P1, P5 | ✓ |
| [Lottery, digit mask.] Congrats! You’ve w0n Rs 5,00,000 in PM Jan Dhan Scheme. Call 0ur RBI Officer at 91-9876543210 immediately to claim! | SCAM | P6, P3, P2, P1 | ✓ |
| [Banking, homoglyph] Dear customer, your 0TP for UPI transaction of Rs 2,000 is 483921. Do NOT share with anyone. Valid for 10 minutes. | NON-SCAM | P6 | ✗ |
| [Job scam, no obfusc.] Work from home opportunity! Earn Rs 15,000 daily by completing simple data entry tasks. No experience needed. Registration fee Rs 500 only. WhatsApp: [PHONE] | SCAM | P3 | ✗ |

---

## 📊 Table 8: Hindi SMS Examples

| Message | Type | Obfusc. | Flip? |
|--------|------|---------|-------|
| [Govt. scheme, authority] Native script: “Pradhan Mantri Awas Yojana ke tahat aapko Rs 2.5 lakh ki sahayata milegi. Abhi register karein: pmay-reg.co/form2024 — RBI adhikari Verma” Transliteration: You are eligible for Rs 2.5 lakh housing subsidy under PM scheme. Register now. RBI officer Verma. | SCAM | P2, P4 | ✓ |
| [Investment, urgency] “Sirf aaj! Share market mein Rs 10,000 lagao aur 3 din mein Rs 50,000 kamao. Offer sirf aaj raat tak — call karein: [PHONE]” Only today! Invest Rs 10,000 in shares and earn Rs 50,000 in 3 days. Offer till tonight only. | SCAM | P1, P3 | ✓ |
| [Legitimate alert] “Aapka HDFC bank account statement tayaar hai. Dekhne ke liye net banking mein login karein. Helpline: 1800-XXX-XXXX” Your HDFC bank statement is ready. Log in to net banking to view. Helpline: [number] | NON-SCAM | — | ✗ |

---

## 📊 Table 9: Bengali SMS Examples

| Message | Type | Obfusc. | Flip? |
|--------|------|---------|-------|
| [Phishing, digit mask.] Native Bengali: “Apnar SBI account-er OTP: 739184. Ei OTP share korben na. Jodi apni eta request koren ni, ekhuni [PHONE]-e call korun — RBI official.” Your SBI account OTP: 739184. Do not share this OTP. If you did not request this, call [PHONE] immediately — RBI official. | SCAM | P2, P1, P3 | ✓ |
| [Lottery, spacing distort.] “A p n i b a c h a i pa e c h e n! Bangla lottery-te Rs 3,00,000 jitechen. Claim korte ekhuni call korun: [PHONE]” You have been selected! You won Rs 3,00,000 in Bangla lottery. Call now to claim. | SCAM | P5, P1, P3 | ✓ |
| [Legitimate notification] “Apnar Paytm wallet-e Rs 50 cashback joma hoyeche. Balance: Rs 237.50. Transaction ID: PTM2024XXXXXX.” Rs 50 cashback has been credited to your Paytm wallet. Balance: Rs 237.50. | NON-SCAM | — | ✗ |

---

## 📊 Table 10: Code-Mixed SMS Examples

| Message | Type | Obfusc. | Flip? |
|--------|------|---------|-------|
| [Crypto, EN-HI mixed] Bhai, yeh GENUINE opportunity hai! Crypto mein sirf Rs 5000 invest karo aur 30 din mein 10x return guaranteed. Limited seats — abhi join karo: t.me/cryptogain2024 Bro, this is a GENUINE opportunity! Invest just Rs 5000 in crypto, guaranteed 10x return in 30 days. Limited seats — join now. | SCAM | P1, P4 | ✓ |
| [Task scam, EN-BN mixed] Apnar jonno ekta part-time job ache! Daily 2 ghanta kaj kore Rs 1500 earn korte parben. Kono experience lagbe na — aaj-i apply korun. WhatsApp: [PHONE] There is a part-time job for you! Earn Rs 1500 working 2 hours daily. No experience required — apply today. | SCAM | P1, P3 | ✓ |
| [EN-HI, low-salience] Hello sir, main ek financial advisor hun. Aapke liye ek achha investment plan hai jo aapki savings ko grow karega. Kya hum baat kar sakte hain? Hello sir, I am a financial advisor. I have a good investment plan that will grow your savings. Can we talk? | SCAM | — | ✗ |
| [EN-HI, legitimate] Dear customer, aapka Axis Bank FD maturity date 15 Jan 2025 hai. Renewal ke liye branch visit karein ya net banking use karein. For help: 1860-419-5555 | NON-SCAM | — | ✗ |

---

## 🎥 Table 11: Video Scam Detection

| Video ID | Frame 1 | Frame 2 | Frame 3 | Label |
|----------|--------|--------|--------|-------|
| V1 | ![](assets/v1_f1.jpg) | ![](assets/v1_f2.jpg) | ![](assets/v1_f3.jpg) | SCAM |
| V2 | ![](assets/v2_f1.jpg) | ![](assets/v2_f2.jpg) | ![](assets/v2_f3.jpg) | NON-SCAM |
| V3 | ![](assets/v3_f1.jpg) | ![](assets/v3_f2.jpg) | ![](assets/v3_f3.jpg) | SCAM |

---

## 🧠 Obfuscation Patterns

| Code | Meaning |
|------|--------|
| P1 | Malicious links |
| P2 | Authority impersonation |
| P3 | Financial lure |
| P4 | Urgency |
| P5 | Domain/spacing tricks |
| P6 | Character obfuscation |
