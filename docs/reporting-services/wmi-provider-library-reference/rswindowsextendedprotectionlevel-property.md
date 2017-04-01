---
title: "RSWindowsExtendedProtectionLevel-Eigenschaft (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
caps.latest.revision: 6
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 6
---
# RSWindowsExtendedProtectionLevel-Eigenschaft (WMI MSReportServer_ConfigurationSetting)
  Gibt einen Zeichenfolgenwert zurück, der die Schutzebene angibt, für deren Unterstützung der Berichtsserver konfiguriert ist. Diese Eigenschaft ist schreibgeschützt.  
  
## Syntax  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## Hinweise  
 Gibt einen Zeichenfolgenwert zurück, der die Schutzebene angibt, für deren Unterstützung der Berichtsserver konfiguriert ist. Wenn der Berichtsserver, mit dem der WMI-Anbieter verbunden wird, keinen erweiterten Schutz unterstützt, wird “” (leere Zeichenfolge) zurückgegeben. In der folgenden Liste werden gültige Werte aufgeführt:  
  
 `“Off” | “Allow” | “Require”`  
  
## Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Siehe auch  
 [RSWindowsExtendedProtectionScenario-Eigenschaft &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario property.md)   
 [SetExtendedProtectionSettings-Methode &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setextendedprotectionsettings-method-wmi-msreportserver-configurationsetting.md)   
 [Erweiterter Schutz für die Authentifizierung mit Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  