---
title: Legen Sie die Eigenschaften einer Datenflusskomponente | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e2073bf67289ff1d54a364f6a82bff51779dc1c5
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="set-the-properties-of-a-data-flow-component"></a>Festlegen der Eigenschaften einer Datenflusskomponente
  Die Eigenschaften von Datenflusskomponenten, z. B. Quellen, Ziele und Transformationen, können Sie mithilfe eine der folgenden Funktionen festlegen:  
  
-   Die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bereitgestellten Komponenten-Editoren. Diese Editoren schließen nur die benutzerdefinierten Eigenschaften jeder Datenflusskomponente ein.  
  
-   Im Fenster **Eigenschaften** werden die benutzerdefinierten Eigenschaften auf Komponentenebene jedes Elements sowie die allen Datenflusselementen gemeinsamen Eigenschaften aufgelistet.  
  
-   Das Dialogfeld **Erweiterter Editor** ermöglicht den Zugriff auf benutzerdefinierte Eigenschaften für jede Komponente. Das Dialogfeld **Erweiterter Editor** ermöglicht außerdem den Zugriff auf benutzerdefinierte Eigenschaften für die einzelnen Komponenten sowie auf die für alle Datenflusskomponenten gemeinsamen Eigenschaften – die Eigenschaften von Eingaben, Ausgaben, Fehlerausgaben, Spalten und externen Spalten.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-a-component-editor"></a>Legen Sie die Eigenschaften einer Datenflusskomponente mit eines Komponenten-Editors  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** , und doppelklicken Sie anschließend auf den Datenflusstask, der den Datenfluss mit der Komponente enthält, deren Eigenschaften Sie anzeigen und ändern möchten.  
  
4.  Doppelklicken Sie auf die Datenflusskomponente.  
  
5.  Zeigen Sie im Komponenten-Editor die Eigenschaftswerte an, oder ändern Sie diese, und schließen Sie dann den Editor.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**, um das aktualisierte Paket zu speichern.  
  
## <a name="set-the-properties-of-a-data-flow-component-in-the-properties-window"></a>Legen Sie die Eigenschaften einer Datenflusskomponente im Eigenschaftenfenster  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** , und doppelklicken Sie anschließend auf den Datenflusstask, der die Komponente enthält, deren Eigenschaften Sie anzeigen und ändern möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Datenflusskomponente, und klicken Sie anschließend auf **Eigenschaften**.  
  
5.  Zeigen Sie die Eigenschaftswerte an, oder ändern Sie diese, und schließen Sie dann das Fenster **Eigenschaften** .  
  
    > [!NOTE]  
    >  Viele Eigenschaften sind schreibgeschützt und können nicht geändert werden.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**, um das aktualisierte Paket zu speichern.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-the-advanced-editor"></a>Legen Sie die Eigenschaften einer Datenflusskomponente mithilfe des erweiterten Editors  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** , und doppelklicken Sie anschließend auf den Datenflusstask, der die Komponente enthält, die Sie anzeigen oder ändern möchten.  
  
4.  Klicken Sie im Datenfluss-Designer mit der rechten Maustaste auf die Datenflusskomponente, und klicken Sie anschließend auf **Erweiterten Editor anzeigen**.  
  
    > [!NOTE]  
    >  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kann **Erweiterter Editor**nicht für Datenflusskomponenten verwendet werden, die mehrere Eingaben unterstützen.  
  
