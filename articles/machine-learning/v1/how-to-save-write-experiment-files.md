---
title: Where to save & write experiment files
titleSuffix: Azure Machine Learning
description: Learn where to save your input and output files to prevent storage limitation errors and experiment latency.
services: machine-learning
author: rastala
ms.author: roastala
manager: danielsc
ms.service: machine-learning
ms.subservice: core
ms.topic: how-to
ms.date: 01/25/2023

---
# Where to save and write files for Azure Machine Learning experiments
[!INCLUDE [sdk v1](../includes/machine-learning-sdk-v1.md)]

In this article, you learn where to save input files, and where to write output files from your experiments to prevent storage limit errors and experiment latency.

When launching training jobs on a [compute target](../concept-compute-target.md), they are isolated from outside environments. The purpose of this design is to ensure reproducibility and portability of the experiment. If you run the same script twice, on the same or another compute target, you receive the same results. With this design, you can treat compute targets as stateless computation resources, each having no affinity to the jobs that are running after they are finished.

## Where to save input files

Before you can initiate an experiment on a compute target or your local machine, you must ensure that the necessary files are available to that compute target, such as dependency files and data files your code needs to run.

Azure Machine Learning jobs training scripts by copying the entire source directory. If you have sensitive data that you don't want to upload, use a [.ignore file](how-to-save-write-experiment-files.md#storage-limits-of-experiment-snapshots) or don't include it in the source directory. Instead, access your data using a [datastore](/python/api/azureml-core/azureml.data).

The storage limit for experiment snapshots is 300 MB and/or 2000 files.

For this reason, we recommend:

* **Storing your files in an Azure Machine Learning [dataset](/python/api/azureml-core/azureml.data).** This prevents experiment latency issues, and has the advantages of accessing data from a remote compute target, which means authentication and mounting are managed by Azure Machine Learning. Learn more about how to specify a dataset as your input data source in your training script with [Train with datasets](how-to-train-with-datasets.md).

* **If you only need a couple data files and dependency scripts and can't use a datastore,** place the files in the same folder directory as your training script. Specify this folder as your `source_directory` directly in your training script, or in the code that calls your training script.

<a name="limits"></a>

### Storage limits of experiment snapshots

For experiments, Azure Machine Learning automatically makes an experiment snapshot of your code based on the directory you suggest when you configure the job. This has a total limit of 300 MB and/or 2000 files. If you exceed this limit, you'll see the following error:

```Python
While attempting to take snapshot of .
Your total snapshot size exceeds the limit of 300.0 MB
```

To resolve this error, store your experiment files on a datastore. If you can't use a datastore, the below table offers possible alternate solutions.

Experiment&nbsp;description|Storage limit solution
---|---
Less than 2000 files & can't use a datastore| Override snapshot size limit with <br> `azureml._restclient.snapshots_client.SNAPSHOT_MAX_SIZE_BYTES = 'insert_desired_size'`<br> This may take several minutes depending on the number and size of files.
Must use specific script directory| [!INCLUDE [amlinclude-info](../includes/machine-learning-amlignore-gitignore.md)]
Pipeline|Use a different subdirectory for each step
Jupyter notebooks| Create a `.amlignore` file or move your notebook into a new, empty, subdirectory and run your code again.

## Where to write files

Due to the isolation of training experiments, the changes to files that happen during jobs are not necessarily persisted outside of your environment. If your script modifies the files local to compute, the changes are not persisted for your next experiment job, and they're not propagated back to the client machine automatically. Therefore, the changes made during the first experiment job don't and shouldn't affect those in the second.

When writing changes, we recommend writing files to storage via an Azure Machine Learning dataset with an [OutputFileDatasetConfig object](/python/api/azureml-core/azureml.data.output_dataset_config.outputfiledatasetconfig). See [how to create an OutputFileDatasetConfig](how-to-train-with-datasets.md#where-to-write-training-output).

Otherwise, write files to the `./outputs` and/or `./logs` folder.

>[!Important]
> Two folders, *outputs* and *logs*, receive special treatment by Azure Machine Learning. During training, when you write files to`./outputs` and`./logs` folders, the files will automatically upload to your job history, so that you have access to them once your job is finished.

* **For output such as status messages or scoring results,** write files to the `./outputs` folder, so they are persisted as artifacts in job history. Be mindful of the number and size of files written to this folder, as latency may occur when the contents are uploaded to job history. If latency is a concern, writing files to a datastore is recommended.

* **To save written file as logs in job history,** write files to `./logs` folder. The logs are uploaded in real time, so this method is suitable for streaming live updates from a remote job.

## Next steps

* Learn more about [accessing data from storage](how-to-access-data.md).

* Learn more about [Create compute targets for model training and deployment](../how-to-create-attach-compute-studio.md)