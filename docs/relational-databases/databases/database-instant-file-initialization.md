---
title: Sofortige Datenbankdateiinitialisierung | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization (SQL Server)
- file initialization [SQL Server]
- IFI [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3f0ef2d2c733a0ab1f349d42d621303cc6c133a5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="database-file-initialization"></a>Datenbankdatei-Initialisierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Daten- und Protokolldateien werden initialisiert, um vorhandene Daten zu überschreiben, die von zuvor gelöschten Dateien auf dem Datenträger zurückgelassen wurden. Daten- und Protokolldateien werden erstmals durch Ausfüllen der Dateien mit Nullen initialisiert, wenn Sie einen der folgenden Vorgänge durchführen:  
  
- Erstellen einer Datenbank  
  
- Fügen Sie Dateien oder Protokolldateien zu einer vorhandenen Datenbank hinzu.  
  
- Vergrößern einer vorhanden Datei (einschließlich Vorgängen zur automatischen Vergrößerung).  
  
- Wiederherstellen einer Datenbank oder Dateigruppe  
  
Die Dateiinitialisierung führt dazu, dass diese Vorgänge mehr Zeit benötigen. Aber wenn die Daten zum ersten Mal an die Dateien geschrieben werden, muss das Betriebssystem die Dateien nicht mit Nullen ausfüllen.  
  
# <a name="instant-file-initialization-ifi"></a>Schnelle Dateiinitialisierung (IFI)  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Datendateien sofort initialisiert werden, um Löschvorgänge zu vermeiden. Mit der sofortigen Dateiinitialisierung ist eine schnelle Ausführung der zuvor erwähnten Dateivorgänge möglich. Bei der sofortigen Dateiinitialisierung wird belegter Speicherplatz freigegeben, ohne diesen Speicherplatz mit Nullen auszufüllen. Stattdessen wird Datenträgerinhalt überschrieben, wenn neue Daten an die Dateien geschrieben werden. Protokolldateien können nicht sofort initialisiert werden.  
  
> [!NOTE]  
>  Die sofortige Dateiinitialisierung ist nur in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] oder [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] oder höheren Versionen verfügbar.  

> [!IMPORTANT]
> Die schnelle Dateiinitialisierung (Instant File Initialization, IFI) ist nur für Datendateien verfügbar. Protokolldateien werden immer auf Null gesetzt, wenn diese erstellt oder die Dateien größer werden.
  
Die schnelle Dateiinitialisierung ist nur verfügbar, wenn dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienststartkonto *SE_MANAGE_VOLUME_NAME* erteilt wurde. Mitglieder der Windows-Administratorengruppe verfügen über dieses Recht und können es anderen Benutzern erteilen, indem sie diese der Sicherheitsrichtlinie **Durchführen von Volumewartungsaufgaben** hinzufügen.  
  
Die Verwendung bestimmter Features wie [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) kann die schnelle Dateiinitialisierung blockieren.  
  
So erteilen Sie einem Konto die Berechtigung `Perform volume maintenance tasks` :  
  
1.  Öffnen Sie auf dem Computer, auf die Sicherungsdatei erstellt wird, die Anwendung für **lokale Sicherheitsrichtlinien** (`secpol.msc`).  
  
2.  Erweitern Sie im linken Bereich **Lokale Richtlinien**, und klicken Sie dann auf **Zuweisen von Benutzerrechten**.  
  
3.  Doppelklicken Sie im rechten Bereich auf **Durchführen von Volumewartungsaufgaben**.  
  
4.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und fügen Sie alle Benutzerkonten hinzu, die für Sicherungen verwendet werden.  
  
5.  Klicken Sie auf **Übernehmen**, und schließen Sie dann alle Dialogfelder von **Lokale Sicherheitsrichtlinie** .  
  
### <a name="security-considerations"></a>Sicherheitsüberlegungen  
 Da der gelöschte Datenträgerinhalt nur überschrieben wird, wenn neue Daten in die Dateien geschrieben werden, kann ein nicht autorisierter Prinzipal möglicherweise so lange auf den gelöschten Inhalt zugreifen, bis andere Daten in diesen Bereich der Datendatei geschrieben werden. Während die Datenbankdatei an die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angefügt ist, wird diese Gefahr einer Offenlegung von Informationen durch die besitzerverwaltete Zugriffssteuerungsliste (Discretionary Access Control List, DACL) in der Datei verringert. Diese DACL gewährt den Dateizugriff nur für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto und den lokalen Administrator. Wenn die Datei jedoch getrennt wird, kann möglicherweise ein Benutzer oder Dienst darauf zugreifen, der nicht über *SE_MANAGE_VOLUME_NAME* verfügt. Eine ähnliche Betrachtung ergibt sich bei der Sicherung der Datenbank: Der gelöschte Inhalt kann für einen nicht autorisierten Benutzer oder Dienst verfügbar werden, wenn die Sicherungsdatei nicht mit einer entsprechenden DACL geschützt wird.  
 
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einer sicheren Umgebung installiert wird, können die aus der Aktivierung von IFI resultierenden Leistungsvorteile das Sicherheitsrisiko überwiegen. Aus diesem Grund werden folgende Empfehlungen gegeben.
  
 Wenn Sie sich Gedanken über eine potenzielle Offenlegung von Informationen machen, sollten Sie eine oder beide der folgenden Maßnahmen treffen:  
  
- Stellen Sie immer sicher, dass alle angebundenen Daten- und Sicherungsdateien über restriktive DACLs verfügen.  
  
- Deaktivieren Sie die schnelle Dateiinitialisierung für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], indem Sie *SE_MANAGE_VOLUME_NAME* im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienststartkonto widerrufen.  
  
> [!NOTE]  
> Das Deaktivieren der sofortigen Dateiinitialisierung wirkt sich nur auf Dateien aus, die nach dem Widerrufen des Benutzerrechts erstellt oder vergrößert werden.  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
