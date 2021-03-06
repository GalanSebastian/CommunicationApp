# Terraform Datadog synthetics monitor

## This module:
- Creates Datadog website synthetics `browser test`, `api test` and `api test with SSL` in Datadog. 
- You can monitor information in your Datadog account.
- You will receive messages about changing the status.


## Usage:

 There are three operating modes: `test_browser`, `test_api`, `test_api/ssl`. 
 - to choose `test_api` mode you should pass variables (`synthetics_type=api` and `synthetics_subtype=http`)
 - to choose `test_api/ssl` mode you should pass variables (`synthetics_type=api` and `synthetics_subtype=ssl`)
 - to choose `browser test`(it runs by default in minimal configuration) you should pass variable (`synthetics_type=browser`)
  

## Examples:

#### Minimal:
```hcl
module "datadog_synthetics" {
  source               = "github.com/PerionNet/terraform-module-datadog-synthetics?ref=v1.0.8"
  env                  = "your-environment"
  name                 = "Frontend Test"
  datadog_secret_name  = "ut-datadog-api-key"
  service_name         = "your-service"
  synthetics_url       = "https://someurl.com"
  notification_targets = [
    "@slack-alerts",    
    "@user@somemail.com"
  ]
}
```

#### Complete:
```hcl
module "datadog_synthetics" {
  source                            = "github.com/PerionNet/terraform-module-datadog-synthetics?ref=v1.0.8"
  enabled                           = true
  env                               = "your-environment"
  name                              = "Frontend Test"
  service_name                      = "your-service"
  api_request_frequency             = 60
  api_assertions                    = [{operator = "is", target = "200", type = "statusCode", property = ""}]
  synthetics_url                    = "https://someurl.com"
  synthetics_type                   = "browser"
  synthetics_subtype                = "laptop_large"
  synthetics_locations              = ["aws:us-west-1"]
  synthetics_device_ids             = ["laptop_large"]
  browser_request_frequency         = 300
  synthetics_alert_down_message     = "There are some problems on:"
  synthetics_alert_up_message       = "The problems are gone on:"
  synthetics_ssl_port               = "443"
  synthetics_ssl_request_frequency  = 900
  synthetics_ssl_accept_self_signed = true
  ssl_assertion_type                = "certificate"
  ssl_assertion_operator            = "isInMoreThan"
  ssl_assertion_target              = 30
  synthetics_status                 = "live"
  datadog_secret_name               = "ut-datadog-api-key"
  notification_targets = [
    "@slack-alerts",
    "@user@somemail.com"
  ]
}
```

