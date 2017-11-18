---
title: Verwenden von Tabellenwertparametern | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
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
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 91777796843557cf6c5e6f7667994d7743b608a0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-table-valued-parameters"></a>Verwenden von Tabellenwertparametern
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Tabellenwertparameter bieten eine einfache Möglichkeit, mehrere Datenzeilen aus einer Clientanwendung mit SQL Server zu marshallen, ohne dass mehrere Roundtrips oder spezielle serverseitige Logik für die Verarbeitung der Daten. Tabellenwertparameter können Sie Datenzeilen in einer Clientanwendung zu kapseln und die Daten in einem einzelnen parametrisierten Befehl an den Server gesendet. Die eingehenden Datenzeilen werden in einer Tabellenvariablen gespeichert, die Sie dann auf mithilfe von Transact-SQL bearbeitet werden können.  
  
 Spaltenwerte in Tabellenwertparametern können mithilfe standardmäßiger Transact-SQL SELECT-Anweisungen zugegriffen werden. Tabellenwertparameter sind stark typisiert, und deren Struktur werden automatisch überprüft. Die Größe der Tabellenwertparameter wird nur vom Serverarbeitsspeicher beschränkt.  
  
> [!NOTE]  
>  Unterstützung für Tabellenwertparameter ist ab Microsoft JDBC Driver 6.0 für SQL Server verfügbar.  
  
> [!NOTE]  
>  Sie können keine Daten in einem Tabellenwertparameter zurückgeben. Tabellenwertparameter sind reine; Die OUTPUT-Schlüsselwort wird nicht unterstützt.  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter den folgenden Ressourcen.  
  
