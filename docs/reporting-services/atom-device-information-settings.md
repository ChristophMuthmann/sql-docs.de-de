---
title: "ATOM-Ger&#228;teinformationseinstellungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
caps.latest.revision: 7
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 7
---
# ATOM-Ger&#228;teinformationseinstellungen
  Die Geräteinformationseinstellungen für die Atom-Renderingerweiterung unterstützen die Übergabe des Namens eines Atom-Feeds und der zu verwendenden Zeichencodierung.  
  
 In der folgenden Tabelle sind die Geräteinformationseinstellungen für das Rendering in einem Datendienstdokument aufgeführt.  
  
|Einstellung|Wert|  
|-------------|-----------|  
|**DataFeed**|Wenn diese Einstellung angegeben ist, wird der Atom-Feed entsprechend dem Feednamen gerendert, der in ihr bereitgestellt wird. Andernfalls wird das Atom-Dienstdokument für den Bericht gerendert. Der eindeutige automatisch generierte Bezeichner des Datenfeeds. Dieser Wert wird intern verwendet, und Sie sollten ihn nicht ändern.|  
|**Codierung**|Der Internet Assigned Numbers Authority (IANA)-Name einer Zeichencodierung, die von .NET Framework unterstützt wird. Der Standardwert ist **UTF-8**. Beispiele für andere Werte: ASCII, UTF-7 und UTF-16.|  
  
## Siehe auch  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Übergeben von Geräteinformationseinstellungen an Renderingerweiterungen](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Anpassen der Parameter für Renderingerweiterungen in der Datei RSReportServer.config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Technische Referenz &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  