5.  Führen Sie im Dialogfeld **Erweiterter Editor** einen beliebigen der folgenden Schritte aus:  
  
    -   Klicken Sie auf die Registerkarte **Verbindungs-Manager** , um die von der Komponente verwendete Verbindung anzuzeigen und anzugeben.  
  
        > [!NOTE]  
        >  Die Registerkarte **Verbindungs-Manager** ist nur für Datenflusskomponenten verfügbar, die Verbindungs-Manager zum Herstellen einer Verbindung mit Datenquellen wie z.B. Dateien und Datenbanken verwenden.  
  
    -   Klicken Sie auf die Registerkarte **Komponenteneigenschaften** , um die Eigenschaften auf Komponentenebene anzuzeigen und zu ändern.  
  
    -   Klicken Sie auf die Registerkarte **Spaltenzuordnungen** , um Zuordnungen zwischen externen Spalten und der verfügbaren Ausgabe anzuzeigen und zu ändern.  
  
        > [!NOTE]  
        >  Die Registerkarte **Spaltenzuordnungen** ist nur verfügbar, wenn Sie Quellen oder Ziele anzeigen oder bearbeiten.  
  
    -   Klicken Sie auf die Registerkarte **Eingabespalten** , um eine Liste der verfügbaren Eingabespalten anzuzeigen und die Namen von Ausgabespalten zu aktualisieren.  
  
        > [!NOTE]  
        >  Die Registerkarte Eingabespalten ist nur verfügbar, wenn Sie mit Transformationen oder Zielen arbeiten. Weitere Informationen finden Sie unter [Integration Services Transformations](../../integration-services/data-flow/transformations/integration-services-transformations.md).  
  
    -   Klicken Sie auf die Registerkarte **Eingabe- und Ausgabeeigenschaften** , um die Eigenschaften von Eingaben, Ausgaben und Fehlerausgaben sowie die Eigenschaften der enthaltenen Spalten anzuzeigen und zu ändern.  
  
        > [!NOTE]  
        >  Quellen weisen keine Eingaben auf. Ziele haben keine Ausgaben, mit Ausnahme einer optionalen Fehlerausgabe.  
  
6.  Zeigen Sie die Eigenschaftswerte an, oder ändern Sie diese.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**, um das aktualisierte Paket zu speichern.  

