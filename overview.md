# Tanzu Application Platform v1.0

## <a id='overview'></a> Overview of Tanzu Application Platform

<p class="note warning">
<strong>Warning:</strong> Tanzu Application Platform is currently in beta (intended for evaluation and test purposes only).
</p>

VMware Tanzu Application Platform delivers a superior developer experience for enterprises building and deploying cloud native applications on Kubernetes. It enables application teams to get to production faster by automating source to production pipelines. It clearly defines the roles of developers and operators so they can work collaboratively and integrate their efforts.

The Tanzu Application Platform includes elements that enable developers to quickly begin building and testing applications regardless of their familiarity with Kubernetes. Operations teams can create application scaffolding templates with built-in security and compliance guardrails, making those considerations mostly invisible to developers. Starting with the templates, developers turn source code into a container and get a URL to test their app in minutes. Once the container is built, updating it happens automatically every time there’s a new code commit or dependency patch. And connecting to other applications and data, regardless of how they’re built or what kind of infrastructure they run on, has never been easier, thanks to an internal API management portal.

![TAP conceptual value](images/tap-conceptual-value.png)

Customers can simplify workflows in both the inner loop and outer loop of Kubernetes-based app development with Tanzu Application Platform while creating supply chains.

* **Inner Loop**:
    - The inner loop describes a developer’s development cycle of iterating on code.
    - Inner loop activities include coding, testing, and debugging before making a commit.
    - On cloud-native or Kubernetes platforms, developers in the inner loop often build container images and connect their apps to all necessary services and APIs to deploy them to a development environment.

* **Outer Loop**:
    - The outer loop describes how operators deploy apps to production and maintain them over time.
    - On a cloud-native platform, outer loop activities include building container images, adding container security, and configuring continuous integration and continuous delivery (CI/CD)  pipelines.
    - Outer loop activities are challenging in a Kubernetes-based development environment due to app delivery platforms being constructed from various third-party and open source components with numerous configuration options.

* **Supply Chains and choreography**:

Tanzu Application Platform uses the choreography pattern inherited from the context of microservices[^1] and applies it to continuous integration and continuous deployment (CI/CD) to create a path to production.[^2]

[^1]: https://stackoverflow.com/questions/4127241/orchestration-vs-choreography
[^2]: https://tanzu.vmware.com/developer/guides/supply-chain-choreography/

Supply Chains provide a way of codifying all of the steps of your path to production, or what is more commonly known as CI/CD. A supply chain differs from CI/CD in that you can add any and every step that is necessary for an application to reach production or a lower environment.

![Diagram depicting a simple path to production: CI to Security Scan to Build Image to Image Scan to CAB Approval to Deployment.](images/path-to-production.png)

In order to address the developer experience gap, the path to production allows users to create a unified access point for all of the tools required for their applications to reach a customer-facing environment. Instead of having four tools that are loosely coupled to each other, a path to production defines all four tools in a single, unified layer of abstraction. Where tools typically aren’t able to integrate with one another and additional scripting or webhooks are necessary, a unified automation tool codifies all the interactions between each of the tools.


Tanzu Application Platform provides a default set of components that automates pushing an app to staging and production on Kubernetes, removing the pain points for both inner and outer loops. In addition, it allows the operators to customize the platform by replacing Tanzu Application Platform components with other products.

![Diagram depicting the layered structure of TAP](images/tap-layered-capabilities.png)

The following packages are part of the Tanzu Application Platform:

- **Application Accelerator**
  The Application Accelerator component helps app developers and app operators through the creation and generation of application accelerators. Accelerators are templates that codify best practices and ensure important configurations and structures are in place from the start.

  Developers can bootstrap their applications and get started with feature development right away. Application operators can create custom accelerators that reflect their desired architectures and configurations and enable fleets of developers to utilize them, decreasing operator concerns about whether developers are implementing their desired best practices.

- **API Portal**

  API portal for VMware Tanzu enables API consumers to find APIs they can use in their own applications. Consumers can view detailed API documentation and try out an API to see if it will meet their needs. API portal assembles its dashboard and detailed API documentation views by ingesting OpenAPI documentation from the source URLs. An API portal operator can add any number of OpenAPI source URLs to be displayed in a single instance.

- **Tanzu Developer Tools for VSCode**

  Tanzu Developer Tools for Visual Studio Code is VMware Tanzu’s official IDE extension for VSCode to help you develop code using the Tanzu Application Platform The VSCode extension enables live updates of your application while it runs on the cluster and lets you debug your application directly on the cluster.

- **Tanzu Build Service**

  Tanzu Build Service uses the open-source Cloud Native Buildpacks project to turn application source code into container images. Build Service executes reproducible builds that align with modern container standards and additionally keeps images up to date. It does so by leveraging Kubernetes infrastructure with kpack, a Cloud Native Buildpacks Platform, to orchestrate the image life cycle. The kpack CLI tool, kp can aid in managing kpack resources. Build Service helps you develop and automate containerized software workflows securely and at scale.

