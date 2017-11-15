---
title: "Serverkonfigurationsoptionen für den Serverarbeitsspeicher | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Virtual Memory Manager
- max server memory option
- virtual memory [SQL Server]
- VMM
- server memory options [SQL Server]
- servers [SQL Server], memory
- buffer pools [SQL Server]
- min server memory option
- manual memory options [SQL Server]
- memory [SQL Server], servers
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
caps.latest.revision: "78"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f6e39e3275e64d5f6df2621385ff834f2dd5856d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="server-memory-server-configuration-options"></a>Serverkonfigurationsoptionen für den Serverarbeitsspeicher
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mit den beiden Arbeitsspeicheroptionen für den Server, **Min. Serverarbeitsspeicher** und **Max. Serverarbeitsspeicher**, können Sie die Größe des Arbeitsspeichers (in Megabytes) umkonfigurieren, der vom SQL Server-Speicher-Manager für einen von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendeten SQL Server-Prozess verwaltet wird.  
  
 Die Standardeinstellung für **Min. Serverarbeitsspeicher** ist 0, die für **Max. Serverarbeitsspeicher** 2147483647 MB. Standardmäßig können die Arbeitsspeicheranforderungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anhand der verfügbaren Systemressourcen dynamisch geändert werden.  
  
> [!NOTE]  
>  Wenn die Option **Max. Serverarbeitsspeicher** auf den Minimalwert festgelegt ist, kann dies die Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erheblich einschränken und sogar den Start von SQL Server verhindern. Wenn sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach dem Ändern dieser Option nicht starten lässt, müssen Sie es mithilfe der Startoption **–f** starten und die Option **Max. Serverarbeitsspeicher** auf ihren vorherigen Wert zurücksetzen. Weitere Informationen finden Sie unter [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
 Bei dynamischer Verwendung des Arbeitsspeichers von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird der im System verfügbare Arbeitsspeicher in regelmäßigen Abständen abgefragt. Bei Beibehaltung dieses freien Arbeitsspeichers werden Auslagerungsvorgänge durch das Betriebssystem verhindert. Wenn weniger freier Arbeitsspeicher vorhanden ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arbeitsspeicher für das Betriebssystem frei. Wenn mehr Arbeitsspeicher frei ist, kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auch mehr Speicher reservieren. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fügt Arbeitsspeicher nur dann hinzu, wenn durch die Arbeitsauslastung mehr Arbeitsspeicher erforderlich ist. Bei einem ruhenden Server wird die Größe seines virtuellen Adressraums nicht vergrößert.  
  
 Beispiel B enthält eine Abfrage, welche den derzeit verwendeten Arbeitsspeicher zurückgibt. **Max. Serverarbeitsspeicher** steuert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Speicherzuweisung, einschließlich Pufferpool, Arbeitsspeicherkompilierung, alle Caches, Arbeitsspeicherzuweisungen, Sperren-Manager-Speicher und Clr-Speicher (im Wesentlichen alle Arbeitsspeicherclerks in **sys.dm_os_memory_clerks**). Arbeitsspeicher für Threadstapel, Arbeitsspeicherheaps, andere verknüpfte Serveranbieter als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]und durch Nicht- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -DLL zugewiesener Speicher werden nicht von max. Serverarbeitsspeicher kontrolliert.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Mithilfe der für Speicherbenachrichtigungen verfügbaren API **QueryMemoryResourceNotification** ermittelt SQL Server, wann der SQL Server-Speicher-Manager Speicher zuordnen oder freigeben kann.  
  
 Grundsätzlich empfiehlt es sich, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine dynamische Verwendung des Arbeitsspeichers zuzulassen. Sie können die Speicheroptionen jedoch auch manuell festlegen und den Umfang des für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugreifbaren Arbeitsspeichers einschränken. Bevor Sie den Umfang des Arbeitsspeichers für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]festlegen, sollten Sie die geeignete Arbeitsspeichereinstellung ermitteln. Ziehen Sie dazu vom gesamten physischen Speicher den Arbeitsspeicher ab, der für das Betriebssystem und alle weiteren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erforderlich ist. (Falls der Computer nicht vollständig für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]reserviert ist, müssen Sie zusätzlich auch den für andere Verwendungen des Systems benötigten Arbeitsspeicher abziehen.) Die Differenz entspricht der maximalen Arbeitsspeichergröße, die Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zuweisen können.  
  