## <a name="common-properties-of-data-flow-components"></a>Allgemeine Eigenschaften von Datenflusskomponenten
Die Datenflussobjekte im [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell verfügen über allgemeine Eigenschaften und benutzerdefinierte Eigenschaften auf der Komponentenebene, der Eingabe- und Ausgabeebene und der Ebene der Eingabe- und Ausgabespalten. Viele Eigenschaften verfügen über schreibgeschützte Werte, für die zur Laufzeit eine Zuweisung über das Datenflussmodul erfolgt.  
  
 In diesem Thema werden die allgemeinen Eigenschaften von Datenflussobjekten aufgelistet und beschrieben.  
  
-   [Komponenten](#components)  
  
-   [Eingaben](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [Ausgaben](#outputs)  
  
-   [Ausgabespalten](#outputcolumns)  
  
 
###  <a name="components"></a> Component properties  
 Im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Objektmodell implementiert eine Komponente im Datenfluss die Schnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 Die folgende Tabelle beschreibt die Eigenschaften der Komponenten in einem Datenfluss. Einige Eigenschaften verfügen über schreibgeschützte Werte, für die zur Laufzeit eine Zuweisung über das Datenflussmodul erfolgt.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|Die CLSID der Komponente.|  
|ContactInfo|String|Kontaktinformationen für den Entwickler einer Komponente.|  
|Description|String|Die Beschreibung der Datenflusskomponente. Der Standardwert dieser Eigenschaft entspricht dem Namen der Datenflusskomponente.|  
|ID|Integer|Ein Wert, der diese Instanz der Komponente eindeutig identifiziert.|  
|IdentificationString|String|Identifiziert die Komponente.|  
|IsDefaultLocale|Boolean|Gibt an, ob die Komponente das Gebietsschema des Datenflusstasks verwendet, zu dem es gehört.|  
|LocaleID|Integer|Das Gebietsschema, das die Datenflusskomponente verwendet, wenn das Paket ausgeführt wird. Alle Windows-Gebietsschemas sind zur Verwendung in Datenflusskomponenten verfügbar.|  
|Name|String|Der Name der Datenflusskomponente.|  
|PipelineVersion|Integer|Die Version des Datenflusstasks, innerhalb derer eine Komponente zur Ausführung entworfen wird.|  
|UsesDispositions|Boolean|Gibt an, ob eine Komponente über eine Fehlerausgabe verfügt.|  
|ValidateExternalMetadata|Boolean|Gibt an, ob die Metadaten externer Spalten überprüft werden. Der Standardwert dieser Eigenschaft ist **True**.|  
|Version|Integer|Die Version einer Komponente.|  
  
###  <a name="inputs"></a>Eingabeeigenschaften  
 Im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell verfügen Transformationen und Ziele über Eingaben. Eine Eingabe einer Komponente im Datenfluss implementiert die Schnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>.  
  
 Die folgende Tabelle beschreibt die Eigenschaften der Eingaben von Komponenten in einem Datenfluss. Einige Eigenschaften verfügen über schreibgeschützte Werte, für die zur Laufzeit eine Zuweisung über das Datenflussmodul erfolgt.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|Description|String|Die Beschreibung der Eingabe.|  
|ErrorOrTruncationOperation|String|Eine optionale Zeichenfolge, die die Fehlertypen oder abgeschnittene Daten angibt, die bei der Verarbeitung einer Zeile auftreten können.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Ein Wert, der die Behandlung von Fehlern angibt. Mögliche Werte sind **Fail component**, **Ignore failure**und **Redirect row**.|  
|HasSideEffects|Boolean|Gibt an, ob eine Komponente aus dem Ausführungsplan des Datenflusses entfernt werden kann, wenn diese nicht an eine Downstreamkomponente angefügt ist und **RunInOptimizedMode** auf **true**gesetzt ist.|  
|ID|Integer|Ein Wert, der die Eingabe eindeutig identifiziert.|  
|IdentificationString|String|Eine Zeichenfolge, die die Eingabe identifiziert.|  
|IsSorted|Boolean|Gibt an, ob die Daten in der Eingabe sortiert werden.|  
|Name|String|Der Name der Eingabe.|  
|SourceLocale|Integer|Die Gebietsschema-ID (Locale ID, LCID) der Eingabedaten.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Ein Wert, der bestimmt, wie die Komponente das Abschneiden von Daten behandelt, das bei der Verarbeitung von Zeilen auftritt. . Mögliche Werte sind **Fail component**, **Ignore failure**und **Redirect row**.|  
  
 Ziele und einige Transformationen unterstützen keine Fehlerausgaben, und die Eigenschaften ErrorRowDisposition und TruncationRowDisposition dieser Komponenten sind schreibgeschützt.  
  
###  <a name="inputcolumns"></a>Eigenschaften der Eingabespalten  
 Im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell enthält eine Eingabe eine Auflistung von Eingabespalten. Eine Eingabespalte einer Komponente im Datenfluss implementiert die Schnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100>.  
  
 Die folgende Tabelle beschreibt die Eigenschaften der Eingabespalten von Komponenten in einem Datenfluss. Einige Eigenschaften verfügen über schreibgeschützte Werte, für die zur Laufzeit eine Zuweisung über das Datenflussmodul erfolgt.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Eine Gruppe von Flags, die den Vergleich von Spalten angeben, die über einen Zeichendatentyp verfügen. Weitere Informationen finden Sie unter [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).|  
|Description|String|Beschreibt die Eingabespalte.|  
|ErrorOrTruncationOperation|String|Eine optionale Zeichenfolge, die die Fehlertypen oder abgeschnittene Daten angibt, die bei der Verarbeitung einer Zeile auftreten können.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Ein Wert, der die Behandlung von Fehlern angibt. Mögliche Werte sind **Fail component**, **Ignore failure**und **Redirect row**.|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|Die ID der externen Metadatenspalte, die einer Eingabespalte zugewiesen ist.|  
|ID|Integer|Ein Wert, der die Eingabespalte eindeutig identifiziert.|  
|IdentificationString|String|Eine Zeichenfolge, die die Eingabespalte identifiziert.|  
|LineageID|Integer|Die ID der Upstreamspalte.|  
|LineageIdentificationString|String|Die Identifikationszeichenfolge, die den Namen der Upstreamspalte enthält.|  
|Name|String|Der Name der Eingabespalte.|  
|SortKeyPosition|Integer|Ein Wert, der anzeigt, ob eine Spalte sortiert ist, und der die zugehörige Sortierreihenfolge und die Reihenfolge, in der mehrere Spalten sortiert werden, angibt. Der Wert **0** weist darauf hin, dass die Spalte nicht sortiert ist.  Weitere Informationen finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Ein Wert, der bestimmt, wie die Komponente das Abschneiden von Daten behandelt, das bei der Verarbeitung von Zeilen auftritt. Mögliche Werte sind **Fail component**, **Ignore failure**und **Redirect row**.|  
|UpstreamComponentName|String|Der Name der Upstreamkomponente.|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|Ein Wert, der bestimmt, wie eine Eingabespalte von der Komponente verwendet wird.|  
  
 Eingabespalten verfügen auch über die Datentypeigenschaften, die unter "Datentypeigenschaften" beschrieben sind.  
  
###  <a name="outputs"></a>Ausgabeeigenschaften  
 Im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell verfügen Quellen und Transformationen über Ausgaben. Eine Ausgabe einer Komponente im Datenfluss implementiert die Schnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>.  
  
 Die folgende Tabelle beschreibt die Eigenschaften der Ausgaben von Komponenten in einem Datenfluss. Einige Eigenschaften verfügen über schreibgeschützte Werte, für die zur Laufzeit eine Zuweisung über das Datenflussmodul erfolgt.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Boolean|Ein Wert, der bestimmt, ob ein Datenflussmodul die Ausgabe löscht, wenn sie von einem Pfad getrennt wird.|  
|Description|String|Beschreibt die Ausgabe.|  
|ErrorOrTruncationOperation|String|Eine optionale Zeichenfolge, die die Fehlertypen oder abgeschnittene Daten angibt, die bei der Verarbeitung einer Zeile auftreten können.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Ein Wert, der die Behandlung von Fehlern angibt. Mögliche Werte sind **Fail component**, **Ignore failure**und **Redirect row**.|  
|ExclusionGroup|Integer|Ein Wert, der eine Gruppe sich gegenseitig ausschließender Ausgaben identifiziert.|  
|HasSideEffects|Boolean|Ein Wert, der angibt, ob eine Komponente aus dem Ausführungsplan des Datenflusses entfernt werden kann, wenn diese nicht an eine Upstreamkomponente angefügt ist und **RunInOptimizedMode** auf **true**gesetzt ist.|  
|ID|Integer|Ein Wert, der die Ausgabe eindeutig identifiziert.|  
|IdentificationString|String|Eine Zeichenfolge, die die Ausgabe identifiziert.|  
|IsErrorOut|Boolean|Gibt an, ob es sich bei der Ausgabe um eine Fehlerausgabe handelt.|  
|IsSorted|Boolean|Gibt an, ob die Ausgabe sortiert wird. Der Standardwert ist **False**.<br /><br /> **\*\*Wichtige \* \***  Festlegen des Werts der **IsSorted** Eigenschaft, um **"true"** werden die Daten nicht sortiert. Diese Eigenschaft ist lediglich ein Hinweis für die Downstreamkomponenten, dass die Daten vorher sortiert wurden. Weitere Informationen finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|Name|String|Der Name der Ausgabe.|  
|SynchronousInputID|Integer|Die ID einer Eingabe, die zur Ausgabe synchron ist.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Ein Wert, der bestimmt, wie die Komponente das Abschneiden von Daten behandelt, das bei der Verarbeitung von Zeilen auftritt. Mögliche Werte sind **Fail component**, **Ignore failure**und **Redirect row**.|  
  
###  <a name="outputcolumns"></a>Eigenschaften der Ausgabespalten  
 Im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell enthält eine Ausgabe eine Auflistung von Ausgabespalten. Eine Ausgabespalte einer Komponente im Datenfluss implementiert die Schnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100>.  
  
 Die folgende Tabelle beschreibt die Eigenschaften der Ausgabespalten von Komponenten in einem Datenfluss. Einige Eigenschaften verfügen über schreibgeschützte Werte, für die zur Laufzeit eine Zuweisung über das Datenflussmodul erfolgt.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Eine Gruppe von Flags, die den Vergleich von Spalten angeben, die über einen Zeichendatentyp verfügen. Weitere Informationen finden Sie unter [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).|  
|Description|String|Beschreibt die Ausgabespalte.|  
|ErrorOrTruncationOperation|String|Eine optionale Zeichenfolge, die die Fehlertypen oder abgeschnittene Daten angibt, die bei der Verarbeitung einer Zeile auftreten können.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Ein Wert, der die Behandlung von Fehlern angibt. Mögliche Werte sind **Fail component**, **Ignore failure**und **Redirect row**. Der Standardwert lautet **Fehler bei Komponente**.|  
|ExternalMetadataColumnID|Integer|Die ID der externen Metadatenspalte, die einer Eingabespalte zugewiesen ist.|  
|ID|Integer|Ein Wert, der die Ausgabespalte eindeutig identifiziert.|  
|IdentificationString|String|Eine Zeichenfolge, die die Ausgabespalte identifiziert.|  
|LineageID|Integer|Die ID der Ausgabespalte. Downstreamkomponenten verweisen auf die Spalte, indem sie diesen Wert verwenden.|  
|LineageIdentificationString|String|Die Identifikationszeichenfolge, die den Namen der Spalte enthält.|  
|Name|String|Der Name der Ausgabespalte.|  
|SortKeyPosition|Integer|Ein Wert, der anzeigt, ob eine Spalte sortiert ist, und der die zugehörige Sortierreihenfolge und die Reihenfolge, in der mehrere Spalten sortiert werden, angibt. Der Wert **0** weist darauf hin, dass die Spalte nicht sortiert ist. Weitere Informationen finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|SpecialFlags|Integer|Ein Wert, der die speziellen Flags der Ausgabespalte enthält.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Ein Wert, der bestimmt, wie die Komponente das Abschneiden von Daten behandelt, das bei der Verarbeitung von Zeilen auftritt. Mögliche Werte sind **Fail component**, **Ignore failure**und **Redirect row**. Der Standardwert lautet **Fehler bei Komponente**.|  
  
 Ausgabespalten schließen auch eine Gruppe von Datentypeigenschaften ein.  
  
### <a name="external-metadata-column-properties"></a>Eigenschaften externer Metadatenspalten  
 Im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell können Eingaben und Ausgaben eine Auflistung externer Metadatenspalten enthalten. Eine externe Metadatenspalte einer Komponente im Datenfluss implementiert die Schnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>.  
  
 Die folgende Tabelle beschreibt die Eigenschaften der externen Metadatenspalten von Komponenten in einem Datenfluss. Einige Eigenschaften verfügen über schreibgeschützte Werte, für die zur Laufzeit eine Zuweisung über das Datenflussmodul erfolgt.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|Description|String|Beschreibt die externe Spalte.|  
|ID|Integer|Ein Wert, der die Spalte eindeutig identifiziert.|  
|IdentificationString|String|Eine Zeichenfolge, die die Spalte identifiziert.|  
|Name|String|Der Name der externen Spalte.|  
  
 Externe Metadatenspalten schließen auch eine Gruppe von Datentypeigenschaften ein.  
  
### <a name="data-type-properties"></a>Datentypeigenschaften  
 Ausgabespalten und externe Metadatenspalten schließen eine Gruppe von Datentypeigenschaften ein. Je nach dem Datentyp der Spalte können Eigenschaften einen Lese-/Schreibzugriff oder einen Schreibschutz festlegen.  
  
 Die folgende Tabelle beschreibt die Datentypeigenschaften von Ausgabespalten und externen Metadatenspalten.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|CodePage|Integer|Gibt die Codepage für Zeichenfolgendaten an, bei denen es sich nicht um Unicode handelt.|  
|DataType|Ganze Zahl (Enumeration)|Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentyp der Spalte. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|Länge|Integer|Die Länge der Zeichen in einer Spalte.|  
|Genauigkeit|Integer|Die Genauigkeit einer numerischen Spalte.|  
|Dezimalstellen|Integer|Die Dezimalstellen einer numerischen Spalte.|  

## <a name="custom-properties-of-data-flow-components"></a>Benutzerdefinierte Eigenschaften von Datenflusskomponenten
Informationen zu benutzerdefinierten Eigenschaften finden Sie unter den folgenden Themen  
  
-   [Benutzerdefinierte Eigenschaften von ADO.NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des CDC-Steuerungstasks](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften der CDC-Quelle](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des Ziels des Data Mining-Modelltrainings](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des DataReader-Ziels](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des Ziels für Dimensionsverarbeitung](../../integration-services/data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Benutzerdefinierte Eigenschaften von Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften der Flatfile](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von ODBC-Zielen](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften der ODBC-Quelle](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)Benutzerdefinierte Eigenschaften für OLE DB  
  
-   [Benutzerdefinierte Eigenschaften des Ziels für Partitionsverarbeitung](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften der Rohdatendatei](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des Recordsetziels](../../integration-services/data-flow/recordset-destination-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des Ziels für SQL Server Compact Edition](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des SQL Server-Ziels](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
-   [Benutzerdefinierte Eigenschaften der XML-Quelle](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
## <a name="use-an-expression-in-a-data-flow-component"></a>Verwenden eines Ausdrucks in einer Datenflusskomponente
In diesem Verfahren wird beschrieben, wie ein Ausdruck der Transformation für bedingtes Teilen oder der Transformation für abgeleitete Spalten hinzugefügt wird. Die Transformation für bedingtes Teilen verwendet Ausdrücke zum Definieren der Bedingungen, die Datenzeilen in eine Transformationsausgabe leiten, und die Transformation für abgeleitete Spalten verwendet Ausdrücke zum Definieren von Werten, die Spalten zugewiesen sind.  
  
 Um einen Ausdruck in einer Transformation zu implementieren, muss das Paket bereits mindestens einen Datenflusstask und eine Quelle einschließen. 
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Ablaufsteuerung** , und klicken Sie dann auf den Datenflusstask mit dem Datenfluss, den Sie in einem Ausdruck implementieren möchten.  
  
4.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus der **Toolbox** die Transformation für bedingtes Teilen oder die Transformation für abgeleitete Spalten auf die Entwurfsoberfläche.  
  
5.  Ziehen Sie den grünen Konnektor von der Quelle oder einer Transformation auf die Transformation für bedingtes Teilen oder abgeleitete Spalten.  
  
6.  Doppelklicken Sie auf die Transformation, um ihr Dialogfeld zu öffnen.  
  
7.  Erweitern Sie im linken Fenster die Option **Variablen** , um system- und benutzerdefinierte Variablen anzuzeigen, und erweitern Sie **Spalten** , um die Transformationseingabespalten anzuzeigen.  
  
8.  Erweitern Sie im rechten Fenster die Option **Mathematische Funktionen**, **Zeichenfolgenfunktionen**, **Datums-/Uhrzeitfunktionen**, **NULL-Funktionen**, **Typumwandlungen**und **Operatoren** , um auf die Funktionen, die Umwandlungen und die Operatoren zuzugreifen, die von der Ausdrucksgrammatik bereitgestellt werden.  
  
9. Gehen Sie je nach Transformation zum Erstellen eines Ausdrucks wie folgt vor  
  
    -   Ziehen Sie im Dialogfeld **Transformations-Editor für bedingtes Teilen** die Variablen, Spalten, Funktionen, Operatoren und Umwandlungen in die Spalte **Bedingung** . Sie können den Ausdruck aber auch direkt in die Spalte **Bedingung** eingeben.  
  
    -   Ziehen Sie im Dialogfeld **Transformations-Editor für abgeleitete Spalten** die Variablen, Spalten, Funktionen, Operatoren und Umwandlungen in die Spalte **Ausdruck** . Sie können den Ausdruck aber auch direkt in die Spalte **Ausdruck** eingeben.  
  
        > [!NOTE]  
        >  Wenn Sie den Fokus von der Spalte **Bedingung** oder **Ausdruck** entfernen, kann der Ausdruckstext hervorgehoben dargestellt werden, was auf eine falsche Ausdruckssyntax hinweist.  
  
10. Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
    > [!NOTE]  
    >  Wenn der Ausdruck ungültig ist, wird eine Warnung angezeigt, die die Syntaxfehler im Ausdruck beschreibt.  

## <a name="data-flow-properties-that-you-can-set-with-an-expression"></a>Data Flow-Eigenschaften, die Sie mit einem Ausdruck festlegen können
Die Werte mancher Eigenschaften von Datenflussobjekten können mithilfe von Eigenschaftsausdrücken festgelegt werden, die im Datenflusstask-Container verfügbar sind.  
  
 Weitere Informationen zum Verwenden von Eigenschaftsausdrücken finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Sie können Eigenschaftsausdrücke dazu verwenden, Konfigurationen für jede bereitgestellte Instanz eines Pakets anzupassen. Sie können Eigenschaftsausdrücke auch zur Festlegung von Laufzeiteinschränkungen für ein Paket nutzen, indem Sie die Option **/set** mit dem Eingabeaufforderungshilfsprogramm **dtexec** verwenden. Sie können z. B. die von der Transformation für Sortierung verwendeten **MaximumThreads** oder die **MaxMemoryUsage** der Transformationen für die Fuzzygruppierung und die Fuzzysuche einschränken. Wenn keine Einschränkungen bestehen, legen diese Transformationen möglicherweise große Datenmengen im Arbeitsspeicher ab.  
  
 Um einen Eigenschaftsausdruck für eine der Eigenschaften eines unter diesem Thema aufgelisteten Datenflussobjekts festzulegen, zeigen Sie das Fenster **Eigenschaften** für den Datenflusstask an, indem Sie den Datenflusstask auf der Oberfläche **Ablaufsteuerung** des Designers auswählen oder indem Sie die Registerkarte **Datenfluss** des Designers auswählen, ohne eine individuelle Komponente oder einen Pfad auszuwählen. Wählen Sie die **Ausdrücke** -Eigenschaft aus, und klicken Sie auf die Schaltfläche mit den drei Punkten, um das Dialogfeld **Eigenschaftsausdrucks-Editor** anzuzeigen. Öffnen Sie die Dropdownliste **Eigenschaft** , um eine Eigenschaft auszuwählen, und geben Sie dann einen Ausdruck in das Textfeld **Ausdruck** ein, oder klicken Sie auf die Schaltfläche mit den drei Punkten, um das Dialogfeld **Ausdrucks-Generator** anzuzeigen.  
  
 Die **Eigenschaft** -Liste zeigt nur die verfügbaren Eigenschaften der Datenflussobjekte an, die bereits in der **Datenfluss** -Oberfläche des Designers platziert wurden. Deshalb können Sie die **Eigenschaft** -Liste nicht dazu verwenden, alle möglichen Eigenschaften von Datenflussobjekten anzuzeigen, die Eigenschaftsausdrücke unterstützen. Wenn Sie z.B. eine ADO.NET-Quelle auf der Designer-Oberfläche platziert haben, enthält die Liste **Eigenschaft** einen Eintrag für die Eigenschaft **[ADO.NET-Quelle].[SQL-Befehl]** . Die Liste zeigt außerdem viele Eigenschaften des Datenflusstasks selbst an.  
 
 Die Werte der Eigenschaften in der folgenden Liste können über Eigenschaftsausdrücke angegeben werden.  
  
### <a name="data-flow-sources"></a>Datenflussquellen  
  
|Datenflussobjekt|Eigenschaft|  
|----------------------|--------------|  
|ADO NET-Quelle|TableOrViewName-Eigenschaft<br /><br /> SqlCommand-Eigenschaft|  
|XML-Quelle|XMLData-Eigenschaft<br /><br /> XMLSchemaDefinition-Eigenschaft|  
  
### <a name="data-flow-transformations"></a>Datenflusstransformationen  
 Weitere Informationen zu diesen benutzerdefinierten Eigenschaften finden Sie unter [Transformation Custom Properties](../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
|Datenflussobjekt|Eigenschaft|  
|----------------------|--------------|  
|Transformation für bedingtes Teilen|FriendlyExpression-Eigenschaft|  
|Transformation für abgeleitete Spalten|FriendlyExpression-Eigenschaft|  
|Transformation für Fuzzygruppierung|MaxMemoryUsage-Eigenschaft|  
|Transformation für Fuzzysuche|MaxMemoryUsage-Eigenschaft|  
|Transformation für Suche|SqlCommand-Eigenschaft<br /><br /> SqlCommandParam-Eigenschaft|  
|Transformation für OLE DB-Befehl|SqlCommand-Eigenschaft|  
|Transformation für Prozentwert-Stichproben|SamplingValue-Eigenschaft|  
|Transformation für Pivot|PivotKeyValue-Eigenschaft|  
|Transformation für Zeilenstichproben|SamplingValue-Eigenschaft|  
|Transformation zum Sortieren|MaximumThreads-Eigenschaft|  
|Entpivotierungstransformation|PivotKeyValue-Eigenschaft|  
  
### <a name="data-flow-destinations"></a>Datenflussziele  
  
|Datenflussobjekt|Eigenschaft|  
|----------------------|--------------|  
|ADO NET-Ziel|TableOrViewName-Eigenschaft<br /><br /> BatchSize-Eigenschaft<br /><br /> CommandTimeout-Eigenschaft|  
|Flatfileziel|Header-Eigenschaft|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Compact-Ziel|TableName-Eigenschaft|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Ziel|BulkInsertTableName-Eigenschaft<br /><br /> BulkInsertFirstRow-Eigenschaft<br /><br /> BulkInsertLastRow-Eigenschaft<br /><br /> BulkInsertOrder-Eigenschaft<br /><br /> Timeout-Eigenschaft|  


