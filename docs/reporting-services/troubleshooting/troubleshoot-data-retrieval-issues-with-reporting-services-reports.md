---
title: Abrufen von Daten, die Problembehandlung bei Reporting Services-Berichten | Microsoft Docs
ms.custom: 
ms.date: 02/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7680946a-1660-4b59-a03a-c4d474cd8ed3
caps.latest.revision: 4
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3f801ab4a8033d7f457aad0483ead5cb080fd8ed
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-data-retrieval-issues-with-reporting-services-reports"></a>Behandlung von Problemen beim Abrufen von Daten in Reporting Services-Berichten
Der erste Schritt bei der Berichtsverarbeitung ist das Abrufen der Berichtsdaten für jedes Dataset durch Ausführen der Datasetabfrage. Wenn Sie einen Bericht lokal in der Vorschau anzeigen, müssen für die Datenquellenverbindungen und Anmeldeinformationen ausreichende Berechtigungen zum Abrufen der Daten auf den Computer verwendet werden. Wenn Sie einen Bericht auf dem Berichtsserver ausführen, müssen für die Datenquellenverbindungen und Anmeldeinformationen ausreichende Berechtigungen zum Abrufen der Daten auf den Berichtsserver verwendet werden. Dieses Thema soll Ihnen beim Behandeln von Problemen beim Abrufen von Berichtsdaten helfen.   
  
## <a name="i-cannot-create-a-connection-to-a-data-source"></a>Ich kann keine Verbindung mit einer Datenquelle herstellen.  
Wenn Sie eine Datenquelle erstellen, eine Datasetabfrage ausführen oder eine Vorschau eines Berichts anzeigen, erhalten Sie möglicherweise die folgende Meldung: Es kann keine Verbindung mit der `<data source name>`-Datenquelle hergestellt werden.   
    
### <a name="data-source-is-not-available"></a>Die Datenquelle ist nicht verfügbar.  
Die Datenquelle ist offline oder aus einem anderen Grund nicht verfügbar.   
  
Überprüfen Sie, ob Sie über Zugriff auf die Datenquelle verfügen und ob die Datenbank verfügbar ist. Verwenden Sie z. B. SQL Server Management Studio, um eine Verbindung mit der Datenquelle herzustellen. Verwenden Sie für relationale und mehrdimensionale Datenbanken die Schaltfläche **Testen** im Dialogfeld **Verbindungseigenschaften** , um die Verbindung mit der Datenquelle und die Berechtigungen für die Datenquelle zu überprüfen.   
  
### <a name="data-source-credentials-are-not-valid"></a>Die Datenquellen-Anmeldeinformationen sind ungültig.  
Die Berechtigungen der Anmeldeinformationen, die Sie zum Herstellen der Verbindung mit der Datenquelle verwenden, reichen nicht zum Abrufen der in der Abfrage angegebenen Daten aus.  
  
Überprüfen Sie, ob Sie die richtigen Anmeldeinformationen verwenden. Beispielsweise verfügen Sie eventuell über die Berechtigung zum Abrufen von Daten aus einer Tabelle oder Sicht, jedoch nicht für eine bestimmte Spalte. Oder Sie verfügen möglicherweise nicht über ausreichende Berechtigungen zum Ausführen einer gespeicherten Prozedur, mit der eine Sicht aufgefüllt wird.   
  
> [!NOTE]  
> Berechtigungen, die Sie zum Abrufen von Daten für die Vorschau eines Berichts verwenden, unterscheiden sich möglicherweise von den Berechtigungen, die zum Abrufen von Daten nach der Veröffentlichung eines Berichts auf einem Berichtsserver erforderlich sind.   
  
### <a name="not-a-valid-password"></a>Kein gültiges Kennwort  
Bei Datenquellen mit Aufforderung zur Eingabe von Anmeldeinformationen oder mit Anmeldeinformationen, die in der Verbindungszeichenfolge angegeben sind, werden die Zeichen für das Kennwort an die zugrunde liegenden Datenquellentreiber übergeben. Wenn das Kennwort oder die Zeichenfolge Sonderzeichen, z. B. Satzzeichen, enthält, können einige Datenquellentreiber die Sonderzeichen nicht überprüfen.   
  
