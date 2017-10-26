---
title: "Systemanforderungen für JDBC Driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eed93fab6f0ceec655b7b9f6b392abc390b5f0ff
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-jdbc-driver"></a>Systemanforderungen für den JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Für den Datenzugriff aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] mithilfe der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], müssen die folgenden Komponenten auf Ihrem Computer installiert sein:  
  
-   [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]  
  
     Sie können die Microsoft JDBC-Treiber unter folgenden Links zum Microsoft Download Center herunterladen: 
     * [Microsoft JDBC Driver 6.2 für SQLServer](http://go.microsoft.com/fwlink/?linkid=852460)
     * [Microsoft JDBC Driver 6.0 für SQLServer](http://go.microsoft.com/fwlink/?linkid=841535)
     * [Microsoft JDBC Driver 4.2 für SQLServer](http://go.microsoft.com/fwlink/?linkid=841534) 
     * [Microsoft JDBC Driver 4.1 für SQLServer](http://go.microsoft.com/fwlink/?linkid=841533) 
     * [Microsoft JDBC Driver 4.0 für SQL Server](http://go.microsoft.com/fwlink/?linkid=841532)
  
-   Java Runtime Environment (JRE)  
  
## <a name="java-runtime-environment-requirements"></a>Anforderungen der Java-Laufzeitumgebung  
 Ab Version 4.2 des Microsoft JDBC-Treibers für SQL Server werden das Sun Java SE Development Kit (JDK) 8.0 und die Java-Laufzeitumgebung (JRE) 8.0 unterstützt. Die Unterstützung für die Java Database Connectivity (JDBC) Spec-API wurde nun auf die JDBC 4.1 und 4.2-API ausgeweitet.  
  
 Ab Microsoft JDBC Driver 4.1 für SQL Server werden Sun Java SE Development Kit (JDK) 7.0 und Java Runtime Environment (JRE) 7.0 unterstützt.  
  
 Beginnend mit der [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], die JDBC-treiberunterstützung für Java Database Connectivity (JDBC) Spec-API wurde erweitert, damit die JDBC 4.0-API erweitert. Die JDBC 4.0-API wurde als Bestandteil des Sun Java SE Development Kits (JDK) 6.0 und der Java Runtime Environment (JRE) 6.0 eingeführt. JDBC 4.0 ist eine Obermenge der JDBC 3.0-API.  
  
 Bei der Bereitstellung der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] auf Windows- und UNIX-Betriebssystemen müssen Sie die Installationspakete verwenden *"sqljdbc_"\<Version > _enu.exe* und *"sqljdbc_"\<Version > _ ENU.TAR.GZ*zugeordnet. Weitere Informationen zum Bereitstellen des JDBC-Treibers finden Sie unter [Bereitstellen des JDBC-Treibers](../../connect/jdbc/deploying-the-jdbc-driver.md) Thema.  
  
**Microsoft JDBC Driver 6.2 für SQLServer:**  
  
  Der JDBC-Treiber 6.2 umfasst zwei JAR-Klassenbibliotheken in jedem Installationspaket: **Mssql-Jdbc-6.2.1.jre7.jar**, und **Mssql-Jdbc-6.2.1.jre8.jar**. 
  
 Der JDBC-Treiber 6.2 dient zum Arbeiten mit und vom alle wichtigen Sun entsprechende Java-VMs unterstützt werden, jedoch wird nur auf der Sun JRE 5.0, 6.0, 7.0 und 8.0 getestet. 
  
 Im folgenden wird die Unterstützung durch die zwei JAR-Dateien, die mit Microsoft JDBC Driver 6.0 und 4.2 für SQL Server enthaltenen zusammengefasst:  
  
|JAR|JDBC-Versionskompatibilität|Empfohlene Java-Version|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|MSSQL-Jdbc-6.2.1.jre7.jar|4.1|7|Erfordert die Java-Laufzeitumgebung( JRE) Version 7.0. Bei Verwendung von JRE löst 6.0 oder niedriger eine Ausnahme.<br /><br /> Neue Funktionen in 6.2 umfassen: Azure AD-Authentifizierung für Linux Prinzipal/Kennwort-Methode für die automatische Erkennung des Bereichs DARSTELLT, in der SPN für domänenübergreifende Authentifizierung, Kerberos Constrained Delegation, Abfragetimeout, Sockettimeout, Kerberos und vorbereitete Anweisungshandle wiederzuverwenden. |  
|MSSQL-Jdbc-6.2.1.jre8.jar|4.2|8|Erfordert die Java-Laufzeitumgebung(JRE) Version 8.0. Bei Verwendung von JRE löst 7.0 oder niedriger eine Ausnahme.<br /><br /> Neue Funktionen in 6.2 umfassen: Azure AD-Authentifizierung für Linux Prinzipal/Kennwort-Methode für die automatische Erkennung des Bereichs DARSTELLT, in der SPN für domänenübergreifende Authentifizierung, Kerberos Constrained Delegation, Abfragetimeout, Sockettimeout, Kerberos und vorbereitete Anweisung Handle erneut verwenden|    

  Der JDBC-Treiber 6.2 steht auch auf dem zentralen Repository Maven und kann durch Hinzufügen des folgenden Codes in der POM eine Maven-Projekt hinzugefügt. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 und 4.2 für SQLServer:**  
  
  Der JDBC-Treiber 6.0 und 4.2 enthalten zwei JAR-Klassenbibliotheken in jedem Installationspaket: **"sqljdbc41.jar"**, und **"sqljdbc42.jar"**. 
  
 Der JDBC-Treiber 6.0 und 4.2 dienen zum Arbeiten mit und von allen wichtigen Sun entsprechende Java virtuellen Computern unterstützt werden, aber nur auf der Sun JRE 5.0, 6.0, 7.0 und 8.0 getestet wird. 
  
 Im folgenden wird die Unterstützung durch die zwei JAR-Dateien, die mit Microsoft JDBC Driver 6.0 und 4.2 für SQL Server enthaltenen zusammengefasst:  
  
|JAR|JDBC-Versionskompatibilität|Empfohlene Java-Version|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Erfordert die Java-Laufzeitumgebung( JRE) Version 7.0. Bei Verwendung von JRE löst 6.0 oder niedriger eine Ausnahme.<br /><br /> Neue Funktionen in 6.0- und 4.2-Paketen schließen Folgendes mit ein: JDBC 4.1-Kompatibilität und Massenkopieren<br /><br /> Außerdem neue Funktionen in im 6.0-Paket einschließen: Always Encrypted Table-Valued Parameters, Azure Active Directory-Authentifizierung, transparente Verbindungen mit AlwaysOn-Verfügbarkeitsgruppen, zur Verbesserung der im Parameters Abruf von Metadaten für vorbereitete Abfragen und Internationalized Domain Name (IDN)|  
|sqljdbc42.jar|4.2|8|Erfordert die Java-Laufzeitumgebung(JRE) Version 8.0. Bei Verwendung von JRE löst 7.0 oder niedriger eine Ausnahme.<br /><br /> Neue Funktionen in 6.0- und 4.2-Paketen schließen Folgendes mit ein: JDBC 4.1 Compliance, JDBC 4.2 Compliance und Massenkopieren<br /><br /> Außerdem neue Funktionen in im 6.0-Paket einschließen: Always Encrypted Table-Valued Parameters, Azure Active Directory-Authentifizierung, transparente Verbindungen mit AlwaysOn-Verfügbarkeitsgruppen, zur Verbesserung der im Parameters Abruf von Metadaten für vorbereitete Abfragen und Internationalized Domain Name (IDN)|  
  
 **Microsoft JDBC Driver 4.1 für SQLServer:**  
  
 Der JDBC Driver 4.1 beinhaltet eine JAR-Klassenbibliothek in jedem Installationspaket: **"sqljdbc41.jar"**.  
    
|JAR|Description|  
|---------|-----------------|  
|sqljdbc41.jar|**"sqljdbc41.jar"** -Klassenbibliothek bietet Unterstützung für JDBC 4.0-API. Sie umfasst alle Funktionen von der JDBC 4.0-Treiber sowie die JDBC 4.0-API-Methoden. JDBC 4.1 wird nicht unterstützt (die Ausnahme SQLFeatureNotSupportedException wird ausgelöst).<br /><br /> **"sqljdbc41.jar"** -Klassenbibliothek ist eine Java Runtime Environment (JRE) 7.0 erforderlich. Mit **"sqljdbc41.jar"** für JRE 6.0 und 5.0 wird eine Ausnahme ausgelöst.<br /><br /> 
  
 Beachten Sie, dass der JDBC-Treiber zwar für die Verwendung mit und die Unterstützung aller wichtigen Sun-kompatiblen Java-VMs (Virtual Machines) ausgelegt ist, aber mit Sun JRE 5.0, 6.0 oder 7.0 getestet wird.  
  
 Im folgenden zusammengefasst Unterstützung durch die mit Microsoft JDBC Driver 4.1 für SQL Server enthaltenen JAR-Datei.  
  
|JAR|JDBC-Version|JRE (kann ausgeführt werden)|JDK (kann kompilieren)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
 **Microsoft JDBC Driver 4.0 für SQLServer:**  
  
 Um Abwärtskompatibilität zu gewährleisten und mögliche upgradeszenarios zu unterstützen, umfasst der JDBC-Treiber zwei JAR-Klassenbibliotheken in jedem Installationspaket: **"sqljdbc.jar"** und **"sqljdbc4.jar"**.  
  
|JAR|Description|  
|---------|-----------------|  
|sqljdbc.jar|**"sqljdbc.jar"** -Klassenbibliothek bietet Unterstützung für JDBC 3.0.<br /><br /> **"sqljdbc.jar"** -Klassenbibliothek erfordert eine Java Common Language Runtime Environment (JRE) Version 5.0. Mit **"sqljdbc.jar"** für JRE 6.0 oder JRE 7.0 löst eine Ausnahme bei der Verbindung mit einer Datenbank.<br /><br /> **Hinweis:** der JDBC-Treiber unterstützt JRE 1.4 nicht. Sie müssen ein Upgrade von JRE 1.4 auf JRE 5.0, JRE 6.0 oder JRE 7.0 ausführen, wenn Sie den JDBC-Treiber verwenden. In bestimmten Fällen müssen Sie die Anwendung neu kompilieren, da sie möglicherweise nicht mit der JDK 5.0-API oder JDK 6.0-API kompatibel ist. Weitere Informationen finden Sie in der Dokumentation auf der Sun Microsystems-Website.<br /><br /> [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]JDK 7 wird nicht unterstützt werden.|  
|sqljdbc4.jar|**"sqljdbc4.jar"** -Klassenbibliothek bietet Unterstützung für JDBC 4.0-API. Sie umfasst alle Funktionen von der **"sqljdbc.jar"** sowie die neuen JDBC 4.0-API-Methoden.<br /><br /> **"sqljdbc4.jar"** -Klassenbibliothek ist eine Java-Runtime-Umgebung (JRE) Version 6.0 oder 7.0 erforderlich. Mit **"sqljdbc4.jar"** für JRE 5.0 wird eine Ausnahme ausgelöst.<br /><br /> **Hinweis:** verwenden **"sqljdbc4.jar"** Wenn muss die Anwendung unter JRE 6.0 oder 7.0 ausgeführt, selbst wenn Ihre Anwendung keine JDBC 4.0-API-Funktionen verwendet werden.|  
  
 Beachten Sie, dass der JDBC-Treiber zwar für die Verwendung mit und die Unterstützung aller wichtigen Sun-kompatiblen Java-VMs (Virtual Machines) ausgelegt ist, aber mit Sun JRE 5.0, 6.0 oder 7.0 getestet wird.  
  
## <a name="sql-server-requirements"></a>SQL Server-Anforderungen  
 Der JDBC-Treiber unterstützt Verbindungen mit Azure SQL-Datenbank und SQL Server. Microsoft JDBC Driver 4.2 und 4.1 für SQL Server werden beginnend mit SQL Server 2008 unterstützt. Beim Microsoft JDBC Driver 4.0 für SQL Server ist Unterstützung ab SQL Server 2005 verfügbar.  
  
## <a name="operating-system-requirements"></a>Betriebssystemanforderungen  
 Der JDBC-Treiber ist für die Verwendung mit einem Betriebssystem konzipiert, das die Java Virtual Machine (JVM) unterstützt. Allerdings wurden nur die Betriebssysteme Sun Solaris, SUSE Linux und Windows offiziell getestet.  
  
## <a name="supported-languages"></a>Unterstützte Sprachen  
 Der JDBC-Treiber unterstützt alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] spaltensortierungen. Weitere Informationen zu den vom JDBC-Treiber unterstützten Sortierungen finden Sie unter [internationale Features des JDBC-Treibers](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Weitere Informationen zu Sortierungen finden Sie unter "Arbeiten mit Sortierungen" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

