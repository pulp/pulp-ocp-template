# ABOUT

This is a template to quick test or try [Pulp](https://pulpproject.org/).
> **WARNING**: Any data stored will be lost upon pod destruction. Only use this template for testing.

<br/>

# PRE-REQS
## "Registering" the template
To make this template available we first need to "register" it in `openshift` namespace:
```
$ oc apply -f pulp-template.yaml
```
This command will create a new template called `pulp-example`.
> **note**: make sure that you have permissions to create templates in `openshift` namespace

<br/>

# INSTALLING PULP THROUGH WEB CONSOLE

* In "*Developer*" view, select "*+Add*" then click on "*All Services*"  
<img src="images/pulp-1.png" width="800">

* Now search for "*pulp*" template and select it  
<img src="images/pulp-2.png" width="800">

* A new panel will open on the right side of the screen. Click "*Instatiate Template*"  
<img src="images/pulp-3.png" width="800">

* The last step is to define in which namespace **Pulp** should be provisioned  
<img src="images/pulp-4.png" width="800">

<br/>

# INSTALLING PULP THROUGH COMMAND LINE

* [optional] Create a new namespace to run pulp
```
$ oc new-project test-pulp
```

* Deploy pulp
```
$ oc new-app pulp-example
```

<br/>

# CHECKING INSTALLATION

## Through command line
* verify if all pods are in a running state
```
$ oc get pods
NAME                                    READY   STATUS    RESTARTS   AGE
example-pulp-api-79454fdbf9-7bgv8       1/1     Running   0          3m38s
example-pulp-content-7cbf4b4589-gnz58   1/1     Running   0          3m38s
example-pulp-database-0                 1/1     Running   0          3m35s
example-pulp-web-96cb4cd55-5v2tw        1/1     Running   0          3m38s
example-pulp-worker-5d7c9685c-7g8rk     1/1     Running   0          3m38s
```

* check the /status endpoint
```
$ oc exec deployment/example-pulp-api -- curl -s localhost:24817/pulp/api/v3/status/|jq
```

## Through web console

* from "*Topology*" view all deployments (`api`,`content`,`worker`,`database`,`web`) should be surrounded with a "dark blue" circle  
<img src="images/pulp-5.png" width="800">
