# univ-devtest-lab
   Sample solution to demonstrate how Azure Dev Test Lab can be provisioned by university staff, with precreated templates for each semister/ semister courses

## Overview

### Overview Diagram
![overview diagram](https://raw.githubusercontent.com/maniSbindra/univ-devtest-lab/master/images/solution-overview.png)

### Context
This sample is intented to demonstrate how Azure Dev Test Laps with template repositories could be used By Universities  to allow students to instantiate preconfigured course Lab VMs. One potential contextual flow could be
* The University/College Admin would first provision the Dev Test Lab by following the steps mentioned below
* The Admin would then add/invite students to use the dev test Lab, giving them devtestlab user permission
* students would then use the dev test lab to create new VMs with preconfigured course lab content (based on templates from the template repository)

### Key Points
* The Templates folder should have semester wise templates provisioning the lab material for each course in that semester. Currently only a BE-Sem5 sample template has been added.
* The DTL-Deployment folder has scripts which provisions a Dev Test Lab, Configured with The Template repository. That is once the Dev Test Lab is provisioned users will be able to create VMs containing their course where by selecting the appropriate template

## Steps to Provision the Dev Test Lab
  * Fork this repo
  * Clone your fork locally
  * Generate Github PAT (read access) token
  * create azuredeploy.parameters.withtoken.json which is a copy of azuredeploy.parameters.json with the following changes
    * https://github.com/maniSbindra/univ-devtest-lab.git needs to be replaced by your github fork repository uri
    * PAT token from your github repository needs to be replaced. in this file
  * execute the script below (This assumes Azure CLI 2 has been installed)

    
    ```sh

    # cd into the DTL-Deployment folder
    cd DTL-Deployment

    # create resource group if not already existing
    az group create -n dtlWithTemplateRepo -l westus

    # deploy devtestlab with template repository 
    az group deployment create -n dtldep1 -g dtlWithTemplateRepo --template-file azuredeploy.json --parameters @azuredeploy.parameters.withtoken.json
    ```

     
     