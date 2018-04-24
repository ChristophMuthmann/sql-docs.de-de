---
title: Ändern von Spalten (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- modifying data types
- column data types [SQL Server]
- data types [SQL Server], columns
ms.assetid: b67b95c5-61ef-4bd8-9a3e-1640eb7583ac
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7ffdd8c6eaa007b0b06b69c02f37ef54a9299f92
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="modify-columns-database-engine"></a>Ändern von Spalten (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können den Datentyp einer Spalte in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]ändern.  
  
> [!WARNING]  
>  Das Ändern des Datentyps einer Spalte, die bereits Daten enthält, kann zu einem dauerhaften Datenverlust führen, wenn die vorhandenen Daten in den neuen Typ konvertiert werden. Außerdem können Code und Anwendungen, die von der geänderten Spalte abhängen, womöglich nicht mehr ausgeführt werden. Dies schließt Abfragen, Sichten, gespeicherte Prozeduren, benutzerdefinierte Funktionen und Clientanwendungen ein. Beachten Sie, dass dabei ein Fehler durch Verkettung weitere Fehler nach sich ziehen kann. Beispielsweise kann eine gespeicherte Prozedur, die eine von der geänderten Spalte abhängige benutzerdefinierte Funktion aufruft, möglicherweise nicht mehr ausgeführt werden. Bedenken Sie sorgfältig die Konsequenzen, bevor Sie Änderungen an einer Spalte vornehmen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So ändern Sie den Datentyp einer Spalte mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>So ändern Sie den Datentyp einer Spalte  
  
1.  Klicken Sie im **Objekt-Explorer**mit der rechten Maustaste auf die Tabelle mit den Spalten, für die Sie Dezimalstellen ändern möchten, und klicken Sie auf **Entwerfen**.  
  
2.  Wählen Sie die Spalte aus, deren Datentyp Sie ändern möchten.  
  
3.  Klicken Sie auf der Registerkarte **Spalteneigenschaften** auf die Datenblattzelle der Eigenschaft **Datentyp** , und wählen Sie aus der Dropdownliste einen neuen Datentyp aus.  
  
4.  Klicken Sie im Menü **Datei** auf **Speichern** > *Tabellenname*.  
  
> [!NOTE]  
>  Wenn Sie den Datentyp einer Spalte ändern, wendet der Tabellen-Designer die Standardlänge des neuen Datentyps an, auch wenn Sie zuvor eine andere Länge angegeben haben. Legen Sie deshalb die Datentyplänge erst nach dem Ändern des Datentyps fest.  
  
> [!WARNING]  
>  Wenn Sie versuchen, den Datentyp einer Spalte zu ändern, die sich auf andere Tabellen bezieht, fordert Tabellen-Designer Sie auf zu bestätigen, dass die Änderung auch an den Spalten in den anderen Tabellen vorgenommen werden soll.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>So ändern Sie den Datentyp einer Spalte  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    CREATE TABLE dbo.doc_exy (column_a INT ) ;  
    GO  
    INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
    GO  
    ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
    GO  
  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
  
