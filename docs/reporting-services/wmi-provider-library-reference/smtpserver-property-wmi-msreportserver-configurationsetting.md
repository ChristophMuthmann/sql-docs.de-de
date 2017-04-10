---
title: "SMTPServer-Eigenschaft (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "SMTPServer"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "SMTPServer-Eigenschaft"
ms.assetid: 8bcceeba-e1a0-44ef-bda1-600c6925e1db
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# SMTPServer-Eigenschaft (WMI: MSReportServer_ConfigurationSetting)
  Ruft die SMTP-Server-Eigenschaft aus der Berichtsserver-Konfigurationsdatei ab. Schreibgeschützt.  
  
## Syntax  
  
```vb  
Public Dim SMTPServer As String  
```  
  
```csharp  
public string SMTPServer;  
```  
  
## Eigenschaftswerte  
 Ein schreibgeschütztes **String**-Objekt, das den Wert der **SMTPServer**-Eigenschaft aus der Datei RSReportServer.config enthält.  
  
## Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  