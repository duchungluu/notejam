****************
Notejam: Express
****************

Notejam application implemented using `Express.js <http://expressjs.com/>`_ microframework.

Express version: 4.2

Middlewares/extentions used:

* `Passport.js <http://passportjs.org/>`_ for authentication
* `Node ORM 2 <https://github.com/dresende/node-orm2>`_ for database
* `Mocha <http://mochajs.org/>`_ and `Superagent <http://visionmedia.github.io/superagent/>`_ for testing
* ... and `others <https://github.com/komarserjio/notejam/blob/express/express/notejam/package.json>`_

==========================
Installation and launching
==========================

-------
Cloning
-------

Clone the repo:

.. code-block:: bash

    $ git clone git@github.com:komarserjio/notejam.git YOUR_PROJECT_DIR/

-------------------
Install environment
-------------------
Use `npm <https://www.npmjs.org/>`_ to manage dependencies.

Install dependencies

.. code-block:: bash

    $ cd YOUR_PROJECT_DIR/express/notejam/
    $ npm install

Create database schema

.. code-block:: bash

    $ cd YOUR_PROJECT_DIR/express/notejam/
    $ node db.js

------
Launch
------

Start built-in web server:

.. code-block:: bash

    $ cd YOUR_PROJECT_DIR/express/notejam/
    $ DEBUG=* ./bin/www

Go to http://127.0.0.1:3000/ in your browser

------------------
Running unit tests
------------------

Run unit tests:

.. code-block:: bash

    $ cd YOUR_PROJECT_DIR/express/notejam/
    $ ./node_modules/mocha/bin/mocha tests

============
Contribution
============

Please send your pull requests in the ``master`` branch.

Always prepend your commits with a framework name:

.. code-block:: bash

    Express: Implemented sign in functionality


============
2021 Update
============


# Serverless Deployment on GCP


## Tech stack: Node ExpressJs, Sqlite, Cloud Run, Terraform, Container Registry, Docker, GKE, Kubernetes

### Implementation:

.. Preq: GCP service account, Docker, K8s, node, editor
.. 

0. Add Dockerfile + .dockerignore to create Docker image

1. Create and push Docker image to Container Registry    
```
    $gcloud builds submit --tag gcr.io/<project-id>/gke-test-image:v1 .
```
2. Create new GKE cluster to run the web app
 ```   $gcloud container clusters create gke-test-cluster --disk-size 10 --num-nodes 2 --enable-autoscaling --min-nodes 2 --max-nodes 5 --zone europe-north1-a
```
3. Deploy Docker image to the GKE cluster
 ```$kubectl create deployment gke-test-app --image=gcr.io/<project-id>/gke-test-image:v1 -replicas=3 --cpu-percent=80 --min=1 --max=5
    $kubectl scale deployment gke-test-app --replicas=3
    $kubectl autoscale deployment gke-test-app --cpu-percent=80 --min=1 --max=5
```
   Create LoadBalancer to expose the service to the Hello, World! 
```    $kubectl expose deployment gke-test-app --name=test-app-service --type=LoadBalancer --port 80 --target-port 3000 
```

3.1. Infra aas 
    Reserve Static IP
        gcloud compute addresses create gke-tutorial-ip
    Create Kubernetes service
        deployment.yaml ingress.yaml service.yaml podscaler.yaml
    Apply the service
        kubectl apply -f k8s/

n. Clean Up
    kubectl delete service gke-test-app
    gcloud container clusters delete gke-test-cluster
    gcloud container images delete gcr.io/${PROJECT_ID}/gke-test-image:v1  --force-delete-tags --quiet
 


# TO DO :rocket:


1. Refactoring the code to JS 2017, update libraries

2. Decouple the frontend and backend, deprecate Sqlite, use GCP Cloud SQL.

3. More automation