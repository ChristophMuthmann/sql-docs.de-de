---
title: Detailbereich des Objekt-Explorers | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.summary.general.f1
- sql13.swb.summary.report.f1
helpviewer_keywords:
- object search [SQL Server], Object Explorer
- Object Explorer
- object search [SQL Server]
- searching objects [SQL Server]
ms.assetid: b963e3c2-dc9e-4d38-bd28-2e00fe9e0e47
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4a6a6ac677e6c084015b0d562f9382b53c2d9b0c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="object-explorer-details-pane"></a>Detailbereich des Objekt-Explorers
Details zum Objekt-Explorer, eine Komponente von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], stellt eine tabellarische Ansicht aller Objekte im Server sowie eine Benutzeroberfläche zu deren Verwaltung bereit. Die Funktionalität des Objekt-Explorers variiert abhängig vom Servertyp, enthält aber im Allgemeinen die Entwicklungsfunktionen für Datenbanken und die Verwaltungsfunktionen für alle Servertypen.  
  
Der Bereich Details zum Objekt-Explorer ist standardmäßig in [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] sichtbar. Wenn der Objekt-Explorer nicht angezeigt wird, klicken Sie im Menü **Ansicht** auf **Details zum Objekt-Explorer** , oder drücken Sie **F7**.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] zeigt Datumsangaben gemäß der Einstellung in den Regions- und Sprachoptionen von Microsoft Windows beim Starten von [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] an. Starten Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] neu, um die neuen Einstellungen wiederzugeben.  
  
## <a name="object-explorer-details"></a>Details zum Objekt-Explorer  
Mithilfe von Details zum Objekt-Explorer können Sie in Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz durch Ordner und Objekte navigieren. Bei 32-Bit-Betriebssystemen kann der Objekt-Explorer nur 64.000 Objekte anzeigen. Um auf zusätzliche Objekte zuzugreifen, muss ein Symbol ausgewählt werden.  
  
Details zum Objekt-Explorer verfügt über eine Symbolleiste, die die in der folgenden Tabelle beschriebenen Symbole enthält. Die Symbole sind nur verfügbar, wenn die entsprechenden Aktionen anwendbar sind.  
  
|Symbol|Aktion|  
|--------|----------|  
|**Zurück**|Wechselt zu den vorherigen in Details zum Objekt-Explorer angezeigten Elementen. Wiederholt eine Suche, wenn die vorherige Anzeige das Ergebnis eines Suchvorgangs ist.|  
|**Vorwärts**|Wechselt zum nächsten Bildschirm, nachdem eine **Zurück** -Aktion ausgewählt wurde.|  
|**Nach oben**|Wechselt zum übergeordneten Objekt oder Ordner.|  
|**Synchronisieren**|Legt den Fokus von Objekt-Explorer auf das in Details zum Objekt-Explorer ausgewählte Objekt fest.|  
|**Filter**|Zeigt, soweit verfügbar, eine konfigurierbare Teilmenge von Objekten an.|  
|**Aktualisieren**|Aktualisiert die Anzeige in Details zum Objekt-Explorer.|  
|**Suchen**|Stellt einen Bereich bereit, um einen Suchbegriff für bestimmte Datenbankobjekte einzugeben.|  
  
### <a name="column-header-selections"></a>Spaltenheaderauswahl  
Details zum Objekt-Explorer verfügt über auswählbare Spalten. Sie können in jedem Spaltenheader mit der rechten Maustaste klicken und die Elemente aktivieren, die Sie anzeigen möchten. Ihre Auswahl wird für alle Objekte, durch die Sie navigieren, beibehalten. Die Auswahl wird für jeden Benutzer individuell beibehalten, wenn [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]beendet und neu gestartet wird.  
  
> [!CAUTION]  
> Wenn bei einigen Objekttypen (wie z. B. Datenbanken) alle Spalten angezeigt werden, kann das Rendering der Anzeige bei großen Objektsätzen geringfügig verlangsamt werden.  
  
### <a name="sorting"></a>Sortierung  
Wenn Sie auf einen Spaltenheader einmal klicken, erfolgt eine Sortierung nach dieser Spalte. Wenn Sie auf denselben Header erneut klicken, erfolgt eine umgekehrte Sortierung nach dieser Spalte. Die Sortierauswahl wird für jeden Benutzer für alle Objekte und Ordner sowie für den Neustart von [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] beibehalten.  
  
### <a name="filtering"></a>Filterung  
Bestimmte Listen von Objekten, die in Details zum Objekt-Explorer angezeigt werden, können mithilfe des **Filter** -Symbols auf der Symbolleiste „Details“ zum Objekt-Explorer gefiltert werden. Das Symbol wird aktiviert, wenn eine Filterung möglich ist.  
  
