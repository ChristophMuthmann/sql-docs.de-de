---
title: Soft-NUMA (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- NUMA
- soft-NUMA
helpviewer_keywords:
- NUMA
- non-uniform memory access
- soft-NUMA
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
caps.latest.revision: 53
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a6f1b3615631660b04b01c1107c64e66adf6c237
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="soft-numa-sql-server"></a>Soft-NUMA (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Moderne Prozessoren verfügen über mehrere Kerne pro Socket. Jeder Socket wird in der Regel als ein einzelner NUMA-Knoten dargestellt. Das SQL Server-Datenbankmodul partitioniert pro NUMA-Knoten verschiedene interne Strukturen und Dienstthreads für Partitionen.  Bei Prozessoren mit zehn oder mehr Kernen pro Socket, erhöht die Verwendung von Software-NUMA zum Teilen von NUMA-Hardwareknoten in der Regel die Skalierbarkeit und die Leistung, da Prozessoren mit zehn oder mehr Kernen pro Socket verwendet werden. Vor [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 war beim softwarebasierten NUMA (Soft-NUMA) eine Bearbeitung der Registrierung erforderlich, um eine Affinitätsmaske für die Knotenkonfiguration hinzuzufügen. Außerdem wurde der softwarebasierte NUMA auf Hostebene statt über eine Instanz konfiguriert. Ab [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] wird Soft-NUMA automatisch auf die Datenbankinstanzebene konfiguriert, wenn der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Dienst gestartet wird.  
  
> [!NOTE]  
> Hot-Add-Prozessoren werden von Soft-NUMA nicht unterstützt.  
  
## <a name="automatic-soft-numa"></a>Automatischer Soft-NUMA  
 Immer wenn [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] beim Start mehr als acht physische CPU-Kerne pro NUMA-Knoten oder Socket erkennt, werden standardmäßig automatisch Soft-NUMA-Knoten erstellt. Prozessorkerne mit Hyperthreading werden beim Zählen der physischen Kerne auf einem Knoten nicht unterschieden.  Wenn mehr als acht physische Prozessoren pro Socket erkannt werden, erstellt [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Soft-NUMA-Knoten, die im Idealfall acht Kerne enthalten, jedoch auch fünf bis neun logische Kerne pro Knoten enthalten können. Die Größe des Hardwareknotens kann durch eine CPU-Affinitätsmaske eingeschränkt werden. Die Anzahl von NUMA-Knoten übersteigt die maximale Anzahl von unterstützten NUMA-Knoten nie.  
  
 Sie können Soft-NUMA mithilfe der [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)-Anweisung mit dem Argument `SET SOFTNUMA` deaktivieren oder erneut aktivieren. Nach der Änderung des Werts dieser Einstellung ist ein Neustart des Datenbankmoduls erforderlich, damit diese wirksam wird.  
  
 Die folgende Abbildung stellt die Art von Informationen zu Soft-NUMA dar, die im SQL Server-Fehlerprotokoll angezeigt werden, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NUMA-Hardwareknoten mit mehr als acht physischen Prozessoren pro Knoten oder Socket erkennt.  


```
2016-11-14 13:39:43.17 Server      SQL Server detected 2 sockets with 12 cores per socket and 24 logical processors per socket, 48 total logical processors; using 48 logical processors based on SQL Server licensing. This is an informational message; no user action is required.     
2016-11-14 13:39:43.35 Server      Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than 8 physical cores.     
2016-11-14 13:39:43.63 Server      Node configuration: node 0: CPU mask: 0x0000000000555555:0 Active CPU mask: 0x0000000000555555:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.    
2016-11-14 13:39:43.63 Server      Node configuration: node 1: CPU mask: 0x0000000000aaaaaa:0 Active CPU mask: 0x0000000000aaaaaa:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.    
2016-11-14 13:39:43.63 Server      Node configuration: node 2: CPU mask: 0x0000555555000000:0 Active CPU mask: 0x0000555555000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.     
2016-11-14 13:39:43.63 Server      Node configuration: node 3: CPU mask: 0x0000aaaaaa000000:0 Active CPU mask: 0x0000aaaaaa000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.   
```   

## <a name="manual-soft-numa"></a>Manueller Soft-NUMA  
Deaktivieren Sie den automatischen Soft-NUMA, und bearbeiten Sie die Registrierung, um eine Affinitätsmaske für die Knotenkonfiguration hinzuzufügen, damit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuell für die Verwendung von Soft-NUMA konfiguriert werden kann. Wenn Sie diese Methode verwenden, kann die Soft-NUMA-Maske als binärer Eintrag, als DWORD-Registrierungseintrag (hexadezimal oder dezimal) oder als QWORD-Registrierungseintrag (hexadezimal oder dezimal) angegeben werden. Verwenden Sie QWORD- oder BINARY-Registrierungswerte (QWORD-Werte können vor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] nicht verwendet werden), um mehr als die ersten 32 CPUs zu konfigurieren. Nach Änderung der Registrierung müssen Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)] neu starten, damit die Konfiguration von Soft-NUMA wirksam wird.  
  
> [!TIP]
> Die Nummerierung der CPUs beginnt mit 0.  

> [!WARNING]
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
Gehen Sie von einem Beispielcomputer aus, der acht CPUs besitzt, jedoch keinen Hardware-NUMA. Drei Soft-NUMA-Knoten werden konfiguriert.   
[!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz A wird für die Verwendung der CPUs 0 bis 3 konfiguriert. Eine zweite [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz wird installiert und für die Verwendung der CPUs 4 bis 7 konfiguriert. Das Beispiel kann wie folgt visuell dargestellt werden:  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 Instanz A, die eine hohe E/A-Aktivität aufweist, verfügt nun über zwei E/A-Threads und einen LAZY WRITER-Thread. Instanz B, auf der prozessorintensive Vorgänge ausgeführt werden, verfügt nur über einen E/A-Thread und einen LAZY WRITER-Thread. Den Instanzen können zwar unterschiedliche Mengen an Arbeitsspeicher zugewiesen werden. Im Unterschied zu Hardware-NUMA erhalten beide Instanzen den Arbeitsspeicher jedoch aus demselben Speicherblock des Betriebssystems, außerdem ist keine Speicher-Prozessor-Affinität vorhanden.  
  
 Der LAZY WRITER-Thread ist an die SQLOS-Ansicht der physischen NUMA-Arbeitsspeicherknoten gebunden. Deshalb entspricht die von der Hardware angegebene Anzahl von physischen NUMA-Knoten der Anzahl von erstellten LAZY WRITER-Threads. Weitere Informationen finden Sie unter [How It Works: Soft NUMA, I/O Completion Thread, Lazy Writer Workers and Memory Nodes](http://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx).  
  
> [!NOTE]
> Die **Soft-NUMA** -Registrierungsschlüssel werden nicht kopiert, wenn Sie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="set-the-cpu-affinity-mask"></a>Festlegen der CPU-Affinitätsmaske  
 Führen Sie auf Instanz A die folgende Anweisung aus, um die Instanz durch Festlegen der CPU-Affinitätsmaske für die Verwendung der CPUs 0, 1, 2 und 3 zu konfigurieren:  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 3;  
```  
  
Führen Sie auf Instanz B die folgende Anweisung aus, um die Instanz durch Festlegen der CPU-Affinitätsmaske für die Verwendung der CPUs 4, 5, 6 und 7 zu konfigurieren:  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=4 TO 7;  
```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>Zuordnen von Soft-NUMA-Knoten zu den CPUs  
 Fügen Sie mithilfe des Registrierungs-Editors (regedit.exe) die folgenden Registrierungsschlüssel hinzu, um den CPUs 0 und 1 den Soft-NUMA-Knoten 0, den CPUs 2 und 3 den Soft-NUMA-Knoten 1 und den CPUs 4, 5, 6 und 7 den Soft-NUMA-Knoten 2 zuzuordnen.  
  
> [!TIP]
> Verwenden Sie zum Angeben der CPUs 60 bis 63 den QWORD-Wert F000000000000000 oder den BINARY-Wert 1111000000000000000000000000000000000000000000000000000000000000.  
  
 Legen Sie für das folgende Beispiel einen DL580 G9-Server mit 18 Kernen pro Socket (in vier Sockets) zugrunde, wobei jeder Socket eine eigene K-Gruppe darstellt. Eine von Ihnen erstellte Soft-NUMA-Konfiguration würde Folgendem ähneln: sechs Kerne pro Knoten, drei Knoten pro Gruppe, vier Gruppen.  
  
|Beispiel für einen [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] -Server mit mehreren K-Gruppen|Typ|Wertname|Wertdaten|  
|-----------------------------------------------------------------------------------------------------------------|----------|----------------|----------------|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|Gruppieren|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|Gruppieren|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|Gruppieren|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|Gruppieren|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|Gruppieren|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|Gruppieren|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|Gruppieren|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|Gruppieren|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|Gruppieren|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|Gruppieren|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|Gruppieren|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|Gruppieren|3|  
  
## <a name="metadata"></a>Metadaten  
 Sie können die folgenden DMVs zum Anzeigen des aktuellen Status und der Konfiguration von Soft-NUMA verwenden.  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md): Zeigt den aktuellen Wert (0 oder 1) für SOFTNUMA an  
  
-   [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md): The *softnuma* and *softnuma_desc* columns displays the current configuration values.  
  
> [!NOTE]
> Obwohl Sie den ausgeführten Wert für automatischen soft-NUMA mithilfe von [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) anzeigen können, können Sie dessen Wert mit **sp_configure** nicht ändern. Sie müssen die [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)-Anweisung mit dem `SET SOFTNUMA`-Argument verwenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Zuordnen von TCP/IP-Ports zu NUMA-Knoten &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)    
[Affinitätsmaske (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)    
[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)     
[sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)   
  
