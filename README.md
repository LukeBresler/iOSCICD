# iOSCICD

A demonstration iOS application showcasing a complete CI/CD pipeline using Fastlane and GitHub Actions.

## Overview

This project serves as a practical example of setting up continuous integration and deployment for iOS applications. It demonstrates industry-standard practices for automating build, test, and deployment workflows using Fastlane and GitHub Actions.

## Features

- **Automated Testing**: Run unit and UI tests automatically on every push
- **Continuous Integration**: GitHub Actions workflow for building and testing
- **Fastlane Integration**: Streamlined deployment and release management
- **Code Signing**: Automated certificate and provisioning profile management
- **Version Management**: Automated version bumping and changelog generation

## Prerequisites

Before you begin, ensure you have the following installed:

- **Xcode** (latest stable version recommended)
- **Ruby** (2.7 or higher)
- **Bundler**: `gem install bundler`
- **Fastlane**: Installed via Bundler (see setup below)

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/LukeBresler/iOSCICD.git
cd iOSCICD
```

### 2. Install Dependencies

```bash
# Install Ruby dependencies
bundle install
```

### 3. Open the Project

```bash
open iOSCICD.xcodeproj
```

## Project Structure

```
iOSCICD/
├── .github/
│   └── workflows/        # GitHub Actions workflow files
├── fastlane/
│   ├── Fastfile         # Fastlane automation scripts
│   ├── Appfile          # App configuration
│   └── Matchfile        # Code signing configuration
├── iOSCICD/             # Main app source code
├── iOSCICDTests/        # Unit tests
├── iOSCICDUITests/      # UI tests
├── Gemfile              # Ruby dependencies
└── Gemfile.lock         # Locked dependency versions
```

## Fastlane Setup

This project uses Fastlane for build automation. The following lanes are available:

### Available Lanes

```bash
# Run tests
bundle exec fastlane test

# Build the app
bundle exec fastlane build

# Beta deployment to TestFlight
bundle exec fastlane beta

# Release to App Store
bundle exec fastlane release
```

### Configuration

1. **Update Fastfile**: Customize lanes in `fastlane/Fastfile` for your specific needs
2. **App Credentials**: Update `fastlane/Appfile` with your Apple ID and app identifier
3. **Code Signing**: Configure `fastlane/Matchfile` for certificate management

## GitHub Actions CI/CD

This repository includes GitHub Actions workflows for automated testing and deployment.

### Workflow Triggers

- **Push to main**: Runs tests and builds
- **Pull Requests**: Runs tests for verification
- **Tags**: Triggers deployment workflows

### Setting Up Secrets

Configure the following secrets in your GitHub repository settings:

1. Navigate to **Settings** → **Secrets and variables** → **Actions**
2. Add the following secrets:
   - `APPLE_ID`: Your Apple Developer account email
   - `APP_STORE_CONNECT_API_KEY`: API key for App Store Connect
   - `MATCH_PASSWORD`: Password for Fastlane Match repository
   - `GIT_AUTHORIZATION`: Token for accessing match certificates repository

## Code Signing

This project uses Fastlane Match for code signing management:

```bash
# Initialize match (first time setup)
bundle exec fastlane match init

# Sync certificates and profiles
bundle exec fastlane match development
bundle exec fastlane match appstore
```

## Testing

### Run Tests Locally

```bash
# Using Fastlane
bundle exec fastlane test

# Using xcodebuild directly
xcodebuild test -project iOSCICD.xcodeproj -scheme iOSCICD -destination 'platform=iOS Simulator,name=iPhone 15'
```

### Test Types

- **Unit Tests**: Located in `iOSCICDTests/`
- **UI Tests**: Located in `iOSCICDUITests/`

## Deployment

### TestFlight (Beta)

Deploy to TestFlight for beta testing:

```bash
bundle exec fastlane beta
```

### App Store (Production)

Deploy to the App Store:

```bash
bundle exec fastlane release
```

## Best Practices

This project demonstrates several CI/CD best practices:

1. **Automated Testing**: Tests run automatically on every push
2. **Version Control**: Semantic versioning and automated version bumping
3. **Code Signing**: Centralized certificate management with Match
4. **Environment Separation**: Different configurations for development, staging, and production
5. **Continuous Deployment**: Automated releases to TestFlight and App Store
6. **Documentation**: Comprehensive README and inline code comments

## Troubleshooting

### Common Issues

**Build Failures**
- Ensure Xcode Command Line Tools are installed: `xcode-select --install`
- Clean build folder: `xcodebuild clean`
- Update dependencies: `bundle update`

**Code Signing Issues**
- Verify certificates: `bundle exec fastlane match development --readonly`
- Update provisioning profiles: `bundle exec fastlane match development --force`

**GitHub Actions Failures**
- Check secret configuration in repository settings
- Review workflow logs for specific error messages
- Ensure all required secrets are properly set

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Resources

- [Fastlane Documentation](https://docs.fastlane.tools/)
- [GitHub Actions for iOS](https://docs.github.com/en/actions)
- [Apple Developer Documentation](https://developer.apple.com/documentation/)
- [Fastlane Match Guide](https://docs.fastlane.tools/actions/match/)

## License

This project is available for educational and demonstration purposes.

## Author

**Luke Bresler**
- GitHub: [@LukeBresler](https://github.com/LukeBresler)

## Acknowledgments

- Thanks to the Fastlane team for their excellent automation tools
- GitHub Actions for providing robust CI/CD infrastructure
- The iOS development community for best practices and guidance

---

**Note**: This is a demonstration project. For production use, ensure you customize configurations, add appropriate security measures, and follow your organization's deployment policies.
