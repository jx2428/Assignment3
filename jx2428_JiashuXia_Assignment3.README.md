# Assignment3
This Assignment applys SVM and PCA tp classify brain state fMRI images.

## Image Prepocessing
Run realign_test.m file and segment_test.m in SPM12. These two steps realign fMRI image data and create a mask to filter non-brain voxels in the image. The implementation follows the same instructions in Ch30 from SPM12 manual except in segmentation part, we set 6th tissue to be 'Native Space' and all other tissues are set 'None' in SPM12, which makes sure that only the brain voxels are segmented from the background. After running these two files, a mask is generated from SPM12 and saved locally. This mask is later referred as 'mask_img' in python file and used to mask all test images. 

## Image Masking & Feature Selection
Using the convolution method with the mask image and apply it to all test images, we obtain an array of all masked images. Then PCA is performed so that dimension can be reduced to a desirable level. After applying PCA techniques, we shuffle the pca data and our labels to avoid too many class '1' labels dominating the classification result. 

## Results
Running experiment on test data with PCA, the best model I got is:
![image](https://user-images.githubusercontent.com/77409643/144136851-47c871db-3377-4450-91b9-bc44b2dc9079.png)

Running experiment on unreduced masked data (without PCA), the best result I got is:
![image](https://user-images.githubusercontent.com/77409643/144137106-a1c76f98-6008-41b0-b104-e0325910d36f.png)

For test data, I choose my PCA component to be 100 and fold number to be 10, and masking threshold to be 0.9.

Running experiment on retest data with PCA, the best modeel I got is:
![image](https://user-images.githubusercontent.com/77409643/144137365-b2bea2a3-5a09-4e51-be3b-6f2a4170b138.png)

Without PCA, I have:
![image](https://user-images.githubusercontent.com/77409643/144137459-a2e4cfa1-d845-460b-afca-b734017474a3.png)

For retest data, I choose PCA component to be 80, cv fold number to be 8, and masking threshold to be 0.8.

Overall, whether with or without PCA, the performances on test and retest datasets are very close. Running PCA & SVM on retest data would generate a slightly higher accuracy rate than just implementing SVM. I think that the models with PCA are better because they can maintain and even improve accuracy rates on our experimented datasets. PCA also reduces running time and avoid overfitting issues. Models with PCA are less complicated than justing running SVM. Thus, SVM + PCA is a better approach. 

## Limitations
For some reason, the best result I have for retest data cannot exceed 85%. I have tried tuning PCA components, number of cv folds, masking threshold, and svm parameters, but they could only achieve accuracy rates from 80% to 84.5%. I think that limitations lie on masking methods. Other techniques could be applied to generate similar or better results to compare. 
