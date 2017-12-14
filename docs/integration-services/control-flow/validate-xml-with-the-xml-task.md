---
title: Validieren von XML-Dokumenten mit dem XML-Task | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML validation
- XML, validating
ms.assetid: 224fc025-c21f-4d43-aa9d-5ffac337f9b0
caps.latest.revision: "9"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 71429997374af75e681da85b0f54588448e8937a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="validate-xml-with-the-xml-task"></a>Validieren von XML-Dokumenten mit dem XML-Task
  Validieren Sie XML-Dokumente und erhalten Sie eine umfangreiche Fehlerausgabe durch die Aktivierung der Eigenschaft **ValidationDetails** des XML-Tasks.  
  
 Die folgende Abbildung zeigt den **XML-Task-Editor** eingestellt für die XML-Validierung mit umfassender Fehlerausgabe.  
  
 ![XML-Taskeigenschaften im XML-Task-Editor](../../integration-services/control-flow/media/xmltaskproperties.jpg "XML-Taskeigenschaften im XML-Task-Editor")  
  
 Bevor die Eigenschaft **ValidationDetails** verfügbar war, gab die XML-Validierung durch den XML-Task nur „true“ oder „false“ als Ergebnis zurück, ohne Informationen zu Fehlern oder wo diese auftraten. Wenn Sie jetzt die Eigenschaft **ValidationDetails** auf TRUE festlegen, enthält die Ausgabedatei ausführliche Informationen zu jedem Fehler, einschließlich der Zeilennummer und der Position. Sie können diese Informationen verwenden, um Fehler in XML-Dokumenten zu verstehen, zu finden und zu beheben.  
  
 Die XML-Validierungsfunktion lässt sich problemlos auch für große XML-Dokumente und eine große Anzahl von Fehlern skalieren. Da die Ausgabedatei selbst im XML-Format ist, können Sie die Ausgabe abfragen und analysieren. Enthält die Ausgabe beispielsweise sehr viele Fehler, so können Sie diese, wie in diesem Thema beschrieben, mit einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage gruppieren.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) führte die Eigenschaft **ValidationDetails** im [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 2 ein. Die Eigenschaft ist auch in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]verfügbar.  
  
## <a name="sample-output-for-xml-thats-valid"></a>Beispielausgabe für eine XML-Datei ohne Fehler  
 Hier ist eine Beispiel-Ausgabedatei mit Validierungsergebnissen für eine gültige XML-Datei.  
  
```xml  
  
<root xmlns:ns="http://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>true</result>  
        <errors>0</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:27:22.087</startTime>  
        <endTime>2015-05-28T10:29:07.007</endTime>  
        <xmlFile>d:\Temp\TestData.xml</xmlFile>  
        <xsdFile>d:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages />  
</root>  
```  
  
## <a name="sample-output-for-xml-thats-not-valid"></a>Beispielausgabe für eine XML-Datei mit Fehlern  
 Hier ist eine Beispiel-Ausgabedatei mit Validierungsergebnissen für eine XML-Datei mit einer geringen Anzahl an Fehlern. Der Text der <error\<-Elemente wurde zur besseren Lesbarkeit umbrochen.  
  
```xml  
  
<root xmlns:ns="http://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>false</result>  
        <errors>2</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:45:09.538</startTime>  
        <endTime>2015-05-28T10:45:09.558</endTime>  
        <xmlFile>C:\Temp\TestData.xml</xmlFile>  
        <xsdFile>C:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages>  
        <error line="5" position="26">The 'ApplicantRole' element is invalid - The value 'wer3' is invalid  
    according to its datatype 'ApplicantRoleType' - The Enumeration constraint failed.</error>  
        <error line="16" position="28">The 'Phone' element is invalid - The value 'we3056666666' is invalid  
     according to its datatype 'phone' - The Pattern constraint failed.</error>  
    </messages>  
</root>  
```  
  
## <a name="analyze-xml-validation-output-with-a-transact-sql-query"></a>Analysieren der XML-Validierungsausgabe mit einer Transact-SQL-Abfrage  
 Wenn die Ausgabe der XML-Validierung sehr viele Fehler enthält, können Sie die Ausgabe mit einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]laden. Danach können Sie die Fehlerliste mit allen Funktionen der Programmiersprache T-SQL, einschließlich WHERE, GROUP BY, ORDER BY, JOIN usw. analysieren.  
  
```sql  
DECLARE @xml XML;  
  
SELECT @xml = XmlDoc     
FROM OPENROWSET (BULK N'C:\Temp\XMLValidation_2016-02-212T10-41-00.xml', SINGLE_BLOB) AS Tab(XmlDoc);  
  
-- Query # 1, flat list of errors  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('http://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT * FROM rs;  
-- WHERE error LIKE ‘%whatever_string%’  
  
-- Query # 2, count of errors grouped by the error message  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('http://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT COALESCE(error,'Total # of errors:') AS [error], COUNT(*) AS [counter]  
FROM rs  
GROUP BY GROUPING SETS ((error), ())  
ORDER BY 2 DESC, COALESCE(error, 'Z');  
  
```  
  
 Hier ist das Ergebnis in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] der zweiten Beispielabfrage aus dem vorangegangenen Text.  
  
 ![Abfrage zum Gruppieren von XML-Fehlern in Management Studio](../../integration-services/control-flow/media/queryforxmlerrors.jpg "Abfrage zum Gruppieren von XML-Fehlern in Management Studio")  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Task](../../integration-services/control-flow/xml-task.md)   
 [Editor für den XML-Task &#40;Seite Allgemein&#41;](../../integration-services/control-flow/xml-task-editor-general-page.md)  
  
  
