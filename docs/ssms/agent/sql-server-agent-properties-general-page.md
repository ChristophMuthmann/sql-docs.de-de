---
title: SQL Server-Agent-Eigenschaften (Seite Allgemein)|Microsoft-Dokumente
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4046c9c45fda98646043e73c8a9b1e1bacfdd335
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-agent-properties-general-page"></a>SQL Server-Agent-Eigenschaften (Seite Allgemein)
Mithilfe dieser Seite können Sie die allgemeinen Eigenschaften des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstes anzeigen und ändern.  
  
## <a name="options"></a>enthalten  
**Dienststatus**  
Zeigt den aktuellen Status des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstes an.  
  
**SQL Server nach unerwartetem Beenden automatisch neu starten**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent startet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] neu, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] unerwartet beendet wird.  
  
**SQL Server-Agent nach unerwartetem Beenden automatisch neu starten**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] startet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent neu, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent unerwartet beendet wird.  
  
**Filename**  
Geben Sie den Dateinamen für das Fehlerprotokoll an.  
  
**...**  
Mit dieser Schaltfläche können Sie nach der Fehlerprotokolldatei suchen.  
  
**Meldungen zur Ablaufverfolgung einschließen**  
Meldungen zur Ablaufverfolgung werden in das Fehlerprotokoll eingeschlossen. Meldungen zur Ablaufverfolgung stellen detaillierte Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Vorgängen bereit. Deshalb benötigt die Protokolldatei mehr Datenträgerspeicherplatz, wenn diese Option ausgewählt ist. Diese Option sollte nur bei der Behandlung eines Problems ausgewählt werden, bei dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent eine Rolle spielt.  
  
**OEM-Datei schreiben**  
Speichert die Fehlerprotokolldatei als Nicht-Unicode-Datei. Dadurch wird der für die Protokolldatei erforderliche Datenträgerspeicherplatz reduziert. Meldungen, die Unicode enthalten, können jedoch schwieriger lesbar sein, wenn diese Option aktiviert ist.  
  
**NET SEND-Empfänger**  
Geben Sie den Namen eines Operators ein, der NET SEND-Benachrichtigungen von Meldungen empfängt, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent in die Protokolldatei schreibt.  
  
## <a name="see-also"></a>Siehe auch  
[Operatoren](../../ssms/agent/operators.md)  
[SQL Server-Agent-Fehlerprotokoll](../../ssms/agent/sql-server-agent-error-log.md)  
  
