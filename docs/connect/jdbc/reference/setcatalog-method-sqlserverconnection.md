---
title: SetCatalog-Methode (SQLServerConnection) | Microsoft Docs
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
apiname:
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0dbb0bbaa8a927ed34bd6d08f96a0f8713f31b94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="setcatalog-method-sqlserverconnection"></a>setCatalog-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebenen Katalognamen auf einen Teilbereich davon [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objektspezifischen-Datenbank, in dem Sie arbeiten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>Parameter  
 *catalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetCatalog-Methode wird durch die SetCatalog-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Die *Katalog* Argument wird mit Escapezeichen versehen, indem die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] automatisch. Mithilfe dieser Methode wird die Catalog-Eigenschaft für das Verbindungsobjekt. Diese wird auf keine andere Weise implizit festgelegt.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
