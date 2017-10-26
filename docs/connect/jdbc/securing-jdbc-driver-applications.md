---
title: Sichern von JDBC-Treiberanwendungen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 5051d2d668105bd0a309eb64f2b8becd459d8a6b
ms.openlocfilehash: 097978fa39709dc3c5cd1b8ef150ce4f4c189b17
ms.contentlocale: de-de
ms.lasthandoff: 10/12/2017

---
# <a name="securing-jdbc-driver-applications"></a>Sichern von JDBC-Treiberanwendungen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Verbessern der Sicherheit einer [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anwendung umfasst das Vermeiden der häufigsten Programmierfehler. Eine Anwendung, die auf Daten zugreift, weist eine Vielzahl von möglichen Fehlern auf, die Angreifer ausnutzen können, um vertrauliche Daten abzurufen, zu ändern oder zu beschädigen. Es ist daher wichtig, alle Aspekte der Sicherheit zu kennen, von der Bedrohungsmodellierung während der Entwurfsphase der Anwendung bis zur endgültigen Bereitstellung und weiter bei der laufenden Wartung.  
  
 In den Themen in diesem Abschnitt werden einige häufige Sicherheitsrisiken beschrieben, unter anderem Verbindungszeichenfolgen, das Überprüfen von Benutzereingaben und allgemeine Anwendungssicherheit.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Sichern von Verbindungszeichenfolgen](../../connect/jdbc/securing-connection-strings.md)|Beschreibt Verfahren zum Schützen von Informationen, mit denen eine Verbindung mit einer Datenquelle hergestellt wird.|  
|[Überprüfen der Benutzereingabe](../../connect/jdbc/validating-user-input.md)|Beschreibt Verfahren zum Überprüfen von Benutzereingaben.|  
|[Anwendungssicherheit](../../connect/jdbc/application-security.md)|Beschreibt die Verwendung von Java-Richtlinienberechtigungen zum Sichern einer JDBC-Treiberanwendung.|  
|[Verwenden der SSL-Verschlüsselung](../../connect/jdbc/using-ssl-encryption.md)|Beschreibt das Herstellen ein sicheren Kommunikationskanals mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbank mithilfe von Secure Sockets Layer (SSL).|  
|[FIPS-Modus](../../connect/jdbc/fips-mode.md)|Beschreibt, wie JDBC-Treiber im FIPS-kompatiblen Modus verwendet wird.| 
  
## <a name="see-also"></a>Siehe auch  
 [Overview of the JDBC Driver (Übersicht über den JDBC-Treiber)](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

