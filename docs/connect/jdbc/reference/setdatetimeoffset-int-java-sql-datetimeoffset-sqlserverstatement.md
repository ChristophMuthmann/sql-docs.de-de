---
title: SetDateTimeOffset (Int, java.sql.DateTimeOffset) | Microsoft Docs
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
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b9b18af7823f8d02f80ba636fe57b5d6cd807770
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="setdatetimeoffsetint-javasqldatetimeoffset-sqlserverstatement"></a>setDateTimeOffset(int, java.sql.DateTimeOffset) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebenen Parameter auf den angegebenen DateTimeOffset-Wert fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setDateTimeOffset(int parameterIndex, DateTimeOffset dateTime)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterIndex*  
  
 Der Index der festzulegenden Spalte.  
  
 *"DateTimeOffset"*  
  
 Ein DateTimeOffset-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Das DateTimeOffset-Format lautet "YYYY-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM". Verwenden Sie die folgende Tabelle als Referenz.  
  
|SQL-Typ|Insert|  
|--------------|------------|  
|datetime|Kann nur Folgendes einfügen: "YYYY-MM-DD hh:mm:ss[.nnn]"|  
|smalldatetime|Kann nur Folgendes einfügen: "YYYY-MM-DD hh:mm:ss"|  
|Uhrzeit|Kann nur Folgendes einfügen: "hh:mm:ss[.nnnnnnn]"|  
|Datum|Kann nur Folgendes einfügen: "YYYY-MM-DD"|  
|datetime2|Kann nur Folgendes einfügen: "YYYY-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Siehe auch  
 [GetDateTimeOffset &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
