---
title: Festlegen von Verarbeitungsoptionen (Reporting Services im integrierten SharePoint-Modus) | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 645e4258f9185f748af496aa37aff13af08ce2a7
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>Festlegen von Verarbeitungsoptionen (Reporting Services im integrierten SharePoint-Modus)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Sie können Verarbeitungsoptionen für einen Reporting Services-Bericht, um zu bestimmen, wann eine Datenverarbeitung ausgeführt festlegen. Sie können auch einen Timeoutwert für die Berichtsverarbeitung und Optionen festlegen, mit denen bestimmt wird, ob der Berichtsverlauf für den aktuellen Bericht aktiviert ist.  
  
-   Sie können einen Bericht als Berichtsmomentaufnahme ausführen, um zu verhindern, dass der Bericht zu willkürlichen Zeiten ausgeführt wird (z. B. während einer geplanten Sicherung). Eine Berichtsmomentaufnahme wird gewöhnlich gemäß einem Zeitplan erstellt und später aktualisiert. Auf diese Weise können Sie genau planen, wann der Bericht und die Daten verarbeitet werden. Falls ein Bericht auf Abfragen basiert, deren Ausführung viel Zeit in Anspruch nimmt oder die Daten von einer Datenquelle verwenden, auf die während eines bestimmten Zeitraums kein Benutzer Zugriff haben soll, sollten Sie den Bericht als Momentaufnahme ausführen.  
  
-   Ein Berichtsserver kann eine Kopie eines verarbeiteten Berichts zwischenspeichern und diese anzeigen, wenn ein Benutzer den Bericht öffnet. Die Zwischenspeicherung ist eine Technik zur Leistungsoptimierung. Durch die Zwischenspeicherung kann ein Bericht schneller abgerufen werden, falls der Bericht sehr umfangreich ist oder häufig abgerufen wird.  
  
-   Der Berichtsverlauf enthält eine Auflistung der zuvor ausgeführten Kopien eines Berichts. Mithilfe des Berichtsverlaufs können Sie eine Aufzeichnung eines Berichts für einen bestimmten Zeitraum verwalten. Der Berichtsverlauf ist nicht für Berichte mit vertraulichen oder persönlichen Daten gedacht. Aus diesem Grund kann der Berichtsverlauf nur jene Berichte enthalten, von denen die Abfrage einer Datenquelle mithilfe eines einzigen Satzes von Anmeldeinformationen durchgeführt wird, die für alle einen Bericht ausführenden Benutzer verfügbar sind. (Die Anmeldeinformationen müssen entweder gespeicherte Anmeldeinformationen oder Anmeldeinformationen für die unbeaufsichtigte Berichtsausführung sein.)  

    Reporting Services-Integration mit SharePoint verwendet das Auschecken und Einchecken von Content Management-Funktionen von SharePoint, um Updates in Reporting Services-Inhaltstypen zu speichern. Dies umfasst auch die Erstellung von Berichtsmomentaufnahmen. Wenn Sie die Versionsverwaltung für eine Dokumentbibliothek aktiviert haben, wird die Berichtsversion aktualisiert, wenn eine neue Berichtsverlaufs-Momentaufnahme erstellt wird. Dies ist eine zusätzliche Auswirkung der Aktualisierung von Momentaufnahmen. Bei der Aktualisierung einer Momentaufnahme wird die LastExecution-Eigenschaft des Berichts geändert, und dadurch erfolgt gleichzeitig eine Änderung in der Version des Berichts.  

-   Mithilfe von Timeoutwerten können Sie Grenzwerte für die Verwendung der Systemressourcen festlegen.  

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

## <a name="set-data-refresh-options"></a>Datenaktualisierungsoptionen festlegen
  
1.  Zeigen Sie auf einen Bericht in der Bibliothek.  
  
2.  Klicken Sie auf den Pfeil nach unten, und wählen Sie **Verarbeitungsoptionen verwalten**aus.  
  
3.  Klicken Sie unter **Datenaktualisierungsoptionen**auf **Momentaufnahmedaten verwenden**. Wenn die Meldung "Dieser Bericht kann nicht über eine Momentaufnahme ausgeführt werden, da mindestens eine Anmeldeinformation für die Datenquellen nicht gespeichert ist" angezeigt wird, bedeutet dies, dass der Bericht nicht für die unbeaufsichtigte Ausführung konfiguriert ist und Sie vor dem Festlegen dieser Option die Datenquellen zum Verwenden gespeicherter Anmeldeinformationen konfigurieren müssen.  
  
4.  Wählen Sie unter **Optionen für Datenmomentaufnahmen**die Option **Datenverarbeitung planen**aus.  
  
