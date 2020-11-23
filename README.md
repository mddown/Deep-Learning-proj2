# Deep Learning Project 2: Explainable AI
Gene Eagle and Matt Downing

## What is in this repo?
- [XAI Write Up](https://github.com/mddown/Deep-Learning-proj2/blob/main/XAI%20write%20up.pdf)
- [python notebook](https://github.com/mddown/Deep-Learning-proj2/blob/main/covid-cxr.ipynb)
    - notebook contains LIME replication results (task #1) and SHAP results (task #3)
    - notebook also contains write up and observations on resutls

## Instructions on how to use this repo
1. Clone this repository (for help see this
   [tutorial](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository)).
2. Install the necessary dependencies (listed in
   [requirements.txt](requirements.txt)). To do this, open a terminal in
   the root directory of the project and run the following:
   ```
   $ pip install -r requirements.txt
   ```
3. Create a new folder to contain all of your raw data. Set the _RAW_DATA_
   field in the _PATHS_ section of [config.yml](config.yml) to the
   address of this new folder.
4. Clone the
   [covid-chestxray-dataset](https://github.com/ieee8023/covid-chestxray-dataset)
   repository inside of your _RAW_DATA_ folder. Set the _MILA_DATA_
   field in the _PATHS_ section of [config.yml](config.yml) to the
   address of the root directory of the cloned repository (for help see
   [Project Config](#project-config)).
5. Clone the
   [Figure1-COVID-chestxray-dataset](https://github.com/agchung/Figure1-COVID-chestxray-dataset)
   repository inside of your _RAW_DATA_ folder. Set the _FIGURE1_DATA_
   field in the _PATHS_ section of [config.yml](config.yml) to the
   address of the root directory of the cloned repository.
6. Download and unzip the
   [RSNA Pneumonia Detection Challenge](https://www.kaggle.com/c/rsna-pneumonia-detection-challenge)
   dataset from Kaggle somewhere on your local machine. Set the
   _RSNA_DATA_ field in the _PATHS_ section of
   [config.yml](config.yml) to the address of the folder containing the
   dataset.
7. Execute [_preprocess.py_](src/data/preprocess.py) to create Pandas
   DataFrames of filenames and labels. Preprocessed DataFrames and
   corresponding images of the dataset will be saved within
   _data/preprocessed/_.
8. Refer to the file covid-cxr.ipynb for a step by step flow of data training followed by LIME, GRADCAM, and SHAP evaluations. The notebook is a wrapper on the lower levels python scripts and can be used directly for running them. Additionally, the file config.yml facilitates configuring the parameters used by the python scripts; in the notebook, specific settings of the parameters are set as can be seen in the files config_class_weights.yml and config_random_oversample.yml.  

    Optionally, you can directly execute the following scripts to perform LIME and GRADCAM evaluations:

    - Execute [_train.py_](src/train.py) to train the neural network model.
   The trained model weights will be saved within _results/models/_, and
   its filename will resemble the following structure:
   modelyyyymmdd-hhmmss.h5, where yyyymmdd-hhmmss is the current time.
   The [TensorBoard](https://www.tensorflow.org/tensorboard) log files
   will be saved within _results/logs/training/_.
    - In [config.yml](config.yml), set _MODEL_TO_LOAD_ within _PATHS_ to
   the path of the model weights file that was generated in step 6 (for
   help see [Project Config](#project-config)). Execute
   [_lime_explain.py_](src/interpretability/lime_explain.py) to generate
   interpretable explanations for the model's predictions on the test
   set. See more details in the [LIME Section](#lime).

   ## Acknowledgements
   The starting code of this repository is based on the [Covid-19 Chest X-Ray Model repository](https://github.com/aildnont/covid-cxr), which provides the core code platform used for the evaluation. The SHAP implementation is based on the following [repository](https://github.com/slundberg/shap).