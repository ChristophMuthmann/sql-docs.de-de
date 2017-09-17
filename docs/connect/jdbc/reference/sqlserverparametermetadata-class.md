---
title: SQLServerParameterMetaData-Klasse | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 836d6d90405e42df25a9bffb025a6113268560c8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverparametermetadata-class"></a>SQLServerParameterMetaData-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt die Metadaten für die Parameter vorbereiteter Anweisungen dar.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Erweitert:** java.lang.Object  
  
 **Implementiert:** java.sql.ParameterMetaData  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>Hinweise  
 Zum Abrufen der Metadaten von Parametern werden vorbereitete Anweisungen mit SET FMT ONLY ausgeführt. Von aufrufbaren Anweisungen wird "sp_sproc_columns" aufgerufen, um Namen und Metadaten für die Prozedurparameter abzurufen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerParameterMetaData-Elemente](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
