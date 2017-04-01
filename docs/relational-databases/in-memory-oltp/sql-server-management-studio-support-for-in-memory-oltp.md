---
title: "SQL Server Management Studio-Unterst&#252;tzung f&#252;r In-Memory OLTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee847b5f-6a1a-448e-a746-d61a023881ff
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# SQL Server Management Studio-Unterst&#252;tzung f&#252;r In-Memory OLTP
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ist eine integrierte Umgebung für das Verwalten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Infrastruktur. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] werden Tools zum Konfigurieren, Überwachen und Verwalten von Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [SQL Server Management Studio](../Topic/SQL%20Server%20Management%20Studio.md).  
  
 In den Tasks in diesem Thema wird beschrieben, wie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwendet wird, um speicheroptimierte Tabellen, Indizes für speicheroptimierte Tabellen, systemintern kompilierte gespeicherte Prozeduren und benutzerdefinierte speicheroptimierte Tabellentypen zu verwalten.  
  
 Informationen zum programmgesteuerten Erstellen speicheroptimierter Tabellen finden Sie unter [Erstellen einer speicheroptimierten Tabelle und einer systemintern kompilierten gespeicherten Prozedur](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
### So erstellen Sie eine Datenbank mit einer speicheroptimierten Datendateigruppe  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmoduls her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Datenbanken**, und klicken Sie dann auf **Neue Datenbank**.  
  
3.  Klicken Sie zum Hinzufügen einer neuen speicheroptimierten Datendateigruppe auf die Seite **Dateigruppen**. Klicken Sie unter **MEMORY OPTIMIZED DATA** auf **Dateigruppe hinzufügen**, und geben Sie dann den Namen der speicheroptimierten Datendateigruppe ein.  Die Spalte mit der Bezeichnung **FILESTREAM-Dateien** stellt die Anzahl der Container in der Dateigruppe dar. Container werden auf der Seite **Allgemein** hinzugefügt.  
  
4.  Um der Dateigruppe eine Datei (Container) hinzuzufügen, klicken Sie auf die Seite **Allgemein**. Klicken Sie unter **Datenbankdateien**auf **Hinzufügen**. Wählen Sie als **Dateityp** **FILESTREAM-Daten** aus, geben Sie den logischen Namen des Containers an, wählen Sie die speicheroptimierte Dateigruppe aus, und stellen Sie sicher, dass **Automatische Vergrößerung/Maximale Größe** auf **Unbegrenzt** festgelegt ist.  
  
     Weitere Informationen zum Erstellen einer neuen Datenbank mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] finden Sie unter [Erstellen einer Datenbank](../../relational-databases/databases/create-a-database.md).  
  
### So erstellen Sie eine speicheroptimierte Tabelle  
  
1.  Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf den Datenbankknoten **Tabellen**, klicken Sie auf **Neu** und dann auf **Speicheroptimierte Tabelle**.  
  
     Eine Vorlage zum Erstellen von speicheroptimierten Tabellen wird angezeigt.  
  
2.  Um die Vorlagenparameter zu ersetzen, klicken Sie auf **Werte für Vorlagenparameter angeben** im Menü **Abfrage** .  
  
     Weitere Informationen zur Verwendung von Vorlagen finden Sie unter [Template Explorer](../../ssms/template/template-explorer.md).  
  
3.  Im **Objekt-Explorer** werden Tabellen zuerst nach datenträgerbasierten Tabellen und dann nach speicheroptimierten Tabellen angeordnet. Verwenden Sie **Details zum Objekt-Explorer** , um alle Tabellen nach dem Namen geordnet anzuzeigen.  
  
### So erstellen Sie eine systemintern kompilierte gespeicherte Prozedur  
  
1.  Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf den Datenbankknoten **Gespeicherte Prozeduren**, klicken Sie auf **Neu** und dann auf **Systemintern kompilierte gespeicherte Prozedur**.  
  
     Eine Vorlage zum Erstellen von systemintern kompilierten gespeicherten Prozeduren wird angezeigt.  
  
2.  Um die Vorlagenparameter zu ersetzen, klicken Sie auf **Werte für Vorlagenparameter angeben** im Menü **Abfrage**.  
  
     Weitere Informationen zum Erstellen einer neuen gespeicherten Prozedur finden Sie unter [Create a Stored Procedure](../../relational-databases/stored-procedures/create-a-stored-procedure.md).  
  
### So erstellen Sie einen benutzerdefinierten speicheroptimierten Tabellentyp  
  
