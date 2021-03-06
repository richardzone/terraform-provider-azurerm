---
subcategory: "Storage"
layout: "azurerm"
page_title: "Azure Resource Manager: azurerm_storage_data_lake_gen2_filesystem"
sidebar_current: "docs-azurerm-resource-storage-data-lake-gen2-filesystem"
description: |-
  Manages a Data Lake Gen2 File System within an Azure Storage Account.
---

# azurerm_storage_data_lake_gen2_filesystem

Manages a Data Lake Gen2 File System within an Azure Storage Account.

~> **NOTE:** This Resource requires using Azure Active Directory to connect to Azure Storage, which in turn requires the `Storage` specific roles - which are not granted by default.

## Example Usage

```hcl
resource "azurerm_resource_group" "test" {
  name     = "example-resources"
  location = "West Europe"
}

resource "azurerm_storage_account" "test" {
  name                     = "examplestorageacc"
  resource_group_name      = azurerm_resource_group.test.name
  location                 = azurerm_resource_group.test.location
  account_tier             = "Standard"
  account_replication_type = "LRS"
  account_kind             = "StorageV2"
  is_hns_enabled           = "true"
}

resource "azurerm_storage_data_lake_gen2_filesystem" "test" {
  name               = "example"
  storage_account_id = azurerm_storage_account.test.id

  properties = {
    hello = "aGVsbG8="
  }
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the Data Lake Gen2 File System which should be created within the Storage Account. Must be unique within the storage account the queue is located. Changing this forces a new resource to be created.

* `storage_account_id` - (Required) Specifies the ID of the Storage Account in which the Data Lake Gen2 File System should exist. Changing this forces a new resource to be created.

~> **NOTE:** The Storage Account requires `account_kind` to be either `StorageV2` or `BlobStorage`. In addition, `is_hns_enabled` has to be set to `true`.

* `properties` - (Optional) A mapping of Key to Base64-Encoded Values which should be assigned to this Data Lake Gen2 File System. 

## Attributes Reference

The following attributes are exported in addition to the arguments listed above:

* `id` - The ID of the Data Lake Gen2 File System.

## Import

Data Lake Gen2 File System's can be imported using the `resource id`, e.g.

```shell
terraform import azurerm_storage_data_lake_gen2_filesystem.queue1 https://account1.dfs.core.windows.net/fileSystem1
```
