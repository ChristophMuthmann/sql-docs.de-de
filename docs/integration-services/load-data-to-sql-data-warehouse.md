---
title: Laden von Daten aus SQL Server in Azure SQL Data Warehouse (SSIS) | Microsoft-Dokumentation
description: In diesem Artikel wird erläutert, wie ein SQL Server Integration Services-Paket (SSIS) erstellt wird, um Daten aus einer Vielzahl von Datenquellen in SQL Data Warehouse zu verschieben.
services: sql-data-warehouse
documentationcenter: NA
author: douglaslMS
manager: craigg-msft
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 04/04/2018
ms.author: douglasl
ms.openlocfilehash: 6be9111a29156c7bea74dc27bbb0ca5351259018
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="load-data-from-sql-server-to-azure-sql-data-warehouse-with-sql-server-integration-services-ssis"></a>Laden von Daten aus SQL Server in Azure SQL Data Warehouse mit SQL Server Integration Services (SSIS)

Erstellen Sie ein SQL Server Integration Services-Paket (SSIS), um Daten von SQL Server in [Azure SQL Data Warehouse](/azure/sql-data-warehouse/index.md) zu verschieben. Sie können die Daten optional umstrukturieren, transformieren und bereinigen, während diese den SSIS-Datenfluss durchlaufen.

In diesem Tutorial lernen Sie Folgendes:

* Erstellen Sie ein neues Integration Services-Projekt in Visual Studio.
* Stellen Sie eine Verbindung mit Datenquellen wie SQL Server (als Quelle) und SQL Data Warehouse (als Ziel) her.
* Entwerfen Sie ein SSIS-Paket, das Daten aus der Quelle in das Ziel lädt.
* Führen Sie das SSIS-Paket aus, um die Daten zu laden.

In diesem Tutorial wird SQL Server als Datenquelle verwendet. SQL Server kann auf lokalen Computern oder auf einem virtuellen Azure-Computer ausgeführt werden.

## <a name="basic-concepts"></a>Grundlegende Konzepte
Das Paket ist die Bereitstellungseinheit in SSIS. Zugehörige Pakete werden in Projekten gruppiert. Sie erstellen Projekte und entwerfen Pakete in Visual Studio mit SQL Server Data Tools. Der Entwurfsprozess ist ein visueller Prozess, bei dem Sie Komponenten per Drag & Drop aus der Toolbox auf die Entwurfsoberfläche ziehen, diese verbinden und ihre Eigenschaften festlegen. Wenn Sie das Paket fertiggestellt haben, können Sie es zur umfassenden Verwaltung, Überwachung und Sicherheit optional in SQL Server bereitstellen.

## <a name="options-for-loading-data-with-ssis"></a>Optionen zum Laden von Daten mit SSIS
SQL Server Integration Services (SSIS) ist eine vielseitige Gruppe von Tools, die eine große Bandbreite an Optionen bereitstellen, um eine Verbindung mit SQL Data Warehouse herzustellen und Daten zu laden.

1. Verwenden Sie ein ADO NET-Ziel, um eine Verbindung mit SQL Data Warehouse herzustellen. Dieses Tutorial verwendet ein ADO NET-Ziel, da es die wenigsten Konfigurationsoptionen enthält.
2. Verwenden Sie ein OLE DB-Ziel, um eine Verbindung mit SQL Data Warehouse herzustellen. Diese Option stellt möglicherweise eine etwas bessere Leistung bereit als das ADO NET-Ziel.
3. Verwenden Sie den Task „Azure-Blob hochladen“ zum Bereitstellen von Eingabedaten in den Azure Blob Storage. Starten Sie dann mithilfe des SSIS-Tasks „SQL ausführen“ ein PolyBase-Skript, das die Daten in SQL Data Warehouse lädt. Diese Option bietet unter den drei hier aufgeführten Optionen die beste Leistung. Um den Task „Azure-Blob hochladen“ abzurufen, laden Sie das [Microsoft SQL Server 2016 Integration Services Feature Pack für Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure] herunter. Weitere Informationen zu PolyBase finden Sie unter [PolyBase-Leitfaden][PolyBase Guide].

## <a name="before-you-start"></a>Vorbereitungen
Zum Durchlaufen dieses Tutorials benötigen Sie Folgendes:

