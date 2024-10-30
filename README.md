

<!-- markdownlint-disable -->
<a href="https://cpco.io/homepage"><img src="https://github.com/cloudposse/terraform-aws-ses/blob/main/.github/banner.png?raw=true" alt="Project Banner"/></a><br/>
    <p align="right">
<a href="https://github.com/cloudposse/terraform-aws-ses/releases/latest"><img src="https://img.shields.io/github/release/cloudposse/terraform-aws-ses.svg?style=for-the-badge" alt="Latest Release"/></a><a href="https://github.com/cloudposse/terraform-aws-ses/commits"><img src="https://img.shields.io/github/last-commit/cloudposse/terraform-aws-ses.svg?style=for-the-badge" alt="Last Updated"/></a><a href="https://slack.cloudposse.com"><img src="https://slack.cloudposse.com/for-the-badge.svg" alt="Slack Community"/></a></p>
<!-- markdownlint-restore -->

<!--




  ** DO NOT EDIT THIS FILE
  **
  ** This file was automatically generated by the `cloudposse/build-harness`.
  ** 1) Make all changes to `README.yaml`
  ** 2) Run `make init` (you only need to do this once)
  ** 3) Run`make readme` to rebuild this file.
  **
  ** (We maintain HUNDREDS of open source projects. This is how we maintain our sanity.)
  **





-->

Terraform module to provision Simple Email Service on AWS.


