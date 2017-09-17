---
title: SQLServerXAResource-Klasse | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4c5e0cb02544e0ea96c29758f7c50179de48cf7a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverxaresource-class"></a>SQLServerXAResource-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt einen XAResource für den XA-verteilter Verwaltung Transaktionen.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Erweitert:** java.lang.Object  
  
 **Implementiert:** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Hinweise  
 XA-Transaktionen werden in implementiert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mit [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Distributed Transaction Manager (DTC). SQLServerXAResource-Klasse aufruft, um eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] erweiterte DLL-Datei mit dem Namen "sqljdbc_xa.dll", die Verbindung mit DTC herstellt. XA-Aufrufe, die von der SQLServerXAResource (XA_START, XA_END, XA_PREPARE usw.) empfangen wurden, werden den entsprechenden Aufrufen der DTC-Funktionen zugeordnet.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAResource-Elemente](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
