---
title: "RSWindowsExtendedProtectionScenario-Eigenschaft (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
caps.latest.revision: 6
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# RSWindowsExtendedProtectionScenario-Eigenschaft (WMI: MSReportServer_ConfigurationSetting)
  Gibt einen Zeichenfolgenwert zurück, der das erweiterte Schutzszenario angibt, für das der Berichtsserver konfiguriert ist.  
  
## Syntax  
  
```vb  
Public Dim RSWindowsExtendedProtectionScenario As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionScenario;  
```  
  
## Hinweise  
 Gibt einen Zeichenfolgenwert zurück, der das erweiterte Schutzszenario angibt, für das der Berichtsserver konfiguriert ist. Wenn der Berichtsserver, mit dem der WMI-Anbieter verbunden wird, keinen erweiterten Schutz unterstützt, wird “” (leere Zeichenfolge) zurückgegeben.  
  
 In der folgenden Liste werden gültige Werte aufgeführt:  
  
 `”Any | Proxy | Direct”`  
  
## Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Siehe auch  
 [RSWindowsExtendedProtectionLevel-Eigenschaft &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [SetExtendedProtectionSettings-Methode &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setextendedprotectionsettings-method-wmi-msreportserver-configurationsetting.md)   
 [Erweiterter Schutz für die Authentifizierung mit Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  