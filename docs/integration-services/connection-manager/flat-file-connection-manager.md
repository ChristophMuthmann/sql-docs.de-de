---
title: "Verbindungs-Manager f&#252;r Flatfiles | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verbindungs-Manager [Integration Services], Flatfile"
  - "Verbindungen [Integration Services], Flatfiles"
  - "Dateien [Integration Services], Verbindungen"
  - "Verbindungs-Manager für Flatfiles"
  - "Flatfiles"
  - "Flatfileverbindungen [Integration Services]"
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
caps.latest.revision: 49
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 49
---
# Verbindungs-Manager f&#252;r Flatfiles
  Mit einem Verbindungs-Manager für Flatfiles kann ein Paket auf Daten in einer Flatfile zugreifen. Beispielsweise können die Flatfilequellen und -ziele Verbindungs-Manager für Flatfiles zum Extrahieren und Laden von Daten verwenden.  
  
 Der Verbindungs-Manager für Flatfiles kann nur auf eine einzige Datei zugreifen. Wenn Sie auf mehrere Dateien verweisen möchten, verwenden Sie anstelle eines Verbindungs-Managers für Flatfiles einen Verbindungs-Manager für mehrere Flatfiles. Weitere Informationen finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Spaltenlänge  
 Der Verbindungs-Manager für Flatfiles legt die Länge von Zeichenfolgenspalten standardmäßig auf 50 Zeichen fest. Sie können im Dialogfenster **Verbindungs-Manager-Editor für Flatfiles** Beispieldaten auswerten und automatisch die Länge dieser Spalten ändern, um zu vermeiden, dass die Daten abgeschnitten werden oder die Spaltenbreite überschritten wird. Es sei denn, Sie ändern danach die Spaltenlänge in einer Flatfilequelle oder in einer Transformation. Dann bleibt die Spaltenlänge der Zeichenfolgenspalte im gesamten Datenfluss gleich. Wenn diese Zeichenfolgenspalten Zielspalten zugeordnet sind, die schmaler sind, werden in der Benutzeroberfläche Warnungen angezeigt. Darüber hinaus können aufgrund der abgeschnittenen Daten zur Laufzeit Fehler auftreten. Um Fehler bzw. das Abschneiden von Daten zu vermeiden, können Sie im Verbindungs-Manager für Flatfiles, in der Flatfilequelle oder in einer Transformation die Größe der Spalten auf die Größe der Zielspalten ändern. Legen Sie zum Ändern der Länge von Ausgabespalten auf der Registerkarte **Eingabe- und Ausgabeeigenschaften** im Dialogfeld **Erweiterter Editor** die **Length** -Eigenschaft der Ausgabespalte fest.  
  
 Wenn Sie die Spaltenlängen im Verbindungs-Manager für Flatfiles aktualisieren, nachdem Sie die Flatfilequelle, die den Verbindungs-Manager verwendet, hinzugefügt und geändert haben, ist das manuelle Ändern der Ausgabespaltengröße in der Flatfilequelle nicht erforderlich. Wenn Sie das Dialogfeld **Flatfilequelle** öffnen, stellt die Flatfilequelle eine Option zum Synchronisieren der Spaltenmetadaten bereit.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Konfiguration des Verbindungs-Managers für Flatfiles  
 Wenn Sie einem Paket einen Verbindungs-Manager für Flatfiles hinzufügen, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine Flatfileverbindung aufgelöst wird, die Eigenschaften der Flatfileverbindung festlegt und der **Connections** -Sammlung des Pakets den Verbindungs-Manager für Flatfiles hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **FLATFILE**festgelegt.  
  
 Standardmäßig sucht der Verbindungs-Manager für Flatfiles immer nach einem Zeilentrennzeichen in Daten ohne Anführungszeichen und startet eine neue Zeile, wenn ein Zeilentrennzeichen gefunden wird. Dadurch kann der Verbindungs-Manager für Flatfiles Dateien mit Zeilen, in denen Spaltenfelder fehlen, ordnungsgemäß analysieren.  
  
 In einigen Fällen wird die Paketleistung verbessert, wenn Sie diese Funktion deaktivieren. Sie können diese Funktion deaktivieren, indem Sie die Eigenschaft für den Verbindungs-Manager für Flatfiles von **AlwaysCheckForRowDelimiters**auf **False**festlegen.  
  
 Es gibt folgende Möglichkeiten, um den Verbindungs-Manager für Flatfiles zu konfigurieren:  
  
-   Geben Sie die Datei, das Gebietsschema und die Codepage an, die Sie verwenden möchten. Mithilfe des Gebietsschemas werden gebietsschemabezogene Daten interpretiert, wie z. B. Datumsangaben, und mithilfe der Codepage werden Zeichenfolgendaten in Unicode-Daten konvertiert.  
  
-   Geben Sie das Dateiformat an. Sie können ein Format mit Trennzeichen, fester Breite oder rechtem Flatterrand verwenden.  
  
-   Geben Sie eine Kopfzeile, eine Datenzeile und Spaltentrennzeichen an. Spaltentrennzeichen können auf Dateiebene festgelegt und auf Spaltenebene überschrieben werden.  
  
-   Zeigen Sie an, ob die erste Zeile in der Datei Spaltennamen enthält.  
  
-   Geben Sie ein Textqualifiziererzeichen an. Für jede Spalte kann die Erkennung eines Textqualifizierers konfiguriert werden.  
  
     Die Verwendung eines Qualifiziererzeichens zum Einbetten eines Qualifiziererzeichens in eine qualifizierte Zeichenfolge wird durch den Verbindungs-Manager für Flatfiles unterstützt. Eine doppelte Instanz eines Textqualifizierers wird als literale, einzelne Instanz dieser Zeichenfolge interpretiert. Ist der Textqualifizierer beispielsweise ein einfaches Anführungszeichen, und die Eingabedaten sind 'abc', 'def', 'g'hi', so sind die Ausgabedaten abc, def, g'hi. Eine Instanz eines Textqualifizierers, die in eine qualifizierte Zeichenfolge eingebettet ist, verursacht jedoch den Fehler DTS_E_PRIMEOUTPUTFAILED in der Flatfilequelle.
  
-   Legen Sie Eigenschaften wie z. B. den Namen, den Datentyp und die maximale Breite für einzelne Spalten fest.  
  
 Sie können die ConnectionString-Eigenschaft für den Verbindungs-Manager für Flatfiles festlegen, indem Sie einen Ausdruck im Eigenschaftenfenster von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]angeben. Um einen Überprüfungsfehler zu vermeiden, gehen Sie wie folgt vor.  
  
-   Wenn Sie einen Ausdruck verwenden, um die Datei anzugeben, fügen Sie einen Dateipfad im Feld **Dateiname** unter **Verbindungs-Manager-Editor für Flatfiles**hinzu.  
  
-   Legen Sie die Eigenschaft **DelayValidation** im Verbindungs-Manager für Flatfiles auf **True**fest.  
  
 Sie können einen Ausdruck verwenden, um einen Dateinamen zur Laufzeit zu erstellen, indem Sie den Verbindungs-Manager für Flatfiles mit dem Flatfileziel verwenden.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Allgemein&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)  
  
-   [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Spalten&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)  
  
-   [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Erweitert&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)  
  
-   [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Vorschau&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
  