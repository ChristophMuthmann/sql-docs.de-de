---
title: Registrieren einer Instanz von SQL Server (SQL Server-Hilfsprogramm) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.SWB.makemanaged.agentaccount.F1
- sql13.SWB.makemanaged.welcome.F1
- sql13.SWB.makemanaged.enrolling.F1
- sql13.SWB.makemanaged.instancename.F1
- sql13.SWB.makemanaged.Summary.F1
- sql13.SWB.makemanaged.progress.F1
- sql13.SWB.makemanaged.validation.F1
helpviewer_keywords:
- Enroll instance
ms.assetid: a801c619-611b-4e82-a8d8-d1e01691b7a1
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c5bb6279f7fd96f30aa3f19628e2edc5edb5cc53
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="enroll-an-instance-of-sql-server-sql-server-utility"></a>Registrieren einer Instanz von SQL Server (SQL Server-Hilfsprogramm)
  Registrieren Sie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einem vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm, um deren Leistung und Konfiguration als verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu überwachen. Der Steuerungspunkt für das Hilfsprogramm (UCP) erfasst alle 15 Minuten Konfigurations- und Leistungsinformationen von verwalteten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen. Diese Informationen werden auf dem UCP im Utility Management Data Warehouse (UMDW) gespeichert. Der UMDW-Dateiname lautet "sysutility_mdw". [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Leistungsdaten werden mit Richtlinien verglichen, sodass Sie Engpässe bei der Ressourcennutzung und Konsolidierungsmöglichkeiten leichter erkennen können.  
  
 In dieser Version müssen der UCP und alle verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die folgenden Anforderungen erfüllen:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss Version 10.50 oder höher entsprechen.  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanztyp muss dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]entsprechen.  
  
-   Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm muss innerhalb einer einzelnen Windows-Domäne oder zwischen Domänen ausgeführt werden, die sich gegenseitig vertrauen.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonten auf dem UCP und alle verwalteten Instanzen von SQL Server müssen über die Leseberechtigung für Benutzer in Active Directory verfügen.  
  
-   Die zu registrierende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz darf nicht SQL Azure sein.  
  
 In dieser Version muss der UCP die folgenden Anforderungen erfüllen:  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz muss eine unterstützte Edition sein. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   Als Host für den UCP wird eine SQL Server-Instanz empfohlen, bei der Groß-/Kleinschreibung beachtet wird.  
  
-   Berücksichtigen Sie die folgenden Empfehlungen für die Kapazitätsplanung auf dem UCP-Computer:  
  
    -   In einem typischen Szenario beträgt der von der UMDW-Datenbank (sysutility_mdw) auf dem UCP belegte Speicherplatz ungefähr 2 GB pro verwalteter SQL Server-Instanz im Jahr. Diese Schätzung kann sich je nach der Anzahl der Datenbank- und Systemobjekte ändern, die von der verwalteten Instanz gesammelt werden. Die Wachstumsrate des UMDW-Speicherplatzes ist während der ersten beiden Tage am höchsten.  
  
    -   In einem typischen Szenario beträgt der von der msdb-Datenbank auf dem UCP belegte Speicherplatz ungefähr 20 MB pro verwalteter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Diese Schätzung kann sich je nach den Richtlinien für die Ressourcennutzung und der Anzahl der Datenbank- und Systemobjekte ändern, die von der verwalteten Instanz gesammelt werden. Im Allgemeinen nimmt die Speicherplatznutzung proportional zum Anstieg der Richtlinienverstöße und zur Dauer des beweglichen Zeitfensters für veränderliche Ressourcen zu.  
  
    -   Wenn Sie eine verwaltete Instanz aus dem UCP entfernen, verringert sich der von den UCP-Datenbanken belegte Speicherplatz erst nach Ablauf der Beibehaltungsdauer für die verwaltete Instanz.  
  
 In dieser Version müssen alle verwalteten Instanzen von SQL Server die folgenden Anforderungen erfüllen:  
  
-   Wenn der UCP von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz gehostet wird, bei der keine Groß-/Kleinschreibung beachtet wird, sollte bei verwalteten Instanzen von SQL Server ebenfalls keine Groß-Kleinschreibung beachtet werden.  
  
-   FILESTREAM-Daten werden von der Überwachungsfunktion des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms nicht unterstützt.  
  
 Weitere Informationen finden Sie unter [Spezifikationen der maximalen Kapazität für SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md) und unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogrammkonzepten finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
