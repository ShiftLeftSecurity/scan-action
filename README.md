# Introduction

ShiftLeft Scan is a free commercial grade security tool for modern DevOps teams. With an integrated multi-scanner based design, ShiftLeft Scan can detect various kinds of security flaws in your application and infrastructure code in a single scan.

- Secrets leak detection
- Static Analysis Security Testing (SAST)
- Open-source dependencies audit
- License violation checks
- Business logic flaws (*)
- Sensitive data disclosure (*)

(*) Throttling and restrictions applied per application for unregistered users. Please signup [here](https://www.shiftleft.io/register?utm_source=gh-action) to increase the usage allowance.

## Usage

With minimal configuration

```yaml
- uses: ShiftLeftSecurity/scan-action@master
  with:
    type: "credscan,java,depscan"
```

Upload reports to build artifacts

```yaml
- uses: ShiftLeftSecurity/scan-action@master
  with:
    type: "credscan,python"

- uses: actions/upload-artifact@v1
  with:
    name: reports
    path: reports
```

## Support

Have a question or request? We’d love to hear from you. Contact us [here](https://www.shiftleft.io/contact/)
