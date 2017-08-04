---
title: "Verbindungs-Manager für mehrere Flatfiles | Microsoft Docs"
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
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 04900b28471f2dc4b0eb7d06fcc7f0c5acf69468
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="multiple-flat-files-connection-manager"></a>Verbindungs-Manager für mehrere Flatfiles
  Mit einem Verbindungs-Manager für mehrere Flatfiles kann ein Paket auf Daten in mehreren Flatfiles zugreifen. Eine Flatfilequelle kann beispielsweise einen Verbindungs-Manager für mehrere Flatfiles verwenden, wenn sich der Datenflusstask in einem Schleifencontainer wie dem For-Schleifencontainer befindet. In jeder Schleife des Containers werden von der Flatfilequelle Daten vom nächsten Dateinamen geladen, der vom Verbindungs-Manager für mehrere Flatfiles bereitgestellt wird.  
  
 Wenn Sie einem Paket einen Verbindungs-Manager für mehrere Flatfiles hinzufügen, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine Verbindung für mehrere Flatfiles aufgelöst wird, die Eigenschaften im Verbindungs-Manager für mehrere Flatfiles festlegt und der **Connections** -Sammlung des Pakets die Verbindung für mehrere Flatfiles hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **MULTIFLATFILE**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um einen Verbindungs-Manager für mehrere Flatfiles zu konfigurieren:  
  
-   Geben Sie die Dateien, das Gebietsschema und die Codepage an, die Sie verwenden möchten. Mithilfe des Gebietsschemas werden gebietsschemabezogene Daten interpretiert, wie z. B. Datumsangaben, und mithilfe der Codepage werden Zeichenfolgendaten in Unicode-Daten konvertiert.  
  
-   Geben Sie das Dateiformat an. Sie können ein Format mit Trennzeichen, fester Breite oder rechtem Flatterrand verwenden.  
  
-   Geben Sie eine Kopfzeile, eine Datenzeile und Spaltentrennzeichen an. Spaltentrennzeichen können auf Dateiebene festgelegt und auf Spaltenebene überschrieben werden.  
  
-   Zeigen Sie an, ob die erste Zeile in den Dateien Spaltennamen enthalten.  
  
-   Geben Sie ein Textqualifiziererzeichen an. Für jede Spalte kann die Erkennung eines Textqualifizierers konfiguriert werden.  
  
-   Legen Sie Eigenschaften wie z. B. den Namen, den Datentyp und die maximale Breite für einzelne Spalten fest.  
  
 Wenn der Verbindungs-Manager für mehrere Flatfiles auf mehrere Dateien verweist, werden die Pfade der Dateien durch einen senkrechten Strich (|) getrennt. Die **ConnectionString** -Eigenschaft des Verbindungs-Managers hat folgendes Format:  
  
 \<*Pfad*>|\<*Pfad*>  
  
 Mehrere Dateien können Sie auch mithilfe von Platzhalterzeichen angeben. Wenn z.B. auf alle Textdateien auf Laufwerk C verwiesen werden soll, kann der Wert der **ConnectionString** -Eigenschaft auf C:\\*.txt festgelegt werden.  
  
 Falls ein Verbindungs-Manager für Flatfiles auf mehrere Dateien verweist, müssen alle Dateien das gleiche Format aufweisen.  
  
 Der Verbindungs-Manager für mehrere Flatfiles legt die Länge von Zeichenfolgenspalten standardmäßig auf 50 Zeichen fest. Sie können im Dialogfenster **Verbindungs-Manager-Editor für mehrere Flatfiles** Beispieldaten auswerten und automatisch die Länge dieser Spalten ändern, um zu vermeiden, dass Daten abgeschnitten werden oder die Spaltenbreite überschritten wird. Es sei denn, Sie ändern die Spaltenlänge in einer Flatfilequelle oder in einer Transformation. Dann bleibt die Spaltenlänge der Zeichenfolgenspalte im gesamten Datenfluss gleich. Wenn diese Spalten Zielspalten zugeordnet sind, die schmaler sind, werden in der Benutzeroberfläche Warnungen angezeigt. Darüber hinaus können aufgrund der abgeschnittenen Daten zur Laufzeit Fehler angezeigt werden. Sie können im Verbindungs-Manager für Flatfiles, in der Flatfilequelle oder in einer Transformation die Größe der Spalten auf die Größe der Zielspalten ändern. Legen Sie zum Ändern der Länge von Ausgabespalten auf der Registerkarte **Eingabe- und Ausgabeeigenschaften** im Dialogfeld **Erweiterter Editor** die **Length** -Eigenschaft der Ausgabespalte fest.  
  
 Wenn Sie die Spaltenlängen im Verbindungs-Manager für mehrere Flatfiles aktualisieren, nachdem Sie die Flatfilequelle, die den Verbindungs-Manager verwendet, hinzugefügt und geändert haben, ist das manuelle Ändern der Ausgabespaltengröße in der Flatfilequelle nicht erforderlich. Wenn Sie das Dialogfeld **Flatfilequelle** öffnen, stellt die Flatfilequelle eine Option zum Synchronisieren der Spaltenmetadaten bereit.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>Konfiguration des Verbindungs-Managers für mehrere Flatfiles  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Allgemein“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)  
  
-   [Verbindungs-Manager-Editor für mehrere Flatfiles &#40; Seite "Spalten" &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)  
  
-   [Verbindungs-Manager-Editor für mehrere Flatfiles &#40; Seite "Erweitert" &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)  
  
-   [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Vorschau“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und unter [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
## <a name="see-also"></a>Siehe auch  
 [Flatfilequelle](../../integration-services/data-flow/flat-file-source.md)   
 [Flatfileziel](../../integration-services/data-flow/flat-file-destination.md)   
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
