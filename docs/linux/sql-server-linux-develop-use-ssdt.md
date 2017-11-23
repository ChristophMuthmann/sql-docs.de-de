---
title: "Entwickeln und Bereitstellen von SQL Server-Datenbanken für Linux | Microsoft Docs"
description: 
author: erickangMSFT
ms.author: erickang
manager: jroth
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.custom: 
ms.workload: On Demand
ms.openlocfilehash: 91ab1a812b55c84e3b55c439290d247df91eea40
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Verwenden Sie Visual Studio zum Erstellen von Datenbanken für SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server Data Tools (SSDT) wandelt Visual Studio in eine leistungsstarke Entwicklungs- und Datenbank Lifecycle Management (DLM)-Umgebung, für die SQL Server on Linux. Sie können entwickeln, erstellen, testen und Ihre Datenbank aus einem Projekt quellcodeverwaltete veröffentlichen, wie Sie den Anwendungscode entwickeln.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Visual Studio und SQL Server Datatools installieren

1. Wenn Sie nicht bereits Visual Studio auf Ihrem Windows-Computer installiert haben [herunterladen und installieren Sie Visual Studio]. Wenn Sie nicht über eine Visual Studio-Lizenz verfügen, wird Visual Studio Community Edition ist eine kostenlose, vollständig ausgestatteten IDE für Studenten, Open Source- und einzelne Entwickler.

2. Wählen Sie während der Installation von Visual Studio **benutzerdefinierte** für die **wählen Sie die Installationsart** Option. Klicken Sie auf **Weiter**.

3. Wählen Sie **Microsoft SQL Server Data Tools**, **Git für Windows**, und **GitHub-Erweiterung für Visual Studio** aus der Auswahlliste der Funktion.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Den Vorgang fortzusetzen Sie, und schließen Sie die Installation von Visual Studio. Es kann einige Minuten dauern.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>Aktualisieren von SQL Server Data Tools auf SSDT 17,0 RC-Version

SQL Server-2017 unter Linux wird von SSDT-Version 17,0 RC oder höher unterstützt.

* [Herunterladen und installieren Sie SSDT 17,0 RC2](https://go.microsoft.com/fwlink/?linkid=837939).

## <a name="create-a-new-database-project-in-source-control"></a>Erstellen eines neuen Datenbankprojekts in der quellcodeverwaltung

1. Starten Sie Visual Studio.

2. Wählen Sie **Team Explorer** auf die **Ansicht** Menü. 

3. Klicken Sie auf **neu** in **lokales Git-Repository** Abschnitt der **verbinden** Seite.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. Klicken Sie auf **Erstellen**. Nachdem die lokale Git-Repository erstellt wurde, doppelklicken klicken Sie auf **SSDTRepo**.

4. Klicken Sie auf **neu** in der **Lösungen** Abschnitt. Wählen Sie **SQL Server** unter **andere Sprachen** Knoten in der **neues Projekt** Dialogfeld.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. Geben Sie in **TutorialDB** für den Namen und klicken Sie auf **OK** um ein neues Datenbankprojekt zu erstellen.

## <a name="create-a-new-table-in-the-database-project"></a>Erstellen Sie eine neue Tabelle im Datenbankprojekt

1. Wählen Sie **Projektmappen-Explorer** auf die **Ansicht** Menü.

2. Öffnen Sie im Menü des Datenbank-Projekt, indem Sie mit der rechten Maustaste auf **TutorialDB** im Projektmappen-Explorer.

3. Wählen Sie **Tabelle** unter **hinzufügen**.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. Fügen Sie mithilfe des Tabellen-Designer zwei Spalten, Name `nvarchar(50)` und den Speicherort `nvarchar(50)`, wie in der Abbildung dargestellt. SSDT generiert die `CREATE TABLE` wie Sie die Spalten in den Designer fügen ein Skript.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. Speichern Sie die **Table1.sql** Datei.

## <a name="build-and-validate-the-database"></a>Erstellen Sie und überprüfen Sie die Datenbank

1. Öffnen Sie im Menü des Datenbank-Projekt auf **TutorialDB** , und wählen Sie **erstellen**. SSDT SQL Quellcodedateien im Projekt kompiliert und erstellt eine Datenebenen-Paketdatei (DACPAC-Datei). Dies kann zum Veröffentlichen einer Datenbank in Ihrer 2017 von SQL Server-Instanz unter Linux verwendet werden. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Erfolg Buildmeldung Einchecken **Ausgabe** Fenster in Visual Studio. 

## <a name="publish-the-database-to-sql-server-2017-instance-on-linux"></a>Veröffentlichen der Datenbank auf 2017 von SQL Server-Instanz unter Linux

1. Öffnen Sie im Menü des Datenbank-Projekt auf **TutorialDB** , und wählen Sie **veröffentlichen**.

2. Klicken Sie auf **bearbeiten** , wählen Sie die SQL Server-Instanz unter Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. Klicken Sie im Dialogfeld "Verbindung" Geben Sie in der IP-Adresse oder den Hostnamen der Name Ihrer SQL Server-Instanz unter Linux, Benutzername und Kennwort.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. Klicken Sie auf die **veröffentlichen** Schaltfläche auf das Dialogfeld "Veröffentlichen".

5. Überprüfen des Veröffentlichungsstatus der **Datentoolvorgänge** Fenster.

6. Klicken Sie auf **Ansicht Reulst** oder **Skript anzeigen** auf Details zu den Editions veröffentlichen Ergebnis auf dem SQL Server unter Linux finden Sie unter.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Sie haben erfolgreich eine neue Datenbank auf SQL Server-Instanz unter Linux erstellt und die Grundlagen des Entwickelns von einer Datenbank mit einem Datenbankprojekt quellcodeverwaltete gelernt.

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie noch nicht in T-SQL vertraut sind, finden Sie unter [Lernprogramm: Schreiben von Transact-SQL-Anweisungen] und [Transact-SQL-Referenz (Datenbankmodul)].

Weitere Informationen zum Entwickeln von einer Datenbank mit SQL Data Tools finden Sie unter [SSDT MSDN-Dokumente]

[herunterladen und installieren Sie Visual Studio]:https://www.visualstudio.com/downloads/
[Download and Install SSDT 17.0 RC2]:https://aka.ms/ssdt-download
[SSDT MSDN-Dokumente]: https://msdn.microsoft.com/en-us/library/hh272686(v=vs.103).aspx
[Lernprogramm: Schreiben von Transact-SQL-Anweisungen]:https://msdn.microsoft.com/library/ms365303.aspx
[Transact-SQL-Referenz (Datenbankmodul)]:https://msdn.microsoft.com/library/bb510741.aspx
