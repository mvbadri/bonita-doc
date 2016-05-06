# 2.4.7 Two main types of deployment

**Note: **It is highly recommended to use the provided Tomcat or JBoss bundles or the artifacts `bonita.war` and `bonita.ear` provided in the deploy bundle, in order to carry out these deployments successfully.

There are two main types of deployment:

1. using a [local](#sameapp) Bonita BPM Engine
2. using a [remote](#http) Bonita BPM Engine.

## 1\. Bonita BPM Portal + Bonita BPM Engine on the same application server

![deploy1](images/images-6_0/poss_deploy1.png)

deploy1

This is the simplest deployment configuration. The BPM engine used is the one embedded in the webapp bonita.war. Using the pre-packaged Tomcat bundle is the easiest way to achieve this kind of deployment, but it is also possible to retrieve the `bonita.war` webapp provided in the **deploy.zip** and deploy it on another application server/servlet container.
It is fast because the Bonita BPM Portal and the Bonita BPM Engine run on the same JVM and so there is no serialization and network overhead every time the Bonita BPM Portal calls the engine.

**Advantages**

* simple (single webapp and application server)
* works out of the box if you use the provided Tomcat bundle
* you can still access the embedded Bonita BPM Engine API (or the Bonita BPM Portal REST API) through HTTP if you need an external application to access it
* improved performance

**Drawbacks**

* may not be adapted to some architecture constraints

## 2\. Bonita BPM Engine on a remote application server

Even if the `bonita.war` comes with an embedded Bonita BPM Engine, you can choose **not** to use it, by configuring `bonita-client.properties` in `BONITA_HOME`.

### 2.1 Accessible through HTTP

![deploy2](images/images-6_0/poss_deploy2.png)

deploy2

With this deployment, the Bonita BPM Engine is accessed by the portal (and possibly other applications) through HTTP. The Bonita BPM Portal is deployed on one application server and the engine on another one.
But you can still use the pre packaged Tomcat bundles or the `bonita.war` webapp provided in the **deploy.zip**, in both servers. On one of them, only the Bonita BPM Portal part will be used and on the other one, only the engine server. Access to the portal can be de-activated by server or webapp configuration if necessary.

**Advantages**

* may be adapted to some architecture and network constraints

**Drawbacks**

* more complex than the first deployment option (two application servers instead of one)
* impact on performance (serialization + network overhead)

### 2.2 Accessible through RMI (EJB3)

![deploy3](images/images-6_0/poss_deploy3.png)

deploy3

With this third type of deployment, the engine is accessed by the Bonita BPM Portal (and possibly other applications) through the EJB.
The Portal is deployed on one application server and the engine on another one.
However, you can still use the pre packaged Tomcat bundle for the Bonita BPM Portal and the pre-packaged JBoss Bundle for the Bonita BPM Engine.
In this case, you will need to add the JBoss client libraries to the classpath of the Bonita BPM Portal webapp. 
You can also use the bonita.war webapp provided in the deploy zip on the portal application server and use the bonita.ear application on the engine application server. 
On one of the application servers, only the portal part will be used and on the other one, only the engine server. 
Access to the Bonita BPM Portal can be deactivated by server or app configuration, if necessary.

**Advantages**

* may fit some architecture and network constraints

**Drawbacks**

* more complex than the first deployment option (two application servers instead of one)
* impact on performance (serialization + network overhead) but it should be faster than the second option though (no HTTP protocol overhead)