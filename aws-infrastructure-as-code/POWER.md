---
name: "aws-infrastructure-as-code"
displayName: "Build AWS infrastructure with CDK and CloudFormation"
description: "Generate well-architected AWS infrastructure with CDK and CloudFormation - access latest documentation, validate templates, and troubleshoot deployments"
keywords: ["aws", "cdk", "cloudformation", "troubleshoot", "validate", "compliance", "cfn-lint", "cfn-guard", "infrastructure", "iac", "template", "stack", "construct", "resource", "deployment"]
author: "AWS"
---

# AWS Infrastructure as Code

## Overview

Generate well-architected CDK code using latest documentation on constructs and best practices, and improved correctness with CloudFormation syntax validation, compliance and troubleshooting tools.

## When to Use This Power

- **Validating CloudFormation templates** before deployment to catch syntax errors, invalid properties, and schema violations
- **Checking security compliance** of CloudFormation templates against AWS Guard Rules Registry and Control Tower proactive controls
- **Debugging failed CloudFormation deployments** with intelligent failure analysis and CloudTrail deep links
- **Searching CloudFormation documentation** for resource types, properties, and template syntax
- **Finding CDK documentation** for constructs, APIs, best practices, and CDK-NAG security checks
- **Discovering CDK code samples** and community constructs across TypeScript, Python, Java, C#, and Go
- **Applying CDK best practices** for application configuration, coding, constructs, security, and testing
- **Reading complete documentation pages** for CloudFormation resources or CDK constructs
- **Getting pre-deployment validation guidance** for CloudFormation change sets

## MCP Servers

This power includes the `awslabs.aws-iac-mcp-server` MCP server which provides the following tools:

### Documentation Tools

- **read_iac_documentation_page** - Fetches and converts CDK or CloudFormation documentation pages to markdown for reading complete resource references, API docs, and implementation guides

### CloudFormation Tools

- **validate_cloudformation_template** - Validates CloudFormation template syntax and schema using cfn-lint, returning specific fix suggestions with line numbers
- **check_cloudformation_template_compliance** - Checks CloudFormation templates against security and compliance rules using cfn-guard with detailed remediation guidance
- **troubleshoot_cloudformation_deployment** - Analyzes failed CloudFormation stacks with pattern matching against 30+ known failure cases and provides CloudTrail deep links
- **search_cloudformation_documentation** - Searches CloudFormation documentation for resource types, properties, template syntax, and best practices
- **get_cloudformation_pre_deploy_validation_instructions** - Returns CLI commands and guidance for CloudFormation's pre-deployment validation during change set creation

### CDK Tools

- **search_cdk_documentation** - Searches CDK API Reference, Best Practices Guide, Code Samples, and CDK-NAG rules for constructs, patterns, and implementation guidance
- **search_cdk_samples_and_constructs** - Finds CDK code samples and community constructs across multiple languages (TypeScript, Python, Java, C#, Go)
- **cdk_best_practices** - Provides comprehensive CDK best practices for application configuration, coding, constructs, security, and testing

## Tool Usage Examples

### Validate CloudFormation Template

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "validate_cloudformation_template", {
  "template_content": `
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-app-bucket
  `,
  "regions": ["us-east-1"]
})
```

### Check Template Compliance

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "check_cloudformation_template_compliance", {
  "template_content": `
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-app-bucket
      BucketEncryption:
        ServerSideEncryptionConfiguration:
          - ServerSideEncryptionByDefault:
              SSEAlgorithm: AES256
  `
})
```

### Troubleshoot Failed Stack

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "troubleshoot_cloudformation_deployment", {
  "stack_name": "my-app-stack",
  "region": "us-east-1",
  "include_cloudtrail": true
})
```

### Search CloudFormation Documentation

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "search_cloudformation_documentation", {
  "query": "AWS::Lambda::Function properties"
})
```

### Read Full Documentation Page

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "read_iac_documentation_page", {
  "url": "https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html"
})
```

### Search CDK Documentation

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "search_cdk_documentation", {
  "query": "S3 bucket encryption best practices"
})
```

### Find CDK Code Samples

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "search_cdk_samples_and_constructs", {
  "query": "Lambda function with VPC",
  "language": "typescript"
})
```

### Get CDK Best Practices

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "cdk_best_practices", {})
```

### Get Pre-Deploy Validation Instructions

```javascript
usePower("aws-infrastructure-as-code", "awslabs.aws-iac-mcp-server", "get_cloudformation_pre_deploy_validation_instructions", {})
```

## AWS Credentials & Permissions

**Only the `troubleshoot_cloudformation_deployment` tool requires AWS credentials.** All other tools (template validation, compliance checking, documentation search) run locally or against public APIs without credentials.

**For deployment troubleshooting**, configure AWS credentials and the following IAM permissions:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:DescribeStacks",
        "cloudformation:DescribeStackEvents",
        "cloudformation:DescribeStackResources",
        "cloudtrail:LookupEvents"
      ],
      "Resource": "*"
    }
  ]
}
```

**Configure credentials** via AWS CLI (`aws configure`) or environment variables (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_DEFAULT_REGION`).

## Security Considerations

⚠️ **Privacy Notice**: This MCP server executes AWS API calls using your credentials and shares the response data with your third-party AI model provider (e.g., Amazon Q, Claude Desktop, Cursor, VS Code). Users are responsible for understanding your AI provider's data handling practices and ensuring compliance with your organization's security and privacy requirements when using this tool with AWS resources.


