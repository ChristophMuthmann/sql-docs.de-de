---
title: Task 'Datenbank sichern' (Wartungsplan) | Microsoft-Dokumentation
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
- sql13.swb.maint.maintplanproperties.logbackup.f1
- sql13.swb.maint.backup.f1
helpviewer_keywords:
- Back Up Database Task dialog box
ms.assetid: ed1ef012-fa14-4ba5-bafe-d1527ba065b3
caps.latest.revision: 52
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 190b77647ebce66f7cf7af006f3b817605969bae
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="options-in-the-back-up-database-task-for-maintenance-plan"></a>Optionen des Task 'Datenbank sichern' für Wartungsplan
  Mithilfe des Dialogfelds **Task 'Datenbank sichern'** können Sie dem Wartungsplan einen Sicherungstask hinzufügen. Eine Sicherung der Datenbank ist für den Fall wichtig, dass die Datenbank bei einem System- oder Hardwareausfall (oder einem Benutzerfehler) beschädigt wird. In diesem Fall muss eine Sicherungskopie wiederhergestellt werden. Dieser Task ermöglicht vollständige und differenzielle Sicherungen sowie Sicherungen von Dateien, Dateigruppen und Transaktionsprotokollen.  
  
 **So erstellen Sie einen Datenbanksicherungstask**  
  
