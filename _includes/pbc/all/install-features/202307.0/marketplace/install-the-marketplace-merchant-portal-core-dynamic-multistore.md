{% info_block warningBox %}

Dynamic Multistore is currently running under an *Early Access Release*. Early Access Releases are subject to specific legal terms, they are unsupported and do not provide production-ready SLAs. They can also be deprecated without a General Availability Release. Nevertheless, we welcome feedback from early adopters on these cutting-edge, exploratory features.

{% endinfo_block %}

This document describes how to integrate the Marketplace MerchantPortal Core + Dynamic Store feature into a Spryker project.

## Install feature core

Follow the steps below to install the Marketplace MerchantPortal Core + Dynamic Store feature core.

### Prerequisites

Install the required features:

| NAME | VERSION |
| -------------------- | ------- |
| Spryker Core | {{page.version}}  |
| Marketplace Merchant Portal Core | {{page.version}}  |  

### 1) Set up behavior

Enable the following behaviors by registering the plugins:

| PLUGIN | SPECIFICATION | PREREQUISITES | NAMESPACE |
| --- | --- | --- | --- |
| CountryStoreAclEntityConfigurationExpanderPlugin | Expands provided `AclEntityMetadataConfig` transfer object with country store composite data. | None | Spryker\Zed\Country\Communication\Plugin\AclMerchantPortal |
| CurrencyStoreAclEntityConfigurationExpanderPlugin | Expands provided `AclEntityMetadataConfig` transfer object with country store composite data. | None | Spryker\Zed\Country\Communication\Plugin\AclMerchantPortal |
| LocaleStoreAclEntityConfigurationExpanderPlugin |Expands provided `AclEntityMetadataConfig` transfer object with country store composite data. | None | Spryker\Zed\Country\Communication\Plugin\AclMerchantPortal |


**src/Pyz/Zed/AclMerchantPortal/AclMerchantPortalDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\AclMerchantPortal;

use Spryker\Zed\AclMerchantPortal\AclMerchantPortalDependencyProvider as SprykerAclMerchantPortalDependencyProvider;
use Spryker\Zed\Country\Communication\Plugin\AclMerchantPortal\CountryStoreAclEntityConfigurationExpanderPlugin;
use Spryker\Zed\Currency\Communication\Plugin\AclMerchantPortal\CurrencyStoreAclEntityConfigurationExpanderPlugin;
use Spryker\Zed\Locale\Communication\Plugin\AclMerchantPortal\LocaleStoreAclEntityConfigurationExpanderPlugin;

class AclMerchantPortalDependencyProvider extends SprykerAclMerchantPortalDependencyProvider
{
    /**
     * @return list<\Spryker\Zed\AclMerchantPortalExtension\Dependency\Plugin\AclEntityConfigurationExpanderPluginInterface>
     */
    protected function getAclEntityConfigurationExpanderPlugins(): array
    {
        return [
            new CountryStoreAclEntityConfigurationExpanderPlugin(),
            new CurrencyStoreAclEntityConfigurationExpanderPlugin(),
            new LocaleStoreAclEntityConfigurationExpanderPlugin(),
        ];
    }
}

```

{% info_block warningBox "Verification" %}

Make sure that access to tables `SpyCurrencyStore`, `SpyCountryStore`, `SpyLocaleStore` is allowed.

{% endinfo_block %}
