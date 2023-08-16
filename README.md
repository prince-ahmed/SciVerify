<table align="center"><tr><td align="center" width="9999">
<img src="/static/ORI.png"  width="100%" align="center" alt="Logos">
<!-- <img src="/static/codeplus_logo.png" width="49%" align="center" alt="Logo for Code+"> -->

# Using ML/NLP to Identify Relationships and Similarities in Grant Proposal Texts



The code can be found [here](https://gitlab.oit.duke.edu/code-plus-ml-nlp/codeplus-final).


**README documentation for the project**
</td></tr></table>

## Table of Contents
- [Problem Statement](#prob_statement)
- [Project Goals](#goals)
- [Solution Overview](#solution_overview)
  - [User Interface](#user-interface)
  - [General Workflow](#general-workflow)
  - [Tests and Results](#tests_results)
- [In-Depth Look at Features](#features)
  - [Database Comparison](#db_compare)
  - [Batch Comparison](#batch_compare)
  - [Keyword Flagging](#keywords)
  - [View Summary](#summary)
  - [Additional Functionalities](#custom_file)
- [Getting Started](#starting)
  - [Dependencies](#dependencies)
  - [Installation](#installing)
  - [Executing the Program](#executing)
- [The Team](#team)
- [Acknowledgments](#acknowledgments)

## Problem Statement <a name = "prob_statement"></a>
As the Office of Research & Innovation (OR&I) compare grant proposals for similarities, there are thousands of documents from the Duke database that OR&I must manually parse through before the proposal can be submitted to ensure that the proposal does not have overlaps with an already existing proposal.


## Project Goals <a name = "goals"></a>
**In developing the algorithm, the program can help OR&I and researchers in:**
1. Increasing the efficiency of document parsing, processing, and comparisons
2. Optimizing funding allocation by reducing the competition among Duke researchers for grant funds
3. Fostering academic collaboration by connecting researchers with similar proposals and goals


## Solution Overview <a name = "solution_overview"></a>
Using Machine Learning and Natural Language Processing, our Code+ team developed an algorithm, as well as a user interface, to aid OR&I in swiftly identifying grant proposals with overlaps, with a focus on the projects' abstracts.

### User Interface <a name = "user-interface"></a>
Developed using Voila, which allowed the Jupyter Notebooks used in the project's development to be rendered as interactive HTML pages:
<img src="/static/demo_general_1.gif" width="100%" alt="File upload widget"/>
<img src="/static/demo_general_2.gif" width="100%" alt="View of results (from database comparison)"/>

### General Workflow <a name = "workflow"></a>
Once a file is uploaded, this is a high-level overview of the processing it goes through in order to identify similar grant proposals:
<img src="/static/workflow.png" align="center" width="100%" alt="Algorithm Workflow Diagram">

### Tests and Results <a name = "tests_results"></a>

**Ground Truth Files** were 5 pairs of documents that the ORI office deemed worthy of flagging. We used these files to test our algorithms, models and filters.

Some of the variables that we explored were:

- Different combinations of keywords

- Grouping files by proposal

- Length of summaries

- Models to get the embeddings

The experiments followed:

1. Populating a data frame by changing an associated variable.

2. Running the associated algorithm on the 10 ground truth files.

3. Looking at the index of the associated pair in the return list - **zero index indicating the pair has been correctly flagged.**

Using all-MiniLM-L6-v2 for both the summaries and the semantic search yielded zero indexes for all the 10 test cases - a perfect score:

**[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]**

To achive this result the files were not grouped by proposal ID (SPS number). The keywords used to filter the files were:

- _Aim_

- _Strategy_

- _Abstract_

- _Experiment_

- _Overview_

- _We will_

- _We propose_


To take a deeper look into all the different test results look at [results.pdf](https://gitlab.oit.duke.edu/code-plus-ml-nlp/codeplus-final/-/blob/main/results.pdf)

## In-Depth Look at Features <a name = "features"></a>
### Notebooks Containining Pages Rendered in Voila 
#### Database Comparison: dbcompare.ipynb <a name = "db_compare"></a>
- **Input:** 1 PDF file
- **Output:** 
  - Top 5 most similar grant proposals in database (with option to see more matches)
  - Summary of each match in the top 5
  - Most similar sentence pairs relative to each proposal in the top 5
- **Workflow:**
  - Text from uploaded file is extracted, filtered, and summarized
  - Sentences are separated from within filtered text
  - Summary and sentences are compared to information stored in a Pandas dataframe

<img src="/static/demo_database_1.gif" width="100%" alt="File upload for database comparison"/>
<img src="/static/demo_database_2.gif" width="100%" alt="Results for database comparison"/>

#### Batch Comparison: batchcompare.ipynb <a name = "batch_compare"></a>
- **Input:** 2 or more PDF files
- **Output:** 
  - Summary for each file
  - Cosine similarity score and most similar sentences between each pair of uploaded documents
- **Workflow:**
  - Text from each uploaded file is extracted, filtered, and summarized
  - Sentences are separated from within each filtered text
  - Each pair of files has their summaries and sentences compared
<img src="/static/demo_batch_1.gif" width="100%" alt="File upload for batch comparison"/>
<img src="/static/demo_batch_2.gif" width="100%" alt="Results for batch comparison"/>

#### Keyword Flagging: keywords.ipynb <a name = "keywords"></a>
- **Input:** 1 PDF file and custom list of keywords
- **Output:** 
  - Sentences and pages in which keywords were found
  - List of keywords that were not found in document
- **Workflow:**
  - Text from each uploaded file is extracted, filtered, and summarized
  - Sentences are separated from within each filtered text
  - Each pair of files has their summaries and sentences compared

<img src="/static/demo_keywords_1.gif" width="100%" alt="File upload for keyword flagging"/>
<img src="/static/demo_keywords_2.gif" width="100%" alt="Results for keyword flagging"/>

#### View Summary: viewsummary.ipynb <a name = "summary"></a>
- **Input:** 1 PDF file
- **Output:** summary of uploaded file
- **Workflow:** text from uploaded file is extracted, filtered, and summarized

<img src="/static/demo_summary.gif" width="100%" alt="File upload and results for viewing summary"/>

### Notebook for additional functionalities <a name = "custom_file"></a>
**File for Program Customization:** **usefulfunctions.ipynb**
- User can customize for filtered keywords, update the database of files, and view feedback results for each file
  - **Saving files to dataframe**
    - Contains function that allows user to input a path to a file
      - Extracts relevant information and stores it in Pandas dataframe
      - Can then be processed when new file is inserted through the "Database Comparison" page
  - **View Feedback Results**
    - Loops through list stored in Pickle file which contains results
      - Data is not aggregated in any way, just laid out so it's more easily human-readable


## Getting Started <a name = "starting"></a>
- The program was written in Python, on Jupyter Notebook, through computer sessions created within the Duke Compute Cluster, a high-performance computing cluster.
- To start the program locally, follow these example steps:
### Dependencies <a name = "dependencies"></a>
Packages the project uses are listed in [dependencies.txt](https://gitlab.oit.duke.edu/code-plus-ml-nlp/codeplus-final/-/blob/main/dependencies.txt)
### Installation <a name = "installing"></a>
1. Clone the repo

    **SSH**
    ```
      git clone git@gitlab.oit.duke.edu:code-plus-ml-nlp/codeplus-final.git
    ```
    **HTTPS** 
    ```   
      git clone https://gitlab.oit.duke.edu/code-plus-ml-nlp/codeplus-final.git
    ```

### Executing the Program <a name = "executing"></a>

1. On your code program, open the "codeplus-final" folder in your dashboard

  <img src="/static/folder_view.png"  width="49%" align="center" alt="View of folder name after cloning repo">

  Inside the folder

  <img src="/static/inside_folder.png" width="49%" align="center" alt="View of files in codeplus-final folder">

2. If you are not working with custom file usefulfunctions.ipynb: 
  Choose **dbcompare.ipynb**, **batchcompare.ipynb**, **keywords.ipynb**, or **viewsummary.ipynb**

  <img src="/static/choosing_files.png"  width="49%" align="center" alt="Example of choosing a file in codeplus-final folder">

  View of dbcompare.ipynb

  <img src="/static/dbcompare_view.png"  width="49%" align="center" alt="View of dbcompare.ipynb file">

3. After choosing your .ipynb file, run the code (all) in your code editor/program
   A user interface will be displayed, click on choose file to submit your file
   
  <img src="/static/user_interface.png" width="100%" alt="User Interface display example"/>

4. From the interface, after choosing your input PDF file. Press Submit.
  <img src="/static/demo_general_1.gif" width="100%" alt="File upload for database comparison"/>

### Webserver configuration with Nginx <a name = "Nginx"></a>

1. Set up a server with the dependencies listed in the [dependencies.txt file](https://gitlab.oit.duke.edu/code-plus-ml-nlp/codeplus-final/-/blob/main/dependencies.txt)

2. Install nginx following https://voila.readthedocs.io/en/stable/deploy.html#running-voila-on-a-private-server

3. Get a site certificate and get HTTPS encryption by following https://voila.readthedocs.io/en/stable/deploy.html#enable-https-with-let-s-encrypt

4. Set up basic authorization using https://www.digitalocean.com/community/tutorials/how-to-set-up-basic-http-authentication-with-nginx-on-ubuntu-14-04

5. The nginx file at 
/etc/nginx/sites-enabled
should look like the [server_configs_file_for_nginx.txt](https://gitlab.oit.duke.edu/code-plus-ml-nlp/codeplus-final/-/blob/main/server_config_file_for_nginx.txt) with the different domain names




## The Team <a name = "team"></a>

**Prince Ahmed**

**Rose DiPietro**

**Quan Doan**

**Rodrigo Guerreiro**

**Julie Ou**

**Isabelle Xiong**

## Acknowledgments <a name = "acknowledgments"></a>

**Duke Faculty**

**Project Leads**
- **Mark McCahill**
- **Andy Ingham**

**Project Managers**
- **Peining Yang**

**Program Staff**
- **Christopher Hall**


<img src="/static/bottom_home_page.png" align="center" width="100%" alt="Algorithm Workflow Diagram">

