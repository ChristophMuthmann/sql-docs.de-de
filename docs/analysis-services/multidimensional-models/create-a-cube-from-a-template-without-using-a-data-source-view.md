---
title: Erstellen Sie einen Cube ohne Verwendung einer Datenquellensicht aus einer Vorlage | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5c8c09b1-140c-48db-9b9f-d18a051d7dbd
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 80680ae03ee8ac059cfe3c9b47c3abe6b67db511
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-cube-from-a-template-without-using-a-data-source-view"></a>Erstellen eines Cubes aus einer Vorlage, ohne eine Datenquellensicht zu verwenden
  Wählen Sie **Cube ohne eine Datenquelle erstellen** auf der ersten Seite des Cube-Assistenten aus, um einen Cube ohne Verwendung einer Datenquellensicht zu erstellen. Später können Sie das relationale Schema für die Datenquellensicht mit dem Schemagenerierungs-Assistenten auf der Grundlage der Cubestruktur und möglicherweise anderer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte generieren. Weitere Informationen zum Generieren eines Schemas finden Sie unter [Schemagenerierungs-Assistent &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md).  
  
## <a name="selecting-the-build-method"></a>Auswählen der Erstellungsmethode  
 Klicken Sie im Cube-Assistenten auf der Seite **Erstellungsmethode auswählen** auf **Cube ohne eine Datenquelle erstellen**. Um den Cube mithilfe einer vorhandenen Cubevorlage zu erstellen, aktivieren Sie das Kontrollkästchen **Cubevorlage verwenden** . . Wenn Sie sich gegen die Verwendung einer Vorlage entscheiden, müssen Sie die Optionen manuell festlegen.  
  
 In Cubevorlagen sind vordefinierte Measures, Measuregruppen, Dimensionen, Hierarchien und Attribute enthalten. Wenn Sie eine Vorlage auswählen, verwendet der Assistent die Objektdefinitionen in den Vorlagen als Grundlage zum Festlegen der Optionen auf den folgenden Seiten. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] wird mit mehreren Vorlagen für Standardcubes installiert. Der Serveradministrator kann auch Cube- oder Dimensionsvorlagen hinzufügen, die speziell auf die Daten in Ihrem Unternehmen abgestimmt sind.  
  
## <a name="selecting-dimensions"></a>Auswählen von Dimensionen  
 Mithilfe der Seite **Dimensionen auswählen** des Assistenten können Sie dem Cube vorhandene Dimensionen hinzufügen. Diese Seite wird nur angezeigt, wenn im Projekt oder der Datenbank bereits freigegebene Dimensionen ohne eine Datenquelle vorhanden sind. Dimensionen, die über eine Datenquelle verfügen, sind nicht aufgeführt.  
  
 Um vorhandene Dimensionen hinzuzufügen, wählen Sie in der Liste **Gemeinsame Dimensionen** mindestens eine Dimension aus, und klicken Sie auf die Schaltfläche mit dem Pfeil nach rechts (**>**), um sie in die Liste **Cubedimensionen** zu verschieben. Klicken Sie auf die Schaltfläche mit dem Doppelpfeil (**>>**), um alle Dimensionen in der Liste zu verschieben.  
  
## <a name="defining-new-measures"></a>Definieren neuer Measures  
 Verwenden Sie die Seite **Neue Measures definieren** des Assistenten, um die Measures und Measuregruppen im neuen Cube anzugeben. Die hier angegebenen Measuregruppen entsprechen den Faktentabellen im generierten Schema. Die hier angegebenen Measures entsprechen den numerischen Nichtschlüsselspalten in den Tabellen.  
  
 Wenn Sie den Cube auf der Grundlage einer Vorlage erstellen, werden die Measures in der Vorlage unter **Measures aus der Vorlage auswählen**in einem Rasterformat aufgeführt. Die Kontrollkästchen neben den einzelnen Measures in der Liste sind automatisch ausgewählt. Sie können das Kontrollkästchen neben Measures, die nicht in den Cube übernommen werden sollen, deaktivieren. Um alle Measures aus der Liste hinzuzufügen oder zu entfernen, aktivieren oder deaktivieren Sie das Kontrollkästchen auf der Titelleiste des Rasters.  
  
 Sie können dem Cube Measures aus der Liste unter **Neue Measures hinzufügen**hinzufügen. Um ein neues Measure hinzuzufügen, klicken Sie in der Spalte **Measurename** (in der **Neues Measure hinzufügen**angezeigt wird) auf die erste leere Zelle. Geben Sie einen Measurenamen, eine Measuregruppe, einen Datentyp und eine Aggregation für jedes neue Measure an. Um ein Measure aus der Liste **Neue Measures hinzufügen** zu löschen, klicken Sie auf das Löschsymbol (**X**). Wenn Sie keine Vorlage verwenden, ist **Neue Measures hinzufügen** die einzige Liste auf dieser Seite des Assistenten.  
  
 Sowohl das Raster **Measures aus der Vorlage auswählen** als auch das Raster **Neue Measures hinzufügen** enthält Werte in den Spalten, die in der folgenden Tabelle beschrieben sind. Sie können auf einen Wert in einer der Listen klicken, um ihn zu ändern.  
  
