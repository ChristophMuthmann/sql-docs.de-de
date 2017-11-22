---
title: Verwenden von Massenkopieren mit dem JDBC-Treiber | Microsoft Docs
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
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f4a714ce9ea2a076b922de3fc66851fa58110eb4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>Verwenden von Massenkopieren mit dem JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft SQL Server enthält ein beliebtes Befehlszeilentools-Hilfsprogramm, die mit dem Namen **Bcp** für schnellen Massenkopieren großer Dateiumfänge in Tabellen oder Sichten in SQL Server-Datenbanken. Der Klasse "sqlserverbulkcopy" ermöglicht Ihnen das Schreiben von codelösungen in Java, die ähnliche Funktionalität bereitzustellen. Es gibt andere Möglichkeiten zum Laden von Daten in einer SQL Server-Tabelle (z. B. INSERT-Anweisungen) aber bietet "sqlserverbulkcopy" einen deutlichen Leistungsvorteil über diese.  
  
 Die Klasse „SQLServerBulkCopy“ kann nur verwendet werden, um Daten in SQL Server-Tabellen zu schreiben. Die Datenquelle ist aber nicht auf SQL Server beschränkt; jede beliebige Datenquelle kann verwendet werden, sofern die Daten mit einer Implementierung von „ResultSet“, „RowSet“ oder „ISQLServerBulkRecord“ gelesen werden können.  
  
 Mithilfe der SQLServerBulkCopy-Klasse können Sie folgende Vorgänge ausführen:  
  
-   Einen einzelnen Massenkopiervorgang  
  
-   Mehrere Massenkopiervorgänge  
  
-   Einen Massenkopiervorgang mit einer Transaktion  
  
> [!NOTE]  
>  Wenn Sie den Microsoft JDBC Driver 4.1 für SQL Server (der die SQLServerBulkCopy-Klasse nicht unterstützt) oder eine frühere Version verwenden, können Sie stattdessen die SQL Server Transact-SQL-Anweisung „BULK INSERT“ ausführen.  
  
## <a name="bulk-copy-example-setup"></a>Einrichten des Massenkopierbeispiels  
 Die Klasse „SQLServerBulkCopy“ kann nur verwendet werden, um Daten in SQL Server-Tabellen zu schreiben. Die in diesem Thema gezeigten Codebeispiele verwenden die SQL Server-Beispieldatenbank „AdventureWorks“. Um eine Änderung der vorhandenen Codebeispiele zu vermeiden, schreiben die Codebeispiele Daten in Tabellen, die zuvor von Ihnen erstellt werden.  
  
 Die Tabellen „BulkCopyDemoMatchingColumns“ und „BulkCopyDemoDifferentColumns“ basieren beide auf der Tabelle „AdventureWorks Production.Products“. In Codebeispielen, die diese Tabellen verwenden, werden Daten aus der Tabelle „Production.Products“ einer dieser Beispieltabellen hinzugefügt. Die Tabelle „BulkCopyDemoDifferentColumns“ wird verwendet, um im Beispiel zu veranschaulichen, wie Spalten aus den Quelldaten der Zieltabelle zugeordnet werden; für die meisten anderen Beispiele wird „BulkCopyDemoMatchingColumns“ verwendet.  
  
 Einige der Codebeispiele zeigen, wie eine Klasse „SQLServerBulkCopy“ zum Schreiben in mehrere Tabellen verwendet werden kann. Für diese Beispiele werden die Tabellen „BulkCopyDemoOrderHeader“ und „BulkCopyDemoOrderDetail“ als Zieltabellen verwendet. Diese Tabellen basieren auf den Tabellen „Sales.SalesOrderHeader“ und „Sales.SalesOrderDetail“ in „AdventureWorks“.  
  
> [!NOTE]  
>  Die Codebeispiele zu „SQLServerBulkCopy“ werden nur zur Verfügung gestellt, um die Syntax für die Verwendung von „SQLServerBulkCopy“ zu veranschaulichen. Wenn sich die Quell- und Zieltabellen in der gleichen SQL Server-Instanz befinden, ist die Verwendung einer Transact-SQL-Anweisung „INSERT … SELECT“ zum Kopieren der Daten einfacher und schneller.  
  
###  <a name="BKMK_TableSetup"></a>Tabelleneinrichtung  
 Zum Erstellen der Tabellen, die für die ordnungsgemäße Ausführung der Codebeispiele erforderlich sind, müssen Sie die folgenden Transact-SQL-Anweisungen in einer SQL Server-Datenbank ausführen.  
  
```  
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')   
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED   
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')   
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED   
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')   
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED   
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')   
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED   
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
```  
  
## <a name="single-bulk-copy-operations"></a>Einzelne Massenkopiervorgänge  
 Die einfachste Herangehensweise an einen SQL Server-Massenkopiervorgang ist das Durchführen eines einzelnen Vorgangs für eine Datenbank. Standardmäßig wird ein Massenkopiervorgang als isolierter Vorgang ausgeführt: Der Kopiervorgang erfolgt in nicht transaktionaler Weise, ohne Möglichkeit zum Rollback.  
  
> [!NOTE]  
>  Wenn Sie für den Massenkopiervorgang beim Auftreten eines Fehlers einen teilweisen oder vollständigen Rollback ausführen müssen, können Sie entweder eine verwaltete SQLServerBulkCopy-Transaktion verwenden oder den Massenkopiervorgang innerhalb einer vorhandenen Transaktion ausführen.  
>   
>  Weitere Informationen finden Sie unter [Transaktion und der Massenimport Kopiervorgänge](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TransactionBulk)  
  
 Dies sind die allgemeinen Schritte zum Durchführen eines Massenkopiervorgangs:  
  
1.  Herstellen einer Verbindung mit dem Quellserver und Abrufen der zu kopierenden Daten. Daten können auch aus anderen Quellen stammen, sofern sie von einem ResultSet-Objekt oder einer ISQLServerBulkRecord-Implementierung abgerufen werden können.  
  
2.  Herstellen einer Verbindung mit dem Zielserver (es sei denn, Sie **"sqlserverbulkcopy"** zum Herstellen einer Verbindung für Sie).  
  
3.  Erstellen ein SQLServerBulkCopy-Objekts festlegen aller erforderlichen Eigenschaften über **SetBulkCopyOptions**.  
  
4.  Rufen Sie die **SetDestinationTableName** Vorgang zum Einfügen von Methode, um die Zieltabelle für den Masseneinfügevorgang anzugeben.  
  
5.  Rufen Sie eine von der **WriteToServer** Methoden.  
  
6.  Optional Aktualisieren der Eigenschaften über **SetBulkCopyOptions** , und rufen Sie **WriteToServer** erneut nach Bedarf.  
  
7.  Rufen Sie **schließen**, oder umschließen der Massenkopiervorgänge innerhalb einer Try-with-Resources-Anweisung.  
  
