---
title: Automatisierte Verwaltung in einem Unternehmen | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- enterprise automatic administration [SQL Server]
- multiserver administration [SQL Server]
- SQL Server Agent jobs, multiserver administration
- jobs [SQL Server Agent], multiserver administration
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- master servers [SQL Server]
- multiple instances of SQL Server
- target servers [SQL Server]
ms.assetid: 44d8365b-42bd-4955-b5b2-74a8a9f4a75f
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77867115cb6d169bf7a3c84c8737d54f9657651f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="automated-administration-across-an-enterprise"></a>Automatisierte Verwaltung in einem Unternehmen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das Automatisieren der Verwaltung über mehrere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] hinweg wird *Multiserververwaltung* genannt. Verwenden Sie die Multiserveradministration für folgende Aufgaben:  
  
-   Verwalten von zwei oder mehr Servern.  
  
-   Erstellen von Zeitplänen für den Informationsfluss zwischen Unternehmensservern für Dataware Housing.  
  
Für die Multiserveradministration benötigen Sie mindestens einen Masterserver und mindestens einen Zielserver. Ein Masterserver verteilt Aufträge an die Zielserver und empfängt Ereignisse von ihnen. Auf dem Masterserver ist zudem die zentrale Kopie der Auftragsdefinitionen für Aufträge gespeichert, die auf Zielservern ausgeführt werden. Zielserver stellen in regelmäßigen Abständen Verbindungen mit dem Masterserver her, um den Zeitplan der Aufträge zu aktualisieren. Ist ein neuer Auftrag auf dem Masterserver vorhanden, lädt der Zielserver den Auftrag herunter. Nach dem Beenden des Auftrags stellt der Zielserver erneut eine Verbindung mit dem Masterserver her und berichtet den Status des Auftrags. Beachten Sie, dass Sie dieselbe Auftragsdefinition verwenden müssen, wenn Sie datenbankbezogene Aktivitäten ausführen.  
  
Die folgende Abbildung stellt die Beziehung zwischen Master- und Zielserver dar:  
  
![Multiserver-Verwaltungskonfiguration](../../ssms/agent/media/multisvr.gif "Multiserver administration configuration")  
  
Wenn Sie Abteilungsserver in einem großen Unternehmen verwalten, können Sie Folgendes definieren:  
  
-   Einen Sicherungsauftrag mit Auftragsschritten.  
  
-   Operatoren, die bei einem Sicherungsfehler zu benachrichtigen sind.  
  
-   Einen Ausführungszeitplan für den Sicherungsauftrag.  
  
Richten Sie diesen Sicherungsauftrag einmal auf dem Masterserver ein, und tragen Sie anschließend alle Abteilungsserver als Zielserver ein. Ab dem Zeitpunkt der Eintragung können alle Abteilungsserver denselben Sicherungsauftrag ausführen, obwohl Sie ihn nur ein einziges Mal definiert haben.  
  
> [!NOTE]  
> Die Funktionen der Multiserveradministration sind für Mitglieder der sysadmin-Serverrolle bestimmt. Ein Mitglied der sysadmin-Rolle auf dem Zielserver kann jedoch die Vorgänge nicht bearbeiten, die auf dem Zielserver vom Masterserver ausgeführt werden. Durch diese Sicherheitsmaßnahme soll das versehentliche Löschen von Auftragsschritten und die Unterbrechung von Operationen auf dem Zielserver verhindert werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
[Erstellen einer Multiserverumgebung](../../ssms/agent/create-a-multiserver-environment.md)  
Enthält Informationen zum Erstellen und Verwalten von Master- und Zielservern.  
  
[Auswählen des richtigen SQL Server-Agent-Dienstkontos für Multiserverumgebungen](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
Enthält Informationen dazu, wie sich die Verwendung von Windows-Konten ohne Administratorberechtigungen oder des Kontos LocalSystem für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst auf Multiserverumgebungen auswirken kann.  
  
[Festlegen von Verschlüsselungsoptionen auf Zielservern](../../ssms/agent/set-encryption-options-on-target-servers.md)  
Enthält Informationen zum Festlegen des[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Registrierungsunterschlüssels „MsxEncryptChannelOptions“ auf Zielservern.  
  
[Verwalten von Aufträgen über ein gesamtes Unternehmen](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
Enthält Informationen zum Überprüfen des Auftragsstatus, Ändern der Zielserver für Aufträge, Synchronisieren von Zielserveruhren, Abrufen des aktuellen Auftragsstatus von Masterservern.  
  
[Problembehandlung von proxybasierten Multiserveraufträgen](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
Enthält Informationen zur Problembehandlung von Multiserveraufträgen, die Proxys verwenden, bei denen ein Fehler auftritt.  
  
[Abfragen von Servern](../../ssms/agent/poll-servers.md)  
Enthält Informationen zum impliziten und expliziten Abfragen des Masterservers durch Zielserver zum Synchronisieren von Auftragsinformationen.  
  
[Verwalten von Ereignissen](../../ssms/agent/manage-events.md)  
Enthält Informationen zur Weiterleitung von Ereignissen von den Zielservern auf die Masterserver.  
  
[Optimieren der automatischen Verwaltung in einem Unternehmen](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
Enthält Informationen dazu, wie die automatisierte Verwaltung in einer Multiserverumgebung die Selbstoptimierungsfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]nutzt.  
  
## <a name="see-also"></a>Siehe auch  
[Themen zur Abwärtskompatibilität zum Installieren des SQL Server-Datenbankmoduls](http://msdn.microsoft.com/en-us/10de5ec6-d3cf-42ef-aa62-1bdf3fbde841)  
[Registrieren von Servern](http://msdn.microsoft.com/en-us/c2a2513e-fa09-419c-99e7-a12d57c5a0db)  
[sp_add_targetservergroup](http://msdn.microsoft.com/en-us/acb69343-d766-46ff-b771-0c7655c5231a)  
[sp_delete_targetserver](http://msdn.microsoft.com/en-us/cc438701-ad91-419d-9f23-ebc4c548c700)  
[sp_delete_targetservergroup](http://msdn.microsoft.com/en-us/d8dd838e-64aa-419f-9ccb-ff04908cf3e4)  
[sp_help_downloadlist](http://msdn.microsoft.com/en-us/745b265b-86e8-4399-b928-c6969ca1a2c8)  
[sp_help_jobserver](http://msdn.microsoft.com/en-us/57971787-f9f5-4199-9f64-c2b61a308906)  
[sp_help_targetservergroup](http://msdn.microsoft.com/en-us/ec3a4a68-b591-431c-9518-053ede522d0c)  
[sp_resync_targetserver](http://msdn.microsoft.com/en-us/40e44df7-d3e3-44ee-b149-08aba629a21f)  
[sp_update_targetservergroup](http://msdn.microsoft.com/en-us/4ac65ed6-e07e-40e4-a282-13bfd92dfa41)  
[sysjobservers](http://msdn.microsoft.com/en-us/9abcc20f-a421-4591-affb-62674d04575e)  
[syslogins](http://msdn.microsoft.com/en-us/4cb34f17-a4bb-469f-a218-71f074e6308f)  
[systargetservers](http://msdn.microsoft.com/en-us/479d1314-be37-4d19-ac9c-419fc9110e53)  
  
