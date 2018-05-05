---
title: GetSendTimeAsDatetime-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d9c9379a90dc85eb1579a8354816b8ee4abf93e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Diese Methode wurde hinzugefügt, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 Gibt die Einstellung von der **SendTimeAsDatetime** Connection-Eigenschaft.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn java.sql.Time-Werte als an den Server gesendet werden eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **"DateTime"** Typ. **"false"** , wenn java.sql.Time-Werte als an den Server gesendet werden eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **Zeit** Typ.  
  
## <a name="remarks"></a>Hinweise  
 Finden Sie unter [Festlegen der Verbindungseigenschaften](../../../connect/jdbc/setting-the-connection-properties.md) Weitere Informationen zu den **SendTimeAsDatetime** Connection-Eigenschaft.  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) können Sie programmgesteuert festlegen der **SendTimeAsDatetime** Connection-Eigenschaft.  
  
 Weitere Informationen finden Sie unter [konfigurieren wie java.sql.Time-Werte werden an den Server gesendet](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
