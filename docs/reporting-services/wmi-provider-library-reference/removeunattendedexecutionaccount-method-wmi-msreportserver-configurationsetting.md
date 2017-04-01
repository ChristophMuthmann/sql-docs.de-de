---
title: "RemoveUnattendedExecutionAccount-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "RemoveUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "RemoveUnattendedExecutionAccount-Methode"
ms.assetid: 77e371c1-7c26-44f9-9119-7c8dc838db32
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# RemoveUnattendedExecutionAccount-Methode (WMI: MSReportServer_ConfigurationSetting)
  Löscht den Eintrag für das Konto für die unbeaufsichtigte Ausführung aus der Berichtsserver-Konfigurationsdatei  
  
## Syntax  
  
```vb  
Public Sub RemoveUnattendedExecutionAccount(ByRef HRESULT as Int32)  
```  
  
```csharp  
public void RemoveUnattendedExecutionAccount (out Int32 HRESULT);  
```  
  
## Parameter  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  