# devexp

**Tell me about yourself:**

I’m a DevOps Engineer with around 4 years of experience in cloud operations and DevOps. I began my career with Accenture, where I worked in a centralized CloudOps team managing cloud provisioning, incident response, and DR drills. In 2024, I transitioned to TCS as a DevOps Engineer, where I’m currently leading a critical migration project for a banking client — moving from OpenShift to Standard Chartered Kubernetes Engine (SKE).
I specialize in tools like Azure DevOps, Docker, Kubernetes, Helm, Terraform, and Azure Cloud. I’ve built and optimized CI/CD pipelines, automated infrastructure with Terraform, and enabled secure deployments using HashiCorp Vault integration. I’ve also worked on database migrations, Ingress with TLS, and created custom BASH scripts to automate daily tasks.
I hold AZ-104 and AZ-900 certifications, and I was honored with two “Best People” awards for impactful contributions. My future goal is to upskill in AI/ML and integrate those capabilities into intelligent DevOps automation.

**Project:**

The Notification Hub is a critical microservices-based application responsible for dispatching real-time notifications like OTPs, SMS, push notifications, and soft tokens to millions of users. The application is built using Java, containerized via Docker, and deployed on OpenShift in the legacy setup and SKE in the new one using Helm charts and Azure DevOps CI/CD pipelines.
From an architecture standpoint, we follow a standard ingress → service → pod model. External apps connect to NH via Solace message queues — these requests are processed and routed to downstream systems. For emails and SMS, we pass messages to the MDIS platform, which then relays them to the SMTP server and telco gateways. For push notifications, we integrate with FCM (Android) and APNS (iOS) using a secure proxy for outbound traffic.
We’ve set up TLS ingress termination, network policies for access control, HPA for autoscaling, and Vault integration for secret management. Infra is provisioned through manifest files (compute_mf, firewall_mf, container_mf) and deployed via Azure DevOps.


1. Migration from OpenShift to SKE & CI/CD Setup in Azure DevOps
    1. What challenges did you face while migrating workloads from OpenShift to SKE?
    2. How did you handle differences in ingress controllers between OpenShift and SKE?
    3. What changes were required in your Helm charts during the migration?
    4. How did you provision and isolate the 6+ namespaces in SKE?
    5. How did you manage RBAC and user access in each namespace post-migration?
    6. What tools or manifests did you use to recreate firewall rules and compute resources in SKE?
    7. How did you ensure zero-downtime or minimal impact during the migration?
    8. How did you validate application health post-migration across environments?
    9. What role did Azure DevOps play in this migration? How was the pipeline structured?
    10. How did you manage secrets across environments while switching to SKE?

2. CI/CD Pipeline Creation in Azure DevOps for Java App
    1. Can you walk me through your CI/CD pipeline flow in Azure DevOps?
    2. What were the stages defined in your YAML pipeline for CI and CD?
    3. How did you handle deployment approvals and environment-specific variables?
    4. How did you manage rollback in case of deployment failure?
    5. What triggers did you set for pipeline execution (push, tag, PR)?
    6. How did you build and store Docker images — which registry did you use?
    7. How was the Helm deployment integrated in your CD stage?
    8. How did you optimize pipeline runtime to achieve the 30% improvement?
    9. How did you monitor pipeline health and handle flaky builds?
    10. Did you use templates or parameterized pipelines? How?

3. Kubernetes Security via Checkov & Helm Chart Hardening
    1. What is Checkov, and how did you integrate it into your CI/CD process?
    2. What kinds of vulnerabilities did Checkov typically detect in your Helm charts?
    3. Can you give examples of 3 critical findings and how you resolved them?
    4. How did you enforce image pull policies or restrict privilege escalation via Helm?
    5. How did you ensure secrets weren’t hardcoded in values.yaml?
    6. What was your approach for securing service accounts and role bindings?
    7. Did you define PodSecurityContext in your Helm charts? How?
    8. How did you validate the fixed Helm charts before pushing to production?
    9. How often did you scan the Helm charts — per PR, daily builds?
    10. How did you ensure Checkov compliance is followed by other developers?

4. Kubernetes Resource Optimization (Requests & Limits)
    1. Why is it important to set resource requests and limits in Kubernetes?
    2. How did you determine the right values for CPU/memory per pod?
    3. What tools or metrics did you use to analyze current resource consumption?
    4. What was the impact of over-provisioning in your project before optimization?
    5. How did you apply these changes across 6+ environments without disruption?
    6. What’s the risk of setting memory requests too low or too high?
    7. Did you use LimitRanges or ResourceQuotas at the namespace level?
    8. How did you test and tune requests and limits iteratively?
    9. How does HPA work with requests/limits? Did you make any adjustments?
    10. Can you show a sample values.yaml snippet where you tuned resources?

