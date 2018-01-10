---
title: "XML-Geräteinformationseinstellungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
caps.latest.revision: "43"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3f0600b91d43e8449fc00eac14a699e07121fb52
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="xml-device-information-settings"></a>XML-Geräteinformationseinstellungen
  In der folgenden Tabelle werden die Geräteinformationseinstellungen zum Rendern in das XML-Format aufgeführt.  
  
|Einstellung|Werte|Details|  
|-------------|------------|-------------|  
|**XSLT**|Der Pfad zum Berichtsserver-Namespace von XSLT, der auf die XML-Datei, z.B. **/Transforms/myxslt**angewendet werden soll.|Die XSL-Datei muss eine veröffentlichte Ressource auf einem Berichtsserver sein, und Sie müssen über einen Berichtsserver-Elementpfad darauf zugreifen. Der Wert dieser Einstellung wird nach jedem XSLT übernommen, das im Bericht angegeben wird. Wird die **XSLT** -Einstellung angewendet, wird die **OmitSchema** -Einstellung nicht beachtet.|  
|**MIMEType**|MIME-Typ (Multipurpose Internet Mail Extensions) der XML-Datei||  
|**UseFormattedValues**|**true**<br /><br /> **false**|Gibt an, ob der formatierte Wert eines Textfelds beim Generieren der XML-Daten gerendert werden soll.<br /><br /> Ein false-Wert gibt an, dass der zugrundeliegende Wert des Textfelds verwendet wird.|  
|**Indented**|**true**<br /><br /> **false**|Gibt an, ob XML-Dateien mit Einzug generiert werden sollen. Der Standardwert **FALSE** generiert komprimierte XML-Dateien ohne Einzug.|  
|**OmitNamespace**|**true**<br /><br /> **false**|Gibt an, ob der Standardnamespace in der XML-Datei weggelassen werden soll.<br /><br /> Bei "true" wird kein Standardnamespace in der XML-Datei angegeben.<br /><br /> Bei "false" gibt die XML-Datei einen Standardnamespace mit dem Wert der DataSchema-Eigenschaft des Berichts an. Die DataSchema-Eigenschaft verwendet standardmäßig den Berichtsnamen.<br /><br /> Der Standardwert ist**false**.|  
|**OmitSchema**|**true**<br /><br /> **false**|Gibt an, ob der Schemaspeicherort in der XML-Datei weggelassen werden soll. Der Speicherort ist das SchemaLocation-Attribut.<br /><br /> Der Standardwert von OmitSchema hängt vom OmitNamespace-Wert ab:<br /><br /> Wenn OmitNamespace = False, gilt standardmäßig OmitSchema = **False** . Der Benutzer kann den Standardwert überschreiben, indem OmitSchema = True festgelegt wird.<br /><br /> Wenn OmitNamespace = true, gilt für OmitSchema **TRUE** – unabhängig vom explizit für OmitSchema konfigurierten Wert.|  
|**Codierung**|Der Internet Assigned Numbers Authority (IANA)-Name einer Zeichencodierung, die von .NET Framework unterstützt wird.|Der Standardwert ist **UTF-8**. Beispiele für andere Werte: ASCII, UTF-7 und UTF-16.|  
|**FileExtension**|Die Dateierweiterung für die generierte Datei.||  
|**Schema**|Der Wert **true** gibt an, dass ein XML-Schema gerendert wird. Der Standardwert ist **false**.|Gibt an, ob die XML-Schemadefinition (XSD) gerendert wird oder ob die tatsächlichen XML-Daten gerendert werden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Übergeben von Geräteinformationseinstellungen an Renderingerweiterungen](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Anpassen der Parameter für Renderingerweiterungen in der Datei „RSReportServer.config“](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Technische Referenz (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  