1. **SQL Server Integration Services (SSIS)**. SSIS ist eine Komponente von SQL Server und erfordert eine Evaluierungsversion oder eine lizenzierte Version von SQL Server. Um eine Evaluierungsversion der Vorschauversion von SQL Server 2016 zu erhalten, lesen Sie [SQL Server-Evaluierungsversionen][SQL Server Evaluations].
2. **Visual Studio**. Die kostenlose Visual Studio Community Edition können Sie unter [Visual Studio Community][Visual Studio Community] abrufen.
3. **SQL Server Data Tools for Visual Studio (SSDT)**. Informationen zum Installieren von SQL Server Data Tools for Visual Studio finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Beispieldaten**. Dieses Tutorial verwendet als Quelldaten zum Laden in SQL Data Warehouse Beispieldaten, die in der AdventureWorks-Beispieldatenbank in SQL Server gespeichert sind. Weitere Informationen zum Abrufen der AdventureWorks-Beispieldatenbank finden Sie in den [AdventureWorks 2014-Beispieldatenbanken][AdventureWorks 2014 Sample Databases].
5. **Eine SQL Data Warehouse-Datenbank und Berechtigungen**. In diesem Tutorial stellen Sie eine Verbindung mit einer SQL Data Warehouse-Instanz her und laden Daten in diese. Sie benötigen Berechtigungen zum Erstellen einer Tabelle und zum Laden von Daten.
6. **Eine Firewallregel**. Sie müssen eine Firewallregel für SQL Data Warehouse mit der IP-Adresse Ihres lokalen Computers erstellen, bevor Sie Daten in SQL Data Warehouse hochladen können.

## <a name="step-1-create-a-new-integration-services-project"></a>Schritt 1: Erstellen eines neuen Integration Services-Projekts
1. Starten Sie Visual Studio.
2. Wählen Sie im Menü **Datei** die Option **Neu | Projekt** aus.
3. Navigieren Sie zu den Projekttypen **Installiert | Vorlagen | Business Intelligence | Integration Services**.
4. Wählen Sie ein **Integration Services-Projekt** aus. Geben Sie Werte für **Name** und **Speicherort** ein, und klicken Sie dann auf **OK**.

Visual Studio wird geöffnet und erstellt ein neues Integration Services-Projekt (SSIS). Dann öffnet Visual Studio den Designer für das neue SSIS-Paket (Package.dtsx) im Projekt. Die folgenden Bildschirmbereiche werden angezeigt:

* Auf der linken Seite befindet sich die **Toolbox** der SSIS-Komponenten.
* In der Mitte befindet sich die Entwurfsoberfläche mit mehreren Registerkarten. In der Regel verwenden Sie mindestens die Registerkarten **Ablaufsteuerung** und **Datenfluss**.
* Auf der rechten Seite befinden sich die Bereiche **Projektmappen-Explorer** und **Eigenschaften**.
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a>Schritt 2: Erstellen des grundlegenden Datenflusses
1. Ziehen Sie einen Datenflusstask aus der Toolbox in die Mitte der Entwurfsoberfläche (auf der Registerkarte **Ablaufsteuerung**).
   
    ![][02]
2. Doppelklicken Sie auf den Datenflusstask, um zur Registerkarte „Datenfluss“ zu wechseln.
3. Ziehen Sie aus der Liste „Andere Quellen“ in der Toolbox eine ADO.NET-Quelle auf die Entwurfsoberfläche. Ändern Sie mit noch ausgewähltem Quelladapter den Namen im Bereich **Eigenschaften** in **SQL Server-Quelle**.
4. Ziehen Sie aus der Liste „Andere Ziele“ in der Toolbox ein ADO.NET-Ziel auf die Entwurfsoberfläche unter der ADO NET-Quelle. Ändern Sie mit noch ausgewähltem Zieladapter den Namen im Bereich **Eigenschaften** in **SQL DW-Ziel**.
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a>Schritt 3: Konfigurieren des Quelladapters
1. Doppelklicken Sie auf den Quelladapter, um den **ADO.NET-Quellen-Editor** zu öffnen.
   
    ![][03]
2. Klicken Sie im **ADO.NET-Quellen-Editor** auf der Registerkarte **Verbindungs-Manager** auf die Schaltfläche **Neu** neben der Liste **ADO.NET-Verbindungs-Manager**, um das Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** zu öffnen. Nehmen Sie dann Verbindungseinstellungen für die SQL Server-Datenbank vor, von der in diesem Tutorial Daten geladen werden.
   
    ![][04]
