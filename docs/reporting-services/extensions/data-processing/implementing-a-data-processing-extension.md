---
title: Implementing a Data Processing Extension | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 372d21a412efec6306912950e7f9f5a6f577ee3f
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-a-data-processing-extension"></a>Implementieren von Datenverarbeitungserweiterungen
  Mithilfe von Datenverarbeitungserweiterungen in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] können Sie eine Verbindung zu einer Datenquelle herstellen und Daten abrufen. Sie dienen außerdem als Verbindung zwischen einer Datenquelle und einem Dataset. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]datenverarbeitungserweiterungen werden nach einer Untermenge der modelliert die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] .NET-datenanbieterschnittstellen nachgebildet.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Übersicht über die Verarbeitung von Erweiterungen](../../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)  
 Erläutert, wie eine benutzerdefinierte Datenverarbeitungserweiterung für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] geschrieben wird.  
  
 [Vorbereiten der Implementierung von Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/preparing-to-implement-a-data-processing-extension.md)  
 Beschreibt die verfügbaren Schnittstellen beim Implementieren einer [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterung sowie den Fall, in dem Sie eine bestimmte Schnittstelle implementieren müssen.  
  
 [Erstellen eine Bibliothek für Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/creating-a-data-processing-extension-library.md)  
 Beschreibt die Zuordnung eines Namespace für Ihre [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterung und die Kompilierung Ihrer Datenverarbeitungserweiterung in eine DLL-Bibliothek.  
  
 [Implementieren einer Connection-Klasse für eine Datenverarbeitungserweiterung](../../../reporting-services/extensions/data-processing/implementing-a-connection-class-for-a-data-processing-extension.md)  
 Beschreibt die Attribute einer Verbindung und eine eigene Implementierung **Verbindung** Klasse für Ihre datenverarbeitungserweiterung.  
  
 [Implementieren eine Befehlsklasse für eine Datenverarbeitungserweiterung](../../../reporting-services/extensions/data-processing/implementing-a-command-class-for-a-data-processing-extension.md)  
 Beschreibt die Attribute eines Befehls und eine eigene Implementierung **Befehl** Klasse für Ihre datenverarbeitungserweiterung.  
  
 [Implementieren einer DataReader-Klasse für Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/implementing-a-datareader-class-for-a-data-processing-extension.md)  
 Beschreibt die Attribute eines Datenlesers und eine eigene Implementierung **DataReader** Klasse für Ihre datenverarbeitungserweiterung.  
  
 [Verwenden eines externen Datasets mit Reporting Services](../../../reporting-services/extensions/data-processing/using-an-external-dataset-with-reporting-services.md)  
 Beschreibt, wie Sie Ihre benutzerdefinierte verfügbar zu machen **DataSet** Objekte auf dem Berichtsserver für die Nutzung.  
  
 [Deploying a Data Processing Extension](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
 Beschreibt, wie Sie eine Datenverarbeitungserweiterung bereitstellen  
  
 [Debuggen von Code für Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/debugging-data-processing-extension-code.md)  
 Beschreibt, wie Sie Code in Ihren Datenverarbeitungserweiterungen debuggen  
  
 [Entfernen von Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/removing-a-data-processing-extension.md)  
 Beschreibt, wie Sie eine Datenverarbeitungserweiterung von einem Berichtsserver oder Berichts-Designer entfernen  
  
 Ein Beispiel für eine vollständig implementierte datenverarbeitungserweiterung finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
