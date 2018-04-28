---
title: Mithilfe von erweiterten Datentypen | Microsoft Docs
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
ms.topic: article
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
caps.latest.revision: 58
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: df610dec98d98d497b21b5e297781fa0a3375bf8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-advanced-data-types"></a>Verwenden von erweiterten Datentypen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] verwendet die erweiterten JDBC-Datentypen konvertieren die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen in ein Format, das von der Programmiersprache Java verarbeitet werden können, Programmiersprache.  
  
## <a name="remarks"></a>Hinweise  
 In der folgenden Tabelle enthält eine Liste der standardzuordnungen zwischen den erweiterten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und Java-Datentypen.  
  
|SQL Server-Typen|JDBC-Typen (java.sql.Types)|Java-Typen|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|Byte [] \(Standard), Blob, InputStream, String|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String (Standard), Clob, InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (Standard), Clob, NClob (Java SE 6.0)|  
|xml|LONGVARCHAR<br /><br /> SQLXML (Java SE 6.0)|String (Standard), InputStream, Clob, byte[], Blob, SQLXML (Java SE 6.0)|  
|UDT<sup>1</sup>|VARBINARY|String (Standard), byte[], InputStream|  
  
 <sup>1</sup> der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt das Senden und Abrufen von CLR-UDTs als binäre Daten, jedoch keine Bearbeitung von CLR-Metadaten.  
  
 Die folgenden Abschnitte enthalten Beispiele für die Verwendung des JDBC-Treibers und der erweiterten Datentypen.  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>BLOB-, CLOB- und NCLOB-Datentypen  
 Der JDBC-Treiber implementiert alle Methoden der java.sql.Blob-, java.sql.Clob- und java.sql.NClob-Schnittstellen.  
  
> [!NOTE]  
>  CLOB-Werte verwendet werden können, mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] (oder höher) Datentypen mit umfangreichen Werten. Insbesondere können CLOB-Typen verwendet werden, mit der **varchar(max)** und **nvarchar(max)** -Datentypen BLOB-Typen können verwendet werden mit **varbinary(max)** und **Bild**  Datentypen sowie NCLOB-Typen mit verwendet werden können **Ntext** und **nvarchar(max)**.  
  
## <a name="large-value-data-types"></a>Datentypen mit umfangreichen Werten  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], arbeiten mit Datentypen mit umfangreichen Werten Typen eine besondere Behandlung erforderlich. Datentypen mit umfangreichen Werten sind solche, die die maximale Zeilengröße von 8 KB überschreiten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Führt einen maximalbezeichner für **Varchar**, **Nvarchar**, und **Varbinary** Datentypen um Speicherung von Werten zu ermöglichen, die so groß wie 2 ^ 31 Byte. Spalten der Tabelle und [!INCLUDE[tsql](../../includes/tsql_md.md)] Variablen festlegbaren **varchar(max)**, **nvarchar(max)**, oder **varbinary(max)** Datentypen.  
  
 Die Verarbeitung von Typen mit umfangreichen Werten umfasst hauptsächlich das Abrufen aus einer Datenbank sowie das Hinzufügen zu einer Datenbank. Die folgenden Abschnitte beschreiben die verschiedenen Verfahren für diese Aufgaben.  
  
