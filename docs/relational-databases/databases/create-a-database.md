---
title: "Erstellen einer Datenbank | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbanken [SQL Server], erstellen"
  - "Datenbankerstellung [SQL Server], SQL Server Management Studio"
  - "Erstellen von Datenbanken"
ms.assetid: 4c4beea2-6cbc-4352-9db6-49ea8130bb64
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Erstellen einer Datenbank
  In diesem Thema wird beschrieben, wie eine Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]erstellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So erstellen Sie eine Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Maximal 32.767 Datenbanken können auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angegeben werden.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Die CREATE DATABASE-Anweisung muss im Autocommitmodus (dem Standardmodus für die Transaktionsverwaltung) ausgeführt werden und ist in einer expliziten oder impliziten Transaktion nicht zulässig.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Die [master](../../relational-databases/databases/master-database.md) -Datenbank sollte immer dann gesichert werden, wenn eine Benutzerdatenbank erstellt, geändert oder gelöscht wird.  
  
-   Wenn Sie eine Datenbank erstellen, sollten die Datendateien möglichst groß sein. Orientieren Sie sich dabei an den maximal zu erwartenden Datenmengen, die in der Datenbank gespeichert werden sollen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Berechtigung CREATE DATABASE in der master-Datenbank oder die Berechtigung CREATE ANY DATABASE oder ALTER ANY DATABASE.  
  
 Zur Steuerung der Datenträgernutzung einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die Berechtigung zum Erstellen von Datenbanken in der Regel auf einige wenige Anmeldekonten beschränkt.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So erstellen Sie eine Datenbank  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Datenbanken**, und klicken Sie anschließend auf **Neue Datenbank**.  
  
3.  Geben Sie unter **Neue Datenbank**einen Datenbanknamen ein.  
  
4.  Zum Erstellen der Datenbank unter Übernahme aller Standardwerte klicken Sie auf **OK**; ansonsten fahren Sie mit den folgenden optionalen Schritten fort.  
  
5.  Zum Ändern des Besitzernamens klicken Sie auf (**…**), um einen anderen Besitzer auszuwählen.  
  
    > [!NOTE]  
    >  Die Option **Volltextindizierung verwenden** ist immer aktiviert und wird ausgegraut angezeigt, da ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] alle Benutzerdatenbanken volltextfähig sind.  
  
6.  Zum Ändern der Standardwerte der Primärdaten- und Transaktionsprotokolldateien klicken Sie im Bereich **Datenbankdateien** auf die entsprechende Zelle und geben den neuen Wert ein. Weitere Informationen finden Sie unter [Add Data or Log Files to a Database](../../relational-databases/databases/add-data-or-log-files-to-a-database.md).  
  
7.  Zum Ändern der Sortierung der Datenbank klicken Sie auf die Seite **Optionen** , und wählen dann eine Sortierung aus der Liste aus.  
  
8.  Zum Ändern des Wiederherstellungsmodells klicken Sie auf die Seite **Optionen** aus und wählen dann ein Wiederherstellungsmodell aus der Liste aus.  
  
9. Zum Ändern der Datenbankoptionen klicken Sie auf die Seite **Optionen** aus und ändern anschließend die Datenbankoptionen. Eine Beschreibung jeder Option finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md).  
  
10. Zum Hinzufügen einer neuen Dateigruppe klicken Sie auf die Seite **Dateigruppen** . Klicken Sie auf **Hinzufügen** , und geben Sie dann die Werte für die Dateigruppe ein.  
  
11. Zum Hinzufügen einer erweiterten Eigenschaft zur Datenbank klicken Sie auf die Seite **Erweiterte Eigenschaften** .  
  
    1.  Geben Sie in die Spalte **Name** einen Namen für die erweiterte Eigenschaft ein.  
  
    2.  Geben Sie in die Spalte **Wert** den Text für die erweiterte Eigenschaft ein. Geben Sie beispielsweise eine oder mehrere Angaben zur Beschreibung der Datenbank ein.  
  
12. Klicken Sie auf **OK**, um die Datenbank zu erstellen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So erstellen Sie eine Datenbank  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die Datenbank mit dem Namen `Sales` erstellt. Da das PRIMARY-Schlüsselwort nicht verwendet wird, wird die erste Datei (`Sales`_`dat`) zur primären Datei. Da im SIZE-Parameter für die Datei `Sales`\_`dat` weder MB noch KB angegeben ist, wird die Einheit MB verwendet und in Megabyte zugeordnet. Die `Sales`\_`log` wird in Megabyte zugeordnet, weil das Suffix `MB` explizit im `SIZE` -Parameter angegeben ist.  
  
```tsql  
USE master ;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
 Weitere Beispiele finden Sie unter [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## Siehe auch  
 [Datenbankdateien und Dateigruppen](../../relational-databases/databases/database-files-and-filegroups.md)   
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Hinzufügen von Daten- oder Protokolldateien zu einer Datenbank](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
  
  