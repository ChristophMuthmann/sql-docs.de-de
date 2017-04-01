---
title: "SetVirtualDirectory-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "SetVirtualDirectory-Methode"
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
caps.latest.revision: 11
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# SetVirtualDirectory-Methode (WMI: MSReportServer_ConfigurationSetting)
  Legt den Namen des virtuellen Verzeichnisses für eine angegebene Anwendung fest.  
  
## Syntax  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## Parameter  
 *Application*  
 Der für das virtuelle Verzeichnis festzulegende Name der Anwendung.  
  
 *VirtualDirectory*  
 Der Name des virtuellen Verzeichnisses  
  
 *lcid*  
 Die Gebietsschema-ID für das virtuelle Verzeichnis  
  
 *Fehler*  
 [out] Die Beschreibung des Fehlers, der aufgetreten ist  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## Hinweise  
 Eine Anwendung kann nur einen Namen für ein virtuelles Verzeichnis für alle URL-Reservierungen verwenden.  
  
 VirtualDirectory muss den Namenskonventionen für virtuelle Verzeichnisse entsprechen. VirtualDirectory darf keine leere Zeichenfolge sein.  
  
 Aktualisiert den Wert des \Configuration\URLReservations\Application\VirtualDirectory-Elements. Ist erfolgreich, auch wenn noch keine URL-Reservierungen erstellt wurden.  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  