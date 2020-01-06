# Introduction

This action wraps the [oss sast](https://github.com/AppThreat/sast-scan/) scanning tool called `sast-scan`. sast-scan supports a range of free and open source SAST scanners and comes with optimal configurations for various languages and frameworks.

## Usage

With minimal configuration

```yaml
- uses: AppThreat/sast-scan-action@master
  with:
    type: "python"
```

```yaml
- uses: AppThreat/sast-scan-action@master
  with:
    type: "python"

- uses: actions/upload-artifact@v1
  with:
    name: reports
    path: reports
```
