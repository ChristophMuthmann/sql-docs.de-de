---
title: Verwenden von ADO mit OLE DB-Treiber für SQLServer | Microsoft Docs
description: Verwenden von ADO mit OLE DB-Treiber für SQLServer
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 48f16f274d616489a5b7a796c6327ce59427f4a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>Verwenden von ADO mit OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Um die neuen Funktionen in nutzen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] z. B. mehrere aktive Resultsets (MARS), abfragebenachrichtigungen, benutzerdefinierte Typen (UDTs) oder das neue **Xml** -Datentyp, vorhandene Anwendungen, die mithilfe von ActiveX Data Objects (ADO) sollte der OLE DB-Treiber für SQL Server als Datenzugriffsanbieter verwenden.  
  
 So aktivieren Sie ADO verwenden Sie die neue Funktionen von neueren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Verbesserungen an der OLE DB-Treiber für SQL Server, die die Kernfunktionen von OLE DB erweitert vorgenommen wurden. Diese Erweiterungen erlauben es ADO-Anwendungen, neuere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Funktionen und zwei Daten verarbeiten, Typen, die in eingeführt [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **Xml** und **Udt**. Diese Verbesserungen nutzen auch Verbesserungen an der **Varchar**, **Nvarchar**, und **Varbinary** Datentypen. OLE DB-Treiber für SQL Server fügt die Initialisierungseigenschaft SSPROP_INIT_DATATYPECOMPATIBILITY dem DBPROPSET_SQLSERVERDBINIT-Eigenschaft, die für die Verwendung von ADO-Anwendungen so festlegen, dass die neuen Datentypen in einer mit ADO kompatiblen Weise verfügbar gemacht werden. Darüber hinaus definiert der OLE DB-Treiber für SQL Server auch ein neues Schlüsselwort für Verbindungszeichenfolgen mit dem Namen **DataTypeCompatibility** , die in der Verbindungszeichenfolge festgelegt ist.  

> [!NOTE]  
>  Vorhandene ADO-Anwendungen können über den SQLOLEDB-Anbieter auf XML, UDT, umfangreiche Textwerte und Werte von Binärfeldern zugreifen und diese aktualisieren. Die neuen größeren **varchar(max)**, **nvarchar(max)**, und **varbinary(max)** Datentypen werden als die ADO-Datentypen zurückgegeben **AdLongVarChar**, **AdLongVarWChar** und **AdLongVarBinary** bzw. XML-Spalten werden zurückgegeben, als **AdLongVarChar**, UDT-Spalten werden als zurückgegeben **AdVarBinary**. Jedoch, wenn Sie den OLE DB-Treiber für SQL Server (MSOLEDBSQL) statt des SQLOLEDB verwenden, müssen Sie sicherstellen der **DataTypeCompatibility** Schlüsselwort auf "80", damit die neuen Datentypen richtig den entsprechenden ADO-Datentypen zugeordnet werden.  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>Aktivieren der OLE DB-Treiber für SQLServer über ADO  
 Um die Verwendung von OLE DB-Treiber für SQL Server zu aktivieren, müssen ADO-Anwendungen implementieren die folgenden Schlüsselwörter in ihrer Verbindungszeichenfolge angeben:  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 Weitere Informationen zu den ADO-Verbindungszeichenfolgen in OLE DB-Treiber für SQL Server unterstützten Schlüsselwörter finden Sie unter [Schlüsselwörtern für Verbindungszeichenfolgen mit OLE DB-Treiber für SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  

 Im folgenden finden ein Beispiel zum Einrichten einer ADO-Verbindungszeichenfolge, die vollständig aktiviert ist, arbeiten mit OLE DB-Treiber für SQL Server, einschließlich der MARS-Funktion zu aktivieren:  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  

## <a name="examples"></a>Beispiele  
 Die folgenden Abschnitte enthalten Beispiele dafür, wie Sie ADO mit dem OLE DB-Treiber für SQL Server verwenden können.  

### <a name="retrieving-xml-column-data"></a>Abrufen von XML-Spaltendaten  
 In diesem Beispiel wird ein Recordset verwendet, abrufen und Anzeigen der Daten aus einer XML-Spalte in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** -Beispieldatenbank.  

```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _   
         & "DataTypeCompatibility=80;"  

con.Open  

' Get the xml data as a recordset.  
Set rst.ActiveConnection = con  
rst.Source = "SELECT AdditionalContactInfo FROM Person.Contact " _  
   & "WHERE AdditionalContactInfo IS NOT NULL"  
rst.Open  

' Display the data in the recordset.  
While (Not rst.EOF)  
   sXMLResult = rst.Fields("AdditionalContactInfo").Value  
   Debug.Print (sXMLResult)  
   rst.MoveNext  
End While  

con.Close  
Set con = Nothing  
```  

> [!NOTE]  
>  Recordset-Filter werden bei XML-Spalten nicht unterstützt. Wenn sie verwendet werden, wird ein Fehler zurückgegeben.  

### <a name="retrieving-udt-column-data"></a>Abrufen von UDT-Spaltendaten  
 In diesem Beispiel wird eine **Befehl** Objekt wird verwendet, um eine SQL-Abfrage ausführen, die einen UDT zurückgibt, die UDT-Daten werden aktualisiert, und klicken Sie dann die neuen Daten zurück in die Datenbank eingefügt werden. In diesem Beispiel wird vorausgesetzt, dass die **Punkt** UDT in der Datenbank wurde bereits registriert.  

```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;"  

con.Open  

' Get the UDT value.  
Set cmd.ActiveConnection = con  
cmd.CommandText = "SELECT ID, Pnt FROM dbo.Points.ToString()"  
Set rst = cmd.Execute  
strTempID = rst.Fields(0).Value  
strOldUDT = rst.Fields(1).Value  

' Do something with the UDT by adding i to each point.  
arytempUDT = Split(strOldUDT, ",")  
i = 3  
strNewUDT = LTrim(Str(Int(aryTempUDT(0)) + i)) + "," + _  
   LTrim(Str(Int(aryTempUDT(1)) + i))  

' Insert the new value back into the database.  
cmd.CommandText = "UPDATE dbo.Points SET Pnt = '" + strNewUDT + _  
   "' WHERE ID = '" + strTempID + "'"  
cmd.Execute  

con.Close  
Set con = Nothing  
```  

### <a name="enabling-and-using-mars"></a>Aktivieren und Verwenden von MARS  
 In diesem Beispiel wird die Verbindungszeichenfolge zum Aktivieren von MARS über den OLE DB-Treiber für SQL Server erstellt, und anschließend werden zwei Recordset-Objekte erstellt, um mithilfe derselben Verbindung ausgeführt.  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  

Dim recordset1 As New ADODB.Recordset  
Dim recordset2 As New ADODB.Recordset  

Dim recordsaffected As Integer  
Set recordset1 =  con.Execute("SELECT * FROM Table1", recordsaffected, adCmdText)  
Set recordset2 =  con.Execute("SELECT * FROM Table2", recordsaffected, adCmdText)  

con.Close  
Set con = Nothing  
```  

 In früheren Versionen des OLE DB-Anbieters hätte dieser Code bewirkt, dass für den zweiten Execute-Aufruf eine Standardverbindung erstellt wird, weil in diesen Versionen nur ein aktives Resultset pro Verbindung geöffnet werden konnte. Weil die Standardverbindung nicht in den OLE DB-Verbindungspool aufgenommen wurde, bedeutete dies zusätzlichen Aufwand. Mit der MARS-Funktion, die von der OLE DB-Treiber für SQL Server verfügbar gemacht werden erhalten Sie mehrere aktive Resultsets in einer Verbindung.  

## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem OLE DB-Treiber für SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
