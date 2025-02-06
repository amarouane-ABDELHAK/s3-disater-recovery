# Ansible with Github Actions

- Status: draft
- Deciders: [Iksha, Ajinkya]
- Date: [YYYY-MM-DD when the decision was last updated] <!-- optional. To customize the ordering without relying on Git creation dates and filenames -->
- Tags: [Deployment CICD]



## Context and Problem Statement

OASIS teams require a standardized and automated deployment process to efficiently manage and deploy applications. The current deployment practices lack consistency and automation, leading to inefficiencies and potential errors. The proposed solution is to use Ansible with GitHub Actions to automate and standardize the deployment process across all teams.

## Decision Drivers

- Consistency in Deployment Processes: Ensuring a standardized approach to application deployment across all teams.
- Automation and Efficiency: Reducing manual intervention and potential errors by automating the deployment process.
- Flexibility and Control: Allowing teams to define their deployment processes while maintaining organizational control over environments.
- Cost-Effectiveness: Utilizing open-source tools to minimize additional costs while avoiding the need to maintain any service.
- Reusability of Deployment Logic: Facilitating the reuse of the deployment logic and roles across various projects to save time and effort.

## Considered Options

- Ansible with GitHub Actions: Automating Playbook Runs

## Decision Outcome

We will implement a deployment automation framework using Ansible and GitHub Actions. This approach will involve integrating Ansible for infrastructure provisioning and application deployment, while GitHub Actions will handle the continuous integration (CI) and trigger the deployment processes.

## Considerations
- Setup Ansible Playbooks: 
    - Each team will create Ansible playbooks tailored to their application deployment needs.
    - The playbooks will be stored in the respective repositories, using a provided repository template.

- GitHub Actions for CI: 
    - Workflows will be defined in the `.github/workflows` directory of each repository to automate building, testing, and triggering deployment processes via GitHub Actions.

- Trigger Ansible Deployments: 
    - Deployments will be triggered using GitHub Actions, with the option of using self-hosted runners or installing Ansible for every run.
    - Ansible should handle the deployment logic. The playbooks will execute the deployment steps on the necessary infrastructure, which could be on-premises servers or cloud platforms.

- Centralized Inventory Management: 
    - A centralized inventory file or dynamic inventory script will be maintained to ensure consistent host operations.

- Secrets Management: 
    - Sensitive deployment information will be stored using AWS Secret Manager or GitHub Secrets, accessible by GitHub Actions and passed to Ansible.

- Logging and Monitoring: 
    - Ansible playbooks and GitHub Actions will implement logging to track deployment progress and errors. Integrated monitoring tools will ensure application functionality post-deployment.

- Documentation and Governance: 
    - Documentation will be provided for creating and maintaining Ansible playbooks, with governance policies to ensure compliance with organizational standards.

## Pros
- Simplifies setup through agentless deployments compared to agentic tools like Chef and Puppet.
- Using Ansible playbooks ensures consistency with declarative infrastructure definitions.
- Ansible ansures idempotent deployments prevent unexpected issues.
- Reusable playbooks and roles streamline deployment logic across projects.

## Cons
- Teams unfamiliar with Ansible may face a learning curve, requiring time and resources to become proficient.
- Limited debugging insights compared to dedicated CI/CD tools sush as Bamboo or Jenkins.
- SSH access requirements for GitHub Actions runners requires careful security configurations.
- Stateless nature of Ansible requires careful change management compared to stateful IaC such as Terraform.
- Lack of built-in rollback mechanisms in GitHub Actions necessitates custom rollback handling.


## Decision Outcome
By adopting Ansible with GitHub Actions, OASIS teams will benefit from a consistent, flexible, and cost-effective deployment process. This approach aligns with organizational goals to streamline operations and maintain control over deployment environments while addressing both current inefficiencies and potential security concerns.

## Links
- [Ansible with Github actions](https://spacelift.io/blog/github-actions-ansible)
