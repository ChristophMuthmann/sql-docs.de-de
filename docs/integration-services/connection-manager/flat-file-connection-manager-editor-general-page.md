---
title: Flatfile-Verbindungs-Manager-Editor (Seite Allgemein) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.ffileconnection.general.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 77296024-5c1a-4f6a-9665-0b50d45d744c
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e94228deef3c278239cc9f24026677a175d3a65
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-connection-manager-editor-general-page"></a>Verbindungs-Manager-Editor für Flatfiles (Seite Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Verbindungs-Manager-Editor für Flatfiles** wählen Sie eine Datei und ein Dateiformat aus. Eine Flatfileverbindung ermöglicht das Herstellen einer Verbindung von einem Paket zu einer Textdatei.  
  
 Weitere Informationen zum Verbindungs-Manager für Flatfiles finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
## <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Flatfileverbindung im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Es ist eine bewährte Methode, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und einfacher zu verwalten sind.  
  
 **Dateiname**  
 Geben Sie den Pfad und den Dateinamen ein, die für die Flatfileverbindung verwendet werden sollen.  
  
 **Durchsuchen**  
 Suchen Sie den Dateinamen, der für die Flatfileverbindung verwendet werden soll.  
  
 **Gebietsschema**  
 Gibt das Gebietsschema für die Bereitstellung sprachspezifischer Informationen für das Bestellen sowie für Datums- und Zeitformate an.  
  
 **Unicode**  
 Gibt an, ob Unicode verwendet werden soll. Wenn Sie Unicode verwenden, können Sie keine Codepage angeben.  
  
 **Codepage**  
 Gibt die Codepage für Nicht-Unicode-Text an.  
  
 **Format**  
 Gibt an, ob die Datei Formatierung mit Trennzeichen, fester Breite oder rechtem Flatterrand verwendet.  
  
|Wert|Description|  
|-----------|-----------------|  
|Mit Trennzeichen|Die Trennung von Spalten erfolgt durch Trennzeichen. Welche Trennzeichen dies sind, wird auf der Seite **Spalten** angegeben.|  
|Feste Breite|Spalten haben eine feste Breite.|  
|Rechter Flatterrand|Bei Dateien mit rechtem Flatterrand haben die Spalten mit Ausnahme der letzten Spalte eine feste Breite. Die Trennung der letzten Spalte erfolgt mit einem Zeilentrennzeichen.|  
  
 **Textqualifizierer**  
 Gibt die zu verwendenden Textqualifizierer an. So können Sie beispielsweise angeben, dass Textfelder in Anführungszeichen eingeschlossen sind.  
  
> [!NOTE]  
>  Nachdem Sie einen Textqualifizierer ausgewählt haben, können Sie die Option **Keine** nicht erneut auswählen. Geben Sie **Keine** ein, um die Auswahl des Textqualifizierers aufzuheben.  
  
 **Kopfzeilentrennzeichen**  
 Wählen Sie aus einer Liste mit Trennzeichen für Kopfzeilen ein Trennzeichen aus, oder geben Sie den Trennzeichentext ein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Als Trennzeichen für Kopfzeilen dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Als Trennzeichen für Kopfzeilen dient ein Wagenrücklauf.|  
|**{LF}**|Als Trennzeichen für Kopfzeilen dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Kopfzeilen dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Kopfzeilen dient ein Doppelpunkt.|  
|**Komma {,}**|Als Trennzeichen für Kopfzeilen dient ein Komma.|  
|**Tabulator {t}**|Als Trennzeichen für Kopfzeilen dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Kopfzeilen dient ein senkrechter Strich.|  
  
 **Auszulassende Kopfzeilen**  
 Gibt an, wie viele Kopfzeilen bzw. erste Datenzeilen ggf. ausgelassen werden sollen.  
  
 **Spaltennamen in der ersten Datenzeile**  
 Gibt an, ob in der ersten Datenzeile Spaltennamen erwartet werden bzw. bereitzustellen sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)   
 [Flatfile-Verbindungs-Manager-Editor &#40; Seite "Spalten" &#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)   
 [Flatfile-Verbindungs-Manager-Editor &#40; Seite "Erweitert" &#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)   
 [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Vorschau&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
  
