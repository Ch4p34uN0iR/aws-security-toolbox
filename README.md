# AWS Security Toolbox :lock:

This toolbox will bring to you all necessary apps and tooling as a simple portable and preinstalled Docker container for SecOps on AWS, especially for auditing and assessment purpose.

This will reduce the overhead and the headache of installation these tools and dependencies.

## Requirements

- docker [macOS](https://docs.docker.com/docker-for-mac/) or [Linux](https://docs.docker.com/install/linux/docker-ce/debian/)
- `awscli` configured

## Tools

### Optional tools (host machine)

- [aws-vault](https://github.com/99designs/aws-vault)

### Tools (guest container)

- [awscli](https://aws.amazon.com/cli/)
- [CloudMapper](https://github.com/duo-labs/cloudmapper)
- [CloudTracker](https://github.com/duo-labs/cloudtracker)
- [prowler](https://github.com/toniblyx/prowler)
- [ScoutSuite](https://github.com/nccgroup/ScoutSuite)
- [PMapper](https://github.com/nccgroup/PMapper)
- [Enumerate-IAM](https://github.com/andresriancho/enumerate-iam)

## Usage

Clone the repository:

        $ git clone https://github.com/z0ph/aws-security-toolbox.git

There is two options to use this toolbox, 

- Option #1, you are using local `awscli` with `~/.aws/credentials` populated.
- Option #2, you want to use local `aws-vault`.

Info: Working directory within the container: `/opt/secops`

## Option 1 (Interactive)

        $ ./ast.sh login

When you are logged into the shell of the container in interactive mode (`-it`), you will be able to perform your audit/assessment with confidence.

Example:

        $ ./opt/secops/prowler/prowler -b | ansi2html -la > /tmp/prowler-report.html

*nb: `/tmp` is mapped to your own host `/tmp` folder.*

## Option 2 (`aws-vault`)

        $ ./ast.sh exec COMMAND="./prowler -b | ansi2html -la > prowler-report.html" 

*nb: if you are not using `default` aws-vault profile name, use the following:*

        $ ./ast.sh exec PROFILE_NAME="your_profile_name" COMMAND="/opt/secops/prowler/prowler -b > prowler-report.html" 

### Optional

if you want to build your own container **locally** to get latest updates from tools maintainers

        $ ./ast.sh build