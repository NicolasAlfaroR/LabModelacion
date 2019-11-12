# LabModelacion MAT-282
 
#### Repository created with the purpose of build recommender systems and as a "Laboratorio de modelación"(subject of college) Project .

#### Partial structure of README: https://www.kaggle.com/WinningModelDocumentationGuidelines

Matrix size (update 6/11): ~100000x1000000

#ARCHIVE CONTENTS
.ipynb_checkpoints       :carpet with some checkpoints(User-User.ipynb)
User-User.ipynb          : Jupyter notebook file with all the code (Kernel=Python 3)
BX-Users.csv                     : Generic dataset with information associated to Users
BX-Books-Rating.csv                    : Generic with information associated to the "Rating"-interaction
BX-Books.csv                  : Generic dataset with information associated to Items

Soon...
train_code                  : code to rebuild models from scratch
predict_code                : code to generate predictions from model binaries

#HARDWARE: (The following specs were used to create the original solution)
Windows 10 Home 64 bits 10.0,compilation:18362 (512Gb boot disk)
Intel(R) Core(TM) i5-8250U CPU @ 1.60Ghz (8CPUs) , ~1.8GHz
8192MB RAM

#SOFTWARE (python packages are detailed separately in `requirements.txt`):
Python 3.7.3
nvidia drivers v.384

#Python library used:
Pandas Ver. 0.25.1
Numpy Ver. 1.17.1
scikit-surprise 1.1.0
