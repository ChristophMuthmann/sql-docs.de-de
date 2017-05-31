---
title: Verschieben eines vorhandenen Indexes in eine andere Dateigruppe | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving tables
- switching filegroups for index
- moving indexes
- indexes [SQL Server], moving
- filegroups [SQL Server], switching
ms.assetid: 167ebe77-487d-4ca8-9452-4b2c7d5cb96e
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cfc19f15cee7ca1185a2a9177474510c368b56bf
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="move-an-existing-index-to-a-different-filegroup"></a>Verschieben eines vorhandenen Indexes in eine andere Dateigruppe
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie einen vorhandenen Index in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]von der aktuellen Dateigruppe in eine andere verschieben.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **Verschieben eines vorhandenen Indexes in eine andere Dateigruppe mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Bei Tabellen mit gruppiertem Index wird beim Verschieben des gruppierten Index in eine neue Dateigruppe auch die Tabelle in diese Dateigruppe verschoben.  
  
-   Mit einer UNIQUE- oder PRIMARY KEY-Einschränkung mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]erstellte Indizes können nicht verschoben werden. Verwenden Sie zum Verschieben dieser Indizes die [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) -Anweisung mit der Option (DROP_EXISTING=ON) in [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-using-table-designer"></a>So verschieben Sie einen vorhandenen Index mit dem Tabellen-Designer in eine andere Dateigruppe  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle mit dem zu verschiebenden Index enthält.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Tabelle mit dem zu verschiebenden Index, und wählen Sie **Entwurf**aus.  
  
4.  Klicken Sie im Menü **Tabellen-Designer** auf **Indizes/Schlüssel**.  
  
5.  Wählen Sie den Index aus, den Sie verschieben möchten.  
  
6.  Erweitern Sie im Hauptraster **Datenbereichsspezifikation**.  
  
7.  Wählen Sie **Schemaname der Dateigruppe oder Partition** aus, und wählen Sie in der Liste die Dateigruppe oder das Partitionsschema aus, in die bzw. den Sie den Index verschieben möchten.  
  
8.  Klicken Sie auf **Schließen**.  
  
9. Klicken Sie im Menü **Datei** auf **Speichern***table_name*.  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-in-object-explorer"></a>So verschieben Sie einen vorhandenen Index im Objekt-Explorer in eine andere Dateigruppe  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle mit dem zu verschiebenden Index enthält.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle mit dem zu verschiebenden Index zu erweitern.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Indizes** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, den Sie verschieben möchten, und wählen Sie **Eigenschaften**aus.  
  
6.  Wählen Sie unter **Seite auswählen**die Option **Speicher**aus.  
  
7.  Wählen Sie die Dateigruppe aus, in die der Index verschoben werden soll.  
  
     Wählen Sie bei partitionierten Tabellen und Indizes das Partitionsschema aus, in das der Index verschoben werden soll. Weitere Informationen zu partitionierten Indizes finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
     Für das Verschieben von gruppierten Indizes können Sie die Onlineverarbeitung verwenden. Die Onlineverarbeitung ermöglicht, dass Benutzer während des Verschiebungsvorgangs des Indexes auf die dem Index zugrunde liegenden Daten sowie auf nicht gruppierte Indizes zugreifen können. Weitere Informationen finden Sie unter [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
     Auf Multiprozessorcomputern mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie die Anzahl der zum Ausführen der Indexanweisung verwendeten Prozessoren mit einem maximalen Grad an Parallelität konfigurieren. Die Funktion für parallele Indexvorgänge ist nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter „Von den SQL Server 2016-Editionen unterstützte Funktionen“. Weitere Informationen zu parallelen Indexvorgängen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
8.  Klicken Sie auf **OK**.  
  
 Die folgenden Informationen sind auf der Seite **Speicher** des Dialogfelds **Indexeigenschaften –** *Indexname* verfügbar:  
  
 **Dateigruppe**  
 Speichert den Index in der angegebenen Dateigruppe. Diese Liste enthält nur Standarddateigruppen (ROW). Die Standardauswahl in der Liste ist die PRIMARY-Dateigruppe der Datenbank.  
  
 **FILESTREAM-Dateigruppe**  
 Gibt die Dateigruppe für FILESTREAM-Daten an. Diese Liste zeigt nur FILESTREAM-Dateigruppen an. Die Standardlistenauswahl ist die Dateigruppe PRIMARY FILESTREAM.  
  
 **Partitionsschema**  
 Speichert den Index in einem Partitionsschema. Wenn Sie auf **Partitionsschema** klicken, wird das unten stehende Raster aktiviert. Die Standardlistenauswahl ist das für das Speichern der Tabellendaten verwendete Partitionsschema. Bei Auswahl eines anderen Partitionsschemas in der Liste werden die im Raster angezeigten Informationen aktualisiert.  
  
 Die Option Partitionsschema ist nicht verfügbar, wenn in der Datenbank keine Partitionsschemas vorhanden sind.  
  
 **Dateidatenstrom-Partitionsschema**  
 Gibt das Partitionsschema für FILESTREAM-Daten an. Das Partitionsschema muss mit dem Schema symmetrisch sein, das in der Option **Partitionsschema** angegeben wird.  
  
 Wenn die Tabelle nicht partitioniert ist, ist das Feld leer.  
  
 **Partitionsschemaparameter**  
 Zeigt den Namen der Spalte an, die Teil des Partitionsschemas ist.  
  
 **Tabellenspalte**  
 Wählt die Tabelle oder Sicht aus, die dem Partitionsschema zugeordnet werden soll.  
  
 **Datentyp der Spalte**  
 Zeigt Datentypinformationen zu der Spalte an.  
  
> [!NOTE]  
>  Wenn die Tabellenspalte eine berechnete Spalte ist, wird unter **Spaltendatentyp** „berechnete Spalte“ angezeigt.  
  
 **Onlineverarbeitung von DML-Anweisungen während der Indexverschiebung zulassen**  
 Ermöglicht Benutzern während des Indexvorgangs den Zugriff auf die zugrunde liegenden Tabellen- bzw. gruppierten Indexdaten und zugehörigen nicht gruppierten Indizes.  
  
> [!NOTE]  
>  Diese Option ist für XML-Indizes nicht verfügbar. Das gilt auch, wenn der Index ein deaktivierter gruppierter Index ist.  
  
 **Maximalen Grad an Parallelität festlegen**  
 Begrenzt die Anzahl der bei der Ausführung paralleler Pläne einzusetzenden Prozessoren. Der Standardwert ist 0; bei diesem Wert wird die tatsächliche Anzahl der verfügbaren CPUs verwendet. Wenn Sie den Wert auf 1 setzen, wird die Ausführung paralleler Pläne unterdrückt; bei einem Wert von größer als 1 wird die maximale Anzahl der bei der Ausführung einer einzelnen Abfrage zu verwendenden Prozessoren begrenzt. Diese Option ist nur verfügbar, wenn sich das Dialogfeld im Status **Neu organisieren** oder **Neu erstellen** befindet.  
  
> [!NOTE]  
>  Wird ein Wert angegeben, der über der Anzahl der verfügbaren CPUs liegt, wird die tatsächliche Anzahl der CPUs verwendet.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup"></a>So verschieben Sie einen vorhandenen Index in eine andere Dateigruppe  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the TransactionsFG1 filegroup on the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP TransactionsFG1;  
    GO  
    /* Adds the TransactionsFG1dat3 file to the TransactionsFG1 filegroup. Please note that you will have to change the filename parameter in this statement to execute it without errors.  
    */  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = TransactionsFG1dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\DATA\TransactionsFG1dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP TransactionsFG1;  
    GO  
    /*Creates the IX_Employee_OrganizationLevel_OrganizationNode index  
      on the TransactionsPS1 filegroup and drops the original IX_Employee_OrganizationLevel_OrganizationNode index.  
    */  
    CREATE NONCLUSTERED INDEX IX_Employee_OrganizationLevel_OrganizationNode  
        ON HumanResources.Employee (OrganizationLevel, OrganizationNode)  
        WITH (DROP_EXISTING = ON)  
        ON TransactionsFG1;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
  

