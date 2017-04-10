---
title: "ConnectionPoolSize-Eigenschaft (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "ConnectionPoolSize"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "ConnectionPoolSize-Eigenschaft"
ms.assetid: b80c8e5d-b725-4fe4-aec6-02fb18ec4434
caps.latest.revision: 17
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ConnectionPoolSize-Eigenschaft (WMI: MSReportServer_ConfigurationSetting)
  Die Größe des Verbindungspools, über den der Berichtsserver mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz kommuniziert, die die Berichtsserver-Datenbank hostet. Schreibgeschützt.  
  
## Syntax  
  
```vb  
Public Dim ConnectionPoolSize As UInt32  
```  
  
```csharp  
public UInt32 ConnectionPoolSize;  
```  
  
## Eigenschaftswerte  
 Ein schreibgeschütztes **integer**-Objekt, das den Wert **768** zurückgibt.  
  
## Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  