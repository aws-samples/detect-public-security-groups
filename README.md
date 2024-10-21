## Automatically audit AWS security groups that allow access from public IP addresses

As a security best practice, it's crucial to minimize the exposure of AWS resources to only what is absolutely necessary. For example, web servers that serve the general public need to allow inbound access from the internet, but access to other workloads should be restricted to specific networks to reduce unnecessary exposure. Security groups in Amazon Virtual Private Cloud (Amazon VPC) are an effective control to help you limit resource access. However, evaluating security groups can be a cumbersome task, especially in multi-account architectures. AWS Config rules and AWS Security Hub controls can help you identify security groups that permit access from the public internet (0.0.0.0/0) to specific network communication protocols, such as Secure Shell (SSH), HTTP, HTTPS, and Windows remote desktop protocol (RDP). However, these rules and controls are not applicable if services run on non-standard ports or if access is restricted to certain public IP addresses. For instance, this might occur when a web service is associated with TCP port 8443 instead of the standard TCP port 443. This might also occur when developers have access to the server from their home networks, such as for testing purposes.

To address this, you can use the infrastructure as code (IaC) solution provided in this pattern to identify security groups that allow access from any non-private (RFC 1918
noncompliant) IP addresses to any workload in your AWS account or AWS organization. The AWS CloudFormation template provisions a custom AWS Config rule, an AWS Lambda function, and the necessary permissions. You can deploy it as a stack in a single account or as a stack set across the entire organization, managed through AWS Organizations.

![Target Architecture](./target-architecture.png)

For prerequisites and instructions for using this AWS Prescriptive Guidance pattern, see [Automatically audit AWS security groups that allow access from public IP addresses](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/audit-security-groups-access-public-ip.html).

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
