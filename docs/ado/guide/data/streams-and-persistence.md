---
title: Streams und Persistenz | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4a0a45a32086dc3befd19e720c8d600b6b43adde
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="streams-and-persistence"></a>Streams und Persistenz
Die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt [speichern](../../../ado/reference/ado-api/save-method.md) Methode speichert, oder *weiterhin*, eine **Recordset** in einer Datei und die [Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md)Methode Wiederherstellungen der **Recordset** aus dieser Datei.  
  
 Mit ADO 2.7 oder höher die **speichern** und **öffnen** Methoden erhalten bleiben können eine **Recordset** auf eine [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt ebenfalls. Diese Funktion ist besonders nützlich, bei der Arbeit mit Remote Data Service (RDS) und Active Server Pages (ASP).  
  
 Weitere Informationen, wie die Persistenz von sich selbst auf ASP-Seiten verwendet werden kann finden Sie in der aktuellen ASP-Dokumentation.  
  
 Im folgenden sind einige Szenarien, die zeigen, wie **Stream** Objekte und Persistenz können verwendet werden.  
  
## <a name="scenario-1"></a>Szenario 1  
 Dieses Szenario einfach speichert eine **Recordset** in eine Datei, und klicken Sie dann auf eine **Stream**. Dann wird der permanenten Datenstrom geöffnet, in eine andere **Recordset**.  
  
```  
Dim rs1 As ADODB.Recordset  
Dim rs2 As ADODB.Recordset  
Dim stm As ADODB.Stream  
  
Set rs1 = New ADODB.Recordset  
Set rs2 = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
rs1.Open   "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;""", adopenStatic, adLockReadOnly, adCmdText  
rs1.Save "c:\myfolder\mysubfolder\myrs.xml", adPersistXML  
rs1.Save stm, adPersistXML  
rs2.Open stm  
```  
  
## <a name="scenario-2"></a>Szenario 2  
 Dieses Szenario weiterhin eine **Recordset** in einer **Stream** im XML-Format. Anschließend liest der **Stream** in eine Zeichenfolge, die Sie untersuchen, bearbeiten oder anzeigen können.  
  
```  
Dim rs As ADODB.Recordset  
Dim stm As ADODB.Stream  
Dim strRst As String  
  
Set rs = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
' Open, save, and close the recordset.   
rs.Open "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
rs.Save stm, adPersistXML  
rs.Close  
Set rs = nothing  
  
' Put saved Recordset into a string variable.  
strRst = stm.ReadText(adReadAll)  
  
' Examine, manipulate, or display the XML data.  
...  
```  
  
## <a name="scenario-3"></a>Szenario 3  
 Dieser Beispielcode zeigt ASP Code beibehalten einer **Recordset** als XML direkt auf die **Antwort** Objekt:  
  
```  
...  
<%  
response.ContentType = "text/xml"  
  
' Create and open a Recordset.  
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select * from Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
  
' Save Recordset directly into output stream.  
rs.Save Response, adPersistXML   
  
' Close Recordset.  
rs.Close  
Set rs = nothing  
%>  
...  
```  
  
## <a name="scenario-4"></a>Szenario 4  
 In diesem Szenario ASP-Code schreibt den Inhalt der **Recordset** ADTG-Format an den Client. Die [Microsoft Cursor Service für OLE DB-](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) können diese Daten zum Erstellen einer nicht verbundenen **Recordset**.  
  
 Eine neue Eigenschaft für den RDS [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md), [URL](../../../ado/reference/rds-api/url-property-rds.md), verweist auf die ASP-Seite, die generiert die **Recordset**. Dies bedeutet, dass eine **Recordset** -Objekt abgerufen werden kann ohne RDS mithilfe der serverseitigen [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt oder der Benutzer, die beim Schreiben eines Geschäftsobjekts sein. Dadurch wird das RDS-Programmiermodell erheblich vereinfacht.  
  
 Serverseitiger Code, mit dem Namen http://server/directory/recordset.asp:  
  
```  
<%  
Dim rs   
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select au_fname, au_lname, phone from Authors", ""& _  
        "Provider=sqloledb;Data Source=MyServer;" & _  
        "Initial Catalog=Pubs;Integrated Security=SSPI;"  
response.ContentType = "multipart/mixed"  
rs.Save response, adPersistADTG  
%>  
```  
  
 Clientseitiger Code:  
  
```  
<HTML>  
<HEAD>  
<TITLE>RDS Query Page</TITLE>  
</HEAD>  
<body>  
<CENTER>  
<H1>Remote Data Service 2.5</H1>  
<TABLE DATASRC="#DC1">  
   <TR>   
      <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
      <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
      <TD><SPAN DATAFLD="phone"></SPAN></TD>  
   </TR>  
</TABLE>  
<BR>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
    ID=DC1 HEIGHT=1 WIDTH = 1>  
    <PARAM NAME="URL" VALUE="http://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 Entwickler haben auch die Möglichkeit der Verwendung einer **Recordset** Objekt auf dem Client:  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "http://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Record Object (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save-Methode](../../../ado/reference/ado-api/save-method.md)
