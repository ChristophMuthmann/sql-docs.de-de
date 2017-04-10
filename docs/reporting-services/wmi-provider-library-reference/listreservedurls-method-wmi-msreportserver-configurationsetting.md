---
title: "ListReservedURLs-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "ListReservedURLs-Methode"
ms.assetid: 32335af1-5eae-4420-a0ef-b1e8a3267166
caps.latest.revision: 11
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ListReservedURLs-Methode (WMI: MSReportServer_ConfigurationSetting)
  Listet für alle Anwendungen auf dem Berichtsserver reservierte URLs auf  
  
## Syntax  
  
```vb  
Public Sub ListReservedUrls(ByRef Application() as String, ByRef UrlString() as String, _  
    ByRef Account() as String, ByRef AccountSID() as String, _  
    ByRef length() as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListReservedUrls(out string[] Application, out string[] UrlString,  
        out string[] Account, out string[] AccountSID,  
        out int[] Length, out int[] HRESULT);  
```  
  
## Parameter  
 *Application[]*  
 [out] Die Anwendungen, die URL-Reservierungen aufweisen  
  
 *UrlString[]*  
 [out] Die URLs, die reserviert sind  
  
 *Account[]*  
 [out] Die mit dem Konto für die URL-Reservierungen verknüpften Kontonamen  
  
 *AccountSID[]*  
 [out] Die mit dem Konto für die URL-Reservierungen verknüpften Konto-SIDs  
  
 *Länge*  
 [out] Die Länge der von der Methode zurückgegebenen Arrays  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## Hinweise  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  