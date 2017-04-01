---
title: "SecureConnectionLevel-Eigenschaft (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "SecureConnectionLevel"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "SecureConnectionLevel-Eigenschaft"
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
caps.latest.revision: 19
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# SecureConnectionLevel-Eigenschaft (WMI: MSReportServer_ConfigurationSetting)
  Gibt die in der Datei RSReportServer.config angegebene sichere Verbindungsebene zurück. Schreibgeschützt.  
  
## Syntax  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## Eigenschaftswerte  
 Ein **Integer** -Wert, der die sichere Verbindungsebene darstellt. Die Rückgabewerte geben an, dass SSL entweder konfiguriert ist oder nicht. Ein Wert größer oder gleich 1 gibt an, dass SSL aktiviert ist. Der Wert 0 gibt an, dass SSL deaktiviert wird.  
  
## Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  