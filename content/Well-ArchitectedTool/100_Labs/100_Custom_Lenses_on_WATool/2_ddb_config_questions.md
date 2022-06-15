---
title: "Structure of a custom lenses - Questions"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---


### Questions in Custom Pillars:

After pillars been defined, we start to work on related key items we want to focus in each pillar. We aggregated different options for a best practices, and design the logic behind the question, to identify if that was a potential high risk or in medium level. 

Take DynamoDB as example, operating team and development team want to make sure a valid backup for DynamoDB table is always there, Custom Lens author decided to collect all the possible options for this purpose. 

Since we are going to setup a check item in operating procedure, we decided to put this question into one custom pillar - *Operating Readiness*.

#### How to backup your data in DynamoDB table?

Reference on [Amazon DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/), we found a clear guidance on [Backing Up a DynamoDB Table](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Backup.Tutorial.html) providing two options: *Create a table backup from Console* and *Create a Table backup from CLI*. These two options were both require manual process. 
So here we have one "Choice" been appended:

`Manually trigger Amazon DynamoDB Backup process` - *Means backup process been handled by it's native bacup feature, a full backup.*

To improve the operating process as a long term goal, also aligned with the Design Principles - "Perform operations as code" (AWS Well-Architected Framework, Operational Excellence Pillar), we start to collect more possible options on automation backup. 
We found that DynamoDB natively support Point-in-time recovery (PITR) feature, it provides continuous backups for DynamoDB table data. Also the AWS Backup is another fully-managed service that can automate the backup process. Thus, we have two more "Choices":

`Enable Amazon DynamoDB PITR Feature` - *A native support feature, but it provide point-in-time restore.*

`Use AWS Backup for Amazon DynamoDB tabls` - *Leverage another service, which might aligned with broader backup purpose and multiple data sources.*

In some cases, we found out the operating team could use Amazon DynamoDB [Data Export](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DataExport.html) feature to have a full duplication on table. Also give us an insight that this can also be achieved with direct API call or table scan. So we append a new choice to cover the export behavior which operating team and store the backup into preferred storage media.

`Export DynamoDB to other storage media` 

After researching and collecting all the related data for this questions, the lens JSON now will looks like this:

```
.....
                   "choices": [
                        {
                            "id": "choice1",
                            "title": "Manually trigger Amazon DynamoDB Backup process",
                            ...
                            },
                            "improvementPlan": {
                                "displayText": "This is text that will be shown for improvement of this choice."
                            }
                        },
                        {
                            "id": "choice2",
                            "title": "Enable Amazon DynamoDB PITR Feature",
                            ...
                        },
                        {
                            "id": "choice3",
                            "title": "Use AWS Backup for Amazon DynamoDB tabls",
                            ...
                        },
                        {
                            "id": "choice4",
                            "title": "Export DynamoDB to other storage media",
                            ...
                        }

                        ....

```

And, we put an default one to cover some cases not really apply with these options. 

```
                        {
                            "id": "choice5",
                            "title": "None of Above",
                            ...
                        }
```

{{< prev_next_button link_prev_url="../1_ddb_config_pillars_and_bps/" link_next_url="../3_ddb_config_options_risks/" />}}
