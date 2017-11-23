---
title: "Löschen von Datenbankobjekten | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: deleting database objects
ms.assetid: dbb94fdf-c85b-477b-8e84-f830d259bade
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d8e3d5eba52076ae58337fb9579781cad10a5f42
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="lesson-3-1---deleting-database-objects"></a>Lektion 3-1: Löschen von Datenbankobjekten
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]Um dieses Lernprogramm vollständig zu entfernen, könnten Sie nur die Datenbank löschen. In diesem Thema führen Sie jedoch die erforderlichen Schritte aus, um jede Aktion rückgängig zu machen, die Sie im Lernprogramm ausgeführt haben.  
  
### <a name="removing-permissions-and-objects"></a>Entfernen von Berechtigungen und Objekten  
  
1.  Bevor Sie Objekte löschen, stellen Sie sicher, dass Sie sich in der richtigen Datenbank befinden:  
  
    ```  
    USE TestData;  
    GO  
    ```  
  
2.  Führen Sie die `REVOKE` -Anweisung aus, um die Ausführungsberechtigung für `Mary` in der gespeicherten Prozedur zu entfernen:  
  
    ```  
    REVOKE EXECUTE ON pr_Names FROM Mary;  
    GO  
  
    ```  
  
3.  Führen Sie die `DROP` -Anweisung aus, um die Berechtigung für `Mary` zum Zugriff auf die `TestData` -Datenbank zu entfernen:  
  
    ```  
    DROP USER Mary;  
    GO  
  
    ```  
  
4.  Führen Sie die `DROP` -Anweisung aus, um die Berechtigung für `Mary` zum Zugriff auf die Instanz von [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]zu entfernen:  
  
    ```  
    DROP LOGIN [<computer_name>\Mary];  
    GO  
  
    ```  
  
5.  Verwenden Sie die `DROP` -Anweisung zum Entfernen der gespeicherten Prozedur `pr_Names`:  
  
    ```  
    DROP PROC pr_Names;  
    GO  
  
    ```  
  
6.  Verwenden Sie die `DROP` -Anweisung zum Entfernen der `vw_Names`-Sicht:  
  
    ```  
    DROP View vw_Names;  
    GO  
  
    ```  
  
7.  Verwenden Sie die `DELETE` -Anweisung zum Entfernen von Datenzeilen aus der `Products` -Tabelle:  
  
    ```  
    DELETE FROM Products;  
    GO  
  
    ```  
  
8.  Verwenden Sie die `DROP` -Anweisung zum Entfernen der `Products` -Tabelle:  
  
    ```  
    DROP Table Products;  
    GO  
  
    ```  
  
9. Es ist nicht möglich, die `TestData` -Datenbank zu entfernen, während Sie sich in der Datenbank befinden. Wechseln Sie daher den Kontext zu einer anderen Datenbank, und verwenden Sie dann die `DROP` -Anweisung, um die `TestData` -Datenbank zu entfernen.  
  
    ```  
    USE MASTER;  
    GO  
    DROP DATABASE TestData;  
    GO  
  
    ```  
  
Damit ist das Lernprogramm zum Schreiben von [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen beendet. Beachten Sie, dass dieses Lernprogramm nur eine kurze Übersicht bietet und darin nicht alle Optionen der verwendeten Anweisungen beschrieben werden. Das Entwerfen und Erstellen einer effizienten Datenbankstruktur und das Konfigurieren des sicheren Zugriffs auf die Daten erfordern eine komplexere Datenbank als in diesem Lernprogramm gezeigt.  
  
## <a name="return-to-sql-server-tools-portal"></a>Zurück zum Portal für SQL Server-Tools  
[Lernprogramm: Schreiben von Transact-SQL-Anweisungen](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>Siehe auch  
[REVOKE &#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
[DROP USER &#40;Transact-SQL&#41;](../t-sql/statements/drop-user-transact-sql.md)  
[DROP LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/drop-login-transact-sql.md)  
[DROP PROCEDURE &#40;Transact-SQL&#41;](../t-sql/statements/drop-procedure-transact-sql.md)  
[DROP VIEW &#40;Transact-SQL&#41;](../t-sql/statements/drop-view-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../t-sql/statements/delete-transact-sql.md)  
[DROP TABLE &#40;Transact-SQL&#41;](../t-sql/statements/drop-table-transact-sql.md)  
[DROP DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/drop-database-transact-sql.md)  
  
  
  
