---
title: Entfernen von Renderingerweiterungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: "38"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8ede297625756d8e1d13f2f5a297ebf72e580a21
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="removing-a-rendering-extension"></a>Entfernen von Renderingerweiterungen
  Um eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Renderingerweiterung zu entfernen, entfernen Sie einfach das **Extension**-Element für Ihre Renderingerweiterung im Ordner **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<Instanzname>\Reporting Services\ReportServer** aus der Datei „rsreportserver.config“. Wenn Sie Einträge für einen Berichts-Designer und einen Berichtsserver vorgenommen haben, entfernen Sie das **Extension**-Element auch aus der [Konfigurationsdatei RSReportDesigner](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md). Nachdem Sie die Konfigurationsdaten entfernt haben, steht die Renderingerweiterung nicht mehr für die Komponente zur Verfügung.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Konfigurationsdateien](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Implementing a Rendering Extension (Implementieren von Renderingerweiterungen)](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Übersicht über Renderingerweiterungen](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementieren der IRenderingExtension-Schnittstelle](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Überlegungen zur Sicherheit von Erweiterungen](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [Bereitstellen von Renderingerweiterungen](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