|Column|Description|  
|------------|-----------------|  
|**Measurename**|Durch einen Wert in dieser Spalte wird der Name eines im Cube enthaltenen Measures definiert. Klicken Sie auf einen Wert in dieser Spalte, um einen Namen einzugeben. Klicken Sie in dieser Spalte auf **Neues Measure hinzufügen** , um ein neues Measure zu erstellen. In dieser Spalte wird die **Name** -Eigenschaft für das Measureobjekt festgelegt.|  
|**Measuregruppe**|Der Name der Measuregruppe, in der das Measure enthalten ist. Klicken Sie auf diesen Wert, um einen Namen auszuwählen oder einzugeben. Wenn Sie alle Measures löschen, die zu einer bestimmten Measuregruppe gehören, wird die Measuregruppe ebenfalls entfernt. In dieser Spalte wird die **Name** -Eigenschaft für das Measuregruppenobjekt festgelegt.|  
|**Datentyp**|Der Datentyp des Measures. Klicken Sie auf diesen Wert, um den Datentyp zu ändern. Der Standardwert bei der Erstellung eines Measures ist **Single**. In dieser Spalte wird die **DataType** -Eigenschaft für das Measureobjekt festgelegt.|  
|**Aggregation**|Die Standardaggregation des Measures. Klicken Sie auf diese Zelle, um eine der Standardaggregationen für das Measure (oder **keine**) anzugeben. Der Standardwert bei der Erstellung eines Measures ist **Sum**. In dieser Spalte wird die **AggregationFunction** -Eigenschaft für das Measureobjekt festgelegt.|  
  
## <a name="defining-new-dimensions"></a>Definieren neuer Dimensionen  
 Verwenden Sie die Seite **Neue Dimensionen definieren** des Assistenten, um die Dimensionen im neuen Cube anzugeben.  
  
 Wenn Sie den Cube auf der Grundlage einer Vorlage erstellen, werden im Raster unter **Dimensionen aus der Vorlage auswählen** die in der Vorlage enthaltenen Dimensionen aufgelistet. Sie können das Kontrollkästchen neben einer beliebigen Dimension deaktivieren, um sie aus dem Cube zu entfernen. Deaktivieren Sie das Kontrollkästchen auf der Titelleiste des Rasters, um alle aufgeführten Dimensionen zu entfernen. Wenn Sie keine Vorlage verwenden, ist in diesem Raster nur die Time-Dimension aufgeführt.  
  
 Sie können dem Cube im Raster unter **Neue Dimensionen hinzufügen**Dimensionen hinzufügen. Um eine Dimension hinzuzufügen, klicken Sie auf die Zelle in der Spalte **Name** , in der der Text **Neue Dimension hinzufügen**enthalten ist, und geben Sie dann einen Namen für die Dimension ein. Um eine Zeile aus der Liste zu entfernen, klicken Sie auf das Löschsymbol (**X**).  
  
 Sowohl das Raster **Dimensionen aus der Vorlage auswählen** als auch das Raster **Neue Dimensionen hinzufügen** enthält Werte in den Spalten, die in der folgenden Tabelle beschrieben sind. Sie können auf einen Wert in einer der Listen klicken, um ihn zu ändern.  
  