5. Custom BASH Scripts for Troubleshooting
    1. Can you describe a BASH script you wrote to fetch pod logs?
    2. What were the inputs and outputs of your log script?
    3. How did you parameterize namespaces or pod names in your script?
    4. Did you integrate the script with your pipeline or use it manually?
    5. How did you ensure the script worked across multiple environments?
    6. How do you handle stale pod names or crashlooped pods in the script?
    7. Did you add color-coded outputs or logging to your script?
    8. How did this script reduce the time spent on troubleshooting?
    9. Did you store these scripts in version control and share with the team?
    10. How would you convert your BASH script into a more scalable CLI tool?

6. Diagnosed 100+ Deployment Issues via CI/CD Analysis
    1. What were the most common reasons for deployment failures?
    2. How did you trace and debug Helm deployment failures?
    3. Can you explain how you debugged an “ImagePullBackOff” error?
    4. How did you use pipeline logs to diagnose YAML or container issues?
    5. How did you reduce repeat issues and build long-term solutions?
    6. What dashboards or tools helped you visualize pipeline success/failure?
    7. How did you collaborate with developers during triaging?
    8. Did you create postmortem documents or RCA reports?
    9. What’s the process for rollback or hotfix deployment in your team?
    10. Share a tough issue you resolved that helped improve your team's velocity.

7. Kubernetes Orchestration Efficiency
    1. What optimizations did you apply to speed up deployments?
    2. How did parallelizing steps in pipelines help with speed?
    3. Did you modify readiness/liveness probes to reduce startup time?
    4. Did you enable pre-pulled images or image caching?
    5. How did Helm chart structure affect your deployment time?
    6. How did HPA tuning affect pod startup/termination speed?
    7. Did you leverage rolling updates or blue/green deployments?
    8. How did you batch deploy multiple services to avoid delay?
    9. What were the before/after metrics that proved 40% time savings?
    10. How did reduced deployment time affect your release cycle or SLAs?

8. Solace MQ Integration for SMS & Email
    1. What is Solace, and how does it differ from Kafka or RabbitMQ?
    2. Can you explain how Solace topics and queues are used in your project?
    3. How did you configure Solace connectivity (truststore, keystore) from your app?
    4. What kind of payloads were sent via Solace topics (for SMS/email)?
    5. How did you ensure message delivery reliability in Solace?
    6. What happens if the downstream MDIS system is down — how is retry handled?
    7. How did you segregate topics for SMS and Email — were they static or dynamic?
    8. Did you use Solace PubSub+ Event Portal or CLI for setup?
    9. How did you test and validate end-to-end message flow in lower environments?
    10. Did you implement any monitoring or dead-letter queue strategy for failed messages?

9.  Database Migration from Oracle to PostgreSQL
    1. What were the key challenges while migrating from Oracle to PostgreSQL?
    2. How did you handle Oracle-specific functions or data types during migration?
    3. What tool(s) did you use for schema/data migration — ora2pg, DMS, etc.?
    4. How did you provision a shared PostgreSQL DB for multiple applications?
    5. Why did you choose schema-level isolation instead of DB-level separation?
    6. How did you manage credentials securely while connecting from pods?
    7. How was rollback planned in case of migration failure?
    8. What was your approach to validating data integrity post-migration?
    9. Did you perform performance tuning for PostgreSQL after migration?
    10. How did you test connectivity from the SKE pods to private DB?

10. NGINX Ingress with TLS Termination & Routing
    1. What is TLS termination and where did it happen in your architecture?
    2. How did you create and manage TLS certificates — manually or via cert-manager?
    3. How did you configure path-based routing in Ingress — can you give an example?
    4. How did you ensure secure communication between client and pod?
    5. How did you configure annotations or config maps for NGINX?
    6. Did you use Ingress class or default ingress controller?
    7. How did you handle 404/502 errors in NGINX?
    8. What’s the difference between Layer 4 and Layer 7 load balancing, and which applies here?
    9. How did you test and validate the routing behavior across environments?
    10. Did you use Helm to deploy NGINX ingress and TLS resources?

