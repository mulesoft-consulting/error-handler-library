# error-handler-library
An advanced mule 4 error handler library with handler overriding and extension

Design document: https://wiki.corp.mulesoft.com/display/OBD/Error+Handler+Library

- Step 1: Publish this library to your/customer artifact repo (Nexus, artefactory, azure repo etc)
- Step 2: Add it to the Mule project and execute command `mvn generate-sources` (See [mule4-rest-api-template](https://github.com/mulesoft-consulting/mule4-rest-api-template) project example)
- Step 3: Test

> [ Note: This library uses [Azure repo as an example](https://docs.microsoft.com/en-us/azure/devops/pipelines/artifacts/maven?view=azure-devops). ]
