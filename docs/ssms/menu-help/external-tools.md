---
title: Externe Tools | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vs.externaltools
helpviewer_keywords: External Tools dialog box
ms.assetid: d7dae88f-0781-4162-96cd-d3a3a4d82035
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07746b7c20e8bed6bb71abb3c62adb6354f921dd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="external-tools"></a>Externe Tools
Verwenden Sie dieses Dialogfeld, um dem Menü **Extras** externe Tools hinzuzufügen, z. B. SQL Server-Konfigurations-Manager oder Editor. Durch das Hinzufügen externer Tools erleichtern Sie das Starten anderer Anwendungen während der Arbeit mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Sie können beim Starten des Tools Argumente und ein Arbeitsverzeichnis angeben. Zusätzlich können die Ausgaben einiger Tools im Ausgabefenster angezeigt werden. Das Dialogfeld **Externe Tools** wird über das Menü **Extras** aufgerufen.  
  
## <a name="options"></a>enthalten  
**Menüinhalt**  
Führt die Titel der Elemente auf, die aktuell dem Menü **Extras** hinzugefügt sind. Verwenden Sie die Schaltflächen **Nach oben** und **Nach unten** , um die Reihenfolge zu ändern, in der die Elemente im Menü angezeigt werden. Verwenden Sie die Schaltfläche **Löschen** , um ein Element aus dem Menü zu entfernen.  
  
**Nach oben**  
Verschiebt das ausgewählte Tool innerhalb der Liste der Tools im Menü **Extras** nach oben.  
  
**Nach unten**  
Verschiebt das ausgewählte Tool innerhalb der Liste der Tools im Menü **Extras** nach unten.  
  
**Hinzufügen**  
Löscht die Textfelder, sodass Sie ein neues Tool angeben können.  
  
**Löschen**  
Entfernt das Tool oder den Befehl aus der Liste **Menüinhalt** und aus dem Menü **Extras** .  
  
**Titel**  
Der Name des Tools oder Befehls, der im Untermenü **Externe Tools** des Menüs **Extras** angezeigt wird. Setzen Sie ein kaufmännisches Und-Zeichen vor einen Buchstaben im Namen des Tools, um diesen Buchstaben als Zugriffstaste für das Tool zu verwenden. Der Eintrag `&Spy++` würde beispielsweise als **Spy++** im Menü **Extras** angezeigt.  
  
**Befehl**  
Gibt den Pfad zu der Datei mit der Endung EXE, COM, PIF, BAT, CMD oder einer anderen Datei an, die gestartet werden soll. Die Ausgabe von `.bat`-, `.com`- und anderen Dateien kann im Ausgabefenster angezeigt werden, wenn Sie das Kontrollkästchen **Ausgabefenster verwenden** aktivieren.  
  
**Argumente**  
Gibt die Variablen an, die an das Tool übergeben werden, wenn es im Menü aufgerufen wird. Argumente können Werte festlegen, die beim Starten an das Tool oder den Befehl übergeben werden. Ein Wert kann beispielsweise einen Dateinamen oder ein Verzeichnis angeben. Verwenden Sie die **Pfeil** Schaltfläche, um aus einer Liste vordefinierter Argumente eines auszuwählen. Sie können mehrere Argumente hinzufügen. Eine vollständige Liste vordefinierter Argumente und ihrer Definitionen finden Sie unter [Arguments for External Tools](../../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md). Außerdem können Sie benutzerdefinierte Argumente (z. B. Befehlszeilenoptionen) eingeben, je nach verwendetem Befehl bzw. Tool.  
  
**Ausgangsverzeichnis**  
Gibt das Arbeitsverzeichnis für das Tool an. Verwenden Sie die **Pfeil** -Schaltfläche, um die Verzeichnisse auszuwählen. Sie können mehrere Verzeichnisse auswählen.  
  
**Use output Window**  
Gibt an, ob die Ergebnisse des Tools im Ausgabefenster angezeigt werden sollen oder nicht. Diese Option ist nur für Dateien verfügbar, die normalerweise eine Ausgabe im Befehlszeilenfenster anzeigen (z. B. BAT- und COM-Dateien). Ist sie aktiviert, vereinfacht diese Option die Fensterverwaltung beim Verfolgen der Fortschritte eines Tools.  
  
**Zur Argumenteingabe auffordern**  
Zeigt das Dialogfeld **Argumente** an, mit dem Sie Werte für die Argumente jedes Mal eingeben oder bearbeiten können, wenn Sie das externe Tool starten.  
  
**Ausgabe als Unicode behandeln**  
Ermöglicht dem Ausgabefenster die Annahme von Unicode.  
  
**Nach Beenden schließen**  
Schließt das vom Fenster geöffnete Tool, wenn das Tool geschlossen wird.  
  
## <a name="example"></a>Beispiel  
  
#### <a name="to-add-sql-server-configuration-manager-to-the-tools-menu"></a>So fügen Sie „SQL Server-Konfigurations-Manager“ dem Menü „Extras“ hinzu  
  
1.  Klicken Sie im Menü **Extras** auf **Externe Tools**.  
  
2.  Geben Sie in das Feld **Titel** den Titel **SQL Server-Konfigurations-Manager**ein.  
  
3.  Geben Sie in das Feld **Befehl** den Pfad zur ausführbaren Datei von [!INCLUDE[msCoName](../../includes/msconame_md.md)] Management Console ein, z. B. **C:\WINNT\system32\mmc.exe**.  
  
4.  Geben Sie in das Feld **Argumente** den Pfad zur MSC-Datei ein, z. B. **C:\WINNT\system32\SQLServerManager.msc**.  
  
> [!NOTE]  
> Zeigen Sie die Eigenschaften der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] -Verknüpfung im **Startmenü** an, um den Speicherort der Dateien auf dem Computer zu überprüfen.  
  
