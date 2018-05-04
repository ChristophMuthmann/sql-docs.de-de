---
title: GetURL-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dd0d5d2c-91fe-4b0f-a162-69d898ba176e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 005da5eaf520fa1233b3c8ddcf6d42dcf5d8882a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="geturl-method-sqlserverdatasource"></a>getURL-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt die URL zurück, die zum Herstellen einer Verbindung mit der Datenquelle verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , die die URL enthält.  
  
## <a name="remarks"></a>Hinweise  
 Aus Gründen der Sicherheit sollten Sie nicht das Kennwort enthalten, in der URL, die an die [SetURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) Methode. Der Grund hierfür ist, dass Java-Anwendungsserver von Drittanbietern oft den für die URL-Eigenschaft festgelegten Wert auf der Benutzeroberfläche für die Datenquellenkonfiguration anzeigen. Verwenden Sie stattdessen die [SetPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) Methode, um den Kennwortwert einzurichten. Java-Anwendungsserver zeigen kein in der Datenquelle festgelegtes Kennwort auf der Konfigurationsbenutzeroberfläche an.  
  
> [!NOTE]  
>  SetURL-Methode nicht vor dem Aufrufen der Methode "getURL" aufgerufen wird, gibt "getURL" den Wert von "SQLServer: / /".  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
