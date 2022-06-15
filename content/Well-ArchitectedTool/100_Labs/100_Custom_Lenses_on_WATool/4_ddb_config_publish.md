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

#### Sample JSON files:

* [Custom lens sample - Dynamodb Configuration Check](/watool/100_Custom_Lenses_on_WATool/JSON/custom_lense_ddb_config_check_2022Q2.JSON)



{{< prev_next_button link_prev_url="../3_ddb_config_options_risks/" link_next_url="../5_tear_down/" />}}
