---
title: Integration Services-Pfade | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.patheditor.general.f1
- sql13.dts.designer.patheditor.metadata.f1
- sql13.dts.designer.patheditor.visualizers.f1
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 541c8faa4c878922411680646f3fa7a557eefe0f
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-paths"></a>SQL Server Integration Services-Pfade
  Ein Pfad verbindet zwei Komponenten in einem Datenfluss, indem die Ausgabe einer Datenflusskomponente mit der Eingabe einer anderen Komponente verbunden wird. Ein Pfad weist eine Quelle und ein Ziel auf. Wenn z. B. ein Pfad eine Verbindung mit einer OLE DB-Quelle und einer Transformation zum Sortieren herstellt, ist die OLE DB-Quelle die Quelle des Pfads, und die Transformation zum Sortieren ist das Ziel des Pfads. Die Quelle ist die Komponente, wo der Pfad beginnt, und das Ziel ist die Komponente, wo der Pfad endet.  
  
 Wenn Sie ein Paket im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer ausführen, können Sie die Daten in einem Datenfluss anzeigen, indem Sie Daten-Viewer an einen Pfad anfügen. Ein Daten-Viewer kann zur Anzeige von Daten in einem Raster konfiguriert werden. Ein Daten-Viewer ist ein hilfreiches Tool zum Debuggen. Weitere Informationen finden Sie unter [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## <a name="configure-the-path"></a>Konfigurieren Sie den Pfad  
 Der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer stellt das Dialogfeld **Datenflusspfad-Editor** bereit, in dem Sie Pfadeigenschaften festlegen, die Metadaten der Datenspalten, die über den Pfad übergeben werden, anzeigen sowie Daten-Viewer konfigurieren können.  
  
 Zu den konfigurierbaren Pfadeigenschaften gehört der Name, die Beschreibung und die Anmerkung des Pfads. Pfade können auch programmgesteuert konfiguriert werden. Weitere Informationen finden Sie unter [Programmgesteuertes Verbinden von Datenflusskomponenten](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
 Eine Pfadanmerkung zeigt den Namen der Pfadquelle oder den Pfadnamen in der Entwurfsoberfläche der Registerkarte **Datenfluss** im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer an. Pfadanmerkungen sind mit den Anmerkungen vergleichbar, die Sie Datenflüssen, Ablaufsteuerungen und Ereignishandlern hinzufügen können. Der einzige Unterschied besteht darin, dass eine Pfadanmerkung einem Pfad hinzugefügt wird, während andere Anmerkungen auf den Registerkarten **Datenfluss**, **Ablaufsteuerung**und **Ereignishandler**des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers angezeigt werden.  
  
 Die Metadaten zeigen den Namen, den Datentyp, die Genauigkeit, die Dezimalstellen, die Länge, die Codepage und die Quellkomponente jeder Spalte in der Ausgabe der vorherigen Komponente an. Die Quellkomponente ist jene Datenflusskomponente, die die Spalte erstellt hat. Dies kann, muss aber nicht die erste Komponente im Datenfluss sein. Beispielsweise werden mit einer Transformation für UNION ALL und einer Transformation zum Sortieren eigene Spalten erstellt, die die Quelle der Ausgabespalten sind. Dagegen können Spalten mit einer Transformation für das Kopieren von Spalten durchlaufen werden, ohne sie zu ändern. Es können auch neue Spalten erstellt werden, indem Eingabespalten kopiert werden. Die Transformation für das Kopieren von Spalten ist nur für neue Spalten die Quellkomponente.  

## <a name="set-the-properties-of-a-path-with-the-data-flow-path-editor"></a>Legen Sie die Eigenschaften eines Pfads mit dem Daten Datenflusspfad-Editor
Mit Pfaden werden zwei Datenflusskomponenten verbunden. Wenn Sie Pfadeigenschaften festlegen möchten, muss der Datenfluss mindestens zwei verbundene Datenflusskomponenten enthalten.
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und doppelklicken Sie auf einen Pfad.  
  
4.  Klicken Sie im Dialogfeld **Datenflusspfad-Editor**auf **Allgemein**. Nun können Sie den Standardnamen des Pfades bearbeiten und eine Beschreibung des Pfades angeben. Sie können auch die PathAnnotation-Eigenschaft ändern.  
  
5.  Klicken Sie auf **OK**.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

## <a name="general-page---data-flow-path-editor"></a>Seite "Allgemein" - Daten Datenflusspfad-Editors
Mithilfe des Dialogfelds **Datenflusspfad-Editor** legen Sie Pfadeigenschaften fest, zeigen Metadaten an und verwalten die mit dem Pfad verknüpften Daten-Viewer.  
  
 Mit dem Knoten **Allgemein** des Dialogfelds **Datenflusspfad-Editor** werden der Pfad benannt und beschrieben und die Optionen für die Pfadanmerkungen angegeben.  
  
### <a name="options"></a>enthalten  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Pfad an.  
  
 **ID**  
 Der Herkunftsbezeichner des Pfads. Diese Eigenschaft ist schreibgeschützt.  
  
 **IdentificationString**  
 Die Zeichenfolge, die den Pfad identifiziert. Wird automatisch aus dem oben eingegebenen Namen erzeugt.  
  
 **Description**  
 Beschreiben Sie den Pfad.  
  
 **PathAnnotation**  
 Geben Sie den Typ der zu verwendenden Anmerkung ein. Wählen Sie **Never** , um Anmerkungen zu deaktivieren, **AsNeeded** , um Anmerkungen bei Bedarf zu aktivieren, **SourceName** , um eine Anmerkung automatisch anhand des Werts der Option **SourceName** zu erzeugen, oder **PathName** , um eine Anmerkung automatisch aus dem Wert der **Name** -Eigenschaft zu erzeugen.  
  
 **DestinationName**  
 Zeigt die Eingabe an, die das Ende des Pfads angibt.  
  
 **SourceName**  
 Zeigt die Ausgabe an, die den Beginn des Pfads angibt.  
 
## <a name="metadata-page---data-flow-path-editor"></a>Seite "Metadaten" – Daten Datenflusspfad-Editors
Verwenden Sie die Seite **Metadaten** im Dialogfeld **Datenflusspfad-Editor** , um die Metadaten der Pfadspalten anzuzeigen.  
  
### <a name="options"></a>enthalten  
 **Pfadmetadaten**  
 Listet die Spaltenmetadaten auf. Klicken Sie auf die Spaltenüberschriften, um die Spaltendaten zu sortieren.  
  
 **Name**  
 Listet den Spaltennamen auf.  
  
 **Datentyp**  
 Listet den Datentyp der Spalte auf.  
  
 **Genauigkeit**  
 Listet die Anzahl der Stellen einer numerischen Zahl auf.  
  
 **Dezimalstellen**  
 Listet die Anzahl der Stellen rechts von der Dezimalstelle einer numerischen Zahl auf.  
  
 **Länge**  
 Listet die aktuelle Länge der Spalte auf.  
  
 **Codepage**  
 Listet die Codepage der Spalte auf. Der Wert **0** weist darauf hin, dass die Spalte keine Codepage verwendet. Dies ist der Fall, wenn die Daten als Unicode-, numerischer, Datums- oder Uhrzeitdatentyp vorliegen.  
  
 **Sortierschlüsselposition**  
 Listet die Sortierschlüsselposition der Spalte auf. Der Wert **0** weist darauf hin, dass die Spalte nicht sortiert ist.  
  
> [!NOTE]  
>  Ein Minus-Präfix (-) weist darauf hin, dass die Spalte in absteigender Reihenfolge sortiert ist.  
  
 **Vergleichsflags**  
 Listet die Vergleichsflags auf, die auf die Spalte angewendet werden.  
  
 **Quellkomponente**  
 Listet die Datenflusskomponente auf, die die Quelle der Spalte darstellt.  
  
 **In Zwischenablage kopieren**  
 Kopiert die Spaltenmetadaten in die Zwischenablage. Standardmäßig werden alle Metadatenzeilen in der aktuell angezeigten Reihenfolge kopiert und sortiert.  
 
## <a name="data-viewers-page---data-flow-path-editor"></a>Seite der Daten-Viewer - Daten Datenflusspfad-Editors
Verwenden Sie die Seite **Daten-Viewer** des Dialogfelds **Datenflusspfad-Editor** , um die Daten-Viewer zu verwalten, die dem Pfad zugeordnet sind.  
  
### <a name="options"></a>enthalten  
 **Name**  
 Listet die Daten-Viewer auf.  
  
 **Typ des Daten-Viewers**  
 Listet den Typ des Daten-Viewers auf.  
  
 **Hinzufügen**  
 Klicken Sie auf diese Schaltfläche, um mithilfe des Dialogfelds **Daten-Viewer konfigurieren** einen Daten-Viewer hinzuzufügen.  
  
 **Delete**  
 Klicken Sie auf diese Schaltfläche, um den ausgewählten Daten-Viewer zu löschen.  
  
 **Konfigurieren**  
 Klicken Sie auf diese Schaltfläche, um mithilfe des Dialogfelds **Daten-Viewer konfigurieren** einen ausgewählten Daten-Viewer zu konfigurieren.  
 
## <a name="path-properties"></a>Path Properties
Die Datenflussobjekte im [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell verfügen über allgemeine Eigenschaften und benutzerdefinierte Eigenschaften auf der Komponentenebene, der Eingabe- und Ausgabeebene und der Ebene der Eingabe- und Ausgabespalten. Viele Eigenschaften verfügen über schreibgeschützte Werte, für die zur Laufzeit eine Zuweisung über das Datenflussmodul erfolgt.  
  
 In diesem Thema werden die benutzerdefinierten Eigenschaften der Pfade, die Datenflussobjekte verbinden, aufgelistet und beschrieben.  
  
### <a name="custom-properties-of-a-path"></a>Benutzerdefinierte Eigenschaften eines Pfads  
 Im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Objektmodell implementiert ein Pfad, der Komponenten im Datenfluss verbindet, die Schnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>.  
  
 Die folgende Tabelle beschreibt die konfigurierbaren Eigenschaften der Pfade in einem Datenfluss. Das Datenflussmodul weist auch zusätzlichen schreibgeschützten Eigenschaften, die nicht hier aufgelistet sind, Werte zu.  
  
|Eigenschaftsname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Ganze Zahl (Enumeration)|Ein Wert, der angibt, ob eine Anmerkung mit dem Pfad auf der Designeroberfläche angezeigt werden soll. Die möglichen Werte sind **AsNeeded**, **SourceName**, **PathName**und **Never**. Der Standardwert ist **AsNeeded**.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|Die dem Pfad zugeordnete Eingabe.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|Die dem Pfad zugeordnete Ausgabe.|  

