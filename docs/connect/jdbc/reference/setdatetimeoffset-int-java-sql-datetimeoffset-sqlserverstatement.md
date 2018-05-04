---
title: SetDateTimeOffset (Int, java.sql.DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 722250967bca8484f359d1e33a7541d34eb3ac79
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
|Zeit|Kann nur Folgendes einfügen: "hh:mm:ss[.nnnnnnn]"|  
|Datum|Kann nur Folgendes einfügen: "YYYY-MM-DD"|  
|datetime2|Kann nur Folgendes einfügen: "YYYY-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Siehe auch  
 [GetDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
