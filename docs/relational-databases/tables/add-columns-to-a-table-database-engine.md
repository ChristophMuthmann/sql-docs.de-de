---
title: Hinzufügen von Spalten zu einer Tabelle (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/27/2016
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
- inserting columns
- columns [SQL Server], adding
- adding columns
ms.assetid: abeb8d52-d562-4e29-9e1e-2923ae874859
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c4aacbc8abc1b454acd0a27cac9c8dc1a089f30
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="add-columns-to-a-table-database-engine"></a>Hinzufügen von Spalten zu einer Tabelle (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [Hinzufügen von Spalten zu einer Tabelle (Datenbankmodul)](https://msdn.microsoft.com/en-US/library/ms190238(SQL.120).aspx).


  In diesem Thema wird beschrieben, wie mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Tabellenspalten in [!INCLUDE[tsql](../../includes/tsql-md.md)]hinzugefügt werden können.  

  ##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Wenn Spalten mithilfe der ALTER TABLE-Anweisung zu einer Tabelle hinzugefügt werden, dann werden diese Spalten automatisch am Ende der Tabelle hinzugefügt. Wenn die Spalten in einer bestimmten Reihenfolge in der Tabelle eingefügt werden sollen, verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Beachten Sie jedoch, dass dies keine Best Practice für den Datenbankentwurf-ist. Best Practice ist, in der Anwendung oder auf der Abfrageebene die Reihenfolge anzugeben, in der die Spalten zurückgegeben werden sollen. Sie sollten sich nicht darauf verlassen, dass bei Verwendung von SELECT * alle Spalten in der Reihenfolge, in der sie in der Tabelle definiert worden sind, zurückgegeben werden. Geben Sie die Spalten in Abfragen und Anwendungen immer namentlich in der Reihenfolge an, in der sie angezeigt werden sollen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-insert-columns-into-a-table-with-table-designer"></a>So fügen Sie mit dem Tabellen-Designer Spalten in eine Tabelle ein  
  
1.  Klicken Sie im **Objekt-Explorer**mit der rechten Maustaste auf die Tabelle, der Sie Spalten hinzufügen möchten, und klicken Sie dann auf **Entwerfen**.  
  
2.  Klicken Sie auf die leere Zelle in der Spalte **Spaltenname** .  
  
3.  Geben Sie den Spaltennamen in die Zelle ein. Der Spaltenname muss angegeben werden.  
  
4.  Drücken Sie die TAB-TASTE, um zu der Zelle **Datentyp** zu gelangen, und wählen Sie in der Dropdownliste einen Datentyp aus. Dieser Wert ist obligatorisch. Wenn Sie keinen Wert auswählen, wird der Standardwert verwendet.  
  
    > [!NOTE]  
    >  Sie können den Standardwert im Dialogfeld **Optionen** unter **Datenbanktools**ändern.  
  
5.  Definieren Sie auf der Registerkarte **Spalteneigenschaften** weitere Spalteneigenschaften.  
  
    > [!NOTE]  
    >  Die Standardwerte für die Spalteneigenschaften werden hinzugefügt, wenn Sie eine neue Spalte erstellen. Sie können die Werte jedoch auf der Registerkarte **Spalteneigenschaften** ändern.  
  
6.  Wenn Sie die gewünschten Spalten hinzugefügt haben, wählen Sie im Menü **Datei** die Option **Speichern***table name*aus.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-insert-columns-into-a-table"></a>So fügen Sie Spalten eine neue Tabelle ein  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Im folgenden Beispiel werden der Tabelle `dbo.doc_exa`zwei Spalten hinzugefügt. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
```  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL, column_c INT NULL ;  
```  
  
####  <a name="FollowUp"></a> Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
