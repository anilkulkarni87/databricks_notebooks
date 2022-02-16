# Great expectations - Open Source Data Quality Tool
Great expectations fills the void that our Data pipeline exists. As we transition from Big Data to Good Data, teams have begun to realize the importance of good data. But the definition of good has also evolved over time. We want metrics to define the health of our pipeline and beyond. 

## Concepts in great-expectations
1. Data Context
    1. Data Sources
    2. Data Connectors
2. Stores
    1. Expectations Store - Where expectations are stored
    2. Validations Store - Where the validation results are stored. Its the output when an expectation is run on a batch of data.
    3. Evaluation Parameter store - Yet to figure out
    4. Profile Store - There is still work happening on this one
    5. Metrics Store - Where metrics extracted from validation results are stored. 
    6. Checkpoint Store - Where Checkpoint definitions are stored
3. Data docs Sites
4. Checkpoints

### Installation
  Installation is a cakewalk. I have tried this in the Databricks community edition.

### Notebooks reference
1. Setup Cluster by installing required libraries [Setup cluster](./greatexpectations/GE_CLUSTER_SETUP.html)
2. Define the BaseDataContext for GE [Setup Data Context](./greatexpectations/GE_PROPERTIES.html)
3. Define expectations and run tests [Data Quality](./greatexpectations/GE_POC.html)


### Data Docs
Please click here to look at the Data docs that GE is able to build [Data Docs](./web/$web/index.html)

## Advantages (from my perspective)
1. Helps in building a static website for data docs and can be shared across the company.
2. Can easily translate result to Spark Dataframe for persisting the result in Database.



