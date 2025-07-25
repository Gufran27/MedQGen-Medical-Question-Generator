# MedQGen-Medical-Question-Generator

Medical Q&A Generator from PDFs
This repository contains a Python script designed to extract text from medical PDF documents and generate question-answer (Q&A) pairs using the Ollama language model. The script processes PDFs, extracts text using PyPDF2, and generates detailed Q&A pairs based on the content, saving the results in JSON format. It is specifically tailored for medical documents, focusing on diseases, symptoms, causes, treatments, and prevention strategies.
Features

PDF Text Extraction: Extracts text from PDF files page by page using PyPDF2.
Q&A Generation: Uses the Ollama model (llama3.1:8b) to generate comprehensive Q&A pairs from the extracted text.
Structured Output: Saves Q&A pairs in JSON format for easy integration and further processing.
Batch Processing: Processes PDF content in chunks (5 pages at a time) to handle large documents efficiently.
Customizable: Supports multiple PDF inputs and organizes outputs in a specified directory.

Prerequisites
To run the script, ensure you have the following installed:

Python 3.8 or higher
PyPDF2 (pip install PyPDF2)
Requests (pip install requests)
Ollama (pip install ollama) and the llama3.1:8b model installed locally
A compatible PDF file (e.g., medical documents like "21. Heart attack. Know the symptoms. Take action (Article) Autor National Heart, Lung, and Blood Institute.pdf")

Installation


Install Dependencies:
pip install PyPDF2 requests ollama


Set Up Ollama:

Install Ollama by following the official instructions: Ollama Documentation.
Ensure the llama3.1:8b model is downloaded and available:ollama pull llama3.1:8b




Prepare PDF Files:

Place your PDF files in the project directory or specify their paths in the pdf_paths list in the script.



Usage

Configure the Script:

Update the pdf_paths list in the script with the paths to your PDF files.
Specify the output directory in the output_dir variable (e.g., "heart").


Run the Script:
python medical_qa_generator.py


Output:

The script processes each PDF, extracts text, generates Q&A pairs, and saves them as JSON files in the specified output directory (e.g., heart/21_Heart_attack_Know_the_symptoms_Take_action_Article_Autor_National_Heart_Lung_and_Blood_Institute.json).
Each JSON file contains a list of Q&A pairs in the format:[
    {
        "instruction": "What is the main cause of this condition based on the document?",
        "output": "The PDF explains that this condition is mainly caused by..."
    },
    ...
]





Script Details

Text Extraction:
Uses PyPDF2 to read PDFs and extract text page by page.
Stores text in a list (text_per_page) for further processing.


Q&A Generation:
Processes text in chunks of 5 pages to manage memory and improve performance.
Sends text chunks to the Ollama model with a detailed prompt to generate Q&A pairs.
The prompt ensures questions cover all medical aspects (e.g., causes, symptoms, treatments) and answers are detailed (200-250 words).


Error Handling:
Handles empty responses and JSON parsing errors from Ollama.
Skips chunks with no valid Q&A output.


Output Formatting:
Converts Q&A pairs into a standardized JSON format with instruction and output fields.
Saves results in a directory with filenames derived from the input PDFs.



Example
For a PDF named  Heart attack. Know the symptoms. Take action (Article) Autor National Heart, Lung, and Blood Institute.pdf, the script:

Extracts text from all pages.
Generates Q&A pairs like:[
    {
        "instruction": "What are the symptoms of a heart attack according to the document?",
        "output": "The document lists symptoms such as chest pain, shortness of breath, nausea..."
    },
    ...
]


Saves the output to heart/21_Heart_attack_Know_the_symptoms_Take_action_Article_Autor_National_Heart_Lung_and_Blood_Institute.json.

Notes

Ensure the Ollama server is running locally before executing the script.
The script processes PDFs sequentially; for large PDFs, consider increasing the chunk size or optimizing memory usage.
The generated Q&A pairs are based solely on the PDF content, adhering to the prompt's strict guidelines.
If you encounter JSON decoding errors, check the Ollama model's response for formatting issues.

