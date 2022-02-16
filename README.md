# Oracle Accelerated Data Science SDK (ADS)

The Oracle Accelerated Data Science (ADS) SDK is maintained by the Oracle Cloud Infrastructure Data Science service. It speeds up common data science activities by providing tools that automate and/or simplify common data science tasks, along with providing a data scientist friendly pythonic interface to Oracle Cloud Infrastructure (OCI) services.

With ADS you can:

 - Read datasets from Oracle Object Storage, Oracle RDBMS (ATP/ADW/On-prem) into `Pandas dataframes`
 - With `feature types`, create semantic types with multiple inheritances that are not bound by restrictions on the data type
 - Create reusable summary statistics, summary plots and validate data against a feature type schema
 - Tune models using hyperparameter optimization with the `ADSTuner`
 - Load text from files into `Pandas dataframe`

OCI service integrations are a key feature of ADS. These focus on making it easier for data scientists to use this broader set of services. Among the integrations are the Vault service that allows you to store secrets, such as access credentials to use with other OCI services. Others include integrations with other cloud services such as Model catalog, Model deployment, Data Science Jobs, Oracle Autonomous Database, and Object Storage.

## Installation

You have various options when installing ADS.

### Installing the oracle-ads base package

```bash
  $ python3 -m pip install oracle-ads
```

### Installing extras libraries

To use ADS within a notebook session run

```bash
  $ python3 -m pip install oracle-ads[notebook]
```

For machine learning tasks install

```bash
  $ python3 -m pip install oracle-ads[boosted]
```

To work on text related tasks run

```bash
  $ python3 -m pip install oracle-ads[text]
```

For access to a broad set of data formats (for example, Excel, Avro, etc.) run

```bash
  $ python3 -m pip install oracle-ads[data]
```

**Note**

Multiple extra dependencies can be installed together. For example:

```bash
  $ python3 -m pip install  oracle-ads[notebook,boosted,text]
```

## Documentation

  - [Oracle Accelerated Data Science SDK (ADS) Documentation](https://docs.oracle.com/en-us/iaas/tools/ads-sdk/latest/index.html)
  - [Oracle Cloud Infrastructure Data Science and AI services Examples](https://github.com/oracle/oci-data-science-ai-samples)
  - [Oracle AI & Data Science Blog](https://blogs.oracle.com/ai-and-datascience/)
  - [Oracle Cloud Infrastructure Documentation](https://docs.oracle.com/en-us/iaas/data-science/using/data-science.htm)

## Examples

### Load data from Object Storage

```python
  import ads
  from ads.common.auth import default_signer

  ads.set_auth(auth="api_key", profile="DEFAULT")
  bucket_name = <bucket-name>
  file_name = <file-name>
  namespace = <namespace>
  df = pd.read_csv(f"oci://{bucket_name}@{namespace}/{file_name}", storage_options=default_signer())
```

### Load data from ADB (simple)

```python
  connection_parameters = {
      "user_name": "<username>",
      "password": "<password>",
      "service_name": "<service_name_{high|med|low}>",
      "wallet_location": "/full/path/to/my_wallet.zip",
  }
  import pandas as pd
  import ads

  # simple read of a SQL query into a dataframe with no bind variables
  df = pd.DataFrame.ads.read_sql(
      "SELECT * FROM SH.SALES",
      connection_parameters=connection_parameters,
  )
```

### Load data from ADB (using sql-injection-safe bind variables)

```python
  df = pd.DataFrame.ads.read_sql(
      """
      SELECT
      *
      FROM
      SH.SALES
      WHERE
          ROWNUM <= :max_rows
      """,
      bind_variables={
          max_rows : 100
      },
      connection_parameters=connection_parameters,
  )
```

## Contributing

This project welcomes contributions from the community. Before submitting a pull request, please review our contribution guide.

Find Getting Started instructions for developers in README-development.md

## Security

Please consult the security guide for our responsible security vulnerability disclosure process.

## License

Copyright (c) 2020, 2022 Oracle and/or its affiliates. Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
