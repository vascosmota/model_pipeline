# model_pipeline
Generalist ML model engine with a Python backend

This engine goal is to run ML models in Python, in a batch fashion. 

# Information requirements
The following forms of infomation are availlable:
* Datasets, used to train and predict the ML model. Each ML model type has a different Dataset. This data is tabular.
* Model setups. Each ML model type and model flavour has a specific model setup.
* Metadata about the dataset.
* Prediction runtime parameters

# How the engine works
* Each model type/solution implements a specific pipeline. (TBD: Where are the pipelines declared)
* The pipeline needs to inherit from `PipelineCore`.

# How pipelines work
* Pipelines run one model type, of type <ModelPipelineType>. The <ModelPipelineType> class needs to inherit from the `ModelCore` class.
* Additionally, a Factory (inherited from `FactoryCore`) needs to be provided.

# `PipelineCore` class
* train method:
  * Instanciates a model using the Factory provided.
  * Fits the model
  * Serializes the model into the model artifactory
* \[batch\] prediction method
  * Deseralizes a model
  * Updates model with Prediction runtime parameters
  * Creates predictions
  * Stores predictions?

# Requirements for Factories
* A factory of <ModelFactoryType> type (inherited from `FactoryCore`) instantiates models of type <ModelPipelineType>.
* The factory has access to both **model setup** parameters and **model setup** of the model to instantiate. Factories for a given <ModelPipelineType> type are also aware of all model flavours availlable (which inherit from <ModelPipelineType>).

# Requirements for models to run
* Each <ModelPipelineType> inherits from  `ModelCore`.
* Each model flavour inherits from  <ModelPipelineType>.


# `ModelCore` class
* Implements the following methods: 
  * `fit`
  * `predict`
  * `serialize`
  * `deserialize`

# Model Artifactory
Use MLFlow?

# Future work
* Create `PipelineCore` class
* Create `FactoryCore` class
* Create `ModelCore` class
* Create NoSQL DB for model setups
* Create Unsupervised model for Pengins dataset `UnsupervisedPenguins(ModelCore)`
  * Create model flavour A
  * Create model flavour B
  * Create `PenguinsPipeline`
  * Create `PenguinsFactory`
* Create Supervised model for Titanic dataset
  * Create model flavour A
  * Create model flavour B
  * Create `TitanicPipeline`
  * Create `TitanicFactory`
* Support model-specific runtimes using different Docker images for each model
* Support non-tabular data
