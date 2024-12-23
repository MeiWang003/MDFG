# MDFG: Multi-Dimensional Fine-Grained Modeling for Fatigue Detection
## Abstract

Fatigue is a critical factor contributing to accidents in industries such as safety monitoring and engineering construction. Fatigue exhibits dynamic complexity and non-stationary characteristics, so there are many intermediate states of short-term variation between alert and fatigue. Capturing and learning the signs of these intermediate states is essential for accurate fatigue assessment. However, current fatigue detection methods primarily rely on coarse-grained labels, typically spanning minutes to hours, and commonly treat alert and fatigue as two distinctly separate distributions, overlooking the expression of intermediate states and oversimplifying the rich distribution information of fatigue types and levels, thereby limiting detection effectiveness. To address these, this paper explores a refined representation of fatigue in terms of three dimensions: time, type, and level, and proposes a Multi-Dimensional Fine-Grained Modeling for Fatigue Detection (MDFG). This introduces the SmallLoss to extract trustworthy samples, utilizes clustering to identify diverse subtypes under alert and fatigued states, and establishes base class sets in each state. Subsequently, a complete base class set containing intermediate state bases is constructed using the base class synthesis method, which achieves the expression of intermediate fatigue states from absence to presence. Finally, fatigue levels are quantified based on the matching between samples and the complete base class set. Moreover, to cope with the complex variability of fatigue states, MDFG employs meta-learning for training. MDFG achieves an Average accuracy improvement of 10.0% and 12.1% on two real datasets compared to methods that do not consider fine-grained information. Extensive experiments demonstrate that the MDFG exhibits superior robustness and stability among current fatigue detection methods. \red{Code and Datasets are available at https://github.com/MeiWang003/MDFG/.
### The framework of our proposed method

![image-20241216231650888](/Farmework/image-20241216231650888.png)
## Installation & Requirements

The code has been tested with the following environment:

Python: 3.7

PyTorch: 1.13.1
### Install Python Packages

To install the required Python packages, run the following command:
```python
python -m pip install -r requirements.txt
```
## Dataset

Our experiments utilize the **reRLDD** and **reDROZY** datasets.
### Dataset Setup

1. **Training and Testing Split**:

   - The first 8 participants are used as the training set.
   - The remaining participants are used as the testing set.

2. **Feature Extraction**:

   - The Eye Aspect Ratio (EAR) is input into the wavelet packet for feature extraction.
   - The extracted features are stored in the `/wavelet_feature` directory.

3. **Confident Sample Selection**:

   - Confident samples are identified in FGT.
     - Update the paths: `path="your_wavelet_feature_path"` and `save_path="your_confident_data_save_path"`.
     - Run the following command to extract confident samples:
       ```python
       python ./small_loss/small_loss_confident_ind.py --dataset reRLDD
       ```
   - Both confident samples and remaining samples are stored in the `/confident_analysis` directory.

4. **Fine-Grained Feature Extraction**:

   - Input the confident samples, training set, and testing set into `gmm_extract_Fine_feature.py` to perform fine-grained classification.
     - Update the paths: `path="your_confident_data_save_path"` and `save_path="your_fine_data_save_path"`.
     - Run the following command to generate fine-grained samples:
       ```python
       python ./gmm_extract_Fine_feature.py --dataset reRLDD
       ```
   - This process generates quantified fatigue sequence features, which are stored in the `/fine_grained_feature` directory.
## Training & Testing
To train and test the model, use the following commands:
   ```python
   python ./MDFG_meta.py 
   ```

