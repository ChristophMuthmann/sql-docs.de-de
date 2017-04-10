---
title: "DatabaseQueryTimeout-Eigenschaft (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "DatabaseQueryTimeout Property"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "DatabaseQueryTimeout-Eigenschaft"
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
caps.latest.revision: 35
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# DatabaseQueryTimeout-Eigenschaft (WMI: MSReportServer_ConfigurationSetting)
  Gibt die Anzahl von Sekunden an, die verstreichen müssen, ehe der Berichtsserver annimmt, dass der Befehl fehlgeschlagen ist oder die Ausführungszeit zu lang war. Der Berichtsserver nimmt die zeitliche Steuerung der Abfrage anhand des SQL-Katalogs und nicht anhand einer Datenquelle für den Bericht vor. Lese-/Schreibzugriff.  
  
## Syntax  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## Eigenschaftswerte  
 Ein 32-Bit-**Integer**-Objekt ohne Vorzeichen, das die Anzahl der Sekunden darstellt, die für die Ausführung der Abfrage erlaubt sind.  
  
## Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  