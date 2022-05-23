# Deep Learning Models to Predict Skin Cancer
- Problem Statement

Skin Cancer is an extremely prevelent form of cancer. In the US, about 9,500 people in the US are diagnosed with skin cancer every day. When detected early, patients with skin cancer have an extremely high survival rate. Steps should be taken to improve the accessibility of early detection. With an accurate deep learning model, patients could take pictures of their own skin abnormalities and detect cancer early. We aim to develop a deep learning model that can correctly classify the type of skin cancer a patient has.

- Project learning/experience goals

We really wanted to get comfortable with working with image data. For this reason, we decided to focus more on making conv2d models, rather than also implementing ML models.

- Data description

This dataset contains 10015 dermatoscopic images of pigmented lesions for patients in 7 diagnostic categories. For more than half of the subjects, the diagnosis was confirmed through histopathology and for the rest of the patience through follow-up examinations, expert consensus, or by in-vivo confocal microscopy. More information about the dataset and the diagnosis categories, features and patience conditions besides the links to download the dataset can be found on either Harvard Dataverse https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/DBW86T or on Kaggle https://www.kaggle.com/kmader/skin-cancer-mnist-ham10000/home.

Actinic keratoses and intraepithelial carcinoma / Bowen's disease (AKIEC),
basal cell carcinoma (BCC),
benign keratosis-like lesions (solar lentigines / seborrheic keratoses and lichen-planus like keratoses, BKL),
dermatofibroma (DF),
melanoma (MEL),
melanocytic nevi (NV)
vascular lesions (angiomas, angiokeratomas, pyogenic granulomas and hemorrhage, VASC).

- Literature Review

In recent times, the major work was carried out on developing models based on CNN variants (ResNet, EfficientNets,
SENet, so on) for classifying skin lesions using dermoscopic images [1, 2, 3]. They preprocessed the images
to eliminate the not interesting regions like eliminating dark circles in the images around the lesion region, contrast
balancing, etc. They used data augmentation, random cropping strategies for tackling class imbalance. 5-fold crossvalidation, Ensembling strategy for making the model robust.

1.  Nils Gessert, Maximilian Nielsen, Mohsin Shaikh, René Werner, and Alexander Schlaefer. Skin lesion classification using ensembles of multi-resolution efficientnets with meta data. MethodsX, page 100864, 2020.
2. Quoc V. Le Mingxing Tan. Efficientnet: Rethinking model scaling for convolutional neural networks. ICML 2019
3. Giuseppe Argenziano, HP Soyer, V De Giorgi, Domenico Piccolo, Paolo Carli, and Mario Delfino. Interactive
atlas of dermoscopy (book and cd-rom). 2000.

- Hypothesis

From our initial testing, we found that working with this data set was extremely difficult. Because the data is highly imbalance, our models would only predict images as "NV" (the dominant class). Therefore, we set out to improve the performance by changing the data set. We tried making the data set binary, (either "NV" or "Other"), and we tried under sampling the data to fix the imbalance. The binary data did not perform well. The under sampled data on the other hand began to give promising results. After observing the confusion matrix we found that the model was doing well at distinguing classes 2 (NV) and 6 (VASC).

[ 7  7 3 6  7  1 2 ]

[21 25 6 7 10  3  4]
   
$$\begin{bmatrix} 7 & 7 & 3 & 6 & 7 & 1 & 2 \\ 21 & 25 & 6 & 7 & 10 & 3 & 4 \\  0 & 0 &  5 & 4 & 2 & 10 & 0\\ 1 & 1 & 3 & 5 & 3 & 7 & 1 \\ 1 & 0 & 7 & 6 & 4 & 7 & 0 \\ 0 & 0 & 0 & 0 & 1 & 0 & 23\end{bmatrix}$$
                  
For this reason, we also decided to make another data sample that splits the data into three categories. NV, VASC and OTHER. 

We predict that the binary data set will perform the worst of all of them. Then, the next highest performer will be the over/under sampled multi class data set. We predict that the highest performer will be the data set using three categories. 
