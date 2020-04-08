## Ruby

These settings apply only when `--ruby` is specified on the command line.

```yaml
package-name: azure_mgmt_newservice
package-version: 2020-03-31
azure-arm: true
```

### Tag: package-2020-03-31 and ruby

These settings apply only when `--tag=package-2020-03-31 --ruby` is specified on the command line.
Please also specify `--ruby-sdks-folder=<path to the root directory of your azure-sdk-for-ruby clone>`.

```yaml $(tag) == 'package-2020-03-31' && $(ruby)
namespace: Microsoft.NewResourceProvider
output-folder: $(ruby-sdks-folder)/newservice
```