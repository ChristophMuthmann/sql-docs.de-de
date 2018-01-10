---
title: "Verwenden einer externen Datenquelle für Abonnentendaten (datengesteuertes Abonnement) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: subscriptions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriber data sources [Reporting Services]
- subscriptions [Reporting Services], external data sources
- query-based subscriptions [Reporting Services]
- external data sources [Reporting Services]
- data-driven subscriptions
- data sources [Reporting Services], subscriptions
ms.assetid: 1cade8ec-729c-4df8-a428-e75c9ad86369
caps.latest.revision: "43"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d500b82566f2efaed147f7c7697bf0cf404e37b5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="use-an-external-data-source-for-subscriber-data-data-driven-subscription"></a>Verwenden einer externen Datenquelle für Abonnentendaten (datengesteuertes Abonnement)
  In einem datengesteuerten Abonnement werden dynamische Abonnementdaten von einer Abfrage oder einem Befehl bereitgestellt, die bzw. der Daten aus einer externen Datenquelle abruft. Abonnementdaten können aus allen unterstützten Datenquellen abgerufen werden, die die Anforderungen der datengesteuerten Abonnementverarbeitung erfüllen. Die Abfrage- oder Befehlssyntax muss für eine Datenverarbeitungserweiterung gültig sein, die mit dem Berichtsserver installiert wurde.  
  
## <a name="data-processing-requirements"></a>Anforderungen für die Datenverarbeitung  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet Datenverarbeitungserweiterungen zum Abrufen von Abonnementdaten. Folgende Datenquellentypen werden empfohlen:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken  
  
-   Oracle-Datenbanken  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - und Data Mining-Datenquellen  
  
-   XML-Datenquellen  
  
     Stellen Sie sicher, dass Sie die Einstellungen für das Abfragetimeout im Abonnement erhöht haben, wenn Sie die XML-Datenverarbeitungserweiterung für Abonnentendaten verwenden. Bei der XML-Datenverarbeitungserweiterung werden für die Abfragetimeoutwerte Millisekunden statt Sekunden verwendet. Wenn Sie den Wert für das Timeout nicht erhöhen, führt das Abonnement möglicherweise zu einem Fehler, da die Verarbeitungszeit zu kurz ist.  
  
     Verwenden Sie die Option **Anmeldeinformationen sind nicht erforderlich** möglichst nicht, wenn Sie die Verbindung zur Datenquelle für Abonnentendaten konfigurieren. Bei der Verwendung der XML-Datenverarbeitungserweiterung zum Abrufen von Abonnementdaten zur Laufzeit werden gespeicherte Anmeldedaten empfohlen.  
  
 Sie können möglicherweise andere unterstützte Datenquellentypen verwenden, aber es kann nicht garantiert werden, dass diese funktionsfähig sind. Die folgenden Datenquellentypen können beispielsweise nicht für Abonnentendaten verwendet werden:  
  
-   SAP Netweaver BI-Datenbanken  
  
-   Berichtsmodelle  
  
 Wenn Sie über eine benutzerdefinierte Datenverarbeitungserweiterung verfügen, die Sie in datengesteuerten Abonnements verwenden möchten, muss diese die Schnittstellen <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> und <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> implementieren. Die Datenverarbeitungserweiterung muss eine Abfrageausführung vom Typ schema only unterstützen. Diese Abfrage wird zum Abrufen von Spaltenmetadaten zur Entwurfszeit verwendet, damit Benutzer Übermittlungsoptionen und Berichtsparametern in der Abonnementdefinition Spalten zuordnen können. Die Abfrageausführung vom Typ schema only tritt in einem frühen Stadium auf, wenn der Benutzer das Abonnement definiert.  
  
## <a name="query-requirements"></a>Abfrageanforderungen  
 Beachten Sie beim Erstellen einer Abfrage, bei der Abonnementdaten abgerufen werden, folgende Punkte:  
  
-   Sie können nur eine Abfrage für das Abonnement erstellen.  
  
-   Die Abfrage muss alle Werte zurückgeben, die Sie für Übermittlungsoptionen und zum Angeben von Berichtsparametern verwenden möchten.  
  
-   Vom Berichtsserver wird eine Berichtsübermittlung für jede Zeile im Resultset erstellt. Wenn das Resultset aus dreihundert Zeilen besteht, versucht der Berichtsserver, dreihundert Berichte zu übermitteln.  
  
## <a name="setting-delivery-options-using-variable-data-from-a-subscriber-database"></a>Festlegen von Übermittlungsoptionen mithilfe von Variablendaten aus einer Abonnentendatenbank  
 Sie können Daten in der Abonnentendatenbank verwenden, um die Übermittlungsoptionen für die einzelnen Empfänger anzupassen. Mit der von Ihnen verwendeten Art der Übermittlungserweiterung wird bestimmt, welche Optionen verfügbar sind. Falls Sie die E-Mail-Übermittlungserweiterung des Berichtsservers verwenden, sollte die Abfrage für jeden Abonnenten einen E-Mail-Alias enthalten. Wenn Sie die Dateifreigabeübermittung verwenden, sollten die Abonnentendaten Werte enthalten, die zum Erstellen abonnentenspezifischer Berichtsdateien oder zum Bereitstellen eines Ziels für die Übermittlung verwendet werden können. Weitere Informationen finden Sie unter [E-Mail-Übermittlung in Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
## <a name="passing-parameter-values-from-the-subscriber-database-to-the-report"></a>Übergeben von Parameterwerten aus der Abonnentendatenbank an den Bericht  
 Wenn Sie ein datengesteuertes Abonnement für einen parametrisierten Bericht erstellen, können Sie Variablenparameterwerte verwenden, um die Ausgabe der einzelnen Berichte anzupassen. Beispielsweise könnte die Abonnentendatenbank Mitarbeiteridentifikationsnummern, Einstellungsdaten, Tätigkeitsbezeichnungen und Informationen zum Bürostandort enthalten, mit denen Berichtsdaten gefiltert werden können. Falls der Bericht Parameter akzeptiert, die auf diesen oder anderen verfügbaren Spaltendaten basieren, können Sie den Parameter der entsprechenden Spalte zuordnen.  
  
 Stellen Sie beim Zuordnen von Abonnentenfeldern zu Berichtsparametern sicher, dass die Datentypen und Spaltenlängen kompatibel sind. Bei einem Datentypenkonflikt tritt bei der Abonnementverarbeitung ein Fehler auf. Weitere Informationen zum Verwenden von Abonnentendaten in einem parameterisierten Bericht finden Sie unter [Erstellen eines datengesteuerten Abonnements (SSRS-Tutorial)](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md).  
  
## <a name="modifying-the-subscriber-data-source"></a>Ändern der Datenquelle für Abonnentendaten  
 Die folgenden Änderungen an der Datenquelle für Abonnentendaten können das Ausführen des Abonnements verhindern:  
  
-   Entfernen von Spalten, auf die im Abonnement verwiesen wird.  
  
-   Ändern der Tabellenstruktur der Datenquelle.  
  
-   Ändern des Datentyps und anderer Spalteneigenschaften.  
  
 Falls Sie solche Änderungen vornehmen, müssen Sie das Abonnement aktualisieren.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen, Ändern und Löschen von datengesteuerten Abonnements](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [Datengesteuerte Abonnements](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Abonnements und Übermittlung (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  
