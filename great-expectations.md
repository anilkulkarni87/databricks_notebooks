## 📝 Table of Contents

- [About](#about)
- [Concepts in GE](#concepts)
  - [Data Context](#data-context)
  - [Stores](#stores)
  - [Data Docs](#datadocs)
  - [Checkpoints](#checkpoints)
- [Notebooks](#notebooks)
- [Open questions](#todo)
- [Advantages of GE](#advantages)
- [Authors](#authors)
- [Acknowledgments](#acknowledgement)


# Great expectations - Open Source Data Quality Tool <a name = "about"></a>
Great expectations fills the void that our Data pipeline exists. As we transition from Big Data to Good Data, teams have begun to realize the importance of good data. But the definition of good has also evolved over time. We want metrics to define the health of our pipeline and beyond.  

## Concepts in great-expectations <a name = "concepts"></a>
1. **Data Context** <a name = "data-context"></a>
    1. Data Sources
    2. Data Connectors
2. **Stores** <a name = "stores"></a>
    1. **Expectations Store** 
        - Expectations are stored
        - Backend: Azure Storage
    2. **Validations Store** 
        - Validation results are stored. Its the output when an expectation is run on a batch of data.
        - Backend: Azure Storage
    3. **Evaluation Parameter store** 
        - Yet to figure out
        - I want to compare todays rowcounts with yeaterday's rowcount for a specific batch. How do I do it?
    4. **Profile Store** 
        - There is still work happening on this one.
        - What does this mean?
    5. **Metrics Store** 
        - Metrics extracted from validation results are stored. 
        - Backend: Postgres
        - Only some metrics are being inserted.
        - ***This feature is still evolving.***  
    6. **Checkpoint Store** 
        - Checkpoint definitions are stored.
        - Backend: Azure Storage
3. **Data docs Sites** <a name = "datadocs"></a>
      - Backend: Azure Storage
      - The static html site is built.
4. **Checkpoints** <a name = "checkpoints"></a>
      - Backend: Azure Storage
      - The complete yaml files are persisted.
      - Can define email alerts.

### Installation
  Installation was a cakewalk. I have tried this in the Databricks community edition.

### Notebooks reference <a name = "notebooks"></a>
1. Setup Cluster by installing required libraries [Setup cluster](./greatexpectations/GE_CLUSTER_SETUP.html)
2. Define the BaseDataContext for GE [Setup Data Context](./greatexpectations/GE_PROPERTIES.html)
3. Define expectations and run tests [Data Quality](./greatexpectations/GE_POC.html)


### Data Docs
Please click here to look at the Data docs that GE is able to build [Data Docs](./web/$web/index.html)

## Advantages (from my perspective) <a name = "advantages"></a>
1. The open source version is complete in terms of defining data quality checks, executing, persisting the expectations and the results. Finally the Data Docs which makes them presentable.
2. Helps in building a static website for data docs and can be shared across the company/team.
3. Can easily translate result to Spark Dataframe for persisting the result in Database.
4. Can build wrapper around the configs to make onboarding easier. 


### Open Questions or ToDo: <a name = "todo"></a>
- How to define and leverage Evaluation Parameter Store?
- What is SqlAlchemyQueryStore?
- What is HtmlSiteStore?
- What does the error ``` Unrecognized urn_type in ge_urn: must be 'stores' to use a metric store.``` mean?
- How to define Database backend for the different stores?
- Can we filter out rows which fail and expectation and ingest only valid rows?
- How to define Data Sources like - S3 storage, Azure blob storage, Snowflake, Postgres? (Add an example) 


## ✍️ Authors <a name = "authors"></a>
- [@anilkulkarni87](https://github.com/anilkulkarni87) 


## 🎉 Acknowledgements <a name = "acknowledgement"></a>
- [Great expectations with Azure Backend](#https://medium.com/codex/pythonic-data-pipeline-testing-on-azure-databricks-2d27d3b5d587)


