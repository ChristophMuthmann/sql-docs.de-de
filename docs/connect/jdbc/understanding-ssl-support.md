---
title: "Grundlegendes zur SSL-Unterstützung | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82440c6d3ffe0ee0f2c2b9080328c0fed302cb31
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-ssl-support"></a>Grundlegendes zur SSL-Unterstützung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Beim Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], wenn die Anwendung, Verschlüsselung und die Instanz von anfordert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ist zur Unterstützung der SSL-Verschlüsselung konfiguriert die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] des SSL-Handshakes initiiert. Mithilfe des Handshakes können der Server und der Client die Verschlüsselungs- und Kryptografiealgorithmen aushandeln, mit denen Daten geschützt werden sollen. Nachdem der SSL-Handshake abgeschlossen wurde, können der Client und der Server die verschlüsselten Daten sicher senden. Während der SSL-Handshakes sendet der Server seine Zertifikat für öffentliche Schlüssel an den Client. Der Aussteller eines Zertifikats für öffentliche Schlüssel wird als Zertifizierungsstelle bezeichnet. Der Client ist dafür verantwortlich zu überprüfen, ob der Client der Zertifizierungsstelle vertraut.  
  
 Wenn die Anwendung keine Verschlüsselung anfordert, wird die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] wird nicht erzwungen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL-Verschlüsselung unterstützt. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz nicht zum Erzwingen der SSL-Verschlüsselung konfiguriert ist, eine Verbindung ohne Verschlüsselung hergestellt. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz zum Erzwingen der SSL-Verschlüsselung konfiguriert ist, aktiviert der Treiber automatisch SSL-Verschlüsselung beim Ausführen auf ordnungsgemäß konfigurierten Java Virtual Machine (JVM), oder andernfalls die Verbindung wird beendet und der Treiber löst einen Fehler.  
  
> [!NOTE]  
>  Stellen Sie sicher, dass den an übergebenen Wert **ServerName** entspricht genau der allgemeine Name (CN) oder DNS-Namen in den Antragstellernamen alternativen (SAN) in das Serverzertifikat für eine SSL-Verbindung erfolgreich hergestellt werden kann.  
  
> [!NOTE]  
>  Weitere Informationen zum Konfigurieren von SSL für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter dem Verschlüsseln von Verbindungen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Thema in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="remarks"></a>Hinweise  
 Damit können Anwendungen für die Verwendung von SSL-Verschlüsselung der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] wurde eingeführt, die folgenden Verbindungseigenschaften, beginnend mit der Version 1.2: **verschlüsseln**, **"TrustServerCertificate"**, **TrustStore**, **TrustStorePassword**, und **HostNameInCertificate**. Weitere Informationen finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Die folgende Tabelle enthält wie die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Version verhält sich, für mögliche Szenarien der SSL-Verbindung. In jedem Szenario wird ein anderer Satz von SSL-Verbindungseigenschaften verwendet. Die Tabelle schließt Folgendes ein:  
  
-   **leere**: "die Eigenschaft ist nicht in der Verbindungszeichenfolge vorhanden."  
  
-   **Wert**: "die Eigenschaft, die in der Verbindungszeichenfolge vorhanden ist und ihr Wert ist gültig."  
  
-   **alle**: "Es ist unerheblich, ob die Eigenschaft in der Verbindungszeichenfolge vorhanden oder ihr Wert ungültig ist"  
  
> [!NOTE]  
>  Das gleiche Verhalten trifft für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Benutzerauthentifizierung und integrierte Windows-Authentifizierung.  
  
