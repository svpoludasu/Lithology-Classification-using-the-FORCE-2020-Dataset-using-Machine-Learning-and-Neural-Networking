# Lithology Classification using the FORCE 2020 Dataset using Machine Learning and Neural Networking

## About
This project was done using the dataset from [FORCE: Machine Predicted Lithology](https://xeek.ai/challenges/force-well-logs/overview) contest. The analysis presented here was done after the competition was closed.

## Problem Statement
The objective of the competition is to correctly predict lithology labels based on the provide well logs, NPD lithostratigraphy and well X, Y position.

## Description of Dataset
The provided dataset contains well logs, interpreted lithofacies and lithostratigraphy from offshore Norway wells . The well logs include the well name (WELL), the measured depth, x,y,z location for the wireline measurement as well as the well logs CALI, RDEP, RHOB, DHRO, SGR,  GR, RMED, RMIC, NPHI, PEF, RSHA, DTC, SP, BS, ROP, DTS, DCAL, MUDWEIGHT. The total dataset is divided into three parts as seen below.

![image](https://user-images.githubusercontent.com/69025410/113922128-86670680-97ac-11eb-8023-96ecaf4c185e.png)

1. **Training Data**  
The training data consists of well logs from 98 wells. For each log depth, the interpreted lithofacies class is given as an integer in the column FORCE_2020_LITHOFACIES_LITHOLOGY. Missing logs as marked as NaN. The only features guaranteed to be present are DEPT and GR. 

1. **Leaderboard Test Data**  
10 wells are included in leaderboard dataset and will be used to measeure accuracy in an open leaderboard. The open dataset only contains the well logs, not the interpretations.

1. **Hidden Test Data**  
10-20 wells will be kept in a hidden test dataset will to measure the final prediction score. The committee will run the participants’ submitted code on the closed test dataset for final scoring. Both logs and the interpretations on the closed test dataset is kept secret during the competition, but will be in the same format as the open test data. Eventhough, this analysis is done after the competition, the same rules of the competition were followed. ***The hidden and leaderboard dataset are only used to measure the prediction accuracy and were not used as the part of the model.*** 

### Lithology Key
The lithology key for the curve “FORCE_2020_LITHOFACIES_LITHOLOGY” is coded as seen below:
- 30000: Sandstone
- 65030: Sandstone/Shale
- 65000: Shale
- 80000: Marl
- 74000: Dolomite
- 70000: Limestone
- 70032: Chalk
- 88000: Halite
- 86000: Anhydrite
- 99000: Tuff
- 90000: Coal
- 93000: Basement

### Custom Scoring Function
Instead of penalizing each wrong prediction of the lithofacies similarly we decided to use a custom made penalty matrix derived from the averaged input of a representative sample of geoscientists. This allows for petrophysically unreasonable predictions to be scored by a degree of “wrongness”. 
The scoring function used to evaluate predictions is given by

![image](https://user-images.githubusercontent.com/69025410/113922742-494f4400-97ad-11eb-9cea-bd133b5514da.png)

where, 
- A is the scoring penalty matrix
- N is the number of samples
- ŷ<sub>i</sub> is the true lithology label 
- y<sub>i</sub> is the predicted lithology label

### Penalty matrix
The penalty matrix is shown below is the basis of the scoring function.

![image](https://user-images.githubusercontent.com/69025410/113922696-38063780-97ad-11eb-86d1-dab37caff07c.png)

