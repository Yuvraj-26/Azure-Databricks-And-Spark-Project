# Databricks Notebooks

## Azure Databricks Notebooks
- Notebooks are a common tool in data science and machine learning for developing code and presenting results. In Azure Databricks, notebooks are the primary tool for creating data science and machine learning workflows and collaborating with colleagues. Databricks notebooks provide real-time coauthoring in multiple languages, automatic versioning, and built-in data visualizations.

### Magic Commands
- %sql %scala %python %md
- Run all runs commands in the context or language specified  
- %fs file system with ls
- %sh shell with ps to see processes running in cluster

### Databricks Utilities
- File system utilities to access Databricks file system from notebooks and use file system operations
- Secrets utilities to obtain values stored in secrets scopes or Azure Key Vault
- Widget Utilities to parametrize notebooks so calls to notebooks or another application such as ADF pipeline can pass a parameter value to the notebook at runtime (useful for creating reusable notebooks)
- Notebook Workflow utilities to invoke one notebook from another and chain notebooks
  - dbutils.fs.ls('/databricks-datasets')
  - programmatically combine dbutils with python
