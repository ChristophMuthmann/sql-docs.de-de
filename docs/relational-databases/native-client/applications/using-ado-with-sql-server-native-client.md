---
title: Verwenden von ADO mit SQL Server Native Client | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 143ecc459ba43c4f0bc68c0a03c3ffa4f4cfb9e7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="using-ado-with-sql-server-native-client"></a>Verwenden von ADO mit SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Um die neuen Funktionen in nutzen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] z. B. mehrere aktive Resultsets (MARS), abfragebenachrichtigungen, benutzerdefinierte Typen (UDTs) oder das neue **Xml** -Datentyp, vorhandene Anwendungen, die mithilfe von ActiveX Data Objects (ADO) verwenden, sollten die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter als Datenzugriffsanbieter.  
  
 Wenn keine der neuen Funktionen von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] erforderlich ist, dann ist es auch nicht notwendig, den OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client zu verwenden. Sie können weiterhin mit dem aktuellen Datenzugriffsanbieter (in der Regel SQLOLEDB) arbeiten. Wenn Sie eine bestehende Anwendung erweitern und die neuen Funktionen von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] verwenden müssen, dann sollten Sie den OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwenden.  
  
> [!NOTE]  
>  Wenn Sie eine neue Anwendung entwickeln, wird empfohlen, über ADO.NET und den .NET Framework-Datenanbieter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] statt über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client auf die neuen Funktionen der letzten Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zuzugreifen. Weitere Informationen zum .NET Framework-Datenanbieter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] finden Sie in der .NET Framework-SDK-Dokumentation für ADO.NET.  
  
 Damit ADO die neuen Funktionen der letzten Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nutzen kann, wurde der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, der die Kernfunktionen von OLE DB erweitert, um einige Erweiterungen ergänzt. Diese Erweiterungen erlauben es ADO-Anwendungen, neuere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Funktionen und zwei Daten verarbeiten, Typen, die in eingeführt [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **Xml** und **Udt**. Diese Verbesserungen nutzen auch Verbesserungen an der **Varchar**, **Nvarchar**, und **Varbinary** Datentypen. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt die Initialisierungseigenschaft SSPROP_INIT_DATATYPECOMPATIBILITY dem DBPROPSET_SQLSERVERDBINIT-Eigenschaft, die für die Verwendung von ADO-Anwendungen so festlegen, dass die neuen Datentypen in einer mit ADO kompatiblen Weise verfügbar gemacht werden. Darüber hinaus die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter definiert auch ein neues Schlüsselwort für Verbindungszeichenfolgen mit dem Namen **DataTypeCompatibility** , die in der Verbindungszeichenfolge festgelegt ist.  
  
> [!NOTE]  
>  Vorhandene ADO-Anwendungen können über den SQLOLEDB-Anbieter auf XML, UDT, umfangreiche Textwerte und Werte von Binärfeldern zugreifen und diese aktualisieren. Die neuen größeren **varchar(max)**, **nvarchar(max)**, und **varbinary(max)** Datentypen werden als die ADO-Datentypen zurückgegeben **AdLongVarChar**, **AdLongVarWChar** und **AdLongVarBinary** bzw. XML-Spalten werden zurückgegeben, als **AdLongVarChar**, UDT-Spalten werden als zurückgegeben **AdVarBinary**. Allerdings bei Verwendung der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter (SQLNCLI11) statt des SQLOLEDB, müssen Sie sicherstellen der **DataTypeCompatibility** Schlüsselwort auf "80", damit die neuen Datentypen richtig zugeordnet werden, auf die ADO-Daten Typen.  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>Aktivieren von SQL Server Native Client über ADO  
 So aktivieren Sie die Verwendung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ADO-Anwendungen müssen die folgenden Schlüsselwörter in den Verbindungszeichenfolgen zu implementieren:  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 Weitere Informationen zu den ADO-Verbindungszeichenfolgen Schlüsselwörter unterstützt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Im folgenden ist ein Beispiel zum Einrichten einer ADO-Verbindungszeichenfolge, die vollständig aktiviert ist, arbeiten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, einschließlich der MARS-Funktion zu aktivieren:  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Abschnitte enthalten Beispiele für die Verwendung von ADO mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter.  
  
### <a name="retrieving-xml-column-data"></a>Abrufen von XML-Spaltendaten  
 In diesem Beispiel wird ein Recordset verwendet, abrufen und Anzeigen der Daten aus einer XML-Spalte in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** -Beispieldatenbank.  
  
```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
 In diesem Beispiel wird die Verbindungszeichenfolge erstellt, zum Aktivieren von MARS über den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter, und klicken Sie dann zwei Recordset-Objekte werden erstellt, um mithilfe derselben Verbindung ausgeführt.  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
  
 In früheren Versionen des OLE DB-Anbieters hätte dieser Code bewirkt, dass für den zweiten Execute-Aufruf eine Standardverbindung erstellt wird, weil in diesen Versionen nur ein aktives Resultset pro Verbindung geöffnet werden konnte. Weil die Standardverbindung nicht in den OLE DB-Verbindungspool aufgenommen wurde, bedeutete dies zusätzlichen Aufwand. Mit MARS-Funktion verfügbar gemacht, indem die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter, erhalten Sie mehrere aktive Resultsets in einer Verbindung.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen von Anwendungen mit SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
