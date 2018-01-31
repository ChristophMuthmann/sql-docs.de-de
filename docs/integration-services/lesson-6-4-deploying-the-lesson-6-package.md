---
title: 'Schritt 4: Bereitstellen des Pakets aus Lektion 6 | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e3a8947b1212aafe5fb3d233400900ab320a80f6
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-6-4---deploying-the-lesson-6-package"></a>Lektion 6-4 – Bereitstellen des Pakets aus Lektion 6
Zum Bereitstellen des Pakets muss das Paket dem SSISDB-Katalog in Integration Services in einer Instanz von SQL Server hinzugefügt werden. In dieser Lektion werden Sie dem SSISDB-Katalog das Paket aus Lektion 6 hinzufügen, den Parameter festlegen und das Paket ausführen. Für diese Lektion werden Sie mithilfe von SQL Server Management Studio dem SSISDB-Katalog das Paket aus Lektion 6 hinzufügen und das Paket bereitstellen. Nach dem Bereitstellen des Pakets, ändern Sie den Parameter, um auf einen neuen Speicherort zu verweisen, und führen dann das Paket aus.  
  
In dieser Lektion führen Sie die folgenden Aktionen aus:  
  
-   Hinzufügen des Pakets zum SSISDB-Katalog im SSIS-Knoten in SQL Server.  
  
-   Bereitstellen des Pakets.  
  
-   Festlegen des Paketparameterwerts.  
  
-   Ausführen des Pakets in SSMS.  
  
### <a name="to-locate-or-add-the-the-ssisdb-catalog"></a>So suchen Sie den SSISDB-Katalog oder fügen ihn hinzu  
  
1.  Klicken Sie auf "Start", zeigen Sie auf "Alle Programme" und auf "Microsoft SQL Server 2012", und klicken Sie anschließend auf "SQL Management Studio".  
  
2.  Überprüfen Sie im Dialogfeld "Verbindung mit dem Server herstellen" die Standardeinstellungen, und klicken Sie dann auf "Verbinden". Damit die Verbindung hergestellt werden kann, muss das Feld "Servername" den Namen des Computers enthalten, auf dem SQL Server installiert ist. Wenn es sich beim Datenbankmodul um eine benannte Instanz handelt, sollte das Feld „Servername“ zudem den Instanznamen im Format <Computername>\\<Instanzname> enthalten.  
  
3.  Erweitern Sie im Objekt-Explorer "Integration Services-Kataloge".  
  
4.  Wenn unter "Integration Services-Kataloge" keine Kataloge aufgeführt sind, fügen Sie dann den SSISDB-Katalog hinzu.  
  
5.  Um den SSISDB-Katalog hinzuzufügen, klicken Sie mit der rechten Maustaste auf "Integration Services-Kataloge", und klicken Sie dann auf "Katalog erstellen".  
  
6.  Wählen Sie im Dialogfeld "Katalog erstellen" die Option "CLR-Integration aktivieren" aus.  
  
7.  Geben Sie im Feld "Kennwort" ein neues Kennwort ein, und geben Sie es erneut im Feld "Kennwort erneut eingeben" ein. Achten Sie darauf, dass Sie das eingegebene Kennwort nicht vergessen.  
  
8.  Klicken Sie auf "OK", um den SSISDB-Katalog hinzuzufügen.  
  
### <a name="to-add-the-package-to-the-ssisdb-catalog"></a>So fügen Sie das Paket dem SSISDB-Katalog hinzu  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf "SSISDB", und klicken Sie auf "Ordner erstellen".  
  
2.  Geben Sie im Dialogfeld "Ordner erstellen" in das Feld "Ordnername" den Namen "SSIS-Lernprogramm" ein, und klicken Sie auf "OK".  
  
3.  Erweitern Sie den Ordner "SSIS-Lernprogramm", klicken Sie mit der rechten Maustaste auf "Projekte" und dann auf "Pakete importieren".  
  
4.  Klicken Sie auf der Seite "Einführung" des Assistenten zum Konvertieren von Integration Services-Projekten auf "Weiter".  
  
5.  Stellen Sie auf der Seite "Pakete suchen" sicher, dass das Dateisystem in der Liste "Quelle" ausgewählt ist, und klicken Sie auf "Durchsuchen".  
  
6.  Navigieren Sie im Dialogfeld "Nach Ordner suchen" zum Ordner mit dem Projekt "SSIS-Lernprogramm", und klicken Sie dann auf "OK".  
  
7.  Klicken Sie auf Weiter.  
  
8.  Auf der Seite "Pakete auswählen" sollten alle sechs Pakete aus dem SSIS-Lernprogramm angezeigt werden. Wählen Sie in der Liste "Pakete" die Datei "Lektion 6.dtsx" aus, und klicken Sie dann auf "Weiter".  
  
9. Geben Sie auf der Seite "Ziel auswählen" in das Feld "Projektname" "SSIS-Lernprogrammbereitstellung" ein, und klicken Sie auf "Weiter".  
  
