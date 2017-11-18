---
title: MoveToInsertRow-Methode (SQLServerResultSet) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.moveToInsertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 396367249ad1b786064d6fc5685e505590bbc4af
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="movetoinsertrow-method-sqlserverresultset"></a>MoveToInsertRow-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Versetzt den Cursor in die Einfügezeile.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void moveToInsertRow()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese MoveToInsertRow-Methode wird von der MoveToInsertRow-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Die aktuelle Cursorposition wird gespeichert und der Cursor in die Einfügezeile versetzt. Die Einfügezeile ist eine spezielle Zeile, die einem aktualisierbaren Resultset zugewiesen ist. Sie ist eigentlich ein Puffer, in dem eine neue Zeile durch Aufrufen der Aktualisierungsmethoden vor dem Hinzufügen der Zeile zum Resultset erstellt wird.  
  
 Nur die Updater, abrufen und [InsertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) Methoden aufgerufen werden können, wenn der Cursor in der Einfügezeile befindet. Alle Spalten in einem Resultset muss der angegebene Wert jedes Mal, wenn diese Methode aufgerufen wird und vor dem Aufrufen von InsertRow. Bevor eine Getter-Methode für einen Spaltenwert aufgerufen werden kann, muss eine Aktualisierungsmethode aufgerufen werden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

