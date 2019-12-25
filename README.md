# LabModelacion MAT-282
 
Repository created with the purpose of build recommender systems and as a "Laboratorio de modelación"(subject of college) Project.
Partial structure of README was obtained from the next link:

https://www.kaggle.com/WinningModelDocumentationGuidelines


## Content Table

- [ARCHIVE CONTENTS](#archive-contents).
- [HARDWARE](#hardware-the-following-specs-were-used-to-create-the-original-solution).
- [SOFTWARE](#software-python-packages-are-detailed-separately-in-requirementstxt).
- [COMMENTS 6/11/2019 UPDATE](#comments-about-6112019-update).

<br/><br/>

### ARCHIVE CONTENTS


__.ipynb_checkpoints__       :carpet with some checkpoints(User-User.ipynb)

__User-User.ipynb__          : Jupyter notebook file with all the code (Kernel=Python 3)

__BX-Users.csv__                     : Generic dataset with information associated to Users

__BX-Books-Rating.csv__                    : Generic with information associated to the "Rating"-interaction

__BX-Books.csv__                  : Generic dataset with information associated to Items


_Soon..._

_train_code                  : code to rebuild models from scratch_

_predict_code                : code to generate predictions from model binaries_

<br/><br/>

### HARDWARE (The following specs were used to create the original solution)

Windows 10 Home 64 bits 10.0,compilation:18362 (512Gb boot disk)

Intel(R) Core(TM) i5-8250U CPU @ 1.60Ghz (8CPUs) , ~1.8GHz

8192MB RAM



<br/><br/>

### SOFTWARE (python packages are detailed separately in `requirements.txt`) 

Python 3.7.3

nvidia drivers v.384

**Python library used**:

Pandas Ver. 0.25.1

Numpy Ver. 1.17.1

scikit-surprise 1.1.0


<br/><br/>

### Comments about 6/11/2019 update

Sparse Matrix size: ~100k users X 100k items
