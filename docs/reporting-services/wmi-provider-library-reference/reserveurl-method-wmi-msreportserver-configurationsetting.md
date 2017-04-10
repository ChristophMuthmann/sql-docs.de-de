---
title: "ReserveURL-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "ReservedURL-Methode"
ms.assetid: b9008a62-3edd-4f8a-99f2-7598c2133899
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ReserveURL-Methode (WMI: MSReportServer_ConfigurationSetting)
  Fügt eine URL-Reservierung für eine gegebene Anwendung hinzu  
  
## Syntax  
  
```vb  
Public Sub ReserveURL(Application as String, _  
    UrlString as String, Lcid as Int32, _   
    ByRef [Error] as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ReserveURL(string Application, string UrlString, int Lcid,   
    out string error, out int HRESULT);  
```  
  
## Parameter  
 *Application*  
 Der Name der Anwendung, für die die URL reserviert werden soll  
  
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
 *UrlString* beinhaltet nicht den Namen des virtuellen Verzeichnisses. Dazu wird die [SetVirtualDirectory](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md) -Methode bereitgestellt.  
  
 URL-Reservierungen werden für das aktuelle Windows-Dienstkonto erstellt. Eine Änderung des Windows-Dienstkontos erfordert das manuelle Aktualisieren der URL-Reservierungen.  
  
 Diese Methode verursacht einen "harten" Wiederverwendungsvorgang. Anwendungsdomänen werden neu gestartet, nachdem dieser Vorgang abgeschlossen wurde.  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  