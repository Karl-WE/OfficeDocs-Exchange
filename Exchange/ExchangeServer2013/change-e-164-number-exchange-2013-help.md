---
title: 'Change an E.164 number: Exchange 2013 Help'
TOCTitle: Change an E.164 number
ms.author: serdars
author: msdmaguire
manager: serdars
ms.reviewer:
ms.assetid: 2a3da11b-bb9b-4d4d-9238-6a1a47ef63f2
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Change an E.164 number in Exchange Server

_**Applies to:** Exchange Server 2013, Exchange Server 2016_

When you enable a user for UM and link them to an E.164 dial plan, two EUM proxy addresses are created. One contains the user's extension number and the other contains the E.164 number for the user. The extension number is used when the user calls in to an Outlook Voice Access number.

You can change the primary E.164 number that was added when the user was enabled for UM or a secondary E.164 number that was added later, along with the EUM proxy addresses for the user. The primary E.164 number you added when the user was enabled for UM will be listed as the primary EUM proxy address. Any additional secondary E.164 numbers you added will be listed as secondary EUM proxy addresses. When E.164 numbers have been changed, callers can leave voice mail for the user at all the new E.164 numbers that have been set. All the voice messages will be delivered to the same user's mailbox.

You can use the EAC or the Shell to change the primary and secondary E.164 numbers for a user. You can use the **Email Address** page on the user's mailbox to change a primary or secondary E.164 number. However, you can't use the **UM Mailbox** page in the EAC to change a primary or secondary E.164 number.

You can view the primary and secondary E.164 numbers for a user by using the **Get-UMMailbox** cmdlet or the **Get-Mailbox** cmdlet in the Shell.

For additional management tasks related to users who are enabled for voice mail, see [Voice mail-enabled user procedures](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

- Estimated time to complete: 3 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailboxes" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

- Before you perform these procedures, confirm that an E.164 UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-um-dial-plan-exchange-2013-help.md).

- Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-um-mailbox-policy-exchange-2013-help.md).

- Before you perform these procedures, confirm that the user's mailbox has been enabled for UM and linked to an E.164 dial plan. For detailed steps, see [Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md).

- Before you perform these procedures, confirm that the E.164 number that will be assigned to the UM-enabled user is valid.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center in Exchange 2013](keyboard-shortcuts-in-the-exchange-admin-center-2013-help.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

## Use the EAC to change the primary or a secondary E.164 number

1. In the EAC, navigate to **Recipients** \> **Mailboxes**.

2. In the list view, select the mailbox for which you want to change an E.164 number, and then click **Edit** ![Edit icon.](images/ITPro_EAC_EditIcon.gif).

3. On the **User Mailbox** page, under **Email address**, select the E.164 number you want to change, and then click **Edit** ![Edit icon.](images/ITPro_EAC_EditIcon.gif). The primary E.164 number is listed in bold letters and numbers.

4. On the **Email address** page, in the **Address/Extension** box, enter the new E.164 number for the user, and then click **OK**. If you need to select a new UM dial plan, you can click **Browse**.

5. Click **Save**.

## Use the Shell to change the primary or a secondary E.164 number

This example changes an E.164 number for Tony Smith, a UM-enabled user.

> [!NOTE]
> Before you change an E.164 number using the Shell, you need to determine the position of the EUM proxy address that you want to change. To determine the position, use the **$mbx.EmailAddresses** command. The first EUM proxy address is the default (primary) E.164 number and it will be 0 in the list.

```powershell
$mbx=Get-Mailbox tony.smith
$mbx.EmailAddresses.Item(1)="eum:+14255550123;phone-context=MyE.164DialPlan.contoso.com"
Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses
```
