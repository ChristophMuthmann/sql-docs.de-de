---
title: RowDeleted-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5a42409119b1d0e4280e36d417fd4d149b7625a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="rowdeleted-method-sqlserverresultset"></a>RowDeleted-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob eine Zeile gelöscht wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** Wenn eine Zeile gelöscht wurde und löschungen ermittelt wurden. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese RowDeleted-Methode wird von der RowDeleted-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Eine gelöschte Zeile hinterlässt in einem Resultset ggf. eine sichtbare Lücke. Diese Methode kann verwendet werden, um Löcher in einem Resultset zu ermitteln. Der zurückgegebene Wert hängt davon ab, ob dies [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt löschungen kann ermittelt werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Gelöschte Zeilen für alle aktualisierbaren Cursortypen erkennt, obwohl die Erkennung für Vorwärtscursor und dynamische Cursor flüchtig ist.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
