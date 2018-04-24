---
title: Sofortige Datenbankdateiinitialisierung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: b558a09e99dfb8c92778fa4cf2b5e1333bd49d33
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="database-file-initialization"></a>Datenbankdatei-Initialisierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Daten- und Protokolldateien werden initialisiert, um vorhandene Daten zu überschreiben, die von zuvor gelöschten Dateien auf dem Datenträger zurückgelassen wurden. Daten- und Protokolldateien werden erstmals durch Ausfüllen der Dateien mit Nullen initialisiert, wenn Sie einen der folgenden Vorgänge durchführen:  
  
- Erstellen einer Datenbank  
- Fügen Sie Dateien oder Protokolldateien zu einer vorhandenen Datenbank hinzu.  
- Vergrößern einer vorhanden Datei (einschließlich Vorgängen zur automatischen Vergrößerung).  
- Wiederherstellen einer Datenbank oder Dateigruppe  
  
Die Dateiinitialisierung führt dazu, dass diese Vorgänge mehr Zeit benötigen. Aber wenn die Daten zum ersten Mal an die Dateien geschrieben werden, muss das Betriebssystem die Dateien nicht mit Nullen ausfüllen.  
  
## <a name="instant-file-initialization-ifi"></a>Schnelle Dateiinitialisierung (IFI)  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Datendateien sofort initialisiert werden, um Löschvorgänge zu vermeiden. Mit der sofortigen Dateiinitialisierung ist eine schnelle Ausführung der zuvor erwähnten Dateivorgänge möglich. Bei der sofortigen Dateiinitialisierung wird belegter Speicherplatz freigegeben, ohne diesen Speicherplatz mit Nullen auszufüllen. Stattdessen wird Datenträgerinhalt überschrieben, wenn neue Daten an die Dateien geschrieben werden. Protokolldateien können nicht sofort initialisiert werden.  
  
> [!NOTE]  
> Die sofortige Dateiinitialisierung ist nur in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] oder [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] oder höheren Versionen verfügbar.  

> [!IMPORTANT]
> Die schnelle Dateiinitialisierung (Instant File Initialization, IFI) ist nur für Datendateien verfügbar. Protokolldateien werden immer auf Null gesetzt, wenn diese erstellt oder die Dateien größer werden.
  
Die schnelle Dateiinitialisierung ist nur verfügbar, wenn dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienststartkonto *SE_MANAGE_VOLUME_NAME* erteilt wurde. Mitglieder der Windows-Administratorengruppe verfügen über dieses Recht und können es anderen Benutzern erteilen, indem sie diese der Sicherheitsrichtlinie **Durchführen von Volumewartungsaufgaben** hinzufügen.  
  
> [!IMPORTANT]
> Die Verwendung bestimmter Features wie [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) kann die schnelle Dateiinitialisierung blockieren.  
  
So erteilen Sie einem Konto die Berechtigung `Perform volume maintenance tasks` :  
  
1.  Öffnen Sie auf dem Computer, auf die Sicherungsdatei erstellt wird, die Anwendung für **lokale Sicherheitsrichtlinien** (`secpol.msc`).  
  
2.  Erweitern Sie im linken Bereich **Lokale Richtlinien**, und klicken Sie dann auf **Zuweisen von Benutzerrechten**.  
  
3.  Doppelklicken Sie im rechten Bereich auf **Durchführen von Volumewartungsaufgaben**.  
  
4.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und fügen Sie alle Benutzerkonten hinzu, die für Sicherungen verwendet werden.  
  
5.  Klicken Sie auf **Übernehmen**, und schließen Sie dann alle Dialogfelder von **Lokale Sicherheitsrichtlinie** .  

> [!NOTE]
> Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] kann diese Berechtigung dem Dienstkonto beim Setup im Rahmen einer Installation erteilt werden. Wenn Sie eine [Installation über die Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md) durchführen, fügen Sie das Argument /SQLSVCINSTANTFILEINIT hinzu oder aktivieren im [Installationsassistenten](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) das Kontrollkästchen *SQL Server-Datenbank-Engine-Dienst Berechtigung zum Ausführen von Volumewartungstasks gewähren*.

