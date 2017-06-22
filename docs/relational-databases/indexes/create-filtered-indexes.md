---
title: Erstellen gefilterter Indizes | Microsoft Dokumentation
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtered indexes [SQL Server], about filtered indexes
- designing indexes [SQL Server], filtered
- filtered indexes [SQL Server]
- nonclustered indexes [SQL Server], filtered
- indexes [SQL Server], filtered
ms.assetid: 25e1fcc5-45d7-4c53-8c79-5493dfaa1c74
caps.latest.revision: 73
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de8d5ce869856d289b70b028ede2bc1009220a38
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="create-filtered-indexes"></a>Erstellen gefilterter Indizes
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie ein gefilterter Index in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]erstellt wird. Ein gefilterter Index ist ein optimierter nicht gruppierter Index, der sich besonders für Abfragen eignet, bei denen aus einer fest definierten Teilmenge von Daten ausgewählt wird. Dieser verwendet ein Filterprädikat, um einen Teil der Zeilen in der Tabelle zu indizieren. Mit einem sorgfältig entworfenen gefilterten Index können im Vergleich zu Tabellenindizes die Abfrageleistung verbessert und der Aufwand für die Indexverwaltung und die Indexspeicherung reduziert werden.  
  
 Gefilterte Indizes können gegenüber Tabellenindizes folgende Vorteile bieten:  
  
-   **Verbesserte Abfrageleistung und Planqualität**  
  
     Mit einem sorgfältig entworfenen gefilterten Index wird die Abfrageleistung und die Ausführungsplanqualität verbessert, da dieser kleiner ist als ein nicht gruppierter Tabellenindex und mit gefilterten Statistiken arbeitet. Die gefilterten Statistiken sind genauer als Tabellenstatistiken, da diese nur die Zeilen im gefilterten Index umfassen.  
  
-   **Reduzierter Aufwand bei der Indexverwaltung**  
  
     Ein Index wird nur beibehalten, wenn DML-Anweisungen (Data Manipulation Language) die Daten im Index beeinflussen. Ein gefilterter Index reduziert im Vergleich zu einem nicht gruppierten Tabellenindex den Aufwand für die Indexverwaltung, da dieser kleiner ist und nur beibehalten wird, wenn die Daten im Index geändert werden. Eine große Anzahl von gefilterten Indizes ist insbesondere dann von Vorteil, wenn diese Daten enthalten, die nur selten geändert werden. Ebenso reduziert die geringere Indexgröße den Aufwand für das Aktualisieren der Statistiken, wenn ein gefilterter Index nur die häufig geänderten Daten enthält.  
  
