---
title: Forward alert information
description: You can send alert information to partner systems by working with forwarding rules.
ms.date: 08/29/2021
ms.topic: how-to
---

# Forward alert information

You can send alert information to partners who are integrating with Azure Defender for IoT, to syslog servers, to email addresses, and more. Working with forwarding rules lets you quickly deliver alert information to security stakeholders.

Define criteria by which to trigger a forwarding rule. Working with forwarding rule criteria helps pinpoint and manage the volume of information sent from the sensor to external systems.

Syslog and other default forwarding actions are delivered with your system. More forwarding actions might become available when you integrate with partner vendors, such as Microsoft Azure Sentinel, ServiceNow, or Splunk.

:::image type="content" source="media/how-to-work-with-alerts-sensor/alert-information-screen.png" alt-text="Alert information.":::

Defender for IoT administrators has permission to use forwarding rules.

## About forwarded alert information

Alerts provide information about an extensive range of security and operational events. For example:

- Date and time of the alert

- Engine that detected the event

- Alert title and descriptive message

- Alert severity

- Source and destination name and IP address

- Suspicious traffic detected

:::image type="content" source="media/how-to-work-with-alerts-sensor/address-scan-detected-screen.png" alt-text="Address scan detected.":::

Relevant information is sent to partner systems when forwarding rules are created.

## About Forwarding rules and certificates

Certain Forwarding rules allow encryption and certificate validation between the sensor or on-premises management console, and the server of the integrated vendor.

In these cases, the sensor or on-premises management console is the client and initiator of the session.  The certificates are typically received from the server, or use asymmetric encryption where a specific certificate will be provided to set up the integration.

