---
title: 'rsServerConfigurationError: Reporting Services-Fehler | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b10e27361b75891fda0501b218ce6d634d52103e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError – Reporting Services-Fehler
    
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|rsServerConfiguration|  
|Ereignisquelle|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Komponente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Meldungstext|Konfigurationsfehler beim Berichtsserver.|  
  
## <a name="explanation"></a>Erklärung  
 Dies ist ein allgemeiner Fehler, der auftritt, wenn der Berichtsserver oder ein Berichterstellungstool fehlerhaft konfiguriert wurde. Der Fehler wird normalerweise mit einer zweiten Meldung ausgegeben, die die tatsächliche Ursache des Fehlers enthält.  
  
 Die folgende Liste enthält die möglichen Ursachen:  
  
-   Die RSReportServer.config-Datei oder die RSReportDesigner.config-Datei kann nicht gefunden oder gelesen werden.  
  
-   XML-Elemente in einer der beiden Konfigurationsdateien fehlen oder sind ungültig.  
  
-   Werte für einen oder mehrere XML-Elemente fehlen oder sind ungültig.  
  
-   Registrierungseinstellungen sind ungültig.  
  
## <a name="user-action"></a>Benutzeraktion  
 Wenn dieser Fehler auftritt, nachdem Sie manuell eine Konfigurationsdatei bearbeitet haben, machen Sie die Änderungen rückgängig, indem Sie den ursprünglichen Wert wieder eingeben, oder stellen Sie eine vorherige Version wieder her, wenn eine Sicherung existiert.  
  
 Öffnen Sie die Ablaufverfolgungsprotokolldatei des Berichtsservers unter \Microsoft SQL Server\MSRS12.\<Instanzname>\Reporting Services\LogFiles, um zusätzliche Fehlermeldungsinformationen zu überprüfen, die mit dem **rsServerConfiguration**-Fehler ausgegeben werden. Weitere Informationen finden Sie unter [Reporting Services-Protokolldateien und Quellen](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="internal-only"></a>Nur intern  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Konfigurationsdateien](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Ändern einer Reporting Services-Konfigurationsdatei (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