> [!IMPORTANT]  
>  Der Sammlungssatz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms kann parallel mit Sammlungssätzen verwendet werden, die nicht zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm gehören. Eine verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann also von anderen Sammlungssätzen überwacht werden, während sie einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm zugeordnet ist. Beachten Sie jedoch, dass alle Sammlungssätze für die verwaltete Instanz ihre Daten in das UMDW (Utility Management Data Warehouse) hochladen. Weitere Informationen finden Sie unter [Überlegungen zum Ausführen von Hilfsprogramm- und Nicht-Hilfsprogramm-Sammlungssätzen auf derselben Instanz von SQL Server](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) und [Konfigurieren des Data Warehouse für den Steuerungspunkt für das Hilfsprogramm &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md).  
  
## <a name="wizard-steps"></a>Schritte des Assistenten  
 Die folgenden Abschnitte enthalten ausführliche Informationen zu jeder Seite im Assistentenworkflow. Klicken Sie auf einen Link, um zu den Details für eine Assistentenseite zu navigieren. Weitere Informationen zu einem PowerShell-Skript dieses Vorgangs finden Sie im PowerShell- [Beispiel](#PowerShell_enroll).  
  
-   [Einführung in den Instanzregistrierungs-Assistenten](#Welcome)  
  
-   [Angeben der Instanz von SQL Server](#Instance_name)  
  
-   [Verbindungsdialogfeld](#Connection_dialog)  
  
-   [Konto des Hilfsprogramm-Sammlungssatzes](#Proxy_configuration)  
  
-   [Überprüfung der SQL Server-Instanz](#Validation_rules)  
  
-   [Zusammenfassung der Instanzregistrierung](#Summary)  
  
-   [Registrieren der Instanz von SQL Server](#Enrolling)  
  
##  <a name="Welcome"></a> Einführung in den Instanzregistrierungs-Assistenten  
 Um den Assistenten zu starten, erweitern Sie auf einem Steuerungspunkt für das Hilfsprogramm (UCP, Utility Control Point) die Hilfsprogramm-Explorer-Struktur, klicken mit der rechten Maustaste auf **Verwaltete Instanzen**und wählen **Verwaltete Instanz hinzufügen...**aus.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Instance_name"></a> Angeben der Instanz von SQL Server  
 Um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Verbindungsdialogfeld auszuwählen, klicken Sie auf **Verbinden**. Stellen Sie den Computernamen und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanznamen im Format „Computername\Instanzname“ bereit. Weitere Informationen finden Sie unter [Verbindung mit Server herstellen &#40;Datenbankmodul&#41;](http://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41).  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Connection_dialog"></a> Verbindungsdialogfeld  
 Überprüfen Sie im Dialogfeld Verbindung mit Server herstellen den Servertyp, den Computernamen und die Informationen zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanznamen. Weitere Informationen finden Sie unter [Verbindung mit Server herstellen &#40;Datenbankmodul&#41;](http://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41).  
  
> [!NOTE]  
>  Wenn die Verbindung verschlüsselt ist, wird dieser Verbindungstyp verwendet. Wenn die Verbindung nicht verschlüsselt ist, stellt das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm über eine verschlüsselte Verbindung erneut eine Verbindung her.  
  
 Klicken Sie auf **Verbinden**, um den Vorgang fortzusetzen.  
  
##  <a name="Proxy_configuration"></a> Konto des Hilfsprogramm-Sammlungssatzes  
 Geben Sie ein Windows-Domänenkonto an, um den Sammlungssatz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms auszuführen. Dieses Konto wird als Proxykonto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents für den Sammlungssatz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms verwendet. Alternativ können Sie das vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto verwenden. Um die Überprüfungsanforderungen zu erfüllen, geben Sie das Konto unter Beachtung folgender Richtlinien an.  
  
 Angeben des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkontos:  
  
-   Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto muss ein Windows-Domänenkonto sein, das keinem integrierten Konto wie LocalSystem, NetworkService oder LocalService entspricht.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Validation_rules"></a> Überprüfung der SQL Server-Instanz  
 In dieser Version müssen die folgenden Bedingungen erfüllt sein, damit die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm registriert werden kann:  
  
|Bedingung|Korrekturmaßnahme|  
|---------------|-----------------------|  
|Sie müssen für die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und für den UCP über Administratorrechte verfügen.|Melden Sie sich unter einem Konto an, das für die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und für den UCP über Administratorrechte verfügt.|  
|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Edition muss die Registrierung von Instanzen unterstützen.|Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|Für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -UCP sollte TCP/IP aktiviert sein.|Aktivieren Sie TCP/IP auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -UCP.|  
|Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] darf nicht bereits bei einem anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -UCP registriert sein.|Wenn die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereits als Teil eines vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms verwaltet wird, können Sie sie nicht bei einem anderen UCP registrieren.|  
|Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] darf nicht als UCP eingerichtet sein.|Wenn die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereits ein UCP ist, aber nicht dem UCP entspricht, mit dem Sie verbunden sind, können Sie sie nicht in diesem UCP registrieren.|  
|Für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen Sammlungssätze des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms installiert sein.|Installieren Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erneut.|  
|Sammlungssätze für die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen beendet werden.|Beenden Sie bereits vorhandene Sammlungssätze für die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn der Datensammler deaktiviert ist, aktivieren Sie ihn, beenden alle aktiven Sammlungssätze und führen die Überprüfungsregeln für den Vorgang UCP erstellen erneut aus.<br /><br /> So aktivieren Sie den Datensammler<br /><br /> Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung** .<br /><br /> Klicken Sie mit der rechten Maustaste auf **Datensammlung**, und klicken Sie anschließend auf **Datensammlung aktivieren**.<br /><br /> So beenden Sie einen Sammlungssatz<br /><br /> Erweitern Sie im Objekt-Explorer nacheinander die Knoten **Verwaltung**, **Datensammlung**und dann Systemdaten-Sammlungssätze.<br /><br /> Klicken Sie mit der rechten Maustaste auf den Sammlungssatz, den Sie beenden möchten, und klicken Sie anschließend auf **Datensammlungssatz beenden**.<br /><br /> In einem Meldungsfeld wird das Ergebnis dieser Aktion angezeigt, und ein roter Kreis auf dem Symbol für den Sammlungssatz weist darauf hin, dass der Sammlungssatz beendet wurde.|  
|Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst auf der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss gestartet werden.|Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst auf der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstanz ist, konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst für den manuellen Start. Konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst andernfalls für den automatischen Start.|  
|Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst auf dem UCP muss gestartet werden.|Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst auf dem UCP. Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -UCP eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstanz ist, konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst für den manuellen Start. Konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst andernfalls für den automatischen Start.|  
|WMI muss korrekt konfiguriert sein.|Informationen zur Problembehandlung einer WMI-Konfiguration finden Sie unter [Problembehandlung beim SQL Server-Hilfsprogramm](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453).|  
|Das Proxykonto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents muss ein gültiges Windows-Domänenkonto auf dem UCP sein.|Geben Sie ein gültiges Windows-Domänenkonto an. Um sicherzustellen, dass das Konto gültig ist, melden Sie sich unter dem Windows-Domänenkonto beim UCP an.|  
|Wenn Sie die Proxykonto-Option auswählen, muss das Proxykonto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ein gültiges Windows-Domänenkonto auf der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sein.|Geben Sie ein gültiges Windows-Domänenkonto an. Um sicherzustellen, dass das Konto gültig ist, melden Sie sich unter dem Windows-Domänenkonto bei der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an.|  
|Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto kann kein integriertes Konto, z. B. Netzwerkdienst, sein.|Weisen Sie das Konto einem Windows-Domänenkonto erneut zu. Um sicherzustellen, dass das Konto gültig ist, melden Sie sich unter dem Windows-Domänenkonto bei der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an.|  
|Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto muss ein gültiges Windows-Domänenkonto auf dem UCP sein.|Geben Sie ein gültiges Windows-Domänenkonto an. Um sicherzustellen, dass das Konto gültig ist, melden Sie sich unter dem Windows-Domänenkonto beim UCP an.|  
|Wenn Sie die Dienstkonto-Option auswählen, muss das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto ein gültiges Windows-Domänenkonto auf der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sein.|Geben Sie ein gültiges Windows-Domänenkonto an. Um sicherzustellen, dass das Konto gültig ist, melden Sie sich unter dem Windows-Domänenkonto bei der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an.|  
  
 Wenn die Überprüfungsergebnisse nicht erfüllte Bedingungen enthalten, beheben Sie die blockierenden Probleme, und klicken Sie auf **Überprüfung erneut ausführen** , um die Computerkonfiguration zu überprüfen.  
  
 Um den Überprüfungsbericht zu speichern, klicken Sie auf **Bericht speichern** und geben einen Speicherort für die Datei an.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Summary"></a> Zusammenfassung der Instanzregistrierung  
 Die Zusammenfassungsseite enthält Informationen zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, die dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm hinzugefügt werden soll.  
  
 Einstellungen verwalteter Instanzen:  
  
-   Name der SQL Server-Instanz: ComputerName\InstanceName  
  
-   Konto des Hilfsprogramm-Sammlungssatzes: DomainName\UserName  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Enrolling"></a> Registrieren der Instanz von SQL Server  
 Die Registrierungsseite zeigt den Status des Vorgangs an:  
  
-   Vorbereiten der Instanz für die Registrierung  
  
-   Erstellen des Cacheverzeichnisses für die gesammelten Daten  
  
-   Konfigurieren des Hilfsprogramm-Sammlungssatzes  
  
 Um einen Bericht über den Registrierungsvorgang zu speichern, klicken Sie auf **Bericht speichern** und geben einen Speicherort für die Datei an.  
  
 Zum Abschließen des Assistenten klicken Sie auf **Fertig stellen**.  
  
> [!NOTE]  
>  Wenn Sie die SQL Server-Authentifizierung für die Verbindung mit der Instanz von SQL Server für die Registrierung verwenden, und Sie geben ein Proxykonto an, das zu einer anderen Active Directory-Domäne gehört als die Domäne, wo sich der UCP befindet, ist die Instanzüberprüfung erfolgreich, aber der Registrierungsvorgang schlägt mit der folgenden Fehlermeldung fehl:  
>   
>  Beim Ausführen einer Transact-SQL-Anweisung oder eines Batches ist eine Ausnahme aufgetreten. (Microsoft.SqlServer.ConnectionInfo)  
>   
>  Weitere Informationen: Konnte keine Informationen zu Windows NT Gruppe/Benutzer abrufen '\<DomainName\AccountName>', Fehlercode 0x5. (Microsoft SQL Server, Fehler: 15404)  
>   
>  Weitere Informationen zur Fehlerbehebung finden Sie unter [Problembehandlung beim SQL Server-Hilfsprogramm](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453).  
  
> [!IMPORTANT]  
>  Ändern Sie keine Eigenschaften des Sammlungssatzes "Hilfsprogramminformationen" in einer verwalteten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und aktivieren/deaktivieren Sie die Datensammlung nicht manuell, da die Datensammlung von einem Hilfsprogramm-Agentauftrag gesteuert wird.  
  
 Nachdem der Instanzregistrierungs-Assistent abgeschlossen wurde, klicken Sie auf den Knoten **Verwaltete Instanzen** , der sich im **Hilfsprogramm-Explorer** -Navigationsbereich in SSMS befindet. Registrierte Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden in der Listenansicht in Bereich **Inhalt des Hilfsprogramm-Explorers** angezeigt.  
  
 Der Datensammlungsprozess beginnt sofort, aber es kann bis zu 30 Minuten dauern, bis die ersten Daten im Dashboard und in den Blickpunkten des Bereichs Inhalt des Hilfsprogramm-Explorers angezeigt werden. Die Datensammlung wird alle 15 Minuten einmal ausgeführt. Um Daten zu aktualisieren, klicken Sie mit der rechten Maustaste auf den Knoten **Verwaltete Instanzen** im **Hilfsprogramm-Explorer-Navigationsbereich** und wählen dann **Aktualisieren**aus. Alternativ dazu klicken Sie mit der rechten Maustaste in der Listenansicht auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanznamen und wählen dann **Aktualisieren**aus.  
  
 Um verwaltete Instanzen aus dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm zu entfernen, wählen Sie **Verwaltete Instanzen** im **Hilfsprogramm-Explorer-Navigationsbereich** aus, um die Listenansicht verwalteter Instanzen aufzufüllen. Klicken Sie mit der rechten Maustaste in der Listenansicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inhalt des Hilfsprogramm-Explorers **auf den** -Instanznamen und wählen dann **Instanz als nicht verwaltet einrichten**aus.  
  
##  <a name="PowerShell_enroll"></a> Registrieren einer Instanz von SQL Server mit PowerShell  
 Verwenden Sie das folgende Beispiel, um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einem vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm zu registrieren:  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($SqlStoreConnection);  
> $Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\ManagedInstanceName";  
> $InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
> $ManagedInstance = $Utility.EnrollInstance($InstanceConnection, "ProxyAccount", "ProxyPassword");  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Überwachen von SQL Server-Instanzen im SQL Server-Hilfsprogramm](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Problembehandlung beim SQL Server-Hilfsprogramm](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  

