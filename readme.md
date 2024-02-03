
# HMS - Harmful Brain Activity Classification

**AIM:** Classify seizures and other patterns of harmful brain activity in critically ill patients

**Provided Data**
| Name  | type   | Inside   |
|-------------- | -------------- | -------------- |
| example_figures    | folder     |  Lots of pdf file    |
| test_eegs    |  folder    |  1 parquet file    |
| test_spectrograms    |  folder    |  1 parquet file    |
| train_eegs    |  folder    |  info    |
| train_spectrograms    |  folder    |  info|
| train.csv    |  file    | Shape (106800, 19)    |

**train.csv**
eeg_id,eeg_sub_id,eeg_label_offset_seconds,spectrogram_id,spectrogram_sub_id,spectrogram_label_offset_seconds,label_id,patient_id,expert_consensus,seizure_vote,lpd_vote,gpd_vote,lrda_vote,grda_vote,other_vote
1628180742,0,0.0,353733,0,0.0,127492639,42516,Seizure,3,0,0,0,0,0
1628180742,1,6.0,353733,1,6.0,3887563113,42516,Seizure,3,0,0,0,0,0



![image](https://github.com/phlex-ruby/phlex/assets/43055935/ae51e3d7-b0c1-4bee-a943-4f7a09528934)


**How To Solve**

This is an image classification problem with 5 Classes

Input Image is in the parquet format.
Classes are : 'Seizure', 'LPD', 'GPD', 'LRDA','GRDA', 'Other'

For the trial and baseline, the plan is to build something which works.
I'll build a simple image Classification pipeline and make a submission.

**Data Prprocessing**

The train.df size is (106800, 19) and contain z unique spectrogram_id.

1. Will save all the parquet data to numpy data
2. Will split the data by groupint the spectrogram_i to avoid data leacikage.
3. Will split the data into train and valid with the split ration 80:20.
3. Modify fastai datablock to handle .np data
5. Create a fastai dataloader and train resnet34 for 3 epochs.

**Observations**
1. Trained resnet34 with 3 epochs accuracy is 69.
2. Trained and valid loss is : 0.58 and 0.80.
