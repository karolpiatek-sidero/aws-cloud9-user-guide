# Working with AWS Lambda functions using the AWS Toolkit<a name="lambda-toolkit"></a>

The AWS Toolkit supports [AWS Lambda](https://aws.amazon.com/lambda/) functions\. The AWS Toolkit replaces the functionality formerly provided by the Lambda plug\-in in AWS Cloud9\. Using the AWS Toolkit, you can author code for Lambda functions that are part of [serverless applications](https://aws.amazon.com/serverless/)\. In addition, you can invoke Lambda functions either locally or on AWS\.

Lambda is a fully managed compute service that runs your code in response to events generated by custom code or from various AWS services\. They include Amazon Simple Storage Service \(Amazon S3\), Amazon DynamoDB, Amazon Kinesis, Amazon Simple Notification Service \(Amazon SNS\), and Amazon Cognito\.

**Important**  
If you want to build a Lambda application that uses the resources that are provided by the Serverless Application Model \(SAM\), see [Working with AWS serverless applications using the AWS Toolkit](serverless-apps-toolkit.md)\.

**Topics**
+ [Invoking remote Lambda functions](#remote-lambda)
+ [Downloading, uploading, and deleting Lambda functions](#import-upload-delete-lambda)

## Invoking remote Lambda functions<a name="remote-lambda"></a>

Using the AWS Toolkit you can interact with [AWS Lambda](https://aws.amazon.com/lambda/) functions in various ways\.

For more information about Lambda, see the [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/)\. 

**Note**  
Suppose that you have already created Lambda functions by using the AWS Management Console or in some other way\. You can invoke them from the AWS Toolkit\. To create a new function with AWS Toolkit that you can deploy to AWS Lambda, you must first [create a serverless application](serverless-apps-toolkit.md#sam-create)\.

### Prerequisites<a name="remote-lambda-prereq"></a>
+ Make sure that the credentials that you configured in include appropriate read/write access to the AWS Lambda service\. If in the **AWS Explorer**, under **Lambda**, you see a message similar to "Error loading Lambda resources," check the permissions attached to those credentials\. Changes that you make to permissions take a few minutes to affect the **AWS Explorer** in AWS Toolkit\.

### Invoking a Lambda function<a name="invoke-lam-func"></a>

**Important**  
Calling API methods using the AWS Toolkit might result in changes to resources that can't be undone\. For example, if you call a `POST` method, the API's resources are updated if the call is successful\. 

You can invoke a Lambda function on AWS using the AWS Toolkit\.

****

1. In the **AWS Explorer**, choose the name of the Lambda function you want to invoke, and then open its context menu\.

1. Choose **Invoke on AWS**\.

1. In the **Invoke function** window that opens, choose an option for the payload your Lambda function needs\. \(The payload is the JSON that you want to provide to your Lambda function as input\.\) You can choose ** Browse** to select a file to use as payload or use the dropdown field to pick a template for the payload\. In this case, the Lambda function might appear as a string as an input, as shown in the text box\.

Choose **Invoke** to call the Lambda and pass in the payload\.

You see the output of the Lambda function in the AWS Lambda tab\.

## Downloading, uploading, and deleting Lambda functions<a name="import-upload-delete-lambda"></a>

The AWS Toolkit provides the options for importing and uploading Lambda functions in AWS Cloud9 IDE\. 

### Downloading a Lambda function<a name="w94aac25c30c13b5"></a>

By downloading a Lambda function, you also download the project files that describe the function from the AWS Cloud and work with them in the AWS Cloud9 IDE\.

### To download a Lambda function

1. In the **AWS Explorer**, under the Lambda node, open the context \(right\-click\) menu for the function, and choose **Download**\.

1. When asked to **Select a workspace folder for your new project**, you can do one of the following:
   + Choose the folder that's suggested to create a subfolder with the same name as your Lambda project\.
   + Choose **Select a different folder** to open a dialog box to browse for and select a different parent folder for your project subfolder\. 

   The IDE opens a new editor window\.

### Configuring a downloaded Lambda function for running and debugging<a name="w94aac25c30c13b7"></a>

To run and debug your downloaded Lambda function as a serverless application, you need a launch configuration to be defined in your `launch.json` file\. A Lambda function that was created in the AWS Management Console might not be included in a launch configuration\. So, you might need to add it manually\.

### To add your Lambda function to launch configuration

1. After you' downloaded the Lambda function, open the **Environment** window to view its folders and files\.

1. Next, check that your Lambda function is included in a `/home/ec2-user/.c9/launch.json` file\. If it isn't present, do the following to add a CodeLens link to your function's code:

   1. Open the source code file that defines the Lambda function \(for example, a `.js` or `.py` file\)\. Then, heck if there's a CodeLens link that you can use to add your lambda function to a `launch.json` file\. A CodeLens appears above the function and includes the `Add Debug Config` link\.

   1. Choose **Go** \(the magnifying glass icon\) on the left of the IDE, and enter "sam hint" to display the `AWS: Toggle SAM hints in source files` command\. Choose the command to run it\. 

   1. Close your Lambda source code file and then reopen it\.

   1. If the CodeLens is available in the source code after you reopen the file, choose `Add Debug Config` to add the launch configuration\.

1. If you can't add a CodeLens even after toggling the SAM hint option, do the following to add the launch configuration:

   1. Choose **Go** \(the magnifying glass icon\) on the left of the IDE, and type "config" to display the `AWS: SAM Debug Configuration Editor` command\. Choose the command to run it\.

   1. The **SAM Debug Configuration Editor** displays\. You can use this editor to define launch configuration properties\. For information, see the step for [configuring launch properties](serverless-apps-toolkit.md#properties) in [Using SAM templates to run and debug serverless applications](serverless-apps-toolkit.md#sam-run-debug-template)\. 
**Note**  
If your Lambda function doesn't have a `template.yaml` for SAM applications, you must add one\. For more information, see [Create your AWS SAM template](https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorial-lambda-sam-template.html)\.

   1. After you finished entering the required configuration information in the editor, your launch configuration is added to the **launch\.json** file\.

After you defined a launch configuration for your Lambda function, you can run it by doing the following:

1. At the top of the IDE, choose the arrow beside **Auto** and select the relevant launch configuration\.

1. Next, choose **Run**\.

### Uploading a Lambda function<a name="w94aac25c30c13b9"></a>

You can update existing Lambda functions with local code\. Updating code in this way doesn't use the AWS Serverless Application Model CLI for deployment and doesn't create an AWS CloudFormation stack\. This way, you can upload a Lambda function with any runtime supported by Lambda\. 

There are several interface options for uploading Lambda functions using the AWS Toolkit\. 

#### Upload from **Environment** window or **Command pane**<a name="upload-lambda-from-environment"></a>

1. In the **Environment window** for your project files, choose the context \(right\-click\) menu for the `template.yaml` for the Lambda application that you want to upload and choose **Upload Lambda**\.

   Alternatively, press **Ctrl\+P** to open the **Go to Anything** pane and enter "lambda" to access the **AWS Upload Lambda** command\. Then, choose it to start the upload process\.

1. Next, select an AWS Region that you want to upload to\.

1. Now choose an option for uploading your Lambda function:

   **Upload a \.zip archive**

   1. Choose **ZIP Archive** from the menu\.

   1. Choose a \.zip file from your AWS Cloud9 file system and choose **Open**\.

   **Upload a directory as is**

   1. Choose **Directory** from the menu\.

   1. Choose a directory from your AWS Cloud9 file system and choose **Open**\.

1. Specify the Lambda function handler that processes events\. When your function is invoked, Lambda runs this handler method\.
**Note**  
When selecting your Lambda function, you can select from the list that's displayed\. If you don't know which function to choose, you can enter the Amazon Resource Number \(ARN\) of a Lambda function that's available in the Toolkit\. 

   A dialog displays asking whether you want this code to be published as the latest version of the Lambda function\. Choose **Yes** to confirm publication\.
**Note**  
You can also upload Lambda applications by opening the context \(right\-click\) menu for the parent folder on the folder and selecting **Upload Lambda**\. The parent folder is automatically selected for upload\.

#### Upload from **AWS Explorer**<a name="upload-lambda-from-explorer"></a>

1. In the **AWS Explorer**, open the context \(right\-click\) menu for the name of the Lambda function that you want to import\.

1. Choose **Upload Lambda**\.

1. Choose from the three options for uploading your Lambda function\.

   **Upload a premade \.zip archive**

   1. Choose **ZIP Archive** from the menu\.

   1. Choose a \.zip file from your AWS Cloud9 file system and choose **Open**\.

   1. Confirm the upload with the modal dialog\. This uploads the \.zip file and is immediately updates the Lambda following deployment\.

   **Upload a directory as is**

   1. Choose **Directory** from the menu\.

   1. Choose a directory from your AWS Cloud9 file system and choose **Open**\.

   1. Choose **No** when prompted to build the directory\.

   1. Confirm the upload with the modal dialog\. This uploads the directory as is and immediately updates the Lambda following deployment\.

   **Build and upload a directory**

   1. Choose **Directory** from the menu\.

   1. Choose a directory from your AWS Cloud9 file system and choose **Open**\.

   1. Choose **Yes** when prompted to build the directory\.

   1. Confirm the upload with the modal dialog\. This builds the code in the directory using the AWS SAM CLI `sam build` command and immediately updates the Lambda following deployment\.

### Deploying a Lambda function for remote access<a name="w94aac25c30c13c11"></a>

You can make your local functions available remotely by deploying them as serverless SAM applications\.

### To deploy a Lambda function as a SAM application

1. In **AWS Explorer**, open the context \(right\-click\) menu for the **Lambda** node, and choose **Deploy SAM Application**\.

1. In the command pane, select the [YAML template](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-specification-template-anatomy.html) that defines your function as a serverless application\.

1. Next, select an Amazon S3 bucket for the Lambda deployment\. You can also choose to create a bucket for the deployment\.

1. Now enter the name of an AWS CloudFormation stack that you're deploying to\. If you specify an existing stack, the command updates the stack\. If you specify a new stack, the command creates it\.

   After you enter the name of the stack, your Lambda function starts to deploy as a SAM application\. After a successful deployment, the SAM Lambda application is available remotely\. That way, you can download or invoke it from other AWS Cloud9 development environments\. 

If you want to create a Lambda function from scratch, we recommend following the steps to [Create a serverless application with the AWS Toolkit](serverless-apps-toolkit.md#create-serverless-app)\.

### Deleting a Lambda function<a name="delete-lambda"></a>

You can also delete a Lambda function using the same context \(right\-click\) menu\.

**Warning**  
Do not use this procedure to delete Lambda functions that are associated with [AWS CloudFormation](https://docs.aws.amazon.com/cloudformation/)\. For example, do not delete the Lambda function that was created when [creating a serverless application](serverless-apps-toolkit.md#sam-create) earlier in this guide\. These functions must be deleted through the AWS CloudFormation stack\.

****

1. In the **AWS Explorer**, choose the name of the Lambda function you want to delete, and then open its context \(right\-menu\)\.

1. Choose **Delete**\.

1. In the message that appears, choose **Yes** to conﬁrm the delete\.

After the function is deleted, it's no longer listed in the **AWS Explorer** view\.