Stellen Sie sicher, dass das Kennwort keine Sonderzeichen enthält. Wenn das Kennwort nicht geändert werden kann, können Sie mit Ihrem Datenbankadministrator Maßnahmen ergreifen, damit die entsprechenden Anmeldeinformationen lokal auf dem Berichtsserver als Teil eines ODBC-Datenquellennamens des Systems (Data Source Name oder DSN) gespeichert werden. Weitere Informationen finden Sie unter "OdbcConnection.ConnectionString" in der .NET Framework SDK-Dokumentation auf der MSDN-Website.   
  
> [!NOTE]  
>Es wird empfohlen, der Verbindungszeichenfolge keine Anmeldeinformationen (z. B. Kennwörter) hinzuzufügen. Der Berichts-Designer bietet eine Seite für **Anmeldeinformationen** auf den Dialogfeldern [Datenquelleneigenschaften](~/reporting-services/report-data/enter-data-source-credentials-dialog-box-report-builder.md) oder [Eigenschaften der freigegebenen Datenquelle](~/reporting-services/report-data/enter-data-source-credentials-dialog-box-report-builder.md) , die Sie verwenden können, um Anmeldeinformationen einzugeben. Diese Anmeldeinformationen werden sicher auf dem Computer zur Berichterstellung gespeichert.  
  
## <a name="why-do-i-see-no-data-when-i-run-my-query-in-the-query-designer"></a>Warum werden keine Daten angezeigt, wenn ich meine Abfrage im Abfrage-Designer ausführe?  
Wenn Sie ein Dataset erstellen, wird die Datasetfeldauflistung im Berichtsdatenbereich angezeigt. Manchmal wird die Datasetfeldauflistung nicht wie erwartet angezeigt.   
  
### <a name="import-query-does-not-import-calculated-fields"></a>Mit "Abfrage importieren" werden keine berechneten Felder importiert.  
  
Zwar werden berechnete Felder in einer Berichtsdefinition gespeichert, jedoch sind sie nicht im Import enthalten, wenn Sie eine Datasetabfrage aus einem anderen Bericht importieren. Im Berichtsdatenbereich werden nur in der Datasetabfrage angegebene Felder angezeigt, nachdem Sie ein Dataset durch Importieren einer Abfrage aus einem anderen Bericht erstellt haben.   
  
Um im Berichtsdatenbereich berechnete Felder anzuzeigen, müssen Sie diese für jeden Bericht definieren, in dem sie verwendet werden.   
  
### <a name="some-data-providers-do-not-support-automatic-population-of-the-dataset-field-collection"></a>Einige Datenanbieter unterstützen keine automatische Auffüllung der Datasetfeldauflistung.  
Wenn Sie im Dialogfeld Dataseteigenschaften eine Abfrage definieren und dann das Dialogfeld schließen, wird die Datasetfeldauflistung i. d. R. im Berichtsdatenbereich angezeigt. Bei einigen Datenquellen wird die Datasetfeldauflistung nicht automatisch aufgefüllt.   
  
Gehen Sie zum Auffüllen der Datasetfeldauflistung wie folgt vor:  
* Stellen Sie sicher, dass Sie über die Berechtigungen zum Abrufen von Feldinformationen aus der Datenbank verfügen. Bei einigen Datenquellen verfügen Sie möglicherweise über Berechtigungen für den Zugriff auf die Datenquelle, jedoch nicht für den Zugriff auf die Tabelle oder Spalte. Sie verfügen eventuell über die Berechtigung für den Zugriff auf eine Sicht, jedoch über keine Berechtigungen für die Ausführung der gespeicherten Prozeduren, mit denen die Sicht erstellt wird. Um Ihren Zugriff auf spezifische Tabellen oder Spalten in einer Datenbank zu überprüfen, verifizieren Sie die Abfrageergebnisse in einer separaten Anwendung, z. B. SQL Server Management Studio, unter Verwendung derselben Berechtigungen, die Sie für den Bericht verwenden. Wenn Sie die für Ihre Abfrage gewünschten Ergebnisse nicht sehen können, wenden Sie sich an den Systemadministrator, um Ihre Berechtigungen für die Daten anzupassen.   
* Führen Sie die Abfrage im Abfragebereich des Dialogfelds **Dataseteigenschaften** aus. Weitere Informationen finden Sie im Artikel über [Berichtsdatasets (Berichts-Generator 3.0 und SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md).  
* Fügen Sie manuell Felder hinzu. Weitere Informationen finden Sie unter [Vorgehensweise: Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich (Berichts-Generator 3.0 und SSRS)](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).   
  
## <a name="see-also"></a>Siehe auch  
[Fehler und Ereignisse (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]




