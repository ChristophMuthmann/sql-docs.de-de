---
title: Funktionen in SQL Server Management Studio | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], about SQL Server Management Studio
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: e75504b9-7968-4e3b-8411-fd79fe09021e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82a8f1c09d51ad35b9d61e68b6878dc90b7d617c
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="features-in-sql-server-management-studio"></a>Funktionen in SQL Server Management Studio
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] enthält die folgenden allgemeinen Funktionen:  
  
-   Unterstützt die meisten Verwaltungsaufgaben für [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)].  
  
-   Eine einzelne integrierte Umgebung für die [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)] -Verwaltung und -Berichterstellung.  
  
-   Dialogfelder zum Verwalten von Objekten in [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)]und [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)]. Auf diese Weise können Sie Aktionen unmittelbar ausführen, an einen Code-Editor senden oder ein Skript zur späteren Ausführung erstellen.  
  
-   Nicht modale Dialogfelder und Dialogfelder mit veränderbarer Größe ermöglichen den Zugriff auf verschiedene Tools bei geöffnetem Dialogfeld.  
  
-   Mit einem allgemeinen Planungsdialogfeld können Sie Aktionen in den Verwaltungsdialogfeldern zu einem späteren Zeitpunkt ausführen.  
  
-   Exportieren und Importieren der [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] -Serverregistrierung aus einer [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] -Umgebung in eine andere.  
  
-   Sie können XML-Showplan- oder Deadlockdateien speichern oder drucken, die von SQL Server Profiler generiert wurden, später überprüfen oder zur Analyse an Administratoren senden.  
  
-   Ein neues Fehler- und Informationsmeldungsfeld bietet deutlich mehr Informationen und ermöglicht Ihnen, [!INCLUDE[msCoName](../includes/msconame_md.md)] einen Kommentar zur Meldung zu senden, Meldungen in die Zwischenablage zu kopieren und die Meldungen auf einfache Weise per E-Mail an das Supportteam zu senden.  
  
-   Ein integrierter Webbrowser zum schnellen Durchsuchen von MSDN oder der Onlinehilfe.  
  
-   Integration von Hilfe aus Onlinecommunities.  
  
-   Ein Lernprogramm zu [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] hilft Ihnen, die vielen neuen Funktionen optimal zu nutzen und umgehend produktiver zu werden.  
  
-   Ein neuer Aktivitätsmonitor mit Funktionen zum Filtern und automatischen Aktualisieren.  
  
-   Integrierte Schnittstellen für Datenbank-E-Mail.  
  
## <a name="new-scripting-capabilities"></a>Neue Skripterstellungsfunktionen  
Der Code-Editor in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] enthält integrierte Skript-Editoren zum Erstellen von [!INCLUDE[tsql](../includes/tsql_md.md)], MDX, DMX, und XML/A. Es stehen folgende Funktionen zur Verfügung:  
  
-   Die dynamische Hilfe für den direkten Zugriff auf wichtige Informationen während der Arbeit.  
  
-   Ein funktionsreicher Satz an Vorlagen und die Möglichkeit, benutzerdefinierte Vorlagen zu erstellen.  
  
-   Unterstützung für das Schreiben und Bearbeiten von Abfragen oder Skripts ohne Verbindung mit einem Server.  
  
-   Unterstützung der Skripterstellung für SQLCMD-Abfragen und -Skripts.  
  
-   Eine neue Benutzeroberfläche zum Anzeigen von XML-Ergebnissen.  
  
-   Integrierte Quellcodeverwaltung für Projektmappen und Skriptprojekte mit Unterstützung für das Speichern und Verwalten der Kopien von Skripts, die sich im Laufe der Zeit ändern.  
  
-   [!INCLUDE[msCoName](../includes/msconame_md.md)] IntelliSense-Unterstützung für MDX-Anweisungen.  
  
## <a name="object-explorer-features"></a>Funktionen des Objekt-Explorers  
Der Objekt-Explorer von [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] ist ein integriertes Tool zum Anzeigen und Verwalten von Objekten auf allen Servertypen. Es stehen folgende Funktionen zur Verfügung:  
  
-   Filtern nach einem vollständigen Namen, Schema oder Datum bzw. Teilen davon.  
  
-   Das asynchrone Auffüllen von Objekten mit einer Filterfunktion für Objekte auf Basis ihrer Metadaten.  
  
-   Zugriff auf den [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Agent auf Replikationsservern zu Verwaltungszwecken.  
  
Weitere Informationen finden Sie unter [Objekt-Explorer](../ssms/object/object-explorer.md).  
  
## <a name="extensibility"></a>Erweiterbarkeit  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] basiert auf der Visual Studio Isolated Shell, die die Erweiterbarkeit (Add-Ins/Plug-Ins) standardmäßig unterstützt. Sie können auf die Visual Studio-Erweiterbarkeitsdienste zurückgreifen, um die benutzerdefinierten Funktionen in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]offenzulegen. Diese Erweiterbarkeit wird jedoch nicht unterstützt.  
  
Einige Benutzer und Drittanbieter haben Erweiterungen für [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]entwickelt. Zwar raten wir davon nicht grundsätzlich ab, dennoch ist dabei zu beachten, dass eine derartige Erweiterbarkeit nicht unterstützt wird, weshalb Probleme bezüglich der Abwärts-/Aufwärtskompatibilität auftreten können. Microsoft veröffentlicht keine Dokumentation zum Erweitern von [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]. Dennoch stehen Communityblogs und Beispielcodes zur Verfügung, die Sie möglicherweise nutzen können.  
  
Microsoft unterstützt keine [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] -Installationen, wenn bereits [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] -Erweiterungen installiert sind. Haben Sie also [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] -Erweiterungen installiert, entfernen Sie diese ggf., bevor Sie sich an den Microsoft-Kundensupport bezüglich eines [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] -Problems wenden.  
  
## <a name="see-also"></a>Siehe auch  
[Verwenden von SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
  

