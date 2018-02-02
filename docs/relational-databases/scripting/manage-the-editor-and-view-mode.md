---
title: Verwalten des Editors und Ansichtsmodus | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], managing window behavior
- workbench view modes [SQL Server Management Studio]
- full screen mode [SQL Server Management Studio]
- fonts [SQL Server Management Studio]
- word wraps [SQL Server Management Studio]
- virtual space mode [SQL Server Management Studio]
- splitting document views
- displaying line numbers
- view modes [SQL Server Management Studio]
ms.assetid: 25c58a14-9f94-4296-9770-7d84c6bc3969
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bc33a7d686cd91cb502ac37c0c1ab4ef267ff872
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="manage-the-editor-and-view-mode"></a>Verwalten des Editors und des Ansichtsmodus
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Der Editor bietet mehrere Möglichkeiten, die Ansicht des Codes zu steuern.  
  
## <a name="changing-the-view-mode"></a>Ändern des Ansichtsmodus  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügt über einen Ansichtsmodus namens **Dokumente im Registerformat**. In diesem Modus können Sie mehrere Editoren und Dokumente gleichzeitig öffnen und über Registerkarten am oberen Rand des Editors auf diese zugreifen. Alternativ können Sie die [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] -Umgebung im Modus für eine mehrfache Dokumentschnittstelle (MDI, Multiple Document Interface) öffnen, bei dem Fenster ohne Registerkarten verknüpft werden und nebeneinander angezeigt, minimiert oder ähnlich behandelt werden können.  
  
#### <a name="to-switch-between-view-modes"></a>So wechseln Sie den Ansichtsmodus  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen** .  
  
2.  Klicken Sie auf **Umgebung**. Klicken Sie auf **Allgemein**.  
  
3.  Klicken Sie auf **Dokumente im Registerformat** oder **MDI-Umgebung**.  
  
    > [!NOTE]  
    >  Die Änderungen werden erst beim Neustart von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] wirksam.  
  
## <a name="splitting-the-view"></a>Teilen der Ansicht  
 Ein Editor-Fenster kann zum einfacheren Bearbeiten in zwei Teile geteilt werden.  
  
#### <a name="to-split-a-window"></a>So teilen Sie ein Fenster  
  
1.  Klicken Sie auf die Teilerleiste (über der Bildlaufleiste).  
  
2.  Ziehen Sie die Teilerleiste nach unten.  
  
3.  Um wieder zu einem einzelnen Bereich zu wechseln, doppelklicken Sie auf die Teilerleiste zwischen den beiden Bereichen.  
  
 Der neue Bereich enthält dasselbe Dokument. Alle Änderungen in einem Bereich werden auch im anderen Bereich wiedergegeben, sofern dieser Bereich dieselbe Stelle im Dokument anzeigt.  
  
## <a name="word-wrap"></a>Zeilenumbruch  
 Wenn Sie den Zeilenumbruch aktivieren, wird die horizontale Bildlaufleiste entfernt, und Codezeilen, die die Breite des Editor-Fensters überschreiten, werden automatisch in die nächste angezeigte Zeile umgebrochen, während sie sonst durch einen Bildlauf nach rechts vollständig angezeigt werden können.  
  
#### <a name="to-activate-word-wrap"></a>So aktivieren Sie den Zeilenumbruch  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen** .  
  
2.  Klicken Sie auf **Text-Editor**.  
  
3.  Öffnen Sie den entsprechenden Sprachordner (oder **Alle Sprachen** , wenn alle Sprachen betroffen sein sollen).  
  
4.  Wählen Sie **Zeilenumbruch**.  
  
## <a name="enabling-virtual-space-mode"></a>Aktivieren des Modus des virtuellen Bereichs  
 Im Modus des **virtuellen Bereichs** verhält sich der Editor, als ob der Bereich nach dem Zeilenende mit einer unendlichen Anzahl von Leerzeichen gefüllt wäre, sodass Codezeilen außerhalb des sichtbaren Bildschirmbereichs fortgesetzt werden können.  
  
#### <a name="to-enable-virtual-space-mode"></a>So aktivieren Sie den Modus des virtuellen Bereichs  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen** .  
  
2.  Klicken Sie auf **Text-Editor**.  
  
3.  Öffnen Sie den entsprechenden Sprachordner (oder **Alle Sprachen** , wenn alle Sprachen betroffen sein sollen).  
  
4.  Wählen Sie **Virtuellen Bereich aktivieren**aus.  
  
 Wenn der Modus des virtuellen Bereichs nicht aktiviert ist, bricht die Zeile am Ende mit dem ersten Zeichen der nächsten Zeile um und umgekehrt.  
  
## <a name="displaying-line-numbers"></a>Anzeigen von Zeilennummern  
 Sie können Zeilennummerierung für den Code aktivieren. Zeilennummern sind hilfreich zum Navigieren im Code. Weitere Informationen finden Sie unter [Navigieren in Code und Text](../../relational-databases/scripting/navigate-code-and-text.md).  
  
> [!NOTE]  
>  Das Aktivieren der Zeilennummerierung bedeutet nicht, dass das Dokument mit Zeilennummern gedruckt wird. Zum Drucken von Zeilennummern müssen Sie im Menü **Datei** im Befehl **Seite einrichten** das Kontrollkästchen **Zeilennummern** aktivieren.  
  
#### <a name="to-display-line-numbers-in-code"></a>So zeigen Sie Code mit Zeilennummern an  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen** .  
  
2.  Klicken Sie auf **Text-Editor**.  
  
3.  Klicken Sie auf **Alle Sprachen**.  
  
4.  Klicken Sie auf **Allgemein**.  
  
5.  Wählen Sie **Zeilennummern**aus.  
  
 Wenn Sie die Zeilennummerierung nur für einige Programmiersprachen angeben möchten, wählen Sie **Zeilennummern** nur in bestimmten Ordnern aus.  
  
## <a name="enabling-full-screen-mode"></a>Aktivieren des Vollbildmodus  
 Durch Aktivieren des Vollbildmodus können Sie alle Toolfenster ausblenden und nur Dokumentfenster anzeigen.  
  
#### <a name="to-enable-full-screen-mode"></a>So aktivieren Sie den Vollbildmodus  
  
1.  Drücken Sie ALT+UMSCHALT+EINGABE, um den Vollbildmodus umzuschalten.  
  
## <a name="using-auto-hide-all"></a>Verwenden der automatischen Ausblendung  
  
#### <a name="to-hide-all-the-tool-windows-at-once"></a>So blenden Sie alle Toolfenster gleichzeitig aus  
  
1.  Wählen Sie im Menü **Fenster** die Option **Alle automatisch ausblenden** .  
  
  