-   [Erstellen eines Wartungsplans](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
## <a name="options"></a>Optionen  
 **Verbindung**  
 Wählen Sie die Serververbindung aus, die bei der Ausführung dieses Tasks verwendet werden soll.  
  
 **Neu**  
 Erstellen Sie eine neue Serververbindung, die bei der Ausführung dieses Tasks verwendet werden soll. Das Dialogfeld **Neue Verbindung** wird im Folgenden beschrieben.  
  
 **Datenbanken**  
 Gibt die Datenbanken an, die von dieser Aufgabe betroffen sind. Bei Auswahl dieser Option werden in der Dropdownliste die folgenden Optionen angezeigt: **Alle Datenbanken**, **Alle Systemdatenbanken**, **Alle Benutzerdatenbanken**, **Diese Datenbanken**.  
  
 **Alle Datenbanken**  
 Generiert einen Wartungsplan, der Wartungstasks für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken ausführt.  
  
 **Alle Systemdatenbanken ('master', 'msdb', 'model')**  
 Generiert einen Wartungsplan, der Wartungstasks für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemdatenbanken ausführt. Für benutzerdefinierte Datenbanken werden keine Wartungstasks ausgeführt.  
  
 **Alle Benutzerdatenbanken (außer 'master', 'model', 'msdb', 'tempdb')**  
 Generiert einen Wartungsplan, der Wartungstasks für alle benutzerdefinierten Datenbanken ausführt. Für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemdatenbanken werden keine Wartungstasks ausgeführt.  
  
 **Diese Datenbanken**  
 Generiert einen Wartungsplan, der Wartungstasks nur für die ausgewählten Datenbanken ausführt. Wenn diese Option ausgewählt wird, muss mindestens eine Datenbank in der Liste ausgewählt werden.  
  
 **Sicherungstyp**  
 Zeigt den Typ der Sicherung an, die ausgeführt werden soll.  
  
 **Sicherungskomponente**  
 Wählen Sie **Datenbank** aus, um die gesamte Datenbank zu sichern. Wählen Sie **Datei und Dateigruppen** aus, um nur einen Teil der Datenbank zu sichern. Bei Auswahl dieser Option müssen Sie die Datei bzw. Dateigruppe angeben. Wenn im Feld **Datenbanken** mehrere Datenbanken ausgewählt wurden, geben Sie für die **Sicherungskomponenten** nur **Datenbanken**an. Erstellen Sie einen Task für jede Datenbank, um Datei- oder Dateigruppensicherungen auszuführen.  
  
 **Sicherungssatz läuft ab**  
 Geben Sie an, wann der Sicherungssatz durch einen anderen Sicherungssatz überschrieben werden kann.  
  
 **Sichern auf**  
 Sichert die Datenbank in einer Datei oder auf einem Band. Es stehen nur Bandmedien zur Verfügung, die an den Computer mit der Datenbank angeschlossen sind.  
  
 **Datenbanken in einer oder in mehreren Dateien sichern**  
 Klicken Sie auf **Hinzufügen** , um das Dialogfeld **Sicherungsziel auswählen** zu öffnen, und geben Sie einen oder mehrere Datenträgerspeicherorte oder Bandgeräte an.  
  
 **Wenn Sicherungsdateien vorhanden sind**  
 Wählen Sie **Anfügen** , um diese Sicherung an das Ende der Datei anzufügen. Wählen Sie **Überschreiben**aus, um alle alten Sicherungen in der Datei zu entfernen und sie mit der neuen Sicherung zu ersetzen.  
  
 **Für jede Datenbank eine Sicherungsdatei erstellen**  
 Erstellt eine Sicherungsdatei an dem im Feld für den Ordner angegebenen Speicherort. Für jede ausgewählte Datenbank wird eine Datei erstellt.  
  
 **Unterverzeichnis für jede Datenbank erstellen**  
 Wählen Sie diese Option aus, um alle Datenbanksicherungsdateien in einem Unterordner zu speichern.  
  
> [!IMPORTANT]  
>  Obwohl Unterverzeichnisse von Wartungsplänen erstellt werden können, können Unterverzeichnisse in Wartungstasks nicht gelöscht werden. Diese Funktion reduziert die Möglichkeit eines bösartigen Angriffs, der den Task Wartungscleanup zum Löschen von Dateien verwendet.  
  
> [!IMPORTANT]  
>  Das Unterverzeichnis erbt Berechtigungen vom übergeordneten Verzeichnis. Schränken Sie die Berechtigungen ein, um einen nicht autorisierten Zugriff zu verhindern.  
  
 **Ordner**  
 Gibt den Ordner an, in dem die automatisch erstellten Datenbankdateien gespeichert werden sollen.  
  
 **Sicherungsdateierweiterung**  
 Gibt die Dateierweiterung an, die für Sicherungsdateien verwendet wird. Der Standardwert ist **.bak**.  
  
 **Sicherungsintegrität überprüfen**  
 Überprüft, ob der Sicherungssatz vollständig ist und alle Volumes lesbar sind.  
  
 **Protokollfragment sichern und Datenbank im Wiederherstellungsstatus belassen**  
 Führen Sie eine Protokollsicherung als letzten Schritt vor dem Wiederherstellen einer Datenbank aus. Weitere Informationen finden Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 **Sicherungskomprimierung festlegen**  
 Wählen Sie in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (oder höher) einen der folgenden Werte für die [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md) aus:  
  
|||  
|-|-|  
|**Standardservereinstellungen verwenden**|Klicken Sie hier, um die Standardeinstellung auf Serverebene zu verwenden.<br /><br /> Diese Standardeinstellung wird durch die Serverkonfigurationsoption **backup compression default** festgelegt. Informationen zum Anzeigen der aktuellen Einstellung dieser Option finden Sie unter [Anzeigen oder Konfigurieren der Serverkonfigurationsoption „Standardeinstellung für die Sicherungskomprimierung“](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Sicherung komprimieren**|Klicken Sie hier, um die Sicherung unabhängig von der Standardeinstellung auf Serverebene zu komprimieren.<br /><br /> **\*\* Wichtig \*\*** : Standardmäßig steigt die CPU-Nutzung durch die Komprimierung erheblich, und die bei der Komprimierung zusätzlich verbrauchten CPU-Ressourcen können sich negativ auf gleichzeitige Vorgänge auswirken. Daher ist es u.U. sinnvoll, in einer Sitzung, bei der die CPU-Nutzung durch den [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen. Weitere Informationen finden Sie unter [Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen.|  
|**Sicherung nicht komprimieren**|Klicken Sie hier, um unabhängig von der Standardeinstellung auf Serverebene eine nicht komprimierte Sicherung zu erstellen.|  
  
 **T-SQL anzeigen**  
 Zeigt die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen an, die für diesen Task auf dem Server auf Basis der ausgewählten Optionen ausgeführt werden.  
  
> [!NOTE]  
>  Wenn die Anzahl der betroffenen Objekte groß ist, kann die Anzeige erhebliche Zeit in Anspruch nehmen.  
  
## <a name="new-connection-dialog-box"></a>Neue Verbindung (Dialogfeld)  
 **Verbindungsname**  
 Geben Sie einen Namen für die neue Verbindung ein.  
  
 **Wählen Sie einen Servernamen aus, oder geben Sie ihn ein.**  
 Wählen Sie den Server aus, zu dem bei der Ausführung dieses Tasks eine Verbindung hergestellt werden soll.  
  
 **Aktualisieren**  
 Mithilfe dieser Option aktualisieren Sie die Liste der verfügbaren Server.  
  
 **Geben Sie Informationen zum Anmelden am Server ein**  
 Legt fest, wie die Authentifizierung gegenüber dem Server stattfindet.  
  
 **Integrierte Sicherheit von Windows NT verwenden**  
 Stellt mithilfe der Windows-Authentifizierung eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz her.  
  
 **Bestimmten Benutzernamen und bestimmtes Kennwort verwenden**  
 Stellt mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz her. Diese Option ist nicht verfügbar.  
  
 **Benutzername**  
 Stellt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung für den Gebrauch bei der Authentifizierung bereit. Diese Option ist nicht verfügbar.  
  
 **Kennwort**  
 Stellt ein Kennwort für den Gebrauch bei der Authentifizierung bereit. Diese Option ist nicht verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
  
