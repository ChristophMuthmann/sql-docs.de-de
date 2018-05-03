---
title: SQLServerException-Konstruktor (java.lang.Object, java.lang.String, java.lang.String, Int, Boolean) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: daa4981f2ebb51c40725c1dd6e08935167b91914
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>SQLServerException-Konstruktor (java.lang.Object, java.lang.String, java.lang.String, Int, Boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Initialisiert eine neue Instanz der der [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) Klasse, sofern ein **Objekt**, **Zeichenfolge** -Objekt, eine **Zeichenfolge** -Objekt, das eine **Int**, und ein **booleschen**.

## <a name="syntax"></a>Syntax  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parameter  
 *obj*  
  
 Der e/a-Puffer, der die Ausnahme generiert hat.

 *errText*  
  
 Eine Zeichenfolge mit dem Fehlertext.
  
 *sqlState*  
  
 Ein Enum-Objekt, das den SQL-Status enthält.
 
 *errNum*  
  
 Einen int-Wert, der den Fehlercode für die Ausnahme enthalten.
 
 *bStack*  
  
 Ein boolescher Wert, der angibt, ob die stapelüberwachung generiert werden soll.
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerException-Konstruktoren](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException-Elemente](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException-Klasse](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
