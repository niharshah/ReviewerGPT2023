This directory contains the code and generated data for the pilot study conducted for the NeurIPS checklist portion of “ReviewerGPT? An Exploratory Study on Using Large Language Models for Paper Reviewing” by Ryan Liu and Nihar Shah.

The generated responses from GPT-4 are provided in the corresponding subfolders of data.zip, {q1c, q2a, q3a, q4a, q5a}. Each contains 32 files named as: "pilot_answers_{temp/topp}_{hyperparameter value}_{question name}.json", corresponding to different hyperparameter values. Each of those files contains three generated responses. 

The code used to run the pilot is in NeurIPS_prompting_pilot.ipynb. The sections used in to fill in the section portions in the prompts are in pilot_paper_sections.json. 

For more details, please see ../Hyperparameter_selection.pdf.