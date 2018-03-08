---
title: 'SetExtendedProtectionSettings-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
caps.latest.revision: "7"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f2c5e606cc11ad8e7026dd0d7bebe1d9395d6d2f
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---setextendedprotectionsettings"></a>ConfigurationSetting-Methode: SetExtendedProtectionSettings
  Die SetExtendedProtectionSettings-Methode wird verwendet, um die RSWindowsExtendedProtectionLevel- und RSWindowsExtendedProtectionScenario-Eigenschaft in der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationsdatei "RSReportServer.config" festzulegen.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub SetExtendedProtectionSettings( _  
        ByVal ExtendedProtectionLevel As String, _  
        ByVal ExtendedProtectionScenario As String, _  
        ByRef Warnings() As String, _  
        ByRef Length As Int32, _  
        ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetExtendedProtectionSettings(  
            string ExtendedProtectionLevel,  
            string ExtendedProtectionScenario,  
            out string[] Warnings,  
            out Int32 Length,  
            out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *ExtendedProtectionLevel*  
 Legt "RSWindowsExtendedProtectionLevel" in der Datei "RSRreportserver.config" fest. Beim erforderlichen Wert wird die Groß-/Kleinschreibung nicht beachtet.  
  
 In der folgenden Liste werden gültige Werte aufgeführt:  
  
 `”Off | Allow | Require”`  
  
 *ExtendedProtectionScenario*  
 Legt "RSWindowsExtendedProtectionScenario" in der Datei "RSReportserver.config" fest. Beim erforderlichen Wert wird die Groß-/Kleinschreibung nicht beachtet.  
  
 In der folgenden Liste werden gültige Werte aufgeführt:  
  
 `”Any” | “Proxy” | “Direct”`  
  
## <a name="remarks"></a>Remarks  
 Die RSWindowsExtendedProtectionLevel-Eigenschaft und die RSWindowsExtendedProtectionScenario-Eigenschaft sind gültig, wenn AuthenticationTypes in der Datei RSReportServer.config RSWindowNTLM, RSWindowsNegotiate oder RSWindowsKerberos einschließt. Das Festlegen dieser Eigenschaften wirkt sich darauf aus, wie sich Benutzer und Clientsoftware an einem Berichtsserver authentifizieren. Es wird empfohlen, dass Sie die Dokumentation für erweiterten Schutz vor dem Festlegen von ExtendedProtectionLevel auf **Allow** oder **Require**lesen.  
  
 Zum Festlegen von ExtendedProtectionLevel muss der Benutzer Mitglied der Gruppe "BUILTIN\Administrators" auf dem Berichtsserver sein.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RSWindowsExtendedProtectionScenario-Eigenschaft &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [RSWindowsExtendedProtectionLevel-Eigenschaft &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [Erweiterter Schutz für die Authentifizierung mit Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config Configuration File (RSReportServer.config-Konfigurationsdatei)](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
