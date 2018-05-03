---
title: Herstellen einer Verbindung mit SSL-Verschlüsselung | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86bdeaf93e6269294f15d98cbe0f0a0e88f5788b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-with-ssl-encryption"></a>Herstellen von Verbindungen mit SSL-Verschlüsselung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In diesem Beispiel wird veranschaulicht, wie Verbindungszeichenfolgeneigenschaften verwendet werden, mit denen Anwendungen Secure Sockets Layer (SSL)-Verschlüsselung in einer Java-Anwendung verwenden können. Weitere Informationen zu diesen neuen Verbindung string-Eigenschaften wie z. B. **verschlüsseln**, **"TrustServerCertificate"**, **TrustStore**,  **TrustStorePassword**, und **HostNameInCertificate**, finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Wenn die **verschlüsseln** -Eigenschaftensatz auf **"true"** und die **"TrustServerCertificate"** -Eigenschaftensatz auf **"true"**, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] kann nicht überprüft werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL-Zertifikat. Dies ist in der Regel zum Zulassen von Verbindungen in testumgebungen, z. B. Where erforderlich, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz verfügt über ein selbst signiertes Zertifikat.  
  
 Das folgende Codebeispiel veranschaulicht das Festlegen der **"TrustServerCertificate"** Eigenschaft in einer Verbindungszeichenfolge:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 Wenn die **verschlüsseln** -Eigenschaftensatz auf **"true"** und die **"TrustServerCertificate"** -Eigenschaftensatz auf **"false"**, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] überprüft die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL-Zertifikat. Das Überprüfen des Serverzertifikats ist Teil des SSL-Handshakes und stellt sicher, dass es sich bei dem Server tatsächlich um den Server handelt, mit dem eine Verbindung hergestellt werden soll. Überprüfen des Serverzertifikats muss die Vertrauensinformationen zur Verbindungszeit mithilfe angegeben werden **TrustStore** und **TrustStorePassword** Verbindungseigenschaften explizit oder mithilfe von Standardeinstellung für die Vertrauenswürdigkeit der zugrunde liegenden Java Virtual Machine (JVM) implizit speichern.  
  
 Die **TrustStore** Eigenschaft gibt den Pfad (einschließlich Dateiname) der TrustStore-Zertifikatsdatei, die die Liste der Zertifikate enthält, die der Client vertraut. Die **TrustStorePassword** Eigenschaft gibt an, das zum Überprüfen der Integrität der TrustStore-Daten verwendete Kennwort. Weitere Informationen zur Verwendung des standardvertrauensspeichers der JVM finden Sie unter der [Konfigurieren des Clients für SSL-Verschlüsselung](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md).  
  
 Das folgende Codebeispiel veranschaulicht das Festlegen der **TrustStore** und **TrustStorePassword** Eigenschaften in einer Verbindungszeichenfolge:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 Der JDBC-Treiber bietet eine zusätzliche Eigenschaft **HostNameInCertificate**, die den Hostnamen des Servers angibt. Der Wert dieser Eigenschaft muss mit der subject-Eigenschaft des Zertifikats übereinstimmen.  
  
 Im folgenden Codebeispiel wird veranschaulicht, wie die **HostNameInCertificate** Eigenschaft in einer Verbindungszeichenfolge:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  Alternativ können Sie den Wert von Verbindungseigenschaften festlegen, indem Sie mit dem entsprechenden **Setter** bereitgestellten Methoden die [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse.  
  
 Wenn die **verschlüsseln** -Eigenschaftensatz auf **"true"** und **"TrustServerCertificate"** -Eigenschaftensatz auf **"false"** und wenn der Servername in der Verbindungszeichenfolge entspricht nicht der Name des Servers in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL-Zertifikat, die folgende Fehlermeldung ausgegeben: der Treiber konnte keine sichere Verbindung mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mit Secure Sockets Layer (SSL)-Verschlüsselung. Fehler: "java.security.cert.CertificateException: Fehler bei der Servernamenüberprüfung in einem Zertifikat während der SSL (Secure Sockets Layer)-Initialisierung."  
  
## <a name="see-also"></a>Siehe auch  
 [Mithilfe von SSL-Verschlüsselung](../../connect/jdbc/using-ssl-encryption.md)   
 [Sichern von JDBC-Treiberanwendungen](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
