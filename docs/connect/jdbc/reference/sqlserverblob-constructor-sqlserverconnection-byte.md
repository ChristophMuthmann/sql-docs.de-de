---
title: SQLServerBlob-Konstruktor (SQLServerConnection, Byte) | Microsoft Docs
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
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1c7cc5041821fae51364271ad4ecf7666627cb0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>SQLServerBlob-Konstruktor (SQLServerConnection, Byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Initialisiert eine neue Instanz der dem [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) Klasse, sofern eine [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt und ein **Byte** Array.  
  
> [!NOTE]  
>  Diese Methode ist seit Version 2.0 des JDBC-Treibers veraltet. Verwenden Sie stattdessen die [CreateBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Verbindung*  
  
 Ein SQLServerConnection-Objekt.  
  
 *data*  
  
 Ein **Byte** Array.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerBlob-Konstruktoren](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob-Elemente](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob-Klasse](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
