---
title: Verwenden von XML-Daten in Anwendungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [XML in SQL Server]
- XML [SQL Server], ADO
- columns [XML in SQL Server], ADO.NET
- ADO [XML in SQL Server]
- columns [XML in SQL Server], SQL Server Native Client
- xml data type [SQL Server], ADO
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- ADO.NET [XML in SQL Server]
- XML [SQL Server], ADO.NET
- columns [XML in SQL Server], ADO
- xml data type [SQL Server], ADO.NET
- XML [SQL Server], SQL Server Native Client
ms.assetid: 5dabf7e0-c6df-451d-a070-4661f84607fd
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2ae4b7e7ed2efc44ce1b432313d56288a66e778c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="use-xml-data-in-applications"></a>Verwenden von XML-Daten in Anwendungen
  In diesem Thema werden die Optionen beschrieben, die Ihnen bei der Arbeit mit dem **xml** -Datentyp in Ihrer Anwendung zur Verfügung stehen. Das Thema enthält Informationen zu Folgendem:  
  
-   Verarbeiten von XML in einer Spalte vom Typ **xml** mithilfe von ADO und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Verarbeiten von XML in einer Spalte vom Typ **xml** mithilfe von ADO.NET  
  
-   Verarbeiten des **xml** -Typs in Parametern mithilfe von ADO.NET  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-ado-and-sql-server-native-client"></a>Verarbeiten von XML in einer Spalte vom Typ xml mithilfe von ADO und SQL Server Native Client  
 Damit mit MDAC-Komponenten auf Typen und Funktionen zugegriffen werden kann, die in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]eingeführt wurden, müssen Sie die „DataTypeCompatibility“-Initialisierungseigenschaft in der ADO-Verbindungszeichenfolge festlegen.  
  
 Im folgenden VBScript-Beispiel werden die Ergebnisse der Abfrage einer **xml** -Datentypspalte, `Demographics`, in der `Sales.Store` -Tabelle der `AdventureWorks2012` -Beispieldatenbank angezeigt. Die Abfrage sucht insbesondere nach dem Instanzwert dieser Spalte für die Zeile, in der die `CustomerID` gleich dem Wert `3`ist.  
  
```  
Const DS = "MyServer"  
Const DB = "AdventureWorks2012"  
  
Set objConn = CreateObject("ADODB.Connection")  
Set objRs = CreateObject("ADODB.Recordset")  
  
CommandText = "SELECT Demographics" & _  
              " FROM Sales.Store" & _  
              " INNER JOIN Sales.Customer" & _  
              " ON Sales.Store.BusinessEntityID = sales.customer.StoreID" & _  
              " WHERE Sales.Customer.CustomerID = 3" & _  
              " OR Sales.Customer.CustomerID = 4"  
  
ConnectionString = "Provider=SQLNCLI11" & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;" & _  
                   "DataTypeCompatibility=80"  
  
'Connect to the data source.  
objConn.Open ConnectionString  
  
'Execute command through the connection and display  
Set objRs = objConn.Execute(CommandText)  
  
Dim rowcount  
rowcount = 0  
Do While Not objRs.EOF  
   rowcount = rowcount + 1  
   MsgBox "Row " & rowcount & _  
           vbCrLf & vbCrLf & objRs(0)  
   objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```  
  
 In diesem Beispiel wird dargestellt, wie die Datentyp-Kompatibilitätseigenschaft festgelegt wird. Sie ist standardmäßig auf 0 (null) festgelegt, wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client verwenden. Wenn Sie den Wert auf 80 festgelegt haben, sorgt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Anbieter dafür, dass **xml** -Spalten und Spalten eines benutzerdefinierten Typs als [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] -Datentypen angezeigt werden. Dabei handelt es sich um DBTYPE_WSTR und DBTYPE_BYTES.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client muss ebenfalls auf dem Clientcomputer installiert und in der Verbindungszeichenfolge mit „`Provider=SQLNCLI11;...`“ zur Verwendung als Datenanbieter angegeben sein.  
  
#### <a name="to-test-this-example"></a>So testen Sie dieses Beispiel  
  
1.  Prüfen Sie, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client installiert ist und ob MDAC 2.6.0 oder höher auf dem Clientcomputer zur Verfügung steht.  
  
     Weitere Informationen finden Sie unter [SQL Server Native Client-Programmierung](../../relational-databases/native-client/sql-server-native-client-programming.md).  
  
2.  Prüfen Sie, ob die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist.  
  
     Für dieses Beispiel benötigen Sie die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank.  
  
3.  Kopieren Sie den weiter oben in diesem Thema dargestellten Code, und fügen Sie ihn in Ihren Text- oder Code-Editor ein. Speichern Sie die Datei unter dem Dateinamen HandlingXmlDataType.vbs.  
  
4.  Ändern Sie das Skript entsprechend Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation, und speichern Sie die Änderungen.  
  
     Wenn z. B. `MyServer` angegeben ist, sollten Sie es durch `(local)` oder den tatsächlichen Namen des Servers ersetzen, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist.  
  
5.  Führen Sie HandlingXmlDataType.vbs und das Skript aus.  
  
 Die Ergebnisse sollten ähnlich wie die folgende Beispielausgabe aussehen:  
  
```  
Row 1  
  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>1500000</AnnualSales>  
  <AnnualRevenue>150000</AnnualRevenue>  
  <BankName>Primary International</BankName>  
  <BusinessType>OS</BusinessType>  
  <YearOpened>1974</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>38000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>40</NumberEmployees>  
</StoreSurvey>  
  
Row 2  
  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>United Security</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1976</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>6000</SquareFeet>  
  <Brands>2</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>5</NumberEmployees>  
</StoreSurvey>  
```  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-adonet"></a>Verarbeiten von XML in einer Spalte vom Typ xml mithilfe von ADO.NET  
 Um XML in einer **xml** -Datentypspalte mithilfe von ADO.NET und [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] zu verarbeiten, können Sie das Standardverhalten der **SqlCommand** -Klasse verwenden. Eine **xml** -Datentypspalte und ihre Werte können z. B. mit einem **SqlDataReader**auf dieselbe Weise abgerufen werden wie eine beliebige SQL-Spalte. Wenn Sie jedoch mit dem Inhalt einer **xml** -Datentypspalte als XML arbeiten möchten, müssen Sie den Inhalt zunächst einem **XmlReader** -Typ zuweisen.  
  
 Weitere Informationen sowie einen Beispielcode finden Sie im Abschnitt über die XML-Spaltenwerte in einem Datenleser in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] -SDK-Dokumentation.  
  
## <a name="handling-an-xml-type-column-in-parameters-by-using-adonet"></a>Verarbeiten einer Spalte vom Typ xml in Parametern mithilfe von ADO.NET  
 Um einen xml-Datentyp, der als Parameter in ADO.NET und [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]übergeben wird, zu verarbeiten, können Sie den Wert als eine Instanz des **SqlXml** -Datentyps angeben. Es ist keine besondere Verarbeitung erforderlich, da die **xml** -Datentypspalten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Parameterwerte auf dieselbe Weise annehmen können wie andere Spalten und Datentypen, z. B. **string** oder **integer**.  
  
 Weitere Informationen sowie einen Beispielcode finden Sie im Abschnitt über die als Befehlsparameter verwendeten XML-Werte in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] -SDK-Dokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
