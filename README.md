# DevOps Release Scripts

![PowerShell](https://img.shields.io/badge/PowerShell-7.0+-blue.svg?logo=powershell)
![Octopus Deploy](https://img.shields.io/badge/Octopus%20Deploy-2020.1+-2F93E0.svg?logo=octopusdeploy)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)
![GitHub Stars](https://img.shields.io/github/stars/yourorg/devops-release-scripts?style=social)
![GitHub Issues](https://img.shields.io/github/issues/yourorg/devops-release-scripts)

PowerShell automation scripts for Octopus Deploy release management and deployment orchestration.

## 📋 Overview

This repository contains PowerShell scripts designed to streamline and automate deployment processes using Octopus Deploy. These scripts handle various aspects of the release pipeline, from build preparation to deployment execution and post-deployment verification.

## ✅ Prerequisites

- **PowerShell**: Version 5.1 or higher (PowerShell 7+ recommended)
- **Octopus Deploy**: Server version 2020.1 or higher
- **Octopus CLI**: Install the Octopus Deploy CLI tools
- **API Key**: Valid Octopus Deploy API key with appropriate permissions

### Required Permissions

Ensure your Octopus Deploy API key has the following permissions:
- Project viewer/deployer rights
- Environment deployment permissions
- Release creation capabilities

## 🚀 Installation

1. Clone this repository:
   ```powershell
   git clone <repository-url>
   cd devops-release-scripts
   ```

2. Install Octopus CLI (if not already installed):
   ```powershell
   choco install octopustools
   # or
   dotnet tool install Octopus.DotNet.Cli --global
   ```

3. Configure your Octopus Deploy connection:
   ```powershell
   $env:OCTOPUS_URL = "https://your-octopus-server.com"
   $env:OCTOPUS_API_KEY = "API-XXXXXXXXXXXXXXXXXXXXXXXXXX"
   ```

## 📁 Repository Structure

```
.
├── scripts/
│   ├── deployment/          # Deployment execution scripts
│   ├── releases/            # Release creation and management
│   ├── utilities/           # Helper functions and utilities
│   └── rollback/            # Rollback and recovery scripts
├── config/
│   └── environments.json    # Environment configuration
├── tests/
│   └── *.Tests.ps1         # Pester test files
└── README.md
```

## 💻 Usage

### 🎯 Creating a Release

```powershell
.\scripts\releases\Create-Release.ps1 `
    -ProjectName "MyProject" `
    -Version "1.0.0" `
    -ReleaseNotes "Release notes here"
```

### 🚢 Deploying a Release

```powershell
.\scripts\deployment\Deploy-Release.ps1 `
    -ProjectName "MyProject" `
    -Environment "Production" `
    -ReleaseVersion "1.0.0"
```

### ⬆️ Promoting a Release

```powershell
.\scripts\deployment\Promote-Release.ps1 `
    -ProjectName "MyProject" `
    -FromEnvironment "Staging" `
    -ToEnvironment "Production"
```

## 📜 Common Scripts

### Create-Release.ps1
Creates a new release in Octopus Deploy with specified package versions and release notes.

**Parameters:**
- `ProjectName` - Name of the Octopus project
- `Version` - Release version number
- `ReleaseNotes` - Optional release notes
- `PackageVersion` - Specific package version to use

### Deploy-Release.ps1
Deploys a specific release to a target environment.

**Parameters:**
- `ProjectName` - Name of the Octopus project
- `Environment` - Target environment name
- `ReleaseVersion` - Version of release to deploy
- `WaitForCompletion` - Wait for deployment to complete (default: true)

### Rollback-Deployment.ps1
Rolls back to a previous deployment version.

**Parameters:**
- `ProjectName` - Name of the Octopus project
- `Environment` - Environment to rollback
- `TargetVersion` - Version to rollback to

## ⚙️ Configuration

### Environment Variables

Set the following environment variables for authentication:

```powershell
$env:OCTOPUS_URL = "https://octopus.company.com"
$env:OCTOPUS_API_KEY = "API-YOURAPIKEY"
$env:OCTOPUS_SPACE = "Default"  # Optional, if using spaces
```

### Configuration Files

Edit `config/environments.json` to customize environment-specific settings:

```json
{
  "environments": [
    {
      "name": "Production",
      "requiresApproval": true,
      "notificationEmail": "team@company.com"
    },
    {
      "name": "Staging",
      "requiresApproval": false
    }
  ]
}
```

## 🎯 Best Practices

1. **Always test in lower environments first** - Deploy to Dev/Test before Production
2. **Use semantic versioning** - Follow SemVer for release versions
3. **Include meaningful release notes** - Document changes in each release
4. **Enable logging** - Use the `-Verbose` flag for detailed output
5. **Validate before deployment** - Run pre-deployment checks
6. **Monitor deployments** - Watch deployment progress and logs

## 🧪 Testing

Run Pester tests to validate scripts:

```powershell
Invoke-Pester -Path .\tests\
```

## 🔧 Troubleshooting

### ⚠️ Common Issues

**🔐 Authentication Errors**
- Verify your API key is valid and has necessary permissions
- Check that OCTOPUS_URL is correctly set

**⏱️ Connection Timeouts**
- Ensure network connectivity to Octopus server
- Verify firewall rules allow HTTPS traffic

**❌ Deployment Failures**
- Check Octopus Deploy logs for detailed error messages
- Verify target machines are online and accessible
- Ensure deployment steps are properly configured

## 🤝 Contributing

1. Create a feature branch from `main`
2. Make your changes and test thoroughly
3. Update documentation as needed
4. Submit a pull request with a clear description

## 🔒 Security

- **Never commit API keys or secrets** - Use environment variables
- Store sensitive configuration in Azure Key Vault or similar
- Rotate API keys regularly
- Use least-privilege access principles

## 💬 Support

For issues or questions:
- Check Octopus Deploy documentation: https://octopus.com/docs
- Review script comments and help documentation
- Contact the DevOps team

## 📄 License

[Specify your license here]

## 👥 Authors

[Your team/organization name]

---

**Last Updated**: November 2025