> [!NOTE]
> Für die Versionen von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 über [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 bis hin zu [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] kann in der DMV [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) die Spalte *instant_file_initialization_enabled* verwendet werden, um festzustellen, ob die schnelle Dateiinitialisierung aktiviert ist.

## <a name="remarks"></a>Remarks
Wenn *SE_MANAGE_VOLUME_NAME* für das Dienststartkonto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erteilt wurde, wird eine Meldung ähnlich wie die folgende beim Start im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll protokolliert: 

```
Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

Wenn **nicht** *SE_MANAGE_VOLUME_NAME* für das Dienststartkonto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erteilt wurde, wird eine Meldung ähnlich wie die folgende beim Start im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll protokolliert: 

```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (für Versionen von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 über [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis hin zu [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

## <a name="security-considerations"></a>Überlegungen zur Sicherheit  
Da bei Verwendung der schnellen Dateiinitialisierung (Instant File Initialization, IFI) der gelöschte Datenträgerinhalt nur überschrieben wird, wenn neue Daten in die Dateien geschrieben werden, kann ein nicht autorisierter Prinzipal möglicherweise so lange auf den gelöschten Inhalt zugreifen, bis andere Daten in diesen Bereich der Datendatei geschrieben werden. Während die Datenbankdatei an die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angefügt ist, wird diese Gefahr einer Offenlegung von Informationen durch die besitzerverwaltete Zugriffssteuerungsliste (Discretionary Access Control List, DACL) in der Datei verringert. Diese DACL gewährt den Dateizugriff nur für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto und den lokalen Administrator. Wenn die Datei jedoch getrennt wird, kann möglicherweise ein Benutzer oder Dienst darauf zugreifen, der nicht über *SE_MANAGE_VOLUME_NAME* verfügt. Eine ähnliche Betrachtung ergibt sich bei der Sicherung der Datenbank: Der gelöschte Inhalt kann für einen nicht autorisierten Benutzer oder Dienst verfügbar werden, wenn die Sicherungsdatei nicht mit einer entsprechenden DACL geschützt wird.  

Außerdem kann es sein, dass ein SQL Server-Administrator Zugriff auf die grundlegenden Inhalte der Seite und bereits gelöschte Inhalte erhält, wenn eine Datei über die schnelle Dateiinitialisierung erstellt wird.

Wenn die Datenbankdateien auf einem Storage Area Network gehostet werden, kann es außerdem sein, dass das Storage Area Network neue Seiten immer als vorinitialisiert anzeigt und die Vorinitialisierung der Seiten durch das Betriebssystem würde einen unnötigen zeitlichen Mehraufwand bedeuten.
 
> [!NOTE]
> Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einer sicheren physischen Umgebung installiert wird, können die aus der Aktivierung der schnellen Dateiinitialisierung resultierenden Leistungsvorteile das Sicherheitsrisiko überwiegen. Aus diesem Grund werden folgende Empfehlungen gegeben.
  
Wenn Sie sich Gedanken über eine potenzielle Offenlegung von Informationen machen, sollten Sie eine oder beide der folgenden Maßnahmen treffen:  
  
- Stellen Sie immer sicher, dass alle angebundenen Daten- und Sicherungsdateien über restriktive DACLs verfügen.  
- Deaktivieren Sie die schnelle Dateiinitialisierung für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], indem Sie *SE_MANAGE_VOLUME_NAME* im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienststartkonto widerrufen. 

> [!IMPORTANT]
> Durch die Deaktivierung der schnellen Dateiinitialisierung verlängert sich die Belegungszeit für Datendateien.  
  
> [!NOTE]  
> Das Deaktivieren der sofortigen Dateiinitialisierung wirkt sich nur auf Dateien aus, die nach dem Widerrufen des Benutzerrechts erstellt oder vergrößert werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
