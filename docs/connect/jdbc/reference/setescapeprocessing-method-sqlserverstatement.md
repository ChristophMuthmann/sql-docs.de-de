---
title: SetEscapeProcessing-Methode (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.setEscapeProcessing
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ac0682e-e04c-4fdb-893b-92408d42051e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5e7c53393acca2a1ad95d590ce28fbd7b943b534
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setescapeprocessing-method-sqlserverstatement"></a>setEscapeProcessing-Methode (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Escapeverarbeitungsmodus fest.  
  
> [!NOTE]  
>  Die Escapeverarbeitung für [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ist immer aktiviert. Wird diese Methode auf "false" festgelegt, hat dies keine Auswirkungen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setEscapeProcessing(boolean enable)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Aktivieren*  
  
 **"true"** um die Escapeverarbeitung zu aktivieren. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetEscapeProcessing-Methode wird von der SetEscapeProcessing-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

