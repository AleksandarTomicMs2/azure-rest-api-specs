## AZ

These settings apply only when `--az` is specified on the command line.

``` yaml $(az) && $(target-mode) == 'core'
az:
  extensions: databoxedge
  package-name: azure-mgmt-databoxedge
  namespace: azure.mgmt.databoxedge
az-output-folder: $(azure-cli-folder)/src/azure-cli/azure/cli/command_modules/databoxedge
python-sdk-output-folder: "$(az-output-folder)/vendored_sdks/databoxedge"
extension-mode: preview

directive:
    - where:
        group: databoxedge job
      set:
        group: databoxedge

    - where:
        group: databoxedge node
      set:
        group: databoxedge

    - where:
        group: databoxedge sku
      set:
        group: databoxedge

cli:
    cli-directive:
# -------- DO NOT generate and DO generate --------
        - where:
            group: "*"
            op: "*"
          hidden: true

        - where:
            group: Alerts|BandwidthSchedules|Devices|Jobs|Nodes|Orders|Skus
            op: "*"
          hidden: false

        - where:
            group: Devices
            op: GetExtendedInformation|GetNetworkSettings|CreateOrUpdateSecuritySettings|UploadCertificate
          hidden: true

# -------- rename single command within a group --------
        - where:
            group: Jobs
            op: Get
          name: show_job

        - where:
            group: Nodes
            op: ListByDataBoxEdgeDevice
          name: list_node

        - where:
            group: Skus
            op: List
          name: list_sku

# -------- Devices --------
        - where:
            group: Devices
            param: dataBoxEdgeDeviceStatus
          alias:
            - status

# -------- Alerts --------
        - where:
            group: Alerts
            param: deviceName
          alias:
            - device_name
            - d

        - where:
            group: Alerts
            param: name
          alias:
            - name
            - n

# -------- BandwidthSchedules --------
        - where:
            group: BandwidthSchedules
            param: deviceName
          alias:
            - device_name
            - d

        - where:
            group: BandwidthSchedules
            param: name
          alias:
            - name
            - n

# -------- Jobs --------
        - where:
            group: Jobs
            param: deviceName
          alias:
            - device_name
            - d

        - where:
            group: Jobs
            param: name
          alias:
            - name
            - n

# -------- Nodes --------
        - where:
            group: Nodes
            param: deviceName
          alias:
            - device_name
            - d

# -------- Orders --------
        - where:
            group: Orders
            param: deviceName
          alias:
            - device_name
            - d

        - where:
            type: Order
            prop: contactInformation|shippingAddress
          cli-flatten: true

        - where:
            group: Orders
            op: CreateOrUpdate#Create
            param: addressLine1|postalCode|city|state|country|contactPerson|companyName|phone|emailList
          required: true

        - where:
            param: addressLine1
          alias: address_line1

        - where:
            param: addressLine2
          alias: address_line2

        - where:
            param: addressLine3
          alias: address_line3

        - where:
            param: postalCode
          alias: postal_code

        - where:
            param: city
          alias: city

        - where:
            param: state
          alias: state

        - where:
            param: country
          alias: country

        - where:
            param: contactPerson
          alias: contact_person

        - where:
            param: companyName
          alias: company_name

        - where:
            param: phone
          alias: phone

        - where:
            param: emailList
          alias: email_list

        - where:
            group: Orders
            op: CreateOrUpdate#Create|CreateOrUpdate#Update
            param: status
          alias: status

        - where:
            group: Orders
            op: CreateOrUpdate#Create|CreateOrUpdate#Update
            param: comments
          alias: comments
```