|encrypt|trustServerCertificate|hostNameInCertificate|trustStore|trustStorePassword|Verhalten|  
|-------------|----------------------------|---------------------------|----------------|------------------------|--------------|  
|false oder blank|any|any|any|any|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] wird nicht erzwungen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL-Verschlüsselung unterstützt. Wenn der Server ein selbst signiertes Zertifikat aufweist, initiiert der Treiber den SSL-Zertifikataustausch. Das SSL-Zertifikat wird nicht überprüft, und nur die Anmeldeinformationen (im Anmeldepaket) werden verschlüsselt.<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch. Das SSL-Zertifikat wird nicht überprüft, die gesamte Kommunikation wird jedoch verschlüsselt.|  
|true|true|any|any|any|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch. Beachten Sie, dass bei der **"TrustServerCertificate"** Eigenschaftensatz wird auf "true", den Treiber das SSL-Zertifikat kann nicht überprüft werden.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
|true|false oder blank|leer|leer|leer|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch.<br /><br /> Der Treiber verwendet die **ServerName** -Eigenschaft auf den Verbindungs-URL das SSL-Serverzertifikat überprüfen und basieren auf Suchregeln der Trust-Manager-Factory, um zu bestimmen, welche zu verwendenden Zertifikatspeicher angegeben.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
|true|false oder blank|value|leer|leer|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch.<br /><br /> Der Treiber wird das SSL-Zertifikat Antragsteller-Wert überprüfen, indem der angegebene Wert für die **HostNameInCertificate** Eigenschaft.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
|true|false oder blank|leer|value|value|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch.<br /><br /> Der Treiber verwendet die **TrustStore** Eigenschaftswert angibt, der die TrustStore-Zertifikatsdatei zu suchen und **TrustStorePassword** Eigenschaftswert zum Überprüfen der Integrität der TrustStore-Datei.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
|true|false oder blank|leer|leer|value|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch.<br /><br /> Der Treiber verwendet die **TrustStorePassword** Eigenschaftswert zum Überprüfen der Integrität der Standarddatei TrustStore.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
|true|false oder blank|leer|value|leer|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch.<br /><br /> Der Treiber verwendet die **TrustStore** Eigenschaftswert angibt, der den Speicherort der Datei TrustStore zu suchen.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
|true|false oder blank|value|leer|value|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch.<br /><br /> Der Treiber verwendet die **TrustStorePassword** Eigenschaftswert zum Überprüfen der Integrität der Standarddatei TrustStore. Darüber hinaus verwendet der Treiber die **HostNameInCertificate** Eigenschaftswert zum Überprüfen des SSL-Zertifikats.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
|true|false oder blank|value|value|leer|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch.<br /><br /> Der Treiber verwendet die **TrustStore** Eigenschaftswert angibt, der den Speicherort der Datei TrustStore zu suchen. Darüber hinaus verwendet der Treiber die **HostNameInCertificate** Eigenschaftswert zum Überprüfen des SSL-Zertifikats.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
|true|false oder blank|value|value|value|Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anforderungen zum Verwenden von SSL-Verschlüsselung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Wenn der Server erfordert, dass der Client SSL-Verschlüsselung unterstützt oder der Server die Verschlüsselung unterstützt, initiiert der Treiber den SSL-Zertifikataustausch.<br /><br /> Der Treiber verwendet die **TrustStore** Eigenschaftswert angibt, der die TrustStore-Zertifikatsdatei zu suchen und **TrustStorePassword** Eigenschaftswert zum Überprüfen der Integrität der TrustStore-Datei. Darüber hinaus verwendet der Treiber die **HostNameInCertificate** Eigenschaftswert zum Überprüfen des SSL-Zertifikats.<br /><br /> Wenn der Server nicht für die Unterstützung der Verschlüsselung konfiguriert ist, löst der Treiber einen Fehler aus und trennt die Verbindung.|  
  
 Wenn die Encrypt-Eigenschaft, um festgelegt wird **"true"**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] verwendet JSSE-Standardsicherheitsanbieter der JVM zum Aushandeln der SSL-Verschlüsselung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Der Standardsicherheitsanbieter unterstützt möglicherweise nicht alle erforderlichen Funktionen zum erfolgreichen Aushandeln der SSL-Verschlüsselung. Beispielsweise unterstützt der Standardsicherheitsanbieter möglicherweise die Größe des öffentlichen RSA-Schlüssels verwendet wird, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL-Zertifikat. In diesem Fall löst der Standardsicherheitsanbieter möglicherweise einen Fehler aus, wodurch der JDBC-Treiber die Verbindung trennt. Führen Sie zum Beheben dieses Problems eine der folgenden Aktionen aus:  
  
-   Konfigurieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mit einem Serverzertifikat, das einen kleineren öffentlichen RSA-Schlüssel verfügt.  
  
-   Konfigurieren Sie die JVM Verwendung in einer anderen JSSE-Standardsicherheitsanbieter der "\<Java-Home > / lib/security/java.security" Sicherheitsdatei-Eigenschaften  
  
-   Verwenden Sie eine andere JVM.  
  
## <a name="validating-server-ssl-certificate"></a>Überprüfen des SSL-Serverzertifikats  
 Während der SSL-Handshakes sendet der Server seine Zertifikat für öffentliche Schlüssel an den Client. Der JDBC-Treiber oder Client muss überprüfen, ob das Serverzertifikat von einer Zertifizierungsstelle herausgegeben wurde, der der Client vertraut. Der Treiber erfordert, dass das Serverzertifikat die folgenden Bedingungen erfüllt:  
  
-   Das Zertifikat wurde von einer vertrauenswürdigen Zertifizierungsstelle ausgegeben.  
  
-   Das Zertifikat muss für die Serverauthentifizierung ausgestellt werden.  
  
-   Das Zertifikat ist nicht abgelaufen.  
  
-   Der allgemeine Name (CN) in den Betreff oder einen DNS-Namen in der Subject alternative Name (SAN) des Zertifikats genau entspricht der **ServerName** in der Verbindungszeichenfolge angegebene Wert oder, falls angegeben, die ** HostNameInCertificate** Eigenschaftswert.  
  
-   Ein DNS-Name kann Platzhalterzeichen enthalten. Aber die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt keine Platzhalterzeichen. D. h. abc.com stimmen nicht überein "*.com" jedoch \*".com" entspricht \*. com.  
  
## <a name="see-also"></a>Siehe auch  
 [Mithilfe von SSL-Verschlüsselung](../../connect/jdbc/using-ssl-encryption.md)   
 [Sichern von JDBC-Treiberanwendungen](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
