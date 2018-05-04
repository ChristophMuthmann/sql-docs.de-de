---
title: SetSelectMethod-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b562c12bef0a8057a13a8870bc6ae5dd0b4521b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>setSelectMethod-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Standardcursortyp, der für alle Resultsets verwendet wird, die erstellt werden, mithilfe dieses [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>Parameter  
 *selectMethod*  
  
 Ein **Zeichenfolge** Wert, der den Standardcursortyp enthält.  
  
## <a name="remarks"></a>Hinweise  
 "selectMethod" ist der Standardcursortyp, der für ein Resultset verwendet wird. Diese Eigenschaft ist nützlich für die Verarbeitung großer Resultsets ohne dass das gesamte Resultset im clientseitigen Speicher abgelegt wird. Wenn Sie die Eigenschaft auf "cursor" festlegen, können Sie einen serverseitigen Cursor erstellen, der jeweils kleinere Datenauschnitte abrufen kann. Wenn die SelectMethod-Eigenschaft nicht festgelegt ist, [GetSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md) gibt den Standardwert "Direct" zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
