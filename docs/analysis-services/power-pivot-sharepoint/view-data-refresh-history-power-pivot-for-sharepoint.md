---
title: "Ansicht Datenaktualisierungsverlauf (PowerPivot für SharePoint) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- data refresh history [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 4c8d8aa8-794d-4f72-ace3-78d0e688e1a5
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 43dce2aa27cfda6251eeca52eba4f74f722f4ced
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="view-data-refresh-history-power-pivot-for-sharepoint"></a>Anzeigen des Verlaufs der Datenaktualisierungen (PowerPivot für SharePoint)
  Der Verlauf der Datenaktualisierung ist ein Datensatz aller Datenaktualisierungsaktivitäten für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten in einer Excel-Arbeitsmappe. Datenaktualisierungsvorgänge werden für eine Analysis Services-Serverinstanz in einer SharePoint-Farm nach einem von Ihnen vorgegebenen Zeitplan ausgeführt. Standardmäßig wird der Datenaktualisierungsverlauf ein Jahr lang beibehalten. Ein Farmadministrator kann jedoch eine andere Beibehaltungsrichtlinie für Verwendungs- und Ereignisverläufe angeben. Diese bestimmt, wie lange Datensätze für Datenaktualisierungen beibehalten werden.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **In diesem Thema:**  
  
 [Erforderliche Komponenten](#prereq)  
  
 [Anzeigen des Datenaktualisierungsverlaufs für eine einzelne Arbeitsmappe](#viewhistory)  
  
 [Anzeigen des Datenaktualisierungsverlaufs für alle Arbeitsmappen](#viewITOps)  
  
 [Verwenden von Verlaufsinformationen](#pageelements)  
  
##  <a name="prereq"></a> Erforderliche Komponenten  
 Zum Anzeigen des Datenaktualisierungsverlaufs müssen Sie mindestens über Teilnahmeberechtigungen verfügen.  
  
 Die Datenaktualisierung muss für eine Arbeitsmappe, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthält, aktiviert und geplant sein. Wenn Sie keine Datenaktualisierung geplant haben, wird anstelle von Verlaufsinformationen die Seite zur Definition des Zeitplans angezeigt.  
  
##  <a name="viewhistory"></a> Anzeigen des Datenaktualisierungsverlaufs für eine einzelne Arbeitsmappe  
  
1.  Öffnen Sie auf einer SharePoint-Website die Bibliothek, die eine Excel-Arbeitsmappe mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthält.  
  
     Es gibt keinen visuellen Indikator dafür, welche Arbeitsmappen in einer SharePoint-Bibliothek [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthalten. Sie müssen im Voraus wissen, welche Arbeitsmappe aktualisierbare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthält.  
  
2.  Wählen Sie die Arbeitsmappe aus, und klicken Sie dann auf den rechts angezeigten Pfeil nach unten.  
  
3.  Wählen Sie **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Datenaktualisierung verwalten** aus.  
  
 Die Verlaufsseite wird mit einem vollständigen Datensatz aller Aktualisierungsaktivitäten angezeigt, die für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten in der aktuellen Excel-Arbeitsmappe ausgeführt werden.  
  
##  <a name="viewITOps"></a> Anzeigen des Datenaktualisierungsverlaufs für alle Arbeitsmappen  
 Mithilfe des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboards in der Zentraladministration können Farmadministratoren und Dienstanwendungsadministratoren eine umfassende Ansicht des Datenaktualisierungsverlaufs und -status für alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen abrufen. Weitere Informationen finden Sie unter [PowerPivot-Management-Dashboard und Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="pageelements"></a> Verwenden von Verlaufsinformationen  
 Die Seite Verlauf der Datenaktualisierung enthält ausführliche Informationen zu jedem Aktualisierungsvorgang. Mithilfe der Informationen auf dieser Seite können Sie feststellen, ob eine Aktualisierung ausgeführt wurde bzw. warum ein Fehler aufgetreten ist.  
  
|Element|Description|  
|----------|-----------------|  
|Name|Gibt den Dateinamen der Excel-Arbeitsmappe an, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthält.|  
|Aktueller Status|Die Werte lauten **Geplant**, **Wird aktualisiert**, **Erfolgreich beendet**oder **Fehler**.<br /><br /> **Geplant** wird beim erstmaligen Erstellen des Zeitplans angezeigt. Nachdem die Datenaktualisierung zum ersten Mal ausgeführt wurde, wird diese Statusmeldung nicht mehr angezeigt.<br /><br /> **Wird aktualisiert** gibt an, dass die Datenaktualisierung ausgeführt wird. Eine Anforderung befindet sich entweder in der Verarbeitungswarteschlange oder wird aktiv auf dem Server ausgeführt.<br /><br /> **Erfolgreich beendet** gibt an, dass der letzte Datenaktualisierungsvorgang abgeschlossen und die aktualisierte Arbeitsmappe wieder in die SharePoint-Bibliothek eingecheckt wurde.<br /><br /> **Fehler** gibt an, dass der letzte Datenaktualisierungsvorgang nicht erfolgreich war. Die aktualisierten Daten wurden nicht gespeichert. Die Arbeitsmappe enthält die gleichen Daten wie vor der Datenaktualisierung.|  
|Letzte erfolgreiche Aktualisierung|Gibt das Datum an, zu dem die letzte Datenaktualisierung erfolgreich abgeschlossen wurde.|  
|Nächste planmäßige Aktualisierung|Gibt das Datum an, zu dem die nächste Datenaktualisierung geplant ist.<br /><br /> Über den Link **Zeitplan konfigurieren** rufen Sie die Seite zum Definieren des Zeitplans auf. Wenn Sie über Teilnahmeberechtigungen für die Arbeitsmappe verfügen, können Sie auf den Link klicken, um die Zeitplaninformationen anzuzeigen und zu ändern, über die die unbeaufsichtigte Datenaktualisierung für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten in der Arbeitsmappe gesteuert wird.|  
|Gestartet|**Gestartet** gibt im Abschnitt mit Verlaufsdetails die tatsächliche Verarbeitungszeit an. Die tatsächliche Verarbeitungszeit kann von der geplanten Zeit abweichen. Die Verarbeitung wird gestartet, sobald genügend Arbeitsspeicher auf dem Server verfügbar ist. Wenn der Server sehr ausgelastet ist, kann die Verarbeitung auch einige Stunden nach der angegebenen Startzeit beginnen.|  
|Abgeschlossen|**Abgeschlossen** gibt im Abschnitt mit Verlaufsdetails an, wann der Datenaktualisierungsvorgang beendet wurde. Das Datum und die Uhrzeit geben an, wann die Arbeitsmappe wieder in die Bibliothek eingecheckt wurde.<br /><br /> Bei einem Datenaktualisierungsfehler wird die Fehlerursache anhand mindestens einer Fehlermeldung erläutert. Sie können jeden Datensatz erweitern, um ausführliche Statusinformationen anzuzeigen. Jede Datenquelle wird einzeln mit der jeweiligen Erfolgsmeldung oder der Fehlermeldung aufgeführt, die erklärt, warum die Datenaktualisierung nicht abgeschlossen wurde.|  
|Zeit|Gibt die kumulierte Zeit vom Beginn der Datenaktualisierung bis zu ihrem Ende an.|  
|Status|Stellt einen Verlaufsdatensatz mit Informationen dazu bereit, ob ein Aktualisierungsvorgang erfolgreich oder fehlerhaft war.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren der Sammlung von Verwendungsdaten für Power Pivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Planen einer Datenaktualisierung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/8571208f-6aae-4058-83c6-9f916f5e2f9b)   
 [Power Pivot-Datenaktualisierung](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
