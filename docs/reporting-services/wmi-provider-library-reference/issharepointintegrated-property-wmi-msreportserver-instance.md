---
title: "IsSharePointIntegrated-Eigenschaft (WMI: MSReportServer_Instance) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "IsSharePointIntegrated-Eigenschaft"
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# IsSharePointIntegrated-Eigenschaft (WMI: MSReportServer_Instance)
  Gibt an, ob sich der Berichtsserver im integrierten SharePoint-Modus befindet Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] gibt diese Eigenschaft immer **FALSE** zurück, da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Instanzen im SharePoint-Modus freigegebene SharePoint-Dienste darstellen und nicht von WMI-Anbietern kontrolliert werden.  
  
## Syntax  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## Eigenschaftswerte  
 Ein **Boolean** -Wert, der angibt, ob sich der Berichtsserver im integrierten SharePoint-Modus befindet  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## Siehe auch  
 [MSReportServer_Instance-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)   
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  