Your Defender for IoT system was set up to either validate certificates or ignore certificate validation.  See [About certificate validation](how-to-deploy-certificates.md#about-certificate-validation) for information about enabling and disabling validation.

If validation is enabled and the certificate can not be verified, communication between Defender for IoT and the server will be halted.  The sensor will display an error message indicating the validation failure.  If the validation is disabled and the certificate is not valid, communication will still be carried out.

The following Forwarding rules allow encryption and certificate validation:
- Syslog CEF
- Azure Sentinel
- QRadar

## Create forwarding rules

**To create a new forwarding rule on a sensor**:

1. Sign in to the sensor.

1. Select **Forwarding** on the side menu.

1. Select **Create Forwarding Rule**.

   :::image type="content" source="media/how-to-work-with-alerts-sensor/create-forwarding-rule-screen.png" alt-text="Create a Forwarding Rule icon.":::

1. Enter a name for the forwarding rule.

1. Select the severity level.

   This is the minimum incident to forward, in terms of severity level. For example, if you select **Minor**, minor alerts and any alert above this severity level will be forwarded. Levels are predefined.

1. Select any protocols to apply.

   Only trigger the forwarding rule if the traffic detected was running over specific protocols. Select the required protocols from the drop-down list or choose them all.

1. Select which engines the rule should apply to.

   Select the required engines, or choose them all. Alerts from selected engines will be sent. 

1. Select an action to apply, and fill in any parameters needed for the selected action.

   Forwarding rule actions instruct the sensor to forward alert information to partner vendors or servers. You can create multiple actions for each forwarding rule.

1. Add another action if desired.

1. Select **Submit**.

### Email address action

Send mail that includes the alert information. You can enter one email address per rule.

To define email for the forwarding rule:

1. Enter a single email address. If you need to add more than one email, you will need to create another action for each email address.

    :::image type="content" source="media/how-to-forward-alert-information-to-partners/forward-email.png" alt-text="Scrrenshot of the forwarding alert screen to forward the alerts to an email address.":::

1. Enter the time zone for the time stamp for the alert detection at the SIEM.

1. Select **Submit**.

### Syslog server actions

The following formats are supported:

- Text messages

- CEF messages

- LEEF messages

- Object messages

:::image type="content" source="media/how-to-work-with-alerts-sensor/create-actions-rule.png" alt-text="Create forwarding rule actions.":::

Enter the following parameters:

- Syslog host name and port.

- Protocol TCP and UDP.

- Time zone for the time stamp for the alert detection at the SIEM.

- TLS encryption certificate file and key file for CEF servers (optional).

:::image type="content" source="media/how-to-work-with-alerts-sensor/configure-encryption.png" alt-text="Configure your encryption for your forwarding rule.":::

| Syslog text message output fields | Description |
|--|--|
| Date and time | Date and time that the syslog server machine received the information. |
| Priority | User.Alert |
| Hostname | Sensor IP address |
| Protocol | TCP or UDP |
| Message | Sensor: The sensor name.<br /> Alert: The title of the alert.<br /> Type: The type of the alert. Can be **Protocol Violation**, **Policy Violation**, **Malware**, **Anomaly**, or **Operational**.<br /> Severity: The severity of the alert. Can be **Warning**, **Minor**, **Major**, or **Critical**.<br /> Source: The source device name.<br /> Source IP: The source device IP address.<br /> Destination: The destination device name.<br /> Destination IP: The IP address of the destination device.<br /> Message: The message of the alert.<br /> Alert group: The alert group associated with the alert. |

| Syslog object output | Description |
|--|--|
| Date and Time | Date and time that the syslog server machine received the information. |  
| Priority | User.Alert |
| Hostname | Sensor IP |
| Message | Sensor name: The name of the appliance. <br /> Alert time: The time that the alert was detected: Can vary from the time of the syslog server machine, and depends on the time-zone configuration of the forwarding rule. <br /> Alert title: The title of the alert. <br /> Alert message: The message of the alert. <br /> Alert severity: The severity of the alert: **Warning**, **Minor**, **Major**, or **Critical**. <br /> Alert type: **Protocol Violation**, **Policy Violation**, **Malware**, **Anomaly**, or **Operational**. <br /> Protocol: The protocol of the alert.  <br /> **Source_MAC**: IP address, name, vendor, or OS of the source device. <br /> Destination_MAC: IP address, name, vendor, or OS of the destination. If data is missing, the value will be **N/A**. <br /> alert_group: The alert group associated with the alert. |

| Syslog CEF output format | Description |
|--|--|
| Date and time | Date and time that the syslog server machine received the information. |
| Priority | User.Alert |
| Hostname | Sensor IP address |
| Message | CEF:0 <br />Azure Defender for IoT <br />Sensor name: The name of the sensor appliance. <br />Sensor version <br />Alert title: The title of the alert. <br />msg: The message of the alert. <br />protocol: The protocol of the alert. <br />severity: **Warning**, **Minor**, **Major**, or **Critical**. <br />type: **Protocol Violation**, **Policy Violation**, **Malware**, **Anomaly**, or **Operational**. <br /> start: The time that the alert was detected. <br />Might vary from the time of the syslog server machine, and depends on the time-zone configuration of the forwarding rule. <br />src_ip: IP address of the source device.  <br />dst_ip: IP address of the destination device.<br />cat: The alert group associated with the alert.  |

| Syslog LEEF output format | Description |
|--|--|
| Date and time | Date and time that the syslog server machine received the information. |  
| Priority | User.Alert |
| Hostname | Sensor IP |
| Message | Sensor name: The name of the Azure Defender for IoT appliance. <br />LEEF:1.0 <br />Azure Defender for IoT <br />Sensor  <br />Sensor version <br />Azure Defender for IoT Alert <br />title: The title of the alert. <br />msg: The message of the alert. <br />protocol: The protocol of the alert.<br />severity: **Warning**, **Minor**, **Major**, or **Critical**. <br />type: The type of the alert: **Protocol Violation**, **Policy Violation**, **Malware**, **Anomaly**, or **Operational**. <br />start: The time of the alert. It may be different from the time of the syslog server machine. (This depends on the time-zone configuration.) <br />src_ip: IP address of the source device.<br />dst_ip: IP address of the destination device. <br />cat: The alert group associated with the alert. |

After you enter all the information, select **Submit**.

### Webhook server action

Send alert information to a webhook server. Working with webhook servers lets you set up integrations that subscribe to alert events with Defender for IoT. When an alert event is triggered, the management console sends an HTTP POST payload to the webhook's configured URL. Webhooks can be used to update an external SIEM system, SOAR systems, Incident management systems, etc.

**To define to a webhook action:**

1. Select the Webhook action.

   :::image type="content" source="media/how-to-work-with-alerts-sensor/webhook.png" alt-text="Define a webhook forwarding rule.":::

1. Enter the server address in the **URL** field.

1. In the **Key** and **Value fields**, customize the HTTP header with a key and value definition. Keys can only contain letters, numbers, dashes, and underscores. Values can only contain one leading and/or one trailing space.

1. Select **Save**.

### Webhook extended

Webhook extended can be used to send extra data to the endpoint. The extended feature includes all of the information in the Webhook alert, and adds the following information to the report:

- sensorID
- sensorName
- zoneID
- zoneName
- siteID
- siteName
- sourceDeviceAddress
- destinationDeviceAddress
- remediationSteps
- handled
- additionalInformation

**To define a webhook extended action**:

1. In the management console, select **Forwarding** from the left-hand pane.

1. Add a forwarding rule by selecting the :::image type="icon" source="media/how-to-forward-alert-information-to-partners/add-icon.png" border="false"::: button.

1. Add a meaningful name for the forwarding alert.

1. Select a severity level.

1. Select **Add**.

1. In the Select Type drop down window, select **Webhook Extended**.

   :::image type="content" source="media/how-to-forward-alert-information-to-partners/webhook-extended.png" alt-text="Select the webhook extended option from the select type drop down options menu.":::

1. Add the endpoint data URL in the URL field.

1. (Optional) Customize the HTTP header with a key and value definition. Add extra headers by selecting the :::image type="icon" source="media/how-to-forward-alert-information-to-partners/add-header.png" border="false"::: button.

1. Select **Save**.

Once the Webhook Extended forwarding rule has been configured, you can test the alert from the Forwarding screen on the management console.

**To test the Webhook Extended forwarding rule**:

1. In the management console, select **Forwarding** from the left-hand pane.

1. Select the **run** button to test your alert.

    :::image type="content" source="media/how-to-forward-alert-information-to-partners/run-button.png" alt-text="Select the run button to test your forwarding rule.":::

You will know the forwarding rule is working if you see the Success notification appear.

:::image type="content" source="media/how-to-forward-alert-information-to-partners/success.png" alt-text="The alert has worked correctly if the success notification appears.":::

### NetWitness action

Send alert information to a NetWitness server.

To define NetWitness forwarding parameters:

1. Enter NetWitness **Hostname** and **Port** information.

1. Enter the time zone for the time stamp for the alert detection at the SIEM.

   :::image type="content" source="media/how-to-work-with-alerts-sensor/add-timezone.png" alt-text="Add a time zone to your forwarding rule.":::

1. Select **Submit**.

### Integrated vendor actions

You might have integrated your system with a security, device management, or other industry vendor. These integrations let you:

  - Send alert information.

  - Send device inventory information.

  - Communicate with vendor-side firewalls.

Integrations help bridge previously siloed security solutions, enhance device visibility, and accelerate system-wide response to more rapidly mitigate risks.

Use the actions section to enter the credentials and other information required to communicate with integrated vendors.

For details about setting up forwarding rules for the integrations, refer to the relevant partner integration articles.

## Test forwarding rules

Test the connection between the sensor and the partner server that's defined in your forwarding rules:

1. Select the rule from the **Forwarding rule** dialog box.

1. Select the **More** box.

1. Select **Send Test Message**.

1. Go to your partner system to verify that the information sent by the sensor was received.

## Edit and delete forwarding rules 

**To edit a forwarding rule**:

- On the **Forwarding Rule** screen, select **Edit** under the **More** drop-down menu. Make the desired changes and select **Submit**.

**To remove a forwarding rule**:

- On the **Forwarding Rule** screen, select **Remove** under the **More** drop-down menu. In the **Warning** dialog box, select **OK**.

## Forwarding rules and alert exclusion rules

The administrator might have defined alert exclusion rules. These rules help administrators achieve more granular control over alert triggering by instructing the sensor to ignore alert events based on various parameters. These parameters might include device addresses, alert names, or specific sensors.

This means that the forwarding rules you define might be ignored based on exclusion rules that your administrator has created. Exclusion rules are defined in the on-premises management console.

## See also

[Accelerate alert workflows](how-to-accelerate-alert-incident-response.md)
