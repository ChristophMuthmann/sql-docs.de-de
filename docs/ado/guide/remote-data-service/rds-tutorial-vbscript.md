---
title: RDS-Lernprogramm (VBScript) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 02/14/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70617ccbb2b0b874c68ea45cc72390bd98a52061
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="rds-tutorial-vbscript"></a>RDS-Lernprogramm (VBScript)
Dies ist die RDS-Lernprogramm, in Microsoft Visual Basic Scripting Edition geschrieben. Eine Beschreibung der Zweck dieses Lernprogramms finden Sie in der [RDS-Lernprogramm](../../../ado/guide/remote-data-service/rds-tutorial.md).  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 In diesem Lernprogramm [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) und [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) zur Entwurfszeit erstellt werden – d. h. sie sind mit Objekttags wie folgt definiert: `<OBJECT>...</OBJECT>`. Sie können alternativ erstellt werden, zur Laufzeit mit der [CreateObject-Methode (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md) Methode. Z. B. die **RDS. DataControl** Objekt wie folgt erstellt werden konnte:  
  
```  
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1--specify-a-server-program"></a>Schritt 1 – Geben Sie ein Serverprogramm  
 VBScript erkennen, der Name des im IIS-Webserver ausgeführt wird auf den Zugriff auf die VBScript **Request.ServerVariables** verfügbare Methode zum Active Server Pages:  
  
```  
"http://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 Für dieses Lernprogramm müssen Sie jedoch verwenden Sie die imaginären Server, "Server".  
  
> [!NOTE]
>  Achten Sie darauf, den Datentyp der **ByRef** Argumente. VBScript können Sie weder den Variablentyp angeben, damit Sie immer übergeben müssen eine **Variant**. Bei Verwendung von HTTP RDS können Sie eine Variante an eine Methode übergeben, die eine nicht-Variante erwartet, wenn Sie ihn mit Aufrufen der **RDS. DataSpace** Objekt [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) Methode. Bei Verwendung von DCOM oder in-Process-Server müssen Sie die Parametertypen an den Client und Server Seiten entsprechen, oder wird die Fehlermeldung "Typkonflikt".  
  
```  
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "http://yourServer")  
```  
  
## <a name="step-2a--invoke-the-server-program-with-rdsdatacontrol"></a>Schritt 2a – Aufrufen des Programms mit RDS. DataControl  
 In diesem Beispiel wird lediglich zur Veranschaulichung, die das Standardverhalten der **RDS. DataControl** kann die angegebene Abfrage ausgeführt werden.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b--invoke-the-server-program-with-rdsserverdatafactory"></a>Schritt 2 b – Aufrufen des Programms mit RDSServer.DataFactory  
  
## <a name="step-3--server-obtains-a-recordset"></a>Schritt 3 – Server ruft die einem Recordset ab.  
  
## <a name="step-4--server-returns-the-recordset"></a>Schritt 4 – Server gibt das Recordset zurück.  
  
```  
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5--datacontrol-is-made-usable-by-visual-controls"></a>Schritt 5 – DataControl verwendbaren durch visuelle Steuerelemente erfolgt  
  
```  
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a--changes-are-sent-to-the-server-with-rdsdatacontrol"></a>Schritt 6a – Änderungen mit RDS an den Server gesendet werden DataControl  
 In diesem Beispiel wird lediglich einen Kommentar veranschaulichen wie das **RDS. DataControl** Updates führt.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b--changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>Schritt 6 b – Änderungen mit RDSServer.DataFactory an den Server gesendet werden  
  
```  
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **Dies ist das Ende des Lernprogramms.**  
  
## <a name="see-also"></a>Siehe auch  
 [RDS-Tutorial](../../../ado/guide/remote-data-service/rds-tutorial.md)   
