---
title: Erstellen von Indizes mit eingeschlossenen Spalten | Microsoft Dokumentation
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index size [SQL Server]
- index keys [SQL Server]
- index columns [SQL Server]
- size [SQL Server], indexes
- key columns [SQL Server]
- included columns
- nonclustered indexes [SQL Server], included columns
- designing indexes [SQL Server], included columns
- nonkey columns
ms.assetid: d198648d-fea5-416d-9f30-f9d4aebbf4ec
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6cdd414e056c08b3a7b539baa36f4cdde2a68180
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="create-indexes-with-included-columns"></a>Erstellen von Indizes mit eingeschlossenen Spalten
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie eingeschlossene Spalten (oder Nichtschlüsselspalten) hinzugefügt werden, um die Funktionalität von nicht gruppierten Indizes in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]zu erweitern. Indem Sie Nichtschlüsselspalten einschließen, erstellen Sie nicht gruppierte Indizes, die eine größere Anzahl von Abfragen abdecken. Dies ist der Fall, weil Nichtschlüsselspalten die folgenden Vorteile aufweisen:  
  
-   Es kann sich um Datentypen handeln, die als Indexschlüsselspalten nicht zulässig sind.  
  
-   Sie werden von [!INCLUDE[ssDE](../../includes/ssde-md.md)] beim Berechnen der Indexschlüsselspalten oder Indexschlüsselgröße nicht berücksichtigt.  
  
 Ein Index mit Nichtschlüsselspalten kann die Abfrageleistung erheblich steigern, wenn alle Spalten in der Abfrage in den Index als Schlüssel- oder Nichtschlüsselspalten eingeschlossen werden. Leistungsvorteile werden erzielt, weil der Abfrageoptimierer alle Spaltenwerte im Index finden kann; auf Daten der Tabelle oder des gruppierten Indexes wird nicht zugegriffen, sodass als Ergebnis weniger Datenträger-E/A-Vorgänge auftreten.  
  
> [!NOTE]  
> Wenn ein Index alle Spalten enthält, auf die eine Abfrage verweist, wird dies normalerweise als *Abdecken der Abfrage*bezeichnet.  
   
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="DesignRecs"></a> Entwurfsempfehlungen  
  
-   Überarbeiten Sie nicht gruppierte Indizes mit großen Indexschlüsseln so, dass nur Spalten, die für Suchen und Suchvorgänge verwendet werden, Schlüsselspalten sind. Erklären Sie alle anderen Spalten, die die Abfrage abdecken, zu Nichtschlüsselspalten. Auf diese Weise sind alle Spalten vorhanden, die zum Abdecken der Abfrage erforderlich sind, der Indexschlüssel selbst ist jedoch klein und effizient.  
  
-   Schließen Sie Nichtschlüsselspalten in einen nicht gruppierten Index ein, damit die Größenbegrenzungen des aktuellen Indexes von maximal 32 Schlüsselspalten und einer maximalen Größe des Indexschlüssels von 1,700 Byte (16 Schlüsselspalten und 900 Byte vor [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]) nicht überschritten werden. Nichtschlüsselspalten werden von [!INCLUDE[ssDE](../../includes/ssde-md.md)] beim Berechnen der Indexschlüsselspalten oder Indexschlüsselgröße nicht berücksichtigt.  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Nichtschlüsselspalten können nur für nicht gruppierte Indizes definiert werden.  
  
-   Alle Datentypen außer **text**, **ntext**und **image** können als Nichtschlüsselspalten verwendet werden.  
  
-   Berechnete Spalten, die deterministisch und entweder präzise oder unpräzise sind, können als Nichtschlüsselspalten verwendet werden. Weitere Informationen finden Sie unter [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
-   Berechnete Spalten, die aus den Datentypen **image**, **ntext**und **text** abgeleitet werden, können Nichtschlüsselspalten sein, wenn der Datentyp der berechneten Spalte als Nichtschlüssel-Indexspalte zulässig ist.  
  
-   Nichtschlüsselspalten können nur aus einer Tabelle gelöscht werden, wenn der Index der Tabelle zuvor gelöscht wird.  
  
-   Nichtschlüsselspalten können nur zum Ausführen der folgenden Aufgaben geändert werden:  
  
    -   Ändern der NULL-Zulässigkeit der Spalte von NOT NULL in NULL.  
  
    -   Vergrößern der Länge von **varchar**-, **nvarchar**- oder **varbinary** -Spalten.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>So erstellen Sie einen Index mit Nichtschlüsselspalten  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle enthält, in der Sie einen Index mit Nichtschlüsselspalten erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, für die Sie einen Index mit Nichtschlüsselspalten erstellen möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Ordner **Index** , zeigen Sie auf **Neuer Index**, und wählen Sie **Nicht gruppierter Index…**aus.  
  
5.  Geben Sie in das Dialogfeld **Neuer Index** auf der Seite **Allgemein** den Namen des neuen Indexes in das Feld **Indexname** ein.  
  
6.  Klicken Sie auf der Registerkarte **Indexschlüsselspalten** auf **Hinzufügen…**.  
  
7.  Aktivieren Sie im Dialogfeld **Spalten auswählen aus***Tabellenname* das oder die Kontrollkästchen der Tabellenspalte oder der Spalten, die dem Index hinzugefügt werden sollen.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie auf der Registerkarte **Eingeschlossene Spalten** auf **Hinzufügen…**.  
  
10. Aktivieren Sie im Dialogfeld **Spalten auswählen aus***Tabellenname* das oder die Kontrollkästchen der Tabellenspalte oder der Spalten, die dem Index als Nichtschlüsselspalten hinzugefügt werden sollen.  
  
11. Klicken Sie auf **OK**.  
  
12. Klicken Sie im Dialogfeld **Neuer Index** auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>So erstellen Sie einen Index mit Nichtschlüsselspalten  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Creates a nonclustered index on the Person.Address table with four included (nonkey) columns.   
    -- index key column is PostalCode and the nonkey columns are  
    -- AddressLine1, AddressLine2, City, and StateProvinceID.  
    CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
    GO  
    ```  

## <a name="related-content"></a>Verwandte Inhalte  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)    
[Handbuch zum SQL Server Indexentwurf](../../relational-databases/sql-server-index-design-guide.md)   
