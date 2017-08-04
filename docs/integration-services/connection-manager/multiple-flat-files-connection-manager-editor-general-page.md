---
title: "Verbindungs-Manager-Editor (Seite Allgemein) für mehrere Flatfiles | Microsoft Docs"
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
- sql13.dts.designer.multifile.general.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: 00129d43-2772-413b-bdf8-ac5de81cf4a5
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84e8e23d349266c6c1195a10410085654548c64f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="multiple-flat-files-connection-manager-editor-general-page"></a>Verbindungs-Manager-Editor für mehrere Flatfiles (Seite Allgemein)
  Um eine Gruppe von Dateien im selben Datenformat auszuwählen und das entsprechende Datenformat anzugeben, verwenden Sie im Dialogfeld **Verbindungs-Manager-Editor für mehrere Flatfiles** die Seite **Allgemein** . Durch eine Verbindung für mehrere Flatfiles kann von einem Paket eine Verbindung zu einer Gruppe von Textdateien im selben Format hergestellt werden.  
  
 Weitere Informationen zum Verbindungs-Manager für mehrere Flatfiles finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Verbindung für mehrere Flatfiles im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Die bewährte Methode ist hierbei, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **Dateinamen**  
 Geben Sie den Pfad und den Dateinamen ein, die für die Verbindung für mehrere Flatfiles verwendet werden sollen. Verwenden Sie zum Angeben mehrerer Dateien Platzhalterzeichen, wie in „C:\\*.txt“, oder verwenden Sie den senkrechten Strich (|), um die verschiedenen angegebenen Dateinamen voneinander zu trennen. Alle Dateien müssen dasselbe Datenformat aufweisen.  
  
 **Durchsuchen**  
 Wechseln Sie in das Verzeichnis mit den Dateinamen, die bei der Verbindung für mehrere Flatfiles verwendet werden sollen. Sie können mehrere Dateien auswählen. Alle Dateien müssen dasselbe Datenformat aufweisen.  
  
 **Gebietsschema**  
 Geben Sie den Ort an, um Informationen zu Bestellungen und zur Datums- und Zeitkonvertierung bereitzustellen.  
  
 **Unicode**  
 Gibt an, ob Unicode verwendet werden soll. Bei Verwendung von Unicode wird keine Codepage angegeben.  
  
 **Codepage**  
 Gibt die Codepage für Nicht-Unicode-Text an.  
  
 **Format**  
 Gibt an, ob die Datei Formatierung mit Trennzeichen, fester Breite oder rechtem Flatterrand verwendet. Alle Dateien müssen dasselbe Datenformat aufweisen.  
  
|Wert|Description|  
|-----------|-----------------|  
|Mit Trennzeichen|Die Trennung von Spalten erfolgt durch Trennzeichen. Welche Trennzeichen dies sind, wird auf der Seite **Spalten** angegeben.|  
|Feste Breite|Die Spalten weisen eine feste Breite auf, die auf der Seite **Spalten** durch Ziehen der Markierungslinien angegeben wird.|  
|Rechter Flatterrand|Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das auf der Seite **Spalten** angegebene Zeilentrennzeichen begrenzt.|  
  
 **Textqualifizierer**  
 Gibt die zu verwendenden Textqualifizierer an. Sie können beispielsweise angeben, dass Text in Anführungszeichen eingeschlossen werden soll.  
  
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
 Geben Sie nach Möglichkeit die Anzahl der auszulassenden Kopfzeilen an.  
  
 **Spaltennamen in der ersten Datenzeile**  
 Gibt an, ob in der ersten Datenzeile Spaltennamen erwartet werden bzw. bereitzustellen sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Verbindungs-Manager-Editor für mehrere Flatfiles &#40; Seite "Spalten" &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [Verbindungs-Manager-Editor für mehrere Flatfiles &#40; Seite "Erweitert" &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [Verbindungs-Manager-Editor für mehrere Flatfiles &#40; Seite "Datenvorschau" &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
