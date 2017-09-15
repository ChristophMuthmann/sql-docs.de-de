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
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8033e1690fcaa01ca73ce1a7d0d9972ac2d3ba9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="securing-jdbc-driver-applications"></a>Sichern von JDBC-Treiberanwendungen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Verbessern der Sicherheit einer [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anwendung umfasst das Vermeiden der häufigsten Programmierfehler. Eine Anwendung, die auf Daten zugreift, weist eine Vielzahl von möglichen Fehlern auf, die Angreifer ausnutzen können, um vertrauliche Daten abzurufen, zu ändern oder zu beschädigen. Es ist daher wichtig, alle Aspekte der Sicherheit zu kennen, von der Bedrohungsmodellierung während der Entwurfsphase der Anwendung bis zur endgültigen Bereitstellung und weiter bei der laufenden Wartung.  
  
 In den Themen in diesem Abschnitt werden einige häufige Sicherheitsrisiken beschrieben, unter anderem Verbindungszeichenfolgen, das Überprüfen von Benutzereingaben und allgemeine Anwendungssicherheit.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Sichern von Verbindungszeichenfolgen](../../connect/jdbc/securing-connection-strings.md)|Beschreibt Verfahren zum Schützen von Informationen, mit denen eine Verbindung mit einer Datenquelle hergestellt wird.|  
|[Validieren von Benutzereingaben](../../connect/jdbc/validating-user-input.md)|Beschreibt Verfahren zum Überprüfen von Benutzereingaben.|  
|[Anwendungssicherheit](../../connect/jdbc/application-security.md)|Beschreibt die Verwendung von Java-Richtlinienberechtigungen zum Sichern einer JDBC-Treiberanwendung.|  
|[Mithilfe von SSL-Verschlüsselung](../../connect/jdbc/using-ssl-encryption.md)|Beschreibt das Herstellen ein sicheren Kommunikationskanals mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbank mithilfe von Secure Sockets Layer (SSL).|  
|[FIPS-Modus](../../connect/jdbc/fips-mode.md)|Beschreibt, wie JDBC-Treiber im FIPS-Antragsteller-Modus verwenden.| 
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
