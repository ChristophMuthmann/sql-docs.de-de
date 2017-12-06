---
title: Berichtsdefinitionssprache (Report Definition Language, RDL) (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Reporting Services, RDL
- Reporting Services, RDL
- RDL [Reporting Services], about Report Definition Language
- SSRS, RDL
- Report Definition Language, about Report Definition Language
- Report Definition Language
- RDL [Reporting Services]
- reports [Reporting Services], definitions
ms.assetid: b18b025e-f4bd-4744-8f86-0ac9fb967548
caps.latest.revision: "52"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 735811c38ce6073e9dee4dd5b35cf18645a74a3a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="report-definition-language-ssrs"></a>Berichtsdefinitionssprache (Report Definition Language, RDL) (SSRS)
  Bei der Berichtsdefinitionssprache (RDL) handelt es sich um eine XML-Darstellung einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsdefinition. In einer Berichtsdefinition sind Informationen zum Datenabruf und Datenlayout für einen Bericht enthalten. RDL besteht aus XML-Elementen, die der für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]entwickelten XML-Grammatik entsprechen. Sie können eigene benutzerdefinierte Funktionen zur Steuerung von Werten, Formaten und Formatierungen von Berichtselementen hinzufügen, indem Sie in Berichtsdefinitionsdateien auf Code-Assemblys zugreifen.  
  
 RDL fördert die Interoperabilität von kommerziellen Produkten zur Berichterstellung durch die Definition eines allgemeinen Schemas, das den Austausch von Berichtsdefinitionen ermöglicht. Alle Protokolle und alle programmgesteuerten Schnittstellen, die mit XML funktionieren, können mit RDL verwendet werden. RDL ist:  
  
-   ein XML-Schema für Berichtsdefinitionen  
  
-   ein Austauschformat für Unternehmen und Drittanbieter  
  
-   ein erweiterbares und offenes Schema, das zusätzliche Namespaces und benutzerdefinierte Elemente unterstützt  
  
