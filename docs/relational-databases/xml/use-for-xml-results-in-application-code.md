---
title: Verwenden von FOR XML-Ergebnissen in Anwendungscode | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML clause, application code usage
- XML [SQL Server], FOR XML clause
- ASP.NET [SQL Server]
- .NET Framework [SQL Server], FOR XML data
- ADO [SQL Server]
- XML data islands [SQL Server]
- data islands [SQL Server]
ms.assetid: 41ae67bd-ece9-49ea-8062-c8d658ab4154
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d06987ca4d4f9bf0b9aee605effdeb78ab3f095
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="use-for-xml-results-in-application-code"></a>Verwenden von FOR XML-Ergebnissen in Anwendungscode
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Mithilfe von FOR XML-Klauseln in SQL-Abfragen können Sie Abfrageergebnisse abrufen und sogar in XML-Daten umwandeln. Diese Funktionalität bietet Ihnen die folgenden Möglichkeiten, wenn FOR XML-Abfrageergebnisse in XML-Anwendungscode verwendet werden können:  
  
-   Abfragen von SQL-Tabellen für Instanzen von Werten von [XML-Daten&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
-   Wenden Sie die [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md) an, um das Ergebnis von Abfragen zurückzugeben, die typisierte Text- oder Imagedaten als XML enthalten.  
  
 Dieses Thema enthält Beispiele und veranschaulicht diese Vorgehensweisen.  
  
## <a name="retrieving-for-xml-data-with-ado-and-xml-data-islands"></a>Abrufen von FOR XML-Daten mit ADO und XML-Dateninseln  
 Beim Arbeiten mit FOR XML-Abfragen kann das ADO-Objekt **Stream** oder andere Objekte, die die **IStream** -COM-Schnittstelle unterstützen, wie z.B. die ASP-Objekte (Active Server Pages) **Request** und **Response** , zum Aufnehmen der Ergebnisse verwendet werden.  
  
 Der folgende ASP-Code zeigt z. B. die Ergebnisse der Abfrage der **xml** -Datentypspalte Demographics in der Sales.Store-Tabelle der AdventureWorks-Beispieldatenbank. Insbesondere sucht die Abfrage nach dem Instanzwert dieser Spalte für die Zeile, in der die CustomerID gleich 3 ist.  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<!-- %  Option Explicit      % -->  
<!-- 'Request.ServerVariables("SERVER_NAME") & ";" & _ -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=(local);" & _  
            "Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
   Response.write "Connect String = " & sConn & "<BR/>"  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
   adoConn.Open  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO</sql:query></ROOT>"  
   Response.write "Query String = " & sQuery & "<BR/>"  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
%>  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   Dim root  
   Set root = xmlDoc.documentElement.childNodes.Item(0).childNodes.Item(0).childNodes.Item(0)  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI><B>" & child.nodeName &  ":</B>  " & child.Text  & "</LI>"  
   Next  
   MsgBox xmlDoc.xml  
</SCRIPT>  
</HEAD>  
<BODY>  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
```  
  
 Diese ASP-Beispielseite enthält serverseitiges VBScript, das ADO zum Ausführen der FOR XML-Abfrage und zum Zurückgeben der XML-Ergebnisse in einer XML-Dateninsel (MyDataIsle) verwendet. Diese XML-Dateninsel wird dann an den Browser zurückgegeben und zur weiteren clientseitigen Verarbeitung bereitgestellt. Anschließend wird zusätzlicher clientseitiger VBScript-Code verwendet, um den Inhalt der XML-Dateninsel zu verarbeiten. Dieser Vorgang wird durchgeführt, bevor der Inhalt als Teil des resultierenden DHTML-Codes angezeigt und ein Meldungsfeld geöffnet wird, das den vorverarbeiteten Inhalt der XML-Dateninsel zeigt.  
  
#### <a name="to-test-this-example"></a>So testen Sie dieses Beispiel  
  
1.  Überprüfen Sie, dass IIS installiert ist und dass die AdventureWorks-Beispieldatenbank für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert wurde.  
  
     Für dieses Beispiel ist es erforderlich, dass Internet Information Services (IIS) Version 5.0 oder höher installiert und die ASP-Unterstützung aktiviert ist. Außerdem muss die AdventureWorks-Beispieldatenbank installiert sein.  
  
2.  Kopieren Sie das zuvor bereitgestellte Codebeispiel, und fügen Sie es in den von Ihnen verwendeten XML- oder Texteditor ein. Speichern Sie die Datei als RetrieveResults.asp im Stammverzeichnis, das für IIS verwendet wird. Üblicherweise ist das C:Inetpub\wwwroot.  
  
3.  Öffnen Sie die ASP-Seite in einem Browserfenster, indem Sie die folgende URL verwenden. Ersetzen Sie zunächst 'MyServer' entweder durch "localhost" oder durch den tatsächlichen Namen des Servers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und IIS installiert sind.  
  
    ```  
    http://MyServer/RetrieveResults.asp  
    ```  
  
 Die generierten HTML-Seitenergebnisse, die angezeigt werden, ähneln der folgenden Beispielausgabe:  
  
##### <a name="server-side-processing"></a>Serverseitiges Verarbeiten  
 Page Generated @ 3/11/2006 3:36:02 PM  
  
 Connect String = Provider=SQLOLEDB;Data Source=MyServer;Initial Catalog=AdventureWorks;Integrated Security=SSPI;  
  
 ADO Version = 2.8  
  
 adoConn.State = 1  
  
 Query String = SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO  
  
 Pushen von XML an Client zum Verarbeiten  
  
##### <a name="client-side-processing-of-xml-document-mydataisle"></a>Clientseitiges Verarbeiten von XML-Dokument MyDataIsle  
  
-   **AnnualSales:** 1500000  
  
-   **AnnualRevenue:** 150000  
  
-   **BankName:** Primary International  
  
-   **BusinessType:** OS  
  
-   **YearOpened:** 1974  
  
-   **Specialty:** Road  
  
-   **SquareFeet:** 38000  
  
-   **Brands:** 3  
  
-   **Internet:** DSL  
  
-   **NumberEmployees:** 40  
  
 Das VBScript-Meldungsfeld zeigt dann den folgenden ursprünglichen, ungefilterten Inhalt der XML-Dateninsel, der durch die Ergebnisse der FOR XML-Abfrage zurückgegeben wurde.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Sales.Store>  
    <Demographics>  
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
    </Demographics>  
  </Sales.Store>  
</ROOT>  
```  
  
## <a name="retrieving-for-xml-data-with-aspnet-and-the-net-framework"></a>Abrufen der FOR XML-Daten mit ASP.NET und .Net Framework  
 Wie im vorherigen Beispiel zeigt auch der folgende ASP-Code die Ergebnisse der Abfrage der **xml** -Datentypspalte Demographics in der Sales.Store-Tabelle der AdventureWorks-Beispieldatenbank. Und wie im vorherigen Beispiel sucht die Abfrage nach dem Instanzwert dieser Spalte für die Zeile, in der die CustomerID gleich 3 ist.  
  
 In diesem Beispiel werden jedoch die folgenden verwalteten APIs von Microsoft .NET Framework verwendet, um das Zurückgeben und das Rendering der Ergebnisse der FOR XML-Abfrage zu erzielen.  
  
1.  **SqlConnection** wird verwendet, um basierend auf dem Inhalt einer angegebenen Verbindungszeichenfolgenvariablen stConn eine Verbindung mit SQL Server zu öffnen.  
  
2.  **SqlDataAdapter** wird dann als Datenadapter verwendet, und es verwendet die SQL-Verbindung und eine angegebene SQL-Abfragezeichenfolge, um die FOR XML-Abfrage auszuführen.  
  
3.  Nach dem Ausführen der Abfrage wird die **SqlDataAdapter.Fill** -Methode aufgerufen und an eine Instanz eines **DataSet,** MyDataSet übergeben, um das Dataset mit der Ausgabe der FOR XML-Abfrage zu füllen.  
  
4.  Anschließend wird die **DataSet.GetXml** -Methode aufgerufen, um die Abfrageergebnisse als eine Zeichenfolge zurückzugeben, die in der vom Server generierten HTML-Seite angezeigt werden kann.  
  
    ```  
    <%@ Page Language="VB" %>  
    <HTML>  
    <HEAD>  
    <TITLE>FOR XML Query Example</TITLE>  
    <STYLE>  
       BODY  
       {  
          FONT-FAMILY: Tahoma;  
          FONT-SIZE: 8pt;  
          OVERFLOW: auto  
       }  
       H3  
       {  
          FONT-FAMILY: Tahoma;  
          FONT-SIZE: 8pt;  
          OVERFLOW: auto  
       }  
    </STYLE>  
    </HEAD>  
    <BODY>  
    <%  
    Dim s as String  
    s = "<H3>Server-side processing</H3>" & _  
        "Page Generated @ " & Now() & "<BR/>"  
  
    Dim SQL As String   
    SQL = "SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO"  
  
    Dim strConn As String   
    strConn = "Server=(local);Database=AdventureWorks;Integrated Security=SSPI;"  
  
    Dim MySqlConn As New System.Data.SqlClient.SqlConnection(strConn)  
    Dim MySqlAdapter As New System.Data.SqlClient.SqlDataAdapter(SQL,MySqlConn)  
    Dim MyDataSet As New System.Data.DataSet  
  
    MySqlConn.Open()  
    s = s & "<P>SqlConnection opened.</P>"   
  
    MySqlAdapter.Fill(MyDataSet)  
    s = s & "<P>" & MyDataSet.GetXml  & "</P>"  
  
    MySqlConn.Close()  
    s = s & "<P>SqlConnection closed.</P>"   
  
    Message.InnerHtml=s  
    %>  
    <SPAN id="Message" runat=server />  
    </BODY>  
    </HTML>  
    ```  
  
#### <a name="to-test-this-example"></a>So testen Sie dieses Beispiel  
  
1.  Überprüfen Sie, dass IIS installiert ist und dass die AdventureWorks-Beispieldatenbank für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert wurde.  
  
     Für dieses Beispiel ist es erforderlich, dass Internet Information Services (IIS) Version 5.0 oder höher installiert und die ASP.NET-Unterstützung aktiviert ist. Außerdem muss die AdventureWorks-Beispieldatenbank installiert sein.  
  
2.  Kopieren Sie den zuvor bereitgestellten Code, und fügen Sie ihn in den von Ihnen verwendeten XML- oder Texteditor ein. Speichern Sie die Datei als RetrieveResults.aspx im Stammverzeichnis, das für IIS verwendet wird. Üblicherweise ist das C:Inetpub\wwwroot.  
  
3.  Öffnen Sie die ASP.NET-Seite in einem Browserfenster, indem Sie die folgende URL verwenden. Ersetzen Sie zunächst 'MyServer' entweder durch "localhost" oder durch den tatsächlichen Namen des Servers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und IIS installiert sind.  
  
    ```  
    http://MyServer/RetrieveResults.aspx  
    ```  
  
 Die generierten HTML-Seitenergebnisse, die angezeigt werden, ähneln der folgenden Beispielausgabe:  
  
##### <a name="server-side-processing"></a>Serverseitiges Verarbeiten  
  
```  
Page Generated @ 3/11/2006 3:36:02 PM  
  
SqlConnection opened.  
  
<Sales.Store><Demographics><StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey"><AnnualSales>1500000</AnnualSales><AnnualRevenue>150000</AnnualRevenue><BankName>Primary International</BankName><BusinessType>OS</BusinessType><YearOpened>1974</YearOpened><Specialty>Road</Specialty><SquareFeet>38000</SquareFeet><Brands>3</Brands><Internet>DSL</Internet><NumberEmployees>40</NumberEmployees></StoreSurvey></Demographics></Sales.Store>  
  
SqlConnection closed.  
```  
  
> [!NOTE]  
>  Mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** -Datentyp-Unterstützung, können Sie fordern, dass das Ergebnis einer FOR XML-Abfrage nicht als typisierte Zeichenfolgen- oder Imagedaten zurückgegeben wird, sondern als **xml** -Datentyp. Dazu müssen Sie die [TYPE-Direktive](../../relational-databases/xml/type-directive-in-for-xml-queries.md)angeben. Wenn die TYPE-Direktive in FOR XML-Abfragen verwendet wird, ermöglicht sie den programmgesteuerten Zugriff auf die FOR XML-Ergebnisse, wie das auch in [Verwenden von XML-Daten in Anwendungen](../../relational-databases/xml/use-xml-data-in-applications.md)gezeigt wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
