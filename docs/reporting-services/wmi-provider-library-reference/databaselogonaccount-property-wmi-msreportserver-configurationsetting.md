---
title: "DatabaseLogonAccount-Eigenschaft (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
apiname: 
  - "DatabaseLogonAccount"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "DatabaseLogonAccount-Eigenschaft"
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
caps.latest.revision: 24
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# DatabaseLogonAccount-Eigenschaft (WMI: MSReportServer_ConfigurationSetting)
  Gibt das Anmeldekonto an, mit dem der Berichtsserver eine Verbindung mit der Berichtsserver-Datenbank herstellt. Schreibgeschützt.  
  
## Syntax  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## Eigenschaftswerte  
 Ein **String** -Objekt, das den Namen des Anmeldekontos darstellt  
  
## Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Hinweise  
 Gültige Werte für diese Eigenschaft hängen vom Wert der [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md) -Eigenschaft ab.  
  
 Diese Eigenschaft wird ignoriert, wenn die [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md)-Eigenschaft auf **2 (Service)** festgelegt ist.  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  