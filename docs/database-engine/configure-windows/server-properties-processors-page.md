---
title: "Servereigenschaften (Seite „Prozessoren“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: caeb265188832d61371d0ed4d3f5291235029f72
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="server-properties---processors-page"></a>Servereigenschaften (Seite „Prozessoren“)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Auf dieser Seite können Sie die Prozessoroptionen anzeigen und ändern. Prozessoraffinitätsoptionen sind nur aktiviert, wenn mehr als ein Prozessor installiert ist.  
  
## <a name="options"></a>Optionen  
 **Prozessoraffinität**  
 Weist Prozessoren bestimmte Threads zu, um ein Neuladen des Prozessors zu verhindern und die Threadmigration zwischen Prozessoren zu reduzieren. Weitere Informationen finden Sie unter [Affinitätsmaske (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md).  
  
 **E/A-Affinität**  
 Verbindet die Datenträger-E/A-Operationen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit einer angegebenen CPU-Untergruppe. Weitere Informationen finden Sie unter [Affinity I/O Mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md).  
  
 **Prozessor-Affinitätsmaske für alle Prozessoren automatisch festlegen**  
 Ermöglicht es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die Prozessoraffinität festzulegen.  
  
 **E/A-Affinitätsmaske für alle Prozessoren automatisch festlegen**  
 Ermöglicht es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die E/A-Affinität festzulegen.  
  
 **Maximale Arbeitsthreadanzahl**  
 0 ermöglicht es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die Anzahl der Arbeitsthreads dynamisch festzulegen. Diese Einstellung ist für die meisten Systeme am besten geeignet. In Abhängigkeit von der Systemkonfiguration kann jedoch durch Festlegen dieser Option auf einen bestimmten Wert manchmal die Leistung verbessert werden. Weitere Informationen finden Sie unter [Configure the max worker threads Server Configuration Option](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).  
  
 **SQL Server-Priorität höher stufen**  
 Gibt an, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows mit höherer Planungspriorität als andere Prozesse auf dem gleichen Computer ausgeführt werden soll. Weitere Informationen finden Sie unter [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).  
  
 **Windows-Fibers verwenden ('Lightweightpooling')**  
 Verwendet Windows-Fibers für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst statt Threads. Beachten Sie, dass diese Option nur unter Windows 2003 Server Edition verfügbar ist. Weitere Informationen finden Sie unter [Lightweightpooling (Serverkonfigurationsoption)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
 **Konfigurierte Werte**  
 Zeigt für die Optionen in diesem Bereich konfigurierte Werte an. Wenn Sie diese Werte ändern, klicken Sie anschließend auf **Ausgeführte Werte** , um zu sehen, ob die Änderungen wirksam sind. Sind sie nicht wirksam, muss die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zuerst neu gestartet werden.  
  
 **Ausgeführte Werte**  
 Zeigt die gegenwärtig ausgeführten Werte für die Optionen in diesem Bereich an. Diese Werte sind schreibgeschützt.  
  
## <a name="see-also"></a>Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
