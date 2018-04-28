---
title: Verwenden eine SQL-Anweisung zum Ändern von Daten | Microsoft Docs
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
ms.topic: article
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ac1d0c5ada6d7895384e6133de189818e8cf824
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-an-sql-statement-to-modify-data"></a>Ändern von Daten mit SQL-Anweisungen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  So ändern Sie die Daten, die in enthalten ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe einer SQL-Anweisung können Sie die [ExecuteUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse. Die ExecuteUpdate-Methode wird die SQL-Anweisung zur Verarbeitung an die Datenbank übergeben, und dann einen Wert, der die Anzahl der Zeilen angibt, die betroffen sind zurück.  
  
 Zu diesem Zweck müssen Sie zuerst ein SQLServerStatement-Objekt erstellen, mit der [CreateStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, eine SQL-Anweisung erstellt, die mit der Tabelle neue Daten hinzugefügt und dann die Anweisung wird ausgeführt und der Rückgabewert wird angezeigt.  
  
 [!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]  
  
> [!NOTE]  
>  Wenn Sie eine SQL-Anweisung verwenden müssen, die Parameter zum Ändern der Daten in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank sollten Sie verwenden die [ExecuteUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) Methode der [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse.  
>   
>  Wenn die Spalte, in die Daten eingefügt werden sollen, Sonderzeichen wie Leerzeichen enthält, müssen Sie die einzufügenden Werte angeben, auch wenn es sich um die Standardwerte handelt. Andernfalls schlägt die Einfügeoperation fehl.  
>   
>  Wenn der JDBC-Treiber alle Updatezählungen zurückgeben soll, einschließlich der Updatezählungen, die von eventuell ausgelösten Triggern zurückgegeben werden, müssen Sie die lastUpdateCount-Verbindungseigenschaft auf "false" setzen. Weitere Informationen zur LastUpdateCount-Eigenschaft finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