### <a name="retrieving-large-value-types-from-a-database"></a>Abrufen von Typen mit umfangreichen Werten aus einer Datenbank  
 Beim Abrufen eines nicht-Binary-Datentypen mit umfangreichen Werten-Typs – z. B. die **varchar(max)** Datentyp – aus einer Datenbank ein Ansatz besteht darin, diese Daten als Zeichenstream lesen. Im folgenden Beispiel die [ExecuteQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse dient zum Abrufen von Daten aus der Datenbank, und es als Resultset zurückgegeben. Die [GetCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse wird verwendet, um die Daten mit großen Werten aus dem Resultset gelesen.  
  
```  
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```  
  
> [!NOTE]  
>  Diese Vorgehensweise kann auch verwendet werden, für die **Text**, **Ntext**, und **nvarchar(max)** Datentypen.  
  
 Beim Abrufen von eines binärer Datentyps mit umfangreichen Werten – z. B. die **varbinary(max)** Datentyp – aus einer Datenbank, es gibt verschiedene Methoden, die Sie ergreifen können. Die effizienteste Vorgehensweise besteht darin, die Daten als Binärdatenstrom zu lesen, wie z. B.:  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```  
  
 Sie können auch die [GetBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) Methode zum Lesen der Daten als Bytearray, wie im folgenden:  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```  
  
> [!NOTE]  
>  Die Daten können auch als BLOB gelesen werden. Diese Vorgehensweise ist jedoch weniger effizient als die beiden oben erwähnten Methoden.  
  
### <a name="adding-large-value-types-to-a-database"></a>Hinzufügen von Typen mit umfangreichen Werten zu einer Datenbank  
 Das Hochladen von umfangreichen Daten mit dem JDBC-Treiber funktioniert problemlos, wenn die Daten in den Arbeitsspeicher passen. Wenn der Umfang der Daten größer ist als der Arbeitsspeicher, sollte Streaming verwendet werden. Die effizienteste Möglichkeit für das Hochladen von umfangreichen Daten bilden die stream-Schnittstellen.  
  
 Es besteht auch die Möglichkeit, eine Zeichenfolge oder Bytes zu verwenden, wie z. B.:  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```  
  
> [!NOTE]  
>  Dieser Ansatz kann auch verwendet werden, für Werte, die im rowsetcache **Text**, **Ntext**, und **nvarchar(max)** Spalten.  
  
 Wenn Sie auf dem Server eine Bildbibliothek vorhanden und muss alle binären Bilddateien zum Hochladen einer **varbinary(max)** Spalte, die effizienteste Methode mit dem JDBC-Treiber ist Datenströme direkt, wie im folgenden verwenden:  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)");  
File inputFile = new File("CLOBFile20mb.jpg");  
FileInputStream inStream = new FileInputStream(inputFile);  
int id = 1;  
pstmt.setInt(1,id);  
pstmt.setBinaryStream(2, inStream);  
pstmt.executeUpdate();  
inStream.close();  
```  
  
> [!NOTE]  
>  Das Hochladen von umfangreichen Daten mit der CLOB- oder BLOB-Methode ist nicht effizient.  
  
### <a name="modifying-large-value-types-in-a-database"></a>Ändern von Typen mit umfangreichen Werten in einer Datenbank  
 In den meisten Fällen ist die empfohlene Methode zum Aktualisieren oder Ändern von umfangreichen Werten in der Datenbank zum Übergeben von Parametern über die [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) und [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klassen Mithilfe von [!INCLUDE[tsql](../../includes/tsql_md.md)] Befehle wie UPDATE, WRITE und SUBSTRING.  
  
 Ersetzen eines Worts in einer großen Textdatei, z. B. einer archivierten HTML-Datei haben, können Sie ein Clob-Objekts, wie im folgenden:  
  
```  
String SQL = "SELECT * FROM test1;";  
Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
ResultSet rs = stmt.executeQuery(SQL);  
rs.next();  
  
Clob clob = rs.getClob(2);  
long pos = clob.position("dog", 1);  
clob.setString(pos, "cat");  
rs.updateClob(2, clob);  
rs.updateRow();  
```  
  
 Darüber hinaus besteht die Möglichkeit, die gesamte Arbeit auf dem Server auszuführen und lediglich Parameter an eine vorbereitete UPDATE-Anweisung zu übergeben.  
  
 Weitere Informationen zu Typen mit umfangreichen Werten finden Sie in der SQL Server-Onlinedokumentation unter "Verwenden von Datentypen mit umfangreichen Werten".  
  
## <a name="xml-data-type"></a>XML-Datentyp  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Stellt eine **Xml** -Datentyp, der ermöglicht Ihnen das Speichern von XML-Dokumenten und-Fragmenten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Die **Xml** -Datentyp ist ein integrierter Datentyp in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und einige auf ähnliche Weise wie andere integrierten Typen wie **Int** und **Varchar**. Wie andere integrierte Typen können Sie mit der **Xml** -Datentyp als Spaltentyp, wenn Sie eine Tabelle erstellen, als Variablentyp, Parametertyp oder Funktionsrückgabetyp; oder in [!INCLUDE[tsql](../../includes/tsql_md.md)] Funktionen CAST und CONVERT.  
  
 In der JDBC-Treiber die **Xml** -Datentyp kann als Zeichenfolge, Byte-Array, Datenstrom, CLOB-, BLOB- oder SQLXML-Objekt zugeordnet werden. Der Standard lautet Zeichenfolge. Ab JDBC Driver, Version 2.0, unterstützt der JDBC-Treiber die JDBC 4.0-API, in der die SQLXML-Schnittstelle eingeführt wurde. Die SQLXML-Schnittstelle definiert Methoden zum interagieren und Bearbeiten von XML-Daten. Die **SQLXML** -Datentyp zugeordnet, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Xml** -Datentyp. Weitere Informationen zum Lesen und Schreiben von XML-Daten in bzw. aus einer relationalen Datenbank mit der **SQLXML** Java-Datentyp finden Sie unter [unterstützende XML-Daten](../../connect/jdbc/supporting-xml-data.md).  
  
 Die Implementierung der **Xml** -Datentyp in der JDBC-Treiber bietet Unterstützung für Folgendes:  
  
-   Zugriff auf XML-Daten als normale Java UTF-16-Zeichenfolge bei den gebräuchlichsten Programmierszenarien  
  
-   Eingabe von UTF-8- und anderen 8-Bit-codierten XML-Daten  
  
-   Zugriff auf XML-Daten als Bytearray mit führender Bytereihenfolgemarke (Byte Order Mark, BOM) bei Codierung in UTF-16 für den Austausch mit anderen XML-Prozessoren und Datenträgerdateien  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] setzt eine führende BOM für UTF-16-codierte XML. Die Anwendung muss diese bereitstellen, wenn XML-Parameterwerte als Bytearrays angegeben werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] XML-Werte gibt immer als UTF-16-ohne BOM Zeichenfolgen oder Codierungsdeklaration eingebettete aus. Wenn XML-Werte als "byte[]", "BinaryStream" oder "Blob" abgerufen werden, steht vor dem Wert ein UTF-16-BOM.  
  
 Weitere Informationen zu den **Xml** -Datentyp, finden Sie unter "Xml-Datentyp" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="user-defined-data-type"></a>User-Defined Data Type  
 Die Einführung von benutzerdefinierten Typen (UDTs) in [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] erweitert die SQL-Typsystem werden, wenn Sie das Speichern von Objekten und benutzerdefinierte Datenstrukturen in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. UDTs können mehrere Datentypen enthalten und Verhalten zeigen, das sie von den herkömmlichen Aliasdatentypen aus einem einzelnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Systemdatentyp unterscheidet. UDTs werden mit einer der von der Microsoft .NET Common Language Runtime (CLR) unterstützten Sprachen definiert, die überprüfbaren Code erzeugen. Dazu gehören Visual C# und Visual Basic .NET. Die Daten werden als Felder und Eigenschaften einer .NET Framework-basierten Klasse oder Struktur offen gelegt. Die Verhalten werden durch Methoden der Klasse bzw. Struktur definiert.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ein UDT als Spaltendefinition einer Tabelle, als Variable in verwendet werden kann eine [!INCLUDE[tsql](../../includes/tsql_md.md)] Batch oder als Argument einer [!INCLUDE[tsql](../../includes/tsql_md.md)] Funktion oder gespeicherten Prozedur.  
  
 Weitere Informationen zu benutzerdefinierten Datentypen finden Sie unter "Verwenden und Ändern von Instanzen von benutzerdefinierten Typen" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
