---
title: "Datenbankprüfpunkte (SQL Server) | Microsoft-Dokumentation"
ms.date: 09/23/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic checkpoints
- transaction logs [SQL Server], checkpoints
- logs [SQL Server], active
- pages [SQL Server], dirty
- MinLSN
- checkpoints [SQL Server]
- pages [SQL Server], flushing
- dirty pages
- transaction logs [SQL Server], active logs
- recovery interval option [SQL Server]
- buffer cache [SQL Server]
- logs [SQL Server], checkpoints
- Minimum Recovery LSN
- flushing pages
- active logs
ms.assetid: 98a80238-7409-4708-8a7d-5defd9957185
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7c82c775f808b1747261f3ce33d46ca467d8bca1
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="database-checkpoints-sql-server"></a>Datenbankprüfpunkte (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 Ein *Prüfpunkt* erstellt einen bekannten fehlerfreien Punkt, von dem aus [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Änderungen übernehmen kann, die im Protokoll während der Wiederherstellung nach einem unerwarteten Herunterfahren oder einem Absturz enthalten sind.  
 
  
##  <a name="Overview"></a> Übersicht   
Aus Leistungsgründen führt [!INCLUDE[ssDE](../../includes/ssde-md.md)] Änderungen an Datenbankseiten im Arbeitsspeicher aus (im Puffercache) und schreibt diese Seiten nicht nach jeder Änderung auf den Datenträger. Vielmehr gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] in regelmäßigen Abständen einen Prüfpunkt auf jeder Datenbank aus. Ein *Prüfpunkt* schreibt die aktuellen, speicherintern geänderten Seiten (auch bekannt als *modifizierte Seiten*) sowie Transaktionsprotokollinformationen vom Arbeitsspeicher auf den Datenträger und erfasst auch Informationen zum Transaktionsprotokoll.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] unterstützt mehrere Typen von Prüfpunkten. Dazu gehören "automatisch", "indirekt", "manuell" und "intern". In der folgenden Tabelle werden die **Prüfpunkttypen**zusammengefasst:
  