<!-- BEGINNING OF GENERATED BY TERRAFORM-DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_datadog"></a> [datadog](#requirement\_datadog) | ~> 2.25 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |
| <a name="provider_datadog"></a> [datadog](#provider\_datadog) | ~> 2.25 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [datadog_synthetics_test.test_api](https://registry.terraform.io/providers/DataDog/datadog/latest/docs/resources/synthetics_test) | resource |
| [datadog_synthetics_test.test_browser](https://registry.terraform.io/providers/DataDog/datadog/latest/docs/resources/synthetics_test) | resource |
| [datadog_synthetics_test.test_ssl](https://registry.terraform.io/providers/DataDog/datadog/latest/docs/resources/synthetics_test) | resource |
| [aws_secretsmanager_secret.datadog_secret](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/secretsmanager_secret) | data source |
| [aws_secretsmanager_secret_version.datadog_secret_version](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/secretsmanager_secret_version) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_api_assertions"></a> [api\_assertions](#input\_api\_assertions) | n/a | `list` | `"operator = is, target = 200, type = statusCode"` | no |
| <a name="input_api_request_frequency"></a> [api\_request\_frequency](#input\_api\_request\_frequency) | n/a | `number` | `60` | no |
| <a name="input_aws_region"></a> [aws\_region](#input\_aws\_region) | aws\_region | `string` | n/a | yes |
| <a name="input_browser_request_frequency"></a> [browser\_request\_frequency](#input\_browser\_request\_frequency) | n/a | `number` | `300` | no |
| <a name="input_datadog_api_key"></a> [datadog\_api\_key](#input\_datadog\_api\_key) | Datadog API Key. You can find out how to get it here: https://docs.datadoghq.com/account_management/api-app-keys/ | `string` | n/a | yes |
| <a name="input_datadog_app_key"></a> [datadog\_app\_key](#input\_datadog\_app\_key) | Datadog APP Key. You can find out how to get it here: https://docs.datadoghq.com/account_management/api-app-keys/ | `string` | n/a | yes |
| <a name="input_datadog_secret_name"></a> [datadog\_secret\_name](#input\_datadog\_secret\_name) | datadog\_secret\_name | `string` | `"ut-datadog-api-key"` | no |
| <a name="input_enabled"></a> [enabled](#input\_enabled) | enabled | `bool` | `true` | no |
| <a name="input_env"></a> [env](#input\_env) | env | `string` | n/a | yes |
| <a name="input_name"></a> [name](#input\_name) | name | `string` | n/a | yes |
| <a name="input_notification_targets"></a> [notification\_targets](#input\_notification\_targets) | List of targets to inform. For example it could be @slack-alerts or @user:name@somemail.com. For more info visit https://docs.datadoghq.com/monitors/notifications/?tab=is_alert#notifications | `list` | n/a | yes |
| <a name="input_service_name"></a> [service\_name](#input\_service\_name) | service\_name | `string` | n/a | yes |
| <a name="input_ssl_assertion_operator"></a> [ssl\_assertion\_operator](#input\_ssl\_assertion\_operator) | n/a | `string` | `"isInMoreThan"` | no |
| <a name="input_ssl_assertion_target"></a> [ssl\_assertion\_target](#input\_ssl\_assertion\_target) | n/a | `number` | `30` | no |
| <a name="input_ssl_assertion_type"></a> [ssl\_assertion\_type](#input\_ssl\_assertion\_type) | n/a | `string` | `"certificate"` | no |
| <a name="input_synthetics_alert_down_message"></a> [synthetics\_alert\_down\_message](#input\_synthetics\_alert\_down\_message) | n/a | `string` | `"There are some problems on:"` | no |
| <a name="input_synthetics_alert_up_message"></a> [synthetics\_alert\_up\_message](#input\_synthetics\_alert\_up\_message) | n/a | `string` | `"The problems are gone on:"` | no |
| <a name="input_synthetics_device_ids"></a> [synthetics\_device\_ids](#input\_synthetics\_device\_ids) | n/a | `list(string)` | <pre>[<br>  "laptop_large"<br>]</pre> | no |
| <a name="input_synthetics_locations"></a> [synthetics\_locations](#input\_synthetics\_locations) | n/a | `list(string)` | <pre>[<br>  "aws:us-east-1"<br>]</pre> | no |
| <a name="input_synthetics_ssl_accept_self_signed"></a> [synthetics\_ssl\_accept\_self\_signed](#input\_synthetics\_ssl\_accept\_self\_signed) | n/a | `bool` | `true` | no |
| <a name="input_synthetics_ssl_port"></a> [synthetics\_ssl\_port](#input\_synthetics\_ssl\_port) | n/a | `string` | `"443"` | no |
| <a name="input_synthetics_ssl_request_frequency"></a> [synthetics\_ssl\_request\_frequency](#input\_synthetics\_ssl\_request\_frequency) | n/a | `number` | `900` | no |
| <a name="input_synthetics_status"></a> [synthetics\_status](#input\_synthetics\_status) | n/a | `string` | `"live"` | no |
| <a name="input_synthetics_subtype"></a> [synthetics\_subtype](#input\_synthetics\_subtype) | synthetics\_subtype | `string` | `"http"` | no |
| <a name="input_synthetics_type"></a> [synthetics\_type](#input\_synthetics\_type) | synthetics\_type | `string` | `"browser"` | no |
| <a name="input_synthetics_url"></a> [synthetics\_url](#input\_synthetics\_url) | synthetics\_type | `string` | n/a | yes |
| <a name="input_api_request_headers"></a> [api_request_headers](#input\api_request_headers) | n/a | `map` | n/a | no |
| <a name="input_min_failure_duration"></a> [min_failure_duration](#input\_ssl\_assertion\_min_failure_duration) | n/a | `number` | `300` | no |
| <a name="input_ssl_assertion_target"></a> [min_location_failed](#input\_ssl\_assertion\_min_location_failed) | n/a | `number` | `3` | no |

## Outputs

No outputs.

<!-- END OF GENERATED BY TERRAFORM-DOCS -->