1.  Erweitern Sie im **Objekt-Explorer** den Datenbankknoten **Typen**, klicken Sie mit der rechten Maustaste auf den Knoten **Benutzerdefinierte Tabellentypen,** klicken Sie auf **Neu** und anschließend auf **Benutzerdefinierter speicheroptimierter Tabellentyp**.  
  
     Es wird eine Vorlage zum Erstellen eines benutzerdefinierten speicheroptimierten Tabellentyps angezeigt.  
  
2.  Um die Vorlagenparameter zu ersetzen, klicken Sie auf **Werte für Vorlagenparameter angeben** im Menü **Abfrage** .  
  
     Weitere Informationen zum Erstellen einer neuen gespeicherten Prozedur finden Sie unter [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md).  
  
## Arbeitsspeicher-Überwachung  
  
#### Anzeigen der Speicherauslastung durch den Bericht für speicheroptimierte Objekte  
  
-   Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf die Datenbank, klicken Sie auf **Berichte**, auf **Standardberichte** und dann auf **Speicherauslastung nach speicheroptimierten Objekten**.  
  
     Dieser Bericht stellt detaillierte Daten zur Verwendung des Speicherplatzes durch speicheroptimierte Objekte in der Datenbank bereit.  
  
#### Anzeigen von Eigenschaften für zugeordneten und verwendeten Arbeitsspeicher für eine Tabelle oder eine Datenbank  
  
1.  So erhalten Sie Informationen zur Speicherauslastung:  
  
    -   Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf die speicheroptimierte Tabelle, klicken Sie auf **Eigenschaften** und dann auf die Seite **Speicher**. Der Wert für die Eigenschaft **Datenspeicher** gibt die Menge an Arbeitsspeicher an, die durch die Daten in der Tabelle verwendet wird. Der Wert für die Eigenschaft **Indexspeicher** gibt den Arbeitsspeicher an, der von Indizes in der Tabelle verwendet wird.  
  
    -   Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf die Datenbank, klicken Sie auf **Eigenschaften** und dann auf die Seite **Allgemein**. Der Wert für die Eigenschaft **Speicheroptimierten Objekten zugewiesener Arbeitsspeicher** gibt den Arbeitsspeicher an, der speicheroptimierten Objekten in der Datenbank zugeordnet ist. Der Wert für die Eigenschaft **Von speicheroptimierten Objekten genutzter Arbeitsspeicher** gibt den Arbeitsspeicher an, der von speicheroptimierten Objekten in der Datenbank verwendet wird.  
  
## Unterstützte Funktionen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] unterstützt Funktionen und Vorgänge, die vom Datenbankmodul in Datenbanken mit speicheroptimierten Datendateigruppen, speicheroptimierten Tabellen, Indizes und systemintern kompilierten gespeicherten Prozeduren unterstützt werden.  
  
 Für Datenbank-, Tabellen-, gespeicherte Prozedur-, benutzerdefinierte Tabellentyp- oder Indexobjekte wurden die folgenden [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]-Funktionen aktualisiert oder erweitert, um In-Memory OLTP zu unterstützen.  
  
