# Job-Postings-Text-Summarization
This project aims to analyze and summarize LinkedIn data science job postings to uncover trends in required skills, software proficiencies, and job descriptions. The goal is to provide a concise and comprehensive understanding of employer expectations to help job seekers better align their profiles with industry demands.

## Table of Contents
- [Project Background](#project-background)
- [Dataset Overview](#dataset-overview)
- [Analysis Components and Results](#analysis-components-and-results)
- [Contributors](#contributors)

## Project Background
The demand for data science professionals is rapidly increasing, and LinkedIn serves as a major platform for connecting job seekers with opportunities in this domain. However, the vast amount of job postings makes it challenging to extract actionable insights.

Thus, to provide the best simplicity and easiness for job-seekers, we tried several models including open-source LLM or locally trained models to perform the task of summarization. By comparing different model performance based on selected metrics and also their trade-offs, we may choose to apply them in diffeent contexts if possible.

## [Dataset Overview](https://www.kaggle.com/datasets/asaniczka/data-scientist-linkedin-job-postings)
In today's dynamic job market, understanding the skills and qualifications that employers are seeking is paramount for job seekers, recruiters, and policymakers alike. With the exponential growth of job postings across various industries, extracting meaningful insights from this vast amount of data can be challenging. To address this, we leverage different technique to distill key trends and patterns from job posting datasets. This dataset includes columns such as job titles, job locations, company names, skills required, salary, job level, and job summary etc. 

## Analysis Components and Results
1. [Exploratory Data Analysis](eda.ipynb)
- Main Findings:
    - Top 10 Most Common Job Skills:
    - Top 10 On-Demand Job Titles: Senior Data Scientist, Data Scientist, Data Engineer, Data Analyst, Senior Data Engineer, …
    - Job Levels: Senior >> Associate
    - Key Skill sets:
    ![Key Skill sets](key_skills.png)

2. Data Cleaning & Preprocessing:
- Remove special characters & digits
- Lowercase
- Tokenization
- Retain data-related keywords (skills)
- Remove stop words
3. [Modeling](preprocessing-model-bart-longT5.ipynb)
    
- Models: 
    - baseline: [facebook/bart-large-cnn](models/baseline_model.ipynb)
        - ROUGE scores in the range of 10-20%
        - Relevancy scores - Cosine Similarity: 0.23
        - [results example](zero-shot-summaries.txt)
    - [OpenAI model: gpt-3.5-turbo](models/model-openai.ipynb)
        - Example Prompt：*“You are a helpful assistant. The following data are the job description in the LinkedIn. Summarize the following job description with fluent sentences with the company name, job title, how many years of experience, skills needed.”*
        - ROUGE scores in the range of 19-25%
        - Relevancy scores - Cosine Similarity: 0.6
    - [DistilBART](models/model-LongT5-DistilBart-OPT.ipynb)
        - ROUGE scores in the range of 20-22%
        - Relevancy scores - Cosine Similarity: 0.6
    - [TF-IDF + T5 (t5-small)](models/model-LongT5-DistilBart-OPT.ipynb)
        - ROUGE scores in the range of 9-16%
    - [FLAN-T5](models/mode-flanT5-MiniLML6.ipynb)
        - ROUGE scores in the range of ~28%
        - Relevancy scores - Cosine Similarity: 0.69
    - *Other models tried but not suitable for our case: LDA, BERTSUM, LongT5, Open Pretrained Transformer*

- Results: 
    **FLAN-T5 is the Best Model so far**
    1. Instruction-Tuned for Better Understanding
    2. Handles Long Inputs
    3. Efficient and Versatile
    4. Minimized Repetition Issues
    5. Straightforward Integration

4. Further Improvement: 
- Computational Requirements
- Fine-Tuning Needs

See more discussion and details in the [report](Job_Summarization_Text_Project.pdf).

## Contributors
- Xiyi Lin
- Yi (Grace) Xie
- Sydney Li
- Oliver Zhou
