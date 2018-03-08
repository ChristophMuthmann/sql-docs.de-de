---
title: Verwenden von Standarddatentypen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2018
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
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 66da5301a12427ed50a212abf74a0700d89e8668
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="using-basic-data-types"></a>Verwenden von Standarddatentypen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] verwendet die JDBC-Standarddatentypen konvertieren die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen in ein Format, das von der Programmiersprache Java ab (und umgekehrt) verarbeitet werden können. Der JDBC-Treiber bietet Unterstützung für die JDBC 4.0-API, darunter die **SQLXML** -Datentyp und nationale (Unicode-) Datentypen, wie z. B. **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, und **NCLOB**.  
  
## <a name="data-type-mappings"></a>Datentypzuordnungen  
 In der folgenden Tabelle enthält eine Liste der standardzuordnungen zwischen den-Standarddatentypen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und Java-Datentypen:  
  
|SQL Server-Typen|JDBC-Typen (java.sql.Types)|Java-Typen|  
|----------------------|-----------------------------------|-------------------------|  
|bigint|bigint|long|  
|BINARY|BINARY|byte[]|  
|bit|BIT|boolean|  
|char|CHAR|String|  
|Datum|DATE|java.sql.Date|  
|datetime|TIMESTAMP|java.sql.Timestamp|  
|datetime2|TIMESTAMP|java.sql.Timestamp|  
|datetimeoffset (2)|microsoft.sql.Types.DATETIMEOFFSET|microsoft.sql.DateTimeOffset|  
|Decimal|DECIMAL|java.math.BigDecimal|  
|float|DOUBLE|double|  
|image|LONGVARBINARY|byte[]|  
|int|INTEGER|int|  
|money|DECIMAL|java.math.BigDecimal|  
|NCHAR|CHAR<br /><br /> NCHAR (Java SE 6.0)|String|  
|ntext|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String|  
|numeric|NUMERIC|java.math.BigDecimal|  
|nvarchar|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|String|  
|nvarchar(max)|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|String|  
|real|real|float|  
|smalldatetime|TIMESTAMP|java.sql.Timestamp|  
|smallint|SMALLINT|short|  
|smallmoney|DECIMAL|java.math.BigDecimal|  
|text|LONGVARCHAR|String|  
|Uhrzeit|TIME (1)|java.sql.Time (1)|  
|timestamp|BINARY|byte[]|  
|tinyint|TINYINT|short|  
|udt|VARBINARY|byte[]|  
|uniqueidentifier|CHAR|String|  
|varbinary|VARBINARY|byte[]|  
|varbinary(max)|VARBINARY|byte[]|  
|varchar|VARCHAR|String|  
|varchar(max)|VARCHAR|String|  
|xml|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String<br /><br /> SQLXML|  
|SQLVARIANT|SQLVARIANT|Objekt|  
  
 (1) für die Verwendung von java.sql.Time mit der Zeit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] geben, müssen Sie festlegen der **SendTimeAsDatetime** Verbindungseigenschaft auf "false".  
  
 (2) Sie können die Werte programmgesteuert zugreifen **"DateTimeOffset"** mit ["DateTimeOffset"-Klasse](../../connect/jdbc/reference/datetimeoffset-class.md).  
  
 Die folgenden Abschnitte enthalten Beispiele für die Verwendung des JDBC-Treibers und der Standarddatentypen. Ein ausführlicheres Beispiel zur Verwendung der Standarddatentypen in einer Java-Anwendung finden Sie unter [grundlegende Standarddatentypen-Beispiel](../../connect/jdbc/basic-data-types-sample.md).  
  
