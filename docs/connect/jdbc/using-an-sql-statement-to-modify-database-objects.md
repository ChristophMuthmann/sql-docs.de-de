---
title: Verwenden eine SQL-Anweisung zum Ändern von Datenbankobjekten | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 809ad678f6257e7e2cdc4af5915f5d4902a5c144
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>Ändern von Datenbankobjekten mit SQL-Anweisungen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  So ändern Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbankobjekte mithilfe einer SQL­Anweisung, können Sie die [ExecuteUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse. Die ExecuteUpdate-Methode wird die SQL-Anweisung zur Verarbeitung an die Datenbank übergeben, und kehren Sie dann den Wert 0 zurück, da keine Zeilen betroffen sind.  
  
 Zu diesem Zweck müssen Sie zuerst ein SQLServerStatement-Objekt erstellen, mit der [CreateStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse.  
  
> [!NOTE]  
>  SQL-Anweisungen, die Objekte in einer Datenbank ändern, werden DDL-Anweisungen (Data Definition Language) genannt. Dazu gehören Anweisungen wie CREATE TABLE, DROP TABLE, CREATE INDEX und DROP INDEX. Weitere Informationen zu den Arten von DDL-Anweisungen, die von unterstützt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, eine SQL­Anweisung erstellt, die die einfache Testtabelle in der Datenbank erstellen und die Anweisung wird ausgeführt, und der Rückgabewert wird angezeigt.  
  
 [!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
