---
title: Konfigurieren, wie java.sql.Time-Werte an den Server gesendet werden | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e2e91550767715616599c2720c99b864363a185
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Konfigurieren der Art und Weise, wie java.sql.Time-Werte an den Server gesendet werden
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Wenn Sie ein java.sql.Time-Objekt oder den java.sql.Types.TIME-JDBC-Typ zum Festlegen eines Parameters verwenden, können Sie konfigurieren, wie der java.sql.Time-Wert an den Server gesendet wird. entweder als eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Zeit** Typ oder als eine **"DateTime"** Typ.  
  
 Dies trifft zu, wenn eine der folgenden Methoden verwendet wird:  
  
-   [SQLServerCallableStatement.registerOutParameter (Int, Int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter (Int, Int, Int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 Sie können konfigurieren, wie der java.sql.Time-Wert gesendet wird, mithilfe der **SendTimeAsDatetime** Connection-Eigenschaft. Weitere Informationen finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Sie können den Wert programmgesteuert ändern die **SendTimeAsDatetime** -Verbindungseigenschaft mit [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] vor [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] unterstützen nicht die **Zeit** -Datentyp, damit Anwendungen, die in der Regel mithilfe von java.sql.Time java.sql.Time speichern Werte entweder als **"DateTime"** oder **Smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen.  
  
 Wenn Sie verwenden möchten die **"DateTime"** und **Smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen beim Arbeiten mit java.sql.Time-Werten, die Sie festlegen sollten die **SendTimeAsDatetime** die Verbindungseigenschaft auf **"true"**. Wenn Sie verwenden möchten die **Zeit** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Daten angegeben wird, wenn Arbeiten mit java.sql.Time-Werte können Sie festlegen sollten die **SendTimeAsDatetime** Verbindungseigenschaft auf **"false"**.  
  
 Beachten Sie, dass beim Senden von java.sql.Time-Werte in einen Parameter, deren Datentyp ebenfalls speichern kann des Datums, das Standarddaten unterscheiden sich abhängig davon, ob der java.sql.Time-Wert gesendet wird, als ein **"DateTime"** (1/1/1970) oder **Zeit** Wert (1/1/1900). Weitere Informationen zu datenkonvertierungen beim Senden von Daten an eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Verwenden von Datums- und Zeitdaten](http://go.microsoft.com/fwlink/?LinkID=145211).  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0 **SendTimeAsDatetime** ist standardmäßig "true". In einer zukünftigen Version die **SendTimeAsDatetime** Connection-Eigenschaft möglicherweise standardmäßig auf "false" festgelegt werden.  
  
 Um sicherzustellen, dass Ihre Anwendung wird weiterhin erwartungsgemäß unabhängig vom Standardwert von der **SendTimeAsDatetime** Connection-Eigenschaft Sie können:  
  
-   Beim Arbeiten mit java.sql.Time verwenden die **Zeit** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp.  
  
-   Beim Arbeiten mit java.sql.Timestamp verwenden die **"DateTime"**, **Smalldatetime**, und **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen.  
  
Beachten Sie, dass diese SendTimeAsDatetime für verschlüsselte Spalten "false" sein muss, wie die verschlüsselte Spalten nicht die Konvertierung von Zeit in "DateTime" unterstützen. Ab Microsoft JDBC Driver 6.0 für SQL Server, SQLServerConnection-Klasse verfügt über die beiden folgenden Methoden können Sie den Wert der Eigenschaft SendTimeAsDatetime festlegen/abrufen.

```
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