## <a name="retrieving-data-as-a-string"></a>Abrufen von Daten als Zeichenfolge  
 Wenn Sie zum Abrufen von Daten aus einer Datenquelle, die einem der JDBC-Standarddatentypen für die Anzeige als Zeichenfolge zugeordnet, oder wenn Sie stark typisierte Daten nicht erforderlich ist, können Sie mithilfe der [GetString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) -Klasse, wie im folgenden:  
  
 [!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>Abrufen von Daten nach Datentyp  
 Wenn Sie zum Abrufen von Daten aus einer Datenquelle, und Sie wissen, dass des Typs der Daten, die abgerufen wird, verwenden Sie eine der Get\<Typ >-Methoden von SQLServerResultSet-Klasse, auch bekannt als die *Abrufmethoden*. Sie können einen Spaltennamen oder einen Spaltenindex verwenden, mit dem Get\<Typ > Methoden, wie im folgenden:  
  
 [!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
>  Die GetUnicodeStream GetBigDecimal mit Skalierung Methoden sind veraltet und werden vom JDBC-Treiber nicht unterstützt.  
  
## <a name="updating-data-by-data-type"></a>Aktualisieren von Daten nach Datentyp  
 Wenn Sie den Wert eines Felds in einer Datenquelle aktualisieren müssen, gehen Sie das Update\<Typ >-Methoden der SQLServerResultSet-Klasse. Im folgenden Beispiel die [UpdateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) Methode dient in Verbindung mit der [UpdateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) Methode, um die Daten in der Datenquelle zu aktualisieren:  
  
 [!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
>  Der JDBC-Treiber kann keine SQL Server-Spalte mit einem Spaltennamen aktualisieren, dessen Länge mehr als 127 Zeichen beträgt. Wenn ein Update einer Spalte, deren Name mehr als 127 Zeichen umfasst, ausgeführt werden soll, wird eine Ausnahme ausgegeben.  
  
## <a name="updating-data-by-parameterized-query"></a>Aktualisieren von Daten durch parametrisierte Abfragen  
 Wenn Sie zum Aktualisieren von Daten in einer Datenquelle mithilfe einer parametrisierten Abfrage verfügen, legen Sie den Datentyp der Parameter mithilfe des Satzes\<Typ > Methoden der [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse, auch bekannt als die *festlegungsmethoden*. Im folgenden Beispiel die [PrepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) Methode wird verwendet, um die parametrisierte Abfrage, und klicken Sie dann die [SetString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) Methode wird verwendet, um den Zeichenfolgenwert des Parameters vor dem festzulegen[ExecuteUpdate](../../connect/jdbc/reference/executeupdate-method.md) -Methode aufgerufen wird.  
  
 [!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
 Weitere Informationen zu parametrisierten Abfragen finden Sie unter [mit SQL-Anweisungen mit Parametern](../../connect/jdbc/using-an-sql-statement-with-parameters.md).  
  
## <a name="passing-parameters-to-a-stored-procedure"></a>Übergeben von Parametern an gespeicherte Prozeduren  
 Wenn Sie typisierte Parameter an eine gespeicherte Prozedur übergeben müssen, Sie können festlegen der Parameter über einen Index oder Name mithilfe des Satzes\<Typ > Methoden der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse. Im folgenden Beispiel die [PrepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) Methode wird verwendet, um den Aufruf der gespeicherten Prozedur einrichten und dann die [SetString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) Methode wird verwendet, um die Parameter für den Aufruf vor dem Festlegen der [ ExecuteQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) -Methode aufgerufen wird.  
  
 [!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
>  In diesem Beispiel wird ein Resultset zurückgegeben, das die Ergebnisse der gespeicherten Prozedur enthält.  
  
 Weitere Informationen zur Verwendung des JDBC-Treibers mit gespeicherten Prozeduren und Eingabeparametern finden Sie unter [mithilfe einer gespeicherten Prozedur mit Eingabeparametern](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md).  
  
## <a name="retrieving-parameters-from-a-stored-procedure"></a>Abrufen von Parametern von gespeicherten Prozeduren  
 Wenn Sie Parameter wieder von einer gespeicherten Prozedur abrufen müssen, müssen Sie zuerst registrieren einen Out-Parameter nach Name oder Index mithilfe der [RegisterOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) Methode der SQLServerCallableStatement-Klasse, und weisen Sie anschließend die zurückgegebenen out-Parameter einer geeigneten Variablen nach dem Aufruf der gespeicherten Prozedur. Im folgenden Beispiel wird die PrepareCall-Methode zum Einrichten des Aufrufs der gespeicherten Prozedur verwendet, die RegisterOutParameter-Methode wird verwendet, um das Einrichten des Out-Parameters, und klicken Sie dann die [SetString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) Methode wird zum Festlegen des Parameters für die Rufen Sie vor der ExecuteQuery-Methode aufgerufen wird. Der Wert, der von der Out-Parameter der gespeicherten Prozedur zurückgegebene wird abgerufen, wobei die [GetShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) Methode.  
  
 [!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
>  Zusätzlich zum zurückgegebenen out-Parameter kann auch ein Resultset zurückgegeben werden, das die Ergebnisse der gespeicherten Prozedur enthält.  
  
 Weitere Informationen zur Verwendung des JDBC-Treibers mit gespeicherten Prozeduren und Ausgabeparametern finden Sie unter [mithilfe einer gespeicherten Prozedur mit Ausgabeparameter](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
