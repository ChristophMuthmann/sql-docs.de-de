---
title: Konfigurieren der sofortigen Dateiinitialisierung - Analyseplattformsystem | Microsoft Docs
description: Konfigurieren Sie sofortige Dateiinitialisierung für Analytics Platform System. Sofortige dateiinitialisierung ist eine SQL Server-Funktion, die Datei Datenvorgänge schneller ausführen kann.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 20498cc4e2c4ad959fce263984b58e3186630cea
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="instant-file-initialization-configuration"></a>Sofortige Initialisierung Dateikonfiguration
Sofortige dateiinitialisierung ist eine SQL Server-Funktion, die Datei Datenvorgänge schneller ausführen kann. Überprüfen das Kontrollkästchen, um die sofortige Dateiinitialisierung einschalten verbessert die Leistung von SQL Server PDW. Jedoch wenn dadurch ein Sicherheitsrisiko Business für Sie darstellt, dann lassen Sie das Kontrollkästchen deaktiviert.  
  
> [!IMPORTANT]  
> Wenn die sofortige dateiinitialisierung aktiviert ist, werden SQL Server keine gelöschten Bits mit Nullen überschrieben.  Dieses Verhalten kann ein Sicherheitsrisiko erstellen, wenn nicht autorisierte Benutzer Zugriff auf den gelöschten Daten erhalten. SQL Server PDW verringert jedoch dieses Risiko, indem Sie sicherstellen, dass die SQL Server-Datenbank und die Sicherungsdateien immer mit einer Instanz von SQL Server angefügt werden; nur das SQL Server-Dienstkonto und den lokalen Administrator können die gelöschten Daten in SQL Server PDW zugreifen.  
  
Die sofortige Dateiinitialisierung ist nicht verfügbar, wenn TDE aktiviert ist.  
  
## <a name="add-permission-for-the-backup-account"></a>Berechtigung für das Backup-Konto hinzufügen  
Im Rahmen des Sicherungsvorgangs erfordert eine Netzwerkanmeldeinformationen (Windows-Benutzerkonto), der im Sicherungsspeicherort zugreifen kann. Autorisieren Sie PDW Konto mithilfe der [Sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) Prozedur. Finden Sie unter [SICHERUNGSDATENBANK](../t-sql/statements/backup-database-parallel-data-warehouse.md) für den gesamten Sicherungsvorgang. Um die sofortige dateiinitialisierung zu verwenden, müssen Sie die sicherungskonto gewährt der `Perform volume maintenance tasks` Berechtigung.  
  
1.  Öffnen Sie auf dem backup-Server die **lokale Sicherheitsrichtlinie** Anwendung (`secpol.msc`).  
  
2.  Erweitern Sie im linken Bereich **Lokale Richtlinien**, und klicken Sie dann auf **Zuweisen von Benutzerrechten**.  
  
3.  Doppelklicken Sie im rechten Bereich auf **Durchführen von Volumewartungsaufgaben**.  
  
4.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und fügen Sie alle Benutzerkonten hinzu, die für Sicherungen verwendet werden.  
  
5.  Klicken Sie auf **Übernehmen**, und schließen Sie dann alle Dialogfelder von **Lokale Sicherheitsrichtlinie** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Zum Aktivieren oder deaktivieren Sie die sofortige Dateiinitialisierung  
  
1.  Starten Sie den Konfigurations-Manager. Weitere Informationen finden Sie unter [Starten des Konfigurations-Managers &#40;Analyseplattformsystem&#41;](launch-the-configuration-manager.md).  
  
2.  Klicken Sie im linken Bereich des Konfigurations-Managers auf **Dateiinitialisierung**.  
  
3.  Um die sofortige dateiinitialisierung zu aktivieren, wählen Sie das Kontrollkästchen neben **Dateiinitialisierung aktiviert, auf allen Knoten**. Um die sofortige dateiinitialisierung zu deaktivieren, deaktivieren Sie das Kontrollkästchen neben **Dateiinitialisierung aktiviert, auf allen Knoten**.  
  
    > [!WARNING]  
    > Wenn Sie schnelle dateiinitialisierung deaktivieren, gelten die oben beschriebenen für das Feature Sicherheitsaspekt möglicherweise weiterhin für Dateien gelöscht werden, während die sofortige dateiinitialisierung aktiviert wurde.  
  
4.  Klicken Sie auf **Anwenden**. Die Änderung wird das nächste Mal über die SQL Server-Instanzen für SQL Server PDW weitergegeben, das die Appliance-Dienste neu gestartet werden. Um die Anwendung Dienste neu zu starten, finden Sie unter [PDW-Dienststatus &#40;Analyseplattformsystem&#41;](pdw-services-status.md).  
  
5.  Möglicherweise möchten Sie die oben erläuterten Schritte wiederholen **Berechtigung hinzufügen, für das Konto für die Sicherung** So entfernen Sie die **Durchführen von Volumewartungsaufgaben** Berechtigung.  
  
![DWConfig-Anwendung PDW Instant Dateiinitialisierung](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Weitere Informationen zur sofortigen dateiinitialisierung finden Sie unter [Dateiinitialisierung](http://technet.microsoft.com/en-us/library/ms175935(v=SQL.105).aspx).  
  
