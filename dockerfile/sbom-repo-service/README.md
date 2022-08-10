# sbom-repo-service
The project to build sbom-repo-service docker image.

Sbom-repo-service deploy with daily-build. It's a sbom generator tool for openEuler.Binary file path: /opt/openeuler-sbom-tools

Inner interface:`sbom-repo-api/generateOpenEulerSbom`, method:POST, Return sbom content.

Examples: 
```shell
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" http://127.0.0.1:15551/sbom-repo-api/generateOpenEulerSbom -d '{"artifactPath": "/opt/iso/openEuler-22.03-LTS-x86_64-dvd.iso"}' 
```