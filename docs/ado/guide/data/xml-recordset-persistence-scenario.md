---
title: "Speicherszenario für XML-Recordset | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd47944f218c6cb4d3bea571b27be990c5f7f530
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="xml-recordset-persistence-scenario"></a>Speicherszenario für XML-Recordset
In diesem Szenario erstellen Sie eine Active Server Pages (ASP)-Anwendung, die den Inhalt von einem Recordset-Objekt direkt in die ASP-Response-Objekt speichert.  
  
> [!NOTE]
>  Dieses Szenario erfordert, dass Ihr Server Internet Information Server 5.0 (IIS) oder höher installiert.  
  
 Das zurückgegebene Recordset in Internet Explorer angezeigt wird mithilfe einer [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md).  
  
 Die folgenden Schritte sind erforderlich, dieses Szenario zu erstellen:  
  
-   Einrichten der Anwendung  
  
-   Abrufen von Daten  
  
-   Senden von Daten  
  
-   Empfangen und Anzeigen der Daten  
  
## <a name="step-1-set-up-the-application"></a>Schritt 1: Einrichten der Anwendung  
 Erstellen Sie ein virtuelles IIS-Verzeichnis mit dem Namen "XMLPersist" mit Skriptberechtigungen. Erstellen Sie zwei neue Textdateien im Ordner "auf den das virtuelle Verzeichnis, eine benannte"XMLResponse.asp,"die anderen benannten""default.htm"."zeigt"  
  
## <a name="step-2-get-the-data"></a>Schritt 2: Abrufen der Daten  
 In diesem Schritt schreiben Sie den Code, um ein ADO-Recordset öffnen und Vorbereiten der an den Client zu senden. Öffnen Sie die Datei XMLResponse.asp mit einem Text-Editor wie Notepad, und fügen Sie den folgenden Code.  
  
```  
<%@ language="VBScript" %>  
  
<!-- #include file='adovbs.inc' -->  
  
<%  
  Dim strSQL, strCon  
  Dim adoRec   
  Dim adoCon   
  Dim xmlDoc   
  
  ' You will need to change "MySQLServer" below to the name of the SQL   
  ' server machine to which you want to connect.  
  strCon = "Provider=sqloledb;Data Source=MySQLServer;Initial Catalog=Pubs;Integrated Security=SSPI;"  
  Set adoCon = server.createObject("ADODB.Connection")  
  adoCon.Open strCon  
  
  strSQL = "SELECT Title, Price FROM Titles ORDER BY Price"  
  Set adoRec = Server.CreateObject("ADODB.Recordset")  
  adoRec.Open strSQL, adoCon, adOpenStatic, adLockOptimistic, adCmdText  
```  
  
 Achten Sie darauf, dass Sie zum Ändern des Werts, der die `Data Source` Parameter im `strCon` auf den Namen des Microsoft SQL Server-Computers.  
  
 Behalten Sie die Datei öffnen, und wechseln Sie mit dem nächsten Schritt fort.  
  
## <a name="step-3-send-the-data"></a>Schritt 3: Senden von Daten  
 Nun, da Sie ein Recordset haben, müssen Sie es an den Client senden, durch das Speichern als XML auf der ASP-Response-Objekt. Fügen Sie den folgenden Code am Ende XMLResponse.asp.  
  
```  
  Response.ContentType = "text/xml"  
  Response.Expires = 0  
  Response.Buffer = False  
  
  Response.Write "<?xml version='1.0'?>" & vbNewLine  
  adoRec.save Response, adPersistXML  
  adoRec.Close  
  Set adoRec=Nothing  
%>  
```  
  
 Beachten Sie, dass die ASP-Response-Objekt, als Ziel für das Recordset angegeben wird [Save-Methode](../../../ado/reference/ado-api/save-method.md). Das Ziel die Save-Methode kann jedes Objekt, das die IStream-Schnittstelle, wie z. B. eine ADO unterstützt [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md), oder einen Dateinamen, die den vollständigen Pfad enthält, wird das Recordset gespeichert werden sollen.  
  
 Speichern Sie und schließen Sie XMLResponse.asp, bevor Sie mit dem nächsten Schritt fortfahren. Kopieren Sie außerdem die Datei "adovbs.inc" aus der Standardinstallationsordner für ADO-Bibliothek, im gleichen Ordner, in dem Sie die Datei XMLResponse.asp gespeichert.  
  
## <a name="step-4-receive-and-display-the-data"></a>Schritt 4: Empfangen und Anzeigen der Daten  
 In diesem Schritt erstellen Sie eine HTML-Datei mit einem eingebetteten [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt, das in der Datei XMLResponse.asp abzurufenden das Recordset verweist. Öffnen Sie "default.htm" mit einem Text-Editor wie Notepad, und fügen Sie den folgenden Code hinzu. Ersetzen Sie "Sqlserver" in der URL durch den Namen Ihres Servers.  
  
```  
<HTML>  
<HEAD><TITLE>ADO Recordset Persistence Sample</TITLE></HEAD>  
<BODY>  
  
<TABLE DATASRC="#RDC1" border="1">  
  <TR>  
<TD><SPAN DATAFLD="title"></SPAN></TD>  
<TD><SPAN DATAFLD="price"></SPAN></TD>  
  </TR>  
</TABLE>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="RDC1">  
   <PARAM NAME="URL" VALUE="XMLResponse.asp">  
</OBJECT>  
  
</BODY>  
</HTML>  
```  
  
 Schließen Sie die Datei "default.htm", und speichern Sie sie in den gleichen Ordner, in dem Sie XMLResponse.asp gespeichert. Mithilfe von Internet Explorer 4.0 oder höher, öffnen Sie die URL http://*Sqlserver*/XMLPersist/default.htm und beobachten Sie die Ergebnisse. Die Daten werden in einer gebundenen DHTML-Tabelle angezeigt. Öffnen Sie die URL http:// *Sqlserver* /XMLPersist/XMLResponse.asp und beobachten Sie die Ergebnisse. Der XML-Code wird angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Save-Methode](../../../ado/reference/ado-api/save-method.md)   
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)

