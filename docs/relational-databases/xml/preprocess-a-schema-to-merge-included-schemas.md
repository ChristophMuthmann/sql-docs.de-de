---
title: "Vorverarbeiten eines Schemas zum Zusammenführen eingeschlossener Schemas | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- testing preprocessor tool
- xsd:include
- XML schema collections [SQL Server], preprocessor tool
- include element
- XML schemas [SQL Server], preprocessing
- schema collections [SQL Server], preprocessor tool
- preprocessor tool [XML schemas]
- XML schemas [SQL Server]
ms.assetid: cde1de5f-077a-4a6d-8a81-1ecb6e10d549
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb486493743bc51842c0531e1072aa1eac106d76
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="preprocess-a-schema-to-merge-included-schemas"></a>Vorverarbeiten eines Schemas zum Zusammenführen eingeschlossener Schemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Das W3C XSD **include** -Element stellt Unterstützung für Schemamodularität zur Verfügung, in dem ein XML-Schema in mehrere physische Dateien partitioniert werden kann. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt dieses Element zurzeit nicht. XML-Schemas, die dieses Element enthalten, werden vom Server zurückgewiesen.  
  
 Als Lösung können XML-Schemas, die die \<xsd:include>-Direktive enthalten, so vorverarbeitet werden, dass die Inhalte aller enthaltenen Schemas kopiert und in einem einzigen Schema für den Upload auf den Server zusammengeführt werden. Der folgende C#-Code kann für die Vorverarbeitung verwendet werden: Die Kommentare in den einzelnen Codeteilen stellen Informationen zur Verwendung bereit.  
  
```  
// XSD Schema Include Normalizer  
// To compile:   
// csc filename.cs  
//  
// How to use:  
//  
// Arguments: [-q] input.xsd [output.xsd]  
//  
// input.xsd       - file to normalize  
// output.xsd      - file to output, default is console  
// -q              - quiet  
//   
// Example:  
//   
// filename.exe schema.xsd  
//   
using System;  
using System.Xml;  
using System.Xml.Schema;  
using System.IO;  
using System.Collections;  
public class XsdSchemaNormalizer  
{  
    private static bool NormalizeXmlSchema( String url, TextWriter writer )  
    {  
   try {  
       XmlTextReader txtRead = new XmlTextReader( url );  
       XmlSchema sch = XmlSchema.Read( txtRead, null );  
  
       // Compiling Schema  
       sch.Compile(null);  
  
       XmlSchema outSch =   
      XmlSchemaIncludeNormalizer.BuildIncludeFreeXmlSchema( sch);  
  
       outSch.Write( writer );  
   } catch ( Exception e ) {  
       Console.WriteLine(e.ToString());  
       return false;  
   }  
   return true;  
    }  
    public static void usage()  
    {  
   Console.WriteLine("Arguments: [-q] [-v] input.xsd [output.xsd]\n");  
   Console.WriteLine("input.xsd       - file to normalize");  
   Console.WriteLine("output.xsd      - file to output, default is console");  
   Console.WriteLine("-q              - quiet");  
    }  
    public static void Main(String []args)  
    {  
   if( args.GetLength(0) < 1 ) {  
       usage();  
       return;  
   }  
   int argi = 0;  
   bool quiet = false;  
   if( args[argi] == "-q" ) {  
       quiet = true;  
            argi++;  
   }  
  
   if( argi == args.GetLength(0) )  
   {  
       usage();  
       return;  
   }  
  
   String url = args[argi];  
  
   if( !quiet )  
       Console.WriteLine("Loading Schema: " + url);  
  
   if( argi < ( args.GetLength(0) - 1 ) )  
   {  
       if( !quiet )  
      Console.WriteLine("Outputing to file: " + args[argi+1]);  
  
       StreamWriter output =   
      new StreamWriter( new FileStream(args[argi+1], FileMode.Create ));  
  
       NormalizeXmlSchema( url, output);  
   }  
   else   
   {  
       NormalizeXmlSchema( url, Console.Out);  
   }  
  
    }  
}  
  
// A class to remove all <include> from a Xml Schema  
//  
public class XmlSchemaIncludeNormalizer  
{  
    // Takes as input a XmlSchema which has includes in it   
    // and the schema location uri of that XmlSchema  
    //   
    // Returns a "preprocessed" form of XmlSchema without any   
    // includes. It still retains imports though. Also, it does  
    // not propagate unhandled attributes  
    //  
    // It can throw any exception  
    public static XmlSchema BuildIncludeFreeXmlSchema( XmlSchema inSch )  
    {  
   XmlSchema outSch = new XmlSchema();  
  
   AddSchema( outSch, inSch );  
  
   return outSch;  
    }  
  
    // Adds everything in the second schema minus includes to   
    // the first schema  
    //  
    private static void AddSchema( XmlSchema outSch, XmlSchema add)  
    {  
   outSch.AttributeFormDefault = add.AttributeFormDefault;  
   outSch.BlockDefault = add.BlockDefault;  
   outSch.ElementFormDefault = add.ElementFormDefault;  
   outSch.FinalDefault = add.FinalDefault;  
   outSch.Id = add.Id;  
   outSch.TargetNamespace = add.TargetNamespace;  
   outSch.Version = add.Version;  
  
   AddTableToSchema( outSch, add.AttributeGroups );  
   AddTableToSchema( outSch, add.Attributes );  
   AddTableToSchema( outSch, add.Elements );  
   AddTableToSchema( outSch, add.Groups );  
   AddTableToSchema( outSch, add.Notations );  
   AddTableToSchema( outSch, add.SchemaTypes );  
  
   // Handle includes as a special case  
   for( int i = 0; i < add.Includes.Count; i++ )  
   {  
       if( ! ( add.Includes[i] is XmlSchemaInclude) )  
      outSch.Includes.Add( add.Includes[i] );  
   }  
    }  
  
    // Adds all items in the XmlSchemaObjectTable to the specified XmlSchema  
    //  
    private static void AddTableToSchema( XmlSchema outSch,   
                 XmlSchemaObjectTable table )  
    {  
   IDictionaryEnumerator e = table.GetEnumerator();  
  
   while( e.MoveNext() )  
   {  
       outSch.Items.Add( (XmlSchemaObject)e.Value );  
   }  
    }  
}  
```  
  
## <a name="testing-the-preprocessor-tool"></a>Testen des Präprozessortools  
 Sie können die folgenden XSD-Schemas zum Testen des Präprozessortools verwenden.  
  
### <a name="bookscommonxsd"></a>books_common.xsd  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
     xmlns="bookstore-schema"  
     elementFormDefault="qualified" >  
  <xsd:element name="publisher" type="xsd:string"/>  
</xsd:schema>  
```  
  
### <a name="booksxsd"></a>books.xsd  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
     xmlns="bookstore-schema"  
     elementFormDefault="qualified"  
     targetNamespace="bookstore-schema">  
  <xsd:include id="books_common" schemaLocation="books_common.xsd"/>  
  <xsd:element name="bookstore" type="xsd:string" />  
</xsd:schema>  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
