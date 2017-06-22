---
title: Deploying a Data Processing Extension | Microsoft Docs
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d312cdf2c5588c8dc12ff000fe4163d7f562ea7f
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="deploying-a-data-processing-extension"></a>Bereitstellen von Datenverarbeitungserweiterungen
  Sobald Sie geschrieben und kompiliert Ihre [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] datenverarbeitungserweiterung in eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Bibliothek, müssen Sie sie vom Berichtsserver und Berichts-Designer erkennbar machen. Dazu müssen Sie lediglich die Erweiterung in die entsprechenden Verzeichnisse kopieren und Einträge zu den zugehörigen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Konfigurationsdateien hinzufügen.  
  
## <a name="configuration-file-extension-element"></a>Extension-Element für die Konfigurationsdatei  
 Datenverarbeitungserweiterungen, die Sie auf dem Berichtsserver oder Berichts-Designer bereitstellen müssen eingegeben werden, als **Erweiterung** Elemente in den Konfigurationsdateien. Bei diesen Dateien handelt es sich um RSReportServer.config für den Berichtsserver und RSReportDesigner.config für den Berichts-Designer.  
  
 Die folgende Tabelle beschreibt die Attribute für die **Erweiterung** -Element für datenverarbeitungserweiterungen.  
  
|Attribut|Description|  
|---------------|-----------------|  
|**Name**|Ein eindeutiger Name für die Erweiterung, z. B. "SQL" für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenverarbeitungserweiterung oder "OLEDB" für die OLE DB-Datenverarbeitungserweiterung. Die maximale Länge für das **Name** -Attribut beträgt 255 Zeichen. Der Name muss für sämtliche Einträge im **Extension** -Element einer Konfigurationsdatei eindeutig sein.|  
|**Typ**|Eine durch Trennzeichen getrennte Liste, die den vollqualifizierten Namespace und den Namen der Assembly enthält|  
|**Visible**|Der Wert **"false"** gibt an, dass die datenverarbeitungserweiterung auf Benutzeroberflächen nicht sichtbar sollten. Wenn das Attribut nicht enthalten ist, ist **true**der Standardwert.|  
  
 Weitere Informationen zu den Dateien RSReportServer.config und RSReportDesigner.config finden Sie unter [Reporting Services Configuration Files](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Vorgehensweise: Bereitstellen eine Datenverarbeitungserweiterung auf einem Berichtsserver](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|Beschreibt, wie Sie eine Datenverarbeitungserweiterung auf einem Berichtsserver bereitstellen|  
|[Vorgehensweise: Bereitstellen eine Datenverarbeitungserweiterung für Berichts-Designer](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|Beschreibt, wie Sie eine Datenverarbeitungserweiterung für den Berichts-Designer bereitstellen|  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
