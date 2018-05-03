---
title: Programmieren mit SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cdcf757117e47679df4a1ce694ed20cbc4251d4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="programming-with-sqlxml"></a>Programmieren mit SQLXML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dieser Abschnitt beschreibt, wie die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API-Methoden zum Speichern und Abrufen von XML zu dokumentieren, in und aus einer relationalen Datenbank mit **SQLXML** Objekte.  
  
 Dieser Abschnitt enthält Informationen über die Typen von SQLXML-Objekten auch und bietet eine Liste wichtiger Richtlinien und Einschränkungen bei Verwendung von SQLXML-Objekten.  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>Lesen und Schreiben von XML-Daten mit SQLXML-Objekten  
 Die folgende Liste beschreibt, wie die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API-Methoden zum Lesen und Schreiben von XML-Daten mit SQLXML-Objekten:  
  
-   Um ein SQLXML-Objekt zu erstellen, verwenden die [CreateSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Beachten Sie, dass mit dieser Methode ein SQLXML-Objekt ohne Daten erstellt wird. Hinzuzufügende **Xml** Daten mit SQLXML-Objekt, rufen Sie eine der folgenden Methoden, die in der SQLXML-Schnittstelle angegeben werden: z. B. SetResult, SetCharacterStream, SetBinaryStream, oder SetString.  
  
-   Verwenden Sie zum Abrufen der eigentlichen SQLXML-Objekts der GetSQLXML-Methoden von der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse oder die [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse.  
  
-   Zum Abrufen der **Xml** Daten aus einem SQLXML-Objekt, verwenden Sie eine der folgenden Methoden, die in der SQLXML-Schnittstelle angegeben werden: GetSource, GetCharacterStream, GetBinaryStream, oder GetString.  
  
-   Beim Aktualisieren der **Xml** Daten in einem SQLXML-Objekt verwenden die [UpdateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.  
  
-   Zum Speichern eines SQLXML-Objekts in eine Datenbanktabellen-Spalte vom Typ **Xml**, verwenden Sie die SetSQLXML-Methoden von der [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse oder die [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)Klasse.  
  
 Der Beispielcode in [SQLXML Typ Datenbeispiel](../../connect/jdbc/sqlxml-data-type-sample.md) veranschaulicht, wie dieser allgemeinen API-Aufgaben.  
  
## <a name="readable-and-writable-sqlxml-objects"></a>Lesbare und schreibbare SQLXML-Objekte  
 In der folgenden Tabelle sind die Typen von SQLXML-Objekten aufgeführt, die von den von der JDBC-API bereitgestellten Methoden zum Festlegen, Abrufen und Aktualisieren unterstützt werden. Die Spalten der Tabelle haben die folgende Bedeutung:  
  
-   Die **Methodennamen** Spalte listet die unterstützten Getter und Setter Updater-Methoden in der JDBC-API.  
  
-   Die **SQLXML-Abrufobjekt** Spalte stellt ein SQLXML-Objekt, das entweder erstellt wird die [GetSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) Methode der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse oder der [GetSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.  
  
-   Die **SQLXML-Festlegungsobjekt** Spalte stellt ein SQLXML-Objekt, das von erstellt wird die [CreateSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Beachten Sie, dass akzeptieren Sie die unten aufgeführten festlegungsmethoden nur ein SQLXML-Objekt, das erstellt, indem die [CreateSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) Methode.  
  
|Methodenname|SQLXML-Abrufobjekt<br /><br /> (Lesbar)|SQLXML-Festlegungsobjekt<br /><br /> (Schreibbar)|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement.setSQLXML()|Nicht unterstützt.|Supported|  
|CallableStatement.setObject()|Nicht unterstützt.|Supported|  
|PreparedStatement.setSQLXML()|Nicht unterstützt.|Supported|  
|PreparedStatement.setObject()|Nicht unterstützt.|Supported|  
|ResultSet.updateSQLXML()|Nicht unterstützt.|Supported|  
|ResultSet.updateObject()|Nicht unterstützt.|Supported|  
|ResultSet.getSQLXML()|Supported|Nicht unterstützt.|  
|CallableStatement.getSQLXML()|Supported|Nicht unterstützt.|  
  
 Wie in der Tabelle oben angegeben ist, können die SQLXML-Festlegungsmethoden nicht mit den lesbaren SQLXML-Objekten verwendet werden. Entsprechend können die Abrufmethoden nicht mit den schreibbaren SQLXML-Objekten verwendet werden.  
  
 Wenn die Anwendung die SetObject-Methode aufruft, durch Angeben eines skalierungs- oder längenparameters mit einem SQLXML-Objekt, wird der Parameter skalierungs- oder Längenparameter ignoriert.  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>Richtlinien und Einschränkungen für die Verwendung von SQLXML-Objekten  
 Anwendungen können mit SQLXML-Objekten XML-Daten aus einer Datenbank lesen oder in diese schreiben. Die folgende Liste enthält Informationen über bestimmte Einschränkungen und Richtlinien für die Verwendung von SQLXML-Objekten.  
  
-   Ein SQLXML-Objekt kann nur für die Dauer der Transaktion gültig sein, für die es erstellt wurde.  
  
-   Ein von einer Abrufmethode empfangenes SQLXML-Objekt kann nur zum Lesen von Daten verwendet werden.  
  
-   Ein vom Verbindungsobjekt erstelltes SQLXML-Objekt kann nur zum Schreiben von Daten verwendet werden.  
  
-   Die Anwendung kann zum Lesen von Daten nur eine Abrufmethode für ein lesbares SQLXML-Objekt aufrufen. Nach dem Aufruf der Abrufmethode führen alle weiteren Abruf- oder Festlegungsmethoden für das gleiche SQLXML-Objekt zu einem Fehler.  
  
-   Die Anwendung kann nur die free-Methode auf das SQLXML-Objekt aufrufen, nachdem sie gelesen oder geschrieben wird. Es ist jedoch weiterhin möglich, den zurückgegebenen Datenstrom oder die zurückgegebene Quelle zu verarbeiten, solange die zugrunde liegende Spalte oder der zugrunde liegende Parameter aktiv ist. Wenn die zugrunde liegende Spalte oder der zugrunde liegende Parameter nicht mehr aktiv ist, wird der Datenstrom oder die Quelle geschlossen, der bzw. die dem SQLXML-Objekt zugeordnet ist. Wenn die zugrunde liegende Spalte oder der zugrunde liegende Parameter nicht mehr gültig ist, stehen die zugrunde liegenden Daten den Abrufmethoden des Datenstroms, der SAX (Simple API for XML) und der StAX (Streaming API for XML) nicht zur Verfügung.  
  
-   Die Anwendung kann nur eine Festlegungsmethode für ein schreibbares SQLXML-Objekt aufrufen. Nach dem Aufruf der Festlegungsmethode führen alle weiteren Abruf- oder Festlegungsmethoden für das gleiche SQLXML-Objekt zu einem Fehler.  
  
-   Damit Daten für das SQLXML-Objekt festgelegt werden können, muss die Anwendung die entsprechende Festlegungsmethode und die Funktionen im zurückgegebenen Objekt verwenden.  
  
-   GetSQLXML-Methoden von der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse und die [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) zurück **null** Daten, wenn die zugrunde liegende Spalte ist**null**.  
  
-   Die Festlegungsobjekte können für die Dauer der Verbindung gültig sein, in der sie erstellt wurden.  
  
-   Anwendungen sind nicht zulässig, zum Festlegen einer **null** Wert mithilfe der von der SQLXML-Schnittstelle bereitgestellten festlegungsmethoden. Die Anwendungen können mithilfe der von der SQLXML-Schnittstelle bereitgestellten Festlegungsmethoden eine leere Zeichenfolge ("") festlegen. Festlegen einer **null** Wert, der Anwendungen sollten rufen Sie eine der folgenden:  
  
    -   SetNull-Methoden von der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse und [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse.  
  
    -   SetObject-Methoden von der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse und [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse.  
  
    -   SetSQLXML-Methoden von der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse und [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) -Klasse mit einem **null** Parameterwert.  
  
-   Für die Arbeit mit XML-Dokumenten wird aus Leistungsgründen die Verwendung der SAX (Simple API for XML)- und StAX (Streaming API for XML)-Parser anstelle von DOM (Document Object Model)-Parsern empfohlen.  
  
 XML-Parser können leere Werte nicht behandeln. SQL Server erlaubt Anwendungen jedoch das Abrufen und Speichern leerer Werte aus bzw. in Datenbankspalten mit dem XML-Datentyp. Dies bedeutet, dass beim Analysieren der XML-Daten vom Parser eine Ausnahme ausgelöst wird, wenn der zugrunde liegende Wert leer ist. Bei DOM-Ausgaben fängt der JDBC-Treiber die Ausnahme ab und löst einen Fehler aus. Bei SAX- und StAX-Ausgaben stammt der Fehler direkt vom Parser.  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>Adaptive Pufferung und SQLXML-Unterstützung  
 Die vom SQLXML-Objekt zurückgegebenen Binär- und Zeichendatenströme richten sich nach den Modi für die adaptive oder vollständige Pufferung. Wenn die XML-Parser hingegen keine Datenströme sind, berücksichtigen sie die Einstellungen für adaptive oder vollständige Pufferung nicht. Weitere Informationen zur adaptiven Pufferung finden Sie unter [mithilfe der adaptiven Pufferung](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützen von XML-Daten](../../connect/jdbc/supporting-xml-data.md)  
  
  
