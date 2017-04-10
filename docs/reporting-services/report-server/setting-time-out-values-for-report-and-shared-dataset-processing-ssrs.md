---
title: "Festlegen von Timeoutwerten f&#252;r die Verarbeitung von Berichten und freigegebenen Datasets (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Timeoutwerte [Reporting Services]"
  - "Abfragetimeoutwerte [Reporting Services]"
  - "Berichtsverarbeitung [Reporting Services], Timeouts"
  - "Timeoutwerte für die Berichtsausführung [Reporting Services]"
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
caps.latest.revision: 39
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 39
---
# Festlegen von Timeoutwerten f&#252;r die Verarbeitung von Berichten und freigegebenen Datasets (SSRS)
  Sie können [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Timeoutwerte angeben, um Grenzwerte für die Verwendung der Systemressourcen festzulegen. Der Berichtsserver unterstützt die folgenden beiden Timeoutwerte:  
  
-   Ein Abfragetimeoutwert für ein eingebettetes Dataset gibt an, wie viele Sekunden der Berichtsserver auf eine Antwort von der Datenbank wartet. Dieser Wert wird in einem Bericht definiert.  
  
-   Ein Abfragetimeoutwert für ein freigegebenes Dataset gibt an, wie viele Sekunden der Berichtsserver auf eine Antwort von der Datenbank wartet. Dieser Wert ist Teil der Definition des freigegebenen Datasets und kann geändert werden, wenn Sie das freigegebene Dataset auf dem Berichtsserver verwalten.  
  
-   Ein Timeoutwert für die Berichtsausführung gibt an, wie viele Sekunden diese Berichtsverarbeitung maximal dauern darf, bevor sie beendet wird. Dieser Wert wird auf Systemebene definiert. Sie können diesen Wert für die jeweiligen Berichte anpassen.  
  
 Die meisten Timeoutfehler treten während der Abfrageverarbeitung auf. Verwenden Sie beim Auftreten von Timeoutfehlern einen höheren Abfragetimeoutwert. Passen Sie unbedingt den Timeoutwert für die Berichtsausführung so an, dass dieser Wert höher als der Abfragetimeoutwert ist. Dieser Zeitraum sollte so lang sein, dass sowohl die Abfrage- als auch die Berichtsverarbeitung abgeschlossen werden kann.  
  
## Festlegen eines Abfragetimeouts für ein eingebettetes Dataset in einem Bericht  
 Abfragetimeoutwerte werden im Rahmen der Erstellung eines Berichts beim Definieren eines eingebetteten Datasets angegeben. Der Timeoutwert wird zusammen mit dem Bericht im **Timeout**-Element der Berichtsdefinition gespeichert. Standardmäßig ist dieser Wert auf 30 Sekunden festgelegt. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Benutzer mit der Berechtigung zum Ändern der Eigenschaften eines veröffentlichten Berichts können diesen Wert zurücksetzen, indem sie die Definitionsdatei des Berichts bearbeiten.  
  
 Einen Abfragetimeoutwert können Sie auch für datengesteuerte Abonnements angeben. Der Wert für das Abfragetimeout wird auf den Seiten für die datengesteuerten Abonnements festgelegt. Der angegebene Wert bestimmt, wie lange der Berichtsserver beim Abrufen von Daten aus der Abonnentendatenquelle auf den Abschluss der Abfrageverarbeitung wartet.  
  
## Festlegen eines Abfragetimeouts für einen freigegebenes Dataset  
 Abfragetimeoutwerte werden auf dem Berichtsserver in Sekunden angegeben, wenn Sie ein freigegebenes Dataset erstellen oder verwalten. Standardmäßig wird dieser Wert auf 0 Sekunden festgelegt, was bedeutet, dass kein Timeoutwert vorhanden ist. Weitere Informationen finden Sie unter [Verwalten von freigegebenen Datasets](../../reporting-services/report-data/manage-shared-datasets.md).  
  
## Festlegen eines Timeoutwerts für die Berichtsausführung  
 Sie können einen Timeoutwert für die Berichtsausführung festlegen, um die Verarbeitungszeit des Berichtsservers für einen Bericht zu begrenzen. Timeoutwerte für die Berichtsausführung können im Berichts-Manager angegeben werden. Sie können auf der Seite Siteeinstellungen für alle Berichte einen Standardwert festlegen und diesen Wert später auf der Eigenschaftenseite Ausführung für einen speziellen Bericht überschreiben. Standardmäßig ist der Wert auf 1800 Sekunden festgelegt. Weitere Informationen finden Sie unter [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md).  
  
## Auswerten von Timeoutwerten für die Berichtsausführung  
 Der Berichtsserver wertet Aufträge, die ausgeführt werden,  in Zeitabständen von 60 Sekunden aus. Alle 60  Sekunden vergleicht der Berichtsserver die tatsächliche Verarbeitungszeit mit dem Timeoutwert für die Berichtsausführung. Falls die Verarbeitungszeit für einen Bericht den Timeoutwert für die Berichtsausführung übersteigt, wird die Berichtsverarbeitung angehalten.  
  
 Beachten Sie Folgendes: Wenn ein Timeoutwert unter 60 Sekunden angegeben wird, kann der Bericht vollständig ausgeführt werden, falls die Verarbeitung während der Ruhezeit des Zyklus beginnt und endet, in der der Berichtsserver die ausgeführten Aufträge nicht auswertet. Wenn Sie z. B. einen Timeoutwert von 10 Sekunden für einen Bericht festlegen, dessen Ausführung 20 Sekunden dauert, wird der Bericht vollständig verarbeitet, falls die Berichtsausführung früh im 60 Sekunden-Zyklus beginnt.  
  
> [!NOTE]  
>  Sie können die Einstellung **RunningRequestsDbCycle** in der Datei „RSReportServer.config“ festlegen, um die Häufigkeit zu ändern, mit der Aufträge, die ausgeführt werden, ausgewertet werden.  
  
## Siehe auch  
 [Festlegen von Verarbeitungsoptionen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Verwalten eines ausgeführten Prozesses](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  