|Name|[!INCLUDE[tsql](../../includes/tsql-md.md)] -Schnittstelle|Description|  
|----------|----------------------------------|-----------------|  
|Automatic|EXEC sp_configure **'**Wiederherstellungsintervall**','***Sekunden***'**|Wird automatisch im Hintergrund ausgegeben, um das obere, mittels Serverkonfigurationsoption **Wiederherstellungsintervall** vorgeschlagene Zeitlimit zu erfüllen. Automatische Prüfpunkte werden vollständig ausgeführt.  Automatische Prüfpunkte werden auf Basis der Anzahl an ausstehenden Schreibvorgängen gedrosselt. Zudem hängt die Drosselung auch davon ab, ob [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Erhöhung der Schreiblatenz auf über 50 Millisekunden erkennt.<br /><br /> Weitere Informationen finden Sie unter [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).|  
|Indirekt|ALTER DATABASE … SET TARGET_RECOVERY_TIME **=***Zielwiederherstellungszeit* { SECONDS &#124; MINUTES }|Wird im Hintergrund ausgegeben, um eine benutzerdefinierte Zielwiederherstellungszeit für eine bestimmte Datenbank zu erfüllen. Ab [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]ist der Standardwert 1 Minute. Der Standard für ältere Versionen ist 0 und gibt an, dass die Datenbank automatische Prüfpunkte verwendet, deren Frequenz von der Einstellung für das Wiederherstellungsintervall der Serverinstanz abhängt.<br /><br /> Weitere Informationen finden Sie unter [Ändern der Zielwiederherstellungszeit einer Datenbank &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md).|  
|Manuell|CHECKPOINT [ *checkpoint_duration* ]|Wird ausgegeben, wenn Sie einen [!INCLUDE[tsql](../../includes/tsql-md.md)] -CHECKPOINT-Befehl ausführen. Der manuelle Prüfpunkt tritt in der aktuellen Datenbank für die Verbindung auf. Standardmäßig werden manuelle Prüfpunkte vollständig ausgeführt. Das Drosseln erfolgt auf die gleiche Weise wie für automatische Prüfpunkte.  Optional gibt der *checkpoint_duration* -Parameter die Anforderung an, welchen Zeitraum in Sekunden ein Prüfpunkt benötigen darf, bis er abgeschlossen ist.<br /><br /> Weitere Informationen finden Sie unter [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md).|  
|Intern|Keine.|Wird von verschiedenen Servervorgängen wie Sicherung und Erstellung einer Datenbank-Momentaufnahme ausgegeben. So wird gewährleistet, dass Datenträgerabbilder dem aktuellen Protokollstatus entsprechen.|  
  
>[!NOTE]
> **-k** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht Datenbankadministratoren, das Prüfpunkt-E/A-Verhalten auf Basis des Durchsatzes des E/A-Teilsystems für einige Typen von Prüfpunkten zu drosseln. Die Setupoption **-k** gilt für automatische Prüfpunkte sowie für andere nicht gedrosselte manuelle und interne Prüfpunkte.  
  
 Für automatische, manuelle und interne Prüfpunkte muss nur für Änderungen, die nach dem letzten Prüfpunkt erfolgt sind, während der Datenbankwiederherstellung ein Rollforward ausgeführt werden. Dadurch verringert sich die Zeit, die zur Wiederherstellung einer Datenbank erforderlich ist.  
  
>[!IMPORTANT]
> Lang andauernde Transaktionen ohne Commit erhöhen die Wiederherstellungszeit für alle Prüfpunkttypen.  
  
  
##  <a name="InteractionBwnSettings"></a> Interaktion der Optionen "TTARGET_RECOVERY_TIME" und "Wiederherstellungsintervall"  
 In der folgenden Tabelle wird die Interaktion zwischen der serverweiten Einstellung **sp_configure'**recovery interval**'** und der datenbankspezifischen ALTER DATABASE … TARGET_RECOVERY_TIME-Einstellung zusammengefasst.  
  
|Zielwiederherstellungszeit|'Wiederherstellungsintervall'|Verwendeter Prüfpunkttyp|  
|----------------------------|-------------------------|-----------------------------|  
|0|0|Automatische Prüfpunkte, deren Zielwiederherstellungsintervall 1 Minute beträgt.|  
|0|>0|Automatische Prüfpunkte, deren Zielwiederherstellungsintervall anhand der benutzerdefinierten Einstellung der Option **sp_configure recovery interval** angegeben wurde.|  
|>0|Nicht verfügbar.|Indirekte Prüfpunkte, deren Zielwiederherstellungszeit anhand der TARGET_RECOVERY_TIME-Einstellung definiert ist (in Sekunden ausgedrückt).|  
  
##  <a name="AutomaticChkpt"></a> Automatische Prüfpunkte  
 Ein automatischer Prüfpunkt tritt auf, sobald die Anzahl von Protokolldatensätzen die Anzahl der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Schätzungen erreicht, die während der Zeit verarbeitet werden können, die in der Serverkonfigurationsoption **Wiederherstellungsintervall** angegeben ist. 
 
 In jeder Datenbank ohne benutzerdefinierte Zielwiederherstellungszeit generiert [!INCLUDE[ssDE](../../includes/ssde-md.md)] automatische Prüfpunkte. Die Frequenz richtet sich nach der erweiterten Serverkonfigurationsoption **Wiederherstellungsintervall** , mit der die maximale Zeit angegeben wird, die von einer bestimmten Serverinstanz zur Datenbankwiederherstellung während eines Systemneustarts benötigt werden sollte. [!INCLUDE[ssDE](../../includes/ssde-md.md)] schätzt die maximale Anzahl an Protokolldatensätzen, die innerhalb des Wiederherstellungsintervalls verarbeitet werden können. Erreicht eine Datenbank, die automatische Prüfpunkte verwendet, diese maximale Anzahl an Protokolldatensätzen, gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Prüfpunkt in der Datenbank aus. 
 
 Das Zeitintervall zwischen automatischen Prüfpunkten kann **in hohem Maß** variieren. Bei einer Datenbank mit einer beträchtlichen Transaktionsarbeitsauslastung treten häufiger Prüfpunkte auf als bei einer Datenbank für hauptsächlich schreibgeschützte Vorgänge. Im einfachen Wiederherstellungsmodell wird ein automatischer Prüfpunkt auch in die Warteschlange aufgenommen, wenn das Protokoll zu 70 Prozent gefüllt ist.  
  
Unter dem einfachen Wiederherstellungsmodell wird der ungenutzte Abschnitt des Transaktionsprotokolls durch einen automatischen Prüfpunkt abgeschnitten, sofern nicht gewisse Faktoren die Protokollkürzung verzögern. Im Gegensatz dazu lösen automatische Prüfpunkte im vollständigen und im massenprotokollierten Wiederherstellungsmodell keine Protokollkürzung aus, sobald eine Protokollsicherungskette eingerichtet wurde. Weitere Informationen finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Nach einem Systemabsturz richtet sich die Zeitdauer, die für die Wiederherstellung einer bestimmten Datenbank erforderlich ist, in hohem Maß nach der Menge zufälliger E/A-Vorgänge, die zur Wiederherstellung der zum Zeitpunkt des Absturzes modifizierten Seiten erforderlich sind. Dies bedeutet, dass die Einstellung **Wiederherstellungsintervall** nicht zuverlässig ist. Sie ermöglicht keine genaue Bestimmung der Wiederherstellungsdauer. Zudem erhöht sich die allgemeine E/A-Aktivität für Daten erheblich und eher unvorhersehbar, wenn ein automatischer Prüfpunkt ausgeführt wird.  
  
 
###  <a name="PerformanceImpact"></a> Auswirkungen des Wiederherstellungsintervalls auf die Wiederherstellungsleistung  
 Bei einem System zur Onlinetransaktionsverarbeitung (Online Transaction Processing, OLTP), das Transaktionen mit kurzer Ausführungszeit verwendet, ist das **Wiederherstellungsintervall** der wichtigste Faktor für die Bestimmung der Wiederherstellungszeit. Die Option **Wiederherstellungsintervall** wirkt sich jedoch nicht auf die Zeit aus, die für das Rückgängigmachen einer Transaktion mit langer Ausführungszeit erforderlich ist. Die Wiederherstellung einer Datenbank mit einer Transaktion mit langer Ausführungszeit kann deutlich länger dauern als mit der Option **Wiederherstellungsintervall** angegeben. 
 
 Wenn beispielsweise eine Transaktion mit langer Ausführungszeit zwei Stunden für Updates benötigt hat, bevor die Serverinstanz deaktiviert wurde, dauert die tatsächliche Wiederherstellung erheblich länger als im Wert für das **Wiederherstellungsintervall** zur Wiederherstellung der Transaktion mit langer Ausführungszeit angegeben. Weitere Informationen zu den Auswirkungen einer Transaktion mit langer Ausführungszeit auf die Wiederherstellungsdauer finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 In der Regel gewährleisten die Standardwerte eine optimale Wiederherstellungsleistung. Durch Ändern des Wiederherstellungsintervalls kann sich jedoch die Leistung in folgenden Fällen verbessern:  
  
-   Die Wiederherstellung dauert routinemäßig bedeutend länger als 1 Minute, wenn kein Rollback für Transaktionen mit langer Laufzeit ausgeführt wird.  
  
-   Sie stellen fest, dass häufige Prüfpunkte die Datenbankleistung beeinträchtigen.  
  
 Wenn Sie die Einstellung **recovery interval** erhöhen möchten, empfehlen wir eine schrittweise Erhöhung des entsprechenden Werts. Werten Sie zudem die Auswirkungen der jeweiligen stufenweisen Erhöhung auf die Wiederherstellungsleistung aus. Diese Vorgehensweise ist wichtig, da mit der Erhöhung des Werts für die Einstellung **Wiederherstellungsintervall** die Ausführung der Datenbankwiederherstellung entsprechend länger dauert. Ändern Sie beispielsweise den Wert für das **Wiederherstellungsintervall** in 10 Minuten, dauert die Wiederherstellung ungefähr 10-mal länger als bei einem **Wiederherstellungsintervall** -Wert von 1 Minute.  
  
  
##  <a name="IndirectChkpt"></a> Indirekte Prüfpunkte  
 Indirekte Prüfpunkte (eingeführt in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) stellen auf Datenbankebene eine konfigurierbare Alternative zu automatischen Prüfpunkten dar. Im Fall eines Systemabsturzes ermöglichen indirekte Prüfpunkte eine potenziell schnellere und besser vorhersehbare Wiederherstellungszeit als automatische Prüfpunkte. Indirekte Prüfpunkte bieten folgende Vorteile:  
  
-   Im Fall einer Arbeitsauslastung für Onlinetransaktionen bei einer Datenbank, die für indirekte Prüfpunkte konfiguriert ist, kann eine Verringerung der Leistung auftreten. Indirekte Prüfpunkte stellen sicher, dass die Anzahl der modifizierten Seiten unter einem bestimmten Schwellenwert liegt, sodass die Datenbankwiederherstellung innerhalb der Zielwiederherstellungszeit abgeschlossen wird. 

Die Konfigurationsoption „Wiederherstellungsintervall“ ermittelt die Wiederherstellungszeit über die Anzahl der Transaktionen. Im Gegensatz dazu greifen indirekte Prüfpunkte auf die Anzahl der modifizierten Seiten zurück. Wenn für eine Datenbank, die eine große Anzahl von DML-Vorgängen empfängt, indirekte Prüfpunkte aktiviert sind, können beim Schreiben im Hintergrund leere modifizierte Puffer aggressiv auf den Datenträger geleert werden. Dadurch wird sichergestellt, dass der Zeitaufwand für die Wiederherstellung innerhalb der Zielwiederherstellungszeit der Datenbank liegt. Dies kann auf bestimmten Systemen zusätzliche E/A-Aktivitäten verursachen, die zu einem Leistungsengpass beitragen können, wenn das Datenträgersubsystem über oder nahe dem E/A-Schwellenwert arbeitet.  
  
-   Indirekte Prüfpunkte ermöglichen Ihnen eine zuverlässige Kontrolle der Datenbankwiederherstellungszeit, indem die Kosten für das zufällige E/A-Volumen während des REDO-Vorgangs berücksichtigt werden. Dadurch überschreitet eine Serverinstanz nicht den Obergrenzwert der Wiederherstellungszeiten für eine bestimmte Datenbank, sofern eine Transaktion mit langer Laufzeit keine übermäßig langen UNDO-Vorgänge verursacht.  
  
-   Indirekte Prüfpunkte reduzieren prüfpunktbezogene E/A-Spitzen, indem modifizierte Seiten im Hintergrund kontinuierlich auf den Datenträger geschrieben werden.  
  
 Im Fall einer Arbeitsauslastung für Onlinetransaktionen bei einer Datenbank, die für indirekte Prüfpunkte konfiguriert ist, kann jedoch eine Verringerung der Leistung auftreten. Dies ist darauf zurückzuführen, dass der Hintergrundschreiber, der von indirekten Prüfpunkten verwendet wird, manchmal die Gesamtarbeitsauslastung zum Schreiben für eine Serverinstanz erhöht.  
 
 > [!IMPORTANT]
 > Indirekte Prüfpunkte sind das Standardverhalten für neue Datenbanken , die in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] erstellt wurden. Datenbanken, die direkt aktualisiert oder aus einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wiederhergestellt wurden, verwenden das frühere Verhalten der automatischen Prüfpunkte, sofern nicht explizit die Verwendung indirekter Prüfpunkte angegeben wurde.
  
  
##  <a name="EventsCausingChkpt"></a> Interne Prüfpunkte  
 Interne Prüfpunkte werden von verschiedenen Serverkomponenten generiert, um so gewährleisten zu können, dass Datenträgerabbilder dem aktuellen Protokollstatus entsprechen. Interne Prüfpunkte werden als Antwort auf die folgenden Ereignisse erstellt:  
  
-   Datenbankdateien wurden mit ALTER DATABASE hinzugefügt oder entfernt.  
  
-   Eine vollständige Datenbanksicherung wird ausgeführt.  
  
-   Eine Datenbank-Momentaufnahme wird erstellt, entweder explizit oder intern für DBCC CHECK.  
  
-   Eine Aktivität wird ausgeführt, für die das Herunterfahren einer Datenbank erforderlich ist. Beispielsweise besitzt AUTO_CLOSE den Status ON, und die letzte Benutzerverbindung mit der Datenbank wird geschlossen, oder eine Änderung einer Datenbankoption wird vorgenommen, für die ein Neustart der Datenbank erforderlich ist.  
  
-   Eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz wird beendet, indem der Dienst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) beendet wird. Durch jede der Aktionen wird ein Prüfpunkt in jeder Datenbank der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgelöst.  
  
-   Aktivieren des Offlinemodus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstanz (FCI).  
  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So ändern Sie das Wiederherstellungsintervall auf einer Serverinstanz**  
  
-   [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)  
  
 **So konfigurieren Sie indirekte Prüfpunkte auf einer Datenbank**  
  
-   [Ändern der Zielwiederherstellungszeit einer Datenbank &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)  
  
 **So geben Sie einen manuellen Prüfpunkt auf einer Datenbank aus**  
  
-   [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  

  
## <a name="see-also"></a>Siehe auch  
 - [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) 
 -   [Physische Architektur des Transaktionsprotokolls](http://technet.microsoft.com/library/ms179355.aspx) (aus der [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] -Onlinedokumentation, aber noch immer gültig!)  
  
  
