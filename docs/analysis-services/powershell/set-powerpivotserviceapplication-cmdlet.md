---
title: Set-PowerPivotServiceApplication-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 16d10e2d-d7e1-40f1-bc9d-a4e10c61af95
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 094bf7bdb701140a45dacf0236e59d8f9232e5d4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-powerpivotserviceapplication-cmdlet"></a>Set-PowerPivotServiceApplication-Cmdlet
  
 [!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)] 

  Legt die Eigenschaften einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung fest.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
Set-PowerPivotServiceApplication [-Identity] <SPGeminiServiceApplicationPipeBind> [-AdministrationConnectionPoolSize <int>] [-AllowCustomWindowsCredentials] [-BusinessHoursEndTime <string>] [-BusinessHoursStartTime <string>] [-CachedDatabaseholdLimit <int>] [-Confirm <switch>] [-ConnectionPoolSize <int>] [-ConnectionPoolTimeout <int>] [-DataLoadTimeout <int>] [-DataRefreshFailureThreshold <int>] [-DataRefreshInactiveWorkbooksThreshold <int>] [-DataRefreshMaxHistory <int>] [-HealthBasedAllocation <switch>] [-LoadsToConnectionsRatioCollectionInterval <int>] [-LoadsToConnectionsRatioLimit <int>] [-MemoryDatabaseHoldLimit <int>] [-QueryReportingInterval <int>] [-RoundRobinAllocation <switch>] [-UnattendedAccount <string>] [-UsageDataRetentionPeriod <int>] [-UsageExpectedResponseUpperLimit <int>] [-UsageLongResponseUpperLimit <int>] [-UsageQuickResponseUpperLimit <int>] [-UsageTrivialResponseUpperLimit <int>] [-UsageUpdateDayLimit <int>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Das Set-PowerPivotServiceApplication-Cmdlet aktualisiert die Eigenschaften einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung in der Farm. Der Identity-Parameter ist erforderlich. Sie müssen die GUID der Dienstanwendung bereitstellen, für die Sie Eigenschaften aktualisieren.  
  
 Führen Sie das Cmdlet, um die Änderungen zu überprüfen: Get-PowerPivotServiceApplication-Identity \<GUID > | Format-List.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>-Identity \<SPGeminiServiceApplicationPipeBind >  
 Gibt die zu aktualisierende Dienstanwendung an. Der Typ muss eine gültige GUID oder eine Instanz eines gültigen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungsobjekts sein. Sie können Get-PowerPivotServiceApplication verwenden, um eine Instanz des Objekts zurückzugeben.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-administrationconnectionpoolsize-int"></a>-AdministrationConnectionPoolSize \<Int >  
 Gibt die Anzahl der geöffneten Verbindungen in einem Verbindungspool an, der für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstverbindung mit Analysis Services erstellt wurde. Jede [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstinstanz öffnet eine separate Administratorverbindung zur Analysis Services-Instanz auf demselben Computer. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst erstellt einen separaten Pool, damit Administratorverbindungen wiederverwendet werden können, um Verbindungen im Leerlauf zu suchen und den Serverstatus zu überwachen. Der Standardwert ist 200 Verbindungen. Gültige Werte sind -1 (unbegrenzt), 0 (deaktiviert die Verwendung des Verwaltungsverbindungspools) oder 1 bis 10000. Wenn Sie 0 auswählen, wird jede Verbindung neu erstellt.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|200|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-allowcustomwindowscredentials-switchparameter"></a>-AllowCustomWindowsCredentials [\<Switch-Parameter >]  
 Gibt an, ob Zeitplanbesitzer beliebige Windows-Anmeldeinformationen eingeben können, um einen Zeitplan zur Datenaktualisierung auszuführen. Wenn Sie dieses Kontrollkästchen aktivieren, erstellt und verwaltet die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung eine Zielanwendung für jeden Satz gespeicherter Anmeldeinformationen. Die Standardeinstellung ist true. Legen Sie AllowCustomWindowsCredentials:$false fest, um diese Funktion zu deaktivieren.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-businesshoursendtime-string"></a>-BusinessHoursEndTime \<Zeichenfolge >  
 Gibt den Endpunkt in einem Bereich von Stunden an, die einen Geschäftstag definieren. Zeitpläne zur Datenaktualisierung können am Ende eines Geschäftstags ausgeführt werden, um die während der regulären Geschäftszeiten generierten Transaktionsdaten zu sammeln. Die Standardeinstellung ist 8:00 p.m. (20:00 Uhr).  Gültige Werte werden in Anführungszeichen mit dem Zusatz AM oder PM angegeben (z. B. "08:00PM"). Der Stundenwert muss zwischen 1 und 12 liegen. Der Minutenwert muss zwischen 1 und 59 liegen.  
  
 Um für einen Geschäftstag den vollständigen Stundenbereich anzugeben, müssen Sie sowohl BusinessHoursStartTime als auch BusinessHoursEndTime festlegen. Mit diesen beiden Parametern wird das Stundenintervall für einen Geschäftstag definiert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|8 PM|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-businesshoursstarttime-string"></a>-BusinessHoursStartTime \<Zeichenfolge >  
 Gibt den Startpunkt in einem Bereich von Stunden an, die einen Geschäftstag definieren. Zeitpläne zur Datenaktualisierung können am Ende eines Geschäftstags ausgeführt werden, um die während der regulären Geschäftszeiten generierten Transaktionsdaten zu sammeln. Die Standardeinstellung ist 4:00 a.m.  Gültige Werte werden in Anführungszeichen mit dem Zusatz AM oder PM angegeben (z. B. "04:00AM"). Der Stundenwert muss zwischen 1 und 12 liegen. Der Minutenwert muss zwischen 1 und 59 liegen.  
  
 Um für einen Geschäftstag den vollständigen Stundenbereich anzugeben, müssen Sie sowohl BusinessHoursStartTime als auch BusinessHoursEndTime festlegen. Mit diesen beiden Parametern wird das Stundenintervall für einen Geschäftstag definiert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|4 AM|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-cacheddatabaseholdlimit-int"></a>-CachedDatabaseholdLimit \<Int >  
 Gibt an, wie viele Stunden eine inaktive Datenbank im Dateisystem beibehalten wird, nachdem sie aus dem Arbeitsspeicher entladen wurde. Der Standardwert ist 120 Stunden. Der Cleanupauftrag verwendet diese Einstellung, um die zu löschenden Dateien zu bestimmen. Alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken, die 168 Stunden lang (48 Stunden im Arbeitsspeicher und 120 Stunden im Cache) inaktiv sind, werden durch den Cleanupauftrag vom Datenträger gelöscht.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|120|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-confirm-switch"></a>-Bestätigen Sie \<wechseln >  
 Fordert eine Bestätigung an, bevor der Befehl ausgeführt wird. Dieser Wert ist standardmäßig aktiviert. Geben Sie Confirm:$false für einen Befehl an, um die Bestätigungsantwort in einem Befehl zu umgehen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-connectionpoolsize-int"></a>ConnectionPoolSize - \<Int >  
 Gibt die maximale Anzahl von Verbindungen im Leerlauf an, die der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst in einzelnen Verbindungspools für die einzelnen SharePoint-Benutzer, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datasets und Versionskombinationen erstellt. Der Standardwert ist 1.000 Verbindungen im Leerlauf. Gültige Werte sind -1 (unbegrenzt), 0 (deaktiviert das Pooling von Benutzerverbindungen) oder 1 bis 10.000. Durch diese Verbindungspools kann der Dienst fortlaufende Verbindungen mit den gleichen schreibgeschützten Daten, die vom selben Benutzer hergestellt werden, effizienter unterstützen. Wenn Sie das Verbindungspooling deaktivieren, wird jede Verbindung erneut erstellt. Beachten Sie, dass Änderungen am Grenzwert der Verbindungspoolgröße (auch die Festlegung auf 0) nicht dazu führen, dass Verbindungen getrennt werden. Verbindungspools sind vorhanden, um Wartezeiten beim Herstellen einer Datenverbindung zu reduzieren. Der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst wird nie eine Verbindung aufgrund von Verbindungspooleinstellungen ablehnen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|1000|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-connectionpooltimeout-int"></a>-ConnectionPoolTimeout \<Int >  
 Gibt an, wie viele Minuten eine Datenverbindung im Leerlauf geöffnet bleibt. Der Standardwert ist 1800 Sekunden (oder 30 Minuten). Während dieses Zeitraums wird die Datenverbindung im Leerlauf für schreibgeschützte Anforderungen vom gleichen SharePoint-Benutzer für die gleichen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten von der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung wiederverwendet. Wenn im angegebenen Zeitraum keine weiteren Anforderungen für diese Daten empfangen werden, wird die Verbindung aus dem Pool entfernt. Gültige Werte reichen von 1 bis 3600 Sekunden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|1800|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-dataloadtimeout-int"></a>-DataLoadTimeout \<Int >  
 Gibt an, wie lange die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung auf eine Antwort von der SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])-Instanz wartet, an die eine Anforderung zum Laden von Daten weitergeleitet wurde. Da die Übertragung sehr großer Datasets einige Zeit dauern kann, müssen Sie genügend Zeit vorsehen, damit die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstinstanz die Excel-Arbeitsmappe abrufen und die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten zur Abfrageverarbeitung in eine Analysis Services-Instanz verschieben kann. Der Standardwert ist 1800 Sekunden (oder 30 Minuten). Gültige Werte reichen von 1 bis 3600 Sekunden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|1800|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-datarefreshfailurethreshold-int"></a>-DataRefreshFailureThreshold \<Int >  
 Gibt die Anzahl der aufeinander folgenden Fehler an, nach der ein Zeitplan deaktiviert wird. Der Standardwert lautet 10. Sie können auch 0 eingeben, wenn ein Zeitplan nie infolge von Aktualisierungsfehlern deaktiviert werden soll.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|10|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-datarefreshinactiveworkbooksthreshold-int"></a>-DataRefreshInactiveWorkbooksThreshold \<Int >  
 Geben Sie die Anzahl von Datenaktualisierungszyklen ein, nach denen ein Zeitplan deaktiviert wird. Sie können auch 0 eingeben, wenn ein Zeitplan nie aufgrund von Inaktivität deaktiviert werden soll. Die Standardeinstellung ist 10 Zyklen.  
  
 Die Inaktivität von Arbeitsmappen wird als Fehlen von Verbindungsereignissen über mehrere Datenaktualisierungszyklen gemessen. Ein Datenaktualisierungszyklus wird jedes Mal gezählt, wenn ein Datenaktualisierungsvorgang ausgelöst wird (entweder vom Zeitplan oder einem "Jetzt ausführen"-Vorgang), unabhängig davon, ob der Vorgang erfolgreich ist oder fehlschlägt. Nach Ablauf einer Anzahl von Zyklen (standardmäßig 10) ohne Verbindungsanforderungen für die Arbeitsmappe wird der Datenaktualisierungszeitplan wegen Inaktivität deaktiviert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|10|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-datarefreshmaxhistory-int"></a>-DataRefreshMaxHistory \<Int >  
 Gibt an, wie lange ein Verlaufsdatensatz der Datenaktualisierungsverarbeitung beibehalten wird. Diese Informationen werden auf den Seiten für den Datenaktualisierungsverlauf angezeigt, die für jede Arbeitsmappe angelegt werden, die die Datenaktualisierung nutzt. Sie werden auch im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard angezeigt. Die Standardeinstellung ist 365 Tage.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|365|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-healthbasedallocation-switch"></a>-HealthBasedAllocation \<wechseln >  
 Gibt den zustandsbasierten Zuordnungsalgorithmus an, der Verbindungsanforderungen an [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Server mit der höchsten Verfügbarkeit an CPU- und Speicherressourcen weiterleitet. Dies ist der standardmäßige Zuordnungsalgorithmus. HealthBasedAllocation und RoundRobinBasedAllocation schließen sich gegenseitig aus. Sie müssen eines dieser Zuordnungsverfahren angeben. Wenn Sie beide Optionen auf false festlegen, wird HealthBasedAllocation verwendet, da dies die Standardeinstellung ist. Wenn Sie beide Optionen auf true festlegen, tritt ein Überprüfungsfehler auf. Als Syntax dieser Parameter können Sie entweder nur den Parameternamen oder parameter:$true bzw. parameter:$false eingeben.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-loadstoconnectionsratiocollectioninterval-int"></a>-LoadsToConnectionsRatioCollectionInterval \<Int >  
 Geben Sie das Intervall (in Stunden) an, um Lade- und Verbindungsereignisse zum Berechnen des Lade-/Verbindungsverhältnisses zu zählen. Standardmäßig berechnet das System alle 4 Stunden ein neues Verhältnis. Gültige Werte reichen von 1 bis 24.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|4|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-loadstoconnectionsratiolimit-int"></a>-LoadsToConnectionsRatioLimit \<Int >  
 Gibt das Verhältnis von Ladeereignissen und Verbindungsereignissen an, das als Indikator des Serverzustands verwendet wird. Die Standardeinstellung ist 20 Prozent.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|20|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-memorydatabaseholdlimit-int"></a>MemoryDatabaseHoldLimit - \<Int >  
 Gibt an, wie viele Stunden eine inaktive Datenbank im Arbeitsspeicher bleibt, um neue Anforderungen für diese Daten zu verarbeiten. Eine aktive Datenbank wird immer im Arbeitsspeicher beibehalten, solange Sie sie abfragen. Wenn die Datenbank jedoch nicht mehr aktiv ist, behält das System sie für einen zusätzlichen Zeitraum im Arbeitsspeicher, falls weitere Anforderungen für diese Daten empfangen werden. Der Standardwert beträgt 48 Stunden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|48|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-queryreportinginterval-int"></a>-QueryReportingInterval \<Int >  
 Gibt an, wie viele Sekunden Statistikdaten zu Abfrageantworten gesammelt werden, bevor ein Verwendungsereignis in einen Bericht geschrieben wird. Der Standardwert ist 300 Sekunden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|300|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-roundrobinallocation-switch"></a>– RoundRobinAllocation \<wechseln >  
 Gibt den Roundrobin-Zuordnungsalgorithmus an, der Verbindungsanfragen an den nächsten [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Server weiterleitet. Dabei werden die Anforderungen unabhängig von der Serverlast gleichmäßig auf die verfügbaren Server aufgeteilt. HealthBasedAllocation und RoundRobinBasedAllocation schließen sich gegenseitig aus. Sie müssen eines dieser Zuordnungsverfahren angeben. Wenn Sie beide Optionen auf false festlegen, wird HealthBasedAllocation verwendet, da dies die Standardeinstellung ist. Wenn Sie beide Optionen auf true festlegen, tritt ein Überprüfungsfehler auf. Als Syntax dieser Parameter können Sie entweder nur den Parameternamen oder parameter:$true bzw. parameter:$false eingeben.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-unattendedaccount-string"></a>-UnattendedAccount \<Zeichenfolge >  
 Gibt den Zielanwendungsnamen einer Secure Store Service-Anwendung an, unter der ein vordefiniertes Konto zum Ausführen von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenaktualisierungsaufträgen gespeichert wird.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-usagedataretentionperiod-int"></a>-UsageDataRetentionPeriod \<Int >  
 Gibt die Anzahl von Tagen an, die statistische Verwendungs- und Serverstatus-Verlaufsdaten beibehalten werden sollen. Die Standardeinstellung beträgt 365 Tage. Wenn Sie diesen Wert auf 0 festlegen, wird der gesamte Verlauf unbegrenzt beibehalten.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|365|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-usageexpectedresponseupperlimit-int"></a>-UsageExpectedResponseUpperLimit \<Int >  
 Legt eine Obergrenze fest, die die erwartete Dauer für den Austausch einer Anforderung/Antwort definiert. Der Standardwert beträgt 3000 Millisekunden. Jede Anforderung, die innerhalb von 1000 bis 3000 Millisekunden abgeschlossen wird, wird zu Berichtszwecken als erwartete Antwortdauer angesehen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|3000|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-usagelongresponseupperlimit-int"></a>-UsageLongResponseUpperLimit \<Int >  
 Legt eine Obergrenze fest, die den Austausch einer Anforderung/Antwort mit langer Laufzeit definiert.  Die Obergrenze beträgt 10.000 Millisekunden. Alle Anforderungen, die diese Obergrenze überschreiten, gehören zur Kategorie Überschritten, die keinen oberen Schwellenwert aufweist.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|10000|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-usagequickresponseupperlimit-int"></a>-UsageQuickResponseUpperLimit \<Int >  
 Legt eine Obergrenze fest, die den Austausch einer schnellen Anforderung/Antwort definiert. Der Standardwert beträgt 1.000 Millisekunden. Jede Anforderung, die innerhalb von 500 bis 1000 Millisekunden abgeschlossen wird, wird zu Berichtszwecken als schnelle Antwort angesehen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|1000|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-usagetrivialresponseupperlimit-int"></a>-UsageTrivialResponseUpperLimit \<Int >  
 Gibt eine Kategorie von Antwortzeiten an, die zu niedrig sind, um für Datensammlungszwecke als relevant angesehen zu werden. Die meisten Antworten, die in diese Kategorie fallen, sind der Server-zu-Server-Kommunikation zuzuordnen. Der Standardwert beträgt 500 Millisekunden. Jede Anforderung, die innerhalb von 0 bis 500 Millisekunden abgeschlossen wird, ist eine triviale Anforderung und wird bei der Berichterstellung ignoriert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|500|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-usageupdatedaylimit-int"></a>-UsageUpdateDayLimit \<Int >  
 Geben Sie den Schwellenwert (in Tagen) an, bei dem eine Warnung ausgelöst wird, falls die Datendatei, die von Berichten im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard verwendet wird, nicht aktualisiert wird. Standardmäßig aktualisiert das System die Verwendungsdaten täglich. Die Datei „ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Management Dashboard.xlsx“, die als Datenquelle für Administratorberichte dient, wird nach dem gleichen Zeitplan aktualisiert. Wenn die XLSX-Datei über mehrere Tage hinweg nicht aktualisiert wird, wird eine Integritätsregel ausgelöst, die darauf hinweist, dass die Datei veraltet ist. Die Standardeinstellung beträgt 5 Tage. Gültige Werte sind 1 bis 30.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|5|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die folgenden allgemeinen Parameter: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer und OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|Keine.|  
  
## <a name="example-1"></a>Beispiel 1  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -AllowCustomWindowsCredentials:$false -UnattendedAccount "MyTargetApp"  
```  
  
 In diesem Beispiel wird eine Datenaktualisierungsfunktion deaktiviert, die automatisch Secure Store Service-Zielanwendungen zum Speichern von beliebigen Windows-Anmeldeinformationen erstellt und verwaltet. Außerdem wird das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konto für die unbeaufsichtigte Datenaktualisierung auf eine vordefinierte Zielanwendung festgelegt.  
  
 Verwenden Sie Get-powerpivotserviceapplication, um eine gültige Identität abzurufen.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -HealthBasedAllocation  
```  
  
 In diesem Beispiel wird der zustandsbasierte Zuordnungsalgorithmus angegeben, der Verbindungsanforderungen an den Server weiterleitet, auf dem die meisten Ressourcen verfügbar sind.  
  
 Verwenden Sie Get-powerpivotserviceapplication, um eine gültige Identität abzurufen.  
  
## <a name="example-3"></a>Beispiel 3  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklmn -BusinessHoursStartTime "07:15AM" -BusinessHoursEndTime "08:00PM"  
```  
  
 In diesem Beispiel wird veranschaulicht, wie Sie die erste und letzte Stunde eines Geschäftstags festlegen. Dieser Vorgang wird als Zeitplanoption zum Planen der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenaktualisierung verwendet. In einem Zeitplan kann eine Option für die Zeit außerhalb der Geschäftsstunden angegeben werden, um die Datenaktualisierung nach Ende des Geschäftstags auszuführen.  
  
 Verwenden Sie Get-powerpivotserviceapplication, um eine gültige Identität abzurufen.  
  
  
