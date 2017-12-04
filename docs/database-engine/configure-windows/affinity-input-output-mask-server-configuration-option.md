---
title: Affinity I/O Mask (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
caps.latest.revision: "29"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fbb539201ac8566005913d9b45574aa7f261b089
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>Affinity I/O Mask (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Zum Ausführen von Multitasking verschiebt [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows gelegentlich Prozessthreads zwischen verschiedenen Prozessoren. Obwohl dies aus der Sicht des Betriebssystems effizient ist, kann diese Aktivität die Leistung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei starker Systemauslastung reduzieren, da jeder Prozessorcache wiederholt mit Daten geladen wird. Unter diesen Bedingungen kann das Zuweisen bestimmter Threads zu bestimmten Prozessoren die Leistung verbessern, da das erneute Laden von Prozessoren vermieden wird. Eine solche Zuordnung zwischen einem Thread und einem Prozessor wird als Prozessoraffinität bezeichnet.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die Prozessoraffinität durch zwei Affinitätsmaskenoptionen: **affinity mask** (auch als **CPU-Affinitätsmaske**bezeichnet) und **affinity I/O mask**. Weitere Informationen zur Option **affinity mask** finden Sie unter [Affinitätsmaske (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md). CPU- und E/A-Affinitätsunterstützung für Server mit 33–64 Prozessoren erfordert die zusätzliche Verwendung von [affinity64 mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) bzw. [affinity64 Input-Output mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md) .  
  
> [!NOTE]  
>  Affinitätsunterstützung für Server mit 33 bis 64 Prozessoren steht nur auf 64-Bit-Betriebssystemen zur Verfügung.  
  
 Die Option **affinity I/O mask** bindet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenträger-E/A an eine bestimmte Teilmenge von CPUs. In High-End-OLTP-Umgebungen (Online Transactional Processing, Onlinetransaktionsverarbeitung) für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann diese Erweiterung die Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Threads, die E/A verursachen, verbessern. Diese Verbesserung unterstützt keine Hardwareaffinität für einzelne Datenträger oder Datenträgercontroller.  
  
 Der Wert für **affinity I/O mask** gibt an, welche CPUs eines Multiprozessorcomputers für die Verarbeitung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenträger-E/A-Vorgängen verwendet werden sollen. Die Maske ist eine Bitmap, in der das erste Bit von rechts die CPU mit der niedrigsten Nummer angibt, CPU(0), das zweite Bit von rechts die CPU mit der nächsthöheren Nummer, CPU(1) usw. Bei mehr als 32 Prozessoren legen Sie beide Konfigurationsoptionen **affinity I/O mask** und **affinity64 I/O mask**fest.  
  
 Die Werte für **affinity I/O mask** lauten wie folgt:  
  
-   Eine aus 1 Byte bestehende **affinity I/O mask deckt bis zu 8 CPUs** in einem Multiprozessorcomputer ab.  
  
-   Eine aus 2 Bytes bestehende **affinity I/O mask** deckt bis zu 16 CPUs in einem Multiprozessorcomputer ab.  
  
-   Eine aus 3 Bytes bestehende **affinity I/O mask** deckt bis zu 24 CPUs in einem Multiprozessorcomputer ab.  
  
-   Eine aus 4 Bytes bestehende **affinity I/O mask** deckt bis zu 32 CPUs in einem Multiprozessorcomputer ab.  
  
-   Bei mehr als 32 CPUs konfigurieren Sie eine aus 4 Bytes bestehende **affinity I/O mask** für die ersten 32 CPUs und eine aus maximal 4 Bytes bestehende **affinity64 I/O mask** für die verbleibenden CPUs.  
  
 Ein 1-Bit im E/A-Affinitätsmuster gibt an, dass die entsprechende CPU für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenträger-E/A-Vorgänge geeignet ist; ein 0-Bit gibt an, dass keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenträger-E/A-Vorgänge für die entsprechende CPU geplant werden sollen. Sind alle Bits auf 0 festgelegt oder ist **affinity I/O mask** nicht angegeben, werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenträger-E/A-Vorgänge für eine beliebige CPU geplant, die für die Verarbeitung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Threads geeignet ist.  
  
 Da das Festlegen der Option **Affinity I/O Mask**  (Affinität E/A Maske) von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen spezialisierten Vorgang darstellt, sollte er nur bei Bedarf ausgeführt werden. In den meisten Fällen kann eine optimale Leistung durch die standardmäßige Affinität von Windows 2000 oder Windows Server 2003 erzielt werden.  
  
 Wenn Sie die Option **affinity I/O mask** angeben, müssen Sie sie mit der Konfigurationsoption **affinity mask** verwenden. Aktivieren Sie in der Option **affinity I/O mask** und in der Option **affinity mask** nicht dieselbe CPU. Die Bits, die den einzelnen CPUs entsprechen, sollten sich jeweils in einem der folgenden drei Zustände befinden:  
  
-   0 in der Option **affinity I/O mask** und in der Option **affinity mask** .  
  
-   1 in der Option **affinity I/O mask** und 0 in der Option **affinity mask** .  
  
-   0 in der Option **affinity I/O mask** und 1 in der Option **affinity mask** .  
  
 Die Option **affinity I/O mask** ist eine erweiterte Option. Wenn Sie die Einstellung mithilfe der gespeicherten Systemprozedur **sp_configure** ändern, können Sie **affinity I/O mask** nur ändern, wenn **Erweiterte Optionen anzeigen** auf 1 festgelegt ist. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist für das erneute Konfigurieren der Option **affinity I/O mask** ein Neustart der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz erforderlich.  
  
> [!CAUTION]  
>  Konfigurieren Sie nicht die CPU-Affinität im Windows-Betriebssystem und gleichzeitig die Affinitätsmaske in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Diese Einstellungen zielen auf dasselbe Ergebnis. Wenn die Konfigurationen inkonsistent sind, kann dies zu unvorhersehbaren Ergebnissen führen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU-Affinität wird am besten mit der Option **sp_configure** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfiguriert.  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
