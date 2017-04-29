---
title: "Deaktivieren von Indizes und Einschränkungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.disableindexes.f1
helpviewer_keywords:
- disabled indexes [SQL Server], index operations
- nonclustered indexes [SQL Server], disabling
- disabled indexes [SQL Server], guidelines
- clustered indexes, disabling
- constraints [SQL Server], disabling
- disabled indexes [SQL Server], viewing
- FOREIGN KEY constraints, disabling
- statistical information [SQL Server], indexes
- index disabling [SQL Server]
- indexed views [SQL Server], disabled indexes
ms.assetid: 2198f1af-fa44-47e9-92df-f4fde322ba18
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 02ec61b5f3342ba8c5abd6e5044cd9f6863f6145
ms.lasthandoff: 04/11/2017

---
# <a name="disable-indexes-and-constraints"></a>Deaktivieren von Indizes und Einschränkungen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie ein Index oder Einschränkungen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]deaktiviert werden. Wenn Indizes deaktiviert werden, können Benutzer nicht mehr darauf zugreifen, und bei gruppierten Indizes können sie auch nicht mehr auf die dem Index zugrunde liegenden Tabellendaten zugreifen. Die Indexdefinition verbleibt jedoch in den Metadaten, und bei nicht gruppierten Indizes werden die Indexstatistiken beibehalten. Beim Deaktivieren eines nicht gruppierten oder gruppierten Indexes in einer Sicht werden die Indexdaten physisch gelöscht. Das Deaktivieren eines gruppierten Indexes für eine Tabelle verhindert lediglich das Zugreifen auf die Daten; diese verbleiben in der Tabelle, sind jedoch erst für DML-Vorgänge (Datenbearbeitungssprache) verfügbar, wenn der Index gelöscht oder neu erstellt wurde.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So deaktivieren Sie einen Index mithilfe von:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Der Index wird nicht beibehalten, während er deaktiviert ist.  
  
-   Der deaktivierte Index wird beim Erstellen von Abfrageausführungsplänen nicht vom Abfrageoptimierer berücksichtigt. Des weiteren erzeugen Abfragen einen Fehler, die über einen Tabellenhinweis auf den deaktivierten Index verweisen.  
  
-   Sie können keinen Index mit dem gleichen Namen erstellen, den ein vorhandener deaktivierter Index aufweist.  
  
-   Ein deaktivierter Index kann nicht gelöscht werden.  
  
-   Beim Deaktivieren eines eindeutigen Indexes werden die PRIMARY KEY- oder UNIQUE-Einschränkung sowie alle FOREIGN KEY-Einschränkungen, die aus anderen Tabellen auf die indizierten Spalten verweisen, ebenfalls deaktiviert. Beim Deaktivieren eines gruppierten Indexes werden alle eingehenden und ausgehenden FOREIGN KEY-Einschränkungen der zugrunde liegenden Tabelle ebenfalls deaktiviert. Die Namen der Einschränkungen werden in einer Warnmeldung aufgeführt, wenn der Index deaktiviert wird. Nach dem Neuerstellen des Indexes müssen alle Einschränkungen mithilfe der ALTER TABLE CHECK CONSTRAINT-Anweisung manuell aktiviert werden.  
  
-   Nicht gruppierte Indizes werden mit dem Deaktivieren des gruppierten Indexes, dem sie zugeordnet sind, automatisch deaktiviert. Sie können nicht mehr aktiviert werden, bis der gruppierte Index der Tabelle oder Sicht aktiviert bzw. der gruppierte Index der Tabelle gelöscht wird. Nicht gruppierte Indizes müssen explizit aktiviert werden, es sei denn, der gruppierte Index wurde mithilfe der ALTER INDEX ALL REBUILD-Anweisung aktiviert.  
  
-   Die ALTER INDEX ALL REBUILD-Anweisung erstellt alle deaktivierten Indizes der Tabelle neu und aktiviert sie, mit Ausnahme von deaktivierten Indizes für Sichten. Indizes für Sichten müssen durch eine separate ALTER INDEX ALL REBUILD-Anweisung aktiviert werden.  
  
-   Beim Deaktivieren eines gruppierten Indexes auf einer Tabelle werden auch alle gruppierten und nicht gruppierten Indizes in Sichten deaktiviert, die auf diese Tabelle verweisen. Diese Indizes müssen genau wie die Indizes der Tabelle, auf die sie verweisen, neu erstellt werden.  
  
-   Auf die Datenzeilen des deaktivierten gruppierten Indexes kann nicht zugegriffen werden, mit Ausnahme von Zugriffen zum Löschen oder Neuerstellen des gruppierten Indexes.  
  
-   Sie können einen deaktivierten nicht gruppierten Index online neu erstellen, wenn die Tabelle über einen gruppierten Index verfügt, der nicht deaktiviert ist. Sie müssen jedoch einen deaktivierten gruppierten Index immer offline neu erstellen, wenn Sie die ALTER INDEX REBUILD- oder CREATE INDEX WITH DROP_EXISTING-Anweisung verwenden. Weitere Informationen zu Onlineindexvorgängen finden Sie unter [Ausführen von Onlineindexvorgängen](../../relational-databases/indexes/perform-index-operations-online.md).  
  
