---
title: "Konfigurieren des Clients für SSL-Verschlüsselung | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5c395fcd8ae12a91db5dcd7bf26f8d81589d2f6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-the-client-for-ssl-encryption"></a>Konfigurieren des Clients für SSL-Verschlüsselung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oder Client muss, um sicherzustellen, dass der Server den richtigen Server und das Serverzertifikat herausgegeben wurde von einer Zertifizierungsstelle, die der Client vertraut. Zum Überprüfen des Serverzertifikats müssen die Informationen zur Vertrauenswürdigkeit zur Verbindungszeit angegeben werden. Außerdem muss der Aussteller des Serverzertifikats eine Zertifizierungsstelle sein, der der Client vertraut.  
  
 In diesem Thema wird zuerst beschrieben, wie die Vertrauenswürdigkeitsinformationen auf dem Clientcomputer angegeben werden. Anschließend wird das Importieren eines Serverzertifikats in den Vertrauensspeicher des Clientcomputers erläutert, wenn die Instanz des Secure Sockets Layer (SSL)-Zertifikats von SQL Server von einer privaten Zertifizierungsstelle veröffentlicht wird.  
  
 Weitere Informationen zum Überprüfen des Serverzertifikats finden Sie im Abschnitt "SSL-Serverzertifikat überprüfen" im [Grundlegendes zur SSL-Unterstützung](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="configuring-the-client-trust-store"></a>Konfigurieren des Clientvertrauensspeichers  
 Überprüfen des Serverzertifikats muss die Vertrauensinformationen zur Verbindungszeit mithilfe angegeben werden muss **TrustStore** und **TrustStorePassword** Verbindungseigenschaften explizit oder durch verwenden implizit standardvertrauensspeichers der zugrunde liegenden Java Virtual Machine (JVM). Weitere Informationen zum Festlegen der **TrustStore** und **TrustStorePassword** Eigenschaften in einer Verbindungszeichenfolge finden Sie unter [Herstellen einer Verbindung mit SSL-Verschlüsselung](../../connect/jdbc/connecting-with-ssl-encryption.md).  
  
 Wenn die **TrustStore** Eigenschaft ist nicht angegeben oder auf Null gesetzt, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Sicherheitsanbieter der zugrunde liegenden JVM Java Secure Socket Extension (SunJSSE) basieren. Der SunJSSE-Anbieter stellt eine TrustManager, die verwendet wird, überprüfen Sie anhand der in einem Vertrauensspeicher bereitgestellten Vertrauensinformationen von SQL Server zurückgegebenen x. 509-Zertifikate.  
  
 Die TrustManager versucht, den Standard-TrustStore in der folgenden Suchreihenfolge zu suchen:  
  
-   Wenn die Systemeigenschaft "javax.NET.SSL.trustStore""definiert ist, versucht der TrustManager Standarddatei TrustStore zu ermitteln, indem Sie unter Verwendung des von der Systemeigenschaft angegebenen Dateinamens.  
  
-   Wenn die Systemeigenschaft "javax.NET.SSL.trustStore""nicht angegeben wurde und die Datei"\<Java-Home >/Lib/Security/Jssecacerts "vorhanden ist, wird diese Datei verwendet.  
  
-   Wenn die Datei "\<Java-Home >/Lib/Security/Cacerts" vorhanden ist, wird diese Datei verwendet.  
  
 Weitere Informationen finden Sie in der Dokumentation zur SUNX509 TrustManager-Schnittstelle auf der Sun Microsystems-Website.  
  
 Durch die Java Runtime-Umgebung können Sie die trustStore-Systemeigenschaft und die trustStorePassword-Systemeigenschaft wie folgt festlegen:  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 In diesem Fall verwenden alle Anwendungen, die auf dieser JVM ausgeführt werden, diese Einstellungen als Standard. Um die Standardeinstellungen in Ihrer Anwendung zu überschreiben, sollten Sie ist die **TrustStore** und **TrustStorePassword** Verbindungseigenschaften in der Verbindungszeichenfolge oder in der entsprechenden der Setter-Methode der [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse.  
  
 Darüber hinaus können Sie konfigurieren und verwalten Sie die standardvertrauensspeicherdateien wie z. B. "\<Java-Home >/Lib/Security/Jssecacerts" und "\<Java-Home >/Lib/Security/Cacerts". Verwenden Sie hierzu das JAVA-Hilfsprogramm "keytool", das mit der JRE (Java Runtime Environment) installiert wird. Weitere Informationen zum Hilfsprogramm "keytool" finden Sie in der Dokumentation zu keytool auf der Sun Microsystems-Website.  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>Importieren des Serverzertifikats in den Vertrauensspeicher  
 Während des SSL-Handshakes sendet der Server sein Zertifikat für öffentliche Schlüssel an den Client. Der Aussteller eines Zertifikats für öffentliche Schlüssel wird als Zertifizierungsstelle bezeichnet. Der Client muss sicherstellen, dass der Client der Zertifizierungsstelle vertraut. Dies wird erreicht, indem der öffentliche Schlüssel von vertrauenswürdigen Zertifizierungsstellen im Voraus bekannt ist. Normalerweise wird die JVM mit einem vordefinierten Satz vertrauenswürdiger Zertifizierungsstellen geliefert.  
  
 Wenn die Instanz des Secure Sockets Layer (SSL)-Zertifikats von SQL Server von einer privaten Zertifizierungsstelle veröffentlicht wird, müssen Sie das Zertifikat der Zertifizierungsstelle der Liste der vertrauenswürdigen Zertifikate im Vertrauensspeicher des Clientcomputers hinzufügen.  
  
 Zu diesem Zweck verwenden Sie das JAVA-"Keytool"-Dienstprogramm, das mit der JRE (Java Runtime Environment) installiert ist. Mit der folgenden Eingabeaufforderung wird die Verwendung des Hilfsprogramms "keytool" zum Importieren eines Zertifikats aus einer Datei veranschaulicht:  
  
```  
keytool -import -v -trustcacerts -alias myServer -file caCert.cer -keystore truststore.ks  
```  
  
 Im Beispiel wird die Datei "caCert.cer" als Zertifikatsdatei verwendet. Sie müssen diese Zertifikatsdatei vom Server abrufen. In den folgenden Schritten wird erläutert, wie das Serverzertifikat in eine Datei exportiert wird:  
  
1.  Klicken Sie auf Start, klicken Sie auf Ausführen, und geben Sie MMC ein. (MMC ist die Abkürzung für Microsoft Management Console.)  
  
2.  Öffnen Sie in MMC die Zertifikate.  
  
3.  Erweitern Sie Eigene Zertifikate und dann Zertifikate.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Serverzertifikat, und wählen Sie dann unter Alle Aufgaben die Option Exportieren aus.  
  
5.  Klicken Sie auf Weiter, um das Dialogfeld Willkommen des Zertifikatexport-Assistenten zu überspringen.  
  
6.  Stellen Sie sicher, dass "Nein, privaten Schlüssel nicht exportieren" ausgewählt ist, und klicken Sie dann auf Weiter.  
  
7.  Stellen Sie sicher, dass DER-codiert-binär X.509 (.CER) oder Base-64-codiert X.509 (.CER) ausgewählt ist, und klicken Sie dann auf Weiter.  
  
8.  Geben Sie einen Namen für die Exportdatei ein.  
  
9. Klicken Sie auf Weiter, und klicken Sie dann auf Fertig stellen, um das Zertifikat zu exportieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Mithilfe von SSL-Verschlüsselung](../../connect/jdbc/using-ssl-encryption.md)   
 [Sichern von JDBC-Treiberanwendungen](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  