3. Klicken Sie im Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** auf die Schaltfläche **Neu**, um das Dialogfeld **Verbindungs-Manager** zu öffnen, und erstellen Sie eine neue Datenverbindung.
   
    ![][05]
4. Führen Sie im Dialogfeld **Verbindungs-Manager** folgende Schritte durch:
   
   1. Wählen Sie als **Anbieter** den SqlClient-Datenanbieter aus.
   2. Geben Sie für **Servernamen** den SQL Server-Namen ein.
   3. Wählen Sie im Abschnitt **Beim Server anmelden** die Authentifizierungsinformationen aus, oder geben Sie sie ein.
   4. Wählen Sie im Abschnitt **Mit Datenbank verbinden** die AdventureWorks-Beispieldatenbank aus.
   5. Klicken Sie auf **Verbindung testen**.
      
       ![][06]
   6. Klicken Sie im Dialogfeld, in dem die Ergebnisse des Verbindungstests gemeldet werden, auf **OK**, um zum Dialogfeld **Verbindungs-Manager** zurückzukehren.
   7. Klicken Sie im Dialogfeld **Verbindungs-Manager** auf **OK**, um zum Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** zurückzukehren.
5. Klicken Sie im Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** auf **OK**, um zum **ADO.NET-Quellen-Editor** zurückzukehren.
6. Wählen Sie im **ADO.NET-Quellen-Editor** in der Liste **Name der Tabelle oder Sicht** die Tabelle **Sales.SalesOrderDetail** aus.
   
    ![][07]
7. Klicken Sie auf **Vorschau**, um die ersten 200 Datenzeilen in der Quelltabelle im Dialogfeld **Vorschau der Abfrageergebnisse anzeigen** anzuzeigen.
   
    ![][08]
8. Klicken Sie im Dialogfeld **Vorschau der Abfrageergebnisse anzeigen** auf **Schließen**, um zum **ADO.NET-Quellen-Editor** zurückzukehren.
9. Klicken Sie im **ADO.NET-Quellen-Editor** auf **OK**, um die Konfiguration der Datenquelle abzuschließen.

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a>Schritt 4: Herstellen einer Verbindung zwischen dem Quell- und Zieladapter
1. Wählen Sie den Quelladapter auf der Entwurfsoberfläche aus.
2. Wählen Sie den blauen Pfeil aus, der vom Quelladapter ausgeht, und ziehen Sie ihn zum Ziel-Editor, bis dieser fest positioniert ist.
   
    ![][10]
   
    Bei einem typischen SSIS-Paket verwenden Sie eine Reihe von anderen Komponenten von der SSIS-Toolbox zwischen Quelle und Ziel, um Ihre Daten beim Durchlaufen durch den SSIS-Datenfluss umzustrukturieren, zu transformieren und zu bereinigen. Um dieses Beispiel so einfach wie möglich zu halten, stellen wir eine direkte Verbindung zwischen Quelle und Ziel her.

## <a name="step-5-configure-the-destination-adapter"></a>Schritt 5: Konfigurieren des Zieladapters
1. Doppelklicken Sie auf den Zieladapter, um den **ADO.NET-Ziel-Editor** zu öffnen.
   
    ![][11]
2. Klicken Sie im **ADO.NET-Ziel-Editor** auf der Registerkarte **Verbindungs-Manager** auf die Schaltfläche **Neu** neben der Liste **Verbindungs-Manager**, um das Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** zu öffnen. Nehmen Sie dann Verbindungseinstellungen für die Azure SQL Data Warehouse-Datenbank vor, in die in diesem Tutorial Daten geladen werden.
3. Klicken Sie im Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** auf die Schaltfläche **Neu**, um das Dialogfeld **Verbindungs-Manager** zu öffnen, und erstellen Sie eine neue Datenverbindung.
4. Führen Sie im Dialogfeld **Verbindungs-Manager** folgende Schritte durch:
   1. Wählen Sie als **Anbieter** den SqlClient-Datenanbieter aus.
   2. Geben Sie für **Servername** den Namen von SQL Data Warehouse an.
   3. Wählen Sie im Abschnitt **Beim Server anmelden** die Option **SQL Server-Authentifizierung verwenden** aus, und geben Sie die Authentifizierungsinformationen ein.
   4. Wählen Sie im Abschnitt **Mit Datenbank verbinden** eine vorhandene SQL Data Warehouse-Datenbank aus.
   5. Klicken Sie auf **Verbindung testen**.
   6. Klicken Sie im Dialogfeld, in dem die Ergebnisse des Verbindungstests gemeldet werden, auf **OK**, um zum Dialogfeld **Verbindungs-Manager** zurückzukehren.
   7. Klicken Sie im Dialogfeld **Verbindungs-Manager** auf **OK**, um zum Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** zurückzukehren.