## <a name="setting-the-memory-options-manually"></a>Manuelles Festlegen der Arbeitsspeicheroptionen  
 Legen Sie **Min. Serverarbeitsspeicher** und **Max. Serverarbeitsspeicher** so fest, dass die Werte einen Bereich des Arbeitsspeichers angeben. Diese Methode ist vor allem dann sinnvoll, wenn der System- oder Datenbankadministrator eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Abhängigkeit von den Arbeitsspeicheranforderungen anderer Anwendungen auf demselben Computer konfigurieren möchte.  
  
 Mithilfe der Konfigurationsoption **Min. Serverarbeitsspeicher** wird sichergestellt, dass für den SQL Server-Speicher-Manager einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eine Mindestmenge an Arbeitsspeicher verfügbar ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Allerdings wird die unter **Min. Serverarbeitsspeicher** angegebene Arbeitsspeichermenge von nicht gleich beim Start zugeordnet. Sobald der Wert für die Speicherauslastung aufgrund der Clientauslastung erreicht ist, kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nur dann Arbeitsspeicher freigeben, wenn der Wert für **Min. Serverarbeitsspeicher** reduziert wird.  
  
> [!NOTE]  
>  Allerdings kann nicht sichergestellt werden, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die in **min server memory** angegebene Arbeitsspeichermenge zuordnet. Wenn die in **min server memory**angegebene Arbeitsspeichermenge aufgrund der Serverlast zu keinem Zeitpunkt zugeordnet werden muss, wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit weniger Arbeitsspeicher ausgeführt.  
  
 Die minimal zulässige Arbeitsspeichermenge für **Max. Serverarbeitsspeicher** beträgt 128 MB.  
  
## <a name="how-to-configure-memory-options-using-sql-server-management-studio"></a>So konfigurieren Sie Speicheroptionen mit SQL Server Management Studio  
 Mit den beiden Arbeitsspeicheroptionen für den Server, **Min. Serverarbeitsspeicher** und **Max. Serverarbeitsspeicher**, können Sie den vom SQL Server-Speicher-Manager für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwalteten Umfang des Arbeitsspeichers (in MB) umkonfigurieren. Standardmäßig können die Arbeitsspeicheranforderungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anhand der verfügbaren Systemressourcen dynamisch geändert werden.  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory"></a>Vorgehensweise beim Konfigurieren eines festen Arbeitsspeichers  
 So legen Sie eine feste Arbeitsspeichergröße fest  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den **Speicher** -Knoten.  
  
3.  Geben Sie unter **Arbeitsspeicheroptionen für den Server**den gewünschten Wert für **Minimaler Serverarbeitsspeicher** und **Maximaler Serverarbeitsspeicher**ein.  
  
     Verwenden Sie die Standardeinstellungen, damit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Arbeitsspeicheranforderungen auf der Grundlage der verfügbaren Systemressourcen dynamisch ändert. Die Standardeinstellung für **Minimaler Serverarbeitsspeicher** ist 0; für **Maximaler Serverarbeitsspeicher** liegt der Standardwert bei 2147483647 Megabyte (MB).  
  
## <a name="maximize-data-throughput-for-network-applications"></a>Maximieren des Datendurchsatzes in Netzwerkanwendungen  
 Um die Nutzung des Systemspeichers für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu optimieren, sollten Sie den Arbeitsspeicher einschränken, der vom System zur Zwischenspeicherung von Dateien verwendet wird. Stellen Sie zum Einschränken des Dateisystemcache sicher, dass die Option **Datendurchsatz für Dateifreigabe maximieren** deaktiviert ist. Sie können den kleinsten Dateisystemcache angeben, indem Sie **Verwendeten Arbeitsspeicher minimieren** oder **Lastenausgleich durchführen**auswählen.  
  
#### <a name="to-check-the-current-setting-on-your-operating-system"></a>So überprüfen Sie die aktuellen Einstellungen des Betriebssystems  
  
1.  Klicken Sie im **Startmenü**auf **Systemsteuerung**, doppelklicken Sie auf **Netzwerkverbindungen**, und doppelklicken Sie dann auf **LAN-Verbindung**.  
  