|Ressource|Description|  
|--------------|-----------------|  
|[Tabellenwertparameter (Datenbankmodul)](http://go.microsoft.com/fwlink/?LinkId=98363) in SQL Server-Onlinedokumentation|Beschreibt das Erstellen und Verwenden von Tabellenwertparametern|  
|[Benutzerdefinierte Tabellentypen](http://go.microsoft.com/fwlink/?LinkId=98364) in SQL Server-Onlinedokumentation|Beschreibt benutzerdefinierte Tabellentypen, die zum Deklarieren von Tabellenwertparametern verwendet werden|  
|Die [Microsoft SQL Server-Datenbankmoduls](http://go.microsoft.com/fwlink/?LinkId=120507) Abschnitt von CodePlex|Enthält Beispiele, die veranschaulichen, wie mithilfe von SQL Server-Features und Funktionen|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Übergeben von mehreren Zeilen in früheren Versionen von SQLServer  
 Bevor Tabellenwertparameter auf SQL Server 2008 eingeführt wurden, wurden die Optionen zum Übergeben mehrerer Datenzeilen an eine gespeicherte Prozedur oder einen parametrisierten SQL‑Befehl beschränkt. Ein Entwickler konnte aus folgenden Optionen zum Übergeben mehrerer Zeilen an den Server auswählen:  
  
-   Verwenden Sie eine Reihe einzelner Parameter, um die Werte in mehreren Spalten und Zeilen der Daten darzustellen. Die Menge der Daten, die mit dieser Methode übergeben werden können, wird durch die Anzahl der zulässigen Parameter beschränkt. SQL Server-Prozeduren können, darf höchstens über 2100 Parameter verfügen. Serverseitige Logik ist erforderlich, um diese einzelnen Werte in eine Tabellenvariable oder eine temporäre Tabelle für die Verarbeitung zu assemblieren.  
  
-   Mehrere Datenwerte in voneinander getrennten Zeichenfolgen oder XML-Dokumenten zu bündeln und diese Textwerte anschließend an eine Prozedur oder Anweisung zu übergeben. Dies muss die Prozedur oder Anweisung, um die erforderliche Logik zum Überprüfen der Datenstrukturen und Entbündeln enthalten die Werte.  
  
-   Erstellen Sie eine Reihe einzelner SQL-Anweisungen für datenänderungen, die mehrere Zeilen auswirken. Änderungen können einzeln an den Server gesendet oder in Gruppen gestapelt werden. Allerdings wird auch verwendet werden, wenn in Batches übermittelt, die mehrere-Anweisungen enthalten, jede Anweisung separat auf dem Server ausgeführt.  
  
-   Die Bcp-Hilfsprogramm verwenden oder die ["sqlserverbulkcopy"](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx) Objekt, das viele Datenzeilen in einer Tabelle zu laden. Obwohl diese Technik sehr effizient ist, unterstützt es nicht für serverseitige Verarbeitung, es sei denn, die Daten in eine temporäre Tabelle oder Tabellenvariable geladen werden.  
  
## <a name="creating-table-valued-parameter-types"></a>Erstellen von Tabellenwertparameter-Typen  
 Tabellenwertparameter basieren auf stark typisierten Tabellenstrukturen, die mithilfe von Transact-SQL CREATE TYPE-Anweisungen definiert sind. Sie müssen einen Tabellentyp erstellen und definieren die Struktur in SQL Server, bevor Sie Tabellenwertparameter in Ihren Clientanwendungen verwenden können. Weitere Informationen zum Erstellen von Tabellentypen finden Sie unter [benutzerdefinierte Tabellentypen](http://go.microsoft.com/fwlink/?LinkID=98364) in SQL Server-Onlinedokumentation.  
  
```  
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 Deklarieren Sie nach dem Erstellen eines Tabellentyps können Tabellenwertparameter basierend auf diesen Typ. Das folgende Transact-SQL-Fragment veranschaulicht, wie ein Tabellenwertparameter in der Definition einer gespeicherten Prozedur deklarieren. Beachten Sie, dass die READONLY-Schlüsselwort zum Deklarieren von-Tabellenwertparameter erforderlich ist.  
  
```  
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Ändern von Daten mit Tabellenwertparametern (Transact-SQL)  
 Tabellenwertparameter können in satzbasierte datenänderungen verwendet werden, die auf durch die Ausführung einer einzelnen Anweisung mehrere Zeilen auswirken. Beispielsweise können Sie alle Zeilen in einem Tabellenwertparameter auswählen und in eine Datenbanktabelle einfügen, oder Sie können eine Update-Anweisung erstellen, indem verknüpfen einen Tabellenwertparameter mit der Tabelle, die Sie aktualisieren möchten.  
  
 Die folgende Transact-SQL UPDATE-Anweisung veranschaulicht, wie ein Tabellenwertparameter durch einen Join mit der Categories-Tabelle. Wenn Sie einen Tabellenwertparameter mit einem JOIN in einer FROM-Klausel verwenden, müssen Sie ebenfalls, wie hier gezeigt, in dem der Tabellenwertparameter Alias "EC"versehen ist:  
  
```  
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 Diese Transact-SQL-Beispiel veranschaulicht, wie zum Auswählen von Zeilen aus einem Tabellenwertparameter eine Einfügung in einem einzigen satzbasierten Vorgang ausführen.  
  
```  
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>Einschränkungen von Tabellenwertparametern  
 Es gibt mehrere Einschränkungen bei Tabellenwertparametern:  
  
-   Tabellenwertparameter können nicht auf benutzerdefinierte Funktionen übergeben werden.  
  
-   Tabellenwertparameter können nur zur Unterstützung von UNIQUE- oder PRIMARY KEY-Einschränkungen indiziert werden. SQL Server ist keine Spaltenstatistiken für Tabellenwertparameter verwaltet.  
  
-   Tabellenwertparameter sind in Transact-SQL-Code schreibgeschützt. Sie können nicht die Spaltenwerte in den Zeilen von einem Tabellenwertparameter aktualisieren und Sie können keine Zeilen einfügen oder löschen. Um die Daten ändern, die an eine gespeicherte Prozedur übergeben wird oder eine parametrisierte Anweisung im Tabellenwertparameter, müssen die Daten in eine temporäre Tabelle oder eine Tabellenvariable eingefügt werden.  
  
-   Sie können keine ALTER TABLE-Anweisungen zum Ändern des Entwurfs von Tabellenwertparametern verwenden.
-   Sie können große Objekte in einem Tabellenwertparameter streamen.  
  
## <a name="configuring-a-table-valued-parameter"></a>Konfigurieren einen Tabellenwertparameter  
 Ab Microsoft JDBC Driver 6.0 für SQL Server, werden mit einer parametrisierten Anweisung oder einer parametrisierten gespeicherten Prozedur mit Tabellenwertparametern unterstützt werden. Tabellenwertparameter können aus einem SQLServerDataTable, aus einem ResultSet aufgefüllt oder von einem Benutzer bereitgestellte Implementierung der ISQLServerDataRecord-Schnittstelle. Wenn Sie einen Tabellenwertparameter für eine vorbereitete Abfrage festlegen, müssen Sie einen Namen angeben, der den Namen eines kompatiblen Typs zuvor erstellt haben, auf dem Server übereinstimmen muss.  
  
 Die folgenden zwei Codefragmente veranschaulichen, wie ein Tabellenwertparameter mit Sqlserverpreparedstatement- und ein SQLServerCallableStatement zum Einfügen von Daten konfigurieren. Hier kann SourceTVPObject eine SQLServerDataTable oder ein ResultSet oder ein ISQLServerDataRecord-Objekt. In den Beispielen wird davon ausgegangen, dass eine aktive Verbindungsobjekt aufweist.  
  
```  
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =   
    (SQLServerPreparedStatement) connection.prepareStatement(“INSERT INTO dbo.Categories SELECT * FROM ?”);  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```  
  
```  
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =   
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");       
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Finden Sie im Abschnitt **Table-Valued Parameter-API für JDBC Driver** unten für eine vollständige Liste der APIs für das Festlegen der Tabellenwertparameter verfügbar.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>Übergeben einen Tabellenwertparameter als SQLServerDataTable-Objekt  
 Ab Microsoft JDBC Driver 6.0 für SQL Server, stellt die SQLServerDataTable-Klasse eine in-Memory-Tabelle mit relationalen Daten. In diesem Beispiel wird veranschaulicht, wie ein Tabellenwertparameter von Daten im Arbeitsspeicher, die mit dem SQLServerDataTable-Objekt zu erstellen. Der Code zuerst erstellt ein SQLServerDataTable-Objekt, dessen Schema definiert und wird die Tabelle mit Daten aufgefüllt. Sqlserverpreparedstatement-Klasse, die diese Datentabelle als einen Tabellenwertparameter mit SQL Server übergibt, Code konfiguriert.  
  
```  
// Assumes connection is an active Connection object.  
  
// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();   
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);   
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);   
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");   
sourceDataTable.addRow(2, "CategoryNameValue2");   
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =   
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Finden Sie im Abschnitt **Table-Valued Parameter-API für JDBC Driver** unten für eine vollständige Liste der APIs für das Festlegen der Tabellenwertparameter verfügbar.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>Ein Table-Valued Parameter übergeben wird, als ein ResultSet-Objekt  
 In diesem Beispiel wird veranschaulicht, wie Zeilen mit Daten aus einem ResultSet in einen Tabellenwertparameter zu streamen. Der Code ruft zunächst Daten aus einer Quelltabelle in eine ein SQLServerDataTable-Objekt erstellt, definiert das Schema und die Tabelle mit Daten auffüllt. Sqlserverpreparedstatement-Klasse, die diese Datentabelle als einen Tabellenwertparameter mit SQL Server übergibt, Code konfiguriert.  
  
```  
// Assumes connection is an active Connection object.  
  
// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.   
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  
  
// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =   
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Finden Sie im Abschnitt **Table-Valued Parameter-API für JDBC Driver** unten für eine vollständige Liste der APIs für das Festlegen der Tabellenwertparameter verfügbar.  
  
## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>Übergeben einen Tabellenwertparameter als ISQLServerDataRecord Objekt  
 Ab Microsoft JDBC Driver 6.0 für SQL Server, eine neue Schnittstelle ISQLServerDataRecord steht für das streaming von Daten (je nachdem, wie der Benutzer die Implementierung dafür bietet) mit einem Tabellenwertparameter. Im folgende Beispiel wird veranschaulicht, wie die ISQLServerDataRecord-Schnittstelle implementiert und wie es als ein Tabellenwertparameter übergeben. Aus Gründen der Einfachheit übergibt das folgende Beispiel nur eine Zeile mit hartcodierten Werte an den Tabellenwertparameter an. Im Idealfall würde der Benutzer diese Schnittstelle zum Streamen von Zeilen aus beliebigen Quellen, z. B. von Textdateien implementieren.  
  
```  
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.   
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;       
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }     
}  
  
// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =   
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Finden Sie im Abschnitt **Table-Valued Parameter-API für JDBC Driver** unten für eine vollständige Liste der APIs für das Festlegen der Tabellenwertparameter verfügbar.  
    
## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>Table-Valued Parameter API für den JDBC-Treiber  
 **SQLServerMetaData**  
  
 Diese Klasse stellt die Metadaten für eine Spalte dar. Es wird in der ISQLServerDataRecord-Schnittstelle verwendet, Spaltenmetadaten an die Tabellenwert-Parameter übergeben. Die Methoden in dieser Klasse sind:  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche SQLServerMetaData (Zeichenfolge ColumnName, SqlType Int, Int Genauigkeit, Int Umfang, booleschen UseServerDefault, boolesche IsUniqueKey, SQLServerSortOrder SortOrder, Int SortOrdinal)|Initialisiert eine neue Instanz der SQLServerMetaData angegebene Spaltenname, Sql-Typ, Genauigkeit, Dezimalstellen und Server-Standard. Diese Form des Konstruktors unterstützt Tabellenwertparameter können Sie angeben, ob die Spalte in der Tabellenwertparameter, die Sortierreihenfolge für die Spalte und die Ordnungszahl der Sortierspalte eindeutig ist. <br><br>UseServerDefault - gibt an, wenn diese Spalte den Standardwert für die Server verwenden soll. Standardwert ist "false".<br>IsUniqueKey - gibt an, ob die Spalte in der Tabellenwertparameter eindeutig ist; Standardwert ist "false".<br>SortOrder - gibt die Sortierreihenfolge für eine Spalte an. Standardwert ist SQLServerSortOrder.Unspecified.<br>SortOrdinal - gibt die Ordnungszahl der Sortierspalte. SortOrdinal beginnt mit 0; Standardwert ist-1.|
