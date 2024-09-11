# 💊🦠 **DD-RDL: Drug-Disease Relation Discovery and Labeling** 🧬🔍


### Authors:  
👩‍💻 **Jovana Dobreva**  
👨‍💻 **Milos Jovanovik**  
👨‍💻 **Dimitar Trajanov**

### 🎓 **Institution**  
Faculty of Computer Science and Engineering, Ss. Cyril and Methodius University in Skopje, N. Macedonia

---

## 📜 **Abstract**

Drug repurposing involves using existing drugs to treat new diseases, and it has gained importance in recent years. This repository contains the code for **DD-RDL**, a model that employs **Natural Language Processing (NLP)** to extract drug-disease relations from large corpora of biomedical literature. The pipeline uses state-of-the-art NLP tools to discover relations between drugs and diseases, labeling the relationship using extracted **verbs**. This project is particularly useful for text-mining biological data, especially in the context of the ongoing **COVID-19** pandemic.

---

## 🚀 **Getting Started**

### 1. **Clone the Repository**  
To start using the DD-RDL model, clone the repository:

```bash
git clone https://gitlab.com/jovana.dobreva16/dd-rdl-model.git
```

## 🛠️ Methodology

The DD-RDL model is a pipeline of several NLP tasks designed to extract drug-disease relations from biomedical texts. It processes raw text into structured knowledge in the form of triplets (drug, verb, disease). Below are the key stages of the methodology:

### 1. **Named Entity Recognition (NER)**
- The **MedCAT** library is used for detecting medical entities such as diseases, drugs, proteins, and therapies.
- MedCAT links extracted entities to biomedical ontologies like **UMLS**, enabling accurate identification of domain-specific terms.

### 2. **Co-reference Resolution (CR)**
- We employ **Neural-Coref** to resolve co-references in the text. This step ensures that references like "it" or "they" are replaced with the actual entities (drugs or diseases), improving the accuracy of relation extraction.

### 3. **Semantic Role Labeling (SRL)**
- The **BERT-based** model is used for identifying the roles of words in a sentence (subject, verb, object). 
- We extract relations involving drugs and diseases by focusing on sentences where medical entities are connected with verbs representing actions.

### 4. **Verb Grouping**
- After identifying the verbs, we reduce redundancy by grouping similar verbs.
- Verbs are converted to their present tense and encoded using **word2vec** vectors. Using **cosine similarity**, verbs with similar meanings are grouped, reducing the number of unique actions.

### 5. **Knowledge Extraction**
- The model generates an **adjacency matrix** representing the probabilities of co-occurrence of drug-verb-disease triplets.
- A **bipartite knowledge graph** is constructed, where the **nodes** represent drugs and diseases, and the **edges** represent the verbs connecting them. Each edge is weighted based on the frequency of occurrence of the relation.

---

## 📊 Results

The DD-RDL model successfully extracts relations between drugs and diseases from biomedical texts, producing triplets in the form of (drug, verb, disease). Below are some key findings:

### 1. **Drug-Disease Relations Extraction**
- The model achieves **100% recall** for the known drug-disease pairs present in the gold standard dataset.
- In addition to extracting all predefined relations, the model discovered **18 novel drug-disease pairs**. These new pairs were manually checked and verified against biomedical literature.

### 2. **COVID-19 Case Study**
- The model was applied to the **CORD-19 dataset**, which contains research papers related to COVID-19.
- Key relations extracted from COVID-19-related abstracts:
  - **Selenium** is correlated with the **immune system** in COVID-19 treatments.
  - **Protease inhibitors** were found to help prevent the spread of **SARS-CoV-2**.

### 3. **Example Triplets Extracted**
- **Aspirin** -- (reduce) --> **Cardiovascular Disease**
- **Vitamin D** -- (prevent) --> **Osteoporosis**
- **Zinc** -- (support) --> **Immune System**

### 4. **Knowledge Graph**
- The extracted triplets were visualized as a **knowledge graph**, providing a clear representation of the relationships between various drugs and diseases.
- **Nodes** represent drugs and diseases, while **edges** represent the connecting action (verb), weighted by their relative frequency.

---

## 📂 Datasets

The DD-RDL model was tested on two primary datasets:

### 1. **Gold Standard Dataset**
- This dataset is derived from the **Therapeutic Target Database (TTD)** and contains **360 known drug-disease pairs**.
- The dataset is commonly used for evaluating drug-disease relation discovery models, ensuring that the DD-RDL model produces accurate and reliable results.
- It includes pairs for diseases such as **osteoporosis** and **cardiovascular disease**.

### 2. **COVID-19 Open Research Dataset (CORD-19)**
- **CORD-19** is a public dataset comprising scientific papers related to **COVID-19** and historical coronavirus research.
- The DD-RDL model was applied to abstracts and titles from this dataset to discover new drug-disease relations relevant to the ongoing pandemic.
- Key findings include relations between **supplements** like selenium and zinc with the **immune system** and **SARS-CoV-2** treatments.

Both datasets provide valuable test cases to evaluate the performance and utility of the DD-RDL model in the real-world biomedical research domain.