2.  Klicken Sie auf der Registerkarte **Allgemein** auf **Eigenschaften**, wählen Sie **Datei- und Druckerfreigabe für Microsoft-Netzwerke**aus, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wenn die Option **Datendurchsatz für Netzwerkanwendungen maximieren** ausgewählt ist, wählen Sie ggf. weitere Optionen aus. Klicken Sie auf **OK**, und schließen Sie alle noch geöffneten Dialogfelder.  
  
## <a name="lock-pages-in-memory"></a>Sperren von Seiten im Speicher  
 Mit dieser Windows-Richtlinie werden die Konten bestimmt, die einen Prozess zum Speichern von Daten im physischen Speicher verwenden können, um das systemgesteuerte Auslagern der Daten in den virtuellen Arbeitsspeicher zu vermeiden. Durch Sperren von Seiten im Arbeitsspeicher können Sie die Reaktionsfähigkeit des Servers möglicherweise auch nach Auslagerung von Arbeitsspeicherdaten auf die Festplatte aufrechterhalten. Die SQL Server-Option **Sperren von Seiten im Speicher** wird für Instanzen der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard Edition und höher auf ON gesetzt, wenn dem Konto mit den Privilegien zum Ausführen von "sqlserver.exe" das Windows-Benutzerrecht "Lock Pages in Memory" (LPIM) erteilt wurde.  
  
 Entfernen Sie zum Deaktivieren der Option **Sperren von Seiten im Speicher** für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]das Benutzerrecht "Lock Pages in Memory" für das SQL Server-Startkonto.  
  
### <a name="to-disable-lock-pages-in-memory"></a>So deaktivieren Sie die Option "Sperren von Seiten im Speicher"  
 So deaktivieren Sie die Option "Sperren von Seiten im Speicher"  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**. Geben Sie **gpedit.msc** im Feld **Öffnen**ein.  
  
     Das Dialogfeld **Gruppenrichtlinie** wird geöffnet.  
  
2.  Erweitern Sie in der Konsole **Gruppenrichtlinie** die Option **Computerkonfiguration**und dann **Windows-Einstellungen**.  
  
3.  Erweitern Sie **Sicherheitseinstellungen**und dann **Lokale Richtlinien**.  
  
4.  Wählen Sie den Ordner **Zuweisen von Benutzerrechten** aus.  
  
     Die Richtlinien werden im Detailbereich angezeigt.  
  
5.  Doppelklicken Sie im Detailbereich auf **Sperren von Seiten im Speicher**.  
  
6.  Wählen Sie im Dialogfeld **Lokale Sicherheitseinstellung** das Konto mit Privilegien zum Ausführen von "sqlservr.exe", und klicken Sie auf **Entfernen**.  
  
## <a name="virtual-memory-manager"></a>Manager für virtuellen Arbeitsspeicher  
 Die zugesicherten Bereiche des Adressraums werden vom Windows-Manager für virtuellen Arbeitsspeicher (VMM, Virtual Memory Manager) dem verfügbaren physischen Arbeitsspeicher zugeordnet.  
  
 Weitere Informationen zur von anderen Betriebssystemen unterstützten Größe des physischen Speichers finden Sie in der Windows-Dokumentation "Arbeitsspeichergrenzwerte für Windows-Versionen" (möglicherweise in englischer Sprache).  
  
 Mit virtuellen Speichersystemen kann mehr physischer Arbeitsspeicher zugesichert werden, als tatsächlich vorhanden ist, sodass das Verhältnis von virtuellem zu physischem Arbeitsspeicher das Verhältnis 1:1 überschreiten kann. Auf diese Weise können größere Programme auf Computern mit verschiedenen Konfigurationen des physischen Arbeitsspeichers ausgeführt werden. Wenn jedoch deutlich mehr virtueller Arbeitsspeicher verwendet wird, als die kombinierten durchschnittlichen Workingsets aller Prozesse verwenden, kann dies zu einem ungünstigen Leistungsverhalten führen.  
  
 Bei **min server memory** und **max server memory** handelt es sich um erweiterte Optionen. Wenn Sie diese Einstellungen mithilfe der gespeicherten Systemprozedur **sp_configure** ändern, können Sie diese nur ändern, wenn **Erweiterte Optionen anzeigen** auf 1 festgelegt ist. Diese Einstellungen treten sofort ohne Neustart des Servers in Kraft.  
  