|Öffentliche SQLServerMetaData (ColumnName String, Int SqlType)|Initialisiert eine neue Instanz der SQLServerMetaData mit dem Spaltennamen und dem Sql-Typ.|  
|Öffentliche SQLServerMetaData (Zeichenfolge ColumnName, SqlType Int, Int mit einfacher Genauigkeit, Int Skalierung)|Initialisiert eine neue Instanz der SQLServerMetaData mithilfe einer der Spaltenname, Sql-Datentyp, Genauigkeit und Skalierung.|  
|Öffentliche SQLServerMetaData (SQLServerMetaData SqlServerMetaData)|Initialisiert einer neuen Instanz der SQLServerMetaData von neuem ein anderes SQLServerMetaData-Objekt.|  
|Öffentliche Zeichenfolge getColumName()|Ruft den Namen der Spalte ab.|  
|öffentliches Int getSqlType()|Ruft die Java-Sql-Typ ab.|  
|öffentliches Int getPrecision()|Ruft die Genauigkeit des Datentyps der Spalte übergeben.|  
|öffentliches Int getScale()|Ruft die Dezimalstellen des Typs der Spalte übergeben.|  
|Öffentliche SQLServerSortOrder getSortOrder()|Ruft die Sortierreihenfolge ab.|
|öffentliches Int getSortOrdinal()|Ruft die Ordinalzahl der Sortierung ab.|
|Öffentlicher boolescher isUniqueKey()|Gibt zurück, ob die Spalte eindeutig ist.|
|Öffentlicher boolescher useServerDefault()|Gibt zurück, ob die Spalte auf wird der Standardwert für den Server verwendet.|
  
 **SQLServerSortOrder**
 
 Eine Enumeration, die die Sortierreihenfolge festlegt. Mögliche Werte sind aufsteigend, absteigend und nicht angegeben. 
  
 **SQLServerDataTable**  
  
 Diese Klasse stellt eine in-Memory-Datentabelle mit Tabellenwertparametern verwendet werden soll. Die Methoden in dieser Klasse sind:  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche SQLServerDataTable()|Initialisiert eine neue Instanz der SQLServerDataTable an.|  
|Öffentliche Iterator < Eintrag\<ganze Zahl, Objekt [] >> getIterator()|Ruft einen Iterator für die Zeilen der Datentabelle ab.|  
|Öffentliche void AddColumnMetadata (ColumnName String, Int SqlType)|Fügt Metadaten für die angegebene Spalte.|  
|Öffentliche void AddColumnMetadata (SQLServerDataColumn-Spalte)|Fügt Metadaten für die angegebene Spalte.|  
|Öffentliche void AddRow (Objektwerten...)|Fügt eine Zeile mit Daten der Datentabelle.|  
|Öffentliche Zuordnung\<Integer, SQLServerDataColumn > getColumnMetadata()|Ruft die Spaltenmetadaten dieser Tabelle Daten ab.|
|Öffentliche void clear() |Löscht diese Datentabelle. |  
  
 **SQLServerDataColumn**  
  
 Diese Klasse stellt eine Spalte mit der in-Memory-Datentabelle durch SQLServerDataTable dargestellt. Die Methoden in dieser Klasse sind:  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche SQLServerDataColumn (ColumnName String, Int SqlType)|Initialisiert eine neue Instanz der SQLServerDataColumn mit dem Spaltennamen und Typ an.|  
