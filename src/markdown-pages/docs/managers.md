---
path: "/docs/managers"
title: "Managers"
---

You can find links to the Javadoc API documentation for all the Galasa Managers on the [overview page](https://javadoc.galasa.dev/).

## Managers provided with the current Galasa distribution

| Name | Description | 
| :------------------------ | :------------------------------------- | 
| **[Artifact Manager](/docs/managers/artifact-manager)**<br> ![release](../../images/release.svg)| Provides access to resources within a test bundle. It also provides templating services.|
| **[CECI Manager](/docs/managers/cics-ts-ceci-manager)**<br> ![beta](../../images/beta.svg) | Provides CECI 3270 interaction - initially supporting containers and link programs.|
| **Core Manager**<br> ![release](../../images/release.svg) | Provides tests with access to some of the most common features within the Galasa framework, such as the ability to retrieve credentials and the name of the test run. |
| **[Docker Manager](/docs/managers/docker-manager)**<br> ![release](../../images/release.svg) | Enables containers to run on infrastructure Docker engines - either for testing directly or for assisting the testing process. |
| **[ElasticLog Manager](/docs/managers/elasticlog-manager)**<br> ![alpha](../../images/alpha.svg) | Exports test results to ElasticSearch, which can be subsequently used within Kibana dashboards. |
| **[Galasa Ecosystem Manager](/docs/managers/galasa-ecosystem-manager)**<br>![alpha](../../images/alpha.svg) | Deploys an entire Galasa ecosystem to Kubernetes to enable integration testing against Galasa. |
| **HTTP Client Manager**<br> ![beta](../../images/beta.svg) | Provides a common setup of HTTP client operations for the test (or a Manager) to use. |
| **IP Network Manager**<br> ![alpha](../../images/alpha.svg) | Provides configuration information for IP-based servers. |
| **[JMeter Manager](/docs/managers/jmeter-manager)**<br>![beta](../../images/beta.svg) | Configures and runs JMeter testing via Docker containers.|
| **[Kubernetes Manager](/docs/managers/kubernetes-manager)**<br> ![alpha](../../images/alpha.svg) | Provisions Kubernetes namespaces for tests (or Managers) to use. |
| **Linux Manager**<br> ![alpha](../../images/alpha.svg) | Provides Linux server configuration properties. Drives provisioning by other Managers such as the OpenStack Manager. |
| **OpenStack Manager**<br> ![alpha](../../images/alpha.svg) | Provisions servers within OpenStack. This Manager currently only supports Linux and provides the servers via the Linux Manager. |
| **[Selenium Manager](/docs/managers/selenium-manager)**<br> ![beta](../../images/beta.svg) | Allows tests to drive Web Browser testing using Selenium.|
| **z/OS 3270 Manager**<br> ![alpha](../../images/alpha.svg)| Provides tests and Managers with a 3270 client.|
| **[z/OS Batch z/OS MF Manager](/docs/managers/z-os-batch-z-os-mf-manager)**<br> ![beta](../../images/beta.svg) | Provides the default implementation of the z/OS Batch Manager using z/OS MF. Can only be used via the z/OS Batch Manager interface. |
| **[z/OS Console z/OS MF Manager](/docs/managers/zos-console-zos-mf-manager)**<br> ![beta](../../images/beta.svg) | Provides the default implementation of the z/OS Console using z/OS MF. Can only be used via the z/OS Console Manager interface. |
| **[z/OS File z/OS MF Manager](/docs/managers/zos-file-zos-mf-manager)**<br> ![beta](../../images/beta.svg) | Provides the default implementation of the z/OS File Manager using z/OS MF. Can only be used via the z/OS File Manager interface. |
| **[z/OS Manager](/docs/managers/zos-manager)**<br> ![beta](../../images/beta.svg) | Provides tests and Managers with configuration information about z/OS images and Sysplexes. It offers services such as APF, DUMP, SMF and Log access. Additionally, the z/OS Manager provides access to the following annotations:<br> - **z/OS Batch** which enables tests and Managers to submit, monitor and retrieve z/OS batch jobs. See [BatchAccountsOpenTest](/docs/running-simbank-tests/batch-accounts-open-test) for a walkthrough of a test that employs this Manager.<br> - **z/OS Console** which allows tests and Managers to issue z/OS console commands.<br> - **z/OS File** which provides tests and Managers with the ability to transfer files to and from z/OS. Supported file types include Sequential, PDS, PDSE or KSDS.<br> - **z/OS TSO** which requests the z/OS Manager to provide a z/OS TSO instance associated with a z/OS image. <br> - **z/OS UNIX** which requests the z/OS Manager to provide a z/OS UNIX instance associated with a z/OS image. |   
| **[z/OS MF Manager](/docs/managers/zos-mf-manager)**<br> ![beta](../../images/beta.svg) | Provides tests and Managers with access to z/OS MF functions. It is used by the Batch, File and Console Managers by default. | 
| **[z/OS TSO Command SSH Manager](/docs/managers/zos-tso-command-ssh-manager)**<br> ![alpha](../../images/alpha.svg) | Provides the default implementation of the z/OS TSO Command Manager using SSH. Can only be used via the z/OS TSO Command Manager interface. |
| **[z/OS UNIX Command SSH Manager](/docs/managers/zos-unix-command-ssh-manager)**<br> ![alpha](../../images/alpha.svg) | Provides the default implementation of the z/OS UNIX Command Manager using SSH. Can only be used via the z/OS UNIX Command Manager interface. |


| Key |   | 
| :------------------------ | :------------------------------------- | 
| ![alpha](../../images/alpha.svg)| This Manager is being actively developed. It is subject to change and has not been extensively tested.|
| ![beta](../../images/beta.svg)| This Manager is almost ready.  It has been tested and the TPI is stable, but there may be minor changes to come.|
| ![release](../../images/release.svg)| This Manager is feature complete, has passed all tests and is deemed release grade.|


## Future Managers

| Name | Description | 
| ------------------------ | :------------------------------------- | 
| **AIX Manager** | Provisions AIX server configuration properties, and helps drive provisioning by other Managers such as the OpenStack Manager.|
| **Artifactory Manager** | Provides the ability to retrieve artifacts from Artifactory servers. |
| **CEMT Manager** | Provides CEMT 3270 interaction.|
| **CICS TS Manager** | Provides configuration information for pre-existing CICS TS servers. Drives provisioning services from other managers, e.g. z/OS PT.|
| **CICS z/OS PT Provisioning Manager** | Provisions CICS TS servers for the CICS TS Manager.|
| **GitHub Manager** | Enables tests to retrieve artifacts from GitHub and enables test results to be influenced by the status of issues.|
| **GitLab Manager** | Enables tests to retrieve artifacts from GitLab and enables test results to be influenced by the status of issues.|
| **IMS DB Manager** | Provisions and configures IMS DB subsystems.|
| **IMS TM Manager** | Provisions and configures IMS TM subsystems.|
| **ISPF Manager** | Provides a wrapper for the z/OS 3270 Manager to run ISPF sessions.|
| **Liberty Manager** | Provisions and configures Liberty servers.|
| **MongoDB Manager** | Provisions and configures MongoDB databases via Docker containers.|
| **Nexus Manager** | Provides the ability to retrieve artifacts from Nexus servers.|
| **OpenLDAP Manager** | Provides and configures OpenLDAP servers via Docker containers.|
| **RTC Manager** | Enables tests to retrieve artifacts from RTC, and allows test results to be influenced by the status of defects.|
| **TSO Manager** | Provides a wrapper for the z/OS 3270 Manager to run TSO sessions.|
| **UrbanCode Manager** | Provisions and configures UrbanCode servers.|
| **WAS Manager** | Provisions and configures Websphere Application Servers.|
| **Windows Manager** | Provides Windows server configuration properties, driving provisioning by other Managers such as the OpenStack Manager.|
| **WSIM Manager** | Provisions and configures Workload Simulator servers.|
| **z/Linux Manager** | Provides z/Linux server configuration properties, and drives provisioning by other Managers such as the z/VM Manager.|
| **z/OS Connect Manager** | Provides configuration information for z/OS Connect instances, and provisions z/OS Connect instances.|
| **z/OS DB2 Manager** | Providing configuration information to DB2 instances, this Manager also provisions DB2 instances and schemas.|
| **z/OS MQ Manager** | Provisions and configures z/OS MQ subsystems.|
| **z/OS Security Manager** | Creates and maintains userids and profiles in RACF.|
| **z/VM Manager** | Provisions and configures z/VM userids, mainly for provisioning z/OS and z/Linux systems.|
| **ZOWE Manager** | Provides configuration information for and provisions ZOWE instances.|