> [!CAUTION]  
>  Wir empfehlen die Verwendung gleicher Datentypen für Quell- und Zielspalten. Wenn die Datentypen nicht übereinstimmen, versucht „SQLServerBulkCopy“, jeden Quellwert in den Zieldatentyp zu konvertieren. Konvertierungen wirken sich negativ auf die Leistung aus und können außerdem zu unerwarteten Fehlern führen. Beispielsweise kann ein Datentyp „double“ in den meisten Fällen in den Datentyp „decimal“ konvertiert werden, aber nicht immer.  
  
### <a name="example"></a>Beispiel  
 Die folgende Anwendung zeigt das Laden von Daten mithilfe der Klasse „SQLServerBulkCopy“. In diesem Beispiel wird ein „ResultSet“ verwendet, um Daten aus der Tabelle „Production.Product“ in der SQL Server AdventureWorks-Datenbank in eine ähnliche Tabelle in der gleichen Datenbank zu kopieren.  
  
> [!IMPORTANT]  
>  Dieses Beispiel wird nicht ausgeführt, es sei denn, Sie die Arbeitstabellen erstellt haben, wie in beschrieben [tabelleneinrichtung](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Dieser Code wird nur bereitgestellt, um die Syntax für die Verwendung von „SQLServerBulkCopy“ zu demonstrieren. Wenn sich die Quell- und Zieltabellen in der gleichen SQL Server-Instanz befinden, ist die Verwendung einer Transact-SQL-Anweisung „INSERT … SELECT“ zum Kopieren der Daten einfacher und schneller.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    // Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
                        // Open the destination connection. In the real world you would    
                        // not use SQLServerBulkCopy to move data from one table to the other    
                        // in the same database. This is for demonstration purposes only.   
                        try (Connection destinationConnection =   
                                DriverManager.getConnection(connectionString))  
                        {  
                            // Set up the bulk copy object.    
                            // Note that the column positions in the source   
                            // table match the column positions in    
                            // the destination table so there is no need to   
                            // map columns.   
                            try (SQLServerBulkCopy bulkCopy =  
                                       new SQLServerBulkCopy(destinationConnection))  
                            {  
                                bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                                try  
                                {  
                                    // Write from the source to the destination.  
                                    bulkCopy.writeToServer(rsSourceData);  
                                }  
                                catch (Exception e)  
                                {  
                                    // Handle any errors that may have occurred.  
                                    e.printStackTrace();  
                                }  
                            }  
  
                            // Perform a final count on the destination    
                            // table to see how many rows were added.  
                            try (ResultSet rsRowCount = stmt.executeQuery(  
                                    "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                            {  
                                rsRowCount.next();  
                                long countEnd = rsRowCount.getInt(1);  
                                System.out.println("Ending row count = " + countEnd);  
                                System.out.println((countEnd - countStart) + " rows were added.");  
                            }  
                        }  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
           "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>Ausführen eines Massenkopiervorgangs mithilfe von Transact-SQL  
 Das folgende Beispiel zeigt die Verwendung der Methode „executeUpdate“ zum Ausführen der Anweisung „BULK INSERT“.  
  
> [!NOTE]  
>  Der Dateipfad für die Datenquelle ist relativ zum Server. Der Serverprozess muss Zugriff auf diesen Pfad besitzen, damit der Massenkopiervorgang erfolgreich ausgeführt werden kann.  
  
```  
try (Connection con = DriverManager.getConnection(connectionString))  
{  
    try (Statement stmt = con.createStatement())  
    {  
        // Perform the BULK INSERT  
        stmt.executeUpdate(  
                "BULK INSERT Northwind.dbo.[Order Details] " +  
                        "FROM 'f:\\mydata\\data.tbl' " +  
                        "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");  
    }  
}  
```  
  
## <a name="multiple-bulk-copy-operations"></a>Mehrere Massenkopiervorgänge  
 Mithilfe einer einzelnen Instanz einer SQLServerBulkCopy-Klasse können Sie mehrere Massenkopiervorgänge ausführen. Wenn sich die Parameter für den Vorgang zwischen den Ausführungen ändern (z. B. der Name der Zieltabelle), müssen Sie sie vor allen nachfolgenden Aufrufen einer der writeToServer-Methoden ändern, wie im folgenden Beispiel gezeigt. Sofern sie nicht explizit geändert werden, bleiben alle Eigenschaftswerte die gleichen wie beim letzten Massenkopiervorgang für eine bestimmte Instanz.  
  
> [!NOTE]  
>  Das Ausführen mehrerer Massenkopiervorgänge mithilfe der gleichen Instanz von SQLServerBulkCopy ist normalerweise effizienter als die Verwendung einer separaten Instanz für jeden Vorgang.  
  
 Wenn Sie mehrere Massenkopiervorgänge mithilfe des gleichen SQLServerBulkCopy-Objekts ausführen, bestehen normalerweise keine Einschränkungen hinsichtlich der Gleichheit oder Verschiedenheit der Quell- und Zielinformationen für die einzelnen Vorgänge. Sie müssen jedoch sicherstellen, dass die Informationen zur Spaltenzuordnung bei jedem Schreibvorgang auf dem Server ordnungsgemäß festgelegt sind.  
  
> [!IMPORTANT]  
>  Dieses Beispiel wird nicht ausgeführt, es sei denn, Sie die Arbeitstabellen erstellt haben, wie in beschrieben [tabelleneinrichtung](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Dieser Code wird nur bereitgestellt, um die Syntax für die Verwendung von „SQLServerBulkCopy“ zu demonstrieren. Wenn sich die Quell- und Zieltabellen in der gleichen SQL Server-Instanz befinden, ist die Verwendung einer Transact-SQL-Anweisung „INSERT … SELECT“ zum Kopieren der Daten einfacher und schneller.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection1 = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection1.createStatement())  
                {  
  
                    // Empty the destination tables.   
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoOrderHeader;");  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoOrderDetail;");  
  
                    // Perform an initial count on the destination   
                    //  table with matching columns.  
                    long countStartHeader = 0;  
                    try (ResultSet rsRowCountHeader = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderHeader;"))  
                    {  
                        rsRowCountHeader.next();  
                        countStartHeader = rsRowCountHeader.getInt(1);  
                        System.out.println("Starting row count for Header table = " + countStartHeader);  
                    }  
  
                    // Perform an initial count on the destination   
                    // table with different column positions.  
                    long countStartDetail = 0;  
                    try (ResultSet rsRowCountDetail = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderDetail;"))  
                    {  
                        rsRowCountDetail.next();  
                        countStartDetail = rsRowCountDetail.getInt(1);  
                        System.out.println("Starting row count for Detail table = " + countStartDetail);  
                    }  
  
                    // Get data from the source table as a ResultSet.   
                    // The Sales.SalesOrderHeader and Sales.SalesOrderDetail   
                    // tables are quite large and could easily cause a timeout   
                    // if all data from the tables is added to the destination.    
                    // To keep the example simple and quick, a parameter is     
                    // used to select only orders for a particular account    
                    // as the source for the bulk insert.  
                    try (PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(  
                            "SELECT [SalesOrderID], [OrderDate], " +  
                            "[AccountNumber] FROM [Sales].[SalesOrderHeader] " +  
                            "WHERE [AccountNumber] = ?;"))  
                    {  
                        preparedStmt1.setString(1, "10-4020-000034");  
  
                        try (ResultSet rsHeader = preparedStmt1.executeQuery())  
                        {  
                            // Get the Detail data in a separate connection.   
                            try (Connection sourceConnection2 = DriverManager.getConnection(connectionString))  
                            {  
                                try (PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(  
                                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], " +  
                                                "[SalesOrderDetailID], [OrderQty], [ProductID], " +  
                                                "[UnitPrice] FROM [Sales].[SalesOrderDetail] " +  
                                                "INNER JOIN [Sales].[SalesOrderHeader] " +  
                                                "ON [Sales].[SalesOrderDetail].[SalesOrderID] " +  
                                                "= [Sales].[SalesOrderHeader].[SalesOrderID] " +  
                                                "WHERE [AccountNumber] = ?;"))  
                                {  
                                    preparedStmt2.setString(1, "10-4020-000034");  
  
                                    try (ResultSet rsDetail = preparedStmt2.executeQuery())  
                                    {  
                                        // Create the SQLServerBulkCopySQLServerBulkCopy object.    
                                        try (SQLServerBulkCopy bulkCopy =  
                                                   new SQLServerBulkCopy(connectionString))  
                                        {  
                                            bulkCopy.setBulkCopyOptions(copyOptions);  
                                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoOrderHeader");  
  
                                            // Guarantee that columns are mapped correctly by   
                                            // defining the column mappings for the order.  
                                            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");  
                                            bulkCopy.addColumnMapping("OrderDate", "OrderDate");  
                                            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");  
  
                                            // Write rsHeader to the destination.   
                                            try  
                                            {  
                                                bulkCopy.writeToServer(rsHeader);  
                                            }  
                                            catch (Exception e)  
                                            {  
                                                // Handle any errors that may have occurred.  
                                                e.printStackTrace();  
                                            }  
  
                                            // Set up the order details destination.   
                                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoOrderDetail");  
  
                                            // Clear the existing column mappings  
                                            bulkCopy.clearColumnMappings();  
  
                                            // Add order detail column mappings.  
                                            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");  
                                            bulkCopy.addColumnMapping(  
                                                    "SalesOrderDetailID",   
                                                    "SalesOrderDetailID");  
                                            bulkCopy.addColumnMapping("OrderQty", "OrderQty");  
                                            bulkCopy.addColumnMapping("ProductID", "ProductID");  
                                            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");  
  
                                            // Write rsDetail to the destination.   
                                            try  
                                            {  
                                                bulkCopy.writeToServer(rsDetail);  
                                            }  
                                            catch (Exception e)  
                                            {  
                                                // Handle any errors that may have occurred.  
                                                e.printStackTrace();  
                                            }  
                                        }  
                                    }  
                                }  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination   
                    // tables to see how many rows were added.  
                    try (ResultSet rsRowCountHeader = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderHeader;"))  
                    {  
                        rsRowCountHeader.next();  
                        long countEndHeader =  rsRowCountHeader.getInt(1);  
                        System.out.println(  
                                (countEndHeader - countStartHeader) +   
                                " rows were added to the Header table.");  
                    }  
  
                    try (ResultSet rsRowCountDetail = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderDetail;"))  
                    {  
                        rsRowCountDetail.next();  
                        long countEndDetail = rsRowCountDetail.getInt(1);  
                        System.out.println(  
                                (countEndDetail - countStartDetail) +   
                                " rows were added to the Detail table.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
##  <a name="BKMK_TransactionBulk"></a>Transaktionen und Massenkopiervorgänge  
 Massenkopiervorgänge können als isolierte Vorgänge oder im Rahmen einer aus mehreren Schritten bestehenden Transaktion ausgeführt werden. Diese zweite Option ermöglicht Ihnen das Ausführen mehrerer Massenkopiervorgänge innerhalb der gleichen Transaktion sowie die Durchführung weiterer Datenbankvorgänge (wie etwa Einfüge-, Aktualisierungs- und Löschvorgänge), während die Möglichkeit zum Commit oder Rollback der gesamten Transaktion erhalten bleibt.  
  
 Standardmäßig wird ein Massenkopiervorgang als isolierter Vorgang ausgeführt. Der Massenkopiervorgang erfolgt nicht transaktional, ohne Möglichkeit zum Rollback. Wenn Sie für den Massenkopiervorgang beim Auftreten eines Fehlers einen teilweisen oder vollständigen Rollback ausführen müssen, können Sie eine verwaltete SQLServerBulkCopy-Transaktion verwenden oder den Massenkopiervorgang innerhalb einer vorhandenen Transaktion ausführen.  
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>Ausführen eines nicht transaktionalen Massenkopiervorgangs  
 Die folgende Anwendung zeigt, was geschieht, wenn bei einem nicht transaktionalen Massenkopiervorgang nach teilweiser Ausführung ein Fehler auftritt.  
  
 Im Beispiel enthalten Quell- und Zieltabelle jeweils eine Identitätsspalte mit Namen **"ProductID"**. Der Code bereitet zunächst die Zieltabelle durch das Löschen aller Zeilen, und klicken Sie dann eine einzelne Zeile einfügt, deren **"ProductID"** ist bekannt, in der Quelltabelle vorhanden sein. Standardmäßig wird für die Spalte „Identity“ in der Zieltabelle für jede hinzugefügte Zeile ein neuer Wert generiert. In diesem Beispiel wird beim Öffnen der Verbindung eine Option festgelegt, die den Massenladevorgang zwingt, stattdessen die Identity-Werte aus der Quelltabelle zu verwenden.  
  
 Der Massenkopiervorgang wird ausgeführt, mit der **BatchSize** -Eigenschaft auf 10 festgelegt. Wenn der Vorgang auf die ungültige Zeile trifft, wird eine Ausnahme ausgelöst. In diesem ersten Beispiel ist der Massenkopiervorgang nicht transaktional. Für alle bis zum Auftreten des Fehlers kopierten Batches wird ein Commit ausgeführt; für den Batch, der den doppelten Schlüssel enthält, wird ein Rollback ausgeführt, und der Massenkopiervorgang wird vor dem Verarbeiten weiterer Batches angehalten.  
  
> [!NOTE]  
>  Dieses Beispiel wird nicht ausgeführt, es sei denn, Sie die Arbeitstabellen erstellt haben, wie in beschrieben [tabelleneinrichtung](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Dieser Code wird nur bereitgestellt, um die Syntax für die Verwendung von „SQLServerBulkCopy“ zu demonstrieren. Wenn sich die Quell- und Zieltabellen in der gleichen SQL Server-Instanz befinden, ist die Verwendung einer Transact-SQL-Anweisung „INSERT … SELECT“ zum Kopieren der Daten einfacher und schneller.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.  
                        SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                        copyOptions.setKeepIdentity(true);  
                        copyOptions.setBatchSize(10);  
  
                        try (SQLServerBulkCopy bulkCopy =   
                                new SQLServerBulkCopy(connectionString))  
                        {  
                            bulkCopy.setBulkCopyOptions(copyOptions);  
                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                            // Write from the source to the destination.   
                            // This should fail with a duplicate key error   
                            // after some of the batches have been copied.   
                            try  
                            {  
                                bulkCopy.writeToServer(rsSourceData);  
                            }  
                            catch (Exception e)  
                            {  
                                // Handle any errors that may have occurred.  
                                e.printStackTrace();  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection String.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
              "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="performing-a-dedicated-build-copy-operation-in-a-transaction"></a>Ausführen eines dedizierten Massenkopiervorgangs in einer Transaktion  
 Standardmäßig stellt ein Massenkopiervorgang seine eigene Transaktion dar. Wenn Sie einen dedizierten Massenkopiervorgang ausführen möchten, erstellen Sie eine neue Instanz von „SQLServerBulkCopy“ mit einer Verbindungszeichenfolge. In diesem Szenario erstellt der Massenkopiervorgang die Transaktion, für die er dann einen Commit oder einen Rollback ausführt. Sie können explizit angeben der **UseInternalTransaction** option **SQLServerBulkCopyOptions** so explizit einen Massenkopiervorgang seine eigene Transaktion, wodurch jeder Batch des Masseneinfügevorgangs ausgeführt wird Kopieren Sie Vorgang innerhalb einer separaten Transaktion ausgeführt.  
  
> [!NOTE]  
>  Da verschiedene Batches in verschiedenen Transaktionen ausgeführt werden, wird für alle Zeilen im aktuellen Batch beim Auftreten eines Fehlers ein Rollback ausgeführt, die Zeilen aus vorhergehenden Batches verbleiben jedoch in der Datenbank.  
  
 Die folgende Anwendung ähnelt dem vorhergehenden Beispiel, mit einer Ausnahme: In diesem Beispiel verwaltet der Massenkopiervorgang seine eigenen Transaktionen. Für alle bis zum Auftreten des Fehlers kopierten Batches wird ein Commit ausgeführt; für den Batch, der den doppelten Schlüssel enthält, wird ein Rollback ausgeführt, und der Massenkopiervorgang wird vor dem Verarbeiten weiterer Batches angehalten.  
  
> [!NOTE]  
>  Dieses Beispiel wird nicht ausgeführt, es sei denn, Sie die Arbeitstabellen erstellt haben, wie in beschrieben [tabelleneinrichtung](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Dieser Code wird nur bereitgestellt, um die Syntax für die Verwendung von „SQLServerBulkCopy“ zu demonstrieren. Wenn sich die Quell- und Zieltabellen in der gleichen SQL Server-Instanz befinden, ist die Verwendung einer Transact-SQL-Anweisung „INSERT … SELECT“ zum Kopieren der Daten einfacher und schneller.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object.  
                        // Note that when specifying the UseInternalTransaction   
                        // option, you cannot also use an external transaction.   
                        // Therefore, you must use the SQLServerBulkCopy construct that   
                        // requires a string for the connection, rather than an   
                        // existing Connection object.   
                        SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                        copyOptions.setKeepIdentity(true);  
                        copyOptions.setBatchSize(10);  
                        copyOptions.setUseInternalTransaction(true);  
  
                        try (SQLServerBulkCopy bulkCopy =   
                                new SQLServerBulkCopy(connectionString))  
                        {  
                            bulkCopy.setBulkCopyOptions(copyOptions);  
                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                            // Write from the source to the destination.   
                            // This should fail with a duplicate key error   
                            // after some of the batches have been copied.   
                            try  
                            {  
                                bulkCopy.writeToServer(rsSourceData);  
                            }  
                            catch (Exception e)  
                            {  
                                // Handle any errors that may have occurred.  
                                e.printStackTrace();  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="using-existing-transactions"></a>Verwenden vorhandener Transaktionen  
 Sie können ein Verbindungsobjekt, für das Transaktionen aktiviert sind, als Parameter in einem SQLServerBulkCopy-Konstruktor übergeben. In dieser Situation wird der Massenkopiervorgang in einer vorhandenen Transaktion ausgeführt, und es tritt keine Änderung am Transaktionsstatus ein (d.h. für sie wird weder ein Commit noch ein Abbruch ausgeführt). Dies macht es möglich, dass Anwendungen den Massenkopiervorgang zusammen mit anderen Datenbankvorgängen in einer Transaktion einschließen. Ob Sie einen Rollback des gesamten Massenkopiervorgangs durchführen müssen, weil ein Fehler auftritt, oder ob die Massenkopie im Rahmen eines größeren Prozesses ausgeführt werden soll, für den ein Rollback durchgeführt werden kann, Sie können den Rollback für das Verbindungsobjekt zu jedem beliebigen Zeitpunkt nach dem Massenkopiervorgang ausführen.  
  
 Die folgende Anwendung ähnelt dem ersten (nicht transaktionalen) Beispiel, mit einer Ausnahme: in diesem Beispiel ist der Massenkopiervorgang in einer größeren, externen Transaktion enthalten. Wenn der Fehler aufgrund des Primärschlüsselverstoßes auftritt, wird ein Rollback der gesamten Transaktion ausgeführt, und der Zieltabelle werden keine Zeilen hinzugefügt.  
  
> [!NOTE]  
>  Dieses Beispiel wird nicht ausgeführt, es sei denn, Sie die Arbeitstabellen erstellt haben, wie in beschrieben [tabelleneinrichtung](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Dieser Code wird nur bereitgestellt, um die Syntax für die Verwendung von „SQLServerBulkCopy“ zu demonstrieren. Wenn sich die Quell- und Zieltabellen in der gleichen SQL Server-Instanz befinden, ist die Verwendung einer Transact-SQL-Anweisung „INSERT … SELECT“ zum Kopieren der Daten einfacher und schneller.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object inside the transaction.  
                        try (Connection destinationConnection =   
                                DriverManager.getConnection(connectionString))  
                        {  
                            destinationConnection.setAutoCommit(false);  
  
                            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                            copyOptions.setKeepIdentity(true);  
                            copyOptions.setBatchSize(10);  
  
                            try (SQLServerBulkCopy bulkCopy =   
                                    new SQLServerBulkCopy(destinationConnection))  
                            {  
                                bulkCopy.setBulkCopyOptions(copyOptions);  
                                bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                                // Write from the source to the destination.   
                                // This should fail with a duplicate key error.   
                                try  
                                {  
                                    bulkCopy.writeToServer(rsSourceData);  
                                    destinationConnection.commit();  
                                }  
                                catch (Exception e)  
                                {  
                                    // Handle any errors that may have occurred.  
                                    e.printStackTrace();  
                                    destinationConnection.rollback();  
                                }  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
### <a name="bulk-copy-from-a-csv-file"></a>Massenkopieren aus einer CSV-Datei  
 Die folgende Anwendung zeigt das Laden von Daten mithilfe der Klasse „SQLServerBulkCopy“. In diesem Beispiel wird eine CSV-Datei verwendet, um aus der Tabelle „Production.Product“ in der SQL Server AdventureWorks-Datenbank exportierte Daten in eine ähnliche Tabelle in der gleichen Datenbank zu kopieren.  
  
> [!IMPORTANT]  
>  Dieses Beispiel wird nicht ausgeführt, es sei denn, Sie die Arbeitstabellen erstellt haben, wie in beschrieben [tabelleneinrichtung](../../ssms/download-sql-server-management-studio-ssms.md) Bezugsquelle.  
  
1.  Open **SQL Server Management Studio** und Herstellen einer Verbindung mit SQL Server mit der AdventureWorks-Datenbank.  
  
2.  Erweitern Sie die Datenbanken mit der rechten Maustaste auf die AdventureWorks-Datenbank, wählen Sie **Aufgaben** und **Exportieren von Daten**...  
  
3.  Wählen Sie für die Datenquelle die **Datenquelle** ermöglicht Ihnen das Herstellen einer Verbindung mit SQL Server (z. B. SQL Server Native Client 11.0), überprüfen Sie die Konfiguration und anschließend **weiter**  
  
4.  Wählen Sie für das Ziel der **Flat File Destination** , und geben Sie einen **Dateiname** mit einem Zielspeicherort wie C:\Test\TestBulkCSVExample.csv. Überprüfen Sie, ob die **Format** begrenzt ist, die **Textqualifizierer** ist "none", und aktivieren Sie **Spaltennamen in der ersten Datenzeile**, und wählen Sie dann **weiter**  
  
5.  Wählen Sie **Abfrage zum Angeben der zu übertragenden Daten schreiben** und **Weiter**.  Geben Sie Ihre **SQL-Anweisung** wählen Sie "ProductID", Name, ProductNumber FROM Production.Product und **weiter**  
  
6.  Überprüfen Sie die Konfiguration: Sie können das Zeilentrennzeichen als {CR}{LF} und das Spaltentrennzeichen als Komma {,} belassen.  Wählen Sie **Zuordnungen bearbeiten**... und überprüfen Sie, ob die Daten **Typ** für jede Spalte (z. B. Integer für ProductID und Unicode-Zeichenfolge für die anderen) richtig ist.  
  
7.  Fahren Sie mit **Fertig stellen** und führen Sie den Exportvorgang.  
  
```  
  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        SQLServerBulkCSVFileRecord fileRecord = null;  
        try  
        {              
            // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.  
            // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.  
            fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);      
  
            // Set the metadata for each column to be copied.  
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);  
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);  
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);  
  
            // Open a destinationConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection destinationConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = destinationConnection.createStatement())  
                {  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    // Set up the bulk copy object.    
                    // Note that the column positions in the source   
                    // data reader match the column positions in    
                    // the destination table so there is no need to   
                    // map columns.   
                    try (SQLServerBulkCopy bulkCopy =  
                               new SQLServerBulkCopy(destinationConnection))  
                    {  
                        bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                        try  
                        {  
                            // Write from the source to the destination.  
                            bulkCopy.writeToServer(fileRecord);  
                        }  
                        catch (Exception e)  
                        {  
                            // Handle any errors that may have occurred.  
                            e.printStackTrace();  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
        finally  
        {  
            if (fileRecord != null) try { fileRecord.close(); } catch(Exception e) {}  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
           "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
### <a name="bulk-copy-with-always-encrypted-columns"></a>Massenkopieren mit Always Encrypted-Spalten  
 Ab Microsoft JDBC Driver 6.0 für SQL Server, wird das Massenkopieren mit Always Encrypted-Spalten unterstützt.  
  
 Abhängig von der Bulk Kopieroptionen zu erhalten und die Verschlüsselung kann Typ der Quelle und Ziel Tabellen, die der JDBC-Treiber transparent entschlüsselt und Verschlüsseln der Daten, oder er kann, die verschlüsselten Daten gesendet werden. Z. B. entschlüsselt beim Massenkopieren von Daten aus einer verschlüsselten Spalte auf eine nicht verschlüsselte Spalte, der Treiber transparent Daten vor dem Senden an SQL Server. Auf ähnliche Weise verschlüsselt beim Massenkopieren von Daten aus einer nicht verschlüsselte Spalte (oder aus einer CSV-Datei), um eine verschlüsselte Spalte, der Treiber transparent Daten vor dem Senden an SQL Server. Wenn sowohl Quell-als auch Ziel verschlüsselt ist, klicken Sie dann je nach den **"allowencryptedvaluemodifications"** Massenimport Copy-Option der Treiber beim Senden Daten wie ist oder würden die Daten entschlüsseln und Verschlüsseln Sie ihn erneut, bevor Sie an SQL Server gesendet wird.  
  
 Weitere Informationen finden Sie unter der **"allowencryptedvaluemodifications"** Massenimport Kopierbefehl unten, und [Using Always Encrypted mit dem JDBC-Treiber](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
>  Die Einschränkung von Microsoft JDBC Driver 6.0 für SQL Server verwendet beim Massenkopieren von Daten aus einer CSV-Datei in verschlüsselte Spalten:  
>   
>  Nur die Transact-SQL standardmäßige Format der Zeichenfolgenliterale ist für die Datums- und Uhrzeittypen unterstützt.  
>   
>  DATETIME und SMALLDATETIME-Datentypen werden nicht unterstützt.  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>Massenkopieren-API für JDBC Driver  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy  
 Damit können Sie effizient eine SQL Server-Tabelle mit Massendaten aus einer anderen Quelle laden.  
  
 Microsoft SQL Server enthält ein beliebtes Befehlszeilen-Hilfsprogramm namens bcp zum Verschieben von Daten aus einer Tabelle in eine andere, das auf einem einzelnen Server oder serverübergreifend ausgeführt werden kann. Die Klasse „SQLServerBulkCopy“ ermöglicht Ihnen das Erstellen von Codelösungen in Java, die eine ähnliche Funktionalität bereitstellen. Es gibt eine Reihe weiterer Verfahren, Daten in eine SQL-Server-Tabelle zu laden (beispielsweise INSERT-Anweisungen), doch bietet „SQLServerBulkCopy“ ihnen gegenüber einen erheblichen Leistungsvorteil.  
  
 Die Klasse „SQLServerBulkCopy“ kann nur verwendet werden, um Daten in SQL Server-Tabellen zu schreiben. Die Datenquelle ist aber nicht auf SQL Server beschränkt; jede beliebige Datenquelle kann verwendet werden, sofern die Daten mit einer Instanz von „ResultSet“ oder einer Implementierung von „ISQLServerBulkRecord“ gelesen werden können.  
  
|Konstruktor|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopy(Connection)|Initialisiert eine neue Instanz der Klasse "sqlserverbulkcopy" mithilfe der angegebene offene Instanz einer SQLServerConnection an. Wenn für die Verbindung Transaktionen aktiviert sind, werden die Kopiervorgänge innerhalb der betreffenden Transaktion ausgeführt.|  
|"Sqlserverbulkcopy" (Zeichenfolge ConnectionURL)|Initialisiert und öffnet eine neue Instanz der SQLServerConnection basierend auf den angegebenen ConnectionURL. Der Konstruktor verwendet SQLServerConnection, um eine neue Instanz der Klasse "sqlserverbulkcopy" zu initialisieren.|  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|Zeichenfolge DestinationTableName|Name der Zieltabelle auf dem Server.<br /><br /> Wenn „DestinationTableName“ beim Aufruf von „writeToServer“ nicht festgelegt ist, wird eine SQLServerException ausgelöst.<br /><br /> "DestinationTableName" ist ein dreiteiliger Name (\<Datenbank >.\< OwningSchema >. \<Name >). Sie können den Tabellennamen mit seiner Datenbank und dem besitzenden Schema qualifizieren, wenn Sie das wünschen. Wenn im Tabellennamen jedoch ein Unterstrich ("_") oder ein anderes Sonderzeichen vorkommt, müssen Sie den Namen in eckige Klammern einschließen. Weitere Informationen finden Sie in der SQL Server-Onlinedokumentation unter "Bezeichner".|  
|ColumnMappings|Spaltenzuordnungen definieren die Beziehungen zwischen Spalten in der Datenquelle und Spalten im Ziel.<br /><br /> Wenn keine Zuordnungen definiert sind, werden die Spalten implizit auf der Grundlage ihrer Ordinalposition zugeordnet. Damit dies funktioniert, müssen Quell- und Zielschema übereinstimmen. Ist dies nicht der Fall, wird eine Ausnahme ausgelöst.<br /><br /> Wenn die Zuordnung nicht leer ist, muss nicht jede in der Datenquelle vorhandene Spalte angegeben werden. Nicht zugeordnete Spalten werden ignoriert.<br /><br /> Sie können auf Quell- und Zielspalten über den Namen oder die Ordnungszahl verweisen.|  
  
|Methode|Description|  
|------------|-----------------|  
|"Void" AddColumnMapping ((SourceColumn Int, Int DestinationColumn-Objekt)|Fügt eine neue Spaltenzuordnung hinzu, und verwendet für die Angabe von Quell- und Zielspalten Ordnungszahlen.|  
|"Void" AddColumnMapping ((SourceColumn Int, String DestinationColumn-Objekt)|Fügt eine neue Spaltenzuordnung hinzu und verwendet für die Quellspalte eine Ordnungszahl und für die Zielspalte den Spaltennamen.|  
|"Void" AddColumnMapping ((SourceColumn String, Int DestinationColumn-Objekt)|Fügt eine neue Spaltenzuordnung hinzu und verwendet einen Spaltennamen zum Beschreiben der Quellspalte und eine Ordnungszahl zum Angeben der Zielspalte.|  
|"Void" AddColumnMapping (SourceColumn Zeichenfolge, Zeichenfolge DestinationColumn-Objekt)|Fügt eine neue Spaltenzuordnung hinzu, und verwendet für die Angabe von Quell- und Zielspalten Spaltennamen.|  
|"Void" clearColumnMappings()|Löscht den Inhalt der Spaltenzuordnungen.|  
|Close() "void"|Schließt die SQLServerBulkCopy-Instanz.|  
|SQLServerBulkCopyOptions getBulkCopyOptions()|Ruft den aktuellen Satz von „SQLServerBulkCopyOptions“ ab.|  
|Zeichenfolge getDestinationTableName()|Ruft den Namen der aktuellen Zieltabelle ab.|  
|"Void" setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)|Aktualisiert das Verhalten der SQLServerBulkCopy-Instanz gemäß den angegebenen Optionen.|  
|"Void" setDestinationTableName(String tableName)|Legt den Namen der Zieltabelle fest.|  
|"Void" writeToServer(ResultSet sourceData)|Kopiert alle Zeilen im angegebenen ResultSet in eine Zieltabelle, die durch die Eigenschaft "DestinationTableName" des SQLServerBulkCopy-Objekts angegeben.|  
|"Void" writeToServer(RowSet sourceData)|Kopiert alle Zeilen im angegebenen RowSet in eine durch die Eigenschaft „DestinationTableName“ des SQLServerBulkCopy-Objekts angegebene Zieltabelle.|  
|"Void" writeToServer(ISQLServerBulkRecord sourceData)|Kopiert alle Zeilen in der angegebenen ISQLServerBulkRecord-Implementierung in eine Zieltabelle, die von der Eigenschaft "DestinationTableName" des SQLServerBulkCopy-Objekts angegeben wird.|  
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  
 Eine Auflistung von Einstellungen, die steuern, wie sich die writeToServer-Methoden in einer Instanz von „SQLServerBulkCopy“ verhalten.  
  
|Konstruktor|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopyOptions()|Initialisiert eine neue Instanz der Klasse SQLServerBulkCopyOptions mit Standardwerten für alle Einstellungen.|  
  
 Für die folgenden Optionen sind Getter und Setter vorhanden:  
  
|Option|Description|Standardwert|  
|------------|-----------------|-------------|  
|Boolesche CheckConstraints|Überprüft Bedingungen während der Einfügung von Daten.|False – es werden keine Bedingungen überprüft.|  
|Boolesche FireTriggers|Wenn der Wert angegeben wird, wird der Server veranlasst, die Einfügetrigger für die in die Datenbank eingefügten Zeilen auszulösen.|False – es werden keine Trigger ausgelöst|  
|Boolesche KeepIdentity|Die Identitätswerte der Quelltabelle werden beibehalten.|False – die Identitätswerte werden vom Ziel zugewiesen|  
|Boolesche KeepNulls|NULL-Werte in der Zieltabelle werden beibehalten, unabhängig von der Einstellung für Standardwerte.|False – NULL-Werte werden, falls anwendbar, durch Standardwerte ersetzt.|  
|Boolesche TableLock|Für die Dauer des Massenimportvorgangs wird eine Sperre für Massenaktualisierung aktiviert.|False – es werden Sperren auf Zeilenebene verwendet.|  
|Boolesche UseInternalTransaction|Wenn angegeben, wird jeder Batch des Massenkopiervorgangs innerhalb einer Transaktion verarbeitet. Wenn „SQLServerBulkCopy“ eine vorhandene Verbindung verwendet, (wie im Konstruktor angegeben), tritt eine SQLServerException auf.  Wenn „SQLServerBulkCopy“ eine dedizierte Verbindung erstellt hat, wird eine Transaktion aktiviert.|False – keine Transaktion|  
|Int BatchSize|Anzahl der Zeilen in jedem Batch. Am Ende jedes Batches werden die im Batch enthaltenen Zeilen an den Server gesendet.<br /><br /> Ein Batch ist abgeschlossen, wenn die Anzahl „BatchSize“ Zeilen verarbeitet wurde oder keine weiteren Zeilen zum Senden an die Zieldatenquelle mehr vorhanden sind.  Wenn die SQLServerBulkCopy-Instanz ohne aktive Option „UseInternalTransaction“ deklariert wurde, werden Zeilen zu jeweils „BatchSize“ zugleich an den Server gesendet, es wird jedoch keine transaktionsbezogene Aktion eingeleitet. Wenn „UseInternalTransaction“ aktiviert ist, wird jeder Batch Zeilen als separate Transaktion eingefügt.|0 – gibt an, dass jeder writeToServer-Vorgang ein einzelner Batch ist.|  
|Int BulkCopyTimeout|Anzahl der Sekunden für den Abschluss des Vorgangs, bevor ein Timeout eintritt. Der Wert „0“ bedeutet keine Einschränkung; der Massenkopiervorgang wartet unbegrenzt.|60 Sekunden.|  
|Boolesche "allowencryptedvaluemodifications"|Diese Option ist verfügbar mit Microsoft JDBC Driver 6.0 (oder höher) für SQL Server.<br /><br /> Wenn angegeben, **"allowencryptedvaluemodifications"** Massenkopieren von verschlüsselten Daten zwischen Tabellen oder Datenbanken ohne Entschlüsselung der Daten ermöglicht. In der Regel eine Anwendung würden Daten aus verschlüsselten Spalten aus einer Tabelle ohne Entschlüsselung der Daten (die app würde mit dem Schlüsselwort Spalte Encryption Einstellung auf deaktiviert festgelegt, mit der Datenbank herstellen) auswählen und dann diese Option, um die masseneinfügung die Daten, die weiterhin verschlüsselt ist. Weitere Informationen finden Sie unter [Using Always Encrypted mit dem JDBC-Treiber](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).<br /><br /> Seien Sie vorsichtig beim Angeben von **"allowencryptedvaluemodifications"** da dies zur Beschädigung der Datenbank, da der Treiber nicht überprüft, ob die Daten tatsächlich verschlüsselt führen kann, oder wenn ordnungsgemäß mit der gleichen Verschlüsselung verschlüsselt wurden Typ, Algorithmus und Schlüssel wie die Zielspalte.||  
  
 Getter und Setter:  
  
|Methoden|Description|  
|-------------|-----------------|  
|Boolesche isCheckConstraints()|Gibt an, ob Einschränkungen überprüft werden, während Daten oder nicht eingefügt werden sind.|  
|"Void" setCheckConstraints(Boolean checkConstraints)|Legt fest, ob Einschränkungen überprüft werden, während Daten oder nicht eingefügt werden.|  
|Boolesche isFireTriggers()|Gibt an, ob der Server die Insert-Trigger für die in die Datenbank eingefügten Zeilen auslösen soll.|  
|"Void" setFireTriggers(Boolean fireTriggers)|Legt fest, ob der Server für die Trigger für die in die Datenbank eingefügten Zeilen festgelegt werden soll.|  
|Boolesche isKeepIdentity()|Gibt an, ob sämtliche Quelle Identitätswerte beibehalten werden soll.|  
|"Void" setKeepIdentity(Boolean keepIdentity)|Legt fest, ob Identitätswerte beibehalten werden soll oder nicht.|  
|Boolesche isKeepNulls()|Gibt an, ob null-Werte in der Zieltabelle unabhängig von den Einstellungen für Standardwerte beibehalten, oder wenn sie die Standardwerte (falls zutreffend) ersetzt werden soll.|  
|"Void" setKeepNulls(Boolean keepNulls)|Legt fest, ob null-Werte in der Zieltabelle unabhängig von den Einstellungen für Standardwerte beibehalten, oder wenn sie die Standardwerte (falls zutreffend) ersetzt werden soll.|  
|Boolesche isTableLock()|Gibt an, ob "sqlserverbulkcopy" eine Massenaktualisierungssperre für die Dauer des Massenkopiervorgangs abrufen soll.|  
|"Void" setTableLock(Boolean tableLock)|Legt fest, ob "sqlserverbulkcopy" eine Massenaktualisierungssperre für die Dauer des Massenkopiervorgangs abrufen soll.|  
|Boolesche isUseInternalTransaction()|Gibt an, ob jeder Batch des den Massenkopiervorgang innerhalb einer Transaktion erfolgt.|  
|"Void" setUseInternalTranscation(Boolean useInternalTransaction)|Legt fest, ob jeder Batch des der Massenkopiervorgänge innerhalb einer Transaktion oder nicht auftritt.|  
|Int getBatchSize()|Ruft die Anzahl der Zeilen in jedem Batch an. Am Ende jedes Batches werden die Zeilen im Batch an den Server gesendet.|  
|"Void" setBatchSize(int batchSize)|Legt die Anzahl der Zeilen in jedem Batch an. Am Ende jedes Batches werden die im Batch enthaltenen Zeilen an den Server gesendet.|  
|Int getBulkCopyTimeout()|Ruft die Anzahl der Sekunden, bis der Vorgang abgeschlossen werden, bevor ein Timeout eintritt.|  
|"Void" setBulkCopyTimeout(int timeout)|Legt die Anzahl der Sekunden, bis der Vorgang abgeschlossen werden, bevor ein Timeout eintritt.|  
|Boolesche isAllowEncryptedValueModifications()|Gibt an, ob die Einstellung "allowencryptedvaluemodifications" aktiviert oder deaktiviert ist.|  
|"void" setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications)|Konfiguriert die "allowencryptedvaluemodifications"-Einstellung, die für das Massenkopieren mit Always Encrypted-Spalten verwendet wird.|  
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  
 Die Schnittstelle „ISQLServerBulkRecord“ kann verwendet werden, um Klassen zu erstellen, die Daten aus jeder beliebigen Quelle (wie etwa einer Datei) einlesen und ermöglicht es einer SQLServerBulkCopy-Instanz, ein Massenladen einer SQL Server-Tabelle mit diesen Daten auszuführen.  
  
|Schnittstellenmethoden|Description|  
|-----------------------|-----------------|  
|Legen Sie\<ganze Zahl > getColumnOrdinals()|Ruft die Ordnungszahlen für jede der in diesem Datensatz enthaltenen Spalten ab.|  
|Zeichenfolge getColumnName(int column)|Ruft den Namen der angegebenen Spalte ab.|  
|Int GetColumnType (Int-Spalte)|Ruft den JDBC-Datentyp der angegebenen Spalte ab.|  
|Int GetPrecision (Int-Spalte)|Ruft die Genauigkeit für die angegebene Spalte ab.|  
|Objekt [] getRowData()|Ruft die Daten für die aktuelle Zeile als Array von Objekten ab.<br /><br /> Jedes Objekt muss mit dem Java-Sprachtyp übereinstimmen, der zur Darstellung des angegebenen JDBC-Datentyps für die angegebene Spalte verwendet wird.  Weitere Informationen und die passenden Zuordnungen finden Sie unter „Grundlegendes zu den Datentypen in JDBC Driver“.|  
|Int GetScale (Int-Spalte)|Ruft die Dezimalstellen für die angegebene Spalte ab.|  
|Boolesche IsAutoIncrement (Int-Spalte)|Zeigt an, ob es sich bei der Spalte um eine Identitätsspalte handelt.|  
|Boolesche::Next()|Springt zur nächsten Datenzeile.|  
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  
 Eine einfache Implementierung der ISQLServerBulkRecord-Schnittstelle, die zum Einlesen der einfachen Java-Datentypen aus einer Datei mit Trennzeichen verwendet werden kann, in der jede Zeile eine Datenzeile darstellt.  
  
 Hinweise zur Implementierung und Einschränkungen:  
  
1.  Die maximal in jeder vorhandenen Zeile zulässige Datenmenge ist durch den verfügbaren Arbeitsspeicher begrenzt, da die Daten zeilenweise gelesen werden.  
  
2.  Das Streaming großer Datentypen, wie etwa „varchar(max)“, „varbinary(max)“, „nvarchar(max)“, „sqlxml“, „ntext“ wird nicht unterstützt.  
  
3.  Das für die CSV-Datei verwendete Trennzeichen darf an keiner Stelle innerhalb der Daten auftreten und muss ordnungsgemäß escaped werden, wenn es in den regulären Java-Ausdrücken zu den eingeschränkten Zeichen gehört.  
  
4.  In der CSV-Dateiimplementierung werden doppelte Anführungszeichen als Teil der Daten behandelt. Beispielsweise würde die Zeile Hallo,”Welt”,”Hallo,Welt” als aus vier Spalten mit den Werten Hallo, “Welt”, “Hallo und Welt” bestehend aufgefasst, wenn als Trennzeichen Komma verwendet wird.  
  
5.  Zeilenvorschubzeichen werden als Zeilenendzeichen verwendet und dürfen an keiner Stelle in den Daten auftreten.  
  
|Konstruktor|Description|  
|-----------------|-----------------|  
|SQLServerBulkCSVFileRecord (Zeichenfolge FileToParse, zeichenfolgencodierung, Zeichenfolgentrennzeichen, boolesche FirstLineIsColumnNamesSQLServerBulkCSVFileRecord (String, String, String, Boolean)|Initialisiert eine neue Instanz der SQLServerBulkCSVFileRecord-Klasse, die jede Zeile in der zu analysierenden Datei „fileToParse“ mit dem angegebenen Trennzeichen und der angegebenen Codierung analysiert. Wenn „firstLineIsColumnNames“ auf „True“ festgelegt ist, wird der Inhalt der ersten Zeile der Datei als Spaltennamen analysiert.  Wenn die Codierung NULL ist, wird die Standardcodierung verwendet.|  
|SQLServerBulkCSVFileRecord (Zeichenfolge FileToParse, Zeichenfolge, die Codierung, boolesche FirstLineIsColumnNamesSQLServerBulkCSVFileRecord (String, String, Boolean)|Initialisiert eine neue Instanz der SQLServerBulkCSVFileRecord-Klasse, die jede Zeile in der zu analysierenden Datei „fileToParse“ mit Komma als Trennzeichen und der angegebenen Codierung analysiert. Wenn „firstLineIsColumnNames“ auf „True“ festgelegt ist, wird der Inhalt der ersten Zeile der Datei als Spaltennamen analysiert.  Wenn die Codierung NULL ist, wird die Standardcodierung verwendet.|  
|SQLServerBulkCSVFileRecord (Zeichenfolge FileToParse, boolesche FirstLineIsColumnNamesSQLServerBulkCSVFileRecord (String, Boolean)|Initialisiert eine neue Instanz der SQLServerBulkCSVFileRecord-Klasse, die jede Zeile in der zu analysierenden Datei „fileToParse“ mit Komma als Trennzeichen und der Standardcodierung analysiert. Wenn FirstLineIsColumnNames auf "true" festgelegt ist, wird die erste Zeile in der Datei wird als Spaltennamen analysiert werden.|  
  
|Methode|Description|  
|------------|-----------------|  
|"Void" AddColumnMetadata (Int PositionInFile, Zeichenfolge ColumnName, Int JdbcType, Genauigkeit Int, Int Skalierung)|Fügt Metadaten für die angegebene Spalte in der Datei hinzu.|  
|Close() "void"|Gibt alle dem Dateileser zugeordneten Ressourcen frei.|  
|"Void" SetTimestampWithTimezoneFormat (DateTim eFormatter dateTimeFormatter|Legt das Format für die Analyse von Zeitstempeldaten aus der Datei auf „java.sql.Types.TIMESTAMP_WITH_TIMEZONE“ fest.|  
|"Void" setTimestampWithTimezoneFormat(String dateTimeFormat)setTimeWithTimezoneFormat(DateTimeFormatter)|Legt das Format für die Analyse von Uhrzeitdaten aus der Datei auf „java.sql.Types.TIME_WITH_TIMEZONE“ fest.|  
|"Void" SetTimeWithTimezoneFormat (DateTimeForm Atter DateTimeFormatter)|Legt das Format für die Analyse von Uhrzeitdaten aus der Datei auf „java.sql.Types.TIME_WITH_TIMEZONE“ fest.|  
|"Void" setTimeWithTimezoneFormat(String timeFormat)|Legt das Format für die Analyse von Uhrzeitdaten aus der Datei auf „java.sql.Types.TIME_WITH_TIMEZONE“ fest.|  
  
## <a name="see-also"></a>Siehe auch  
 [Overview of the JDBC Driver (Übersicht über den JDBC-Treiber)](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
