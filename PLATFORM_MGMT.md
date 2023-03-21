# Platform Management

## Platform Management Scope

High level requirements on a DPU/IPU Adapter Card or device on motherboard,
subsequently referred to here as "device"

* Device Identification
  * Identify the device type & serial number
  * Use a standard protocol over the PCIe goldfingers or I2C (no add'l cabling)
* Device Power Snapshot
  * Read the total power consumption at last snapshot
  * Read the timestamp for when the power snapshot was taken 
  * Use a standard protocol over PCIe goldfiingers or I2C (no add'l cabling)
* Device Temperative Snapshot
  * Read the set of available temperature sensors on the card / device
  * Read the timestamp for when the temperature sensor snapshot was taken
  * Use a standard protocol over PCIe goldfingers or I2C (no add'l cabling)
* Device Alerts 
  * Read the most recent set of alerts, warnings or errors on the card
  * Alerts, warnings and errors must follow a standard and are not device
specific
  * Use a standard protocol over PCIe goldfingers or I2C (no add'l cabling)
* Device Throttle Signal
  * Capability to throttle and/or reset a device
  * Use a standard protocol over PCIe goldfingers or I2C (no add'l cabling) 

## Primary Use Cases

### Platform Power Optimization

Sustainability and power consumption reduction is often the #1 concern
of operators.  The BMC of the platform detects that a new device is
found on the platform, and can use a combination of device Identify, Power,
and Thermal information to dynamically adjust the platform fans or platform
components to manage and reduce power consumption as a whole.

### Platform Thermal Management

In certain usages and/or environments the airflow or cooling to the device
may be insufficient.  In this case the BMC of the
platform may decide to thottle this device, based on what is reported from
the device such as alerts or sensor values. 
This is to avoid damage to the platform and/or the device.

## Standards Based Approach

If devices satisfy these requirements then the 'loop logic' for a particular
device can be published (even open-sourced) by the device manufacturer, making
it simpler for the BMC to run the set of use cases above. This loop logic is a
set of rules based on reading the power, temperature and alerts for this
specific family of devices (a set of identifications & serial numbers). As a
result of detecting this type of device on a slot or I2C, the BMC
can pull down the rules for that device without having to code up special
handing logic. 
