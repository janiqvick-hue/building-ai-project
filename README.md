# Symptom Summarizer (Esitietolomakkeen täyttäjä)

Final project for the Building AI course

## Summary

This AI-powered assistant helps patients describe their symptoms in plain, everyday language before seeing a doctor. It then analyzes the input and translates it into a concise, professional medical summary for healthcare providers, saving time and improving diagnostic accuracy. (257 characters)


## Background

Medical consultations are often limited by time, and patients can find it stressful or difficult to recall and describe their symptoms accurately to a doctor. 
* **Time pressure:** Doctors have very few minutes per patient, and extracting history takes up most of it.
* **Communication gap:** Patients use colloquial terms, while electronic health records require structured, clinical language.
* **Motivation:** My motivation is to reduce the administrative burden on healthcare professionals and ensure that patients feel heard and understood, leading to better and faster care.


## How is it used?

Before a scheduled appointment or during digital triage, the patient interacts with a user-friendly chatbot interface. The patient explains what is wrong in their own words (e.g., "My chest feels tight and I've been coughing for three days"). 

The AI asks clarifying follow-up questions if critical information (like duration or severity) is missing. Finally, it generates a structured note directly for the doctor's screen.

This tool is used in:
* General practitioner (GP) clinics
* Digital telehealth platforms
* Emergency room triage desks


## Data sources and AI methods

The system relies on advanced Natural Language Processing (NLP) and Large Language Models (LLMs) trained on medical corpora. 
* **Data Sources:** De-identified, open-source medical dialogue datasets and clinical guidelines (such as [MIMIC-III](https://mit.edu) or public medical ontologies like SNOMED-CT).
* **AI Methods:** 
  * Named Entity Recognition (NER) to extract symptoms, anatomical locations, and timelines.
  * Text Summarization to transform long conversational text into bulleted medical summaries.

```python
# Conceptual example of parsing patient text (simplified NLP concept)
def parse_symptoms(patient_text):
    symptoms_db = ['cough', 'fever', 'headache', 'chest pain']
    detected = [s for s in symptoms_db if s in patient_text.lower()]
    return f"Chief Complaint: Patient reports {', '.join(detected)}."

print(parse_symptoms("I have a bad cough and a mild fever since yesterday."))
```

## Challenges

What this project *does not* solve:
* **No Automatic Diagnosis:** This tool does **not** diagnose diseases or prescribe medication. It only summarizes communication.
* **Ethical and Data Privacy Concerns:** Medical data is highly sensitive (GDPR/HIPAA regulations). The AI must process data securely and completely anonymize or delete conversations after the summary is sent to the electronic health record.
* **Hallucinations:** LLMs can sometimes fabricate information, so the summary must always be easily verifiable by the human doctor.


## What next?

To grow this project into a real-world application, it would need:
* **Integration:** Connecting via API to existing electronic health record (EHR) systems used in hospitals.
* **Multilingual support:** Helping immigrants or non-native speakers describe symptoms in their own language and translating it to the local medical language.
* **Collaboration:** Partnering with medical doctors and healthcare data security experts to ensure clinical safety and compliance.


## Acknowledgments

* Inspired by the challenges faced in modern digital healthcare triage.
* Built as a final project for the Elements of AI / Building AI course by Reaktor and University of Helsinki.
