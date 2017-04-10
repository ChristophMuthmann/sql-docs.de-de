---
title: "ListInstalledSharePointVersions-Methode (WMI) | Microsoft Docs"
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
  - "ListInstalledSharePointVersions-Methode"
ms.assetid: 8f0a5e9f-23f1-41e5-9a90-dfec19ef1df7
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ListInstalledSharePointVersions-Methode (WMI)
  Gibt einen Satz von Token zurück, die die Versionen von Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] darstellen, die auf dem gleichen Computer wie der Berichtsserver installiert sind.  
  
## Syntax  
  
```vb  
Public Sub ListInstalledSharePointVersions(ByRef VersionTokens() _  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] VersionTokens,   
    out Int32 Length, out Int32 HRESULT);  
```  
  
## Parameter  
 *VersionTokens[]*  
 [out] Ein Array, das die Token enthält, welche die Version eines SharePoint-Produkts oder der SharePoint-Technologie darstellen, die mit dem installierten Berichtsserver kompatibel ist  
  
 *Länge*  
 [out] Die Länge des Arrays von Versionstoken  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## Hinweise  
 Jedes Token, das zurückgegeben wird, stellt eine Version von [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] oder [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] dar, die mit dem derzeit installierten Berichtsserver kompatibel ist. Wenn eine bestimmte Version von SharePoint kompatibel mit früheren Versionen von SharePoint ist, werden Token für jede kompatible Version von SharePoint zurückgegeben.  
  
 Die folgende Tabelle enthält die SharePoint-Token, die zurückgegeben werden.  
  
|**Versionstoken**|**Description**|  
|------------------------|---------------------|  
|WSS_V2_Compatible|Es ist eine [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]-, [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]-, [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]-, [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]- oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Installation vorhanden, die mit [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0 kompatibel ist.|  
|WSS_V3_Compatible|Es ist eine [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]-, [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]-, [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]-, [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]- oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Installation vorhanden, die mit [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 kompatibel ist.|  
|WSS_V4_Compatible|Es ist eine [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] - oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Installation vorhanden, die mit Office 14 kompatibel ist.|  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  