-   Die CREATE STATISTICS-Anweisung kann nicht für eine Tabelle mit einem deaktivierten gruppierten Index ausgeführt werden.  
  
-   Die AUTO_CREATE_STATISTICS-Datenbankoption erstellt neue Statistiken für eine Spalte, wenn der Index deaktiviert ist und folgende Bedingungen zutreffen:  
  
    -   AUTO_CREATE_STATISTICS ist auf ON festgelegt.  
  
    -   Es sind keine Statistiken für die Spalte vorhanden.  
  
    -   Statistiken sind während der Abfrageoptimierung erforderlich.  
  
-   Ist ein gruppierter Index deaktiviert, kann [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) keine Informationen über die zugrunde liegende Tabelle zurückgeben. Stattdessen meldet die Anweisung, dass der gruppierte Index deaktiviert ist. [DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md) kann nicht zur Defragmentierung eines deaktivierten Indexes verwendet werden. Die Anweisung schlägt mit einer Fehlermeldung fehl. Zum Neuerstellen eines deaktivierten Indexes können Sie [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md) verwenden.  
  
-   Durch Erstellen eines neuen gruppierten Indexes werden zuvor deaktivierte nicht gruppierte Indizes aktiviert. Weitere Informationen finden Sie unter [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Zum Ausführen von ALTER INDEX benötigen Sie mindestens die ALTER-Berechtigung auf der Tabelle bzw. Sicht.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-disable-an-index"></a>So deaktivieren Sie einen Index  
  
1.  Klicken Sie in Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle enthält, in der Sie einen Index deaktivieren möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, in der Sie einen Index deaktivieren möchten.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Indizes** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, den Sie deaktivieren möchten, und wählen Sie **Deaktivieren**aus.  
  
6.  Überprüfen Sie im Dialogfeld **Index deaktivieren** , dass der richtige Index im Raster **Zu deaktivierende Indizes** ausgewählt ist, und klicken sie auf **OK**.  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>So deaktivieren Sie alle Indizes in einer Tabelle  
  
1.  Klicken Sie in Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle enthält, in der Sie die Indizes deaktivieren möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, in der Sie die Indizes deaktivieren möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Ordner **Indizes** , und wählen Sie **Alle deaktivieren**aus.  
  
5.  Überprüfen Sie im Dialogfeld **Indizes deaktivieren** , dass die richtigen Indizes im Raster **Zu deaktivierende Indizes** ausgewählt sind, und klicken sie auf **OK**. Um einen Index aus dem Raster **Zu deaktivierende Indizes** zu entfernen, wählen Sie den Index aus, und drücken Sie die ENTF-Taste.  
  
 Die folgenden Informationen sind im Dialogfeld **Index deaktivieren** verfügbar:  
  
 **Indexname**  
 Zeigt den Namen des Indexes an. Während der Ausführung wird in dieser Spalte auch ein Symbol angezeigt, das den Status wiedergibt.  
  
 **Tabellenname**  
 Zeigt den Namen der Tabelle oder Sicht an, für die der Index erstellt wurde.  
  
 **Indextyp**  
 Zeigt den Typ des Indexes an: **Gruppiert**, **Nicht gruppiert**, **Räumlich**oder **XML**.  
  
 **Status**  
 Zeigt den Status des Deaktivierungsvorgangs an. Mögliche Werte nach der Ausführung:  
  
-   Leer  
  
     Vor der Ausführung ist **Status** leer.  
  
-   **Vorgang wird ausgeführt**  
  
     Die Deaktivierung der Indizes wurde gestartet, ist aber noch nicht abgeschlossen.  
  
-   **Success**  
  
     Der Deaktivierungsvorgang ist erfolgreich abgeschlossen.  
  
-   **Fehler**  
  
     Während des Indexdeaktivierungsvorgangs ist ein Fehler aufgetreten, und der Vorgang wurde nicht erfolgreich abgeschlossen.  
  
-   **Beendet**  
  
     Die Deaktivierung des Indexes wurde nicht erfolgreich abgeschlossen, weil der Benutzer den Vorgang gestoppt hat.  
  
 **MessageBox**  
 Stellt den Text der Fehlermeldungen während des Deaktivierungsvorgangs bereit. Während der Ausführung werden die Fehler als Links angezeigt. Der Text der Links beschreibt den Hauptteil des Fehlers. Die Spalte **Meldung** ist meist nicht breit genug, um den vollständigen Meldungstext lesen zu können. Der vollständige Text kann auf zwei Arten abgerufen werden:  
  
-   Bewegen Sie den Mauszeiger über die Meldungszelle, um eine QuickInfo mit dem Fehlertext anzuzeigen.  
  
-   Klicken Sie auf den Link, um ein Dialogfeld mit dem vollständigen Fehler anzuzeigen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-disable-an-index"></a>So deaktivieren Sie einen Index  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- disables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    DISABLE;  
    ```  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>So deaktivieren Sie alle Indizes in einer Tabelle  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Disables all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    DISABLE;  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
  