|Column|Description|  
|------------|-----------------|  
|**Typ**|Zeigt den Dimensionstyp einer Vorlagendimension an. Klicken Sie auf diese Zelle, um den Dimensionstyp für eine Dimension zu ändern. In dieser Spalte wird die **Type** -Eigenschaft für das Dimensionsobjekt festgelegt.|  
|**Name**|Zeigt den Namen der Dimension an. Klicken Sie auf diese Zelle, um einen anderen Namen einzugeben. Durch diesen Wert wird die **Name** -Eigenschaft für das Dimensionsobjekt festgelegt.|  
|**SCD**|Gibt an, dass dies eine langsam veränderliche Dimension (Slowly Changing Dimension, SCD) ist. Wenn Sie dieses Kontrollkästchen aktivieren, werden der Dimension die Attribute SCD-Startdatum, Ursprüngliche ID des Enddatums und Status hinzugefügt. **SCD** wird standardmäßig ausgewählt, wenn Sie den Cube anhand einer Vorlage erstellen und der Assistent diese vier Attributtypen in einer Vorlagendimension erkennt.|  
|**Attribute**|Zeigt die Attribute an, die für die Dimension erstellt werden sollen. Jedem Attributnamen in der Liste wird der Dimensionsname vorangestellt. Diese Liste ist schreibgeschützt. Nachdem Sie den Assistenten abgeschlossen haben, können Sie die Attribute mithilfe des Dimensions-Designers ändern.|  
  
## <a name="defining-time-periods"></a>Definieren von Zeiträumen  
 Geben Sie den Datumsbereich, der in der Dimension enthalten sein soll, mithilfe der Seite **Zeiträume definieren** des Assistenten an. Beispielsweise können Sie einen Bereich auswählen, der in Ihren Daten am 1. Januar des ersten Jahres beginnt, und die Jahreszahlen bis über die aktuelle Transaktion hinaus ausweiten. Transaktionen außerhalb dieses Bereichs werden entweder nicht angezeigt, oder sie werden als unbekannte Elemente in der Dimension angezeigt, abhängig von der Einstellung der **UnknownMemberVisible** -Eigenschaft für die Dimension. Die **UnknownMemberName** -Eigenschaft gibt die Beschriftung für das unbekannte Element an. Sie können auch den in Ihren Daten verwendeten Wochenbeginn ändern. (Der Standard ist Sonntag.)  
  
> [!NOTE]  
>  Die Seite **Zeiträume definieren** wird nur angezeigt, wenn Sie auf der Seite **Neue Dimensionen definieren** des Assistenten eine Zeitdimension in den Cube aufnehmen.  
  
 Wählen Sie die Zeiträume (**Jahr**, **Halbjahr**, **Quartal**, **Trimester**, **Monat**, **Zehn Tage**, **Woche**und **Datum**) aus, die Sie in das Schema einfügen möchten. Der Date-Zeitraum muss ausgewählt werden; das Date-Attribut ist das Schlüsselattribut für die Dimension, ohne das die Dimension nicht funktioniert. Sie können auch die Sprache ändern, die zur Beschriftung der Elemente der Dimension verwendet wird.  
  
 Durch die Zeiträume, die Sie auswählen, werden entsprechende Zeitattribute in der neuen Zeitdimension erstellt. Der Assistent fügt außerdem verknüpfte Attribute hinzu, die nicht in der Liste angezeigt werden. Wenn Sie z. B. die Zeitintervalle **Jahr** und **Halbjahr** auswählen, erstellt der Assistent zusätzlich zu den Attributen Jahr und Halbjahr auch die Attribute Tag des Jahres, Tag des Halbjahres und Halbjahr des Jahres.  
  
 Nachdem die Cubeerstellung abgeschlossen wurde, können Sie Zeitattribute mit dem Dimensions-Designer hinzufügen oder entfernen. Das Date-Attribut kann nicht entfernt werden, da es das Schlüsselattribut der Dimension darstellt. Sie können die **AttributeHierarchyVisible** -Eigenschaft in **False**ändern, um das Date-Attribute für Benutzer auszublenden.  
  
 Alle verfügbare Zeiträume werden im Bereich Zeiträume des Dimensions-Designers angezeigt. (Bei Dimensionen, die auf Dimensionstabellen basieren, ersetzt dieser Bereich den Bereich **Datenquellensicht**.) Sie können den Datumsbereich für eine Dimension ändern, indem Sie die Einstellung der **Source**-Eigenschaft (Zeitbindung) für die Dimension ändern. Da es sich hierbei um eine strukturelle Änderung handelt, müssen Sie die Dimension und alle Cubes, die diese verwenden, vor dem Durchsuchen der Daten erneut verarbeiten.  
  
## <a name="specifying-additional-calendars"></a>Angeben zusätzlicher Kalender  
 Auf der Seite **Zusätzliche Kalender angeben** des Assistenten können Sie Kalender auswählen, auf denen die Hierarchien der Dimension basieren sollen. Sie können einen der folgenden Kalender auswählen:  
  
