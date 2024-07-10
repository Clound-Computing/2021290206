Introduction
This repository contains the code and data used for our experiments on fine-grained fake news detection using three datasets: RAWFC, LIAR-RAW, and GossipCop-LLM. The goal is to generate explainable sentences that contribute to the final veracity prediction.

Datasets
RAWFC
RAWFC was constructed to alleviate the dependency on fact-checked reports by using raw reports (from scratch), where gold labels refer to Snopes. Each instance in the train/val/test set is presented as a single file.

LIAR-RAW
LIAR-RAW is based on the LIAR dataset, where gold labels refer to Politifact. To alleviate the dependency on fact-checked reports, we extended the public LIAR dataset with additional raw reports for each claim. These raw reports are put into a single file with the format of LIAR.

GossipCop-LLM
Our dataset is based on GossipCop, which is proposed by FakeNewsNet (ArXiv) (Github). We did some preprocessing to filter the data:

v1: Instances having “text” - 14,991 legitimate, 4,717 fake, 19,708 total
v2: Instances having “title” - 14,928 legitimate, 4,706 fake, 19,634 total
v3: Instances in proper length - 11,945 legitimate, 3,784 fake, 15,729 total
We used version v3 for further processing (refer to gossipcop_v3_origin.json).

Code Structure
Training and Evaluation Scripts
train_exp_fc5_RAWFC.py: Training script for the RAWFC dataset.
train_exp_fc5_LIAR_RAW2.py: Training script for the LIAR-RAW dataset.
train_exp_fc5_gossip.py: Training script for the GossipCop dataset.
eval_exp_fc5.py: Evaluation script for the general model.
eval_exp_fc5_rawfc.py: Evaluation script for the RAWFC dataset.
eval_exp_fc5_LIAR_RAW2.py: Evaluation script for the LIAR-RAW dataset.
eval_exp_fc5_gossip.py: Evaluation script for the GossipCop dataset.
Model Variants
model/model_exp_fc5.py: The main model implementation.
model/model_exp_fc5_remove_RS.py: Model variant without the report selection (RS) module.
model/model_exp_fc5_remove_SE.py: Model variant without the sentence extraction (SE) module.
model/model_exp_fc5_remove_RS_SE.py: Model variant without both the report selection (RS) and sentence extraction (SE) modules.
model/model_exp_fc5_remove_feature.py: Model variant with one of the four semantic features (claim relevance, richness, salience, non-redundancy) removed.
Additional Scripts
reader5.py: Script for reading and processing data.
Usage
Training: Use the corresponding training script for the dataset you are working with. For example:

bash
Copy code
python train_exp_fc5_RAWFC.py
Evaluation: Use the corresponding evaluation script for the dataset you are working with. For example:

bash
Copy code
python eval_exp_fc5_rawfc.py
Model Variants: To evaluate the impact of each component, use the model variants provided. For example, to train the model without the RS module:


change model_exp_fc5.py to model_exp_fc5_remove_RS.py
Preprocessing
For GossipCop-LLM, we used the v3 version after preprocessing for further processing. The preprocessing steps ensured that the instances are in proper length and filtered out irrelevant data.
