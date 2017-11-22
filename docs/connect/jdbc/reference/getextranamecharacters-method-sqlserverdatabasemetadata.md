---
title: GetExtraNameCharacters-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
apiname: SQLServerDatabaseMetaData.getExtraNameCharacters
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: a22becfe-0f07-4a15-8d11-06d4054b2369
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1b27ce9ea2a33db729a8415e58fb6d56759874fe
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getextranamecharacters-method-sqlserverdatabasemetadata"></a>getExtraNameCharacters-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft alle zusätzlichen Zeichen ab, die in Bezeichnernamen ohne Anführungszeichen verwendet werden können (beispielsweise Zeichen, die über "a - z", "A - Z", "0 - 9" und "_" hinausgehen).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getExtraNameCharacters()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , das die zusätzlichen Zeichen enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetExtraNameCharacters-Methode wird von der GetExtraNameCharacters-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Bei Verwendung der [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank, gibt diese Methode $ "," # "zurück und @ zusätzliche Zeichen einzuschleusen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
