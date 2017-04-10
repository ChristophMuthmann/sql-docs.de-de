---
title: "Festlegen oder &#196;ndern der Spaltensortierung | Microsoft Docs"
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
  - "tempdb-Datenbank [SQL Server], Sortierungen"
  - "Sortierungen [SQL Server], Spalte"
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Festlegen oder &#196;ndern der Spaltensortierung
  Sie können die Datenbanksortierung für **char**-, **varchar**-, **text**-, **nchar**-, **nvarchar**- und **ntext** -Daten überschreiben, indem Sie eine andere Sortierung für eine bestimmte Spalte einer Tabelle angeben und dann eine der folgenden Optionen verwenden:  
  
-   Die COLLATE-Klausel von [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) und [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md). Beispiel:  
  
    ```  
    CREATE TABLE dbo.MyTable  
      (PrimaryKey   int PRIMARY KEY,  
       CharCol      varchar(10) COLLATE French_CI_AS NOT NULL  
      );  
    GO  
    ALTER TABLE dbo.MyTable ALTER COLUMN CharCol  
                varchar(10)COLLATE Latin1_General_CI_AS NOT NULL;  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
-   Die **Column.Collation**-Eigenschaft in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
 Sie können die Sortierung einer Spalte nicht ändern, wenn folgende Objekte aktuell auf die Spalte verweisen:  
  
-   Eine berechnete Spalte.  
  
-   Ein Index.  
  
-   Verteilungsstatistiken, die entweder automatisch oder mithilfe der CREATE STATISTICS-Anweisung generiert wurden.  
  
-   Eine CHECK-Einschränkung.  
  
-   Eine FOREIGN KEY-Einschränkung.  
  
 Wenn Sie **tempdb** verwenden, enthält die [COLLATE](../Topic/COLLATE%20\(Transact-SQL\).md)-Klausel eine *database_defauls*-Option, mit der angegeben werden kann, dass für eine Spalte einer temporären Tabelle anstelle der Sortierung von **tempdb** die Standardsortierung der aktuellen Benutzerdatenbank für die Verbindung verwendet wird.  
  
## Sortierungen und text-Spalten  
 Sie können Werte in einer **text** -Spalte einfügen und aktualisieren, deren Sortierung sich von der Codepage der Standardsortierung der Datenbank unterscheidet. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die Werte implizit in die Sortierung der Spalte konvertiert.  
  
## Sortierungen und tempdb  
 Die **tempdb** -Datenbank wird bei jedem Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und weist die gleiche Standardsortierung wie die **model** -Datenbank auf. Dabei handelt es sich normalerweise um die gleiche Sortierung wie die Standardsortierung der Instanz. Wenn Sie eine Benutzerdatenbank erstellen und eine andere Standardsortierung als für die **model**-Datenbank angeben, verwendet die Benutzerdatenbank eine andere Standardsortierung als die **tempdb**-Datenbank. Alle temporären gespeicherten Prozeduren oder temporären Tabellen werden in **tempdb**erstellt und gespeichert. Dies bedeutet, dass alle impliziten Spalten in temporären Tabellen und alle Konstanten, Variablen und Parameter mit erzwingbaren Standards in temporär gespeicherten Prozeduren andere Sortierungen aufweisen als die vergleichbaren Objekte, die in dauerhaften Tabellen und gespeicherten Prozeduren erstellt werden.  
  
 Dies kann zu Problemen hinsichtlich einer Nichtübereinstimmung in Sortierungen zwischen benutzerdefinierten Datenbanken und Systemdatenbankobjekten führen. Eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet z. B. die Latin1_General_CS_AS-Sortierung, und Sie führen die folgenden Anweisungen aus:  
  
```  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 In diesem System verwendet die **tempdb**-Datenbank die Latin1_General_CS_AS-Sortierung mit Codepage 1252, und `TestDB` und `TestPermTab.Col1` verwenden die `Estonian_CS_AS`-Sortierung mit Codepage 1257. Beispiel:  
  
```  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 Im vorherigen Beispiel verwendet die **tempdb**-Datenbank die Latin1_General_CS_AS-Sortierung, und `TestDB` und `TestTab.Col1` verwenden die `Estonian_CS_AS`-Sortierung. Beispiel:  
  
```  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 Da **tempdb** die Standardserversortierung und `TestPermTab.Col1` eine andere Sortierung verwendet, wird in SQL Server der folgende Fehler zurückgegeben: „Ein Sortierungskonflikt zwischen ‚Latin1_General_CI_AS_KS_WS‘ und ‚Estonian_CS_AS‘ im Gleich-Vorgang kann nicht aufgelöst werden.“  
  
 Sie können den Fehler vermeiden, indem Sie stattdessen eine der folgenden Alternativen verwenden:  
  
-   Geben Sie an, dass für die Spalte der temporären Tabelle die Standardsortierung der Benutzerdatenbank und nicht die Standardsortierung von **tempdb**verwendet wird. Auf diese Weise kann die temporäre Tabelle mit ähnlich formatierten Tabellen in mehreren Datenbanken arbeiten, wenn dies in dem System erforderlich ist.  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   Geben Sie die richtige Sortierung für die `#TestTempTab`-Spalte an:  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## Siehe auch  
 [Festlegen oder Ändern der Serversortierung](../../relational-databases/collations/set-or-change-the-server-collation.md)   
 [Festlegen oder Ändern der Datenbanksortierung](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  