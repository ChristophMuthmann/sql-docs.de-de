---
title: SetTrustStorePassword-Methode (SQLServerDataSource) | Microsoft Docs
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
apiname: setTrustStorePassword Method (SQLServerDataSource)
apilocation: setTrustStorePassword Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: fa87cbde-71cc-4f21-bc07-f8ba2b6a0a3f
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d4fe85b3875374e6a0dfc526998635dc38af0b2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="settruststorepassword-method-sqlserverdatasource"></a>setTrustStorePassword-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt das Kennwort fest, das zum Überprüfen der Integrität der trustStore-Daten verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setTrustStorePassword(java.lang.String trustStorePassword)  
```  
  
#### <a name="parameters"></a>Parameter  
 *trustStorePassword*  
  
 Ein **Zeichenfolge** , enthält das Kennwort, das zum Überprüfen der Integrität der TrustStore-Daten verwendet wird.  
  
## <a name="remarks"></a>Hinweise  
 Die trustStorePassword-Eigenschaft kann zusammen mit der trustStore-Eigenschaft angegeben werden, und deren Wert wird zum Prüfen der Integrität der trustStore-Datei verwendet.  
  
 Wenn die trustStore-Eigenschaft festgelegt ist, die trustStorePassword-Eigenschaft jedoch nicht festgelegt wurde, wird die Integrität von "trustStore" nicht überprüft.  
  
 Wenn die trustStore-Eigenschaft und die trustStorePassword-Eigenschaft nicht angegeben wurden, verwendet der Treiber die Java Virtual Machine (JVM)-Systemeigenschaften "javax.net.ssl.trustStore" und "javax.net.ssl.trustStorePassword". Wenn die Systemeigenschaft „javax.net.ssl.trustStorePassword“ nicht angegeben ist, wird die Integrität von „trustStore“ nicht überprüft.  
  
 Wenn die trustStore-Eigenschaft nicht festgelegt ist, die trustStorePassword-Eigenschaft jedoch festgelegt ist, verwendet der JDBC-Treiber die von „javax.net.ssl.trustStore“ angegebene Datei als Vertrauensspeicher, und die Integrität des Vertrauensspeichers wird mithilfe des angegebenen „trustStorePassword“ überprüft. Dies kann erforderlich sein, wenn in der Clientanwendung das Kennwort nicht in der JVM-Systemeigenschaft gespeichert werden soll.  
  
 Weitere Informationen finden Sie unter [Festlegen der Verbindungseigenschaften](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 Ab JDBC Driver 3.0 muss SQLServerDataSource.setTrustStorePassword vor dem Herstellen der Verbindung aufgerufen werden, wenn Sie SQLServerDataSource.setTrustStorePassword vor dem Binden der Datenquelleneigenschaften festlegen. Weitere Informationen finden Sie unter [SQLServerDataSource.getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