11. Namespace, Firewall, and INC Provisioning via Manifests
    1. What are the benefits of isolating environments by namespaces in Kubernetes?
    2. What did your compute_mf, firewall_mf, and network_mf manifest files contain?
    3. How were firewall rules implemented — was there a request workflow?
    4. How did you manage naming conventions and labels across the 6 namespaces?
    5. What were the steps to get INC approved for access provisioning?
    6. How did you use network policies to restrict inter-namespace traffic?
    7. How was resource quota configured per namespace?
    8. How did you manage service accounts and RBAC roles within each namespace?
    9. Did you use Terraform or YAML for these manifests?
    10. How did you audit and monitor namespace resource usage?

12. Helm Chart Reusability Across Environments
    1. What made your Helm charts reusable across environments?
    2. How did you manage values.yaml overrides per environment?
    3. What structure did you follow for your Helm chart directories (templates, charts, values)?
    4. How did you parameterize secret mounts, config maps, or env variables?
    5. Can you share an example of a condition or loop you used in Helm templates?
    6. How did you use .Release.Name, .Values, or lookup functions in your charts?
    7. Did you version and publish Helm charts to a central repository?
    8. How did you validate charts locally before pushing them to ADO pipelines?
    9. How did you structure Helm chart folders for microservices vs monolithic apps?
    10. How did Helm improve deployment consistency compared to plain YAMLs?

13. Proxy Configuration for Outbound Restrictions
    1. What was the need for proxy implementation in your environment?
    2. How did you configure proxy settings in pod-level deployments?
    3. How did you whitelist certain outbound domains/IPs?
    4. Did you use init containers or sidecars to enforce proxy policies?
    5. What security benefits were gained through this proxy setup?
    6. How did you handle DNS resolution or non-proxy domains (no_proxy)?
    7. How did the app handle HTTPS traffic via proxy — any cert issues?
    8. How was proxy routing validated — did you simulate or sniff network calls?
    9. Did the proxy affect performance or latency — how did you measure?
    10. How did you rotate or update proxy configurations across deployments?

14. HCV & Library Integration in ADO Pipelines

    1. How did you authenticate ADO pipelines to HashiCorp Vault?
    2. Did you use Vault Agent Injector or direct API calls for secrets injection?
    3. How did you pass secrets dynamically to Helm charts during deployment?
    4. What was the format of secrets in HCV — KV v1 or v2?
    5. How did you reduce manual secret updates through this integration?
    6. How was access control enforced for different teams/environments in Vault?
    7. Did you face any TTL or lease issues with secrets in pipelines?
    8. What is the difference between HCV and Azure Key Vault, and why HCV?
    9. How did you audit secret access or detect failed secret retrievals?
    10. Did you cache secrets in pipelines, or pull them fresh every time?

15. HPA Using CPU Metrics for Resource Optimization

    1. How did you configure Horizontal Pod Autoscaler in your Kubernetes cluster?
    2. What metrics server or adapter did you use for CPU utilization?
    3. How did you choose min/max replica settings?
    4. What was the threshold percentage for scaling out/in?
    5. How did you monitor HPA behavior — did you use Prometheus/Grafana?
    6. Can you explain how HPA differs from VPA or Cluster Autoscaler?
    7. What issues did you face during initial HPA configuration?
    8. How did you test the effectiveness of HPA under varying load?
    9. Did you observe any thrashing behavior — how was it mitigated?
    10. How did HPA affect cost, latency, or performance in production?


16. Terraform-based Infra Provisioning with High Availability
    1. What Terraform version and provider (e.g., AzureRM) did you use in this project?
    2. How did you ensure idempotency and avoid drift during Terraform deployments?
    3. How did you manage Terraform state — did you use remote backends like Azure Blob?
    4. How did you implement high availability (HA) in the infrastructure provisioned via Terraform?
    5. Did you use Terraform modules or a monolithic .tf approach?
    6. How did you handle dependencies between resources (e.g., VNet before VM)?
    7. Can you walk through a sample main.tf or a resource block for a VM or AKS?
    8. How did you automate Terraform execution in Azure DevOps pipelines?
    9. How did you validate your Terraform plan before applying it?
    10. What naming conventions or tagging strategy did you use for manageability?

