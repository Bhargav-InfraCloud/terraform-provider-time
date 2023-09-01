---
page_title: "time_static Resource - terraform-provider-time"
subcategory: ""
description: |-
  Manages a static time resource, which keeps a locally sourced UTC timestamp stored in the Terraform state. This prevents perpetual differences caused by using the timestamp() function https://www.terraform.io/docs/configuration/functions/timestamp.html.
---


<!-- Please do not edit this file, it is generated. -->
# time_static (Resource)

Manages a static time resource, which keeps a locally sourced UTC timestamp stored in the Terraform state. This prevents perpetual differences caused by using the [`timestamp()` function](https://www.terraform.io/docs/configuration/functions/timestamp.html).

-> Further manipulation of incoming or outgoing values can be accomplished with the [`formatdate()` function](https://www.terraform.io/docs/configuration/functions/formatdate.html) and the [`timeadd()` function](https://www.terraform.io/docs/configuration/functions/timeadd.html).

## Example Usage

### Basic Usage

```python
# DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import TerraformOutput, TerraformStack
#
# Provider bindings are generated by running `cdktf get`.
# See https://cdk.tf/provider-generation for more details.
#
from imports.time.static_resource import StaticResource
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
        example = StaticResource(self, "example")
        TerraformOutput(self, "current_time",
            value=example.rfc3339
        )
```

### Triggers Usage

```python
# DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import Token, Fn, TerraformStack
#
# Provider bindings are generated by running `cdktf get`.
# See https://cdk.tf/provider-generation for more details.
#
from imports.aws.instance import Instance
from imports.time.static_resource import StaticResource
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
        ami_update = StaticResource(self, "ami_update",
            triggers={
                "ami_id": Token.as_string(example.id)
            }
        )
        Instance(self, "server",
            ami=Token.as_string(Fn.lookup_nested(ami_update, ["triggers", "ami_id"])),
            tags={
                "AmiUpdateTime": ami_update.rfc3339
            }
        )
```

<!-- schema generated by tfplugindocs -->
## Schema

### Optional

- `rfc3339` (String) Base timestamp in [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339#section-5.8) format (see [RFC3339 time string](https://tools.ietf.org/html/rfc3339#section-5.8) e.g., `YYYY-MM-DDTHH:MM:SSZ`). Defaults to the current time.
- `triggers` (Map of String) Arbitrary map of values that, when changed, will trigger a new base timestamp value to be saved. See [the main provider documentation](../index.md) for more information.

### Read-Only

- `day` (Number) Number day of timestamp.
- `hour` (Number) Number hour of timestamp.
- `id` (String) RFC3339 format of the offset timestamp, e.g. `2020-02-12T06:36:13Z`.
- `minute` (Number) Number minute of timestamp.
- `month` (Number) Number month of timestamp.
- `second` (Number) Number second of timestamp.
- `unix` (Number) Number of seconds since epoch time, e.g. `1581489373`.
- `year` (Number) Number year of timestamp.


## Import

This resource can be imported using the UTC RFC3339 value, e.g.

```shell
terraform import time_static.example 2020-02-12T06:36:13Z
```

The `triggers` argument cannot be imported.
<!-- cache-key: cdktf-0.18.0 input-2146f927c8bb8e527bb2f114b61e2f9275e5bb5fe013e14866a96eaf7e90c011 556251879b8ed0dc4c87a76b568667e0ab5e2c46efdd14a05c556daf05678783-->