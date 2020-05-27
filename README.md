# sample-dotnet-api

Sample Dotnet API CI/CD Example using Github Actions.

This is a sample of using Github Actions to create a CI/CD workflow to Google Cloud Run. 

Highlevel:
We Build, Test, Submit, Package, and Deploy to Google Cloud Run through a YAML definition using Github Actions. 
Google Cloud Platform picks up the package and deploys based on default specifications.

Monitoring is handled through Github Actions interface (screen shot provided)
Once deployment is completed the rest of the monitoring is handled by GCP. For example, revisions to the deployments. 

New images are automatically tagged as latest and versioning is time-stamp based. 

## Requirements

- [Docker](https://docs.docker.com/docker-for-windows/install/)
- [Dotnet Core 3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [Visual Studio Code](https://code.visualstudio.com/) or [Visual Studio Community](https://visualstudio.microsoft.com/vs/)
- An Account at Google Cloud

## How to build

Commit any code change to Master Branch to kick off CI/CD Flow

## Flow Steps

Flow is started anytime there are changes made to the Master Branch

Upon commit the following things occur in order:
1. Code is checked out
2. .NET Code is setup and dependencies are installed
3. Code is built
4. Unit Tests are run against code. 
5. (Assuming above passes) 
6. Code is checked out again
7. Authenticate to GCloud using provided secrets
8. Submit source code to Google Cloud where an image is built and stored in container registry
9. Code is deployed to Cloud Run container service using default parameters

## Monitoring Flow:
Internally Github Provides 2 methods of monitoring:
1. Email
2. [Dashboard of Deployment and Unit Tests](https://imgur.com/a/sdXax7t)

## Note: Deployment Defaults
By default google sets the concurrency (or parallelism) to 80.

## How to run API
Navigate to https://cloud-run-github-actions-kk3wpkyica-ue.a.run.app/WeatherForecast 

# Further Improvements 
Simulate from Dev to SIT promotion
Currently the flow is triggered on Master Branch. I imagine you can have different triggers based on Dev / SIT / Production branches which would be straight forward to do. However, I imagine promotion would be manual so that QA could test and approve. In in this case it may not be required to be automated. 

Automate image version tagging
"latest" tag for the images are automatic. However, to add versioning either timestamp or perhaps adding a salted key might work. More traditional version control (i.e. 2.0.1) can be added for further tracking. Perhaps based on commit tags or something to that effect. Perhaps even just be using the commit id. Bot of those are the recommended methods recommended on Github Actions. 
