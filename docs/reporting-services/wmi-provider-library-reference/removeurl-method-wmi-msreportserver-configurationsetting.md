---
title: "RemoveURL-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "RemoveURL-Methode"
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# RemoveURL-Methode (WMI: MSReportServer_ConfigurationSetting)
  Entfernt eine für den Berichtsserver reservierte URL Wenn mehrere URLs entfernt werden müssen, muss dies einzeln durch mehrfache Aufrufe dieser API erfolgen.  
  
## Syntax  
  
```vb  
Public Sub RemoveURL(ByVal Application As String, _  
    ByVal UrlString As String, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveURL(string Application, string UrlString, int Lcid,   
    out string Error, out int HRESULT);  
```  
  
## Parameter  
 *Application*  
 Der Name der Anwendung, für die die Reservierung entfernt werden soll  
  
 *URLString*  
 Die URL für die Reservierung  
  
 *lcid*  
 Das Gebietsschema, das für die zurückgegebenen Fehlermeldungen verwendet werden soll  
  
 *Fehler*  
 [out] Die Beschreibung des Fehlers, der aufgetreten ist  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## Hinweise  
 *UrlString* beinhaltet nicht den Namen des virtuellen Verzeichnisses – die Methode [SetVirtualDirectory-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md) ist für diesen Zweck vorgesehen.  
  
 Vor einem Aufruf der [ReserveURL](../../reporting-services/wmi-provider-library-reference/reserveurl-method-wmi-msreportserver-configurationsetting.md)-Methode müssen Sie einen Wert für die VirtualDirectory-Konfigurationseigenschaft des *Anwendungsparameters* angeben. Verwenden Sie die Methode [SetVirtualDirectory-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md), um die VirtualDirectory-Eigenschaft festzulegen.  
  
 Wenn durch [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ein SSL-Zertifikat bereitgestellt wurde und keine anderen URLs dieses benötigen, wird es entfernt.  
  
 Diese Methode verursacht einen "harten" Wiederverwendungsvorgang und ein Beenden aller Nichtkonfigurationsdomänen für Anwendungen. Die Anwendungsdomänen werden nach dem Abschluss des Vorgangs neu gestartet.  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  