## Postman collections for EDP

> These collections include Jenkins integration with SCMs (provisioners will not be created in Jenkins, thus should be created manually), creation of EDP default apps, and deletion of Kubernetes Custom Resources for applications (applications cannot be deleted completely from EDP admin console this way and should be additionally removed from the database manually).

To start using collections, create a workspace in Postman and [import](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) the collections:

1. Import the collection with global [environment variables](https://learning.postman.com/docs/sending-requests/managing-environments/) and add 'CURRENT VALUE' to all variables. Don't forget to save the changes since Postman does not autosave them.
Global environment variables contain Kubernetes cluster info, SCM secrets, .etc.

2. Import other collections for applications:

- Make sure you are on the correct Kubernetes cluster.
- Launch `kubectl proxy` via CLI.
- Double-check the cluster IP and the port in the global variables.
- Run a chosen collection in Postman.

You can create several EDP applications at a time by running multiple [iterations](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).

Application collections will create collection variables automatically and iterate through them. In order to reset the counter, clear all collection scope [variables](https://learning.postman.com/docs/sending-requests/variables/).

3. If you want to use the import strategy, additionally, generate SSH keys, add the public key to an SCM, and then add both private and public keys as secretes in the Postman global variable section. Save the changes. Postman does not sync the data in the 'CURRENT VALUE' field to its servers for security reasons.

4. The collections can be also run by the [newman](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/) CLI tool or by [Postman CLI](https://learning.postman.com/docs/postman-cli/postman-cli-run-collection/).
Don't forget to spin up `kubectl proxy` before executing the `newman` commands.
Example (double-check the global variables):
```
newman run edp_jenkins_java11_gradle.postman_collection.json -g postman_global_environment_vars.json -n 2
```
This will iterate over the collection 2 times and create 2 java11-gradle applications.
