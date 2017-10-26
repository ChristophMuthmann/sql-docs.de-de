---
title: SQLServerBlob-Konstruktor (SQLServerConnection, Byte) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76b8fe0d719a2eb5f53fe20502d0cd3fe35ca6eb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
 *Daten*  
  
 Ein **Byte** Array.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerBlob-Konstruktoren](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob-Elemente](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob-Klasse](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

