---
title: IAM policy 기본 실습
weight: 50
pre: "<b>4-2-c. </b>"
---


## AWS IAM Policy 의 종류

AWS의 접근하는 해당 권한을 정의하는 개체로 AWS IAM 리소스들과 연결하여 사용할 수 있습니다.
즉 AWS IAM policy 는 user 에 할당 할 수 도, group 에 할당 할 수 있습니다.
IAM policy 는 여러 타입으로 나누어져있습니다.\

**AWS Managed policy**: AWS에서 먼저 생성해놓은 Policy set 입니다. 사용자가 권한(Permission)을 변경할 수 없습니다.

**Customer Managed policy**: User 가 직접 생성하는 Policy 로 권한을 직접 상세하게 만들어 관리할 수 있습니다.

## IAM user policy 생성

```bash
resource "aws_iam_user" "gildong_hong" {
  name = "gildong.hong"
}

resource "aws_iam_user_policy" "art_devops_black" {
  name  = "super-admin"
  user  = aws_iam_user.gildong_hong.name

  policy = <<EOF
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
EOF
}
```

Terraform Plan 명령어를 통해 생성되는 리소스를 확인합니다.

```bash
  + create

Terraform will perform the following actions:

  # aws_iam_user_policy.art_devops_black will be created
  + resource "aws_iam_user_policy" "art_devops_black" {
      + id     = (known after apply)
      + name   = "super-admin"
      + policy = jsonencode(
            {
              + Statement = [
                  + {
                      + Action   = [
                          + "*",
                        ]
                      + Effect   = "Allow"
                      + Resource = [
                          + "*",
                        ]
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + user   = "gildong.hong"
    }

Plan: 1 to add, 0 to change, 0 to destroy.
```

Terraform apply 를 통해서 리소스를 생성합니다.

```bash

```