- **Supply Chain Choreographer for Tanzu**

  Supply Chain Choreographer is based on open source [Cartographer](https://cartographer.sh/docs/). It allows App Operators to create pre-approved paths to production by integrating Kubernetes resources with the elements of their existing toolchains (e.g. Jenkins).
  Each pre-approved supply chain creates a paved road to production; orchestrating supply chain resources - test, build, scan, and deploy - allowing developers to be able to focus on delivering value to their users while also providing App Operators with the peace of mind that all code in production has passed through all of the steps of an approved workflow.

- **Supply Chain Security tools for Tanzu - Scan**

  With Supply Chain Security Tools for VMware Tanzu - Scan, Tanzu customers can build and deploy secure, trusted software that complies with their corporate security requirements. To enable this, Supply Chain Security Tools - Scan provides scanning and gatekeeping capabilities that Application and DevSecOps teams can easily incorporate earlier in their path to production. This is a known industry best practice for reducing security risk and ensuring more efficient remediation.

- **Supply Chain Security tools for Tanzu - Store**

  Supply Chain Security Tools - Store saves software bills of materials (SBoMs) to a database and allows you to query for image, source, package, and vulnerability relationships. It integrates with Supply Chain Security Tools - Scan to automatically store the resulting source and image vulnerability reports.

- **Convention Service**

  The convention service provides a means for people in operational roles to express their hard-won knowledge and opinions about how apps should run on Kubernetes as a convention. The convention service applies these opinions to fleets of developer workloads as they are deployed to the platform, saving operator and developer time.

- **Developer Conventions**

  Developer conventions configure workloads to prepare them for inner loop development. It’s meant to be a “deploy & forget” component for developers; once installed on the cluster through the Tanzu Package CLI, developers do not need to directly interact with it. Developers instead interact with the Tanzu Developer Tools for VSCode IDE Extension or Tanzu CLI Apps Plugin, which rely on the Developer Conventions to modify the workload to enable inner loop capabilities.

- **Flux Source Controller**

  The main role of the source management component is to provide a common interface for artifact acquisition. 

- **Grype**

  A vulnerability scanner for container images and filesystems.

- **Cloud Native Runtimes for Tanzu**

  Cloud Native Runtimes for Tanzu is a serverless application runtime for Kubernetes that is based on Knative and runs on a single Kubernetes cluster. For information about Knative, see the [Knative documentation](https://knative.dev/docs/) Cloud Native Runtimes capabilities are included in VMware Tanzu Advanced Edition and VMware Tanzu Application Platform.

- **Services Toolkit**

  The SCP Toolkit comprises a number of Kubernetes native components which support the management, lifecycle, discoverability, and connectivity of Service Resources (databases, message queues, DNS records, etc.) on Kubernetes.

- **Application Live View for VMware Tanzu**

  Application Live View is a lightweight insight and troubleshooting tool that helps application developers and application operators look inside running applications. It is based on the concept of Spring Boot Actuators.
  The fundamental idea is that the application provides information from inside the running processes via endpoints (in our case, HTTP endpoints). Application Live View uses those endpoints to get the data from the application and to interact with it.

- **Tekton**

  Tekton is a powerful and flexible open-source framework for creating CI/CD systems, allowing developers to build, test, and deploy across cloud providers and on-premise systems.

- **Tanzu Application Platform GUI**

  Tanzu Application Platform GUI lets your developers view your organization's running applications and services.
  It provides a central location for viewing dependencies, relationships, technical documentation, and even service status.
  Tanzu Application Platform GUI is built from the Cloud Native Computing Foundation's project Backstage.

## <a id='profiles-and-packages'></a>  Installation profiles and profiles in Tanzu Application Platform v1.0

Tanzu Application Platform is available through pre-defined profiles or individual packages.

The following profiles are available in Tanzu Application Platform:

- **Light:**
  Contains packages that drive the Inner Loop personal developer experience of building and
  iterating on applications.

- **Full:**
  This profile contains all of the Tanzu Application Platform packages.

## <a id='install'></a> About installing the Tanzu Application Platform v1.0

To install the Tanzu Application Platform profiles, see [Installing Tanzu Application Platform](install-intro.md).

## <a id='telemetry-notice'></a> Notice of telemetry collection for Tanzu Application Platform

[//]: # (This following text came from legal. Do not edit it.)

Tanzu Application Platform participates in VMware’s Customer Experience Improvement Program (CEIP).
As part of CEIP, VMware collects technical information about your organization’s use of VMware products and services
in association with your organization’s VMware license keys.
For information about CEIP, see the [Trust & Assurance Center](http://www.vmware.com/trustvmware/ceip.html).
You may join or leave CEIP at any time.
The CEIP Standard Participation Level provides VMware with information to improve its products and services,
identify and fix problems, and advise you on how to best deploy and use VMware products.
For example, this information can enable a proactive product deployment discussion with your VMware account team or
VMware support team to help resolve your issues.
This information cannot directly identify any individual.

[//]: # (The text above came from legal. Do not edit it.)

You must acknowledge that you have read VMware’s CEIP policy before you can proceed with the installation.
For more information, see [Install a Tanzu Application Platform profile](install.md#install-profile) in
_Installing part II: profiles_.
To opt out of telemetry participation after installation, see [Opting out of telemetry collection](opting-out-telemetry.md).
