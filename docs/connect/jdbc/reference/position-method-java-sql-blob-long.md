---
title: Position-Methode (java.sql.Blob, long) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerBlob.position (java.sql.Blob.long)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ebd005e5-f6c5-4789-87f9-d2fdacd35060
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a6289e392663ccd3d5bf25c94e7162bfe507630d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="position-method-javasqlblob-long"></a>position-Methode (java.sql.Blob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt die Position eines angegebenen Musters im BLOB auf der Grundlage des angegebenen Musters und des Startindexes zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public long position(java.sql.Blob pattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Muster*  
  
 Das zu suchende Muster.  
  
 *Starten*  
  
 Der Startindex, in dem gesucht werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **lange** Wert, der die Position, in denen das Muster gefunden wurde, oder -1, wenn es nicht gefunden wurde.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese Position-Methode wird von der Position-Methode in der java.sql.Blob-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Positionieren Sie die Methode &#40; SQLServerBlob &#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [SQLServerBlob-Methoden](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob-Elemente](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob-Klasse](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
