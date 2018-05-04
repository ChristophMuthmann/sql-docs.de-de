---
title: SetCatalog-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91597c7a995fb0ecf810d3b0f58760c12784564e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
  