|Öffentliche Zeichenfolge getColumnName()|Ruft den Namen der Spalte ab.|  
|öffentliches Int getColumnType()|Ruft den Spaltentyp ab.|  
  
 **ISQLServerDataRecord**  
  
 Diese Klasse stellt eine Schnittstelle, die Benutzer zum Streamen von Daten auf einen Tabellenwertparameter implementieren können. Die Methoden in dieser Schnittstelle sind:  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche SQLServerMetaData GetColumnMetaData (Int-Spalte);|Ruft die Spaltenmetadaten des angegebenen Spaltenindexes ab.|  
|öffentliches Int getColumnCount();|Ruft die Gesamtzahl der Spalten ab.|  
|Öffentliche getRowData() für Objekt [];|Ruft die Daten für die aktuelle Zeile als ein Array von Objekten ab.|  
|Öffentlicher boolescher::Next();|Wechselt zur nächsten Zeile. Gibt "true" zurück, wenn die Verschiebung erfolgreich ist, und andernfalls "false" über eine nächste Zeile besteht.|  
  
 **Sqlserverpreparedstatement-Klasse**  
  
 Die folgenden Methoden wurden für diese Klasse zur Übergabe von Tabellenwertparameter-Unterstützung hinzugefügt.  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche endgültigen "void" SetStructured (ParameterIndex Int, String TvpName SQLServerDataTable TvpDataTbale)|Füllt einen Tabellenwert-Parameter mit einer Datentabelle. ParameterIndex ist des parameterindexes und TvpDataTable ist die Tabelle Quelldatenobjekt TvpName ist der Name des Tabellenwertparameter-Parameter.|  
|Öffentliche endgültigen "void" SetStructured (ParameterIndex Int, String TvpName ResultSet TvpResultSet)|Füllt einen Tabellenwert-Parameter mit einem ResultSet, das aus einem anderen Tabelle abgerufen. ParameterIndex ist der Parameterindex, TvpName ist der Name des Parameters mit Tabellenrückgabe und TvpResultSet ist das Ergebnis Set-Quellobjekt.|  
|Öffentliche endgültigen "void" SetStructured (ParameterIndex Int, String TvpName ISQLServerDataRecord TvpDataRecord)|Füllt einen Tabellenwert-Parameter mit einem ISQLServerDataRecord-Objekt. ISQLServerDataRecord dient zum Streamen von Daten und der Benutzer entscheidet, zu dessen Verwendung. ParameterIndex ist der Parameterindex, TvpName ist der Name des Parameters mit Tabellenrückgabe und TvpDataRecord ist ein ISQLServerDataRecord-Objekt.|  
  
 **SQLServerCallableStatement**  
  
 Die folgenden Methoden wurden für diese Klasse zur Übergabe von Tabellenwertparameter-Unterstützung hinzugefügt.  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche endgültigen "void" SetStructured (ParatemeterName Zeichenfolge, Zeichenfolge TvpName, SQLServerDataTable TvpDataTable)|Füllt einen Tabellenwert-Parameter, die an eine gespeicherte Prozedur mit einer Datentabelle übergeben. ParatemeterName ist der Name des Parameters, TvpName ist der Name des Typs TVP und TvpDataTable wird das Datenobjekt für die Tabelle.|  
|Öffentliche endgültigen "void" SetStructured (ParatemeterName Zeichenfolge, Zeichenfolge TvpName ResultSet TvpResultSet)|Füllt einen Tabellenwert-Parameter an eine gespeicherte Prozedur übergeben werden, mit der ein ResultSet aus einer anderen Tabelle abgerufen. ParatemeterName ist der Name des Parameters, TvpName ist der Name des Typs TVP und TvpResultSet ist das Ergebnis Set-Quellobjekt.|  
|Öffentliche endgültigen "void" SetStructured (ParatemeterName Zeichenfolge, Zeichenfolge TvpName, ISQLServerDataRecord TvpDataRecord)|Füllt einen Tabellenwert-Parameter, die an eine gespeicherte Prozedur mit einem ISQLServerDataRecord-Objekt übergeben. ISQLServerDataRecord dient zum Streamen von Daten und der Benutzer entscheidet, zu dessen Verwendung. ParatemeterName ist der Name des Parameters, TvpName ist der Name des Typs TVP und TvpDataRecord ist ein ISQLServerDataRecord-Objekt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