10. Klicken Sie auf jedem der verbleibenden Seiten des Assistenten auf "Weiter", bis Sie zur Seite "Überprüfen" gelangen.  
  
11. Klicken Sie auf der Seite "Überprüfen" auf "Konvertieren".  
  
12. Wenn die Konvertierung abgeschlossen ist, klicken Sie auf "Schließen".  
  
Wenn Sie den Assistenten zum Konvertieren von Integration Services-Projekten schließen, zeigt SSIS den Bereitstellungs-Assistenten für Integration Services an. Verwenden Sie diesen Assistenten jetzt zur Bereitstellung des Pakets aus Lektion 6.  
  
1.  Überprüfen Sie auf der Seite "Einführung" des Bereitstellungs-Assistenten für Integration Services die Schritte zum Bereitstellen des Projekts, und klicken Sie dann auf "Weiter".  
  
2.  Stellen Sie auf der Seite "Ziel auswählen" sicher, dass der Servername die Instanz von SQL Server mit dem SSISDB-Katalog ist und dass der Pfad "SSIS-Lernprogrammbereitstellung" zeigt, und klicken Sie dann auf "Weiter".  
  
3.  Überprüfen Sie auf der Seite "Überprüfen" die Zusammenfassung, und klicken Sie auf "Bereitstellen".  
  
4.  Wenn die Bereitstellung abgeschlossen ist, klicken Sie auf "Schließen".  
  
5.  Klicken Sie mit der rechten Maustaste im Objekt-Explorer auf "Integration Services-Kataloge" und dann auf "Aktualisieren".  
  
6.  Erweitern Sie "Integration Services-Kataloge" und dann "SSISDB". Erweitern Sie weiterhin die Struktur unter "SSIS-Lernprogramm", bis Sie das Projekt vollständig erweitert haben. Unter dem Knoten "Pakete" des Knotens "SSIS-Lernprogrammbereitstellung" sollte "Lektion 6.dtsx" angezeigt werden.  
  
Um sicherzustellen, dass das Paket abgeschlossen ist, klicken Sie mit der rechten Maustaste auf "Lektion 6.dtsx", und klicken Sie auf "Konfigurieren". Wählen Sie im Dialogfeld "Konfigurieren" "Parameter" aus, und überprüfen Sie, ob es einen Eintrag mit "Lektion 6.dtsx" als Container, "VarFolderName" als Namen und dem Pfad zu "Neue Beispieldaten" als Wert vorhanden ist, und klicken Sie dann auf "Schließen".  
  
Erstellen Sie vor dem Fortfahren einen neuen Beispieldatenordner, geben Sie ihm den Namen "Beispieldaten Zwei", und kopieren Sie alle drei der ursprünglichen Beispieldateien hinein.  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>So erstellen und füllen Sie einen neuen Beispieldatenordner  
  
1.  Erstellen Sie im Windows-Explorer im Stammverzeichnis Ihres Laufwerks (beispielsweise C:\\) einen neuen Ordner mit dem Namen „Beispieldaten Zwei“.  
  
2.  Öffnen Sie den Ordner "C:\Programme\Microsoft SQL Server\110\Samples\Integration Services\Tutorial\Creating a Simple ETL Package\Sample Data", und kopieren Sie dann drei der Beispieldateien aus dem Ordner.  
  
3.  Fügen Sie die kopierten Dateien in den Ordner "Neue Beispieldaten" ein.  
  
### <a name="to-change-the-package-parameter-to-point-to-the-new-sample-data"></a>So ändern Sie den Paketparameter, um auf die neuen Beispieldaten zu verweisen  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf "Lektion 6.dtsx", und klicken Sie auf "Konfigurieren".  
  
2.  Ändern Sie im Dialogfeld "Konfigurieren" den Parameterwert in den Pfad zu "Beispieldaten Zwei". Zum Beispiel "C:\Beispieldaten Zwei", wenn Sie den neuen Ordner im Stammordner von Laufwerk C platziert haben.  
  
3.  Klicken Sie auf "OK", um das Dialogfeld "Konfigurieren" zu schließen.  
  
### <a name="to-test-the-lesson-6-package-deployment"></a>So testen Sie die Bereitstellung des Lektion 6-Pakets  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf "Lektion 6.dtsx", und klicken Sie auf "Ausführen".  
  
2.  Klicken Sie im Dialogfeld "Paket ausführen" auf "OK".  
  
3.  Klicken Sie im Dialogfeld "Meldung" auf "Ja", um den Übersichtsbericht zu öffnen.  
  
Der Übersichtsbericht für das Paket wird mit dem Namen des Pakets und einer Statusübersicht angezeigt. Der Abschnitt "Übersicht über die Ausführung" enthält das Ergebnis jeder Aufgabe im Paket, und der Abschnitt "Verwendete Parameter" zeigt die Namen und Werte aller Parameter an, die bei der Ausführung des Pakets verwendet werden, einschließlich "VarFolderName".  
  
  
  
