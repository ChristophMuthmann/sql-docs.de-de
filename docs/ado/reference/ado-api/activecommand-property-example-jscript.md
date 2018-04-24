---
title: Beispiel für ActiveCommand-Eigenschaft (JScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- ActiveCommand property [ADO], JScript example
ms.assetid: be09e2af-ba31-4168-8ccd-2461bb24e49a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aec3a3d79de42a38b4282014b193c2784e5d543a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="activecommand-property-example-jscript"></a>Beispiel für ActiveCommand-Eigenschaft (JScript)
Dieses Beispiel zeigt die [ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md) Eigenschaft. Ausschneiden und fügen Sie den folgenden Code in Editor oder einem anderen Texteditor und speichern Sie diese als **ActiveCommandJS.asp**.  
  
```  
<!-- BeginActiveCommandJS -->  
<%@LANGUAGE="JScript" %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<%  
    // user input  
    strName = new String(Request.Form("ContactName"))  
%>  
  
<html>  
  
<head>  
<title>ActiveCommand Property Example (JScript)</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
-->  
</style>  
</head>  
  
<body bgcolor="White">  
  
<h1>ActiveCommand Property Example (JScript)</h1>  
  
<%  
if (strName.length > 0)  
    {  
        // connection and recordset variables  
        var Cnxn = Server.CreateObject("ADODB.Connection")  
        var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
        var cmdContact = Server.CreateObject("ADODB.Command");  
        var rsContact = Server.CreateObject("ADODB.Recordset");  
        // display variables  
        var strMessage;  
  
        try  
        {  
            // open connection  
            Cnxn.Open(strCnxn);  
  
            // Open a recordset using a command object  
            cmdContact.CommandText = "SELECT ContactName FROM Customers WHERE City = ?";  
            cmdContact.ActiveConnection = Cnxn;  
            // create parameter and insert variable value  
            cmdContact.Parameters.Append(cmdContact.CreateParameter("ContactName", adChar, adParamInput, 30, strName));  
  
            rsContact = cmdContact.Execute();  
  
            while(!rsContact.EOF){  
                // start new line  
                strMessage = "<P>";  
  
                // get data  
                strMessage += rsContact("ContactName")  
  
                // end the line  
                strMessage += "</P>";  
  
                // show data  
                Response.Write(strMessage);  
  
                // get next record  
                rsContact.MoveNext;  
            }  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // 'clean up  
            if (rsContact.State == adStateOpen)  
                rsContact.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsContact = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<hr>  
  
<form method="POST" action="ActiveCommandJS.asp">  
  <p align="left">Enter city of customer to find (e.g., Paris): <input type="text" name="ContactName" size="40" value=""></p>  
  <p align="left"><input type="submit" value="Submit" name="B1"><input type="reset" value="Reset" name="B2"></p>  
</form>  
</body>  
  
</html>  
<!-- EndActiveCommandJS -->  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveCommand-Eigenschaft (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