17. Qualys Vulnerability Management & SLA Compliance
    1. What is Qualys and how did you integrate it into your Azure environment?
    2. What kinds of vulnerabilities were mostly found — OS-level, library-level, or network?
    3. How did you prioritize vulnerabilities — by CVSS score or by asset criticality?
    4. How was Qualys configured — agent-based or agentless scans?
    5. What was your remediation workflow after identifying a vulnerability?
    6. How did you track SLA compliance for vulnerability fixes?
    7. Did you create automated notifications or dashboards from Qualys scan results?
    8. How frequently were scans scheduled — daily, weekly, or triggered manually?
    9. Did you integrate Qualys with ITSM tools like ServiceNow or Jira?
    10. How did you verify that a vulnerability was actually remediated?

18. Disaster Recovery Strategy and RTO Optimization
    1. What does RTO mean and how is it calculated?
    2. What tools did you use to simulate a switchover event?
    3. What were the primary applications or services covered under DR?
    4. What was your DR strategy — active-passive or active-active?
    5. How was DNS or traffic redirection handled during switchover?
    6. How did you document the DR runbooks and validate them?
    7. What Azure services did you rely on for cross-region DR?
    8. How often were DR drills conducted, and how were they reported?
    9. What was your failback strategy after a DR drill?
    10. What challenges did you face in syncing data/state across primary and DR sites?

19. Application-level ASR (Azure Site Recovery)
    1. What is Azure Site Recovery and how does it work at a high level?
    2. For which workloads or app tiers did you enable ASR — VMs, DBs, app servers?
    3. How did you test failover and failback using ASR?
    4. What were the RTO and RPO goals, and how were they achieved?
    5. How was replication traffic managed across regions — any bandwidth throttling?
    6. Did you face any compatibility issues while enabling ASR?
    7. How did ASR integrate with automation tools or pipelines?
    8. How did you handle encryption and data security during replication?
    9. What alerting or monitoring did you set up for ASR health?
    10. How did you document and train others on ASR usage?

20. ADO + Azure Key Vault Integration for Secret Management
    1. How did you configure Azure DevOps pipelines to access secrets from Azure Key Vault?
    2. What kind of secrets were stored — client IDs, secrets, passwords, tokens?
    3. Did you use Key Vault Task in YAML or ARM template with linked secrets?
    4. How did you restrict access to Key Vault — RBAC or access policies?
    5. Did you face throttling or permission issues while retrieving secrets?
    6. How did you rotate secrets securely without pipeline downtime?
    7. How did you audit secret usage and access patterns?
    8. How did you parameterize secrets in Terraform using Key Vault?
    9. How did you manage Key Vault across different environments (dev, test, prod)?
    10. What are some limitations of Azure Key Vault you faced during automation?

21. Azure Vulnerability Management
    1. What tools (besides Qualys) did you use for vulnerability detection?
    2. How did you manage vulnerability remediation across multiple subscriptions?
    3. What was your strategy for patching — automated, scheduled, or manual?
    4. How did you prioritize remediation tasks for critical systems?
    5. How did you ensure least privilege while remediating?
    6. What reporting tools were used to showcase remediation metrics?
    7. How did you collaborate with app teams to avoid downtime while patching?
    8. Were third-party applications also covered in vulnerability scans?
    9. What kinds of false positives did you face and how were they handled?
    10. Did you integrate vulnerability findings into security dashboards or compliance reports?

22. Cross-functional Incident Troubleshooting
    1. How did your team track and manage incidents — Jira, ServiceNow, or other tools?
    2. What role did you play in the troubleshooting lifecycle — L1, L2, or L3?
    3. How did you ensure quick MTTR (Mean Time to Resolve)?
    4. How were RCA (Root Cause Analysis) documents maintained?
    5. What were the most common types of incidents you resolved?
    6. How did you collect logs from Azure or Kubernetes for analysis?
    7. Did you use any observability tools — Application Insights, Prometheus, etc.?
    8. Can you give an example of a high-priority incident and how you resolved it?
    9. How did you prevent recurrence of similar issues?
    10. How was the success of incident response measured and reviewed?
23. Agile Collaboration in Stand-ups, Sprints
    1. What was the team structure in your Agile project — devs, testers, ops?
    2. How often did you participate in stand-ups and what was your typical update?
    3. How were DevOps tasks planned and tracked in sprints?
    4. Did you face scope creep or misalignment — how was it handled?
    5. What tools did you use — Azure Boards, Jira, Confluence?
    6. How did retrospectives help you improve release processes?
    7. How did you contribute to sprint planning for infrastructure tasks?
    8. How did Agile ceremonies help in faster incident resolution?
    9. Can you give an example of process improvement you suggested in a retro?
    10. What KPIs or metrics were tracked for DevOps sprint tasks?

