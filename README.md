# BM7
BM7: Computational phenotyping patients using multimodal EHRs
1. INTRODUCTION
This guide provides step-by-step instructions to reproduce the computational phenotyping pipeline, which involves data preparation, modelling, and evaluation of electronic health records (EHRs) from the MIMIC-III dataset. The project integrates both structured and unstructured data to identify clinically meaningful disease phenotypes using various machine learning and deep learning algorithms.
![image](https://github.com/user-attachments/assets/c3caee26-2b9d-47d7-b966-06bf14af270a)


3. SYSTEM REQUIREMENTS
1.	Operating System: Windows 10 or later, macOS, or Linux
2.	Python Version: 3.10.12
3.	Required Packages:  Listed in requirements.txt , Located in the root directory of the “BM7”repository.

3. SETTING UP THE ENVIRONMENT
Step 1: Clone the Repository
1.	Clone the project repository(BM7) from Github to your local machine:
Command :git clone <repository-url>  
Replace <repository-url> with your actual URL of your GitHub repository.

Step 2: Set up Directory Structure:
Ensure that the following directory structure exists under the BM7/Dissertation/ repository path. 
(The Github link has this folder properly ordered )
 
Figure 1: Repository folder Structure

Step 3: Set Up a Virtual Environment
1.	Navigate to the project directory
Command : cd path_to_project_directory
  

2.	Create a virtual environment
Command : python -m venv venv
 
3.	Activate the virtual environment
a.	On Windows: 
•	.\venv\Scripts\activate
b.	On macOS/Linux:
•	source venv/bin/activate 

Step 4: Install Required Packages
1.	Install all required packages using the ‘requirements.txt’  file.
•	pip install -r requirements.txt
 

4. DATASET ACCESS AND SETUP
Note: This guide assumes that the researcher has access to the MIMIC-III dataset. Data access must comply with all relevant ethical guidelines and regulations. Due to the sensitive nature of MIMIC-III data and with the guidance of project supervisor Dr.Xian Yang, sharing such data will be breach of ethics.
5. DATASET PREPARATION
Step 1: Obtain the MIMIC-III Dataset
1.	Access the MIMIC-III dataset:
•	Ensure that you have proper researcher’s access to the MIMIC-III database, since this dataset is sensitive medical data, so we need to comply by the HIPPA protection law.
•	 Follow the following instructions on PhysioNet to gain access:
 
Figure 2: PhysiNet access steps

2.	Download and Extract the Dataset:
•	Extract the data into a directory on your local machine. Make sure the structure of your directories aligns with the path expected in the code
The 6 code files that need to be downloaded are :
Original Tables	Size
PATIENTS.csv.gz	
ADMISSIONS.csv.gz	2.4 MB
ICUSTAYS.csv.gz	1.9 MB
DIAGNOSES_ICD.csv.gz	4.5 MB
D_DIAGNOSES_ICD.csv.gz	278.3 KB
NOTEEVENTS.csv.gz	1.1 GB

•	‘user_specifc_path/BM7/Dissertation/Datasets/……….’  this is the path where you should extract the 6 tables.


Step 2:  Set Data Paths
1.	Define Base Path: 
a.	The first thing the user/researcher should do is to set a common base path for all files. This should be the folder where you unzipped the BM7 folder.
base_path = 'user_specific_path/’

b.	All file paths in the script should use the base path, so you only need to update it once. At the start of the code.
# Load Data
data_path = f'{base_path}/ BM7/Dissertation/'Datasets/your_data_file.csv'
6. RUNNING PYTHON CODE NOTEBOOKS 
Follow the sequence to run the scripts from the 'user_specific_path/BM7/Code_Files/  folder.
1.demographics_modality (Structured Data Preparation)

2.ClinicalNotes+MedicalCodes_modality (Unstructured Data Preparation)

3.main_merge_file(Multimodal Data Integration)

3. Feature_Engineering

5.Main_Project_File( NLP + Modelling + Evaluation)

1.	Data Preparation and Integration: 
•	Execute script named 1_demographics_modality and 2_clinicalnotes+medicalcodes_modality.ipynb to preprocess raw data.
•	Run ‘3_main_merge_file.ipynb’ to perform the integration of structured and unstructured data
python 1_demographics_modality.ipynb
python  2_clinicalnotes+medicalcodes_modality.ipynb
python 3_main_merge_file.ipynb
(Run from the terminal)

2.	Feature Engineering:
python 4_feature_engineering. ipynb

3.	Text Preprocessing, Modelling, and Evaluation:
python  5_main_project_file. ipynb

	Batch preprocessing for Text preprocessing pipeline:
Due to computational limitations, the intensive preprocessing including MESH knowledge base mapping and Named Entity Recognition, might slowly process 30,000 rows of medical text . This highlighted the need for preprocessing pipeline execution in 6 batches of 5000 rows of data.
	Modelling and Phenotyping
Load pre-trained models from the ‘/BM7/Dissertation/ Saved_models/’.
o	LDA + KMeans: lda_model.pkl
o	NMF + KMeans: nmf _model.pkl
![image](https://github.com/user-attachments/assets/827687ba-8480-4080-ba4b-bb45af879bbe)

o	BERTopic + HDBSCAN: bertopic_ model.pkl
![image](https://github.com/user-attachments/assets/97e1c48c-95a4-4ea1-a182-9f4f34d4d6d1)

o	These models are used to perform computational phenotyping on the dataset. 
4.	Evaluation:
•	The 5_main_project_file.ipynb  has evaluation sections for each model and is easy to run with low resource usage.
7. OUTPUT VERIFICATION
1.	Verify Outputs: 
•	Compare the outputs generated by the scripts with the expected results documented in the report. The results should match the output files stored in the specified directories. 
•	NMF method is likely to perform the best compared to LDA and BERTopic.

•	Compare your results from the following results:
‘/BM7/Dissertation/ Final_Datasets/Saved_models/…….
1.	/ lda+kmeans_cluster_evaluation_metrics.csv
2.	/ nmf_evaluation_results.csv
3.	/bertopic_evaluation_results.csv



8. TROUOUBLEHSOOTING
Common Issues:
1.	Environment Errors: Ensure all packages in ‘requirements.txt’ are installed.
2.	Path Errors: Double-check the ‘base_path’ and ensure all paths are correct as mentioned in the repository structure.
3.	Data Access Issues: Verify access credentials for MIMIC-III dataset.
