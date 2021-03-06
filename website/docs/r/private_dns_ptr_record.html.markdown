---
subcategory: "Private DNS"
layout: "azurerm"
page_title: "Azure Resource Manager: azurerm_private_dns_ptr_record"
sidebar_current: "docs-azurerm-resource-private-dns-ptr-record"
description: |-
  Manages a Private DNS PTR Record.
---

# azurerm_private_dns_ptr_record

Enables you to manage DNS PTR Records within Azure Private DNS.

## Example Usage

```hcl
resource "azurerm_resource_group" "test" {
  name     = "acceptanceTestResourceGroup1"
  location = "West US"
}

resource "azurerm_private_dns_zone" "test" {
  name                = "2.0.192.in-addr.arpa"
  resource_group_name = "${azurerm_resource_group.test.name}"
}

resource "azurerm_private_dns_ptr_record" "test" {
  name                = "15"
  zone_name           = "${azurerm_private_dns_zone.test.name}"
  resource_group_name = "${azurerm_resource_group.test.name}"
  ttl                 = 300
  records             = ["test.example.com"]
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the DNS PTR Record. Changing this forces a new resource to be created.

* `resource_group_name` - (Required) Specifies the resource group where the resource exists. Changing this forces a new resource to be created.

* `zone_name` - (Required) Specifies the Private DNS Zone where the resource exists. Changing this forces a new resource to be created.

* `ttl ` - (Required) The Time To Live (TTL) of the DNS record in seconds.

* `records` - (Required) List of Fully Qualified Domain Names.

* `tags` - (Optional) A mapping of tags to assign to the resource.

## Attributes Reference

The following attributes are exported:

* `id` - The Private DNS PTR Record ID.

## Import

Private DNS PTR Records can be imported using the `resource id`, e.g.

```shell
terraform import azurerm_private_dns_ptr_record.test /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mygroup1/providers/Microsoft.Network/privateDnsZones/2.0.192.in-addr.arpa/PTR/15
```