-   **Reduzierter Aufwand bei der Indexspeicherung**  
  
     Ein gefilterter Index kann den Speicherplatzbedarf von nicht gruppierten Indizes reduzieren, wenn ein Tabellenindex nicht erforderlich ist. Sie können einen nicht gruppierten Tabellenindex durch mehrere gefilterte Indizes ersetzen, ohne damit die Speicherplatzanforderungen wesentlich zu erhöhen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Entwurfsaspekte](#Design)  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So erstellen Sie einen gefilterten Index mithilfe von:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Design"></a> Entwurfsaspekte  
  
-   Wenn eine Spalte nur wenig relevante Werte für Abfragen aufweist, können Sie für die Teilmenge der Werte einen gefilterten Index erstellen. Wenn beispielsweise die Werte in einer Spalte größtenteils NULL sind und die Abfrage nur die Werte ungleich NULL berücksichtigt, können Sie für die Datenzeilen mit den Werten ungleich NULL einen gefilterten Index erstellen. Der resultierende Index ist kleiner und verursacht weniger Verwaltungsaufwand als ein nicht gruppierter Tabellenindex, der für dieselben Schlüsselspalten festgelegt wird.  
  
-   Wenn eine Tabelle heterogene Datenzeilen enthält, können Sie einen gefilterten Index für eine oder mehrere Datenkategorien erstellen. Dies kann die Leistung der Abfragen auf diesen Datenzeilen verbessern, indem es den Fokus einer Abfrage auf einen bestimmten Bereich der Tabelle eingrenzt. Auch hier ist der resultierende Index kleiner und verursacht weniger Verwaltungsaufwand als ein nicht gruppierter Tabellenindex.  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Sie können keinen gefilterten Index für eine Sicht erstellen. Der Abfrageoptimierer kann jedoch von einem für eine Tabelle definierten gefilterten Index profitieren, auf den in einer Sicht verwiesen wird. Der Abfrageoptimierer berücksichtigt einen gefilterten Index für eine Abfrage, die aus einer Sicht auswählt, wenn die Ergebnisse der Abfrage korrekt sind.  
  
-   Gefilterte Indizes haben die folgenden Vorteile gegenüber indizierten Sichten:  
  
    -   Reduzierter Aufwand bei der Indexverwaltung. Im Vergleich zu einer indizierten Sicht benötigt der Abfrageprozessor weniger CPU-Ressourcen, um einen gefilterten Index zu aktualisieren.  
  
    -   Verbesserte Planqualität. Während der Abfragekompilierung wählt der Abfrageoptimierer in vielen Situationen bevorzugt einen gefilterten Index anstelle der äquivalenten indizierten Sicht aus.  
  
    -   Neuerstellung von online geschalteten Indizes. Sie können gefilterte Indizes neu erstellen, während die Indizes für Abfragen verfügbar sind. Die Neuerstellung von online geschalteten Indizes wird bei indizierten Sichten nicht unterstützt. Weitere Informationen finden Sie unter der REBUILD-Option für [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
    -   Nicht eindeutige Indizes Gefilterte Indizes können nicht eindeutig sein, wohingegen indizierte Sichten eindeutig sein müssen.  
  
-   Gefilterte Indizes werden für eine Tabelle definiert und unterstützen nur einfache Vergleichsoperatoren. Wenn Sie einen Filterausdruck benötigen, der auf mehrere Tabellen verweist oder eine komplexe Logik aufweist, sollten Sie eine Sicht erstellen.  
  
-   Eine Spalte im gefilterten Indexausdruck muss in der Definition des gefilterten Indexes keine Schlüsselspalte oder eingeschlossene Spalte sein, wenn der gefilterte Indexausdruck dem Abfrageprädikat entspricht und die Abfrage die Spalte im gefilterten Indexausdruck mit den Abfrageergebnissen nicht zurückgibt.  
  
-   Eine Spalte im gefilterten Indexausdruck sollte in der Definition des gefilterten Indexes eine Schlüsselspalte oder eingeschlossene Spalte sein, wenn das Abfrageprädikat die Spalte in einem Vergleich verwendet, der nicht dem gefilterten Indexausdruck entspricht.  
  
-   Eine Spalte im gefilterten Indexausdruck sollte in der Definition des gefilterten Indexes eine Schlüsselspalte oder eingeschlossene Spalte sein, wenn die Spalte im Abfrageresultset enthalten ist.  
  
-   Der Schlüssel des gruppierten Indexes für die Tabelle muss in der Definition des gefilterten Indexes keine Schlüsselspalte oder eingeschlossene Spalte sein. Der Schlüssel des gruppierten Indexes ist automatisch in allen nicht gruppierten Indizes enthalten, wozu auch gefilterte Indizes zählen.  
  
-   Wenn der im gefilterten Indexausdruck der gefilterten Indexergebnisse angegebene Vergleichsoperator eine implizite oder explizite Datenkonvertierung ergibt, kommt es zu einem Fehler, wenn die Konvertierung auf der linken Seite eines Vergleichsoperators auftritt. Eine mögliche Lösung besteht darin, den gefilterten Indexausdruck mit dem Datenkonvertierungsoperator (CAST oder CONVERT) auf die rechte Seite des Vergleichsoperators zu schreiben.  

- Überprüfen Sie die erforderlichen SET-Optionen für die Erstellung gefilterter Indizes in der [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)-Syntax
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein. Verwenden Sie CREATE INDEX WITH DROP_EXISTING, um den gefilterten Indexausdruck zu ändern.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-create-a-filtered-index"></a>So erstellen Sie einen gefilterten Index  
  
1.  Klicken Sie in Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle enthält, in der Sie einen gefilterten Index erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, in der Sie einen gefilterten Index erstellen möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Ordner **Indizes** , zeigen Sie auf **Neuer Index**, und wählen Sie **Nicht gruppierter Index**aus.  
  
5.  Geben Sie in das Dialogfeld **Neuer Index** auf der Seite **Allgemein** den Namen des neuen Indexes in das Feld **Indexname** ein.  
  
6.  Klicken Sie unter **Indexschlüsselspalten**auf **Hinzufügen…**.  
  
7.  Aktivieren Sie im Dialogfeld **Spalten auswählen aus***table_name* die Kontrollkästchen der Tabellenspalten, die dem eindeutigen Index hinzugefügt werden sollen.  
  
8.  Klicken Sie auf **OK**.  
  
9. Geben Sie auf der Seite **Filter** unter **Filterausdruck**den SQL-Ausdruck ein, mit dem Sie den gefilterten Index erstellen.  
  
10. Klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-filtered-index"></a>So erstellen Sie einen gefilterten Index  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Looks for an existing filtered index named "FIBillOfMaterialsWithEndDate"  
    -- and deletes it from the table Production.BillOfMaterials if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
        WHERE name = N'FIBillOfMaterialsWithEndDate'  
        AND object_id = OBJECT_ID (N'Production.BillOfMaterials'))  
    DROP INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials  
    GO  
    -- Creates a filtered index "FIBillOfMaterialsWithEndDate"  
    -- on the table Production.BillOfMaterials   
    -- using the columms ComponentID and StartDate.  
  
    CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials (ComponentID, StartDate)  
        WHERE EndDate IS NOT NULL ;  
    GO  
    ```  
  
     Der obenstehende gefilterte Index ist für die folgende Abfrage gültig. Sie können den Abfrageausführungsplan anzeigen, um zu bestimmen, ob der Abfrageoptimierer den gefilterten Index verwendet hat.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ProductAssemblyID, ComponentID, StartDate   
    FROM Production.BillOfMaterials  
    WHERE EndDate IS NOT NULL   
        AND ComponentID = 5   
        AND StartDate > '01/01/2008' ;  
    GO  
    ```  
  
#### <a name="to-ensure-that-a-filtered-index-is-used-in-a-sql-query"></a>So stellen Sie sicher, dass ein gefilterter Index in einer SQL-Abfrage verwendet wird  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
        WITH ( INDEX ( FIBillOfMaterialsWithEndDate ) )   
    WHERE EndDate IN ('20000825', '20000908', '20000918');   
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [CCREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
  

