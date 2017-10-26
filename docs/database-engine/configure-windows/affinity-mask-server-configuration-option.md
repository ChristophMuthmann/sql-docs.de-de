---
title: "Affinitätsmaske (Serverkonfigurationsoption) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default affinity mask option
- reloading processor cache
- processor cache [SQL Server]
- CPU [SQL Server], licensing
- deferred process call
- affinity mask option
- processor affinity [SQL Server]
- SMP
- DPC
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0aa50b8c593ced9089a939eb5490380872d38472
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="affinity-mask-server-configuration-option"></a>Affinitätsmaske (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen [ALTER SERVER CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-server-configuration-transact-sql.md).  
  
 Zum Ausführen von Multitasking verschiebt [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows gelegentlich Prozessthreads zwischen verschiedenen Prozessoren. Obwohl dies aus der Sicht des Betriebssystems effizient ist, kann diese Aktivität die Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei starker Systemauslastung reduzieren, da jeder Prozessorcache wiederholt mit Daten geladen wird. Durch das Zuweisen von Prozessoren für bestimmte Threads kann unter diesen Bedingungen die Leistung verbessert werden, weil das erneute Laden von Daten in den Prozessor entfällt und die Threadmigration zwischen Prozessen reduziert wird (wodurch der Kontextwechsel reduziert wird). Diese Zuordnung zwischen einem Thread und einem Prozessor wird als Prozessoraffinität bezeichnet.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die Prozessoraffinität durch zwei Affinitätsmaskenoptionen: Affinity Mask (auch als **CPU-Affinitätsmaske**bezeichnet) und Affinity I/O Mask. Weitere Informationen zur Option Affinity I/O Mask finden Sie unter [Affinity I/O Mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md). CPU- und E/A-Affinitätsunterstützung für Server mit 33–64 Prozessoren erfordert die zusätzliche Verwendung von [affinity64 mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) bzw. [affinity64 Input-Output mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md).  
  
> [!NOTE]  
>  Affinitätsunterstützung für Server mit 33 bis 64 Prozessoren steht nur auf 64-Bit-Betriebssystemen zur Verfügung.  
  
 Mit der Option Affinity Mask aus früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die CPU-Affinität dynamisch gesteuert.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kann die Option Affinity Mask konfiguriert werden, ohne dass ein Neustart der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz erforderlich ist. Wenn Sie sp_configure verwenden, müssen Sie nach dem Festlegen einer Konfigurationsoption entweder RECONFIGURE oder RECONFIGURE WITH OVERRIDE ausführen. Wenn Sie [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]verwenden, ist ein Neustart erforderlich, falls Sie die Option affinity mask ändern.  
  
 Änderungen an den Affinitätsmasken erfolgen dynamisch. Dies ermöglicht das bedarfsgesteuerte Starten und Herunterfahren der CPU-Zeitplanungsmodule, die Prozessthreads in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]binden. Dies kann der Fall sein, wenn sich Bedingungen auf dem Server ändern. Wenn dem Server z. B. eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hinzugefügt wird, müssen Sie möglicherweise die Option Affinity Mask anpassen, um die Prozessorauslastung neu zu verteilen.  
  
 Für Änderungen an den Affinitätsbitmasken muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein neues CPU-Zeitplanungsmodul aktivieren und das vorhandene CPU-Zeitplanungsmodul deaktivieren. Neue Batches können dann im neuen oder alten CPU-Zeitplanungsmodul verarbeitet werden.  
  
 Um ein neues CPU-Zeitplanungsmodul zu starten, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein neues CPU-Zeitplanungsmodul und fügt es der Liste der Standard-Zeitplanungsmodule hinzu. Das neue Zeitplanungsmodul wird nur für die neuen eingehenden Batches verwendet. Die vorhandenen Batches werden weiterhin mit demselben Zeitplanungsmodul ausgeführt. Die Arbeitsthreads werden nach dem neuen Zeitplanungsmodul migriert, wenn sie freigegeben werden oder wenn neue Arbeitsthreads erstellt werden.  
  
 Zum Herunterfahren eines Zeitplanungsmoduls müssen alle Batches im Zeitplanungsmodul ihre Aktivitäten abschließen und beendet werden. Ein heruntergefahrenes Zeitplanungsmodul wird als offline gekennzeichnet, damit kein neuer Batch damit geplant wird.  
  
 Unabhängig davon, ob ein neues Zeitplanungsmodul hinzugefügt oder entfernt wird, werden die permanenten Systemtasks wie z. B. lockmonitor, checkpoint, system task thread (processing DTC) und signal process weiterhin im Zeitplanungsmodul ausgeführt, während der Server betriebsbereit ist. Diese permanenten Systemtasks werden nicht dynamisch migriert. Um die Prozessorauslastung für diese Systemtasks auf die Zeitplanungsmodule zu verteilen, muss die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz neu gestartet werden. Falls [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht, ein Zeitplanungsmodul für einen permanenten Systemtask herunterzufahren, wird der Task weiterhin im Offline-Zeitplanungsmodul ausgeführt (keine Migration). Dieses Zeitplanungsmodul ist an die Prozessoren in der geänderten Affinitätsmaske gebunden und sollte den Prozessor nicht auslasten, dem es vor der Änderung zugeordnet war. Zusätzliche Offline-Zeitplanungsmodule sollten keine signifikanten Auswirkungen auf die Arbeitsauslastung des Systems haben. Falls dies nicht der Fall ist, muss der Datenbankserver neu gestartet werden, um diese Tasks neu zu konfigurieren.  
  
 Die E/A-Affinitätsmaske hat direkte Auswirkungen auf die E/-A-Affinitätstasks (z. B. verzögertes Schreiben und Schreiben von Protokollen). Falls die Tasks für verzögertes Schreiben und das Schreiben von Protokollen nicht an eine Affinität gebunden sind, gelten dieselben Regeln, die für die anderen permanenten Tasks wie z. B. lockmonitor oder checkpoint definiert sind.  
  
 Um sicherzustellen, dass die neue Affinitätsmaske gültig ist, wird mit dem Befehl RECONFIGURE überprüft, ob sich die normalen CPU- und E/A-Affinitäten gegenseitig ausschließen. Falls dies nicht der Fall ist, wird eine Fehlermeldung an die Clientsitzung und an das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll gesendet. Diese Fehlermeldung besagt, dass eine solche Einstellung nicht empfohlen wird. Das Ausführen von RECONFIGURE WITH OVERRIDE ermöglicht CPU- und E/A-Affinitäten, die sich nicht gegenseitig ausschließen.  
  
 Wenn Sie eine Affinitätsmaske angeben, die eine nicht vorhandene CPU zuzuordnen versucht, sendet der Befehl RECONFIGURE eine Fehlermeldung an die Clientsitzung und an das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll. Die Verwendung der Option RECONFIGURE WITH OVERRIDE hat in diesem Fall keine Auswirkung, und der gleiche Konfigurationsfehler wird wiederum gemeldet.  
  
 Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Aktivitäten auch von Prozessoren fernhalten, denen eine bestimmte Arbeitsauslastung durch das Betriebssystem Windows 2000 oder Windows Server 2003 zugewiesen wurde. Wird ein Bit, das einen Prozessor darstellt, auf 1 festgelegt, wird dieser Prozessor vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmodul für die Threadzuweisung ausgewählt. Wenn Sie **affinity mask** auf 0 festlegen (Standardeinstellung), legen die Planungsalgorithmen von Microsoft Windows 2000 oder Windows Server 2003 die Threadaffinität fest. Wenn Sie **affinity mask** auf einen Wert ungleich Null festlegen, legt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Affinität den Wert als Bitmaske aus, die die infrage kommenden Prozessoren angibt.  
  
 Durch das Ausschließen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Threads von der Ausführung auf bestimmten Prozessoren kann Microsoft Windows 2000 oder Windows Server 2003 die Verarbeitung von Windows-spezifischen Prozessen durch das System besser auswerten. Beispielsweise könnte der Systemadministrator auf einem Server mit 8 CPUs und zwei Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Instanz A und B) mithilfe der Option Affinity Mask die ersten 4 CPUs der Instanz A sowie die nächsten 4 CPUs der Instanz B zuweisen. Um mehr als 32 Prozessoren zu konfigurieren, legen Sie die Optionen Affinity Mask und Affinity64 Mask fest. Die Werte für **affinity mask** lauten wie folgt:  
  
-   Ein aus einem Byte bestehender Wert für **affinity mask** deckt bis zu 8 CPUs in einem Multiprozessorcomputer ab.  
  
-   Ein aus zwei Bytes bestehender Wert für **affinity mask** deckt bis zu 16 CPUs in einem Multiprozessorcomputer ab.  
  
-   Ein aus drei Bytes bestehender Wert für **affinity mask** deckt bis zu 24 CPUs in einem Multiprozessorcomputer ab.  
  
-   Ein aus vier Bytes bestehender Wert für **affinity mask** deckt bis zu 32 CPUs in einem Multiprozessorcomputer ab.  
  
-   Für einen Computer mit mehr als 32 CPUs konfigurieren Sie eine aus vier Bytes bestehende affinity mask für die ersten 32 CPUs und eine aus bis zu vier Bytes bestehende affinity64 mask für die restlichen CPUs.  
  
 Da es sich beim Festlegen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozessoraffinität um einen spezialisierten Vorgang handelt, sollten Sie diesen nur bei Bedarf verwenden. In den meisten Fällen kann eine optimale Leistung durch die standardmäßige Affinität von Microsoft Windows 2000 oder Windows Server 2003 erzielt werden. Sie sollten auch die CPU-Anforderungen für andere Anwendungen berücksichtigen, wenn Sie die Affinitätsmasken festlegen. Weitere Informationen finden Sie in der Dokumentation zu Ihrem Windows-Betriebssystem.  
  
> [!NOTE]  
>  Sie können den Windows-Systemmonitor zum Anzeigen und Analysieren der Auslastung einzelner Prozessoren verwenden.  
  
 Bei Angabe der Option Affinity I/O Mask muss diese in Verbindung mit der Konfigurationsoption Affinity Mask verwendet werden. Aktivieren Sie nicht dieselbe CPU beim **affinity mask** -Schalter und der Option Affinity I/O Mask. Die Bits, die jeder CPU entsprechen, sollten einen der folgenden drei Status aufweisen:  
  
-   0 für die Optionen Affinity Mask und Affinity I/O Mask.  
  
-   1 für die Option Affinity Mask und 0 für die Option Affinity I/O Mask.  
  
-   1 für die Option Affinity Mask und 1 für die Option Affinity I/O Mask.  
  
> [!CAUTION]  
>  Konfigurieren Sie nicht die CPU-Affinität im Windows-Betriebssystem und gleichzeitig die Affinitätsmaske in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Diese Einstellungen zielen auf dasselbe Ergebnis. Wenn die Konfigurationen inkonsistent sind, kann dies zu unvorhersehbaren Ergebnissen führen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Die CPU-Affinität wird am besten mit der Option sp_configure in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfiguriert.  
  
## <a name="example"></a>Beispiel  
 Wenn z. B. zum Festlegen der Option Affinity Mask die Prozessoren 1, 2 und 5 als verfügbar ausgewählt wurden und dabei die Bits 1, 2 und 5 auf 1 sowie die Bits 0, 3, 4, 6 und 7 auf 0 festgelegt sind, wird der hexadezimale Wert 0x26 bzw. die Dezimalzahl `38` angegeben. Nummerieren Sie die Bits von rechts nach links. Die Option Affinity Mask zählt die Prozessoren von 0 bis 31 durch. Im folgenden Beispiel steht deshalb der Zähler `1` für den zweiten Prozessor auf dem Server.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'affinity mask', 38;  
RECONFIGURE;  
GO  
```  
  
 Nachfolgend werden die **affinity mask** -Werte für ein System mit 8 CPUs aufgeführt.  
  
|Dezimalzahl|Binäre Bitmaske|Ermöglicht SQL Server-Threads auf Prozessoren|  
|-------------------|---------------------|--------------------------------------------|  
|1|00000001|0|  
|3|00000011|0 und 1|  
|7|00000111|0, 1 und 2|  
|15|00001111|0, 1, 2 und 3|  
|31|00011111|0, 1, 2, 3 und 4|  
|63|00111111|0, 1, 2, 3, 4 und 5|  
|127|01111111|0, 1, 2, 3, 4, 5 und 6|  
|255|11111111|0, 1, 2, 3, 4, 5, 6 und 7|  
  
 Bei Affinity Mask handelt es sich um eine erweiterte Option. Wenn Sie die Einstellung mithilfe der gespeicherten Systemprozedur ändern, können Sie **affinity mask** nur ändern, wenn **Erweiterte Optionen anzeigen** auf 1 festgelegt ist. Die neue Einstellung wird nach Ausführung des [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehls RECONFIGURE sofort wirksam, ohne dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz neu gestartet werden muss.  
  
## <a name="non-uniform-memory-access-numa"></a>Non-Uniform Memory Access (NUMA)  
 Wenn hardwarebasierter NUMA (Non-Uniform Memory Access, nicht einheitlicher Speicherzugriff) verwendet wird und die Affinitätsmaske festgelegt ist, wird jedes Zeitplanungsmodul in einem Knoten seiner eigenen CPU zugeordnet. Wenn die Affinitätsmaske nicht festgelegt ist, wird jedes Zeitplanungsmodul der Gruppe von CPUs innerhalb des NUMA-Knotens zugeordnet, und ein Zeitplanungsmodul, das dem NUMA-Knoten N1 zugeordnet ist, kann Vorgänge auf jeder CPU im Knoten planen, jedoch nicht auf CPUs, die einem anderen Knoten zugeordnet sind.  
  
 Jeder Vorgang, der auf einem einzelnen NUMA-Knoten ausgeführt wird, kann nur Pufferseiten von diesem Knoten verwenden. Wenn ein Vorgang parallel auf CPUs von mehreren Knoten ausgeführt wird, kann Arbeitsspeicher von jedem beteiligten Knoten verwendet werden.  
  
## <a name="licensing-issues"></a>Lizenzierungsprobleme  
 Die dynamische Affinität wird durch die CPU-Lizenzierung streng reguliert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind keine Konfigurationen von Affinitätsmaskenoptionen zulässig, die gegen die Lizenzierungsrichtlinien verstoßen.  
  
### <a name="startup"></a>Starten  
 Wenn eine angegebene Affinitätsmaske während des Starts von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder während des Anfügens einer Datenbank gegen die Lizenzierungsrichtlinien verstößt, führt die Modulschicht den Startprozess oder das Anfügen einer Datenbank bzw. den Wiederherstellungsvorgang aus. Anschließend wird der Wert von sp_configure für die Affinitätsmaske auf 0 zurückgesetzt, wodurch eine Fehlermeldung an das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll ausgegeben wird.  
  
### <a name="reconfigure"></a>Neukonfigurieren  
 Wenn eine angegebene Affinitätsmaske beim Ausführen des [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehls RECONFIGURE gegen die Lizenzierungsrichtlinien verstößt, wird eine Fehlermeldung an die Clientsitzung und an das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll gesendet. Der Datenbankadministrator muss dann die Affinitätsmaske neu konfigurieren. In diesem Fall ist der Befehl RECONFIGURE WITH OVERRIDE nicht zulässig.  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  

