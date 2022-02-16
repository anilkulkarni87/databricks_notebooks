# Soda Spark - Open Source Data Quality Tool

I stumbled upon [Soda](https://www.soda.io/) when on the lookout for open source DQ tools. It was quite easy to get started on it and incorporate it in existing Data pipelines. This repo has a notebook which will help others in exploring Soda more and see if it suits there needs. The notebook is self explanatory, but I wanted to jot down detailed steps and share for folks who are looking for the same.

## Soda Spark
The documentation is quite clean and easy to read and can be found [here](https://docs.soda.io/soda-spark/install-and-use.html). Below are generalised steps to be done for onboarding to Soda.
  1. Install soda spark
  2. Read about metrics available by [default](https://docs.soda.io/soda-sql/sql_metrics.html)
  3. Identify and define Soda scan [yml](https://docs.soda.io/soda-sql/scan-yaml.html) file for your dataset.
  4. Execute the scan on your dataframe. 
      1. It currently returns the object [`scan_results`](https://github.com/sodadata/soda-sql/blob/main/core/sodasql/scan/scan_result.py)
      2. It **used** to return a [Dataframe](https://github.com/sodadata/soda-spark/commit/9b3f4599808564021614fe21560abcf8958b79d8#diff-54ff0fdd14d0c6db5d58d6829438045162b55fb1f58b186ea4e87671cc5c9ba0R194)
  5. Take Action based on results. 
  
  ### Installation
  Installation was tricky currently when I tried it in Databricks Community Edition. You can refer to the Step 1 in the notebook for the workaround. Otherwise its pretty starightforward.

### Notebooks reference
1. Setup Cluster by installing required libraries [Setup cluster](./soda/SODA_CLUSTER_SETUP.html)
2. Define the BaseDataContext for GE [Define variables](./soda/SODA_PROPERTIES.html)
3. Define expectations and run tests [Data Quality](./soda/SODA_POC.html)
  
## Scan Results
Scan Results is a python Object and comprises of two child Objects:
  1. Measurements
      It holds the result of all metrics defined in the yml file.
  2. Test_result
      It holds the results of test defined at a table level and column level. 
 We can programtically check for a specific `measurement` or `test_result` and take action based on it. 
 
  ### My Approach
  I have currently converted the scan results to  a measurement Dataframe and test_result Dataframe for easier analysis. My planned next steps were publishing these results to InfluxDB, visualize and define alerts there. Before I could do that, I stumbled upon **Soda Cloud.** (Paid Service with Free trial)
  
## Soda Cloud
Soda Cloud does exactly what I wanted to do within Influxdata but without any additional work. Here are the steps I needed to do:
1. Setup Soda Cloud account
2. Create an api key
3. Setup the Soda Server Client
4. Add another argument when I execute the scan
`scan.execute(scan_definition, df, soda_server_client=soda_server_client)`

The below image shows a monitor created automatically based on the Scan yml file.
![image](https://user-images.githubusercontent.com/10644132/144951370-574cca6b-f1b2-4b32-b3ad-1db95a863e3e.png)

The below image shows an alert for a test that has failed
![image](https://user-images.githubusercontent.com/10644132/144951459-9756c70a-b685-4a77-9aa9-c13c53738abe.png)

You can look at all the Datasets you are monitoring in one place
![image](https://user-images.githubusercontent.com/10644132/144951554-6084fc07-5c6c-4bfa-bdec-1e58d125864b.png)

You can look at Schema, monitors and Sample_data (if published) for each dataset:
![image](https://user-images.githubusercontent.com/10644132/144951904-7c34da7f-2a11-46f6-a0f3-a0e53003cbfa.png)


## Advantages (from my perspective)
1. Easy setup
2. Quick to onboard
3. Can leverage just open source as we could define actions based on Scan results. 
4. If you leverage soda scan for all pipelines, Soda Cloud has the potential to act as Data Catalog with data health monitor. 
5. Excellent community support on [Slack.](https://community.soda.io/slack).
6. Sample data or Failed records could also be sent to cloud platform instead of Soda Cloud.

Some things which could take time due to the learning curve. I intend to add more examples here.
1. Defining the Scan yml file. 
2. Understanding the metrics that are provided by default.
3. Group metrics and Historical metrics


## Next Steps and Limitations
Soda Cloud is a paid service and I think it should be so for what it provides.
1. Explore publishing the scan result to Influxdata (community edition)
2. Visualize it in influx. This could be a good stack for personal projects. 
3. Soda currently supports many databses and soda-spark.
4. Soda streaming might be up soon. 
