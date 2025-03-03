# AVM Compositions

Composing Infrastructure with Azure Verified Modules (AVM)

## Overview

**AVM Compositions** is an extension of the [Azure Verified Modules (AVM)](https://azure.github.io/Azure-Verified-Modules/) framework, providing a structured approach to assembling AVM pattern modules into reusable, scalable, and production-ready infrastructure solutions.

This repository enables platform engineers, DevOps teams, and cloud architects to create composable infrastructure by leveraging the best practices of AVM while maintaining modularity, consistency, and compliance.

For additional documentation, see the [docs/README.md](docs/README.md) file.

## Features

- **Composable Infrastructure** – Combine multiple AVM modules into cohesive solutions.
- **Scalable & Modular** – Designed for reuse and adaptability across different workloads.
- **AVM-Aligned** – Ensures compatibility with Azure Verified Modules best practices.
- **Infrastructure as Code (IaC)** – Fully Terraform-based for automation and repeatability.
- **Extensible** – Add custom logic while maintaining AVM compliance.

## Getting Started

### Prerequisites

Before using AVM Compositions, ensure you have the following:

- **Terraform** (>= 1.x)
- **Azure CLI** (latest version)
- **Access to an Azure Subscription**
- **Basic knowledge of AVM pattern modules**

### Installation

Clone the repository and navigate to your working directory:

```sh
git clone https://github.com/your-org/avm-compositions.git
cd avm-compositions
```

### Usage

1. **Choose a Composition**
   - Browse the available compositions in the `compositions/` directory.
   - Select a composition that fits your infrastructure needs.

2. **Customize Variables**
   - Modify the `terraform.tfvars` file to suit your environment.

3. **Deploy the Composition**

   ```sh
   terraform init
   terraform plan
   terraform apply
   ```

4. **Verify Deployment**
   - Use Azure Portal or CLI to check deployed resources.

   ```sh
   az resource list --query "[].{Name:name, Type:type}" -o table
   ```

## Repository Structure

```text
📂 avm-compositions
 ├── 📂 compositions/       # Collection of AVM compositions
 ├── 📂 modules/            # Reusable custom modules
 ├── 📂 examples/           # Sample implementations
 ├── 📂 docs/               # Additional documentation and diagrams
 │   ├── 📜 README.md       # Detailed documentation overview
 ├── 📜 README.md           # Main repository overview and usage guide
```

## Contributing

Contributions are welcome! To propose changes:

1. Fork this repository.
2. Create a new feature branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -m "Add new composition"`).
4. Push to your fork and submit a Pull Request.

## License

This project is licensed under the **GPL-3.0 License**. See [LICENSE](LICENSE) for details.

## Resources

- **Azure Verified Modules (AVM):** [Azure GitHub Docs](https://azure.github.io/Azure-Verified-Modules/)
- **Terraform:** [Official Documentation](https://developer.hashicorp.com/terraform/docs)
- **Azure CLI:** [Microsoft Docs](https://learn.microsoft.com/en-us/cli/azure/)
