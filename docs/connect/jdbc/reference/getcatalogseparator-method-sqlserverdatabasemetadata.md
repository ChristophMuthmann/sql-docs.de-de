---
title: GetCatalogSeparator-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getCatalogSeparator
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0bbd6842-7210-432a-bef4-e15a63f5cc96
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5531ae6c62a8e0a588abc136a09e15171074013
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getcatalogseparator-method-sqlserverdatabasemetadata"></a>getCatalogSeparator-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die **Zeichenfolge** , die diese Datenbank wird als Trennzeichen zwischen einem Katalog- und Tabellenname verwendet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getCatalogSeparator()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** dem Katalogtrennzeichen.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetCatalogSeparator-Methode wird von der GetCatalogSeparator-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Bei Verwendung der [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank, diese Methode gibt einen Punkt (".") als Katalogtrennzeichen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