24. Azure Infra Provisioning via Terraform
    1. What resources did you provision in Azure — AKS, VM, VNet, NSG, etc.?
    2. How did you ensure environment isolation — separate VNet or subscriptions?
    3. What kind of security controls did you configure using Terraform?
    4. Did you use service principals or managed identities in Terraform providers?
    5. How did you apply tagging and naming standards consistently?
    6. How did you structure your .tf files and modules?
    7. How did you handle Terraform plan and apply stages in CI/CD?
    8. How did you validate post-provisioning security and access rules?
    9. What strategies did you use to reuse modules across multiple apps?
    10. How was access managed for teams who wanted to make Terraform changes?

25. Terraform Creation & Infra Provisioning)
    1. Write a Terraform file to create an Azure Virtual Machine with a public IP and NSG.
    2. Add a Terraform resource to attach a disk to the VM you created above.
    3. How do you use Terraform variables and output in the VM creation file? Show an example.
    4. Write a Terraform module for reusable VM provisioning.
    5. How do you implement remote backend state management in Terraform?
    6. How did you secure your .tfvars in Azure DevOps pipeline?
    7. Draft a terraform.tfvars for a dev environment with image, size, and subnet inputs.
    8. Add a count loop to deploy 3 identical VMs using Terraform.
    9. How do you reference existing resource group and VNET in Terraform without recreating them?
    10. Show how to write a conditional resource block (e.g., create NSG only for prod).

26. PostgreSQL Scripts (Database & Schema Tasks)
    1. Write a SQL script to create a PostgreSQL database, schema, and a table with constraints.
    2. Create a notify_user table with columns for ID, email, phone, and notification type.
    3. Write a script to migrate data from Oracle to PostgreSQL (e.g., using COPY with CSV).
    4. How do you handle schema-level access control in PostgreSQL? Write a sample GRANT command.
    5. Write a script to create 3 schemas for different NH modules in the same database.
    6. Write SQL to list all tables under a specific schema.
    7. How do you create an index on a column in PostgreSQL?
    8. Write a script to fetch all failed notifications from notify_log table in last 24 hrs.
    9. Explain how you tested data integrity post-migration.
    10. Write a script to delete test data older than 7 days from multiple tables.

27. Bash Scripts (Automation & NH API Performance Testing)
    1. Write a Bash script to hit NH's /notify/send endpoint in a loop for 5000 requests.
    2. Add error handling and logging to the above script.
    3. Write a script to collect pod logs for all pods in a given namespace.
    4. Write a Bash script to list Kubernetes deployments in all namespaces.
    5. Write a script that runs helm upgrade for multiple environments.
    6. Add parallel execution to your NH API testing script for better load simulation.
    7. Script to monitor free memory and alert if below 500MB.
    8. Bash script to check which container is consuming high CPU in a pod.
    9. Schedule a script via cron that exports database size to a file every hour.
    10. Script to clean up Helm releases, dangling images, and unused PVCs.

28. Azure DevOps CI/CD Pipeline (YAML)
    1. Write an Azure DevOps pipeline YAML to:
        ○ Build a Java app using Maven
        ○ Build Docker image
        ○ Push to ACR
        ○ Deploy to Kubernetes using Helm
    2. Add approval gate before deploying to production in YAML.
    3. How do you pass secrets from Azure Key Vault in your YAML pipeline? Show syntax.
    4. Split your pipeline into stages: build, test, deploy with dependsOn.
    5. How do you use template YAMLs in ADO for DRY principle? Show an example.

29. Helm Charts (Ingress, Service, Deployment, Secrets)
    1. Write a Helm deployment.yaml for NH pod with configurable image & replica count.
    2. Draft a service.yaml with port and selector details.
    3. Write an ingress.yaml that supports TLS and /notify path routing.
    4. Create a secrets.yaml template that accepts base64 values via values.yaml.
    5. Provide sample values-dev.yaml and values-prod.yaml files with different replica counts and Solace URLs.

30. Dockerfile (Multi-stage Build for Size Optimization)
    1. Write a multi-stage Dockerfile to build a Spring Boot app and keep the final image minimal.
    2. Explain why you use multi-stage builds and how it helped you reduce image size.
    3. How do you handle .jks file and keystore setup securely in your Docker image?
    4. Add a healthcheck instruction in your Dockerfile for NH.
    5. Write a Dockerfile that runs as a non-root user for security.


