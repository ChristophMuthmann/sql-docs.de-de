---
title: Verwenden von XML-Schemas mit | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XML [SMO]
ms.assetid: 9d04de01-efeb-4b2d-8c28-3234bc7ff2f3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c9aac631cff5fa3ef253721c7677f9f31f71180
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="using-xml-schemas"></a>Verwenden von XML-Schemas
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Die XML-Programmierung in SMO ist auf die Bereitstellung von XML-Datentypen, XML-Namespaces und eine einfache Indizierung für XML-Datentypspalten beschränkt.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stellt systemeigenen Speicher für XML-Dokumentinstanzen bereit. Über XML-Schemas können Sie komplexe XML-Datentypen definieren, die für die Validierung von XML-Dokumenten verwendet werden können, um die Datenintegrität sicherzustellen. Das XML-Schema wird im <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>-Objekt definiert.  
  
## <a name="example"></a>Beispiel  
 Zum Verwenden eines angegebenen Codebeispiels müssen Sie die Programmierumgebung, Programmiervorlage und die zu verwendende Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-an-xml-schema-in-visual-basic"></a>Erstellen eines XML-Schemas in Visual Basic  
 In diesem Codebeispiel wird veranschaulicht, wie zum Erstellen eines XML-Schemas mit der <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> Objekt. Die <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>-Eigenschaft, die die XML-Schemaauflistung definiert, enthält mehrere doppelte Anführungszeichen. Diese werden durch die `chr(34)` -Zeichenfolge ersetzt.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define an XmlSchemaCollection object by supplying the parent database and name arguments in the constructor.
Dim xsc As XmlSchemaCollection
xsc = New XmlSchemaCollection(db, "MySampleCollection")
xsc.Text = "\<schema xmlns=" + Chr(34) + "http://www.w3.org/2001/XMLSchema" + Chr(34) + "  xmlns:ns=" + Chr(34) + "http://ns" + Chr(34) + ">\<element name=" + Chr(34) + "e" + Chr(34) + " type=" + Chr(34) + "dateTime" + Chr(34) + "/></schema>"
'Create the XML schema collection on the instance of SQL Server.
xsc.Create()
```
  
## <a name="creating-an-xml-schema-in-visual-c"></a>Erstellen eines XML-Schemas in Visual C#  
 In diesem Codebeispiel wird veranschaulicht, wie zum Erstellen eines XML-Schemas mit der <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> Objekt. Die <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>-Eigenschaft, die die XML-Schemaauflistung definiert, enthält mehrere doppelte Anführungszeichen. Diese werden durch die `chr(34)` -Zeichenfolge ersetzt.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = default(Server);  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define an XmlSchemaCollection object by supplying the parent  
            // database and name arguments in the constructor.   
            XmlSchemaCollection xsc = default(XmlSchemaCollection);  
            xsc = new XmlSchemaCollection(db, "MySampleCollection");  
            xsc.Text = "\<schema xmlns=" + Strings.Chr(34) + "http://www.w3.org/2001/XMLSchema" + Strings.Chr(34) + " xmlns:ns=" + Strings.Chr(34) + "http://ns" + Strings.Chr(34) + ">\<element name=" + Strings.Chr(34) + "e" + Strings.Chr(34) + " type=" + Strings.Chr(34) + "dateTime" + Strings.Chr(34) + "/></schema>";  
            //Create the XML schema collection on the instance of SQL Server.   
            xsc.Create();  
        }  
```  
  
## <a name="creating-an-xml-schema-in-powershell"></a>Erstellen eines XML-Schemas in PowerShell  
 In diesem Codebeispiel wird veranschaulicht, wie zum Erstellen eines XML-Schemas mit der <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> Objekt. Die <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>-Eigenschaft, die die XML-Schemaauflistung definiert, enthält mehrere doppelte Anführungszeichen. Diese werden durch die `chr(34)` -Zeichenfolge ersetzt.  
  
```powershell   
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalHost  
$srv = get-item default  
  
#Reference the AdventureWorks database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a new schema collection  
$xsc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.XmlSchemaCollection `  
-argumentlist $db,"MySampleCollection"  
  
#Add the xml  
$dq = '"' # the double quote character  
$xsc.Text = "<schema xmlns=" + $dq + "http://www.w3.org/2001/XMLSchema" + $dq + `  
"  xmlns:ns=" + $dq + "http://ns" + $dq + "><element name=" + $dq + "e" + $dq +`  
 " type=" + $dq + "dateTime" + $dq + "/></schema>"  
  
#Create the XML schema collection on the instance of SQL Server.  
$xsc.Create()  
```  
  
  
