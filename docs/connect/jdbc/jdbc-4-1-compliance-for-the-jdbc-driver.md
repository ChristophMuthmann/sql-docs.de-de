---
title: "JDBC 4.1-Kompatibilität für JDBC Driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f087fd40-8451-478e-b465-43112c711515
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: d5b8e44c007766354e5c03058d16a41cbb72ad0e
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="jdbc-41-compliance-for-the-jdbc-driver"></a>JDBC 4.1-Kompatibilität für den JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Versionen von Microsoft JDBC Driver für SQL Server vor Version 4.2 sind mit der Java Database Connectivity API 4.0-Spezifikation kompatibel. Dieser Abschnitt trifft auf Versionen vor der Version 4.2 nicht zu.  
  
 Die Java Database Connectivity API 4.1-Spezifikation wird von Microsoft JDBC Driver 4.2 für SQL Server mit den folgenden API-Methoden unterstützt.  
  
 **SQLServerConnection-Klasse**  
  
|Methode „New“|Description|JDBC-Treiber-Implementierung|  
|----------------|-----------------|--------------------------------|  
|void abort(Executor executor)|Beendet eine geöffnete Verbindung mit SQL Server.|Wird wie unter der java.sql.Connection-Schnittstelle beschrieben implementiert. Weitere Informationen finden Sie unter [java.sql.Connection](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
|void setSchema(String schema)|Legt das Schema für die aktuelle Verbindung fest.|SQL Server unterstützt das Festlegen des Schemas für die aktuelle Sitzung nicht. Der Treiber protokolliert stumm eine Warnmeldung, wenn diese Methode aufgerufen wird. Weitere Informationen finden Sie unter [java.sql.Connection](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
|String „getSchema()“|Gibt den Schemanamen für die aktuelle Verbindung zurück.|Da SQL Server das Festlegen des Schemas für die aktuelle Verbindung nicht unterstützt, gibt der Treiber stattdessen das Standardschema des Benutzers zurück. Weitere Informationen finden Sie unter [java.sql.Connection](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
  
 **SQLServerDatabaseMetaData-Klasse**  
  
|Methode „New“|Description|JDBC-Treiber-Implementierung|  
|----------------|-----------------|--------------------------------|  
|boolean generatedKeyAlwaysReturned()|Gibt „true“ zurück, da der Treiber das Abrufen von generierten Schlüsseln unterstützt|Wird wie für java.sql beschrieben implementiert. DatabaseMetaData-Schnittstelle. Weitere Informationen finden Sie unter [java.sql.DatabaseMetaData](http://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html).|  
|ResultSet getPseudoColumns(String catalog, String schemaPattern,String tableNamePattern,String columnNamePattern)|Ruft eine Beschreibung der Pseudospalten bzw. ausgeblendeten Spalten ab|Gibt eine leere Ergebnismenge zurück, da Pseudospalten in SQL Server formal nicht definiert sind. Weitere Informationen finden Sie unter [java.sql.DatabaseMetaData](http://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html).|  
  
 **SQLServerStatement-Klasse**  
  
|Methode „New“|Description|JDBC-Treiber-Implementierung|  
|----------------|-----------------|--------------------------------|  
|void closeOnCompletion()|Gibt an, dass diese Anweisung geschlossen wird, wenn alle ihre abhängigen Resultsets geschlossen werden.|Wird wie unter der java.sql.Statement-Schnittstelle beschrieben implementiert. Weitere Informationen finden Sie unter [java.sql.Statement](http://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html).|  
|boolean isCloseOnCompletion()|Gibt einen Wert zurück, der anzeigt, ob diese Anweisung geschlossen wird, wenn alle ihre abhängigen Resultsets geschlossen werden.|Wird wie unter der java.sql.Statement-Schnittstelle beschrieben implementiert. Weitere Informationen finden Sie unter [java.sql.Statement](http://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html).|  
  
 Die Java Database Connectivity API 4.1-Spezifikation wird von Microsoft JDBC Driver 4.2 für SQL Server mit den folgenden Funktionen unterstützt.  
  
|Neue Funktion|Description|  
|-----------------|-----------------|  
|Neue Escape-Funktion<br /><br /> Limited Return Rows Escape|Teilweise unterstützt<br /><br /> Escape-Syntax: LIMIT \<Zeilen > [OFFSET < Row_offset >](using-sql-escape-sequences.md).|  
  
 Die Java Database Connectivity API 4.1-Spezifikation wird von Microsoft JDBC Driver 4.2 für SQL Server mit den folgenden Datentypzuordnungen unterstützt.  
  
|Datentypzuordnungen|Description|  
|------------------------|-----------------|  
|In den Methoden „PreparedStatement.setObject()“ und „PreparedStatement.setNull()“ werden jetzt neue Datentypzuordnungen unterstützt.|1. Neue Java- zu JDBC-Typzuordnung<br /><br /> (a) java.math.BigInteger zu JDBC BIGINT<br /><br /> (b) java.util.Date und java.util.Calendar zu JDBC TIMESTAMP<br /><br /> 2. Neue Datentypkonvertierungen:<br /><br /> (a) java.math.BigInteger zu CHAR, VARCHAR, LONGVARCHAR und BIGINT<br /><br /> (b) java.util.Date und java.util.Calendar zu CHAR, VARCHAR, LONGVARCHAR, DATE, TIME und TIMESTAMP<br /><br /> Weitere Informationen finden Sie in der JDBC 4.1-Spezifikation.|  
  
  
