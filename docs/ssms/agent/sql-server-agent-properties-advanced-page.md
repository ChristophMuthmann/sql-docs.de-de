---
title: SQL Server-Agent-Eigenschaften (Seite Erweitert)|Microsoft-Dokumente
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
- sql13.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7239a45e4c3761919503a50f64168e266c58a0f5
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-agent-properties-advanced-page"></a>SQL Server-Agent-Eigenschaften (Seite Erweitert)
Mithilfe dieser Seite können Sie die erweiterten Eigenschaften des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Diensts anzeigen und ändern.  
  
## <a name="options"></a>enthalten  
**SQL Server-Ereignisweiterleitung**  
Durch die Optionen in dieser Kategorie wird die Ereignisweiterleitung aktiviert und konfiguriert.  
  
**Ereignisse an anderen Server weiterleiten**  
Leitet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent-Ereignisse an einen anderen Server weiter.  
  
**Server**  
Wählen Sie den Namen des Servers aus, an den Ereignisse weitergeleitet werden sollen.  
  
**Ereignisse ohne Behandlung**  
Leitet nur Ereignisse ohne Behandlung an den angegebenen Server weiter. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent leitet nur Ereignisse weiter, auf die keine Warnung reagiert.  
  
**Alle Ereignisse**  
Leitet alle Ereignisse weiter. Wenn eine Warnung in der lokalen Instanz auf das Ereignis reagiert, leitet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] das Ereignis weiter und verarbeitet auch die Warnung.  
  
**Bei diesem Schweregrad des Ereignisses oder darüber**  
Leitet nur Ereignisse weiter, deren Schweregrad der angegebenen Ebene entspricht oder darüber liegt.  
  
**Bedingung für 'CPU im Leerlauf'**  
Durch die Optionen in dieser Kategorie werden die Bedingungen definiert, unter denen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent Aufträge ausführt, für die CPU-Leerlaufzeitpläne festgelegt sind.  
  
**Bedingung für 'CPU im Leerlauf' definieren**  
Definiert die Bedingungen, unter denen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent die CPU als im Leerlauf befindlich betrachtet.  
  
**bei durchschnittlicher CPU-Nutzung unter**  
Prozentualer Wert der CPU-Nutzung, unter dem die CPU als im Leerlauf befindlich betrachtet wird.  
  
**und Verbleiben unterhalb dieser Stufe für**  
Die Zeitspanne, für die die durchschnittliche CPU-Nutzung unterhalb des angegebenen Wertes liegen muss, bevor [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent Aufträge dem CPU-Leerlaufzeitplan entsprechend ausführt.  
  
## <a name="see-also"></a>Siehe auch  
[Anlegen und Zuweisen von Zeitplänen zu Aufträgen](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Verwalten von Ereignissen](../../ssms/agent/manage-events.md)  
  

