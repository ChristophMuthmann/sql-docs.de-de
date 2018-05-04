---
title: SSTRANSTIGHTLYCPLD-Feld (SQLServerXAResource) | Microsoft Docs
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
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apilocation:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apitype: Assembly
ms.assetid: 379857c3-9de1-4964-8782-32df317cbfbb
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02f95a1ac9a40cad4ce788edbaea064bd11bfd56
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>SSTRANSTIGHTLYCPLD-Feld (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Hierdurch werden eng verkoppelte XA-Transaktionen ermöglicht, die unterschiedliche XA-Verzweigungstransaktions-IDs (XIDs) aber dieselbe globale Transaktions-ID (GTRID) aufweisen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>Feldwert  
 Ein **Int** Wert (32768).  
  
## <a name="remarks"></a>Hinweise  
 Jede Transaktion wird anhand einer XA-Verzweigungstransaktions-ID (XID) und einer globalen Transaktions-ID (GTRID) identifiziert. Damit können die Anwendungen die eng verkoppelte XA-Transaktionen verwenden, die unterschiedlichen XIDs aber den gleichen GTRID haben, müssen Sie festlegen der [SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) für den Flagsparameter der Methode XAResource.start. Weitere Informationen zum Verwenden dieses Flags finden Sie unter [XA-Transaktionen](../../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAResource-Felder](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [SQLServerXAResource-Elemente](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource-Klasse](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
