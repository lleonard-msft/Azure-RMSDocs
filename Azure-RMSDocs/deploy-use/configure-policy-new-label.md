---
# required metadata

title: New Azure Information Protection label
description: Although Azure Information Protection comes with default labels that you can customize, you can also create your own labels that users see on the Information Protection bar.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod:
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: eymanor
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# How to create a new label for Azure Information Protection

>*Applies to: Azure Information Protection*

Although Azure Information Protection comes with default labels that you can customize, you can also create your own labels that users see on the Information Protection bar.

You can add a new label, or add a new sub-label to an existing label when you need a further level of classification. For example, the last label in the [default policy](configure-policy-default.md), contains sub-labels.

Use the following instructions to add a new label to the Azure Information Protection policy.

1. If you haven't already done so, in a new browser window, sign in to the [Azure portal](https://portal.azure.com) as a security admin or global admin. Then navigate to the **Azure Information Protection** blade. 
    
    For example, on the hub menu, click **More services** and start typing **Information** in the Filter box. Select **Azure Information Protection**.

2. If the new label that you want to add is for all users, stay on the **Azure Information Protection - Global policy** blade.
    
    If the new label that you want to add is for selected users in a [scoped policy](configure-policy-scope.md), from the **POLICIES** menu selection, select **Scoped policies**. Then select your scoped policy from the **Azure Information Protection - Scoped polices** blade.

3. From the **Azure Information Protection - Global policy** blade, or the **Policy:\<name>** blade, do one of the following actions:
    
    - To create a new label: Click **Add a new label**.
    
    - To create a new sub-label: Right-click or select the context menu (**...**) for the label that you want to create a sub-label for, and then click **Add a sub-label**.

4. On the **Label** or **Sub-label** blade, select the options that you want for this new label, and then click **Save**.
    
    Note that new labels are automatically assigned the color black. Choose a distinguishing color from the list of colors, or enter a hex triplet code for the red, green, and blue (RGB) components of the color. For example, **#DAA520**. If you need a reference for these codes, [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85).aspx) from the MSDN documentation is a helpful starting point, and you'll find these codes in many picture editing programs such as Microsoft Paint, where you choose a custom color from a palette and it automatically displays the RGB values.

5. To make your changes available to users, on the initial **Azure Information Protection** blade, click **Publish**.

6. If you want this new label name and description to display in different languages for users, follow the procedures in [How to configure labels for different languages](configure-policy-languages.md). 

## Next steps

For more information about configuring your Azure Information Protection policy, use the links in the [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) section.  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

