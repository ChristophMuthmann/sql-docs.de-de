---
title: "Erstellen eines Steuerungspunkts für das SQL Server-Hilfsprogramm (SQL Server-Hilfsprogramm) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.SWB.create.ucp.validation.F1
- sql13.SWB.create.ucp.Summary.F1
- sql13.SWB.create.ucp.progress.F1
- sql13.SWB.create.ucp.agentconfiguration.F1
- sql13.SWB.create.ucp.welcome.F1
- sql13.SWB.create.ucp.instancename.F1
helpviewer_keywords:
- Create UCP
- UCP
ms.assetid: d5335124-1625-47ce-b4ac-36078967158c
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eaf3148fba4a949d937b725fe4f860f1bb228674
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-sql-server-utility-control-point-sql-server-utility"></a>Erstellen eines Steuerungspunkts für das SQL Server-Hilfsprogramm (SQL Server-Hilfsprogramm)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Ein Unternehmen kann über mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramme verfügen, und jedes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm kann viele Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Datenschichtanwendungen verwalten. Jedes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verfügt über genau einen Steuerungspunkt für das Hilfsprogramm (Utility Control Point, UCP). Sie müssen einen neuen UCP für jedes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm erstellen. Jede verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und jede Datenebenenanwendung gehört mindestens einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm an und wird von einem einzelnen UCP verwaltet.  
  
 Der UCP erfasst alle 15 Minuten Konfigurations- und Leistungsinformationen von verwalteten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen. Diese Informationen werden auf dem UCP im Utility Management Data Warehouse (UMDW) gespeichert. Der UMDW-Dateiname lautet "sysutility_mdw". [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Leistungsdaten werden mit Richtlinien verglichen, sodass Sie Engpässe bei der Ressourcennutzung und Konsolidierungsmöglichkeiten leichter erkennen können.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Bevor Sie einen UCP erstellen, überprüfen Sie die folgenden Anforderungen und Empfehlungen.  
  
 In dieser Version müssen der UCP und alle verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die folgenden Anforderungen erfüllen:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss Version 10.50 oder höher entsprechen.  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanztyp muss dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]entsprechen.  
  
-   Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm muss innerhalb einer einzelnen Windows-Domäne oder über Domänen ausgeführt werden, die sich gegenseitig vertrauen.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonten auf dem UCP und alle verwalteten Instanzen von SQL Server müssen über die Leseberechtigung für Benutzer in Active Directory verfügen.  
  
 In dieser Version muss der UCP die folgenden Anforderungen erfüllen:  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz muss eine unterstützte Edition sein. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   Als Host für den UCP wird eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]empfohlen, bei der die Groß-/Kleinschreibung beachtet wird.  
  
 Berücksichtigen Sie die folgenden Empfehlungen für die Kapazitätsplanung auf dem UCP-Computer:  
  
-   In einem typischen Szenario beträgt der von der UMDW-Datenbank (sysutility_mdw) auf dem UCP belegte Speicherplatz ungefähr 2 GB pro verwalteter SQL Server-Instanz im Jahr. Diese Schätzung kann sich je nach der Anzahl der Datenbank- und Systemobjekte ändern, die von der verwalteten Instanz gesammelt werden. Die Wachstumsrate des UMDW-Speicherplatzes ist während der ersten beiden Tage am höchsten.  
  
-   In einem typischen Szenario beträgt der von der msdb-Datenbank auf dem UCP belegte Speicherplatz ungefähr 20 MB pro verwalteter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Diese Schätzung kann sich je nach den Richtlinien für die Ressourcennutzung und der Anzahl der Datenbank- und Systemobjekte ändern, die von der verwalteten Instanz gesammelt werden. Im Allgemeinen nimmt die Speicherplatznutzung proportional zum Anstieg der Richtlinienverstöße und zur Dauer des beweglichen Zeitfensters für veränderliche Ressourcen zu.  
  
-   Wenn Sie eine verwaltete Instanz aus dem UCP entfernen, verringert sich der von den UCP-Datenbanken belegte Speicherplatz erst nach Ablauf der Beibehaltungsdauer für die verwaltete Instanz.  
  
 In dieser Version müssen alle verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die folgenden Anforderungen erfüllen:  
  
-   Wenn der UCP von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz gehostet wird, bei der keine Groß-/Kleinschreibung beachtet wird, sollte bei den verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ebenfalls keine Groß-/Kleinschreibung beachtet werden.  
  
-   FILESTREAM-Daten werden von der Überwachungsfunktion des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms nicht unterstützt.  
  
 Weitere Informationen finden Sie unter [Spezifikationen der maximalen Kapazität für SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md) und unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
