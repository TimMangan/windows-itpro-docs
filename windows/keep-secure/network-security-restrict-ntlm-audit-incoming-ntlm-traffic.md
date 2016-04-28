---
title: Network security Restrict NTLM Audit incoming NTLM traffic (Windows 10)
description: Describes the best practices, location, values, management aspects, and security considerations for the Network Security Restrict NTLM Audit incoming NTLM traffic security policy setting.
ms.assetid: 37e380c2-22e1-44cd-9993-e12815b845cf
ms.prod: W10
ms.mktglfcycl: deploy
ms.sitesec: library
author: brianlic-msft
---

# Network security: Restrict NTLM: Audit incoming NTLM traffic


**Applies to**

-   Windows 10

Describes the best practices, location, values, management aspects, and security considerations for the **Network Security: Restrict NTLM: Audit incoming NTLM traffic** security policy setting.

## Reference


The **Network Security: Restrict NTLM: Audit incoming NTLM traffic** policy setting allows you to audit incoming NTLM traffic.

When this audit policy is enabled within Group Policy, it is enforced on any server where that Group Policy is distributed. The events will be recorded in the operational event log located in **Applications and Services Log\\Microsoft\\Windows\\NTLM**. Using an audit event collection system can help you collect the events for analysis more efficiently.

When you enable this policy on a server, only authentication traffic to that server will be logged.

When you enable this audit policy, it functions in the same way as the [Network Security: Restrict NTLM: Incoming NTLM traffic](network-security-restrict-ntlm-incoming-ntlm-traffic.md) policy, but it does not actually block any traffic. Therefore, you can use it effectively to understand the authentication traffic in your environment, and when you are ready to block that traffic, you can enable the Network Security: Restrict NTLM: Incoming NTLM traffic policy setting and select **Deny all accounts** or **Deny all domain accounts**.

### Possible values

-   Disable

    The server on which this policy is set will not log events for incoming NTLM traffic.

-   Enable auditing for domain accounts

    The server on which this policy is set will log events for NTLM pass-through authentication requests only for accounts in the domain that would be blocked when the [Network Security: Restrict NTLM: Incoming NTLM traffic](network-security-restrict-ntlm-incoming-ntlm-traffic.md) policy setting is set to **Deny all domain accounts**.

-   Enable auditing for all accounts

    The server on which this policy is set will log events for all NTLM authentication requests that would be blocked when the [Network Security: Restrict NTLM: Incoming NTLM traffic](network-security-restrict-ntlm-incoming-ntlm-traffic.md) policy setting is set to **Deny all accounts**.

-   Not defined

    This is the same as **Disable**, and it results in no auditing of NTLM traffic.

### Best practices

Depending on your environment and the duration of your testing, monitor the log size regularly.

### Location

Computer Configuration\\Windows Settings\\Security Settings\\Local Policies\\Security Options

### Default values

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Server type or GPO</th>
<th align="left">Default value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Default domain policy</p></td>
<td align="left"><p>Not defined</p></td>
</tr>
<tr class="even">
<td align="left"><p>Default domain controller policy</p></td>
<td align="left"><p>Not defined</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Stand-alone server default settings</p></td>
<td align="left"><p>Not defined</p></td>
</tr>
<tr class="even">
<td align="left"><p>Domain controller effective default settings</p></td>
<td align="left"><p>Not defined</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Member server effective default settings</p></td>
<td align="left"><p>Not defined</p></td>
</tr>
<tr class="even">
<td align="left"><p>Client computer effective default settings</p></td>
<td align="left"><p>Not defined</p></td>
</tr>
</tbody>
</table>

 

## Policy management


This section describes different features and tools available to help you manage this policy.

### Restart requirement

None. Changes to this policy become effective without a restart when saved locally or distributed through Group Policy.

### Group Policy

Setting and deploying this policy using Group Policy takes precedence over the setting on the local device. If the Group Policy is set to **Not Configured**, local settings will apply.

### Auditing

View the operational event log to see if this policy is functioning as intended. Audit and block events are recorded on this computer in the operational event log located in **Applications and Services Log\\Microsoft\\Windows\\NTLM**. Using an audit event collection system can help you collect the events for analysis more efficiently.

There are no security audit event policies that can be configured to view output from this policy.

## Security considerations


This section describes how an attacker might exploit a feature or its configuration, how to implement the countermeasure, and the possible negative consequences of countermeasure implementation.

NTLM and NTLMv2 authentication is vulnerable to a variety of malicious attacks, including SMB relay, man-in-the-middle attacks, and brute force attacks. Reducing and eliminating NTLM authentication from your environment forces the Windows operating system to use more secure protocols, such as the Kerberos version 5 protocol, or different authentication mechanisms, such as smart cards.

### Vulnerability

Enabling this policy setting will reveal through logging which servers and client computers within your network or domain handle NTLM traffic. The identity of these devices can be used in malicious ways if NTLM authentication traffic is compromised. The policy setting does not prevent or mitigate any vulnerability because it is for audit purposes only.

### Countermeasure

Restrict access to the log files when this policy setting is enabled in your production environment.

### Potential impact

If you do not enable or configure this policy setting, no NTLM authentication traffic information will be logged. If you do enable this policy setting, only auditing functions will occur; no security enhancements will be implemented.

## Related topics


[Security Options](security-options.md)

 

 




