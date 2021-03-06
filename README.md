### OncoNetExplainer: Explainable Predictions of Cancer Types Based on Gene Expression Data
Code and supplementary materials for our paper titled "Explainable Prediction of Cancer Types Based on Gene Expression Data", in proc. of The 19th annual IEEE International Conference on Bioinformatics and Bioengineering(BIBE 2019) to be held in Athens, Greece. 

#### Methods
In this paper, we collect genomics data about 9,074 cancer patients covering 33 different cancer types from The Cancer Genome Atlas(TCGA) and train a CNN and VGG16 networks using gradient-guided class activation map (Grad-CAM and Grad-CAM++) and Layer-wise relevance propagation (LRP). The following figure shows the workflow of the approach we followed:

<img src="https://github.com/rezacsedu/XAI_Cancer_Pred/blob/master/images/wf.png" width="700" height="650">

Then we identify most significant biomarkers and rank top genes across different cancer types based on mean absolute impact. Both models show high confidence at predicting different cancer types correctly at least 94% of the cases. 

To provide comparison with baselines, we further identify top genes for each cancer type and cancer specific driver genes using gradient boosted trees and SHapley Additive exPlanations(SHAP), which are further validated with the annotation from the TumorPortal.

#### Data collections
Gene expression about 33 different tumor types have been downloaded from The Cancer Genome Atlas(TCGA) portal covering 9,074 samples. See [here](https://github.com/rezacsedu/XAI_Cancer_Pred/tree/master/Data) for more details about the data. 

#### Data availability
The preprocessed data can be downloaded from [here](https://data.fit.fraunhofer.de/index.php/s/4yXxzSoRgnI18XY) with the password of '123' (without quote). 

#### A quick instructions on using GradCAM and ranking important biomarkers
A quick example on a small dataset can be performed as follows: 
* $ cd GradCAM_FI
* $ python3 load_data.py (make sure that the data in CSV format in the 'data' folder)
* $ python3 model.py
* $ python3 grad_cam.py

#### Examples of explanation using LRP
An example predictions with decision visualization with all the methods, in particular for LRP can be found in a [notebook](https://github.com/rezacsedu/XAI_Cancer_Prediction/blob/master/LRP_SoftmaxGradient/LRP_example.ipynb). 

#### Examples of explanation using CNN and SHAP
CNN and VGG16 networks using guided-gradient class activation map~(GradCAM). Further, we generated heat-maps for all the classes based on GradCAM to identify the most significant biomarkers and compute the feature importance in terms of mean absolute impact~(MAI) to rank top genes across cancer types. 

The following figures shows the generated heat-map examples for selected cancer types. Each column represents the result from one  fold. Rows represent the heat-maps of BRCA, KIRC, COAD, LUAD, and PRAD cancer types (from top-down):

<img src="https://github.com/rezacsedu/XAI_Cancer_Pred/blob/master/images/grid.png" width="800" height="350">

We found that KRTAP1-1, INPP5K, GAS8, MC1R, POLR2A, BET1P1, NAT2, PSD3, KAT6A, and INTS10 genes are common across cancer types giving the highest feature importance of 0.6 by protein-coding gene INTS10. The following 25 are top genes/biomarkers across 5 cancer types(sorted based on mean absolute impact(MAI) value:
<img src="https://github.com/rezacsedu/XAI_Cancer_Pred/blob/master/images/top_k.png" width="400" height="450">

The following figures shows common driver genes across 33 cancer types:
<img src="https://github.com/rezacsedu/XAI_Cancer_Pred/blob/master/images/common.png" width="500" height="400">

Nevertheless, a Python notebook will be added soon to show the steps more transparently. 

#### Examples of explanation using SHAP and Gradient Boosted Trees
Refer the [Python notebook](https://github.com/rezacsedu/XAI_Cancer_Pred/blob/master/Notebooks/GeneExpression_Classification_SHAP_XBoost.ipynb) to get an idea how to use SHAP and gradient boosted trees to generate feature importance and explanation about the prediction. 

First, we process the data (see the Python notebook). Then we train a GBT algorithm. Then SHAP explainer is used to provide explanation. The following figure shows clinical features contribution pushing the prediction higher in red and pushing the prediction lower are in blue: 

![](images/shap.png)

The following figure shows clinical features contribution in which features are ordered on the y-axis in a descending order according to their MAI~(each dot represents SHAP value for a specific feature):

<img src="https://github.com/rezacsedu/XAI_Cancer_Pred/blob/master/images/fi.png" width="450" height="550">

As seen, features pushing the prediction higher(i.e. NACA2, LOC442454, and C19orf6 are most significant features) are shown in red~(i.e. how much the probability for which the target is is increased), those pushing the prediction lower are in blue~(ASTN2 and PCDHGC3 are least significant).

### Citation request
If you use the code of this repository in your research, please consider citing the folowing papers:

    @inproceedings{karim2019XAI,
        title={OncoNetExplainer: Explainable Prediction of Cancer Types Based on Gene Expression Data},
        author={Karim, Md Rezaul and Cochez, Michael and Beyan, Oya and Decker, Stefan and Lange, Christoph},
        booktitle={The 19th annual IEEE International Conference on Bioinformatics and Bioengineering (BIBE 2019)},
        year={2019}
    }

### Contributing
For any questions, feel free to open an issue or contact at rezaul.karim@rwth-aachen.de
