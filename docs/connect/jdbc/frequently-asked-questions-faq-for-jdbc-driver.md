---
title: "Häufig gestellte Fragen (FAQ) zu JDBC-Treiber | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508f8526ed13af3f7f92aa500b182e077f5bb23d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>Häufig gestellte Fragen (FAQ) zu JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dieser Artikel enthält Antworten auf häufig gestellte Fragen zu Microsoft JDBC Driver for SQL Server.  
  
## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen  
**Wie kann ich Verbessern der JDBC-Treiber?**  
Der JDBC-Treiber ist open Source und der Quellcode befinden sich auf [GitHub](https://github.com/microsoft/mssql-jdbc). Sie können den Treiber verbessern, indem die Einreichung Probleme und die CodeBase verwendet werden sollen.

**Welche Versionen von SQL Server und Java werden vom Treiber unterstützt?**  
 Finden Sie unter der [Microsoft JDBC Driver für SQL Server-Supportmatrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) Informationen.  
  
 **Was sollte ich noch wissen meinen Treiber aktualisiere?**  
 Die Microsoft JDBC Driver 6.2 unterstützt die JDBC 4.0, 4.1 und 4.2-Spezifikation und enthält zwei JAR-Klassenbibliotheken in das Installationspaket wie folgt:  
  
|JAR|JDBC-Spezifikation|JDK-Version|  
|-|-|-|  
|MSSQL-Jdbc-6.2.1.jre8.jar|JDBC 4.2, 4.1 und 4.0|JDK 8.0|  
|MSSQL-Jdbc-6.2.1.jre7.jar|JDBC 4.1 und 4.0|JDK 7.0|  
 
 Microsoft JDBC Driver 6.0 und 4.2 für SQL Server unterstützt JDBC 4.0, 4.1 und 4.2-Spezifikationen, und wie folgt zwei JAR-Klassenbibliotheken in das Installationspaket einbeziehen:  
  
|JAR|JDBC-Spezifikation|JDK-Version|   
|-|-|-|  
|sqljdbc42.jar|JDBC 4.2, 4.1 und 4.0|JDK 8.0|  
|sqljdbc41.jar|JDBC 4.1 und 4.0|JDK 7.0|  
  
 Der Microsoft JDBC Driver 4.1 für SQL Server unterstützt die JDBC 4.0-Spezifikation und enthält eine JAR-Klassenbibliothek im Installationspaket wie folgt:  
  
|JAR|JDBC-Spezifikation|JDK-Version|    
|-|-|-|  
|sqljdbc41.jar|JDBC 4.0|JDK 7.0 and 6.0|
  
 Der Treiber Microsoft JDBC Driver 4.0 for SQL unterstützt sowohl die JDBC-Spezifikationen 3.0 und 4.0 und das Installationspaket enthält die folgenden zwei JAR-Klassenbibliotheken: sqljdbc.jar und sqljdbc4.jar.  
  
|JAR|JDBC-Spezifikation|JDK-Version|   
|-|-|-|  
|sqljdbc4.jar|JDBC 4.0|JDK 6.0 und 5.0|  
|sqljdbc.jar|JDBC 3.0|JDK 6.0 und 5.0|  
  
 **Benötige ich in meiner Anwendung auf den neuesten Treiber mit meiner vorhandenen SQL Server-Version verwenden alle Änderungen am Code vornehmen?**  
 In der Regel entwerfen wir den Treiber abwärtskompatibel , sodass Sie Ihre vorhandenen Anwendungen bei einer Treiberaktualisierung nicht anpassen müssen. Wenn eine neue Treiberversion eine unterbrechende Änderung, führt der [Anmerkungen zu dieser Version für den JDBC-Treiber](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) Abschnitt stellt detaillierte Informationen zu dieser Änderung und die Auswirkungen auf vorhandene Anwendungen bereit. Darüber hinaus finden Sie in den Versionsanmerkungen des Treibers eine Liste bekannter Probleme und der in diesem Release behobenen Fehler.  
  
 **Wie viel kostet der Treiber?**  
 Microsoft JDBC Driver for SQL steht Ihnen kostenlos zur Verfügung.  
  
 **Kann ich den Treiber Weitervertreiben?** Die JDBC-Treiber 4.1, 4.2, 6.0 und 6.2 sind verteilbar. Überprüfen Sie die Klausel "Verteilbarer Code" in den Lizenzverträgen an.
 
 Der JDBC Driver 4.0 wird unter einem separaten Verteilungslizenz, die für die Registrierung muss frei verteilt. Für das Registrieren oder Weitere Informationen finden in unserer [Neuverteilen von Microsoft JDBC Driver](../../connect/jdbc/redistributing-the-microsoft-jdbc-driver.md). 
 
   
 **Kann der Treiber werden verwendet, um Microsoft SQL Server auf einem linuxcomputer anzumelden?** Ja! Sie können den Treiber verwenden, um von Linux, Unix und anderen nicht-Windows-Plattformen auf SQL Server zuzugreifen. Finden Sie in unserer [Microsoft JDBC Driver für SQL Server-Supportmatrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) Weitere Details.  
  
 **Unterstützt der Treiber die Secure Sockets Layer (SSL)-Verschlüsselung?** Die SSL-Verschlüsselung wird seit Version 1.2 des Treibers unterstützt. Weitere Informationen finden Sie unter [mithilfe von SSL-Verschlüsselung](../../connect/jdbc/using-ssl-encryption.md).  
  
 **Welche Authentifizierungstypen werden von Microsoft JDBC Driver für SQL Server unterstützt?**  
 Die verfügbaren Authentifizierungsoptionen sind in der folgenden Tabelle aufgelistet. Beachten Sie, dass die reine Java Kerberos-Authentifizierung seit Version 4.0 des Treibers verfügbar ist.  
  
|||  
|-|-|  
|Platform|Authentifizierung|  
|Nicht-Windows-System|Reine Java Kerberos|  
|Nicht-Windows-System|SQL Server|  
|Windows|Reine Java Kerberos|  
|Windows|SQL Server|  
|Windows|Kerberos mit NTLM als Backup|  
|Windows|NTLM|  
  
**Unterstützt der Treiber Internetprotokoll Version 6 (IPv6) Adressen?**  
 Ja, der JDBC-Treiber unterstützt die Verwendung von IPv6-Adressen in der Liste der Verbindungseigenschaften und in der Eigenschaft „serverName“ der Verbindungszeichenfolge. Weitere Informationen finden Sie unter [Erstellen der Verbindungs-URL](../../connect/jdbc/building-the-connection-url.md).  
  
**Was ist die adaptive Pufferung?**  
 Die adaptive Pufferung wurde in Version 1.2 des JDBC-Treibers für Microsoft SQL Server 2005 eingeführt, um beliebige umfangreiche Daten ohne Verwendung von Servercursorn abzurufen und den damit einhergehenden Overhead zu vermeiden. Die adaptive Pufferung des Microsoft SQL Server JDBC Drivers stellt mit „responseBuffering“ eine Eigenschaft für Verbindungszeichenfolgen bereit, die auf „adaptive“ oder „full“ festgelegt werden kann. Ab Version 2.0 des JDBC-Treibers ist das Standardverhalten des Treibers „adaptive“. Dies bedeutet, um das Verhalten der adaptiven Pufferung zu verwenden, muss das Verhalten der adaptiven Pufferung in der Anwendung nicht explizit angefordert werden. In Version 1.2 lautete der Puffermodus jedoch standardmäßig „full“, und die Anwendung musste den Modus für die adaptive Pufferung explizit anfordern. Weitere Informationen finden Sie unter [mithilfe der adaptiven Pufferung](../../connect/jdbc/using-adaptive-buffering.md) Thema und im Blogartikel [Was ist-buffering und warum sollte ich verwenden?](http://go.microsoft.com/fwlink/?LinkId=111575).  
  
**Unterstützt der Treiber Verbindungspooling?**  
 Der Treiber unterstützt das Verbindungspooling unter Java Platform, Enterprise Edition 5 (Java EE 5). Der Treiber implementiert die erforderlichen JDBC 3.0-Schnittstellen, damit er implementiertes Verbindungspooling von Anbietern für Anwendungsserver auf Middleware-Ebene nutzen kann. Der Treiber nutzt in diesen Umgebungen Verbindungspool. Weitere Informationen finden Sie unter [Verbindungspooling verwenden](../../connect/jdbc/using-connection-pooling.md). Der Treiber bietet keine eigene Implementierung des Poolings, sondern es beruht auf Java-Anwendungsservern von Drittanbietern.  
  
**Steht Unterstützung für den Treiber?**  
 Es sind zahlreiche Optionen verfügbar. Sie können Ihre Frage oder einer Lösung des Problems unsere [GitHub-Repository](https://github.com/microsoft/mssql-jdbc) wird die von Microsoft überwacht. [Foren](http://go.microsoft.com/fwlink/?LinkID=246673) von Microsoft, MVPS und Community überwacht werden. Sie können sich auch an den Microsoft Kundendienst wenden. Hierbei kann es erforderlich sein, dass Sie das Problem außerhalb einer Drittanbieteranwendung reproduzieren. Wenn das Problem nicht außerhalb der Umgebung des hostenden Java Containers reproduziert werden kann, müssen Sie den Drittanbieter hinzuziehen, damit wir Ihnen weiterhin helfen können. Zusätzlich kann es für die optimale Hilfe nötig sein, dass Sie Ihr Problem auf einem Betriebssystem, wie z. B. Windows, reproduzieren.  
  
**Werden der Treiber ist für die Verwendung mit jeder Drittanbieter-Anwendungsservern zertifiziert?**
Der Treiber wurde mit allen wichtigen Anwendungsserver getestet, wie z. B. IBM WebSphere und SAP NetWeaver.  
  
**Wie aktiviere ich die Ablaufverfolgung?**  
 Der Treiber unterstützt die Verwendung der Ablaufverfolgung (oder Protokollierung). Dies hilft Probleme zu lösen, die bei der Verwendung des JDBC-Treibers in Ihrer Anwendung auftreten können. Der JDBC-Treiber verwendet die Logging-API in java.util.logging, um die clientseitige JAR-Ablaufverfolgung zu aktivieren. Weitere Informationen finden Sie unter [Ablaufverfolgung für Treibervorgänge](../../connect/jdbc/tracing-driver-operation.md). Weitere Informationen zur serverseitigen XA-Ablaufverfolgung finden Sie unter [Verfolgung des Datenzugriffs in SQL Server](http://go.microsoft.com/fwlink/?LinkId=248705).  
  
**Wo kann ich herunterladen ältere Versionen des Treibers, z. B. der SQL Server 2000-JDBC-Treiber, 2005-Treiber, 1.0, 1.1 und 1.2 Treiber?**  
 Diese Treiberversionen stehen nicht zum Download zur Verfügung, da sie nicht mehr unterstützt werden. Wir arbeiten laufend daran, unsere Unterstützung von Java-Konnektivität zu verbessern. Daher raten wir dringend zur Verwendung unseres aktuellsten JDBC-Treibers.  
  
 **Ich verwende JRE 1.4. Welcher Treiber ist mit JRE 1.4 kompatibel** für Kunden, die SAP-Produkte verwenden und Unterstützung für JRE 14. benötigen, können Sie kontaktieren [SAP Service Marketplace](http://service.sap.com/) zu Microsoft JDBC Driver 1.2 zu erhalten.  
  
**Kann der Treiber mit FIPS-validierten Algorithmen kommunizieren?** Der Microsoft JDBC-Treiber enthält keine kryptografischen Algorithmen. Wenn ein Kunde Algorithmen für Betriebssysteme, Anwendungen und JVM verwendet, die entsprechend der Federal Information Processing Standards (FIPS) zulässig sind, und er den Treiber für diese Algorithmen konfiguriert, so wird dieser für die Kommunikation nur die festgelegten Algorithmen verwenden.  
  
  

