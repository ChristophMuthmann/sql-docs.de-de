---
title: "ListReportServersInDatabase-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "ListReportServersInDatabase-Methode"
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ListReportServersInDatabase-Methode (WMI: MSReportServer_ConfigurationSetting)
  Gibt die Liste von Berichtsserverinstallationen zurück, die in der Berichtsserver-Datenbank vorhanden sind. Dies geschieht unabhängig davon, ob diese Installationen Zugriff auf sichere Informationen haben.  
  
## Syntax  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## Parameter  
 *MachineNames[]*  
 [out] Ein Array, das die Computernamen für die Berichtsserverinstallationen in der Datenbank enthält  
  
 *InstanceNames[]*  
 [aus] Ein Array mit den Instanznamen der einzelnen Berichtsserverinstallationen in der Datenbank.  
  
 *InstallationIDs[]*  
 [out] Ein Array, das die Installations-IDs für jede Berichtsserverinstallation in der Datenbank enthält  
  
 *IsInitialized[]*  
 [out] Ein Array, das den Initialisierungsstatus für jede Berichtsserverinstallation in der Datenbank enthält  
  
 *Länge*  
 [out] Die Länge der von der Methode zurückgegebenen Arrays Alle zurückgegebenen Arrays haben die gleiche Länge.  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
 *ExtendedErrors[]*  
 [out] Ein Zeichenfolgenarray, das zusätzliche Fehler enthält, die durch den Aufruf zurückgegeben werden  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## Hinweise  
 ListReportServersInDatabase listet die Berichtsserverinstallationen auf, die in der Berichtsserver-Datenbank vorhanden sind. Dies geschieht unabhängig davon, ob diese Installationen Zugriff auf sichere Informationen haben, und es wird ein übereinstimmender Satz von Arrays mit Informationen zu jeder Installation zurückgegeben.  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  