##  <a name="bkmk_RDL_Specifications"></a> RDL-Spezifikationen  
 Informationen zum Herunterladen von Spezifikation für bestimmte Schemaversionen finden Sie im [Thema zum Angeben der Berichtsdefinitionssprache](http://go.microsoft.com/fwlink/?linkid=116865).  
  
##  <a name="bkmk_RDL_XML_Schema_Definition"></a> RDL-XML-Schemadefinition  
 A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -RDL-Datei (Report Definition Language, Berichtsdefinitionssprache) wird mithilfe einer XSD-Datei (XML Schema Definition) überprüft. Das Schema definiert die Regeln dafür, wo RDL-Elemente in einer RDL-Datei auftreten können. Ein Element schließt seinen Datentyp und seine Kardinalität ein, also die Anzahl der erlaubten Vorkommen. Ein Element kann einfach oder komplex sein. Ein einfaches Element besitzt keine untergeordneten Elemente oder Attribute. Ein komplexes Element verfügt über untergeordnete Elemente und (optional) Attribute.  
  
 Das Schema enthält beispielsweise das RDL-Element **ReportParameters**, das den komplexen Typ **ReportParametersType**aufweist. Gemäß der Konvention ist ein komplexer Typ für ein Element der Name des Elements gefolgt von dem Wort **Type**. Ein **ReportParameters** -Element kann im **Report** -Element (einem komplexen Typ) enthalten sein und selbst **ReportParameter** -Elemente enthalten. Ein **ReportParameterType** ist ein einfacher Typ, bei dem es sich nur um einen der folgenden Werte handeln kann: **Boolean**, **DateTime**, **Integer**, **Float**oder **String**. Weitere Informationen zu XML-Schema-Datentypen finden Sie unter [XML Schema Part 2: Datatypes Second Edition](http://go.microsoft.com/fwlink/?linkid=4871).  
  
 Die RDL-XSD steht in der Datei "ReportDefinition.xsd" zur Verfügung, die sich im Ordner "Extras" auf der Produkt-CD-ROM befindet. Sie ist auch auf dem Berichtsserver über die folgende URL verfügbar: `http://servername/reportserver/reportdefinition.xsd`.  
  
##  <a name="bkmk_Creating_RDL"></a> Erstellen einer RDL  
 Da RDL offen und erweiterbar ist, können viele verschiedene Tools und Anwendungen erstellt werden, die RDL auf Basis des entsprechenden XML-Schemas generieren.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bietet mehrere Tools, mit denen Sie RDL-Dateien erstellen können. Weitere Informationen finden Sie unter [Reporting Services-Tools](../../reporting-services/tools/reporting-services-tools.md).  
  
 Eine der einfachsten Möglichkeiten, RDL in einer Anwendung zu generieren, stellt die Verwendung der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Klassen des <xref:System.Xml> -Namespaces und <xref:System.Linq> -Namespaces dar. Insbesondere die **XmlTextWriter** -Klasse eignet sich zum Schreiben von RDL. Mit **XmlTextWriter**können Sie eine vollständige Berichtsdefinition in jeder [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Anwendung von Grund auf erstellen. Entwickler können RDL auch erweitern, indem sie benutzerdefinierte Berichtselemente mit benutzerdefinierten Eigenschaften hinzufügen. Weitere Informationen zur **XmlTextWriter** -Klasse und dem <xref:System.Xml> -Namespace finden Sie im [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Entwicklerhandbuch. Wenn Sie weitere Informationen zu Language Integrated Query (LINQ) benötigen, suchen Sie auf MSDN nach "LINQ to XML".  
  
 Die Standarddateierweiterung für Berichtsdefinitionsdateien ist RDL. Sie können auch Clientberichtsdefinitions-Dateien mit der Erweiterung RDLC entwickeln. Der MIME-Typ für beide Erweiterungen ist text/XML. Weitere Informationen zu Berichte finden Sie unter [Reporting Services-Berichte &#40;SSRS&#41;](../../reporting-services/reports/reporting-services-reports-ssrs.md).  
  
##  <a name="bkmk_RDL_Types"></a> RDL-Typen  
 Die folgenden Tabelle führt die in RDL-Elementen und Attributen verwendete Typen auf.  
  
|Type|Description|  
|----------|-----------------|  
|**Binär (Binary)**|Eine Eigenschaft mit einem Base-64-codierten Binärwert.|  
|**Boolean**|Eine Eigenschaft, die den Wert **true** oder **false** für ein Objekt annehmen kann. Sofern nichts anderes angegeben ist, hat ein nicht angegebenes, optionales Boolean-Objekt den Wert **False**.|  
|**Datum**|Eine Eigenschaft mit einem vollständigen date- oder datetime-Wert, der im ISO8601-Datumsformat angegeben ist: JJJJ-MM-TT[THH:MM[:SS[.S]]]|  
|**Enum**|Eine Eigenschaft mit einem Zeichenfolgen-Textwert, der einem Wert aus einer Liste mit angegebenen Werten entsprechen muss|  
|**Float**|Eine Eigenschaft mit einem Gleitkommawert. Als optionales Dezimaltrennzeichen wird ein Punkt (.) verwendet.|  
|**Integer**|Eine Eigenschaft mit einem ganzzahligen (int32) Wert|  
|**Sprache**|Eine Eigenschaft mit einem Textwert, der einen Sprach- und Kulturcode enthält, z. B. "en-us" für Englisch (USA). Der Wert muss entweder eine bestimmte Sprache oder eine neutrale Sprache angeben, für die eine Standardsprache in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]definiert ist.|  
|**Name**|Eine Eigenschaft mit einem Zeichenfolgen-Textwert Namen müssen innerhalb des Namespaces des Elements eindeutig sein. Ist der Namespace nicht angegeben, entspricht er dem innersten enthaltenden Objekt, das über einen Namen verfügt.|  
|**NormalizedString**|Eine Eigenschaft mit einem Zeichenfolgen-Textwert, der normalisiert wurde|  
|**Größe**|Ein Größenelement muss eine Zahl (mit einem Punkt als optionalem Dezimaltrennzeichen) enthalten. Auf die Zahl muss ein Kennzeichner für eine CSS-Längeneinheit folgen, beispielsweise cm, mm, in, pt oder pc. Ein Leerzeichen zwischen der Zahl und dem Kennzeichner ist optional. Weitere Informationen über Größenkennzeichner finden Sie in [CSS Length Units Reference](http://go.microsoft.com/fwlink/?LinkId=9257).<br /><br /> In RDL beträgt der maximale Wert für **Size** 160 Zoll. Die minimale Größe beträgt 0 Zoll.|  
|**String**|Eine Eigenschaft mit einem Zeichenfolgen-Textwert|  
|**UnsignedInt**|Eine Eigenschaft mit einem ganzzahligen Wert (uint32) ohne Vorzeichen|  
|**Variant**|Eine Eigenschaft mit einem beliebigen einfachen XML-Typ.|  
  
##  <a name="bkmk_RDL_Data_Types"></a> RDL-Datentypen  
 Die DataType-Enumeration definiert den Datentyp eines Attributs, Ausdrucks oder Parameters in RDL. Die folgende Tabelle zeigt die Zuordnung von CLR-Datentypen (Common Language Runtime) zu RDL-Datentypen.  
  
|**CLR-Typ(en)**|**Entsprechender Datentyp**|  
|-----------------------|---------------------------------|  
|Boolean|Boolean|  
|DateTime, DateTimeOffset|DateTime|  
|Int16, Int32, UInt16, Byte, SByte|Integer|  
|Single, Double|Float|  
|String, Char, GUID, Timespan|String|  
  
## <a name="see-also"></a>Siehe auch  
 [Suchen der Berichtsdefinitions-Schemaversion &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)   
 [Verwenden benutzerdefinierter Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Custom Report Items (Benutzerdefinierte Berichtselemente)](../../reporting-services/custom-report-items/custom-report-items.md)  
  
  