5. Klicken Sie im Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** auf **OK**, um zum **ADO.NET-Ziel-Editor** zurückzukehren.
6. Klicken Sie im **ADO.NET-Ziel-Editor** neben der Liste **Tabelle oder Sicht verwenden** auf **Neu**, um das Dialogfeld **Tabelle erstellen** zu öffnen, um eine neue Zieltabelle mit einer Spaltenliste zu erstellen, die der Quelltabelle entspricht.
   
    ![][12a]
7. Führen Sie im Dialogfeld **Tabelle erstellen** die folgenden Schritte aus:
   
   1. Ändern Sie den Namen der Zieltabelle in **SalesOrderDetail**.
   2. Entfernen Sie die Spalte **rowguid**. Der Datentyp **uniqueidentifier** wird nicht in SQL Data Warehouse unterstützt.
   3. Ändern Sie den Datentyp der Spalte **LineTotal** in **money**. Der Datentyp **decimal** wird nicht in SQL Data Warehouse unterstützt. Informationen zu unterstützten Datentypen finden Sie unter [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Klicken Sie auf **OK**, um die Tabelle zu erstellen und zum **ADO.NET-Ziel-Editor** zurückzukehren.
8. Wählen Sie im **ADO.NET-Ziel-Editor** die Registerkarte **Zuordnungen** aus, um festzustellen, wie Spalten in der Quelle denen im Ziel zugeordnet werden.
   
    ![][13]
9. Klicken Sie auf **OK**, um die Konfiguration der Datenquelle abzuschließen.

## <a name="step-6-run-the-package-to-load-the-data"></a>Schritt 6: Ausführen des Pakets zum Laden der Daten
Führen Sie das Paket aus, indem Sie auf der Symbolleiste auf die Schaltfläche **Starten** klicken oder im Menü **Debuggen** eine der Optionen **Ausführen** auswählen.

Wenn die Paketausführung beginnt, sehen Sie gelbe sich drehende Räder, die auf laufende Aktivität hinweisen, sowie die Anzahl der bisher verarbeiteten Zeilen.

![][14]

Wenn die Ausführung des Pakets abgeschlossen ist, sehen Sie grüne Häkchen, die auf ihre erfolgreiche Ausführung hinweisen, sowie die Gesamtanzahl der Datenzeilen, die von der Quelle in das Ziel geladen wurden.

![][15]

Gratulation! Sie haben mit SQL Server Integration Services erfolgreich Daten in Azure SQL Data Warehouse geladen.

## <a name="next-steps"></a>Nächste Schritte
* Erfahren Sie mehr über den SSIS-Datenfluss. Beginnen Sie hier: [Datenfluss][Data Flow].
* Erfahren Sie mehr über das Debuggen und Behandeln von Problemen mit Ihren Paketen direkt in der Entwurfsumgebung. Legen Sie hiermit los: [Tools zur Problembehandlung für die Paketentwicklung][Troubleshooting Tools for Package Development].
* Erfahren Sie, wie Sie Ihre SSIS-Projekte und -Pakete in Integration Services Server oder an einem anderen Speicherort bereitstellen. Legen Sie hiermit los: [Bereitstellung von Projekten und Paketen][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/load-data-to-sql-data-warehouse/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-data-warehouse/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-data-warehouse/test-connection-06.png
[07]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-data-warehouse/preview-data-08.png
[09]:  ./media/load-data-to-sql-data-warehouse/source-destination-09.png
[10]:  ./media/load-data-to-sql-data-warehouse/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-data-warehouse/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-data-warehouse/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-data-warehouse/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-data-warehouse/column-mapping-13.png
[14]:  ./media/load-data-to-sql-data-warehouse/package-running-14.png
[15]:  ./media/load-data-to-sql-data-warehouse/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: ../relational-databases/polybase/polybase-guide.md
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: ../t-sql/statements/create-table-azure-sql-data-warehouse.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
