---
title: SetSendTimeAsDatetime-Methode (SQLServerDataSource) | Microsoft Docs
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
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15c5d74916499297596a0a22676c8e8fd5465b74
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>setSendTimeAsDatetime-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Diese Methode wurde hinzugefügt, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 Ändert die Einstellung von der **SendTimeAsDatetime** Connection-Eigenschaft.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sendTimeAsDateTime*  
  
 Ein boolescher Wert. Bei "true", bewirkt, dass java.sql.Time-Werte als an den Server gesendet werden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **"DateTime"** Typen. Bei "false", bewirkt, dass java.sql.Time-Werte als an den Server gesendet werden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **Zeit** Typen.  
  
## <a name="remarks"></a>Hinweise  
 [Von SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) gibt die Einstellung von der **SendTimeAsDatetime** Connection-Eigenschaft.  
  
 Weitere Informationen zu den **SendTimeAsDatetime** Verbindungseigenschaft finden Sie unter [Festlegen der Verbindungseigenschaften](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 Weitere Informationen finden Sie unter [konfigurieren wie java.sql.Time-Werte werden an den Server gesendet](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
