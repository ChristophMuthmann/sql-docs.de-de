---
title: "Erweiterte Feldeigenschaften für eine Analysis Services-Datenbank (SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d3cd894cfb7466ae39ac921b8b3405da6c2e77a3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Erweiterte Feldeigenschaften für eine Analysis Services-Datenbank (SSRS)
  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenverarbeitungserweiterung unterstützt erweiterte Feldeigenschaften. Erweiterte Feldeigenschaften sind zusätzlich zu den für die Datenquelle verfügbaren und von der Datenverarbeitungserweiterung unterstützten Feldeigenschaften **Value** und **IsMissing** vorhanden. Erweiterte Eigenschaften werden im Berichtsdatenbereich nicht als Teil der Feldauflistung für ein Berichtsdataset angezeigt. Sie können erweiterte Feldeigenschaftswerte in den Bericht einbeziehen, indem Sie Ausdrücke schreiben, die deren Namen in der integrierten **Fields** -Sammlung angeben.  
  
 Erweiterte Eigenschaften umfassen vordefinierte Eigenschaften und benutzerdefinierte Eigenschaften. Vordefinierte Eigenschaften werden für mehrere Datenquellen gemeinsam verwendet und bestimmten Feldeigenschaftsnamen zugeordnet. Sie sind über die integrierte **Fields** -Sammlung nach Namen verfügbar. Benutzerdefinierte Eigenschaften werden spezifisch für jeden Datenanbieter definiert. Auf diese Eigenschaften kann über die integrierte **Fields** -Sammlung nur mithilfe von Syntax zugegriffen werden, in der der erweiterte Eigenschaftsname als Zeichenfolge verwendet wird.  
  
 Wenn Sie die Abfrage mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -MDX-Abfrage-Designer im grafischen Modus definieren, wird der MDX-Abfrage automatisch ein vordefinierter Satz von Zelleneigenschaften und Dimensionseigenschaften hinzugefügt. Sie können nur erweiterte Eigenschaften verwenden, die in der MDX-Abfrage im Bericht explizit aufgeführt werden. Je nach Bericht möchten Sie möglicherweise den MDX-Standardbefehlstext so ändern, dass weitere im Cube definierte Dimensions- oder benutzerdefinierte Eigenschaften aufgenommen werden. Weitere Informationen über erweiterte Felder in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenquellen, finden Sie unter [Erstellen und Verwenden von Eigenschaftswerten (MDX)](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2).  
  
## <a name="working-with-field-properties-in-a-report"></a>Arbeiten mit Feldeigenschaften in einem Bericht  
 Zu erweiterten Feldeigenschaften zählen vordefinierte Eigenschaften und datenanbieterspezifische Eigenschaften. Feldeigenschaften werden nicht in der Feldliste im **Berichtsdatenbereich** angezeigt, obwohl sie in der für ein Dataset erstellten Abfrage vorhanden sind. Deshalb können Sie keine Feldeigenschaften in Ihre Berichtsentwurfsoberfläche ziehen. Stattdessen ziehen Sie das Feld in den Bericht und ändern anschließend die **Value** -Eigenschaft des Felds in die gewünschte Eigenschaft. Wenn z.B. die Zelldaten aus einem Cube bereits formatiert sind, können Sie die FormattedValue-Feldeigenschaft mithilfe des folgenden Ausdrucks verwenden: `=Fields!FieldName.FormattedValue`.  
  
 Verwenden Sie die folgende Syntax in einem Ausdruck, um auf eine erweiterte Eigenschaft zu verweisen, die nicht vordefiniert ist:  
  
-   *Fields!FieldName("PropertyName")*  
  
## <a name="predefined-field-properties"></a>Vordefinierte Feldeigenschaften  
 Vordefinierte Feldeigenschaften werden in den meisten Fällen auf Measures, Ebenen oder Dimensionen angewendet. Für eine vordefinierte Feldeigenschaft muss ein entsprechender Wert in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle gespeichert sein. Wenn kein Wert vorhanden ist, oder wenn Sie z. B. eine nur Measure-bezogene Feldeigenschaft auf einer Ebene angeben, gibt die Eigenschaft einen NULL-Wert zurück.  
  
 Sie können jede der folgenden Syntaxangaben verwenden, um aus einem Ausdruck auf eine vordefinierte Eigenschaft zu verweisen:  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 In der folgenden Tabelle wird eine Liste der zur Verfügung stehenden vordefinierten Feldeigenschaften bereitgestellt.  
  
