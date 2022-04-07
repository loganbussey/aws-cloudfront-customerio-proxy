# AWS Cloudfront Customer.io HTTPS link tracking proxy

By default, Customer.io's tracked links that use your custom subdomain will be generated as non-secure HTTP links.

Customer.io has released [documentation](https://www.customer.io/docs/https-link-verification/) on how to create a proxy to their service using [AWS Cloudfront](https://aws.amazon.com/cloudfront/). This repository features a [AWS CloudFormation](https://aws.amazon.com/cloudformation/) template which will create the Cloudfront distribution as documented by Customer.io, and request a free SSL Certificate with a single command.

## Prerequisites

### Setting up the AWS CLI

You’ll need to have the [AWS Command Line Interface](https://aws.amazon.com/cli/) installed and configured to connect to your AWS account. On a Mac with [Homebrew](https://brew.sh/) it's as easy as entering the command:

```sh
$ brew install awscli
```

If you don't have or want to use Homebrew, you’ll need Python 2.6.5 or higher and to install using Pip:

```sh
$ pip install awscli
```

For Windows, download and install the installer from [here](https://aws.amazon.com/cli/).

### Authenticating with AWS

Enter `aws configure` at the command line, and then press Enter.

```sh
$ aws configure
AWS Access Key ID [None]:
AWS Secret Access Key [None]:
Default region name [None]:
Default output format [None]:
```

If your AWS account requires Multi-Factor Authentication (MFA), then [aws-mfa](https://github.com/broamski/aws-mfa) makes it easy to manage your AWS SDK Security Credentials when MFA is enforced on your AWS account.

## Getting Started

1. Clone this repository

```sh
$ mkdir aws-cloudfront-customerio-proxy && cd $_
$ git clone https://github.com/loganbussey/aws-cloudfront-customerio-proxy.git .
```

2. Run `setup` and follow the prompts:

```sh
$ ./setup
 This script will help you setup a Cloudfront Distribution for a Customer.io HTTPS link tracking proxy and request a SSL Certificate for the subdomain that you choose.

Enter your link tracking subdomain [ENTER]: link.example.com
Enter your Customer.io tracking domain [ENTER]: track.customer.io
Which validation method would you like to use for your SSL Certificate?
EMAIL
DNS
Which would you like to use? EMAIL
Enter a CloudFormation stack name [customerio-proxy] [ENTER]: my-customerio-proxy
```

Note: If you choose email as the domain validation method, you will need access to the domain administrators inbox to validate the certificate creation. If you choose `DNS`, then you will need to validate the domain with a `CNAME`.

To check on the status of the stack creation the following AWS services will be useful:
* [Cloudformation](https://console.aws.amazon.com/cloudformation/home)
* [Certificate Manager](https://console.aws.amazon.com/acm/home)
* [Cloudfront](https://console.aws.amazon.com/cloudfront/home)

## Next steps

1. Point your domains to the Cloudfront distributions that were created.

2. Once you are sure that your distribution is properly pointing to Customer.io's API, head back to Customer.io and go to your Workspace Settings for Email. If you haven’t already set up your link tracking domain (e.g. link.example.com), enter it now in the HOST NAME field and click the Verify domain button to re-validate the domain. You should now pass the HTTPS check and tracking links will use HTTPS by default.

If you need help setting this up or with your Segment implementation in general, get in touch with us at [hello@loganbussey.com](mailto:hello@loganbussey.com), or visit [Logan Bussey](https://www.loganbussey.com/) for more information.
