---
title: "Abhängigkeiten von Microsoft JDBC Driver für SQLServer Feature | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2018
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
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 703a27220a80744c46ca0bc7667756cec1ab6596
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Featureabhängigkeiten von Microsoft JDBC Driver für SQLServer
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

 Diese Seite enthält die Liste der Bibliotheken, denen von Microsoft JDBC Driver für SQL Server abhängig ist. Das Projekt besitzt die folgenden Abhängigkeiten.
 
 ## <a name="compile-time"></a>Kompilierzeit
 - `azure-keyvault` : Azure Key Vault-Anbieters für Always Encrypted Azure Key Vault-Feature (optional)
 - `adal4j` : Azure Active Directory-Bibliothek für Java für Azure Active Directory-Authentifizierung-Feature und Azure Key Vault-Feature (optional)

 ##  <a name="test-time"></a>Testzeit
Bestimmte Projekte, die eine der oben genannten zwei Funktionen erfordern müssen die entsprechenden Abhängigkeiten in ihrer Datei Pom explizit zu deklarieren:

***Zum Beispiel:*** bei Verwendung von *Azure Active Directory-Authentifizierung-Funktion*, müssen Sie deklarieren *adal4j* Abhängigkeit in Ihrer Projektdatei Pom. Finden Sie unter den folgenden Codeausschnitt: 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>
```

***Z. B.:*** bei Verwendung von *Azure Key Vault-Feature* müssen Sie deklarieren *Azure Keyvault* Abhängigkeit und *adal4j* in Abhängigkeit Ihrer Pom-Datei des Projekts. Finden Sie unter den folgenden Codeausschnitt: 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```
 
 ## <a name="dependency-requirements-for-the-jdbc-driver"></a>Abhängigkeitsanforderungen für den JDBC-Treiber

 ### <a name="azure-keyvault-feature"></a>Azure Keyvault-Feature:
- JDBC Driver version 6.0.0 
    - Abhängigkeit-Versionen: Azure-Keyvault (Version 0.9.7), Adal4j (Version 1.3.0) herunter, und die zugehörigen Abhängigkeiten ( [Beispielanwendung](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))
- JDBC Driver, Version 6.2.2 und höher (einschließlich der neuesten 6.4.0)
    - Abhängigkeit-Versionen: Azure-Keyvault (Version 1.0.0), Adal4j (Version 1.4.0) herunter, und die zugehörigen Abhängigkeiten ([Beispielanwendung](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))

> [!NOTE]
>   Zum Zeitpunkt der v6.2.2 wird die Azure-Keyvault-Java-Abhängigkeit auf Version 1.0.0 aktualisiert. Allerdings wird die neue Version ist nicht kompatibel mit der früheren Version (Version 0.9.7) und wird daher in der Treiber die vorhandene Implementierung unterbrochen. Die neue Implementierung im Treiber erfordert API-Änderungen, die wodurch wiederum Clientprogramme unterbrochen werden, die den Azure Key Vault-Feature verwenden.

  
 ### <a name="azure-active-directory-authentication"></a>Azure Active Directory-Authentifizierung:
- JDBC Driver version 6.0.0 
    - Abhängigkeit-Versionen: Adal4j (Version 1.3.0), und seine Abhängigkeiten
        - In dieser Version des Treibers, Sie können eine Verbindung herstellen mit *ActiveDirectoryIntegrated* Authentifizierungsmodus nur auf ein Windows-Betriebssystem und die Verwendung von "sqljdbc_auth.dll" und Active Directory-Authentifizierungsbibliothek für SQL Server ( ADALSQL. (DLL). 
- JDBC Driver version 6.4.0
    - Abhängigkeit-Versionen: Adal4j (Version 1.4.0) und seine Abhängigkeiten
        - In dieser Version des Treibers erfordert die Anwendung keine ADALSQL verwenden. DLL. Abhängig vom Betriebsystem. Für **nicht-Windows-Betriebssystemen**, der Treiber erfordert Kerberos-Ticket mit ActiveDirectoryIntegrated Authentifizierung arbeiten. Finden Sie unter [legen Sie Kerberos-Ticket unter Windows, Linux und Macintosh](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) Weitere Details. Für **Windows-Betriebssystemen**, Treiber standardmäßig überprüft, ob es sich bei "sqljdbc_auth.dll" wird geladen und erfordert keine Kerberos-Ticket Setup- oder adal4j Abhängigkeit. Wenn jedoch "sqljdbc_auth.dll" nicht geladen wurde, Treiber verhält sich genauso wie nicht-Windows-Betriebssystemen und Setup, die im folgenden Beispiel beschrieben ist, müsste: eine beispielanwendung, die mit dieser Funktion verwendbaren [hier](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) .

 ## <a name="see-also"></a>Siehe auch  
 [JDBC-Treiber-GitHub-Repository](https://github.com/microsoft/mssql-jdbc)  
 [API-Referenz für JDBC-Treiber](../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  