|**Eigenschaft**|**Typ**|**Beschreibung oder erwarteter Wert**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**Objekt**|Gibt den Datenwert des Felds an.|  
|**IsMissing**|**Boolean**|Gibt an, ob das Feld im resultierenden Dataset gefunden wurde.|  
|**UniqueName**|**String**|Gibt den vollqualifizierten Namen einer Ebene zurück. Der **UniqueName**-Wert für einen Mitarbeiter könnte z.B. wie folgt lauten: *[Employee].[Employee Department].[Department].&[Sales].&[North American Sales Manager].&[272]*|  
|**BackgroundColor**|**String**|Gibt die Hintergrundfarbe zurück, die in der Datenbank für das Feld definiert ist.|  
|**Farbe**|**String**|Gibt die Vordergrundfarbe zurück, die in der Datenbank für das Element definiert ist.|  
|**FontFamily**|**String**|Gibt den Namen der Schriftart an, die in der Datenbank für das Element definiert ist.|  
|**FontSize**|**String**|Gibt den Schriftgrad an, der in der Datenbank für das Element definiert ist.|  
|**Schriftbreite**|**String**|Gibt die Schriftbreite an, die in der Datenbank für das Element definiert ist.|  
|**FontStyle**|**String**|Gibt den Schriftschnitt an, der in der Datenbank für das Element definiert ist.|  
|**TextDecoration**|**String**|Gibt spezielle Textformatierungen zurück, die in der Datenbank für das Element definiert sind.|  
|**FormattedValue**|**String**|Gibt einen formatierten Wert für ein Measure oder eine Kennzahl zurück. Die **FormattedValue** -Eigenschaft für **Verkaufsquote** gibt beispielsweise ein Währungsformat wie 1.124.400,00 € zurück.|  
|**Key**|**Objekt**|Gibt den Schlüssel für eine Ebene zurück.|  
|**LevelNumber**|**Integer**|Gibt bei Über-/Unterordnungshierarchien die Nummer der Ebene oder Dimension zurück.|  
|**ParentUniqueName**|**String**|Gibt bei Über-/Unterordnungshierarchien einen vollqualifizierten Namen der übergeordneten Ebene zurück.|  
  
> [!NOTE]  
>  Für diese erweiterten Feldeigenschaften sind nur Werte vorhanden, wenn diese Werte beim Ausführen des Berichts und Abrufen der Daten für die Datasets von der Datenquelle (z.B. dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Cube) bereitgestellt werden. Sie können anschließend von einem beliebigen Ausdruck aus mithilfe der im folgenden Abschnitt erläuterten Syntax auf diese Feldeigenschaftswerte verweisen. Da diese Felder nur für diesen Datenanbieter vorhanden sind, werden jedoch Änderungen, die Sie an diesen Werten vornehmen, nicht mit der Berichtsdefinition gespeichert.  
  
