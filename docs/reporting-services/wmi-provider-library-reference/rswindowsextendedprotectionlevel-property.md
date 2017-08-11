---
title: RSWindowsExtendedProtectionLevel-Eigenschaft | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9249b6abefe1a36e9b7cdb7aff1213b833113812
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="rswindowsextendedprotectionlevel-property"></a>RSWindowsExtendedProtectionLevel-Eigenschaft
  Gibt einen Zeichenfolgenwert zurück, der die Schutzebene angibt, für deren Unterstützung der Berichtsserver konfiguriert ist. Diese Eigenschaft ist schreibgeschützt.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>Hinweise  
 Gibt einen Zeichenfolgenwert zurück, der die Schutzebene angibt, für deren Unterstützung der Berichtsserver konfiguriert ist. Wenn der Berichtsserver, mit dem der WMI-Anbieter verbunden wird, keinen erweiterten Schutz unterstützt, wird “” (leere Zeichenfolge) zurückgegeben. In der folgenden Liste werden gültige Werte aufgeführt:  
  
 `“Off” | “Allow” | “Require”`  
  
## <a name="example-code"></a>Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Siehe auch  
 [RSWindowsExtendedProtectionScenario-Eigenschaft &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [SetExtendedProtectionSettings-Methode &#40; WMI MSReportServer_ConfigurationSetting &#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Erweiterter Schutz für die Authentifizierung mit Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config Configuration File (RSReportServer.config-Konfigurationsdatei)](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
