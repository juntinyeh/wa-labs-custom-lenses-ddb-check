---
title: "Publish Custom Lense on WA Tool"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 4
pre: "<b>4. </b>"
---


### Create custom lens

#### Upload to AWS Console and publish
After previous steps, now we created a full scope custom lenses in JSON format. Now it's time to create the custom lense on our AWS Well-Architected Tool.

* Open AWS Console > Well-Architected Tool > Custom Lenses

* Click "**Create Custom Lens**" > upload the finalized JSON we produced from step3. Or you can try with [sample files](#sample-json-files).

* For more detail on how to publish a custom lens, please refer to [this blog](
https://aws.amazon.com/blogs/aws/well-architected-custom-lenses-internal-best-practices/)).

* After the custom lens created, to [create a workload](../../100_walkthrough_of_the_well-architected_tool/2_create_workload/) for custom lens [review](../../100_walkthrough_of_the_well-architected_tool/3_perform_review/) will all goes the same way as Well-Architected Framework Review.

#### Test the RiskRule and check all the information is ready

* After we created a custom lens and workload, we can start to check the RiskRule work correctly defined in our JSON. 

* Also, to prepare all the related information in the "HelpfulResource" for each choice will give reviewer more clear guidance. For example on the Amazon DynamoDB Point-In-Time Recovery feature, it give a timely explaination if we put a brief text on the "displayText" attribute. 

* In each **"helpfulResource"**, the ***"url"*** can point to external page like service documentation or developer guide, etc.

```
"choices": [
	{
     "id":"ddbops1_2",
     "title":"Enable DynamoDB PITR",
     "description":"Some helpful choice description",
     "helpfulResource":{
        "displayText":"Point-in-time recovery (PITR) provides continuous backups of your DynamoDB table data. When enabled, DynamoDB maintains incremental backups of your table for the last 35 days until you explicitly turn it off.",
        "url":"https://aws.amazon.com/dynamodb/pitr/"
     },
     "improvementPlan":{
        "displayText":"Enable Dynamodb PITR",
        "url":"https://aws.amazon.com/dynamodb/pitr/"
     }
	},
	{
		...
	}
]
```

* With all the reference information ready in the JSON, we will able to a review question looks as follow: indicating to recommended best practices, detail explaination and reference link available. 

![CheckBPInfo](/watool/100_Custom_Lenses_on_WATool/images/WACL41.jpg)

#### JSON Example:

* After previous steps, now we can have a full structure for our first question, with **pillar id**, pillar name, **question id** and descriptions, **choice id** and all the related resource we need to form up this question. The JSON structure for AWS Well-Architected Tool will looks like this:


```
{
   "schemaVersion":"2021-11-01",
   "name":"DynamoDB Best Practice Lens",
   "description":"Best practices for optimization your DynamoDB",
   "pillars":[
        {
         "id":"DDBOPS",
         "name":"Operational Excellence",
         "questions":[
            {
               "id":"ddbops1",
               "title":"How do you backup DynamoDB tables?",
               "description":"With proper backup process, you will be able to prevent unexpected data lost.",
               "choices":[
                  {
                     "id":"ddbops1_1",
                     "title":"Manually trigger Amazon DynamoDB Backup process",
                     "description":"Either use AWS Console or CLI to trigger a table backup.",
                     "helpfulResource":{
                        "displayText":"Amazon DynamoDB supports stand-alone on-demand backup and restores features. Those features are available to you independent of whether you use AWS Backup.",
                        "url":"https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/BackupRestore.html"
                     },
                     "improvementPlan":{
                        "displayText":"Have a regular process to trigger backup process on Amazon DynamoDB",
                        "url":"https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/BackupRestore.html"
                     }
                  },
                  {
                     "id":"ddbops1_2",
                     "title":"Enable DynamoDB PITR",
                     "description":"Some helpful choice description",
                     "helpfulResource":{
                        "displayText":"Point-in-time recovery (PITR) provides continuous backups of your DynamoDB table data. When enabled, DynamoDB maintains incremental backups of your table for the last 35 days until you explicitly turn it off.",
                        "url":"https://aws.amazon.com/dynamodb/pitr/"

                     },
                     "improvementPlan":{
                        "displayText":"Enable Dynamodb PITR",
                        "url":"https://aws.amazon.com/dynamodb/pitr/"
                     }
                  },
                  {
                     "id":"ddbops1_3",
                     "title":"Use AWS Backup for DynamoDB tables",
                     "description":"Some helpful choice description",
                     "helpfulResource":{
                        "displayText":"AWS Backup is a fully-managed service that makes it easy to centralize and automate data protection across AWS services, in the cloud, and on premises.",
                        "url":"https://docs.aws.amazon.com/aws-backup/latest/devguide/about-backup-plans.html"
                     },
                     "improvementPlan":{
                        "displayText":"Use AWS Backup"
                     }
                  },
                  {
                     "id":"ddbops1_4",
                     "title":"Export DynamoDB to other storage media",
                     "description":"Some helpful choice description",
                     "helpfulResource":{
                        "displayText":"Using DynamoDB table export, you can export data from an Amazon DynamoDB table from any time within your point-in-time recovery window to an Amazon S3 bucket.",
                        "url":"https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DataExport.html"
                     },
                     "improvementPlan":{
                        "displayText":"Export Dynamodb To S3"
                     }
                  },
                  {
                     "id":"ddbops1_5",
                     "title":"None of above",
                     "description":"Some helpful choice description",
                     "helpfulResource":{
                        "displayText":"-"
                     },
                     "improvementPlan":{
                        "displayText":"Setup backup process"
                     }
                  }
               ],
               "riskRules":[
                  {
                     "condition":"ddbops1_1 && ddbops1_2 && ddbops1_3 && ddbops1_4",
                     "risk":"NO_RISK"
                  },
                  {
                     "condition":"(!ddbops1_1) || ddbops1_5",
                     "risk":"HIGH_RISK"
                  },
                  {
                     "condition":"default",
                     "risk":"MEDIUM_RISK"
                  }
               ]
            }
         }]
      }
   ]
}
```

And for the 
[Custom lens sample - Dynamodb Configuration Check](https://github.com/aws-samples/custom-lens-wa-sample/tree/main/dynamodb), please check the latest update in aws-samples [repository](https://github.com/aws-samples/custom-lens-wa-sample/). 


{{< prev_next_button link_prev_url="../3_ddb_config_options_risks/" link_next_url="../5_tear_down/" />}}
