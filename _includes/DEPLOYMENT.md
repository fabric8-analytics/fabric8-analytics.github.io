# Deployment
---

<br>

## Core service

#### Local Deployment

Start by cloning or forking the [fabric8-analytics-deployement](https://github.com/fabric8-analytics/fabric8-analytics-deployment). This repository should be everyting you need in order to run the core server API.

 You should check the README file, there should be all the information necessary for local deployment.

<br>

#### Deploying to OpenShift

 If you want to deploy the Analytics to the OpenShift, head over to the [openshift](https://github.com/fabric8-analytics/fabric8-analytics-deployment/tree/master/openshift) folder in the repository and again take a quick look at the README there.

 There are scripts prepared to ease your job, feel free to use them.

 Firstly, you need to have all the [credentials](/resources/credentials) set up and put into `env.sh` file. There is a template `env-template.sh` file, so just copy it over with

 ```bash
 cp env-template.sh env.sh
 ```

 and start setting things up.

---
 > **Proceed further only with `env.sh` file set up (see [credentials](/resources/credentials)) !**
---

Now you can log in with the [oc tool](https://www.openshift.org/download.html).

```bash
oc login $OC_URI -u $OC_USERNAME -p $OC_PASSWD
```

[Here](https://docs.openshift.com/enterprise/3.2/cli_reference/get_started_cli.html#basic-setup-and-login) is more info about the usage of `oc login` command.
The `$OC_URI` is pre-defined in the `env-template.sh` file and to the actual date it should be https://dev.rdu2c.fabric8.io:8443/.


If this is your first time logging into the OpenShift and all credentials were provided correctly, you should see this output in your console:

```
Login successful.            

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>                           

```

Now, let's run the `deploy.sh` script.

*NOTE: If you already have run the deployment before, you might want to add `--purge-aws-resources` argument.*

```bash
./deploy.sh
```
*Note: Don't worry if it takes a while for the pods to appear on the Dev Cluster. Sometimes it takes longer to initials the Amazon RDS.*

You can now head to the [Dev Cluster](https://dev.rdu2c.fabric8.io:8443/) and play with the project in the OpenShift.

Once you no longer need the Analytics deployment, run

```bash
./cleanup.sh
```

<br>

 ## Stack Analyses - Kronos

 You might want to deploy stack analyses localy as well (although that's not what we typicaly do, since it requires some data in order to perform, OpenShift is a better solution ;)).
 In order to to that, you should clone the [fabric8-analytics-stack-analysis](https://github.com/fabric8-analytics/fabric8-analytics-stack-analysis) repository.