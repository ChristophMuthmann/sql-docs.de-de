---
title: "GetAdminSiteUrl-Methode (WMI) | Microsoft Docs"
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
  - "GetAdminSiteUrl-Methode"
ms.assetid: fbc5bf3c-120c-4aec-a4f2-f5391bd415f6
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# GetAdminSiteUrl-Methode (WMI)
  Ruft die absolute URL für die Zentraladministrationswebsite für die Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]-, [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]-, [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]- oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Farm ab, in die der Berichtsserver integriert ist  
  
## Syntax  
  
```vb  
Public Sub GetAdminSiteUrl(ByRef AdminSiteUrl as String, _  
ByRef HRESULT as Int32)  
```  
  
```csharp  
public void GetAdminSiteUrl(out string AdminSiteUrl, out Int32 HRESULT);  
```  
  
## Parameter  
 *AdminSiteUrl*  
 [out] Eine Zeichenfolge, die die absolute URL für die Zentraladministrationswebsite für die SharePoint-Farm enthält, in die der Berichtsserver integriert ist.  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Methoden](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-methods.md)  
  
  