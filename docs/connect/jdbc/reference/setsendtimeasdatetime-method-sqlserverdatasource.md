---
title: SetSendTimeAsDatetime-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f6a576e4cb3ef155092a1244bbf9e7c2fcaaadd5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
  

