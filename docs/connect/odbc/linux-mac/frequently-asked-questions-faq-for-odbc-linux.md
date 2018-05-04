---
title: Häufig gestellte Fragen (FAQ) für ODBC Linux und MacOS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6db6b7ba6a068df6d2706b8e44359122c9f438e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>Häufig gestellte Fragen (FAQ) für ODBC Linux und macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Im folgenden sind Antworten auf Fragen zum ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS.
  
## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

**Wie funktionieren die vorhandene ODBC-Anwendungen unter Linux oder MacOS mit dem Treiber?**  
Sie sollten Lage kompilieren und Ausführen der ODBC-Anwendungen, die Sie kompilieren und Ausführen von unter Linux oder MacOS mit anderen Treibern wurden. 
  
**Welche Funktionen von [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] werden von dieser Version des Treibers unterstützt?**

Der ODBC-Treiber unter Linux und MacOS unterstützt alle Serverfunktionen in [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] außer LocalDB. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unterstützte Funktionen finden Sie unter [Programmierung Richtlinien](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
**Unterstützt der Treiber die Kerberos-Authentifizierung?**  
Ja. Wenn Sie eine vorhandene Einrichten der Kerberos-Umgebung verfügen, sollten Sie mit Server herstellen werden die `Trusted_Connection=Yes` DSN- oder Verbindungszeichenfolge String-Option. Weitere Informationen finden Sie unter [mithilfe der integrierten Authentifizierung](../../../connect/odbc/linux-mac/using-integrated-authentication.md).  
  
**Welche Unicode-Codierung sollte eine Anwendung verwenden?**  
UTF-8 für SQL_CHAR-Daten und UTF-16 für SQL_WCHAR-Daten.  

**Gibt es ODBC-Beispiele, die ich herunterladen und mit dem Treiber zu experimentieren oder Sie auszuwerten ausführen kann?**

Ein Beispiel hierzu finden Sie unter [Vorhandene MSDN C++ ODBC-Beispiele für die ODBC-Treiber unter Linux](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) . Dies gilt auch für den MacOS ODBC-Treiber. 

**Ist der ODBC-Treiber unter Linux oder open MacOS-Source?**

Nein, sind die ODBC-Treiber unter Linux und MacOS nicht open Source-Produkt.  

## <a name="see-also"></a>Siehe auch
[Installieren von Microsoft ODBC Driver für SQL Server unter Linux und macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
