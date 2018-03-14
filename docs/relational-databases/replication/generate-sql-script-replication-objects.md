---
title: SQL-Skript generieren (Replikationsobjekte) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffc0fd061540ec62aae33b2269035d4d63067725
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="generate-sql-script-replication-objects"></a>SQL-Skript generieren (Replikationsobjekte)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ein Replikationsskript enthält die gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Systemprozeduren, die zur Implementierung der Replikationskomponenten, für die Skripts erstellt wurden, erforderlich sind. Dazu gehören eine Veröffentlichung oder ein Abonnement. Für die Replikationskomponenten in einer Topologie sollten im Rahmen des Plans zur Wiederherstellung im Notfall Skripts erstellt werden; diese können dann auch zur Automatisierung sich wiederholender Tasks verwendet werden. Die Replikation stellt zum Erstellen von Skripts für Replikationsobjekte zwei Dialogfelder bereit:  
  
-   **SQL-Skript generieren**: Dieses Dialogfeld kann über das Kontextmenü des Ordners **Replikation** sowie aller untergeordneten Ordner in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aufgerufen werden. Mithilfe dieses Dialogfelds können Sie Skripts für alle Replikationsobjekte einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellen.  
  
-   **SQL-Skript generieren \<ObjectName>**: Auf dieses Dialogfeld können Sie über das Kontextmenü für Veröffentlichungen und Abonnements zugreifen. Mithilfe dieses Dialogfelds können Sie Skripts für einzelne Objekte erstellen.  
  
 In diesen Dialogfeldern werden Skripts für Objekte einer einzelnen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellt; es werden keine Verbindungen mit anderen Instanzen hergestellt, um Skripts für verknüpfte Objekte zu erstellen.  
  
## <a name="generate-sql-script-options"></a>SQL-Skript generieren (Optionen)  
 **Verteilereigenschaften**  
 Wählen Sie diese Option aus, um Skripts für gespeicherte Prozeduren zu erstellen, um: den Verteiler aktivieren oder deaktivieren, mit dem Verteiler verknüpfte Verleger hinzufügen oder löschen sowie die Verteilungsdatenbank erstellen oder löschen zu können.  
  
 **Veröffentlichungen in den folgenden Datenquellen**  
 Wählen Sie diese Option aus, um Skripts für gespeicherte Prozeduren zu erstellen, um: die Veröffentlichung aktivieren oder deaktivieren sowie Veröffentlichungen, Artikel, Pushabonnements und Replikationsaufträge erstellen oder löschen zu können.  
  
 **Abonnements in den folgenden Datenquellen**  
 Durch Auswählen dieser Option können Sie Skripts für gespeicherte Prozeduren erstellen, um Pullabonnements und Replikationsaufträge zu erstellen oder zu löschen.  
  
 **Um Komponenten zu erstellen oder zu aktivieren** und **Um Komponenten zu löschen oder zu deaktivieren**  
 Geben Sie an, ob das Skript Befehle zum Erstellen oder Löschen eines Replikationsobjekts enthalten soll. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, das Dialogfeld zu verwenden, um eine Reihe von Skripts zum Aktivieren und Deaktivieren von Komponenten zu erstellen.  
  
 **Replikationsaufträge**  
 Wählen Sie diese Option aus, um neben Skripts für Aufrufe gespeicherter Prozeduren auch Skripts für Replikationsaufträge zu erstellen. Diese Option ist nur verfügbar, wenn Skripts von einem Verteiler aus erstellt werden.  
  
 Bei der Ausführung gespeicherter Replikationsprozeduren werden die erforderlichen Aufträge erstellt, d. h., die Option muss nicht ausgewählt werden. Einen Datensatz mit den erstellten Aufträgen zur Verfügung zu haben, kann sich jedoch als nützlich erweisen, falls ein einzelner Auftrag erneut erstellt werden muss.  
  
## <a name="generate-sql-script-objectname-options"></a>Optionen von SQL-Skript \<ObjectName> generieren  
 **Um Komponenten zu erstellen oder zu aktivieren** und **Um Komponenten zu löschen oder zu deaktivieren**  
 Geben Sie an, ob das Skript Befehle zum Erstellen oder Löschen eines Replikationsobjekts enthalten soll. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, das Dialogfeld zu verwenden, um eine Reihe von Skripts zum Aktivieren und Deaktivieren von Komponenten zu erstellen.  
  
 **Replikationsaufträge**  
 Auf diese Option kann im Dialogfeld **SQL-Skript generieren** zugegriffen werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen von Skripts für die Replikation](../../relational-databases/replication/scripting-replication.md)  
  
  
