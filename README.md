# Green Jobs

## Identifying Green Jobs 

The aim of this project is to identify green jobs within the [Open Jobs Observatory](https://github.com/nestauk/ojd_daps) job adverts database as part of a case study deliverable for the Department of Education. 

This repo contains the methodology for doing so. At a high level, the methodology is as follows:

1) Preprocess the text to: 
	a) Remove punctuation
	b) Detect sentences
	c) Lemmatise terms
	d) lowercase terms
	e) remove numbers
	f) remove stopwords

2) Generate bespoke normalised green count feature based on keyword expansion   
3) Create tfidf vectors and stack bespoke feature 
4) Oversample labelled training embeddings to address class imbalance using a Synthetic Minority Oversampling Technique (SMOTE)
5) Train a gradient boosted decision tree algorithm to predict whether jobs are green or not_green 

The final output is a saved `.json` file of job IDs and their associated class: green or not_green.

The current methodology results in a weighted F1 score of: **94%**. 

## Running the Green Jobs Pipeline

To clone the repository: 

```git clone git@github.com:nestauk/grjobs.git``` 

Assumed Python version: ```python==3.8```

- Meet the data science cookiecutter [requirements](http://nestauk.github.io/ds-cookiecutter/quickstart), in brief:
  - Install: `git-crypt` and `conda`
  - Have a Nesta AWS account configured with `awscli`
- Run `make install` to configure the development environment:
  - Setup the conda environment
  - Configure pre-commit
  - Configure metaflow to use AWS

Please checkout an existing branch (for example, the branch for the PR you are reviewing), or checkout a new branch (which must conform to our naming convention). If you have already made changes to a branch, you should commit or stash these. Then (from the repo base):

```pip install -U -r requirements.txt``` - to upload the necessary requirements to run the script

```conda install -c anaconda py-xgboost``` - to install mac OS, anaconda-compatible xgboost (see known issue <a target="_blank" href="https://github.com/dmlc/xgboost/issues/1446">here</a>)

To train the model with parameters in the base.yaml config file, run the following metaflow command:

Where `path/to` refers to wherever you have cloned the repository. 

```python path/to/grjobs/pipeline/train_flow.py run```

To run the saved, trained model on data from the database and output results via json:

Where `path/to` refers to wherever you have cloned the repository. 

```python path/to/grjobs/pipeline/green_classifier_flow.py run```

## To Dos

## Contributor guidelines

[Technical and working style guidelines](https://github.com/nestauk/ds-cookiecutter/blob/master/GUIDELINES.md)

---

<small><p>Project based on <a target="_blank" href="https://github.com/nestauk/ds-cookiecutter">Nesta's data science project template</a>
(<a href="http://nestauk.github.io/ds-cookiecutter">Read the docs here</a>).
</small>
