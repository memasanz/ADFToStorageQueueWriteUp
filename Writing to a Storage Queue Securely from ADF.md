Writing to a Storage Queue Securely from ADF.

![Graphical user interface, text Description automatically generated](media/f81ce843cdc964346339fa713b0db139.png)

Steps:

1.  Retrieve SAS Key from Key Vault.

2.  Set a variable to hold that value (technically not needed, but makes things
    clean

3.  Post to the Storage Queue

Retrieve SAS key from Key Vault.

Reference Document: [Use Azure Key Vault secrets in pipeline activities - Azure
Data Factory \| Microsoft
Docs](https://docs.microsoft.com/en-us/azure/data-factory/how-to-use-azure-key-vault-secrets-pipeline-activities)

For a secret stored in key vault – each version will have a url, so be sure to
grab the version specific url.

For this pipeline, I create a few parameters


Parameter Name | Value
------ | ------
account   | storagename  

queue | queue name

kvurl = url for key vault secret



![Graphical user interface, table Description automatically generated](media/09e3e75c4244c5e74ff39f9fe4684614.png)

We will make a Web request that is a get. For this to work with MSI
authentication, be sure to provide access to your ADF Instance in your key vault
instance.

![Graphical user interface, text, application, email Description automatically generated](media/13c258acff40bca82a605754037a383d.png)

![Graphical user interface, application Description automatically generated](media/9dcea0a4cc3687f638788de9534adf41.png)

The Web Request is a GET, the url 

```
@concat(pipeline().parameters.kvurl,'?api-version=7.0')
```


Be sure to grab the output value and place into a variable.

![Graphical user interface, text, application Description automatically generated](media/f18427421bd98d7e551f553a779f50f9.png)

![Graphical user interface, application Description automatically generated](media/b9ec104398bd44e2a142c23ecb48215f.png)

Finish that up with a post

![Graphical user interface, text, application Description automatically generated](media/afc5cc7d0b99603c9a94e678e90b0fa9.png)
