---
title: Sicherheit der Anwendung | Microsoft Docs
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
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77cfbbad8b17236b5609973095e10762e6624ba8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="application-security"></a>Anwendungssicherheit
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei Verwendung der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], es ist wichtig, Sie Vorsichtsmaßnahmen ergreifen, um die Sicherheit der Anwendung sicherzustellen. Die folgenden Abschnitte enthalten Informationen zu den Schritten, die Sie zum Sichern der Anwendung ergreifen können.  
  
## <a name="using-java-policy-permissions"></a>Verwenden von Java-Richtlinienberechtigungen  
 Bei Verwendung der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], es ist wichtig, die erforderlichen Java-Richtlinienberechtigungen angeben, die der JDBC-Treiber erforderlich ist. Die JRE (Java Runtime Environment) stellt ein umfassendes Sicherheitsmodell bereit, mit dem zur Laufzeit ermittelt werden kann, ob ein Thread auf eine Ressource zugreifen kann. Dieser Zugriff kann durch Sicherheitsrichtliniendateien gesteuert werden. Die Richtliniendateien werden vom Entwickler und vom Systemadministrator des Containers verwaltet. Die in diesem Thema aufgeführten Berechtigungen wirken sich jedoch auf die Funktionsweise des JDBC-Treibers aus.  
  
 Eine normale Berechtigung in der Richtliniendatei sieht folgendermaßen aus:  
  
```  
// Example policy file entry.  
grant [signedBy <signer>,] [codeBase <code source>] {  
   permission  <class>  [<name> [, <action list>]];  
};  
```  
  
 Die folgende Codebasis muss auf die Codebasis des JDBC-Treibers beschränkt werden, damit die minimal erforderlichen Privilegien gewährt werden.  
  
```  
grant codeBase "file:/install_dir/lib/-" {  
  
// Grant access to data source.  
permission java.util.PropertyPermission "java.naming.*", "read,write";  
  
// Specify which hosts can be connected to.  
permission java.net.socketPermission "host:port", "connect";  
  
// Logger permission to take advantage of logging.  
permission java.util.logging.LoggingPermission;  
  
// Grant listen/connect/accept permissions to the driver if   
// connecting to a named instance as the client driver.   
// This connects to a udp service and listens for a response.  
permission java.net.SocketPermission "*", "listen, connect, accept";   
};   
```  
  
> [!NOTE]  
>  Der Code "file:/install_dir/lib/-" bezieht sich auf das Installationsverzeichnis des JDBC-Treibers.  
  
## <a name="protecting-server-communication"></a>Schützen der Serverkommunikation  
 Bei Verwendung des JDBC-Treibers für die Kommunikation mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, Sie können den Kommunikationskanal mit Internet Protocol Security (IPSEC) oder Secure Sockets Layer (SSL); oder Sie können beide verwenden.  
  
 Die SSL-Unterstützung kann verwendet werden, um zusätzlich zu IPSEC eine weitere Schutzebene bereitzustellen. Weitere Informationen zur Verwendung von SSL finden Sie unter [mithilfe von SSL-Verschlüsselung](../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern von JDBC-Treiberanwendungen](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
