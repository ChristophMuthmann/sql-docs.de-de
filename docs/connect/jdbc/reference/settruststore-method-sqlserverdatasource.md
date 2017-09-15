---
title: SetTrustStore-Methode (SQLServerDataSource) | Microsoft Docs
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
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e6de008468da81facf98c039457f9248ddddc49
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="settruststore-method-sqlserverdatasource"></a>setTrustStore-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Pfad (einschließlich Dateiname) zur trustStore-Zertifikatsdatei fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>Parameter  
 *truststore-Eigenschaft*  
  
 Ein **Zeichenfolge** , die den Pfad (einschließlich Dateiname) zur TrustStore-Zertifikatsdatei enthält.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die TrustStore-Eigenschaft nicht angegeben oder auf Null gesetzt, wird die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] die Suchregeln der Trust-Manager-Factory Suchregeln, die zu verwendenden Zertifikatspeicher zu ermitteln. Der Standard-SunX509 TrustManagerFactory versucht, die Vertrauenswürdigkeitsinformationen in den folgenden Speicherorten in der angegebenen Reihenfolge zu finden:  
  
-   1. Eine von der Java Virtual Machine (JVM)-Systemeigenschaft "javax.net.ssl.trustStore" angegebene Datei  
  
-   2. "\<Java-Home >/Lib/Security/Jssecacerts" Datei.  
  
-   3. "\<Java-Home >/Lib/Security/Cacerts" Datei.  
  
 Weitere Informationen finden Sie in der Dokumentation zur SunX509 TrustManager-Schnittstelle auf der Website von Sun Microsystems.  
  
 Ist die trustStore-Eigenschaft auf eine Zeichenfolge oder auf eine leere Zeichenfolge ("") festgelegt, wird die trustStore-Datei anhand dieses Werts gesucht, um das SSL-Zertifikat des Servers zu überprüfen.  
  
 Die trustStorePassword-Eigenschaft kann zusammen mit der trustStore-Eigenschaft angegeben werden, und deren Wert wird zum Öffnen der trustStore-Datei verwendet. Weitere Informationen finden Sie unter [SetTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