### <a name="remove-previous-utility-control-points-before-installing-a-new-one"></a>Entfernen Sie frühere Steuerungspunkte für das Hilfsprogramm, bevor Sie einen neuen installieren  
 Wenn Sie einen Steuerungspunkt für das Hilfsprogramm (Utility Control Point, UCP) auf einer Instanz von SQL Server installieren, die nie als UCP konfiguriert wurde, müssen Sie zuvor alle verwalteten Instanzen von SQL Server sowie den UCP entfernen. Dies kann mithilfe der gespeicherten Prozedur **sp_sysutility_ucp_remove** erfolgen.  
  
 Beachten Sie vor dem Ausführen der Prozedur folgende Voraussetzungen:  
  
-   Diese Prozedur muss auf einem Computer ausgeführt werden, der ein UCP ist.  
  
-   Die Prozedur muss von einem Benutzer mit sysadmin-Berechtigungen ausgeführt werden, die gleichen Berechtigungen, die auch zum Erstellen eines UCP erforderlich sind.  
  
-   Alle verwalteten Instanzen von SQL Server müssen von dem UCP entfernt werden. Der UCP ist eine verwaltete Instanz von SQL Server. Weitere Informationen finden Sie unter [Vorgehensweise: Entfernen einer Instanz von SQL Server aus dem SQL Server-Hilfsprogramm](http://go.microsoft.com/fwlink/?LinkId=169392).  
  
 Verwenden Sie diese Vorgehensweise, um einen SQL Server-UCP aus dem SQL Server-Hilfsprogramm zu entfernen. Wenn der Vorgang abgeschlossen ist, kann auf der SQL Server-Instanz wieder ein UCP erstellt werden.  
  
 Verwenden Sie SQL Server Management Studio, um eine Verbindung zum UCP herzustellen, und führen Sie anschließend das folgende Skript aus:  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
> [!NOTE]  
>  Wenn die Instanz von SQL Server, von der der UCP entfernt wurde, nur Datensammlungssätze enthält, die nicht von dem Hilfsprogramm stammen, wird die sysutility_mdw-Datenbank nicht von der Prozedur gelöscht. In diesem Fall muss die sysutility_mdw -Datenbank manuell gelöscht werden, bevor der UCP erneut erstellt werden kann.  
  
 Jede verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und jede Datenebenenanwendung gehört mindestens einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm an und wird von einem einzelnen UCP verwaltet. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogrammkonzepten finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Ein UCP ist der zentrale Ansatzpunkt des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms. Mithilfe des UCPs können Sie Konfigurations- und Leistungsdaten anzeigen, die von den verwalteten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenebenenanwendungen gesammelt wurden, und allgemeine Kapazitätsplanungsaktivitäten ausführen. Der UCP ist der Startpunkt zum Registrieren und Entfernen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm.  
  
 Nach der Registrierung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm können Sie die Ressourcenintegrität für verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Datenebenenanwendungen überwachen, um Konsolidierungsgelegenheiten zu identifizieren und Ressourcenengpässe zu isolieren. Weitere Informationen finden Sie unter [Überwachen von SQL Server-Instanzen im SQL Server-Hilfsprogramm](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md).  
  
> [!IMPORTANT]  
>  Der Sammlungssatz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms kann parallel mit Sammlungssätzen verwendet werden, die nicht zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm gehören. Eine verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann also von anderen Sammlungssätzen überwacht werden, während sie einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm zugeordnet ist. Beachten Sie jedoch, dass alle Sammlungssätze für die verwaltete Instanz ihre Daten in das UMDW (Utility Management Data Warehouse) von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hochladen. Weitere Informationen finden Sie unter [Überlegungen zum Ausführen von Hilfsprogramm- und Nicht-Hilfsprogramm-Sammlungssätzen auf derselben Instanz von SQL Server](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) und [Konfigurieren des Data Warehouse für den Steuerungspunkt für das Hilfsprogramm &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md).  
  
## <a name="wizard-steps"></a>Schritte des Assistenten  
 ![](../../relational-databases/manage/media/create-ucp.gif "Create_UCP")  
  
 Die folgenden Abschnitte enthalten Informationen zu den einzelnen Seiten im Assistentenworkflow, der zum Erstellen eines neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -UCPs ausgeführt wird. Öffnen Sie im Menü „Ansicht“ in SSMS den Bereich „Hilfsprogramm-Explorer“, und klicken Sie dann oben im Bereich „Hilfsprogramm-Explorer“ auf die Schaltfläche ![](../../relational-databases/manage/media/create-ucp.gif "Create_UCP") **Create UCP** (UCP erstellen), um den Assistenten zum Erstellen eines neuen UCP zu starten.  
  
 Klicken Sie auf einen Link in der unten angezeigten Liste, um zu den Details für eine Assistentenseite zu navigieren.  
  
 Weitere Informationen zu einem PowerShell-Skript dieses Vorgangs finden Sie im PowerShell- [Beispiel](#PowerShell_create_UCP).  
  
-   [Einführung in den Assistenten zum Erstellen von UCPs](#Welcome)  
  
-   [Instanz angeben](#Instance_name)  
  
-   [Verbindungsdialogfeld](#Connection_dialog)  
  
-   [Konto des Hilfsprogramm-Sammlungssatzes](#Agent_configuration)  
  
-   [Überprüfungsregeln](#Validation_rules)  
  
-   [Zusammenfassung](#Summary)  
  
-   [Erstellen eines Steuerungspunkts für das Hilfsprogramm](#Creating_UCP)  
  
##  <a name="Welcome"></a> Einführung in den Assistenten zum Erstellen von UCPs  
 Wenn Sie den Hilfsprogramm-Explorer öffnen und keinen verbundenen Steuerungspunkt für das Hilfsprogramm sehen, müssen Sie eine Verbindung mit einem Steuerungspunkt herstellen oder einen neuen erstellen.  
  
 **Mit vorhandenem UCP verbinden**: Wenn bereits ein Steuerungspunkt für das Hilfsprogramm (UCP, Utility Control Point) in der Bereitstellung vorhanden ist, können Sie eine Verbindung mit ihm herstellen, indem Sie oben im Bereich „Hilfsprogramm-Explorer“ auf die Schaltfläche ![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")**Connect to Utility** (Mit Hilfsprogramm verbinden) klicken. Um eine Verbindung mit einem vorhandenen UCP herzustellen, müssen Sie über Administrator-Anmeldeinformationen verfügen oder Mitglied der Utility Reader-Rolle sein. Beachten Sie, dass es nur einen UCP pro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm geben kann, und Sie können nur mit einem UCP von einer Instanz des SSMS verbunden werden.  
  
 **Neuen UCP erstellen**: Um einen neuen Steuerungspunkt für das Hilfsprogramm zu erstellen, klicken Sie oben im Bereich „Hilfsprogramm-Explorer“ auf die Schaltfläche ![](../../relational-databases/manage/media/create-ucp.gif "Create_UCP")**Create UCP** (UCP erstellen). Um einen neuen UCP zu erstellen, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanznamen sowie Administrator-Anmeldeinformationen im Verbindungsdialogfeld angeben. Beachten Sie, dass es nur einen UCP pro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm geben kann.  
  
##  <a name="Instance_name"></a> Instanz angeben  
 Geben Sie die folgenden Informationen zum UCP an, den Sie erstellen:  
  
-   **Instanzname** – Um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Verbindungsdialogfeld auszuwählen, klicken Sie auf **Verbinden...**. Stellen Sie den Computernamen und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanznamen im Format „Computername\Instanzname“ bereit.  
  
-   **Hilfsprogrammname** – Geben Sie einen Namen an, der zur Erkennung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms im Netzwerk verwendet wird.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Connection_dialog"></a> Verbindungsdialogfeld  
 Überprüfen Sie im Dialogfeld Verbindung mit Server herstellen den Servertyp, den Computernamen und die Informationen zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanznamen. Weitere Informationen finden Sie unter [Verbindung mit Server herstellen &#40;Datenbankmodul&#41;](http://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41).  
  
> [!NOTE]  
>  Wenn die Verbindung verschlüsselt ist, wird dieser Verbindungstyp verwendet. Wenn die Verbindung nicht verschlüsselt ist, stellt das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm über eine verschlüsselte Verbindung erneut eine Verbindung her.  
  
 Klicken Sie auf **Verbinden**, um den Vorgang fortzusetzen.  
  
##  <a name="Agent_configuration"></a> Konto des Hilfsprogramm-Sammlungssatzes  
 Geben Sie ein Windows-Domänenkonto an, um den Sammlungssatz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms auszuführen. Dieses Konto wird als Proxykonto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents für den Sammlungssatz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms verwendet. Alternativ können Sie das vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto verwenden. Um die Überprüfungsanforderungen zu erfüllen, geben Sie das Konto unter Beachtung folgender Richtlinien an.  
  
 Angeben des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkontos:  
  
-   Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto muss ein Windows-Domänenkonto sein, das keinem integrierten Konto wie LocalSystem, NetworkService oder LocalService entspricht.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Validation_rules"></a> Überprüfungsregeln  
 In dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]müssen die folgenden Bedingungen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, in der der UCP erstellt wird, erfüllt sein:  
  
|Überprüfungsregel|Korrekturmaßnahme|  
|---------------------|-----------------------|  
|Sie müssen über Administratorrechte für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verfügen, in der der Steuerungspunkt für das Hilfsprogramm (UCP, Utility Control Point) erstellt wird.|Melden Sie sich unter einem Konto an, das über Administratorrechte für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügt.|  
|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version muss Version 10.50 oder höher entsprechen.|Geben Sie eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Hosten des UCPs an.|  
|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz muss eine unterstützte Edition sein. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|Geben Sie eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Hosten des UCPs an.|  
|Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] darf keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz sein, die bei einem anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -UCP angemeldet ist.|Geben Sie eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, um den UCP zu hosten, oder deregistrieren Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vom UCP, wo sie zurzeit eine verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist.|  
|Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] darf nicht bereits als Host für einen Steuerungspunkt für das Hilfsprogramm fungieren.|Geben Sie eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Hosten des UCPs an.|  
|Die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollte aktiviertes TCP/IP haben.|Aktivieren Sie TCP/IP für die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] darf keine Datenbank namens „sysutility_mdw“ enthalten.|Bei der Erstellung des UCPs wird das Utility Management Data Warehouse (UMDW) mit dem Namen "sysutility_mdw" erstellt. Der Vorgang erfordert, dass der Name während der Ausführung der Überprüfungsregeln nicht auf dem Computer vorhanden ist. Um den Vorgang fortzusetzen, müssen Sie jede Datenbank unter dem Namen "sysutility_mdw" entfernen oder umbenennen. Weitere Informationen zu Umbenennungsvorgängen finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|Sammlungssätze für die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen beendet werden.|Beenden Sie bereits vorhandene Sammlungssätze, während der UCP für die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellt wird. Wenn der Datensammler deaktiviert ist, aktivieren Sie ihn, beenden alle aktiven Sammlungssätze und führen die Überprüfungsregeln für den Vorgang UCP erstellen erneut aus.<br /><br /> So aktivieren Sie den Datensammler<br /><br /> Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung** .<br /><br /> Klicken Sie mit der rechten Maustaste auf **Datensammlung**, und klicken Sie anschließend auf **Datensammlung aktivieren**.<br /><br /> So beenden Sie einen Sammlungssatz<br /><br /> Erweitern Sie im Objekt-Explorer nacheinander die Knoten **Verwaltung**, **Datensammlung**und dann Systemdaten-Sammlungssätze.<br /><br /> Klicken Sie mit der rechten Maustaste auf den Sammlungssatz, den Sie beenden möchten, und klicken Sie anschließend auf **Datensammlungssatz beenden**.<br /><br /> In einem Meldungsfeld wird das Ergebnis dieser Aktion angezeigt, und ein roter Kreis auf dem Symbol für den Sammlungssatz weist darauf hin, dass der Sammlungssatz beendet wurde.|  
|Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst auf der angegebenen Instanz muss gestartet werden. Wenn die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstanz ist, konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst für den manuellen Start. Andernfalls müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst für den automatischen Start konfigurieren.|Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst. Wenn die angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstanz ist, konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst für den manuellen Start. Konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst andernfalls für den automatischen Start.|  
|WMI muss korrekt konfiguriert sein.|Informationen zur Problembehandlung einer WMI-Konfiguration finden Sie unter [Problembehandlung beim SQL Server-Hilfsprogramm](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453).|  
|Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Proxykonto kann kein integriertes Konto, z. B. „Netzwerkdienst“, sein.|Wenn das Proxykonto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ein integriertes Konto, z. B. „Netzwerkdienst“ ist, weisen Sie das Konto neu einem Windows-Domänenkonto mit sysadmin-Rechten zu.|  
|Wenn Sie die Proxykonto-Option auswählen, muss das Proxykonto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ein gültiges Windows-Domänenkonto sein.|Geben Sie ein gültiges Windows-Domänenkonto an. Um sicherzustellen, dass das Konto gültig ist, melden Sie sich unter dem Windows-Domänenkonto bei der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an.|  
|Wenn Sie die Dienstkonto-Option auswählen, darf das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto kein integriertes Konto wie „Netzwerkdienst“ sein.|Wenn das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto ein integriertes Konto, z. B. „Netzwerkdienst“, ist, weisen Sie das Konto einem Windows-Domänenkonto neu zu.|  
|Wenn Sie die Dienstkonto-Option auswählen, muss das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto ein gültiges Windows-Domänenkonto sein.|Geben Sie ein gültiges Windows-Domänenkonto an. Um sicherzustellen, dass das Konto gültig ist, melden Sie sich unter dem Windows-Domänenkonto bei der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an.|  
  
 Wenn die Überprüfungsergebnisse nicht erfüllte Bedingungen enthalten, beheben Sie die blockierenden Probleme, und klicken Sie auf **Überprüfung erneut ausführen** , um die Computerkonfiguration zu überprüfen.  
  
 Um den Überprüfungsbericht zu speichern, klicken Sie auf **Bericht speichern** und geben einen Speicherort für die Datei an.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Summary"></a> Zusammenfassung  
 Auf der Zusammenfassungsseite werden die Informationen angezeigt, die Sie zum UCP angegeben haben:  
  
-   Der Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz, die den UCP hostet.  
  
-   Der Name des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms.  
  
-   Der Name des Kontos, das zum Ausführen von Datensammlungsaufträgen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms verwendet wird.  
  
 Um UCP-Konfigurationseinstellungen zu ändern, klicken Sie auf **Zurück**. Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
##  <a name="Creating_UCP"></a> Erstellen eines Steuerungspunkts für das Hilfsprogramm  
 Während der Erstellung des UCPs zeigt der Assistent die Schritte sowie Statusinformationen an:  
  
-   Vorbereiten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für die UCP-Erstellung  
  
-   Erstellen des UMDWs (Utility Management Data Warehouse)  
  
-   Initialisieren des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UMDWs. Der UMDW-Dateiname ist „sysutility_mdw“.  
  
-   Konfigurieren des UCPs  
  
-   Konfigurieren des Hilfsprogramm-Sammlungssatzes von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Um einen Bericht über die UCP-Erstellung zu speichern, klicken Sie auf **Bericht speichern** und geben einen Speicherort für die Datei an.  
  
 Zum Abschließen des Assistenten klicken Sie auf **Fertig stellen**.  
  
 Nachdem Sie den Assistenten zum Erstellen von UCPs abgeschlossen haben, wird im Navigationsbereich des Hilfsprogramm-Explorers in SSMS ein Knoten für den UCP angezeigt, der über die untergeordneten Knoten Bereitgestellte Datenebenenanwendungen, Verwaltete Instanzen und Hilfsprogrammverwaltung verfügt. Der UCP wird automatisch zu einer verwalteten Instanz.  
  
 Der Datensammlungsprozess beginnt sofort, aber es kann bis zu 30 Minuten dauern, bis die ersten Daten im Dashboard und in den Blickpunkten des Bereichs Inhalt des Hilfsprogramm-Explorers angezeigt werden. Die Datensammlung wird alle 15 Minuten einmal ausgeführt. Die Anfangsdaten stammen aus dem UCP selbst. Der UCP ist also die erste verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm.  
  
 Um das Dashboard anzuzeigen, klicken Sie auf **Ansicht** und wählen **Inhalt des Hilfsprogramm-Explorers** im SSMS-Menü aus. Um Daten zu aktualisieren, klicken Sie mit der rechten Maustaste im Bereich „Hilfsprogramm-Explorer“ auf den Hilfsprogrammnamen, und wählen Sie dann **Aktualisieren** aus.  
  
 Weitere Informationen zum Registrieren zusätzlicher Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm finden Sie unter [Registrieren einer Instanz von SQL Server &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md). Um den UCP als verwaltete Instanz aus dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm zu entfernen, wählen Sie **Verwaltete Instanzen** im Bereich **Hilfsprogramm-Explorer** aus, um die Listenansicht verwalteter Instanzen aufzufüllen, klicken Sie mit der rechten Maustaste in der Listenansicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inhalt des Hilfsprogramm-Explorers **auf den** -Instanznamen, und wählen Sie dann **Instanz als nicht verwaltet einrichten**aus.  
  
##  <a name="PowerShell_create_UCP"></a> Erstellen eines neuen Steuerungspunkts für das Hilfsprogramm mithilfe von PowerShell  
 Verwenden Sie das folgende Beispiel, um einen neuen Steuerungspunkt für das Hilfsprogramm zu erstellen:  
  
```  
> $UtilityInstance = new-object –Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::CreateUtility("Utility", $SqlStoreConnection, "ProxyAccount", "ProxyAccountPassword");  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Problembehandlung beim SQL Server-Hilfsprogramm](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
