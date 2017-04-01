---
title: "SQL-Skript generieren (Replikationsobjekte) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.generatesqlscript.f1"
helpviewer_keywords: 
  - "SQL-Skript generieren (Dialogfeld)"
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# SQL-Skript generieren (Replikationsobjekte)
  Ein Replikationsskript enthält die gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Systemprozeduren, die zur Implementierung der Replikationskomponenten, für die Skripts erstellt wurden, erforderlich sind. Dazu gehören eine Veröffentlichung oder ein Abonnement. Für die Replikationskomponenten in einer Topologie sollten im Rahmen des Plans zur Wiederherstellung im Notfall Skripts erstellt werden; diese können dann auch zur Automatisierung sich wiederholender Tasks verwendet werden. Die Replikation stellt zum Erstellen von Skripts für Replikationsobjekte zwei Dialogfelder bereit:  
  
-   **SQL-Skript generieren**, kann über das Kontextmenü des der **Replikation** Ordner und allen Unterordnern in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Mithilfe dieses Dialogfelds können Sie Skripts für alle Replikationsobjekte einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellen.  
  
-   **SQL-Skript generieren \< Objektname>**, der über das Kontextmenü für Veröffentlichungen und Abonnements verfügbar ist. Mithilfe dieses Dialogfelds können Sie Skripts für einzelne Objekte erstellen.  
  
 In diesen Dialogfeldern werden Skripts für Objekte einer einzelnen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellt; es werden keine Verbindungen mit anderen Instanzen hergestellt, um Skripts für verknüpfte Objekte zu erstellen.  
  
## SQL-Skript generieren (Optionen)  
 **Verteilereigenschaften**  
 Wählen Sie diese Option aus, um Skripts für gespeicherte Prozeduren zu erstellen, um: den Verteiler aktivieren oder deaktivieren, mit dem Verteiler verknüpfte Verleger hinzufügen oder löschen sowie die Verteilungsdatenbank erstellen oder löschen zu können.  
  
 **Veröffentlichungen in den folgenden Datenquellen**  
 Wählen Sie diese Option aus, um Skripts für gespeicherte Prozeduren zu erstellen, um: die Veröffentlichung aktivieren oder deaktivieren sowie Veröffentlichungen, Artikel, Pushabonnements und Replikationsaufträge erstellen oder löschen zu können.  
  
 **Abonnements in den folgenden Datenquellen**  
 Durch Auswählen dieser Option können Sie Skripts für gespeicherte Prozeduren erstellen, um Pullabonnements und Replikationsaufträge zu erstellen oder zu löschen.  
  
 **Zum Erstellen oder aktivieren die Komponenten** und **zu löschen oder Deaktivieren von Komponenten**  
 Geben Sie an, ob das Skript Befehle zum Erstellen oder Löschen eines Replikationsobjekts enthalten soll. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, das Dialogfeld zu verwenden, um eine Reihe von Skripts zum Aktivieren und Deaktivieren von Komponenten zu erstellen.  
  
 **Replikationsaufträge**  
 Wählen Sie diese Option aus, um neben Skripts für Aufrufe gespeicherter Prozeduren auch Skripts für Replikationsaufträge zu erstellen. Diese Option ist nur verfügbar, wenn Skripts von einem Verteiler aus erstellt werden.  
  
 Bei der Ausführung gespeicherter Replikationsprozeduren werden die erforderlichen Aufträge erstellt, d. h., die Option muss nicht ausgewählt werden. Einen Datensatz mit den erstellten Aufträgen zur Verfügung zu haben, kann sich jedoch als nützlich erweisen, falls ein einzelner Auftrag erneut erstellt werden muss.  
  
## SQL-Skript generieren \< Objektname> Optionen  
 **Zum Erstellen oder aktivieren die Komponenten** und **zu löschen oder Deaktivieren von Komponenten**  
 Geben Sie an, ob das Skript Befehle zum Erstellen oder Löschen eines Replikationsobjekts enthalten soll. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, das Dialogfeld zu verwenden, um eine Reihe von Skripts zum Aktivieren und Deaktivieren von Komponenten zu erstellen.  
  
 **Replikationsaufträge**  
 Diese Option steht nur über die **SQL-Skript generieren** Dialogfeld.  
  
## Siehe auch  
 [Erstellen von Skripts für die Replikation](../../relational-databases/replication/scripting-replication.md)  
  
  