### <a name="details-pane"></a>Detailbereich  
Am unteren Rand von Details zum Objekt-Explorer befindet sich ein Bereich, in dem bestimmte Details des ausgewählten Objekts angezeigt werden. Bei einer Mehrfachauswahl von Objekten wird nur die Anzahl der Objekte angezeigt. Wenn in dem Bereich Elemente ausgewählt sind, können Sie auf das **Kopieren** -Symbol klicken, um den angezeigten Text in die Zwischenablage zu kopieren.  
  
Mit der NACH-UNTEN-TASTE wird die Auswahl in das nächste Listenelement verschoben. Mit der NACH-OBEN-TASTE wird die Auswahl in das vorherige Listenelement verschoben. Wenn Sie die Pfeiltaste gedrückt halten, können Sie die Elemente schneller durchlaufen. Die Auswahl wird am Anfang oder Ende der Eigenschaftenliste angehalten.  
  
Wenn Sie das erste Zeichen eines Eigenschaftennamens eingeben, wird die Auswahl in die nächste Eigenschaft verschoben, die mit diesem Zeichen beginnt.  
  
Wenn Eigenschaften in mehreren Spalten angeordnet werden, bewegen Sie ein Element mithilfe der NACH-LINKS-TASTE und NACH-RECHTS-TASTE in angrenzende Spalten.  
  
Um Eigenschaftswerte in die Zwischenablage zu kopieren, verwenden Sie die folgenden Tastenkombinationen:  
  
-   STRG+C kopiert den Eigenschaftswert.  
  
-   STRG+UMSCHALT+C kopiert den Eigenschaftennamen und den Eigenschaftswert mit einem als Trennzeichen verwendeten Tabstoppzeichen.  
  
Verwenden Sie das Kontextmenü im Eigenschaftenbereich Details zum Objekt-Explorer, um alle Eigenschaften bzw. alle Eigenschaften und Namen in die Zwischenablage zu kopieren.  
  
Um einen Eigenschaftswert anzuzeigen, wenn er die Breite des Felds überragt, zeigen Sie mit dem Mauscursor auf den Wert oder legen den Benutzeroberflächenfokus auf den Eigenschaftswert fest, um eine QuickInfo mit dem gesamten Eigenschaftswert zu aktivieren. Barrierefreie Sprachausgaben melden den vollständigen Eigenschaftswert, wenn der Benutzer auf den langen Eigenschaftswert fokussiert.  
  
Wenn die Anzahl von Eigenschaften im Eigenschaftenbereich die Anzahl übersteigt, die in den Inhaltsbereich passt, wird auf der rechten Seite des Eigenschaftenbereichs eine Bildlaufleiste angezeigt. Passen Sie die Ansicht der Eigenschaftswerte im Inhaltsbereich mithilfe der Bildlaufleiste ein.  
  
### <a name="multiple-object-selection"></a>Mehrfachauswahl von Objekten  
Details zum Objekt-Explorer unterstützt die Mehrfachauswahl von Objekten. Wenn Sie beispielsweise Tabellen im Objekt-Explorer auswählen, können Sie bei gedrückter **STRG** -TASTE im Fenster „Details zum Objekt-Explorer“ mehrere Tabellen auswählen, mit der rechten Maustaste darauf klicken und dann **Löschen** oder **Skript für Tabelle als** wählen, um diese Befehle sofort für alle ausgewählten Tabellen auszuführen. Mit den standardmäßigen Befehlen zum Kopieren wird der angezeigte Text in die Zwischenablage kopiert.  
  
## <a name="sql-server-object-search"></a>SQL Server-Objektsuche  
Platzhalter  
  
-   Standardmäßige Platzhalterzeichen werden unterstützt. Beispielsweise gibt eine Suche nach **dm_os%counters** die beiden Ergebnisse „dm_os_memory_cache_counters“ und „dm_os_performance_counters“ zurück. Weitere Informationen finden Sie unter [Vorgehensweise: Suchen mit Platzhaltern](http://msdn.microsoft.com/en-us/449600f8-cc87-4b3f-878a-59c158a88a40).  
  
Suchbereich  
  
-   Jede Suche ist auf den aktuellen Fokus in der Strukturansicht des Objekt-Explorers begrenzt. Befindet sich der Fokus des Objekt-Explorers z. B. auf einer Datenbank, gibt eine Suche nach **dm_os%counters** die Ergebnisse „dm_os_memory_cache_counters“ und „dm_os_performance_counters“ in dieser Datenbank zurück. Befindet sich der Fokus des Objekt-Explorers auf dem Knoten Datenbanken, werden alle Datenbanken durchsucht und mehrere Instanzen der dynamischen Sichten zurückgegeben.  
  
Große Objektsätze  
  
-   Das Durchsuchen von großen Objektsätzen kann einige Zeit in Anspruch nehmen und die Serverleistung verringern.  
  
## <a name="see-also"></a>Siehe auch  
[Objekt-Explorer](../../ssms/object/object-explorer.md)  
  

