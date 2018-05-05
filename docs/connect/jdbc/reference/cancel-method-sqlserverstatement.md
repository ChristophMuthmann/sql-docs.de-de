---
title: Cancel-Methode (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.cancel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276bd9c1-9329-4fc9-9622-ed673c83a12d
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1386c17a98b623fee4bf25df949467f5996684d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cancel-method-sqlserverstatement"></a>cancel-Methode (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Bricht die SQL-Anweisung, die derzeit von diesem ausgeführt wird [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void cancel()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode "Abbrechen", wird von der Methode "Abbrechen", in der java.sql.Statement-Schnittstelle angegeben.  
  
 Beim Ausführen einer Anweisung, von der ein einzelnes, umfangreiches und schreibgeschütztes Vorwärts-Resultset erstellt wird, ist für Sie unter Umständen lediglich eine anfängliche Zeilengruppe des zurückgegebenen Resultsets von Interesse. In diesem Fall die Anwendung aufrufen kann die ["Abbrechen"](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) Methode des zugeordneten anweisungsobjekts vor dem Schließen des Ergebnis festlegen, um die Verarbeitungszeit beim Verwerfen der übrigen unnötige Zeilen zu minimieren. Wägen Sie bei der Entscheidung, ob Sie diese Methode verwenden möchten, die eingesparte Verarbeitungszeit gegen die Zeit und den Roundtrip zum Server ab, der zum Abbrechen der Ausführung erforderlich ist.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
