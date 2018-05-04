---
title: SetURL-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd635d0b4adc5b7424b028a831baa5856d0c50ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="seturl-method-sqlserverdatasource"></a>setURL-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt die URL, die für die Verbindung mit der Datenquelle verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>Parameter  
 *URL*  
  
 Ein **Zeichenfolge** , die die URL enthält.  
  
## <a name="remarks"></a>Hinweise  
 Aus Gründen der Sicherheit sollten Sie das Kennwort nicht in der URL für die SetURL-Methode enthalten. Der Grund hierfür ist, dass Java-Anwendungsserver von Drittanbietern oft den für die URL-Eigenschaft festgelegten Wert auf der Benutzeroberfläche für die Datenquellenkonfiguration anzeigen. Verwenden Sie stattdessen die [SetPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) Methode, um den Kennwortwert einzurichten. Java-Anwendungsserver zeigen kein in der Datenquelle festgelegtes Kennwort auf der Konfigurationsbenutzeroberfläche an.  
  
> [!NOTE]  
>  Wenn die SetURL-Methode nicht, vor dem Aufruf aufgerufen wird der ["getURL"](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md) -Methode "getURL" gibt den Standardwert "SQLServer: / /".  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
