# CloudFormation

* CloudFormation is a declarative way of outlining your AWS Infrastructure, for any resources (most of them are supported).

### Benefits of AWS CloudFormation

* Infrastructure as code:
  * No resources are manually created, which is excellent for control.
  * The code can be version controlled for example using git.
  * Changes to the infrastructure are reviewed through code.
* Cost:
  * Each resource within the stack is tagged with an identifier so you can easily see how much a stack cost.
  * You can estimate the cost of your resource using the CloudFormation Template.
  * Savings strategy: In DEV, you could automate the deletion of templates at 5 PM and recreate them at 8 AM, safely.
* Productivity:
  * Ability to destroy and re-create an infrastructure on the cloud on the fly.
  * Declarative programming (no need to figure out ordering and orchestration)
* Separation of Concern:
  * Create many stacks for many apps, and many layers.
  * Example: VPC stacks, Network stacks, App Stacks.

### How CloudFormation Works

* Templates have to be uploaded in S3 and then referenced in CloudFormation.
* To update a template, we can’t edit previous ones. We have to reupload a new version of the template to AWS.
* Stacks are identified by a name.
* • Deleting a stack deletes every single artifact that was created by CloudFormation.

### Deploying CloudFormation templates

* Manual way:
  * Editing templates in the CloudFormation Designer.
  * Using the console to input parameters, etc.
* Automated way:
  * Editing templates in a YAML file.
  * Using the AWS CLI to deply templates.
  * Recommended way when you fully want to automate your flow.

### CloudFormation - Building Blocks

Templates components:

* Resources: your AWS resources declared in the template (MANDATORY).&#x20;
* Parameters: the dynamic inputs for your template.
* 3\. Mappings: the static variables for your template.
* 4\. Outputs: References to what has been created.
* 5\. Conditionals: List of conditions to perform resource creation.
* 6\. Metadata.

### CloudFormation - Resources

* Resources are the core of your CloudFormation template (MANDATORY).
* They represent the different AWS Components that will be created and configured.
* Resources are declared and can reference each other.
* Resource types identifiers are of the form:
  * `AWS::aws-product-name::data-type-name`

All the resources can be found here:

* &#x20;http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aw s-template-resource-type-ref.html
* Example here (for an EC2 instance):&#x20;
  * http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html
  * http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/awsproperties-ec2-instance.html
  * http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/awsproperties-ec2-security-group.html
  * http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/awsproperties-ec2-eip.html

### CloudFormation - Parameters





#### CloudFormation - Pseudo Parameters

