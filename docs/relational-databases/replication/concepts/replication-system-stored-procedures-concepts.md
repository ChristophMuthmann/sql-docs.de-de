---
title: Replication System Stored Procedures Concepts | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server replication], programming
- programming [SQL Server replication], system stored procedures
- programming interfaces [SQL Server replication]
- system stored procedures [SQL Server replication]
- replication [SQL Server], how-to topics
ms.assetid: 816d2bda-ed72-43ec-aa4d-7ee3dc25fd8a
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3385a4f63191544453f58829c1c55bed69b46421
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="replication-system-stored-procedures-concepts"></a>Replication System Stored Procedures Concepts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ermöglichen gespeicherte Systemprozeduren den programmgesteuerten Zugriff auf alle vom Benutzer konfigurierbaren Funktionen in einer Replikationstopologie. Gespeicherte Prozeduren können einzeln mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder dem sqlcmd-Befehlszeilenhilfsprogramm ausgeführt werden. Es ist jedoch nützlich, [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Skriptdateien zu schreiben, mit denen eine logische Sequenz von Replikationstasks ausgeführt werden können.  
  
 Skriptreplikationstasks bieten die folgenden Vorteile:  
  
-   Sie behalten eine dauerhafte Kopie der Schritte bei, die zum Bereitstellen der Replikationstopologie verwendet werden.  
  
-   Sie verwenden ein einzelnes Skript, um mehrere Abonnenten zu konfigurieren.  
  
-   Sie bieten neuen Datenbankadministratoren eine schnelle Einführung, da Skripts die Möglichkeiten zur Verfügung stellen, den Code auszuwerten, zu verstehen, zu ändern oder Probleme im Code zu finden und zu beheben.  
  
    > [!IMPORTANT]  
    >  Skripts können Quellen für Sicherheitsbeeinträchtigungen sein. Sie können Systemfunktionen ohne Wissen oder Eingriff des Benutzers aufrufen und Sicherheitsanmeldeinformationen im Nur-Text-Format enthalten. Überprüfen Sie Skripts auf Sicherheitsprobleme, bevor Sie sie verwenden.  
  
## <a name="creating-replication-scripts"></a>Erstellen von Replikationsskripts  
 Aus der Sicht der Replikation besteht ein Skript aus einer oder mehreren [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisungen, wobei jede Anweisung eine gespeicherte Replikationsprozedur ausführt. Skripts sind Textdateien, die meist die Dateierweiterung SQL aufweisen und mit dem sqlcmd-Hilfsprogramm ausgeführt werden können. Beim Ausführen einer Skriptdatei führt das Hilfsprogramm die in der Datei gespeicherten SQL-Anweisungen aus. Entsprechend kann ein Skript als Abfrageobjekt in einem [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]-Projekt gespeichert werden.  
  
 Replikationsskripts können wie folgt erstellt werden:  
  
-   Erstellen Sie das Skript manuell.  
  
-   Verwenden Sie die Skriptgenerierungsfunktionen, die in den Replikations-Assistenten bereitgestellt werden.  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]installiert haben. Weitere Informationen finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
-   Verwenden Sie Replikationsverwaltungsobjekte (RMO), um das Skript programmgesteuert zu generieren und ein RMO-Objekt zu erstellen.  
  
 Beachten Sie bei der manuellen Erstellung von Replikationsskripts die folgenden Punkte:  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Skripts enthalten mindestens einen Batch. Der GO-Befehl signalisiert das Ende eines Batches. Wenn ein [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Skript keine GO-Befehle enthält, wird es als einzelner Batch ausgeführt.  
  
-   Beim Ausführen mehrerer gespeicherter Replikationsprozeduren in einem einzelnen Batch muss nach der ersten Prozedur allen folgenden Prozeduren das EXECUTE-Schlüsselwort vorangestellt werden.  
  
-   Alle gespeicherten Prozeduren in einem Batch müssen kompiliert werden, bevor ein Batch ausgeführt wird. Nachdem der Batch kompiliert und ein Ausführungsplan erstellt wurde, kann ggf. jedoch ein Laufzeitfehler auftreten.  
  
-   Beim Erstellen von Skripts zur Konfiguration der Replikation sollten Sie die Windows-Authentifizierung verwenden, um zu vermeiden, dass Sicherheitsanmeldeinformationen in der Skriptdatei gespeichert werden. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
## <a name="sample-replication-script"></a>Beispiel für ein Replikationsskript  
 Das folgende Skript kann zum Einrichten der Veröffentlichung und Verteilung auf einem Server ausgeführt werden.  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
 Dieses Skript kann dann lokal unter dem Namen `instdistpub.sql` gespeichert werden, sodass es bei Bedarf wiederholt ausgeführt werden kann.  
  
 Das vorherige Skript umfasst **sqlcmd**-Skriptvariablen, die in vielen Replikationscodebeispielen in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Onlinedokumentation verwendet werden. Skriptvariablen werden mit der `$(MyVariable)`-Syntax definiert. Werte für Variablen können in der Befehlszeile oder in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] an ein Skript übergeben werden. Weitere Informationen finden Sie im nächsten Abschnitt dieses Themas, "Ausführen von Replikationsskripts".  
  
## <a name="executing-replication-scripts"></a>Ausführen von Replikationsskripts  
 Sobald ein Replikationsskript erstellt wurde, kann es wie folgt ausgeführt werden:  
  
### <a name="creating-a-sql-query-file-in-sql-server-management-studio"></a>Erstellen einer SQL-Abfragedatei in SQL Server Management Studio  
 Eine [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Replikationsskriptdatei kann als SQL-Abfragedatei in einem [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]-Projekt erstellt werden. Nachdem das Skript geschrieben wurde, kann für diese Abfragedatei eine Verbindung mit der Datenbank hergestellt und das Skript ausgeführt werden. Weitere Informationen zum Erstellen von [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Skripts mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], finden Sie unter [Abfrage- und Text-Editoren &#40;SQL Server Management Studio&#41;](../../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
 Um ein Skript zu verwenden, das Skriptvariablen enthält, muss [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] im **sqlcmd**-Modus ausgeführt werden. Im **sqlcmd**-Modus lässt der Abfrage-Editor zusätzliche **sqlcmd**-spezifische Syntax zu, wie `:setvar` zum Festlegen eines Werts für eine Variable. Weitere Informationen zum **sqlcmd**-Modus finden Sie unter [Bearbeiten von SQLCMD-Skripts mit dem Abfrage-Editor](../../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md). Im folgenden Skript wird `:setvar` verwendet, um einen Wert für die `$(DistPubServer)`-Variable bereitzustellen.  
  
```  
:setvar DistPubServer N'MyPublisherAndDistributor';  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
--  
-- Additional code goes here  
--  
```  
  
### <a name="using-the-sqlcmd-utility-from-the-command-line"></a>Verwenden des sqlcmd-Hilfsprogramms über die Befehlszeile  
 Das folgende Beispiel veranschaulicht, wie die Befehlszeile zur Ausführung der `instdistpub.sql`-Skriptdatei mit dem [sqlcmd Hilfsprogramm](../../../tools/sqlcmd-utility.md) verwendet wird:  
  
```  
sqlcmd.exe -E -S sqlserverinstance -i C:\instdistpub.sql -o C:\output.log -v DistPubServer="N'MyDistributorAndPublisher'"  
```  
  
 In diesem Beispiel gibt der `-E`-Schalter an, dass beim Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Windows-Authentifizierung verwendet wird. Bei Verwendung der Windows-Authentifizierung entfällt das Speichern des Benutzernamens und Kennworts in der Skriptdatei. Der Name und Pfad der Skriptdatei wird mit dem `-i`-Schalter und der Name der Ausgabedatei mit dem `-o`-Schalter angegeben (bei Verwendung dieses Schalters wird die Ausgabe von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in diese Datei statt in die Konsole geschrieben). Mit dem `sqlcmd`-Hilfsprogramm können Sie Skriptvariablen mit dem `-v`-Schalter zur Laufzeit an das [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Skript übergeben. In diesem Beispiel ersetzt `sqlcmd` vor der Ausführung jede Instanz von `$(DistPubServer)` im Skript durch den `N'MyDistributorAndPublisher'`-Wert.  
  
> [!NOTE]  
>  Der `-X`-Schalter deaktiviert Skriptvariablen.  
  
### <a name="automating-tasks-in-a-batch-file"></a>Automatisieren von Tasks in einer Batchdatei  
 Mit einer Batchdatei können Replikationsverwaltungstasks, Replikationssynchronisierungstasks und andere Tasks in der gleichen Batchdatei automatisiert werden. Die folgende Batchdatei verwendet das **sqlcmd**-Hilfsprogramm, um die Abonnementdatenbank zu löschen und neu zu erstellen und ein Mergepullabonnement hinzuzufügen. Anschließend startet die Datei den Merge-Agent, um das neue Abonnement zu synchronisieren:  
  
```  
REM ----------------------Script to synchronize merge subscription ----------------------  
REM -- Creates subscription database and   
REM -- synchronizes the subscription to MergeSalesPerson.  
REM -- Current computer acts as both Publisher and Subscriber.  
REM -------------------------------------------------------------------------------------  
  
SET Publisher=%computername%  
SET Subscriber=%computername%  
SET PubDb=AdventureWorks  
SET SubDb=AdventureWorksReplica  
SET PubName=AdvWorksSalesOrdersMerge  
  
REM -- Drop and recreate the subscription database at the Subscriber  
sqlcmd /S%Subscriber% /E /Q"USE master IF EXISTS (SELECT * FROM sysdatabases WHERE name='%SubDb%' ) DROP DATABASE %SubDb%"  
sqlcmd /S%Subscriber% /E /Q"USE master CREATE DATABASE %SubDb%"  
  
REM -- Add a pull subscription at the Subscriber  
sqlcmd /S%Subscriber% /E /Q"USE %SubDb% EXEC sp_addmergepullsubscription @publisher = %Publisher%, @publication = %PubName%, @publisher_db = %PubDb%"  
sqlcmd /S%Subscriber% /E /Q"USE %SubDb%  EXEC sp_addmergepullsubscription_agent @publisher = %Publisher%, @publisher_db = %PubDb%, @publication = %PubName%, @subscriber = %Subscriber%, @subscriber_db = %SubDb%, @distributor = %Publisher%"  
  
REM -- This batch file starts the merge agent at the Subscriber to   
REM -- synchronize a pull subscription to a merge publication.  
REM -- The following must be supplied on one line.  
"\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE"  -Publisher  %Publisher% -Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB  %PubDb% -SubscriberDB %SubDb% -Publication %PubName% -PublisherSecurityMode 1 -OutputVerboseLevel 1  -Output  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1 -Validate 3  
  
```  
  
## <a name="scripting-common-replication-tasks"></a>Skripterstellung für allgemeine Replikationstasks  
 Im Folgenden sind einige der häufigsten Replikationstasks aufgeführt, für die mit gespeicherten Systemprozeduren ein Skript erstellt werden kann:  
  
-   Konfigurieren der Veröffentlichung und Verteilung  
  
-   Ändern von Verleger- und Verteilereigenschaften  
  
-   Deaktivieren von Veröffentlichung und Verteilung  
  
-   Erstellen von Veröffentlichungen und Definieren von Artikeln  
  
-   Löschen von Veröffentlichungen und Artikeln  
  
-   Erstellung eines Pullabonnements  
  
-   Ändern eines Pullabonnements  
  
-   Löschen eines Pullabonnements  
  
-   Erstellen eines Pushabonnements  
  
-   Ändern eines Pushabonnements  
  
-   Löschen eines Pushabonnements  
  
-   Synchronisieren eines Pullabonnements  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konzepte für die Replikationsprogrammierung](../../../relational-databases/replication/concepts/replication-programming-concepts.md)   
 [Gespeicherte Replikationsprozeduren &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Erstellen von Skripts für die Replikation](../../../relational-databases/replication/scripting-replication.md)  
  
  
