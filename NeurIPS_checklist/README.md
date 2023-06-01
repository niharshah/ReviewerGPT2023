This directory contains the files to run the NeurIPS checklist experiment detailed in "ReviewerGPT? An Exploratory Study on Using Large Language Models for Paper Reviewing" by Ryan Liu and Nihar Shah. 

Files in the directory: 

 - NeurIPS_prompting.ipynb contains the code used to prompt the GPT-4 API with our prompts. A full set of instructions to replicate our experiments is below.

 - labels.xlsx contains author original checklist answers, our ground truth labels, the sections in the paper that we find most relevant to determining the answer, majority {"Yes"/"No"/"N/A"} responses from GPT-4, and whether the generated answers are correct. Papers (and labels/responses) are sorted by row, and checklist questions are sorted by column. 
 
 - data/ contains one directory for each paper index 0-14. In each sub-directory, save_dict.json stores the paper title, sections, and prompts for the checklist questions asked. Each remaining file corresponds to the responses generated for a particular checklist question in {question_name}.json. 

- Hyperparameter_selection.pdf contains the instructions and results of our GPT-4 hyperparameter pilot study for checklist questions. 

- pilot/ contains the code, data, and instructions for our hyperparameter pilot study. 


To replicate our experiments:

1. Obtain a set of papers from the OpenReview instance of the NeurIPS 2022 conference at openreview.net/group?id=NeurIPS.cc/2022/Conference, and put them in papers/. We provide links to the papers and supplementary materials used in our experiments in column D of labels.xlsx.

2. Obtain the ground truth labels for the author checklist. Most papers on the platform are submitted alongside an author checklist, either at the end of the paper or in the supplemental material (the template is at https://neurips.cc/Conferences/2022/PaperInformation/PaperChecklist). In our experiments, we manually label the author checklist answers, with the results in labels.xlsx. When labeling, make sure to also record which sections the answers are obtained from for easy prompt context construction (see column "label source" -> row "section" for each paper).

3. Use Jupyter Notebook to launch NeurIPS_prompting.ipynb. Make sure you have an OpenAPI API key in the current directory as "credential.json". See more on OpenAI API keys at https://platform.openai.com/account/api-keys. 

4. In the first cell, manually fill in the paper title, index (paper should be stored as papers/{paper_index}.pdf, and supplemental material as papers/{paper_index}supp.pdf), and the sections of the paper that correspond to each question in question_section_mapping.

5. In the second cell, manually fill in the text immediately before and after each of the sections into the corresponding re.search() function arguments. Use unique sequences of text as arguments so that the correct section text is selected. If needed, also separate the appendix into sections in the same way. 

6. Run all the remaining cells. The queried responses (3 per question is the default) will be stored at data/{paper_index}/{problem}.json. The prompts used for the queries will be saved in data/{paper_index}/save_dict.json. The responses will typically begin with "Yes", "No", or "N/A", which can be used as the GPT-4 output labels. 