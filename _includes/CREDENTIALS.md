# Credential Guide

<br>

## Bayesian

Yes, that's our project :) And you still have no access to DSaas and Bayesian, submit a request to the [GitLab].\
[Here](https://gitlab.cee.redhat.com/dtsd/housekeeping/issues/1024) is an example of the form of the request.

<br>

## Dev Cluster

Firstly, since you most certainly want to deploy your application to the [Dev Cluster], you need the credentials for that.

You should request the access at the GitLab. [Here](https://gitlab.cee.redhat.com/dtsd/housekeeping/issues/1025) is an example of the form of the request.

<br>

## [GitHub]

1) [GitHub] account
2) Two factor authentication

You need to set up two factor authentication on [GitHub] for security purposes. You can find the settings on the [Git Hub Security](https://github.com/settings/security) page.

3) Fabric8-Analytics

The [GitHub] token is called in the env files as `GITHUB_API_TOKENS` and it is an OAuth Token can be generated at the [GitHub settings](https://github.com/settings/tokens) page.

<br>

## [AWS] (Amazon Web Services)

1) [AWS] Access

Request the [AWS] acces on [GitLab]. [Here](https://gitlab.cee.redhat.com/dtsd/housekeeping/issues/1026) is an example of such request.

2) [AWS] Credentials


Head to the [AWS website](https://console.aws.amazon.com/) and log in with your login details.
In the sub-menu on the left, go to the `Users` tab, click to your name there.
A new sub-window appears. The tab you are looking for is called `Security Credentials`.\
There you can create your Access Key ID, which we refer to in the environment files as `AWS_ACCESS_KEY_ID`

To create an access key, choose `Create Access Key`. Then choose `Download Credentials` to save the access key ID and secret access key to a CSV file on your computer. Store the file in a secure location. **WARNING: You will not have access to the secret access key again after this dialog box closes.**\
After you have downloaded the CSV file, choose `Close`.

For more information take a look at the [AWS guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html?icmpid=docs_iam_console).

<br>

## PostgreSQL/RDS

You can simply generate the password for the database using `pwgen` command.
Simply by issuing:

```bash
pwgen -1cs 32
```

Don't forget to save it though!

<br>

## OpenShift.io

An OpenShift.io API token is required in order to make recommendations when accessing API running on OpenShift, in the environment files, it is refered to it as `RECOMMENDER_API_TOKEN`. It can be found on the [openshift.io](https://openshift.io/) Profile -> Update Profile page

<br>

## Libraries.io

It is pretty easy to set up Librearies.io credentials. Just jump to the official site.

<br>

## [GitHub] OAuth App

Last step is to create a [GitHub] OAuth App. This is a little bit tricky.
First, you need to access the [developer GitHub settings](https://github.com/settings/developers$) and `Register a new Application`.
There you should set up the configuration for the new OAuth app.

`Application Name`

<input value="My OAuth App" disabled/>

`Homepage URL`

<input style="width: 450px;" value="http://bayesian-jobs-${OC_USERNAME}-fabric8-analytics.dev.rdu2c.fabric8.io/" disabled/>

> Remember the Dev Cluster credentials? Use the `OC_USERNAME` here .

`Application description`

<textarea style="width: 450px;" disabled>Application description is optional.</textarea>

`Authorization callback URL`

<input style="width: 450px;" value="http://bayesian-jobs-${OC_USERNAME}-fabric8-analytics.dev.rdu2c.fabric8.io/api/v1/authorized" disabled/>

> And here as well.


<br>

When you create the application, you should see a page with `Client ID` and `Client Secret`.
These are two env variables called `GITHUB_OAUTH_CONSUMER_KEY` and `GITHUB_OAUTH_CONSUMER_SECRET`, respectively.

<br>

---

And that's it ... now you should be able to deploy the application to the [Dev Cluster]. You can now proceed with the [deployment guide](./DEPLOYMENT.md).


[AWS]:(https://aws.amazon.com/)
[Dev Cluster]:(https://dev.rdu2c.fabric8.io:8443/console/)
[GitLab]:(https://gitlab.cee.redhat.com)
[GitHub]:(https://github.com/)