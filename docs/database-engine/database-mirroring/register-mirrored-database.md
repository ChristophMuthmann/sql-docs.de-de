---
title: Registrieren der gespiegelten Datenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.dbmmonitor.registermirroreddb.f1
ms.assetid: 6acd02b9-2311-49b0-a5f8-3852beecb4b0
caps.latest.revision: "30"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e967a036c5dd230c2ea5c84d0a69b98b368a0ec7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="register-mirrored-database"></a>Registrieren der gespiegelten Datenbank
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Verwenden Sie dieses Dialogfeld, um eine oder mehrere gespiegelte Datenbanken auf einer bestimmten Serverinstanz zu registrieren, indem Sie die Datenbank bzw. Datenbanken dem Datenbankspiegelungs-Monitor hinzufügen. Wenn eine Datenbank hinzugefügt wurde, werden Informationen zu der Datenbank, zu ihren Partnern und zum Herstellen von Verbindungen mit den Partnern vom Datenbankspiegelungs-Monitor lokal zwischengespeichert.  
  
> [!IMPORTANT]  
>  Wenn Sie Mitglied der festen Serverrolle **sysadmin** auf der Prinzipalserverinstanz, jedoch nicht auf der Spiegelserverinstanz sind, wird Ihnen nur der Status auf der Prinzipalserverinstanz angezeigt.  
  
 **So verwenden Sie SQL Server Management Studio zum Überwachen der Datenbankspiegelung**  
  
-   [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Optionen  
 **Serverinstanz**  
 Wählen Sie eine Serverinstanz aus der Liste aus, die Serverinstanzen enthält, für die der Datenbankspiegelungs-Monitor bereits eine Verbindung gespeichert hat, oder klicken Sie auf **Verbinden**. Klicken Sie auf **Verbinden** , und stellen Sie mithilfe der neuen Anmeldeinformationen eine Verbindung her, um neue Anmeldeinformationen für eine aufgelistete Serverinstanz anzugeben.  
  
> [!NOTE]  
>  Wenn Sie Datenbanken auf mehreren Serverinstanzen registrieren möchten, klicken Sie auf **Anwenden**, nachdem Sie die gewünschten Datenbanken für eine Serverinstanz überprüft haben, und wählen Sie dann eine andere Serverinstanz aus.  
  
 **Verbinden**  
 Klicken Sie auf **Verbinden** , und stellen Sie mithilfe der neuen Anmeldeinformationen eine Verbindung her, um neue Anmeldeinformationen für die Serverinstanz anzugeben. Während der Verbindungsherstellung mit einer Serverinstanz zeigt der Datenbankspiegelungs-Monitor **Auf Daten wird gewartet**an.  
  
 **Gespiegelte Datenbanken**  
 Das Raster **Gespiegelte Datenbanken** listet die gespiegelten Datenbanken auf der Serverinstanz auf.  
  
 Das Raster enthält die folgenden Spalten:  
  
|Spaltenname|Beschreibung|  
|-----------------|-----------------|  
|**Registrieren**|Überprüfen Sie jede der Datenbanken, die Sie registrieren möchten. Wenn eine Datenbank gerade überwacht wird, ist das zugehörige Kontrollkästchen aktiviert und abgeblendet.<br /><br /> Hinweis: Schließen Sie das Dialogfeld **Gespiegelte Datenbank registrieren** , wählen Sie die Datenbank in der Navigationsstruktur aus, und wählen Sie im Menü **Aktion** den Befehl **Registrierung aufheben** aus, um die Registrierung einer Datenbank aufzuheben.|  
|**Datenbank**|Der Name einer gespiegelten Datenbank auf der ausgewählten Serverinstanz.|  
|**Aktuelle Rolle**|Die aktuelle Spiegelungsrolle der Datenbank (Prinzipal oder Spiegel) auf der ausgewählten Serverinstanz.|  
|**Partner (Verbinden als)**|Der Name des Failoverpartners für die Datenbank. Es wird entweder **Windows-Authentifizierung des Konsolenbenutzers** oder **SQL Server-Authentifizierung von '***\<Anmeldename>***'** zwischen den Klammern angezeigt. Dies sind die zurzeit verwendeten Authentifizierungsinformationen, wenn die Instanz zuvor hinzugefügt wurde, bzw. die zu verwendenden Authentifizierungsinformationen, wenn diese Instanz dem Monitor nicht hinzugefügt wurde.|  
  
 **Beim Klicken auf "OK" das Dialogfeld "Serververbindungen verwalten" anzeigen**  
 Standardmäßig verwendet der Datenbankspiegelungs-Monitor die Anmeldeinformationen der Windows-Authentifizierung für Partnerserverinstanzen, für die noch keine Anmeldeinformationen angegeben wurden. Aktivieren Sie diese Option, um nach dem Registrieren von Datenbanken die Anmeldeinformationen für eine oder mehrere Serverinstanzen zu ändern.  
  
 Wenn diese Option aktiviert ist und Sie auf **OK**klicken, wird das Dialogfeld **Serververbindungen verwalten** geöffnet. In diesem Dialogfeld können Sie eine Serverinstanz auswählen, für die Sie Anmeldeinformationen angeben möchten, die der Monitor beim Herstellen einer Verbindung mit einem bestimmten Failoverpartner verwenden soll.  
  
 Suchen Sie den betreffenden Eintrag im Raster **Serverinstanzen** , und klicken Sie in dieser Zeile auf **Bearbeiten** , um die Anmeldeinformationen für einen Partner zu bearbeiten. Dadurch wird das Dialogfeld **Verbindung mit Server herstellen** für diesen Serverinstanznamen geöffnet, in dem die Steuerelemente für die Anmeldeinformationen auf den aktuellen zwischengespeicherten Wert initialisiert sind. Ändern Sie die Anmeldeinformationen nach Bedarf, und klicken Sie auf **Verbinden**. Wenn die Anmeldeinformationen über ausreichende Privilegien verfügen, wird die **Verbindung herstellen über** -Spalte mit den neuen Anmeldeinformationen aktualisiert.  
  
 **Anwenden**  
 Klicken Sie auf diese Schaltfläche, um die ausgewählten Datenbanken zu registrieren (und die Anmeldeinformationen für die Partnerserverinstanzen zu speichern), während das Dialogfeld geöffnet bleibt.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Starten des Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
