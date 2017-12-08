---
title: Fehler beim Versuch, eine Verbindung herstellen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bbc70ccf710772ba1b32abe5b65858d95ef2b38e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection"></a>Während eines Versuchs zum Herstellen einer Verbindung ist ein Fehler aufgetreten.
  Dieser Fehler tritt auf, wenn Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten auf einem Server abfragen, auf dem [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint nicht installiert ist. Er tritt auch auf, wenn der SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])-Dienst beendet wird, oder wenn Sie versuchen, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten von einer früheren Version anzuzeigen.  
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Gilt für|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint|  
|Produktversion|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Ursache|Fehler beim Herstellen der Datenverbindung.|  
|Meldungstext|Während des Herstellens einer Verbindung mit der externen Datenquelle ist ein Fehler aufgetreten. Die folgenden Verbindungen wurden nicht aktualisiert: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten|  
  
## <a name="explanation"></a>Erklärung  
 Dieser Fehler wird in Excel Services zurückgegeben, wenn der SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] )-Dienst beendet wurde oder wenn Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten in einer Excel-Arbeitsmappe abfragen, die in SharePoint veröffentlicht ist, und die SharePoint-Umgebung über keinen[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]für SharePoint-Server verfügt.  
  
 Der Fehler tritt auf, wenn Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten nach Slices aufteilen oder filtern, während kein Abfragemodul verfügbar ist.  
  
## <a name="user-action"></a>Benutzeraktion  
 Installieren Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint, oder verschieben Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe in eine SharePoint-Umgebung, in der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint installiert ist. Weitere Informationen finden Sie unter [PowerPivot für SharePoint 2010-Installation](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f).  
  
 Wenn die Software installiert ist, überprüfen Sie, ob die SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])-Instanz ausgeführt wird. Prüfen Sie **Dienste auf dem Server verwalten** in der Zentraladministration. Prüfen Sie auch die Dienste-Konsolenanwendung in der Verwaltung.  
  
 Für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen, die in einer SQL Server 2008 R2-Version von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel erstellt wurden, muss die SQL Server 2008 R2-Version vom OLE DB-Anbieter für Analysis Services installiert werden. Dieser Fehler tritt auf, wenn Sie den Anbieter installiert, die Datei Microsoft.AnalysisServices.ChannelTransport.dll jedoch nicht registriert haben. Weitere Informationen zur Dateiregistrierung finden Sie unter [Installieren des OLE DB-Anbieters für Analysis Services auf SharePoint-Servern](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="see-also"></a>Siehe auch  
 [Die Datenverbindung verwendet die Windows-Authentifizierung, und Benutzeranmeldeinformationen konnten nicht delegiert werden. Die folgenden Verbindungen wurden nicht aktualisiert: Power Pivot-Daten.](../../analysis-services/power-pivot-sharepoint/the-data-connection-user-could-not-be-delegated.md)  
  
  
