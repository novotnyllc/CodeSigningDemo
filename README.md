# CodeSigningDemo
Skeleton for demonstrating use of the .NET Foundation's code signing service

The `azure-pipelines.yml` shows how you can use a multi-stage build with an ``environment` to require
a manual approval for code signing. Once signed, a Release is created and pushed though a release pipeline. 