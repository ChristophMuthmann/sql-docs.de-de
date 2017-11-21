---
title: "Hinzufügen von Funktionen zu einer Instanz von SQL Server (Setup) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/07/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- feature adding [SQL Server]
- SQL Server, features
- adding features to SQL Server
ms.assetid: 97931fdc-d943-48dd-81b9-ae8b8d2c6dad
caps.latest.revision: "29"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: eb201c27f255ac57c667c3a727c2b4c1551f37fe
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="add-features-to-an-instance-of-sql-server-setup"></a>Hinzufügen von Funktionen zu einer Instanz von SQL Server (Setup)
  Dieses Thema bietet eine schrittweise Anleitung zum Hinzufügen von Funktionen zu einer Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Einige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten oder -Dienste gehören speziell zu einer bestimmten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sie werden auch als instanzabhängig bezeichnet. Sie nutzen die gleiche Version wie ihre Hostinstanz und werden ausschließlich für diese Instanz verwendet. Sie können einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die instanzabhängigen Komponenten zusammen mit den freigegebenen Komponenten hinzufügen, wenn sie nicht bereits installiert sind. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen von SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
 Informationen zum Hinzufügen einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] über die Eingabeaufforderung finden Sie unter [Install SQL Server from the Command Prompt (Installieren von SQL Server über die Eingabeaufforderung)](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Bevor Sie den Vorgang fortsetzen, lesen Sie die Themen unter [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
>  Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie auf der Remotefreigabe ein Domänenkonto mit Leseberechtigungen verwenden.  
  
> [!NOTE]  
>  Wenn Sie einer Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Funktionen hinzufügen, werden die vorhandenen Einstellungen für Verwendungsberichte auf die neu hinzugefügten Funktionen angewendet. Um diese Einstellungen zu ändern, verwenden Sie das Tool **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im** -Menü [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Konfigurationstools** .  
  
## <a name="procedures"></a>Vorgehensweisen  
  
#### <a name="to-add-features-to-an-instance-of-includesscurrentincludessscurrent-mdmd"></a>Informationen zum Hinzufügen einer Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Legen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationsmedium ein. Doppelklicken Sie im Stammordner auf setup.exe. Bei einer Installation über eine Netzwerkfreigabe navigieren Sie zum Stammordner der Freigabe, und doppelklicken Sie auf setup.exe. Wenn das Dialogfeld zum Einrichten von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] angezeigt wird, [!INCLUDE[clickOK](../../includes/clickok-md.md)] , um die erforderlichen Komponenten zu installieren, und klicken Sie auf **Abbrechen** , um die Installation von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] abzubrechen.  
  
2.  Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installationscenter wird vom Installations-Assistenten gestartet. Um einer vorhandenen Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] eine neue Funktion hinzuzufügen, klicken Sie im linken Navigationsbereich auf **Installation** und anschließend auf **Neue eigenständige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.  
  
3.  Die Systemkonfigurationsprüfung führt einen Ermittlungsvorgang auf dem Computer aus. Klicken Sie auf **Details anzeigen**, um die Überprüfungsdetails anzuzeigen. [!INCLUDE[clickOK](../../includes/clickok-md.md)], um den Vorgang fortzusetzen.  
  
4.  Auf der Seite für Produktupdates werden die neuesten verfügbaren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produktupdates angezeigt. Wenn Sie die Updates nicht einschließen möchten, deaktivieren Sie das Kontrollkästchen **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produktupdates einschließen**. Wenn keine Produktupdates ermittelt wurden, zeigt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup diese Seite nicht an und geht automatisch zur Seite **Setupdateien installieren** über.  
  
5.  Auf der Seite Setupdateien installieren wird der Status angezeigt, während die Setupdateien heruntergeladen, extrahiert und installiert werden. Wenn ein Update für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup gefunden und angegeben wird, dass das Update eingeschlossen werden soll, wird dieses Update ebenfalls installiert. Klicken Sie auf **Installieren** , um die Unterstützungsdateien für Setup zu installieren.  
  
6.  Die Systemkonfigurationsprüfung überprüft den Systemstatus des Computers, bevor Setup fortgesetzt wird.  
  
7.  Wählen Sie auf der Seite „Installationstyp“ die Option **Funktionen zu einer vorhandenen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz hinzufügen**, und wählen Sie dann die Instanz aus, die Sie aktualisieren möchten.  
  
8.  Wählen Sie auf der Seite Funktionsauswahl die Komponenten für die Installation aus. Nach Auswahl des Funktionsnamens wird im rechten Bereich eine Beschreibung für die einzelnen Komponentengruppen angezeigt. Sie können jede beliebige Kombination von Kontrollkästchen aktivieren. Weitere Informationen finden Sie unter [Editionen und unterstützte Funktionen von SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md). Jede Komponente kann auf einer bestimmten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nur einmal installiert werden. Wenn Sie mehrere Komponenten installieren möchten, müssen Sie eine zusätzliche Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren.  
  
     Die erforderlichen Komponenten für die ausgewählten Funktionen werden im rechten Bereich angezeigt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup installiert die erforderlichen Komponenten, die nicht bereits während des Installationsschritts installiert werden, der im weiteren Verlauf dieser Prozedur beschrieben wird.  
  
     Die Systemkonfigurationsprüfung überprüft den Systemstatus des Computers, bevor Setup fortgesetzt wird. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
9. Auf der Seite Erforderlicher Speicherplatz wird der für die angegebenen Funktionen erforderliche Speicherplatz berechnet, und die Anforderungen werden mit dem Speicherplatz verglichen, der auf dem Computer verfügbar ist, auf dem Setup ausgeführt wird.  
  
10. Der weitere Ablauf dieses Themas hängt von den Funktionen ab, die Sie für die Installation angegeben haben. Je nach Auswahl werden möglicherweise nicht alle Seiten angezeigt.  
  
11. Geben Sie auf der Seite Serverkonfiguration – Dienstkonten Anmeldekonten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste an. Welche Dienste tatsächlich auf dieser Seite konfiguriert werden, hängt von den Funktionen ab, die Sie für die Installation ausgewählt haben.  
  
     Sie können allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Diensten dasselbe Anmeldekonto zuweisen, oder Sie können jedes Dienstkonto einzeln konfigurieren. Außerdem können Sie angeben, ob Dienste automatisch starten sollen, manuell gestartet werden oder deaktiviert sind. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, die Dienstkonten einzeln zu konfigurieren, um möglichst geringe Rechte für jeden Dienst bereitzustellen. Dabei erhalten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste die Berechtigungen, die mindestens erforderlich sind, um ihre Tasks auszuführen. Weitere Informationen finden Sie unter [Serverkonfiguration – Dienstkonten](http://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) und [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Um für alle Dienstkonten in dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dasselbe Anmeldekonto anzugeben, geben Sie im Feld unten auf dieser Seite die entsprechenden Anmeldeinformationen ein.  
  
     **Sicherheitshinweis** : [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Wenn Sie die Angabe der Anmeldeinformationen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste abgeschlossen haben, klicken Sie auf **Weiter**.  
  
12. Verwenden Sie die Registerkarte **Serverkonfiguration – Sortierung** , um nicht standardmäßige Sortierungen für das [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]anzugeben. Weitere Informationen finden Sie unter [Serverkonfiguration – Sortierung](http://msdn.microsoft.com/library/e3986870-5be4-458b-b671-5ff12a27b022).  
  
13. Geben Sie auf der Seite Konfiguration des [!INCLUDE[ssDE](../../includes/ssde-md.md)] s – Kontenbereitstellung folgende Informationen an:  
  
    -   Sicherheitsmodus – Wählen Sie die Windows-Authentifizierung oder die Authentifizierung im gemischten Modus für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aus. Bei Auswahl des gemischten Authentifizierungsmodus müssen Sie ein sicheres Kennwort für das integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministratorkonto angeben.  
  
         Nachdem ein Gerät erfolgreich eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat, wird für die Windows-Authentifizierung und den gemischten Modus derselbe Sicherheitsmechanismus verwendet. Weitere Informationen finden Sie unter [Konfiguration des Datenbankmoduls – Serverkonfiguration](http://msdn.microsoft.com/library/834b26bc-49de-4033-88d5-6aa7b1609720).  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administratoren – Sie müssen wenigstens einen Systemadministrator für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angeben. Um das Konto hinzuzufügen, unter dem das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup ausgeführt werden soll, klicken Sie auf **Aktuellen Benutzer hinzufügen**. Um Konten zur Liste der Systemadministratoren hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**, und bearbeiten Sie anschließend die Liste der Benutzer, Gruppen bzw. Computer, die Administratorrechte für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz haben sollen. Weitere Informationen finden Sie unter [Konfiguration des Datenbankmoduls – Serverkonfiguration](http://msdn.microsoft.com/library/834b26bc-49de-4033-88d5-6aa7b1609720).  
  
     Wenn Sie die Bearbeitung der Liste abgeschlossen haben, klicken Sie auf **OK**. Überprüfen Sie die Liste der Administratoren im Konfigurationsdialogfeld. Sobald die Liste vollständig ist, klicken Sie auf **Weiter**.  
  
14. Geben Sie ggf. auf der Seite [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Konfiguration – Datenverzeichnisse andere Installationsverzeichnisse als das Standardinstallationsverzeichnis an. Wenn die Installation in Standardverzeichnissen erfolgen soll, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie keine Standardverzeichnisse angeben, sollten Sie sicherstellen, dass die Installationsordner nur für die Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen anderer Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]genutzt werden.  
  
     Weitere Informationen finden Sie unter [Konfiguration des Datenbankmoduls – Datenverzeichnisse](http://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487).  
  
15. Aktivieren Sie auf der Seite [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Konfiguration – FILESTREAM den FILESTREAM für Ihre Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen zu FILESTREAM finden Sie unter [Konfiguration des Datenbankmoduls – Filestream](http://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02). Klicken Sie auf Weiter, um den Vorgang fortzusetzen.  
  
16. Verwenden Sie die Seite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Konfiguration – Kontenbereitstellung-Konfiguration – Kontenbereitstellung, um den Servermodus und die Benutzer oder Konten anzugeben, die über Administratorberechtigungen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]verfügen sollen. Durch den Servermodus wird bestimmt, welcher Arbeitsspeicher und welche Speichersubsysteme auf dem Server verwendet werden. Die unterschiedlichen Projektmappentypen werden in verschiedenen Servermodi ausgeführt. Wenn Sie beabsichtigen, mehrdimensionale Cubedatenbanken auf dem Server auszuführen, wählen Sie die Standardoption, den mehrdimensionalen und Data Mining-Servermodus, aus. Damit Administratorberechtigungen vorhanden sind, müssen Sie mindestens einen Systemadministrator für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]angeben. Um das Konto hinzuzufügen, unter dem das SQL Server-Setup ausgeführt wird, klicken Sie auf **Aktuellen Benutzer hinzufügen**. Um Konten zur Liste der Systemadministratoren hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**, und bearbeiten Sie anschließend die Liste der Benutzer, Gruppen bzw. Computer, die Administratorrechte für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]haben sollen. Weitere Informationen zu Servermodus und Administratorberechtigungen finden Sie unter [Analysis Services-Konfiguration – Kontobereitstellung](http://msdn.microsoft.com/library/169b1af2-6fe2-467f-8ca4-919f24c620ce).  
  
     Wenn Sie die Bearbeitung der Liste abgeschlossen haben, klicken Sie auf **OK**. Überprüfen Sie die Liste der Administratoren im Konfigurationsdialogfeld. Sobald die Liste vollständig ist, klicken Sie auf **Weiter**.  
  
17. Geben Sie ggf. auf der Seite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Konfiguration – Datenverzeichnisse andere Installationsverzeichnisse als das Standardinstallationsverzeichnis an. Wenn die Installation in Standardverzeichnissen erfolgen soll, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie keine Standardverzeichnisse angeben, sollten Sie sicherstellen, dass die Installationsordner nur für die Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen anderer Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]genutzt werden.  
  
     Weitere Informationen finden Sie unter [Analysis Services-Konfiguration – Datenverzeichnisse](http://msdn.microsoft.com/library/ef732855-b7af-4f40-a619-5573c1c354bb).  
  
18. Auf der Seite für die Konfiguration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] können Sie die Art der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Installation angeben, die erstellt werden soll. Weitere Informationen zu [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Konfigurationsmodi finden Sie unter [Reporting Services-Konfigurationsoptionen &#40;SSRS&#41;](http://msdn.microsoft.com/library/e4561f6c-bc7f-467e-821a-cde8e5cd7391).  
  
19. Verwenden Sie die Seite für die Distributed Replay Controller-Konfiguration, um die Benutzer anzugeben, denen Sie Administratorberechtigungen für den Distributed Replay Controller-Dienst erteilen möchten. Benutzer, die über Administratorberechtigungen verfügen, besitzen unbeschränkten Zugriff auf den Distributed Replay Controller-Dienst.  
  
     Klicken Sie auf die Schaltfläche **Aktuellen Benutzer hinzufügen** , um die Benutzer hinzuzufügen, denen Sie Zugriffsberechtigungen für den Distributed Replay Controller-Dienst erteilen möchten. Klicken Sie auf die Schaltfläche **Hinzufügen** , um Zugriffsberechtigungen für den Distributed Replay Controller-Dienst hinzuzufügen. Klicken Sie auf die Schaltfläche **Entfernen** , um Zugriffsberechtigungen für den Distributed Replay Controller-Dienst zu entfernen.  
  
     Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
20. Verwenden Sie die Seite für die Distributed Replay Client-Konfiguration, um die Benutzer anzugeben, denen Sie Administratorberechtigungen für den Distributed Replay Client-Dienst erteilen möchten. Benutzer, die über Administratorberechtigungen verfügen, besitzen unbeschränkten Zugriff auf den Distributed Replay Client-Dienst.  
  
     **Controllername** ist ein optionaler Parameter, und der Standardwert ist \<*leer*>. Geben Sie den Namen des Controllers ein, mit dem der Clientcomputer für den Distributed Replay Client-Dienst kommuniziert. Beachten Sie Folgendes:  
  
    -   Wenn Sie bereits einen Controller eingerichtet haben, geben Sie den Namen des Controllers beim Konfigurieren jedes Clients ein.  
  
    -   Wenn Sie noch keinen Controller eingerichtet haben, können Sie das Feld für den Controllernamen leer lassen. Sie müssen den Controllernamen jedoch in der **Clientkonfigurationsdatei** manuell eingeben.  
  
     Geben Sie das **Arbeitsverzeichnis** für den Distributed Replay Client-Dienst an. Das Standardarbeitsverzeichnis ist \<*Laufwerkbuchstabe*>:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     Geben Sie das **Ergebnisverzeichnis** für den Distributed Replay Client-Dienst an. Das Standardergebnisverzeichnis ist \<*Laufwerkbuchstabe*>:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
21. Geben Sie auf der Seite Fehlerberichterstellung die Informationen an, die Sie an [!INCLUDE[msCoName](../../includes/msconame-md.md)] senden möchten, um zur Verbesserung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]beizutragen. Die Option für Fehlerberichte ist standardmäßig aktiviert.  
  
22. Die Systemkonfigurationsprüfung führt einen weiteren Regelsatz aus, um die Konfiguration des Computers anhand der von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen zu überprüfen.  
  
23. Auf der Seite Installationsbereit wird eine Strukturansicht der Installationsoptionen angezeigt, die während des Setups angegeben wurden. Auf dieser Setupseite ist neben der letzten Updateversion auch angegeben, ob die Produktupdatefunktion aktiviert oder deaktiviert ist. Nachdem Sie auf Installieren geklickt haben, werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup zunächst die erforderlichen Komponenten für die ausgewählten Funktionen und anschließend die Funktionen installiert.  
  
24. Während der Installation wird auf der Seite Installationsstatus der Status angegeben, sodass Sie während der Installation den Installationsstatus überwachen können.  
  
25. Nach der Installation bietet die Seite Abgeschlossen einen Link zur zusammenfassenden Protokolldatei für die Installation und andere wichtige Hinweise. Klicken Sie auf **Schließen**, um die Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abzuschließen.  
  
26. Starten Sie den Computer neu, falls Sie dazu aufgefordert werden. Nachdem das Setup abgeschlossen ist, sollten Sie unbedingt die vom Installations-Assistenten ausgegebene Meldung lesen. Weitere Informationen finden Sie unter [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Nächste Schritte  
 Konfigurieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation  
  
-   Zum Reduzieren der Angriffsfläche eines Systems installiert und aktiviert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selektiv Schlüsseldienste und -funktionen. Weitere Informationen finden Sie unter [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Überprüfen einer SQL Server-Installation](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [Reparieren von Fehlern bei einer SQL Server 2016-Installation](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)   
 [Upgrade von SQL Server mithilfe des Installations-Assistenten &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
