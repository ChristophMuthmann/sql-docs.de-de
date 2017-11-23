---
title: ISQLServerResultSet-Schnittstelle | Microsoft Docs
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
ms.assetid: 002496f7-8ec0-4267-b4e6-ba095e2ef306
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4967d971c31eb9a590a8da979cf0018c84845e27
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="isqlserverresultset-interface"></a>ISQLServerResultSet-Schnittstelle
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt ein JDBC-Resultset dar. Diese Schnittstelle wurde hinzugefügt, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Erweitert:** java.sql.ResultSet  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public interface ISQLServerResultSet  
```  
  
## <a name="remarks"></a>Hinweise  
 Diese Schnittstelle wird implementiert, indem [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
 Diese Schnittstelle legt die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifischen Methoden:  
  
|Methode|Weitere Informationen finden Sie unter|  
|------------|-------------------------------|  
|public microsoft.sql.DateTimeOffset getDateTimeOffset(int)|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-int-sqlserverresultset.md)|  
|public microsoft.sql.DateTimeOffset getDateTimeOffset(String)|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-java-lang-string-sqlserverresultset.md)|  
|public void updateDateTimeOffset(int, microsoft.sql.DateTimeOffset)|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-int-microsoft-sql-datetimeoffset-sqlserverresultset.md)|  
|public void updateDateTimeOffset(String, microsoft.sql.DateTimeOffset)|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-string-microsoft-sql-datetimeoffset-sqlserverresultset.md)|  
  
 Diese Schnittstelle legt die folgenden [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifische Felder:  
  
|Feld|Weitere Informationen finden Sie unter|  
|-----------|-------------------------------|  
|public static final int CONCUR_SS_OPTIMISTIC_CC|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|  
|public static final int CONCUR_SS_OPTIMISTIC_CCVAL|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|  
|public static final int CONCUR_SS_SCROLL_LOCKS|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_DIRECT_FORWARD_ONLY|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_SCROLL_DYNAMIC|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_SCROLL_KEYSET|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_SCROLL_STATIC|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
