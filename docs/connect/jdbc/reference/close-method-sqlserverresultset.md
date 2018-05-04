---
title: Close-Methode (SQLServerResultSet) | Microsoft Docs
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
apiname:
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc2ea42ef473e1d68b12fa20427769e27937ff07
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="close-method-sqlserverresultset"></a>close-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Dies frei [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objektspezifischen Datenbank- und JDBC-Ressourcen sofort gewartet, sondern dies so erfolgen kann, wenn sie automatisch geschlossen wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Close-Methode wird von der close-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Ein SQLServerResultSet-Objekt wird automatisch geschlossen, indem die [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, das es generiert, wenn dieses SQLServerStatement-Objekt geschlossen, erneut ausführen oder zur Abrufen des nächsten Ergebnisses aus einer Sequenz von mehreren Ergebnissen . Ein SQLServerResultSet-Objekt wird auch automatisch geschlossen, wenn es sich um Garbage Collection durchgeführt wurde.  
  
 Beim Ausführen einer Anweisung, von der ein einzelnes, umfangreiches und schreibgeschütztes Vorwärts-Resultset erstellt wird, ist für Sie unter Umständen lediglich eine anfängliche Zeilengruppe des zurückgegebenen Resultsets von Interesse. In diesem Fall die Anwendung aufrufen kann die ["Abbrechen"](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) Methode des zugeordneten anweisungsobjekts vor dem Schließen des Ergebnis festlegen, um die Verarbeitungszeit beim Verwerfen der übrigen unnötige Zeilen zu minimieren. Wägen Sie bei der Entscheidung, ob Sie diese Methode verwenden möchten, die eingesparte Verarbeitungszeit gegen die Zeit und den Roundtrip zum Server ab, der zum Abbrechen der Ausführung erforderlich ist.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
