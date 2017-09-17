---
title: Gespeicherte Prozedur Eigenschaften Beispiel (JScript) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- JScript
helpviewer_keywords:
- ActiveConnection property [ADO], JScript example
- CommandText property [ADO], JScript example
- Size property [ADO], JScript example
- Direction property [ADO], JScript example
- CommandTimeout property [ADO], JScript example
ms.assetid: ea74e2a3-c965-43aa-9076-26a084b48ad8
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c975baf653e9cc32432bfec9359ff2caef7dc1c7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="activeconnection-commandtext-commandtimeout-commandtype-size-and-direction-properties-example-jscript"></a>ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (JScript)
Dieses Beispiel verwendet die [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md), [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md), [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md), [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md), [Größe](../../../ado/reference/ado-api/size-property-ado-parameter.md), und [Richtung](../../../ado/reference/ado-api/direction-property.md) Eigenschaften zum Ausführen einer gespeicherten Prozedur. Ausschneiden und fügen Sie den folgenden Code in Editor oder einem anderen Texteditor und speichern Sie diese als **ActiveConnectionJS.asp**.  
  
```  
<!-- BeginActiveConnectionJS -->  
<%@LANGUAGE="JScript"%>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
<head>  
    <title>ActiveConnection, CommandText, CommandTimeout, CommandType, Size, and Direction Properties</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body bgcolor="White">  
  
<%  
    var iRoyalty = parseInt(Request.Form("RoyaltyValue"));  
    // check user input  
  
    if (iRoyalty > -1)  
    {  
            // connection and recordset variables  
        var Cnxn = Server.CreateObject("ADODB.Connection")  
        var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='pubs';Integrated Security='SSPI';";  
        var cmdByRoyalty = Server.CreateObject("ADODB.Command");  
        var rsByRoyalty = Server.CreateObject("ADODB.Recordset");  
        var rsAuthor = Server.CreateObject("ADODB.Recordset");  
        // display variables  
        var filter, strMessage;          
  
        try  
        {  
            // open connection  
            Cnxn.Open(strCnxn);  
  
            cmdByRoyalty.CommandText = "byroyalty";  
            cmdByRoyalty.CommandType = adCmdStoredProc;  
            cmdByRoyalty.CommandTimeOut = 15;  
  
            // The stored procedure called above is as follows:  
                //    CREATE PROCEDURE byroyalty  
                //  @percentage int  
                //    AS  
                //  SELECT au_id from titleauthor  
                //  WHERE titleauthor.royaltyper = @percentage  
                //  GO  
  
            prmByRoyalty = Server.CreateObject("ADODB.Parameter");  
            prmByRoyalty.Type = adInteger;  
            prmByRoyalty.Size = 3;  
            prmByRoyalty.Direction = adParamInput;  
            prmByRoyalty.Value = iRoyalty;  
            cmdByRoyalty.Parameters.Append(prmByRoyalty);  
  
            cmdByRoyalty.ActiveConnection = Cnxn;  
  
            // recordset by Command - Execute  
            rsByRoyalty = cmdByRoyalty.Execute();  
  
            // recordset by Recordset - Open  
            rsAuthor.Open("Authors", Cnxn);  
  
            while (!rsByRoyalty.EOF)  
            {  
                // set filter  
                filter = "au_id='" + rsByRoyalty("au_id")  
                rsAuthor.Filter = filter + "'";  
  
                // start new line  
                strMessage = "<P>";  
  
                // get data  
                strMessage += rsAuthor("au_fname") + " ";   
                strMessage += rsAuthor("au_lname") + " ";  
  
                // end line  
                strMessage += "</P>";  
  
                // show data  
                Response.Write(strMessage);  
  
                // get next record  
                rsByRoyalty.MoveNext;  
            }  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // clean up  
            if (rsByRoyalty.State == adStateOpen)  
                rsByRoyalty.Close;  
            if (rsAuthor.State == adStateOpen)  
                rsAuthor.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsByRoyalty = null;  
            rsAuthor = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<hr>  
  
<form method="POST" action="ActiveConnectionJS.asp">  
  <p align="left">Enter royalty percentage to find (e.g., 40): <input type="text" name="RoyaltyValue" size="5"></p>  
  <p align="left"><input type="submit" value="Submit" name="B1"><input type="reset" value="Reset" name="B2"></p>  
</form>  
  
</body>  
  
</html>  
<!-- EndActiveConnectionJS -->  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveCommand-Eigenschaft (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CommandText-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTimeout-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)   
 [CommandType-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Direction-Eigenschaft](../../../ado/reference/ado-api/direction-property.md)   
 [Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)   
 [Das Datensatzobjekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Eigenschaft "Größe" (ADO-Parameter)](../../../ado/reference/ado-api/size-property-ado-parameter.md)

