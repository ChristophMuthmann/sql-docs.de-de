---
title: Abrufen von Resultsets in Streams | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc99c234d810aef48f4c01bdc83229e55d9c5886
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-resultsets-into-streams"></a>Abrufen von Resultsets in Streams
Anstatt das Empfangen von Ergebnissen in der herkömmlichen **Recordset** -Objekt ADO kann stattdessen Abfrageergebnisse in einen Stream abzurufen. Das ADO **Stream** Objekt (oder andere Objekte, die die COM unterstützt **IStream** Benutzeroberfläche, z. B. die ASP **anfordern** und **Antwort** Objekte ) kann verwendet werden, um diese Ergebnisse enthalten. Eine Verwendung für diese Funktion wird zum Abrufen von Ergebnissen im XML-Format. Mit SQL Server können z. B. XML-Ergebnisse auf verschiedene Weise, wie z. B. mithilfe der FOR XML-Klausel mit einer SQL SELECT-Abfrage oder eine XPath-Abfrage zurückgegeben.  
  
 Zum Empfangen von Abfrageergebnissen im Stream-Format statt in einer **Recordset**, müssen Sie angeben der **AdExecuteStream** aus Konstanten **ExecuteOptionEnum** als Parameter für die **Execute** Methode von einer **Befehl** Objekt. Wenn Ihr Anbieter diese Funktion unterstützt, werden die Ergebnisse in einem Stream bei der Ausführung zurückgegeben. Sie ist möglicherweise erforderlich, um zusätzliche anbieterspezifische Eigenschaften angeben, bevor der Code ausgeführt wird. Z. B. mit der Microsoft OLE DB-Anbieter für SQL Server, Eigenschaften, z. B. **Ausgabestream** in der **Eigenschaften** Auflistung von der **Befehl** Objekt sein muss angegeben. Weitere Informationen zu SQL Server-spezifische dynamische Eigenschaften, die im Zusammenhang mit diesem Feature finden Sie unter XML-Related Eigenschaften in der SQL Server-Onlinedokumentation.  
  
## <a name="for-xml-query-example"></a>XML-BEISPIELABFRAGE  
 Im folgende Beispiel wird mit der Datenbank Northwind in VBScript geschrieben:  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
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
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
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
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
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
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
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
  
 Die FOR XML-Klausel weist SQL Server, um Daten in Form eines XML-Dokuments zurückzugeben.  
  
### <a name="for-xml-syntax"></a>XML-Syntax  
  
```  
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 FÜR XML RAW generische Zeilenelemente, die Spaltenwerte als Attribute aufweisen generiert. FOR XML AUTO verwendet Heuristik, um eine hierarchische Struktur mit Elementnamen, die basierend auf den Tabellennamen zu generieren. FOR XML EXPLICIT generiert eine universelle Tabelle mit Beziehungen, die vollständig von den Metadaten beschrieben.  
  
 Beispielsweise SQL SELECT FOR XML-Anweisung wie folgt:  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 Der Befehl kann in einer Zeichenfolge angegeben werden, vorher gezeigten, zugewiesen an **CommandText**, oder in Form einer XML-Vorlage Abfrage zugewiesen **CommandStream**. Weitere Informationen zu XML-Vorlageabfragen, finden Sie unter [Befehl Streams](../../../ado/guide/data/command-streams.md) in ADO oder Using-Streams für die Eingabe des Befehls in der SQL Server-Onlinedokumentation.  
  
 Die FOR XML-Abfrage wird als eine XML-Vorlage Abfrage wie folgt angezeigt:  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 In diesem Beispiel wird die ASP **Antwort** -Objekt für die **Ausgabestream** Eigenschaft:  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 Geben Sie als Nächstes **AdExecuteStream** Parameter **Execute**. In diesem Beispiel dient als Wrapper für den Datenstrom im XML-Tags, um eine XML-Dateninsel zu erstellen:  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>Hinweise  
 An diesem Punkt XML wurde an den Clientbrowser gestreamt wurde und es kann angezeigt werden. Dies erfolgt mithilfe einer clientseitigen VBScript zum Binden von XML-Dokument an eine Instanz des DOM und Schleifendurchlauf durch jeden untergeordneten Knoten, um eine Liste der Produkte im HTML-Format erstellen.