> [!TIP]
> #### 👽 Use Atmos with Terraform
> Cloud Posse uses [`atmos`](https://atmos.tools) to easily orchestrate multiple environments using Terraform. <br/>
> Works with [Github Actions](https://atmos.tools/integrations/github-actions/), [Atlantis](https://atmos.tools/integrations/atlantis), or [Spacelift](https://atmos.tools/integrations/spacelift).
>
> <details>
> <summary><strong>Watch demo of using Atmos with Terraform</strong></summary>
> <img src="https://github.com/cloudposse/atmos/blob/master/docs/demo.gif?raw=true"/><br/>
> <i>Example of running <a href="https://atmos.tools"><code>atmos</code></a> to manage infrastructure from our <a href="https://atmos.tools/quick-start/">Quick Start</a> tutorial.</i>
> </detalis>





## Usage

This module creates a SES domain with IAM user that is able to send emails with it.
If module is provided with Route53 Zone ID it can also create verification DNS records for domain and DKIM.

For a complete example, see [examples/complete](examples/complete).

For automated tests of the complete example using [bats](https://github.com/bats-core/bats-core) and [Terratest](https://github.com/gruntwork-io/terratest) (which tests and deploys the example on AWS), see [test](test).

What's worth to note is that every AWS SES starts in Sandbox. Sending emails via it (emails not verified in AWS SES) is only allowed after support request.

SES availability in regions can be checked in [latest AWS General Reference](https://docs.aws.amazon.com/general/latest/gr/ses.html)

> [!IMPORTANT]
> In Cloud Posse's examples, we avoid pinning modules to specific versions to prevent discrepancies between the documentation
> and the latest released versions. However, for your own projects, we strongly advise pinning each module to the exact version
> you're using. This practice ensures the stability of your infrastructure. Additionally, we recommend implementing a systematic
> approach for updating versions to avoid unexpected changes.








<!-- markdownlint-disable -->
## Makefile Targets
```text
Available targets:

  help                                Help screen
  help/all                            Display help for all targets
  help/short                          This help short screen
  lint                                Lint terraform code

```
<!-- markdownlint-restore -->
<!-- markdownlint-disable -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.1.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 2.0 |
| <a name="requirement_awsutils"></a> [awsutils](#requirement\_awsutils) | >= 0.11.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 2.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_ses_user"></a> [ses\_user](#module\_ses\_user) | cloudposse/iam-system-user/aws | 0.23.2 |
| <a name="module_this"></a> [this](#module\_this) | cloudposse/label/null | 0.25.0 |

## Resources

| Name | Type |
|------|------|
| [aws_iam_group.ses_users](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_group) | resource |
| [aws_iam_group_policy.ses_group_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_group_policy) | resource |
| [aws_iam_user_group_membership.ses_user](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_group_membership) | resource |
| [aws_iam_user_policy.sending_emails](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_policy) | resource |
| [aws_route53_record.amazonses_dkim_record](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record) | resource |
| [aws_route53_record.amazonses_spf_record](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record) | resource |
| [aws_route53_record.amazonses_verification_record](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record) | resource |
| [aws_route53_record.custom_mail_from_mx](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record) | resource |
| [aws_ses_domain_dkim.ses_domain_dkim](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ses_domain_dkim) | resource |
| [aws_ses_domain_identity.ses_domain](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ses_domain_identity) | resource |
| [aws_ses_domain_mail_from.custom_mail_from](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ses_domain_mail_from) | resource |
| [aws_iam_policy_document.ses_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_region.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/region) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_additional_tag_map"></a> [additional\_tag\_map](#input\_additional\_tag\_map) | Additional key-value pairs to add to each map in `tags_as_list_of_maps`. Not added to `tags` or `id`.<br/>This is for some rare cases where resources want additional configuration of tags<br/>and therefore take a list of maps with tag key, value, and additional configuration. | `map(string)` | `{}` | no |
| <a name="input_attributes"></a> [attributes](#input\_attributes) | ID element. Additional attributes (e.g. `workers` or `cluster`) to add to `id`,<br/>in the order they appear in the list. New attributes are appended to the<br/>end of the list. The elements of the list are joined by the `delimiter`<br/>and treated as a single ID element. | `list(string)` | `[]` | no |
| <a name="input_context"></a> [context](#input\_context) | Single object for setting entire context at once.<br/>See description of individual variables for details.<br/>Leave string and numeric variables as `null` to use default value.<br/>Individual variable settings (non-null) override settings in context object,<br/>except for attributes, tags, and additional\_tag\_map, which are merged. | `any` | <pre>{<br/>  "additional_tag_map": {},<br/>  "attributes": [],<br/>  "delimiter": null,<br/>  "descriptor_formats": {},<br/>  "enabled": true,<br/>  "environment": null,<br/>  "id_length_limit": null,<br/>  "label_key_case": null,<br/>  "label_order": [],<br/>  "label_value_case": null,<br/>  "labels_as_tags": [<br/>    "unset"<br/>  ],<br/>  "name": null,<br/>  "namespace": null,<br/>  "regex_replace_chars": null,<br/>  "stage": null,<br/>  "tags": {},<br/>  "tenant": null<br/>}</pre> | no |
| <a name="input_create_spf_record"></a> [create\_spf\_record](#input\_create\_spf\_record) | If provided the module will create an SPF record for `domain`. | `bool` | `false` | no |
| <a name="input_custom_from_behavior_on_mx_failure"></a> [custom\_from\_behavior\_on\_mx\_failure](#input\_custom\_from\_behavior\_on\_mx\_failure) | The behaviour of the custom\_from\_subdomain when the MX record is not found. Defaults to `UseDefaultValue`. | `string` | `"UseDefaultValue"` | no |
| <a name="input_custom_from_dns_record_enabled"></a> [custom\_from\_dns\_record\_enabled](#input\_custom\_from\_dns\_record\_enabled) | If enabled the module will create a Route53 DNS record for the `From` address subdomain. | `bool` | `true` | no |
| <a name="input_custom_from_subdomain"></a> [custom\_from\_subdomain](#input\_custom\_from\_subdomain) | If provided the module will create a custom subdomain for the `From` address. | `list(string)` | `[]` | no |
| <a name="input_delimiter"></a> [delimiter](#input\_delimiter) | Delimiter to be used between ID elements.<br/>Defaults to `-` (hyphen). Set to `""` to use no delimiter at all. | `string` | `null` | no |
| <a name="input_descriptor_formats"></a> [descriptor\_formats](#input\_descriptor\_formats) | Describe additional descriptors to be output in the `descriptors` output map.<br/>Map of maps. Keys are names of descriptors. Values are maps of the form<br/>`{<br/>   format = string<br/>   labels = list(string)<br/>}`<br/>(Type is `any` so the map values can later be enhanced to provide additional options.)<br/>`format` is a Terraform format string to be passed to the `format()` function.<br/>`labels` is a list of labels, in order, to pass to `format()` function.<br/>Label values will be normalized before being passed to `format()` so they will be<br/>identical to how they appear in `id`.<br/>Default is `{}` (`descriptors` output will be empty). | `any` | `{}` | no |
| <a name="input_domain"></a> [domain](#input\_domain) | The domain to create the SES identity for. | `string` | n/a | yes |
| <a name="input_enabled"></a> [enabled](#input\_enabled) | Set to false to prevent the module from creating any resources | `bool` | `null` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | ID element. Usually used for region e.g. 'uw2', 'us-west-2', OR role 'prod', 'staging', 'dev', 'UAT' | `string` | `null` | no |
| <a name="input_iam_access_key_max_age"></a> [iam\_access\_key\_max\_age](#input\_iam\_access\_key\_max\_age) | Maximum age of IAM access key (seconds). Defaults to 30 days. Set to 0 to disable expiration. | `number` | `2592000` | no |
| <a name="input_iam_allowed_resources"></a> [iam\_allowed\_resources](#input\_iam\_allowed\_resources) | Specifies resource ARNs that are enabled for `var.iam_permissions`. Wildcards are acceptable. | `list(string)` | `[]` | no |
| <a name="input_iam_permissions"></a> [iam\_permissions](#input\_iam\_permissions) | Specifies permissions for the IAM user. | `list(string)` | <pre>[<br/>  "ses:SendRawEmail"<br/>]</pre> | no |
| <a name="input_id_length_limit"></a> [id\_length\_limit](#input\_id\_length\_limit) | Limit `id` to this many characters (minimum 6).<br/>Set to `0` for unlimited length.<br/>Set to `null` for keep the existing setting, which defaults to `0`.<br/>Does not affect `id_full`. | `number` | `null` | no |
| <a name="input_label_key_case"></a> [label\_key\_case](#input\_label\_key\_case) | Controls the letter case of the `tags` keys (label names) for tags generated by this module.<br/>Does not affect keys of tags passed in via the `tags` input.<br/>Possible values: `lower`, `title`, `upper`.<br/>Default value: `title`. | `string` | `null` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | The order in which the labels (ID elements) appear in the `id`.<br/>Defaults to ["namespace", "environment", "stage", "name", "attributes"].<br/>You can omit any of the 6 labels ("tenant" is the 6th), but at least one must be present. | `list(string)` | `null` | no |
| <a name="input_label_value_case"></a> [label\_value\_case](#input\_label\_value\_case) | Controls the letter case of ID elements (labels) as included in `id`,<br/>set as tag values, and output by this module individually.<br/>Does not affect values of tags passed in via the `tags` input.<br/>Possible values: `lower`, `title`, `upper` and `none` (no transformation).<br/>Set this to `title` and set `delimiter` to `""` to yield Pascal Case IDs.<br/>Default value: `lower`. | `string` | `null` | no |
| <a name="input_labels_as_tags"></a> [labels\_as\_tags](#input\_labels\_as\_tags) | Set of labels (ID elements) to include as tags in the `tags` output.<br/>Default is to include all labels.<br/>Tags with empty values will not be included in the `tags` output.<br/>Set to `[]` to suppress all generated tags.<br/>**Notes:**<br/>  The value of the `name` tag, if included, will be the `id`, not the `name`.<br/>  Unlike other `null-label` inputs, the initial setting of `labels_as_tags` cannot be<br/>  changed in later chained modules. Attempts to change it will be silently ignored. | `set(string)` | <pre>[<br/>  "default"<br/>]</pre> | no |
| <a name="input_name"></a> [name](#input\_name) | ID element. Usually the component or solution name, e.g. 'app' or 'jenkins'.<br/>This is the only ID element not also included as a `tag`.<br/>The "name" tag is set to the full `id` string. There is no tag with the value of the `name` input. | `string` | `null` | no |
| <a name="input_namespace"></a> [namespace](#input\_namespace) | ID element. Usually an abbreviation of your organization name, e.g. 'eg' or 'cp', to help ensure generated IDs are globally unique | `string` | `null` | no |
| <a name="input_regex_replace_chars"></a> [regex\_replace\_chars](#input\_regex\_replace\_chars) | Terraform regular expression (regex) string.<br/>Characters matching the regex will be removed from the ID elements.<br/>If not set, `"/[^a-zA-Z0-9-]/"` is used to remove all characters other than hyphens, letters and digits. | `string` | `null` | no |
| <a name="input_ses_group_enabled"></a> [ses\_group\_enabled](#input\_ses\_group\_enabled) | Creates a group with permission to send emails from SES domain | `bool` | `true` | no |
| <a name="input_ses_group_name"></a> [ses\_group\_name](#input\_ses\_group\_name) | The name of the IAM group to create. If empty the module will calculate name from a context (recommended). | `string` | `""` | no |
| <a name="input_ses_group_path"></a> [ses\_group\_path](#input\_ses\_group\_path) | The IAM Path of the group to create | `string` | `"/"` | no |
| <a name="input_ses_user_enabled"></a> [ses\_user\_enabled](#input\_ses\_user\_enabled) | Creates user with permission to send emails from SES domain | `bool` | `true` | no |
| <a name="input_stage"></a> [stage](#input\_stage) | ID element. Usually used to indicate role, e.g. 'prod', 'staging', 'source', 'build', 'test', 'deploy', 'release' | `string` | `null` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | Additional tags (e.g. `{'BusinessUnit': 'XYZ'}`).<br/>Neither the tag keys nor the tag values will be modified by this module. | `map(string)` | `{}` | no |
| <a name="input_tenant"></a> [tenant](#input\_tenant) | ID element \_(Rarely used, not included by default)\_. A customer identifier, indicating who this instance of a resource is for | `string` | `null` | no |
| <a name="input_verify_dkim"></a> [verify\_dkim](#input\_verify\_dkim) | If provided the module will create Route53 DNS records used for DKIM verification. | `bool` | `false` | no |
| <a name="input_verify_domain"></a> [verify\_domain](#input\_verify\_domain) | If provided the module will create Route53 DNS records used for domain verification. | `bool` | `false` | no |
| <a name="input_zone_id"></a> [zone\_id](#input\_zone\_id) | Route53 parent zone ID. If provided (not empty), the module will create Route53 DNS records used for verification | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_access_key_id"></a> [access\_key\_id](#output\_access\_key\_id) | The SMTP user which is access key ID. |
| <a name="output_custom_from_domain"></a> [custom\_from\_domain](#output\_custom\_from\_domain) | The custom mail FROM domain |
| <a name="output_secret_access_key"></a> [secret\_access\_key](#output\_secret\_access\_key) | The IAM secret for usage with SES API. This will be written to the state file in plain text. |
| <a name="output_ses_dkim_tokens"></a> [ses\_dkim\_tokens](#output\_ses\_dkim\_tokens) | A list of DKIM Tokens which, when added to the DNS Domain as CNAME records, allows for receivers to verify that emails were indeed authorized by the domain owner. |
| <a name="output_ses_domain_identity_arn"></a> [ses\_domain\_identity\_arn](#output\_ses\_domain\_identity\_arn) | The ARN of the SES domain identity |
| <a name="output_ses_domain_identity_verification_token"></a> [ses\_domain\_identity\_verification\_token](#output\_ses\_domain\_identity\_verification\_token) | A code which when added to the domain as a TXT record will signal to SES that the owner of the domain has authorised SES to act on their behalf. The domain identity will be in state 'verification pending' until this is done. See below for an example of how this might be achieved when the domain is hosted in Route 53 and managed by Terraform. Find out more about verifying domains in Amazon SES in the AWS SES docs. |
| <a name="output_ses_group_name"></a> [ses\_group\_name](#output\_ses\_group\_name) | The IAM group name |
| <a name="output_ses_smtp_password"></a> [ses\_smtp\_password](#output\_ses\_smtp\_password) | The SMTP password. This will be written to the state file in plain text. |
| <a name="output_spf_record"></a> [spf\_record](#output\_spf\_record) | The SPF record for the domain. This is a TXT record that should be added to the domain's DNS settings to allow SES to send emails on behalf of the domain. |
| <a name="output_user_arn"></a> [user\_arn](#output\_user\_arn) | The ARN assigned by AWS for this user. |
| <a name="output_user_name"></a> [user\_name](#output\_user\_name) | Normalized IAM user name. |
| <a name="output_user_unique_id"></a> [user\_unique\_id](#output\_user\_unique\_id) | The unique ID assigned by AWS. |
<!-- markdownlint-restore -->




> [!TIP]
> #### Use Terraform Reference Architectures for AWS
>
> Use Cloud Posse's ready-to-go [terraform architecture blueprints](https://cloudposse.com/reference-architecture/) for AWS to get up and running quickly.
>
> ✅ We build it together with your team.<br/>
> ✅ Your team owns everything.<br/>
> ✅ 100% Open Source and backed by fanatical support.<br/>
>
> <a href="https://cpco.io/commercial-support?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=commercial_support"><img alt="Request Quote" src="https://img.shields.io/badge/request%20quote-success.svg?style=for-the-badge"/></a>
> <details><summary>📚 <strong>Learn More</strong></summary>
>
> <br/>
>
> Cloud Posse is the leading [**DevOps Accelerator**](https://cpco.io/commercial-support?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=commercial_support) for funded startups and enterprises.
>
> *Your team can operate like a pro today.*
>
> Ensure that your team succeeds by using Cloud Posse's proven process and turnkey blueprints. Plus, we stick around until you succeed.
> #### Day-0:  Your Foundation for Success
> - **Reference Architecture.** You'll get everything you need from the ground up built using 100% infrastructure as code.
> - **Deployment Strategy.** Adopt a proven deployment strategy with GitHub Actions, enabling automated, repeatable, and reliable software releases.
> - **Site Reliability Engineering.** Gain total visibility into your applications and services with Datadog, ensuring high availability and performance.
> - **Security Baseline.** Establish a secure environment from the start, with built-in governance, accountability, and comprehensive audit logs, safeguarding your operations.
> - **GitOps.** Empower your team to manage infrastructure changes confidently and efficiently through Pull Requests, leveraging the full power of GitHub Actions.
>
> <a href="https://cpco.io/commercial-support?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=commercial_support"><img alt="Request Quote" src="https://img.shields.io/badge/request%20quote-success.svg?style=for-the-badge"/></a>
>
> #### Day-2: Your Operational Mastery
> - **Training.** Equip your team with the knowledge and skills to confidently manage the infrastructure, ensuring long-term success and self-sufficiency.
> - **Support.** Benefit from a seamless communication over Slack with our experts, ensuring you have the support you need, whenever you need it.
> - **Troubleshooting.** Access expert assistance to quickly resolve any operational challenges, minimizing downtime and maintaining business continuity.
> - **Code Reviews.** Enhance your team’s code quality with our expert feedback, fostering continuous improvement and collaboration.
> - **Bug Fixes.** Rely on our team to troubleshoot and resolve any issues, ensuring your systems run smoothly.
> - **Migration Assistance.** Accelerate your migration process with our dedicated support, minimizing disruption and speeding up time-to-value.
> - **Customer Workshops.** Engage with our team in weekly workshops, gaining insights and strategies to continuously improve and innovate.
>
> <a href="https://cpco.io/commercial-support?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=commercial_support"><img alt="Request Quote" src="https://img.shields.io/badge/request%20quote-success.svg?style=for-the-badge"/></a>
> </details>

## ✨ Contributing

This project is under active development, and we encourage contributions from our community.



Many thanks to our outstanding contributors:

<a href="https://github.com/cloudposse/terraform-aws-ses/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=cloudposse/terraform-aws-ses&max=24" />
</a>

For 🐛 bug reports & feature requests, please use the [issue tracker](https://github.com/cloudposse/terraform-aws-ses/issues).

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.
 1. Review our [Code of Conduct](https://github.com/cloudposse/terraform-aws-ses/?tab=coc-ov-file#code-of-conduct) and [Contributor Guidelines](https://github.com/cloudposse/.github/blob/main/CONTRIBUTING.md).
 2. **Fork** the repo on GitHub
 3. **Clone** the project to your own machine
 4. **Commit** changes to your own branch
 5. **Push** your work back up to your fork
 6. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!

### 🌎 Slack Community

Join our [Open Source Community](https://cpco.io/slack?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=slack) on Slack. It's **FREE** for everyone! Our "SweetOps" community is where you get to talk with others who share a similar vision for how to rollout and manage infrastructure. This is the best place to talk shop, ask questions, solicit feedback, and work together as a community to build totally *sweet* infrastructure.

### 📰 Newsletter

Sign up for [our newsletter](https://cpco.io/newsletter?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=newsletter) and join 3,000+ DevOps engineers, CTOs, and founders who get insider access to the latest DevOps trends, so you can always stay in the know.
Dropped straight into your Inbox every week — and usually a 5-minute read.

### 📆 Office Hours <a href="https://cloudposse.com/office-hours?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=office_hours"><img src="https://img.cloudposse.com/fit-in/200x200/https://cloudposse.com/wp-content/uploads/2019/08/Powered-by-Zoom.png" align="right" /></a>

[Join us every Wednesday via Zoom](https://cloudposse.com/office-hours?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=office_hours) for your weekly dose of insider DevOps trends, AWS news and Terraform insights, all sourced from our SweetOps community, plus a _live Q&A_ that you can’t find anywhere else.
It's **FREE** for everyone!
## License

<a href="https://opensource.org/licenses/Apache-2.0"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge" alt="License"></a>

<details>
<summary>Preamble to the Apache License, Version 2.0</summary>
<br/>
<br/>

Complete license is available in the [`LICENSE`](LICENSE) file.

```text
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
```
</details>

## Trademarks

All other trademarks referenced herein are the property of their respective owners.


---
Copyright © 2017-2024 [Cloud Posse, LLC](https://cpco.io/copyright)


<a href="https://cloudposse.com/readme/footer/link?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-ses&utm_content=readme_footer_link"><img alt="README footer" src="https://cloudposse.com/readme/footer/img"/></a>

<img alt="Beacon" width="0" src="https://ga-beacon.cloudposse.com/UA-76589703-4/cloudposse/terraform-aws-ses?pixel&cs=github&cm=readme&an=terraform-aws-ses"/>