### <a name="example-extended-properties"></a>Beispiele für erweiterte Eigenschaften  
 Zur Veranschaulichung erweiterter Eigenschaften enthalten die folgende MDX-Abfrage und das Resultset mehrere Elementeigenschaften, die von einem für einen Cube definierten Dimensionsattribut verfügbar sind. Dabei handelt es sich um die Elementeigenschaften MEMBER_CAPTION, UNIQUENAME, Properties("Day Name"), MEMBER_VALUE, PARENT_UNIQUE_NAME und MEMBER_KEY.  
  
 Diese MDX-Abfrage wird für den [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Cube in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -DW-Datenbank ausgeführt, die mit den [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Beispieldatenbanken geliefert wurde.  
  
```  
WITH MEMBER [Measures].[DateCaption]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_CAPTION'   
   MEMBER [Measures].[DateUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.UNIQUENAME'   
   MEMBER [Measures].[DateDayName]   
      AS '[Date].[Date].Properties("Day Name")'   
   MEMBER [Measures].[DateValueinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_VALUE'   
   MEMBER [Measures].[DateParentUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.PARENT_UNIQUE_NAME'   
   MEMBER [Measures].[DateMemberKeyinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_KEY'   
SELECT {  
   [Measures].[DateCaption],   
   [Measures].[DateUniqueName],   
   [Measures].[DateDayName],   
   [Measures].[DateValueinOriginalDatatype],  
   [Measures].[DateParentUniqueName],  
   [Measures].[DateMemberKeyinOriginalDatatype]  
   } ON COLUMNS , [Date].[Date].ALLMEMBERS ON ROWS   
FROM [Adventure Works]  
  
```  
  
 Wenn Sie diese Abfrage in einem MDX-Abfragebereich ausführen, erhalten Sie ein Resultset mit 1158 Zeilen. Die ersten vier Zeilen sind in der nachfolgenden Tabelle angegeben.  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|All Periods|[Date].[Date].[All Periods]|(null)|(null)|(null)|0|  
|1-Jul-01|[Date].[Date].&[1]|Sonntag|7/1/2001|[Date].[Date].[All Periods]|1|  
|2-Jul-01|[Date].[Date].&[2]|Montag|7/2/2001|[Date].[Date].[All Periods]|2|  
|3-Jul-01|[Date].[Date].&[3]|Dienstag|7/3/2001|[Date].[Date].[All Periods]|3|  
  
 Im grafischen Modus des MDX-Abfrage-Designers erstellte MDX-Standardabfragen enthalten nur die Dimensionseigenschaften MEMBER_CAPTION und UNIQUENAME. In der Standardeinstellung sind diese Werte stets vom Datentyp **String**.  
  
 Wenn Sie eine Elementeigenschaft im ursprünglichen Datentyp benötigen, können Sie die zusätzliche Eigenschaft MEMBER_VALUE einbeziehen, indem Sie die MDX-Standardanweisung im textbasierten Abfrage-Designer ändern. In der folgenden einfachen MDX-Anweisung wurde MEMBER_VALUE der Liste der abzurufenden Dimensionseigenschaften hinzugefügt.  
  
```  
SELECT NON EMPTY {[Measures].[Order Count]} ON COLUMNS,   
NON EMPTY { ([Date].[Month of Year].[Month of Year] ) }   
DIMENSION PROPERTIES   
   MEMBER_CAPTION, MEMBER_UNIQUE_NAME, MEMBER_VALUE ON ROWS   
FROM [Adventure Works]  
CELL PROPERTIES   
   VALUE, BACK_COLOR, FORE_COLOR,   
   FORMATTED_VALUE, FORMAT_STRING,   
   FONT_NAME, FONT_SIZE, FONT_FLAGS  
```  
  
 Die folgende Tabelle enthält die ersten vier Zeilen des Ergebnisses im MDX-Ergebnisbereich.  
  
|Monat|Anzahl Bestellungen|  
|-------------------|-----------------|  
|January|2,481|  
|Februar|2,684|  
|March|2,749|  
|April|2,739|  
  
 Obwohl die Eigenschaften Teil der MDX-Select-Anweisung sind, werden sie nicht in den Spalten des Resultsets angezeigt. Die Daten sind jedoch für einen Bericht verfügbar und können mit der Funktion für erweiterte Eigenschaften angezeigt werden. Doppelklicken Sie in einem MDX-Abfrageergebnisbereich in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]auf die Zelle, um die Zelleigenschaftswerte anzuzeigen (sofern diese Werte im Cube festgelegt sind). Wenn Sie auf die erste Zelle "Anzahl Bestellungen" mit dem Wert 1.379 klicken, wird ein Popupfenster mit den folgenden Zelleigenschaften angezeigt:  
  
|Eigenschaft|Value|  
|--------------|-----------|  
|CellOrdinal|0|  
|Value|2481|  
|BACK_COLOR|(null)|  
|FORE_COLOR|(null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(null)|  
|FONT_SIZE|(null)|  
|FONT_FLAGS|(null)|  
  
 Wenn Sie mit dieser Abfrage ein Berichtsdataset erstellen und dieses an eine Tabelle binden, können Sie die VALUE-Standardeigenschaft für ein Feld anzeigen, z. B. `=Fields!Month_of_Year!Value`. Wenn Sie diesen Ausdruck als Sortierausdruck für die Tabelle festgelegt haben, wird die Tabelle im Ergebnis alphabetisch nach Monat sortiert, da das Value-Feld den Datentyp **String** annimmt. Wenn die Tabelle in der Reihenfolge der Monate im Jahr sortiert werden soll, d. h. Januar zuerst und Dezember zuletzt, verwenden Sie den folgenden Ausdruck:  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 Mit diesem Ausdruck werden die Werte im Feld entsprechend ihres ursprünglichen Datentyps in der Datenquelle sortiert.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Integrierte Sammlungen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Datasetfelder-Sammlung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