## <a name="running-multiple-instances-of-sql-server"></a>Ausführen mehrerer Instanzen von SQL Server  
 Wenn Sie mehrere Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]ausführen, stehen Ihnen zum Verwalten des Arbeitsspeichers drei Möglichkeiten zur Verfügung:  
  
-   Steuern Sie die Speicherauslastung mithilfe von **max server memory** . Richten Sie für jede Instanz Maximaleinstellungen ein, und achten Sie darauf, dass der gesamte zugeordnete Arbeitsspeicher nicht größer ist als der insgesamt auf dem Computer verfügbare physische Speicher. Es empfiehlt sich, den jeder Instanz zugeordneten Arbeitsspeicher proportional zur erwarteten Arbeitsauslastung oder Datenbankgröße zu bemessen. Dieser Ansatz hat den Vorteil, dass beim Starten neuer Prozesse oder Instanzen sofort freier Arbeitsspeicher für die Prozesse oder Instanzen zur Verfügung steht. Der Nachteil ist, wenn nicht alle Instanzen ausgeführt werden, dass keine der laufenden Instanzen den verbleibenden freien Arbeitsspeicher nutzen kann.  
  
-   Steuern Sie die Speicherauslastung mithilfe von **min server memory** . Richten Sie für jede Instanz Minimaleinstellungen ein, sodass die Summe dieser Mindestwerte 1 bis 2 GB unterhalb des gesamten physischen Speichers auf dem Computer liegt. Auch bei dieser Methode empfiehlt es sich, die Werte proportional zu der für die jeweilige Instanz erwarteten Arbeitsauslastung zu bemessen. Dieser Ansatz hat den Vorteil, dass die laufenden Instanzen den verbleibenden freien Arbeitsspeicher nutzen können, wenn nicht alle Instanzen gleichzeitig ausgeführt werden. Diese Vorgehensweise ist auch dann sinnvoll, wenn auf dem Computer ein weiterer speicherintensiver Prozess vorhanden ist, da sichergestellt ist, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zumindest eine angemessene Menge an Arbeitsspeicher erhält. Der Nachteil besteht darin, dass es beim Starten einer neuen Instanz (oder eines anderen Prozesses) ggf. etwas dauern kann, bis die laufenden Instanzen Speicher freigeben. Dies trifft vor allem dann zu, wenn die Instanzen zuerst noch geänderte Seiten in ihre jeweiligen Datenbanken zurückschreiben müssen.  
  
-   Unternehmen Sie nichts (dies wird nicht empfohlen). Die ersten Instanzen, denen eine Arbeitslast zugewiesen wird, weisen sich den gesamten Arbeitsspeicher zu. Instanzen im Leerlauf oder Instanzen, die später gestartet werden, müssen in dieser Situation u. U. mit einer minimalen Menge an Arbeitsspeicher auskommen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht nicht, die Speicherauslastung über mehrere Instanzen hinweg auszugleichen. Alle Instanzen antworten jedoch auf Signale der Windows-Arbeitsspeicherbenachrichtigung, um ihren Speicherbedarf anzupassen. Windows nimmt keinen Speicherausgleich bei Anwendungen vor, die über eine Arbeitsspeicherbenachrichtigungs-API verfügen. Es erfolgt lediglich eine globale Rückmeldung über die Verfügbarkeit von Arbeitsspeicher auf dem System.  
  
 Sie können diese Einstellungen ohne Neustart der Instanzen ändern. Dadurch können Sie problemlos mit verschiedenen Einstellungen experimentieren, um die für Ihr Nutzungsmuster am besten geeigneten Einstellungen herauszufinden.  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>Bereitstellen der maximalen Menge von Arbeitsspeicher für SQL Server  
 In allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann der Arbeitsspeicher bis zum Speicherplatzlimit des virtuellen Adressraums des Prozesses (8 TB) konfiguriert werden.  
  
 ***/3gb** ist ein Startparameter des Betriebssystems. Weitere Informationen finden Sie in der [MSDN Library](http://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="example-a"></a>Beispiel A  
 Im folgenden Beispiel wird die Option `max server memory` auf 4 GB festgelegt.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'max server memory', 4096;  
GO  
RECONFIGURE;  
GO  
```  
  
### <a name="example-b-determining-current-memory-allocation"></a>Beispiel B: Bestimmen der aktuellen Speicherbelegung  
 Mit der folgenden Abfrage werden Informationen zur aktuellen Speicherbelegung zurückgegeben.  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
