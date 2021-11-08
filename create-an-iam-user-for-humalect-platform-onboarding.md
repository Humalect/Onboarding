Login to your AWS Account and click on this <a href="https://console.aws.amazon.com/iam/home#/policies$new?step=edit" target="_blank">link</a> 

Go to the JSON tab, replace the existing JSON with JSON below.

Replace 7 occurences of 123456789012 in JSON below with your AWS Account ID

Click on next → click on Next: Review on next page → enter name as **humalect-policy** and click on create policy

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "eks:*",
            "Resource": "*"
        },
        {
            "Action": [
                "ssm:GetParameter",
                "ssm:GetParameters"
            ],
            "Resource": [
                "arn:aws:ssm:*:123456789012:parameter/aws/*",
                "arn:aws:ssm:*::parameter/aws/*"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "kms:CreateGrant",
                "kms:DescribeKey"
            ],
            "Resource": "*",
            "Effect": "Allow"
        },
        {
          "Effect": "Allow",
          "Action": [
              "iam:CreateInstanceProfile",
              "iam:DeleteInstanceProfile",
              "iam:GetInstanceProfile",
              "iam:RemoveRoleFromInstanceProfile",
              "iam:GetRole",
              "iam:CreateRole",
              "iam:DeleteRole",
              "iam:AttachRolePolicy",
              "iam:PutRolePolicy",
              "iam:ListInstanceProfiles",
              "iam:AddRoleToInstanceProfile",
              "iam:ListInstanceProfilesForRole",
              "iam:PassRole",
              "iam:DetachRolePolicy",
              "iam:DeleteRolePolicy",
              "iam:GetRolePolicy",
              "iam:GetOpenIDConnectProvider",
              "iam:CreateOpenIDConnectProvider",
              "iam:DeleteOpenIDConnectProvider",
              "iam:TagOpenIDConnectProvider",
              "iam:ListAttachedRolePolicies",
              "iam:TagRole"
          ],
          "Resource": [
              "arn:aws:iam::123456789012:instance-profile/eksctl-*",
              "arn:aws:iam::123456789012:role/eksctl-*",
              "arn:aws:iam::123456789012:oidc-provider/*",
              "arn:aws:iam::123456789012:role/aws-service-role/eks-nodegroup.amazonaws.com/AWSServiceRoleForAmazonEKSNodegroup",
              "arn:aws:iam::123456789012:role/eksctl-managed-*"
          ]
      },
      {
          "Effect": "Allow",
          "Action": [
              "iam:GetRole"
          ],
          "Resource": [
              "arn:aws:iam::123456789012:role/*"
          ]
      },
      {
          "Effect": "Allow",
          "Action": [
              "iam:CreateServiceLinkedRole"
          ],
          "Resource": "*",
          "Condition": {
              "StringEquals": {
                  "iam:AWSServiceName": [
                      "eks.amazonaws.com",
                      "eks-nodegroup.amazonaws.com",
                      "eks-fargate.amazonaws.com"
                  ]
              }
          }
      },
      {
            "Effect": "Allow",
            "Action": "ecr:*",
            "Resource": "*"
        },

        {
            "Action": "ec2:*",
            "Effect": "Allow",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "elasticloadbalancing:*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "cloudwatch:*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "autoscaling:*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "iam:CreateServiceLinkedRole",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:AWSServiceName": [
                        "autoscaling.amazonaws.com",
                        "ec2scheduled.amazonaws.com",
                        "elasticloadbalancing.amazonaws.com",
                        "spot.amazonaws.com",
                        "spotfleet.amazonaws.com",
                        "transitgateway.amazonaws.com"
                    ]
                }
            }
        },

        {
           "Effect": "Allow",
           "Action": [
               "cloudformation:*"
           ],
           "Resource": "*"
       }
    ]
}
```
We just created a new IAM policy, now let's create a new user to be used with Humalect Platform and associate this policy to the user   

click on this [link](https://console.aws.amazon.com/iam/home#/users$new?step=details)  

add name of user as **humalect-user**  

check the box next to **Access key - Programmatic access**  

Click on **Next: Permissions** button  

Click on **Attach existing policies directly** and select the **humalect-policy**that we created in the previous step  

Click on **Next:Tags** -> click on **Next:Review** -> Click on **Create User**

Now you will see AWS ACCESS KEY ID and AWS SECRET ACCESS KEY. Save them both. You have now successfully created a new user for humalect platform and have obtained its API credentials for programmatic access

Return back to the humalect onboarding screen in the previous tab and enter AWS ACCESS KEY ID and AWS SECRET ACCESS KEY that you created