5.  Wählen Sie **Nach einem freigegebenen Zeitplan** , wenn Sie über einen vorhandenen freigegebenen Zeitplan verfügen, den Sie verwenden möchten. Wählen Sie andernfalls **Nach einem benutzerdefinierten Zeitplan**, und klicken Sie auf **Konfigurieren**.  
  
6.  Wählen Sie eine Häufigkeit, einen Zeitplan sowie Werte für das Start- und das Enddatum aus, und klicken Sie anschließend auf **OK**.  
  
7.  Wählen Sie unter **Optionen für Datenmomentaufnahmen**die Option **Die Momentaufnahme beim Speichern dieser Seite erstellen oder aktualisieren** aus, wenn Sie unmittelbar Momentaufnahmedaten für die Verwendung im Bericht erstellen möchten, ohne auf die Ausführung der geplanten Datenverarbeitung zu warten.  
  
## <a name="set-report-caching-options"></a>Optionen zum Zwischenspeichern von Berichten festlegen
  
1.  Zeigen Sie auf einen Bericht in der Bibliothek.  
  
2.  Klicken Sie auf den Pfeil nach unten, und wählen Sie **Verarbeitungsoptionen verwalten**aus.  
  
3.  Klicken Sie unter **Datenaktualisierungsoptionen**auf **Zwischengespeicherte Daten verwenden**. Wenn die Meldung "Dieser Bericht kann nicht zwischengespeichert werden, da mindestens eine Anmeldeinformation für die Datenquelle nicht gespeichert ist" angezeigt wird, bedeutet dies, dass der Bericht nicht für die unbeaufsichtigte Ausführung konfiguriert ist und Sie vor dem Festlegen dieser Option die Datenquellen zum Verwenden gespeicherter Anmeldeinformationen konfigurieren müssen.  
  
4.  Geben Sie unter **Cacheoptionen**an, wie der Cache abläuft:  
  
    -   Geben Sie an, nach wie vielen Minuten der Cache abläuft.  
  
    -   Verwenden Sie einen freigegebenen Zeitplan, um den Cache zu den im Zeitplan angegebenen Zeiten zu leeren.  
  
    -   Erstellen Sie einen benutzerdefinierten Zeitplan, um den Cache zu einem angegebenen Zeitpunkt zu leeren.  
  
## <a name="set-processing-time-out-values"></a>Timeoutwerte für die Verarbeitung festlegen
  
1.  Zeigen Sie auf einen Bericht in der Bibliothek.  
  
2.  Klicken Sie auf den Pfeil nach unten, und wählen Sie **Verarbeitungsoptionen verwalten**aus.  
  
3.  Klicken Sie unter **Verarbeitungstimeout**auf **Die Standardeinstellung für die Site verwenden** , wenn Sie den auf der Berichtsserverebene angegebenen Wert verwenden möchten. Wählen Sie andernfalls **Kein Timeout für die Berichtsverarbeitung festlegen** oder **Berichtsverarbeitungsbeschränkung (in Sekunden)** aus, wenn Sie keinen Timeoutwert angeben oder den Timeoutwert durch einen anderen Wert überschreiben möchten.  
  
## <a name="set-report-history-options-and-limits"></a>Berichtsverlaufsoptionen und Grenzwerte festlegen
  
1.  Zeigen Sie auf einen Bericht in der Bibliothek.  
  
2.  Klicken Sie auf den Pfeil nach unten, und wählen Sie **Verarbeitungsoptionen verwalten**aus.  
  
3.  Geben Sie unter **Optionen für Verlaufsmomentaufnahmen**an, wie und wann eine Datenverarbeitung ausgeführt und gespeichert wird.  
  
4.  Wählen Sie unter **Grenzwerte für Verlaufsmomentaufnahmen**die Option **Die Standardeinstellung für die Site verwenden** , wenn Sie den auf der Berichtsserverebene angegebenen Wert verwenden möchten. Wählen Sie andernfalls **Die Anzahl von Momentaufnahmen nicht einschränken** , oder geben Sie für **Die Anzahl der Momentaufnahmen auf folgenden Wert beschränken** einen benutzerdefinierten Wert an.  
  
## <a name="set-database-timeout"></a>Datenbank-Timeout festlegen
  
*  Verwenden Sie Windows PowerShell, um das Datenbank-Timeout eines SharePoint-Berichtsservers festzulegen. Weitere Informationen finden Sie im Abschnitt zum Abrufen und Festlegen der Eigenschaften der Reporting Services-Dienstanwendungsdatenbank unter [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="next-steps"></a>Nächste Schritte

 [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Zwischenspeichern von Berichten](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [Festlegen von Timeoutwerten für die Verarbeitung von Berichten und freigegebenen Datasets](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
