---
title: Häufig gestellte Fragen (FAQ) zu JDBC-Treiber | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b2872e0674a8195b2460c229a1244cc399a936b5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>Häufig gestellte Fragen (FAQ) zu JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dieser Artikel enthält Antworten auf häufig gestellte Fragen zum Microsoft JDBC-Treiber für SQL Server.  
  
## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen  
**Wie kann ich Verbessern der JDBC-Treiber?**  
Der JDBC-Treiber ist Open Source- und der Quellcode befinden sich auf [GitHub](https://github.com/microsoft/mssql-jdbc). Sie können den Treiber verbessern, indem die Einreichung Probleme und die CodeBase verwendet werden sollen.

**Welche Versionen von SQL Server und Java stimmen Treibers unterstützt?**  
 Finden Sie unter der [Microsoft JDBC Driver für SQL Server-Supportmatrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) Informationen.  
  
 **Was sollte ich noch wissen meinen Treiber aktualisiere?**  
 Der Microsoft JDBC Driver 6.4 unterstützt der JDBC 4.1, 4.2 und 4.3 (teilweise)-Spezifikationen und enthält drei JAR-Klassenbibliotheken im Installationspaket wie folgt:  
  
|JAR|JDBC-Spezifikation|JDK-Version|  
|-|-|-|  
|mssql-jdbc-6.4.0.jre9.jar|JDBC 4.3 (teilweise), 4.2 und 4.1|JDK 9.0|  
|mssql-jdbc-6.4.0.jre8.jar|JDBC 4.2 und 4.1|JDK 8.0|  
|mssql-jdbc-6.4.0.jre7.jar|JDBC 4.1|JDK 7.0|  

 Die Microsoft JDBC Driver 6.2 unterstützt die JDBC 4.0, 4.1 und 4.2-Spezifikation und enthält zwei JAR-Klassenbibliotheken in das Installationspaket wie folgt:  
  
|JAR|JDBC-Spezifikation|JDK-Version|  
|-|-|-|  
|mssql-jdbc-6.2.1.jre8.jar|JDBC 4.2, 4.1 und 4.0|JDK 8.0|  
|mssql-jdbc-6.2.1.jre7.jar|JDBC 4.1 und 4.0|JDK 7.0|  
 
 Microsoft JDBC Driver 6.0 und 4.2 für SQL Server unterstützt JDBC 4.0, 4.1 und 4.2-Spezifikationen, und wie folgt zwei JAR-Klassenbibliotheken in das Installationspaket einbeziehen:  
  
|JAR|JDBC-Spezifikation|JDK-Version|   
|-|-|-|  
|sqljdbc42.jar|JDBC 4.2, 4.1 und 4.0|JDK 8.0|  
|sqljdbc41.jar|JDBC 4.1 und 4.0|JDK 7.0|  
  
 Der Microsoft JDBC Driver 4.1 für SQL Server unterstützt die JDBC 4.0-Spezifikation und enthält eine JAR-Klassenbibliothek im Installationspaket wie folgt:  
  
|JAR|JDBC-Spezifikation|JDK-Version|    
|-|-|-|  
|sqljdbc41.jar|JDBC 4.0|JDK 7.0 and 6.0|
  
 **Benötige ich in meiner Anwendung auf den neuesten Treiber mit meiner vorhandenen SQL Server-Version verwenden alle Änderungen am Code vornehmen?**  
 Im Allgemeinen wird der Treiber abwärtskompatibel, damit Sie nicht benötigen, um Ihre vorhandenen Anwendungen zu ändern, bei einer treiberaktualisierung ausgelegt. Wenn eine neue Treiberversion eine unterbrechende Änderung, führt der [Anmerkungen zu dieser Version für den JDBC-Treiber](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) Abschnitt enthält detaillierte Informationen zu dieser Änderung und die Auswirkungen auf vorhandene Anwendungen. Darüber hinaus finden Sie in den Versionsanmerkungen des Treibers eine Liste bekannter Probleme und der in diesem Release behobenen Fehler.  
  
 **Wie viel kostet der Treiber?**  
 Der Microsoft JDBC-Treiber für SQL steht Ihnen kostenlos zur Verfügung.  
  
 **Kann ich den Treiber Weitervertreiben?** Die JDBC-Treiber 4.1, 4.2, 6.0, 6.2 und 6.4 sind verteilbar. Überprüfen Sie die Klausel "Verteilbarer Code" in die Lizenzverträge angezeigt. 
   
 **Kann der Treiber werden verwendet, um Microsoft SQL Server auf einem linuxcomputer anzumelden?** Ja! Sie können den Treiber verwenden, um von Linux, Unix und anderen nicht-Windows-Plattformen auf SQL Server zuzugreifen. Finden Sie unter [Microsoft JDBC Driver für SQL Server-Supportmatrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) Weitere Details.  
  
 **Unterstützt der Treiber die Secure Sockets Layer (SSL)-Verschlüsselung?** Die SSL-Verschlüsselung wird seit Version 1.2 des Treibers unterstützt. Weitere Informationen finden Sie unter [mithilfe von SSL-Verschlüsselung](../../connect/jdbc/using-ssl-encryption.md).  
  
 **Welche Authentifizierungstypen werden von Microsoft JDBC Driver für SQL Server unterstützt?**  
 Die verfügbaren Authentifizierungsoptionen sind in der folgenden Tabelle aufgelistet. Beachten Sie, dass die reine Java Kerberos-Authentifizierung seit Version 4.0 des Treibers verfügbar ist.  
  
|||  
|-|-|  
|Platform|Authentifizierung|  
|Nicht-Windows-System|Reine Java Kerberos|  
|Nicht-Windows-System|SQL Server|  
|Nicht-Windows-System|Azure Active Directory-Authentifizierung|
|Windows|Reine Java Kerberos|  
|Windows|SQL Server|
|Windows|Kerberos mit NTLM als Backup|  
|Windows|NTLM|  
|Windows|Azure Active Directory-Authentifizierung|  
  
**Unterstützt der Treiber Internetprotokoll Version 6 (IPv6) Adressen?**  
 Ja, der JDBC-Treiber unterstützt die Verwendung von IPv6-Adressen in der Liste der Verbindungseigenschaften und in der Eigenschaft „serverName“ der Verbindungszeichenfolge. Weitere Informationen finden Sie unter [Erstellen der Verbindungs-URL](../../connect/jdbc/building-the-connection-url.md).  
  
**Was ist die adaptive Pufferung?**  
 Die adaptive Pufferung wurde in Version 1.2 des JDBC-Treibers für Microsoft SQL Server 2005 eingeführt, um beliebige umfangreiche Daten ohne Verwendung von Servercursorn abzurufen und den damit einhergehenden Overhead zu vermeiden. Die adaptive Pufferung des Microsoft SQL Server JDBC Drivers stellt mit „responseBuffering“ eine Eigenschaft für Verbindungszeichenfolgen bereit, die auf „adaptive“ oder „full“ festgelegt werden kann. Ab Version 2.0 des JDBC-Treibers ist das Standardverhalten des Treibers „adaptive“. Dies bedeutet, um das Verhalten der adaptiven Pufferung zu verwenden, muss das Verhalten der adaptiven Pufferung in der Anwendung nicht explizit angefordert werden. In Version 1.2 lautete der Puffermodus jedoch standardmäßig „full“, und die Anwendung musste den Modus für die adaptive Pufferung explizit anfordern. Weitere Informationen finden Sie unter [mithilfe der adaptiven Pufferung](../../connect/jdbc/using-adaptive-buffering.md) Thema und im Blog. [Was ist buffering und warum sollte ich verwenden?](http://go.microsoft.com/fwlink/?LinkId=111575)  
  
**Unterstützt der Treiber Verbindungspooling?**  
 Der Treiber unterstützt das Verbindungspooling unter Java Platform, Enterprise Edition 5 (Java EE 5). Der Treiber implementiert die erforderlichen JDBC 3.0-Schnittstellen, damit er implementiertes Verbindungspooling von Anbietern für Anwendungsserver auf Middleware-Ebene nutzen kann. Der Treiber nutzt in diesen Umgebungen Verbindungspool. Weitere Informationen finden Sie unter [Verbindungspooling verwenden](../../connect/jdbc/using-connection-pooling.md). Der Treiber bietet keine eigene Implementierung des Poolings, sondern es beruht auf Java-Anwendungsservern von Drittanbietern.  
  
**Steht Unterstützung für den Treiber?**  
 Es sind zahlreiche Optionen verfügbar. Sie können Ihre Frage oder einer Lösung des Problems unsere [GitHub-Repository](https://github.com/microsoft/mssql-jdbc) wird die von Microsoft überwacht. [Foren](http://go.microsoft.com/fwlink/?LinkID=246673) von Microsoft, MVPs und Community überwacht werden. Sie können sich auch an den Microsoft Kundendienst wenden. Das Entwicklungsteam möglicherweise zum Reproduzieren des Problems außerhalb alle Drittanbieter-Anwendungsservern aufgefordert. Wenn das Problem außerhalb der Hostingumgebung Java Containers reproduziert werden kann, müssen Sie die verwandte Drittanbieter hinzuziehen, sodass das Team fortgesetzt werden kann, um Sie zu unterstützen. Das Team möglicherweise auch Sie aufgefordert, Ihr Problem auf ein älteres Betriebssystem wie z. B. Windows reproduzieren, damit das Problem am besten unterstützt werden kann.  
  
**Werden der Treiber ist für die Verwendung mit jeder Drittanbieter-Anwendungsservern zertifiziert?**
Der Treiber wurde mit allen wichtigen Anwendungsserver getestet, wie z. B. IBM WebSphere und SAP NetWeaver.  
  
**Wie aktiviere ich die Ablaufverfolgung?**  
 Der Treiber unterstützt die Verwendung der Ablaufverfolgung (oder Protokollierung). Dies hilft Probleme zu lösen, die bei der Verwendung des JDBC-Treibers in Ihrer Anwendung auftreten können. Der JDBC-Treiber verwendet die Logging-API in java.util.logging, um die clientseitige JAR-Ablaufverfolgung zu aktivieren. Weitere Informationen finden Sie unter [Ablaufverfolgung für Treibervorgänge](../../connect/jdbc/tracing-driver-operation.md). Weitere Informationen zur serverseitigen XA-Ablaufverfolgung finden Sie unter [Verfolgung des Datenzugriffs in SQL Server](http://go.microsoft.com/fwlink/?LinkId=248705).  
  
**Wo kann ich herunterladen ältere Versionen des Treibers, z. B. der SQL Server 2000-JDBC-Treiber, 2005-Treiber, 1.0, 1.1 und 1.2 Treiber?**  
 Diese Treiberversionen stehen nicht zum Download zur Verfügung, da sie nicht mehr unterstützt werden. Wir werden die Java-Unterstützung für Clientkonnektivität kontinuierlich verbessern. Daher wird dringend empfohlen, die Sie mit der neuesten Version von Microsoft JDBC Driver arbeiten.  
  
**Ich verwende JRE 1.4. Welcher Treiber ist mit JRE 1.4 kompatibel?**  
 Kunden, die SAP-Produkte verwenden und die Unterstützung für JRE 14. benötigen, können [SAP Service Marketplace](http://service.sap.com/) um den Microsoft JDBC-Treiber 1.2 zu erhalten.  
  
**Kann der Treiber mit FIPS-validierten Algorithmen kommunizieren?**  
 Der Microsoft JDBC-Treiber enthält keine kryptografischen Algorithmen. Wenn ein Kunde nutzt, Betriebssystem, Anwendung und JVM-Algorithmen, die akzeptable von Federal Information Processing Standards (FIPS) bewertet werden und den Treiber konfiguriert, um diese Algorithmen verwenden, verwendet der Treiber nur die festgelegten Algorithmen für die Kommunikation.  
  
 ## <a name="see-also"></a>Siehe auch  
 [Overview of the JDBC Driver (Übersicht über den JDBC-Treiber)](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
