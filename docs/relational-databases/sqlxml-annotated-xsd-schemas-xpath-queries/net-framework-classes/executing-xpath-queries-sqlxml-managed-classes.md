---
title: "Ausführen von XPath-Abfragen (verwaltete SQLXML-Klassen) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], SQLXML Managed Classes
- queries [SQLXML], SQLXML Managed Classes
- Managed Classes [SQLXML], executing XPath queries
- mapping schema [SQLXML], XPath queries
- SQLXML Managed Classes, executing XPath queries
ms.assetid: 8bef4c4d-bf0e-4236-a875-fd7d3e058396
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0465bebf92f57739858f3c478fdd7f467ebd3cff
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="executing-xpath-queries-sqlxml-managed-classes"></a>Ausführen von XPath-Abfragen (verwaltete SQLXML-Klassen)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
In diesem Beispiel wird dargestellt, wie XPath-Abfragen für ein Zuordnungsschema ausgeführt werden.  
  
 Betrachten wir das folgende Schema:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Con" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
     <xsd:attribute name="ContactID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Diese C#-Anwendung führt eine XPath-Abfrage für das Schema (MySchema.xml) aus.  
  
> [!NOTE]  
>  Im Code müssen Sie den Namen der Instanz von Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Verbindungszeichenfolge bereitstellen.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
  
      public static int testXPath()  
      {  
         Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandText = "Con";  
         cmd.CommandType = SqlXmlCommandType.XPath;  
         cmd.RootTag = "ROOT";  
         cmd.SchemaPath = "MySchema.xml";  
         strm = cmd.ExecuteStream();  
         using (StreamReader sr = new StreamReader(strm)){  
            Console.WriteLine(sr.ReadToEnd());  
         }  
         return 0;  
      }  
      public static int Main(String[] args)  
      {  
         testXPath();  
         return 0;  
      }  
   }  
```  
  
### <a name="to-test-the-application"></a>So testen Sie die Anwendung  
  
1.  Stellen Sie sicher, dass [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework auf dem Computer installiert ist.  
  
2.  Speichern Sie das oben in diesem Beispiel bereitgestellte XSD-Schema (MySchema.xml) in einem Ordner.  
  
3.  Speichern Sie den C#-Code (DocSample.cs, der bereitgestellt wird), in diesem Beispiel im selben Ordner, in dem das Schema gespeichert ist. (Wenn Sie die Dateien in einem anderen Ordner speichern, müssen Sie den Code bearbeiten und den entsprechenden Verzeichnispfad für das Zuordnungsschema angeben.)  
  
4.  Kompilieren Sie den Code. Verwenden Sie zur Kompilierung des Codes an der Eingabeaufforderung die folgende Zeichenfolge:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Dadurch wird eine ausführbare Datei (DocSample.exe) erstellt.  
  
5.  Führen Sie DocSample.exe an der Eingabeaufforderung aus.  
  
  
