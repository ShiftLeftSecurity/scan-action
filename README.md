# Overview

```bash
███████╗██╗  ██╗██╗███████╗████████╗██╗     ███████╗███████╗████████╗    ███████╗ ██████╗ █████╗ ███╗   ██╗
██╔════╝██║  ██║██║██╔════╝╚══██╔══╝██║     ██╔════╝██╔════╝╚══██╔══╝    ██╔════╝██╔════╝██╔══██╗████╗  ██║
███████╗███████║██║█████╗     ██║   ██║     █████╗  █████╗     ██║       ███████╗██║     ███████║██╔██╗ ██║
╚════██║██╔══██║██║██╔══╝     ██║   ██║     ██╔══╝  ██╔══╝     ██║       ╚════██║██║     ██╔══██║██║╚██╗██║
███████║██║  ██║██║██║        ██║   ███████╗███████╗██║        ██║       ███████║╚██████╗██║  ██║██║ ╚████║
╚══════╝╚═╝  ╚═╝╚═╝╚═╝        ╚═╝   ╚══════╝╚══════╝╚═╝        ╚═╝       ╚══════╝ ╚═════╝╚═╝  ╚═╝╚═╝  ╚═══╝
```

ShiftLeft [Scan](https://slscan.io) is a free open-source security tool for modern DevOps teams. With an integrated multi-scanner based design, Scan can detect various kinds of security flaws in your application and infrastructure code in a single fast scan without the need for any _remote server_! The product supports a range of integration options: from scanning every push via a git hook to scanning every build and pull-request in the CI/CD pipelines.

## Highlighted Features

### Supported scans

- Credentials Scanning to detect accidental secret leaks
- Static Analysis Security Testing (SAST) for a range of languages and frameworks
- Open-source dependencies and License audit
- Pull Request status checks and Scan summary as comments

### Languages supported

- Salesforce Apex
- bash
- Go
- Java
- JSP
- Node.js
- Oracle PL/SQL
- Python
- Rust (Dependency and Licence scan alone)
- Terraform
- Salesforce Visual Force
- Apache Velocity

## Getting Started

Simply add the following snippet to your GitHub actions workflow.

```yaml
- name: Perform ShiftLeft Scan
  uses: ShiftLeftSecurity/scan-action@master
```

To override the built-in language detection, use the `type` parameter.

```yaml
- name: Perform ShiftLeft Scan
  uses: ShiftLeftSecurity/scan-action@master
  with:
    type: "credscan,java,depscan"
```

For a full example, refer to the [workflow](https://github.com/ShiftLeftSecurity/sast-scan/blob/master/.github/workflows/pythonapp.yml) file used by Scan to scan itself.

### Viewing Reports

Scan summary would get printed directly on the action build log as shown.

![Scan Invocation](docs/scan-invocation.png)

![Scan Summary](docs/scan-summary.png)

The action also produces HTML reports for the various scans. To upload the reports as build artifacts to your pipeline use the `upload-artifact` step as shown:

```yaml
- name: Perform ShiftLeft Scan
  uses: ShiftLeftSecurity/scan-action@master
  with:
    type: "credscan,python"
  env:
    WORKSPACE: https://github.com/${{ github.repository }}/blob/${{ github.sha }}
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

- uses: actions/upload-artifact@v1
  with:
    name: reports
    path: reports
```

In the above configuration, two environment variables are used to customise the behaviour:

- WORKSPACE: Specifying the URL to your repository would transform the filenames in the reports to hyperlinks. Specify empty string `""` when using the `Code Scanning` feature on GitHub
- GITHUB_TOKEN: Passing the GitHub token would improve the scan results by increasing the allowance for package names lookup during dependency scanning

## Tips & Tricks

### Automatic build

Scan can attempt to build certain project types automatically. Java, node.js, rust, go and csharp are currently supported. To enable auto-build, set the environment variable `SCAN_AUTO_BUILD` as shown:

```yaml
- name: Perform ShiftLeft Scan
  uses: ShiftLeftSecurity/scan-action@master
  with:
    type: "credscan,python"
  env:
    WORKSPACE: https://github.com/${{ github.repository }}/blob/${{ github.sha }}
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    SCAN_AUTO_BUILD: true
```

## Documentation

Please refer to the [documentation](https://slscan.io) on using ShiftLeft Scan in your pipelines.

## Already a Scan user?

Please let us [know](https://github.com/ShiftLeftSecurity/sast-scan/issues) so that we can add your logo or link here.
