---
title: Internationale Funktionen des JDBC-Treibers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1fd4eb01d7ab8aa2314dfb8f45e0bd08c3b49488
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="international-features-of-the-jdbc-driver"></a>Internationale Funktionen des JDBC-Treibers
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die Internationalisierungsfunktionen der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] umfassen Folgendes:  
  
-   Unterstützung einer vollständigen Lokalisierung in den gleichen Sprachen wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   Unterstützung für Java-sprachumwandlungen für gebietsschemasensitive [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Daten  
  
-   Unterstützung internationaler Sprachen, unabhängig vom Betriebssystem  
  
-   Unterstützung für internationale Domänennamen (beginnend mit Microsoft JDBC-Treiber 6.0 für SQL Server)  
  
## <a name="handling-of-character-data"></a>Verarbeitung von Zeichendaten  
 Zeichendaten in Java werden standardmäßig als Unicode behandelt; die Java **Zeichenfolge** Objekt stellt Unicode-Zeichendaten dar. Die einzige Ausnahme dieser Regel im JDBC-Treiber bilden die Abruf- und Festlegungsmethoden für ASCII-Datenströme. Dabei handelt es sich um Sonderfälle, da Bytedatenströme mit der impliziten Voraussetzung einer einzelnen bekannten Codepage (ASCII) verwendet werden.  
  
 Darüber hinaus bietet der JDBC-Treiber die **SendStringParametersAsUnicode** Verbindungszeichenfolgen-Eigenschaft. Mit dieser Eigenschaft kann angegeben werden, dass die vorbereiteten Parameter für Zeichendaten anstatt in Unicode in ASCII oder als Multibyte-Zeichensatz (MBCS) gesendet werden. Weitere Informationen zu den **SendStringParametersAsUnicode** Verbindungszeichenfolgen-Eigenschaft finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
### <a name="driver-incoming-conversions"></a>Konvertierung eingehender Daten  
 Unicode-Textdaten vom Server brauchen nicht konvertiert zu werden. Sie werden direkt als Unicode-Daten übergeben. Nicht-Unicode-Daten vom Server werden von der Codepage für die Daten auf Datenbank- oder Spaltenebene in Unicode konvertiert. Der JDBC-Treiber verwendet die JVM-Konvertierungsroutinen (Java Virtual Machine) für diese Konvertierungen. Diese Konvertierungen werden in allen Abrufmethoden für typisierte Zeichenfolge- und Zeichendatenströme ausgeführt.  
  
 Wenn die JVM nicht die richtige Codepage für die Daten aus der Datenbank unterstützt, löst der JDBC-Treiber die Ausnahme "Codepage XXX wird von der Java-Umgebung nicht unterstützt." aus. Zum Beheben dieses Problems sollten Sie die vollständige Unterstützung für internationale Zeichensätze installieren, die für diese JVM erforderlich ist. Ein Beispiel finden Sie auf der Sun Microsystems-Website in der Dokumentation zu unterstützten Codierungen.  
  
### <a name="driver-outgoing-conversions"></a>Konvertierung ausgehender Daten  
 Zeichendaten vom Treiber zum Server können als ASCII oder Unicode übertragen werden. Angenommen, die neuen JDBC 4.0 Methoden für nationale Zeichensätze, z. B. SetNString, SetNCharacterStream und SetNClob-Methode der [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) und [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klassen Senden Sie ihre Parameterwerte immer mit dem Server im Unicode-Format.  
  
 Andererseits, die nicht nationale Zeichensätze API-Methoden, z. B. SetString, SetCharacterStream und SetClob-Methode der [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) und [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klassen Senden Sie ihre Werte an den Server im Unicode-Format nur, wenn die **SendStringParametersAsUnicode** Eigenschaft auf "True", d. h. den Standardwert festgelegt ist.  
  
## <a name="non-unicode-parameters"></a>Nicht-Unicode-Parameter  
 Für eine optimale Leistung mit **CHAR**, **VARCHAR** oder **LONGVARCHAR** geben, der nicht-Unicode-Parameter, legen Sie die **SendStringParametersAsUnicode** Connection string-Eigenschaft auf "False" und die Methoden für nicht nationale Zeichensätze verwenden.  
  
## <a name="formatting-issues"></a>Formatierungsprobleme  
 Für Datum, Uhrzeit und Währungsangaben erfolgt die gesamte Formatierung mit lokalisierten Daten auf Java-Ebene mithilfe der Locale-Objekt; und den verschiedenen Formatierungsmethoden für **Datum**, **Kalender**, und **Anzahl** -Datentypen. In den seltenen Fällen, in denen der JDBC-Treiber gebietsschemasensitive Daten in einem lokalisierten Format übergeben muss, wird die entsprechende Formatierungsmethode mit dem JVM-Standardgebietsschema verwendet.  
  
## <a name="collation-support"></a>Unterstützung für Sortierungen  
 JDBC Driver 3.0 unterstützt alle Sortierungen, die von [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], und die neuen Sortierungen bzw. neuen Versionen der Windows-Sortierungsnamen, in eingeführt [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
 Weitere Informationen zu Sortierungen finden Sie unter [Collation and Unicode Support](http://go.microsoft.com/fwlink/?LinkId=131366) und [Windows-Sortierungsname (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=131367) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="using-international-domain-names-idn"></a>Verwendung internationaler Domänennamen (IDN)  
 Der JDBC Driver 6.0 für SQL Server unterstützt die Verwendung von Internationalized Domain Names (IDNs) und einen Unicode-ServerName in ASCII-kompatible Codierung (Punycode) während einer Verbindung im Bedarfsfall konvertieren kann.  Wenn die IDNs im Domain Name System (DNS) als ASCII-Zeichenfolgen im Punycode-Format (angegeben durch RFC 3490) gespeichert sind, aktivieren Sie die Konvertierung der Unicode-ServerName, indem Sie die ServerNameAsACE-Eigenschaft auf „true“ setzen.  Wenn der DNS-Dienst für die Verwendung von Unicode-Zeichen konfiguriert ist, setzen Sie die ServerNameAsACE-Eigenschaft auf „false“ (Standard).  Für frühere Versionen des JDBC-Treibers ist es auch möglich, der ServerName in Punycode umwandeln [Java's IDN.toASCII](http://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) Methoden vor dem Festlegen dieser Eigenschaft für eine Verbindung.  
  
> [!NOTE]  
>  Der Großteil der für Windows-Plattformen geschriebenen Konfliktlösersoftware basiert auf den Internet-DSN-Standards und verwendet aus diesem Grund mit hoher Wahrscheinlichkeit das Punycode-Format für IDN. Ein Windows-basierter DNS-Server in einem privaten Netzwerk kann hingegen so konfiguriert werden, dass die Verwendung von UTF-8-Zeichen auf Serverbasis möglich ist.  Weitere Informationen finden Sie unter [Unterstützung für Unicode-Zeichen](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx).  
  
## <a name="see-also"></a>Siehe auch  
 [Overview of the JDBC Driver (Übersicht über den JDBC-Treiber)](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
