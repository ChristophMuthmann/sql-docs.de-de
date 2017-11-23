---
title: "Beibehalten von Datensätzen im XML-Format | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 719d6d0575f90f3460de6e8b1285b6a59cf7f791
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="persisting-records-in-xml-format"></a>Beibehalten von Datensätzen im XML-Format
Wie beim ADTG **Recordset** Persistenz im XML-Format ist mit der Microsoft OLE DB-Anbieter für Persistenz implementiert. Dieser Anbieter generiert einen Vorwärtscursor, schreibgeschützte Rowset aus einer gespeicherten XML-Datei oder einem Stream, die die Schemainformationen von ADO generierten enthält. Auf ähnliche Weise kann es dauern, eine ADO **Recordset**, Generieren von XML, und speichern Sie sie in einer Datei oder jedes Objekt, das die COM implementiert **IStream** Schnittstelle. (Eine Datei ist sogar noch ein weiteres Beispiel für ein Objekt, das unterstützt **IStream**.) Für Version 2.5 und höher, ADO basiert auf Microsoft XML Parser (MSXML) beim Laden der XML-Daten in der **Recordset**; daher msxml.dll ist erforderlich.  
  
> [!NOTE]
>  Einige Einschränkungen gelten beim Speichern der hierarchischen **Recordsets** (Daten-Shapes) in XML-Format. Sie können in XML speichern, wenn die hierarchische **Recordset** enthält ausstehende Updates, und Sie können nicht gespeichert werden eine parametrisierte hierarchische **Recordset**. Weitere Informationen finden Sie unter [beibehalten gefiltert und hierarchische Recordsets](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md).  
  
 Die einfachste Möglichkeit zum Beibehalten von Daten in XML, und Laden es wieder wieder über ADO ist mit der **speichern** und **öffnen** Methoden bzw.. Im folgenden Codebeispiel wird für ADO veranschaulicht, wie die Daten in der **Titel** Tabelle in eine Datei mit dem Namen titles.sav.  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 ADO behält immer die gesamte **Recordset** Objekt. Wenn Sie eine Teilmenge von Zeilen beibehalten möchten die **Recordset** -Objekts die **Filter** Methode, um die Zeilen eingrenzen oder ändern Sie Ihre Auswahlklausel. Allerdings müssen Sie öffnen ein **Recordset** Objekt mit einem clientseitigen Cursor (**CursorLocation** = **AdUseClient**) verwenden die **Filtern** Methode für eine Teilmenge von Zeilen zu speichern. Z. B. zum Abrufen von Titeln, die mit dem Buchstaben "b" beginnen, Sie können einen Filter anwenden auf ein offenes **Recordset** Objekt:  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO verwendet immer das Client-Cursormoduls Rowset einen bildlauffähigen erzeugt bookmarkable **Recordset** Objekt oben auf der Persistenz-Provider generierten vorwärts-Daten.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [XML Persistence Format (XML-Beibehaltungsformat)](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [Namespaces](../../../ado/guide/data/namespaces.md)  
  
-   [Schema-Abschnitt](../../../ado/guide/data/schema-section.md)  
  
-   [Datenabschnitt](../../../ado/guide/data/data-section.md)  
  
-   [Hierarchische Recordsets im XML-Format](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [Recordset Dynamic Properties in XML (Dynamische Recordset-Eigenschaften in XML)](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [XSLT-Transformationen](../../../ado/guide/data/xslt-transformations.md)  
  
-   [Saving to the XML DOM Object (Speichern in das XML DOM-Objekts)](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [XML-Sicherheitsüberlegungen](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [Speicherszenario für XML-Recordsets](../../../ado/guide/data/xml-recordset-persistence-scenario.md)