-   Objekt-Explorer  
  
    -   Kontextmenüs  
  
    -   Filtereinstellungen  
  
    -   Script As  
  
    -   Aufgaben  
  
    -   Berichte  
  
    -   Eigenschaften  
  
    -   Datenbankaufgaben:  
  
        -   Anfügen und Trennen einer Datenbank, die speicheroptimierte Tabellen enthält.  
  
             Die speicheroptimierte Datendateigruppe wird auf der Benutzeroberfläche **Datenbanken anfügen** nicht angezeigt. Die Datenbank wird jedoch ordnungsgemäß angefügt, wenn Sie das Anfügen der Datenbank fortsetzen.  
  
            > [!NOTE]  
            >  Wenn Sie eine Datenbank, die über einen Container mit einer speicheroptimierten Datendateigruppe verfügt, unter Verwendung von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] anfügen möchten und der Container der speicheroptimierten Datendateigruppe der Datenbank auf einem anderen Computer erstellt wurde, muss der Speicherort des Containers der speicheroptimierten Datendateigruppe auf beiden Computern identisch sein. Wenn Sie für den Container der speicheroptimierten Datendateigruppe der Datenbank auf dem neuen Computer einen anderen Speicherort verwenden möchten, können Sie die Datenbank mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)] anfügen. Im folgenden Beispiel lautet der Speicherort des Containers der speicheroptimierten Datendateigruppe auf dem neuen Computer C:\Folder2. Als der Container der speicheroptimierten Datendateigruppe auf dem ersten Computer erstellt wurde, lautete der Speicherort jedoch C:\Folder1.  
            >   
            >  `CREATE DATABASE[imoltp] ON`  
            >   
            >  `(NAME =N'imoltp',FILENAME=N'C:\Folder2\imoltp.mdf'),`  
            >   
            >  `(NAME =N'imoltp_mod1',FILENAME=N'C:\Folder2\imoltp_mod1'),`  
            >   
            >  `(NAME =N'imoltp_log',FILENAME=N'C:\Folder2\imoltp_log.ldf')`  
            >   
            >  `FOR ATTACH`  
            >   
            >  `GO`  
  
        -   Generieren von Skripts.  
  
             Im **Assistenten zum Generieren und Veröffentlichen von Skripts**lautet der Standardwert für die Skriptoption **Vorhandensein von Objekten überprüfen** FALSE. Wenn der Wert der Skriptoption **Vorhandensein von Objekten überprüfen** im Bildschirm **Skripterstellungsoptionen festlegen** des Assistenten auf TRUE festgelegt ist, würde das generierte Skript „CREATE PROCEDURE <Prozedurname> AS“ und „ALTER PROCEDURE <Prozedurname> <Prozedurdefinition>“ enthalten. Bei der Ausführung gibt das generierte Skript einen Fehler zurück, da ALTER PROCEDURE bei systemintern kompilierten gespeicherten Prozeduren nicht unterstützt wird.  
  
             So ändern Sie das generierte Skript für jede systemintern kompilierte gespeicherte Prozedur  
  
            1.  Ersetzen Sie "AS" in "CREATE PROCEDURE <procedure_name> AS" durch "<procedure_definition>".  
  
            2.  Löschen Sie "ALTER PROCEDURE <procedure_name> <procedure_definition>".  
  
        -   Kopieren von Datenbanken. Bei Datenbanken mit speicheroptimierten Objekten werden die Erstellung der Datenbank auf dem Zielserver und die Übertragung von Daten nicht in einer Transaktion ausgeführt.  
  
        -   Importieren und Exportieren von Daten. Verwenden Sie die Option **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import/Export-Assistent > Daten aus mindestens einer Tabelle oder Sicht** kopieren. Wenn die Zieltabelle eine speicheroptimierte Tabelle ist, die nicht in der Zieldatenbank vorhanden ist:  
  
            1.  Wählen Sie im **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import/Export-Assistent**im Bildschirm **Tabelle kopieren oder Datenbank abfragen** die Option **Daten aus mindestens einer Tabelle oder Sicht kopieren**aus. Klicken Sie dann auf **Weiter**.  
  
            2.  Klicken Sie auf **Zuordnungen bearbeiten**. Wählen Sie anschließend **Zieltabelle erstellen** aus, und klicken auf **SQL bearbeiten**. Geben Sie die CREATE TABLE-Syntax zum Erstellen einer speicheroptimierten Tabelle in der Zieldatenbank ein. Klicken Sie auf **OK** , und schließen Sie die restlichen Schritte des Assistenten ab.  
  
        -   Wartungspläne. Die Wartungsaufgaben "Index neu organisieren" und "Index neu erstellen" werden in speicheroptimierten Tabellen und deren Indizes nicht unterstützt. Wenn ein Wartungsplan zur Neuerstellung und Neuorganisation des Indexes ausgeführt wird, werden die speicheroptimierten Tabellen und deren Indizes in den ausgewählten Datenbanken daher ausgelassen.  
  
             Der Wartungstask Statistiken aktualisieren wird für Stichprobenscans von speicheroptimierten Tabellen und deren Indizes nicht unterstützt. Wenn also ein Wartungsplan für Statistiken aktualisieren ausgeführt wird, werden die Statistiken für speicheroptimierte Tabellen und deren Indizes immer auf **WITH FULLSCAN, NORECOMPUTE** aktualisiert.  
  
-   Bereich mit Details zum Objekt-Explorer  
  
-   Vorlagen-Explorer  
  
## Nicht unterstützte Funktionen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 Für In-Memory OLTP-Objekte unterstützt [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] keine Funktionen und Vorgänge, die auch nicht vom Datenbankmodul unterstützt werden.  
  
 Weitere Informationen zu nicht unterstützten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen finden Sie unter [Nicht unterstützte SQL Server-Funktionen für In-Memory OLTP](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md).  
  
## Siehe auch  
 [SQL Server-Unterstützung für In-Memory OLTP](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  