---
title: Kopieren von Spalten von einer Tabelle in eine andere Tabelle (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 957858919b96ee580f1c352e77f95df065ca3a4a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>Kopieren von Spalten von einer Tabelle in eine andere Tabelle (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  In diesem Thema wird beschrieben, wie Sie Spalten einer Tabelle in eine andere Tabelle kopieren. Dabei kopieren Sie entweder nur die Spaltendefinition oder die Definition und Daten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , indem Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]verwenden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Security](#Security)  
  
-   **So kopieren Sie Spalten mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Wenn Sie eine Spalte mit einem Aliasdatentyp aus einer Datenbank in eine andere kopieren, steht der Aliasdatentyp in der Zieldatenbank möglicherweise nicht zur Verfügung. In diesem Fall wird der Spalte der ähnlichste Grunddatentyp zugewiesen, der in der Datenbank verfügbar ist.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>So kopieren Sie Spaltendefinitionen von einer Tabelle in eine andere  
  
1.  Öffnen Sie die Tabelle mit den zu kopierenden Spalten und diejenige, in die Sie die Spalten kopieren möchten, indem Sie mit der rechten Maustaste auf die Tabellen und dann auf **Entwerfen**klicken.  
  
2.  Klicken Sie auf die Registerkarte für die Tabelle mit den zu kopierenden Spalten, und wählen Sie diese Spalten aus.  
  
3.  Klicken Sie im Menü **Bearbeiten** auf den Befehl **Kopieren**.  
  
4.  Klicken Sie auf die Registerkarte der Tabelle, in die Sie die Spalten kopieren möchten.  
  
5.  Wählen Sie die Spalte aus, die den eingefügten Spalten folgen soll, und klicken Sie im Menü **Bearbeiten** auf **Einfügen**.  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>So kopieren Sie Daten von einer Tabelle in eine andere  
  
1.  Befolgen Sie die obigen Anweisungen zum Kopieren von Spaltendefinitionen.  
  
    > [!NOTE]  
    >  Bevor Sie Daten von einer Tabelle in eine andere kopieren, stellen Sie sicher, dass die Datentypen in den Zielspalten mit denen der Quellspalten kompatibel sind.  
  
2.  Öffnen eines neuen Fensters des Abfrage-Editors 

3.  Klicken Sie mit der rechten Maustaste auf den Abfrage-Editor, und klicken Sie dann auf **Abfrage in Editor entwerfen**. 

4.  Wählen Sie im Dialogfeld **Tabelle hinzufügen** die Quell- und Zieltabelle aus, klicken Sie auf **Hinzufügen**, und schließen Sie dann das Dialogfeld **Tabelle hinzufügen** . 

5.  Klicken Sie mit der rechten Maustaste in einem offenen Bereich des Abfrage-Editors, zeigen Sie auf **Typ ändern**, und klicken Sie dann auf **Ergebnisse einfügen**.  

6.  Wählen Sie im Dialogfeld **Zieltabelle für Anfügeabfrage auswählen** die Zieltabelle aus. 

7.  Klicken Sie im oberen Teil des Abfrage-Designers auf die Quellspalte in der Quelltabelle.

8. Der Abfrage-Designer hat jetzt eine Einfügeabfrage erstellt. Klicken Sie auf „OK“, um die Abfrage im ursprünglichen Fenster des Abfrage-Editors zu platzieren.  

9.  Führen Sie die Abfrage aus, um die Daten aus der Quelltabelle in der Zieltabelle einzufügen.

  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>So kopieren Sie Spaltendefinitionen von einer Tabelle in eine andere  
  
1.  Anhand von Transact-SQL-Anweisungen können Sie keine einzelnen Spalten aus einer Tabelle in eine andere vorhandene Tabelle kopieren. Mit SELECT INTO können Sie jedoch eine neue Tabelle in der Standarddateigruppe erstellen, und die Ergebniszeilen aus der Abfrage werden darin eingefügt. Weitere Informationen finden Sie unter [INTO-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-into-clause-transact-sql.md).  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>So kopieren Sie Daten von einer Tabelle in eine andere  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.EmployeeSales  
    ( BusinessEntityID   varchar(11) NOT NULL,  
      SalesYTD money NOT NULL  
    );  
    GO  
    INSERT INTO dbo.EmployeeSales  
        SELECT BusinessEntityID, SalesYTD   
        FROM Sales.SalesPerson;  
    GO  
    ```  
  
  