|Kalender|Description|  
|--------------|-----------------|  
|Geschäftskalender|Ein zwölfmonatiger Geschäftskalender. Wenn Sie diesen Kalender auswählen, müssen Sie den Anfangstag des vom Unternehmen verwendeten Geschäftsjahres angeben.|  
|Berichtskalender (oder Marketingkalender)|Ein zwölfmonatiger Berichtskalender, der in einem sich wiederholenden dreimonatigen (quartalsweisen) Muster zwei Monate mit vier und einen Monat mit fünf Wochen enthält. Wenn Sie diesen Kalender auswählen, müssen Sie den Anfangstag und den Anfangsmonat des Dreimonatsmusters mit 4-4-5, 4-5-4 oder 5-4-4 Wochen angeben, wobei diese Zahlen die in einem Monat enthaltenen Wochen darstellen.|  
|Produktionskalender|Ein Kalender, der 13 aus vier Wochen bestehende Zeiträume verwendet, die in drei Quartale mit vier Zeiträumen und ein Quartal mit fünf Zeiträumen unterteilt sind. Wenn Sie diesen Kalender auswählen, geben Sie die Startwoche (zwischen 1 und 4) und den Monat für das Herstellungsjahr und das Quartal mit zusätzlichen Zeiträumen an.|  
|ISO 8601-Kalender|Der Standardkalender für die Daten- und Zeitdarstellung (8601) der Internationalen Organisation für Normung (International Organization for Standardization, ISO). Dieser Kalender besitzt eine integrale Anzahl von 7-Tage-Wochen. Um zu vermeiden, dass eine Woche unterteilt wird, kann ein neues Jahr im Kalender bis zu einige Tage vor oder nach dem 1. Januar starten.|  
  
 Vom Kalender und den ausgewählten Einstellungen hängt es ab, welche Attribute in der Dimension erstellt werden. Wenn Sie im Assistenten auf der Seite **Zeiträume definieren** beispielsweise die Zeiträume **Jahr** und **Quartal** und auf dieser Seite **Geschäftskalender** auswählen, werden die Attribute FiscalYear, FiscalQuarter und FiscalQuarterOfYear für den Geschäftskalender erstellt.  
  
 Im Assistenten werden ebenfalls kalenderspezifische Hierarchien erstellt, die sich aus den für den Kalender erstellten Attributen zusammensetzen. In jedem Kalender werden die einzelnen Ebenen der Hierarchien zusammengefasst und ergeben so die jeweils nächst höhere Ebene. Im 12-monatigen Standardkalender wird beispielsweise über den Assistenten eine Hierarchie erstellt, bestehend aus den Jahres- und Wochenebenen bzw. den Jahres- und Monatsebenen. Die Wochen sind allerdings nicht gleichmäßig in Monate eines Standardkalenders unterteilt, sodass keine Hierarchie zwischen den Jahres-, Monats- und Wochenebenen besteht. Die in einem Berichts- oder Produktionskalender enthaltenen Wochen sind hingegen gleichmäßig in Monate unterteilt, sodass sich aus den in diesen Kalendern enthaltenen Wochen Monate ergeben.  
  
## <a name="defining-dimension-usage"></a>Definieren der Dimensionsverwendung  
 Verwenden Sie die Seite **Dimensionsverwendung definieren** des Assistenten, um die Cubemeasures anzugeben, die von jeder Dimension im Assistenten aggregiert werden. Im Raster **Dimensionsverwendung** auf dieser Seite sind die Dimensionen als Zeilen und Measuregruppen als Spalten aufgeführt. Aktivieren Sie das Kontrollkästchen für eine beliebige Kombination aus Dimension und Measuregruppe, in der die Measures dieser Measuregruppe von der Dimension aggregiert werden.  
  
## <a name="completing-the-cube-wizard"></a>Abschließen des Cube-Assistenten  
 Überprüfen Sie auf der Seite **Assistenten abschließen** die Struktur des neuen Cubes im Feld **Cubename** , und geben Sie einen Namen ein. Aktivieren Sie optional das Kontrollkästchen **Schema jetzt generieren** , um den Schemagenerierungs-Assistent zu starten. In den meisten Fällen sollten Sie dieses Kontrollkästchen nicht aktivieren, wenn Sie weitere Objekte erstellen möchten. Sie können das Schema auch später im Cube-Designer generieren.  
  
  
