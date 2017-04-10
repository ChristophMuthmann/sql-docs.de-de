---
title: "Einstellungen f&#252;r die sekund&#228;re Datenbank | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.databaseproperties.logshipping.settings.dest.f1"
ms.assetid: f992ffc9-ee42-43fe-acec-512032f0ded1
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# Einstellungen f&#252;r die sekund&#228;re Datenbank
  Mithilfe dieses Dialogfelds konfigurieren und ändern Sie die Eigenschaften einer sekundären Datenbank in der Protokollversandkonfiguration.  
  
 Eine Erläuterung zu den Konzepten des Protokollversands finden Sie unter [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## Optionen  
 **Sekundäre Serverinstanz**  
 Zeigt den Namen der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, die in der Protokollversandkonfiguration derzeit als sekundärer Server konfiguriert ist.  
  
 **Sekundäre Datenbank**  
 Zeigt den Namen der sekundären Datenbank für die Protokollversandkonfiguration an. Wenn Sie einer Protokollversandkonfiguration eine neue sekundäre Datenbank hinzufügen, können Sie eine Datenbank aus der Liste auswählen oder den Namen einer neuen Datenbank in das Feld eingeben. Wenn Sie den Namen einer neuen Datenbank in das Feld eingeben, müssen Sie auf der Registerkarte **Initialisierung** eine Option auswählen, die eine vollständige Datenbanksicherung der primären Datenbank in der sekundären Datenbank wiederherstellt. Die neue Datenbank wird im Verlauf des Wiederherstellungsvorgangs erstellt.  
  
 **Connect**  
 Stellen Sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Verwendung als sekundärer Server in der Protokollversandkonfiguration her. Das zum Verbinden verwendete Konto muss Mitglied der festen Serverrolle sysadmin auf der sekundären Serverinstanz sein.  
  
 **Registerkarte Initialisieren**  
 Folgende Optionen stehen zur Verfügung:  
  
 **Ja, eine vollständige Sicherung der primären Datenbank generieren und diese Sicherung in der sekundären Datenbank wiederherstellen**  
 Veranlassen Sie, dass [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] die sekundäre Datenbank konfiguriert, indem die primäre Datenbank gesichert und auf dem sekundären Server wiederhergestellt wird. Wenn Sie in das Feld **Sekundäre Datenbank** den Namen einer neuen Datenbank eingegeben haben, wird die Datenbank im Verlauf des Wiederherstellungsvorgangs erstellt.  
  
 **Wiederherstellungsoptionen**  
 Klicken Sie auf diese Schaltfläche, wenn die Daten und Protokolldateien für die sekundäre Datenbank auf dem sekundären Server an Speicherorten wiederhergestellt werden sollen, die nicht den Standardeinstellungen entsprechen.  
  
 Mit dieser Schaltfläche öffnen Sie das Dialogfeld **Wiederherstellungsoptionen** . Dort können Sie Pfade zu nicht den Standardeinstellungen entsprechenden Ordnern angeben, in denen die sekundäre Datenbank und ihre Protokolle gespeichert werden sollen. Es müssen immer beide Ordner angegeben werden.  
  
 Die Pfade müssen auf Laufwerke verweisen, die auf dem sekundären Server lokale Laufwerke darstellen. Die Pfadangabe muss ferner mit einem lokalen Laufwerkbuchstaben und einem Doppelpunkt beginnen (z. B. `C:`). Zugeordnete Laufwerkbuchstaben bzw. Netzwerkpfade sind ungültig.  
  
 Wenn Sie auf die Schaltfläche **Wiederherstellungsoptionen** klicken und dann entscheiden, dass Sie doch die Standardordner verwenden möchten, empfehlen wir, das Dialogfeld **Wiederherstellungsoptionen** zu schließen (Abbrechen). Wenn Sie bereits nicht den Standardeinstellungen entsprechende Speicherorte angegeben haben und dann doch die Standardspeicherorte verwenden möchten, klicken Sie erneut auf **Wiederherstellungsoptionen** , löschen Sie den Inhalt der Textfelder, und klicken Sie dann auf OK.  
  
 **Ja, eine vorhandene Sicherung der primären Datenbank in der sekundären Datenbank wiederherstellen**  
 Veranlassen Sie, dass [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] für die Initialisierung der sekundären Datenbank eine vorhandene Sicherung der primären Datenbank verwendet. Geben Sie den Speicherort dieser Sicherung in das Feld **Sicherungsdatei** ein. Wenn Sie in das Feld Sekundäre Datenbank den Namen einer neuen Datenbank eingegeben haben, wird die Datenbank im Verlauf des Wiederherstellungsvorgangs erstellt.  
  
 **Sicherungsdatei**  
 Geben Sie den Pfad und den Dateinamen der vollständigen Datenbanksicherung ein, die für die Initialisierung der sekundären Datenbank verwendet werden soll, wenn Sie die Option **Ja, eine vorhandene Sicherung der primären Datenbank in der sekundären Datenbank wiederherstellen** ausgewählt haben.  
  
 **Wiederherstellungsoptionen**  
 Siehe dazu die Beschreibung dieser Schaltfläche an einer früheren Stelle dieses Themas.  
  
 **Nein, die sekundäre Datenbank ist initialisiert**  
 Gibt an, dass die sekundäre Datenbank bereits initialisiert ist und in ihr die Sicherungen der Transaktionsprotokolle aus der primären Datenbank wiederhergestellt werden können. Diese Option ist nicht verfügbar, wenn Sie in das Feld **Sekundäre Datenbank** den Namen einer neuen Datenbank eingegeben haben.  
  
 **Registerkarte Dateien kopieren**  
 Folgende Optionen stehen zur Verfügung:  
  
 **Zielordner für kopierte Dateien**  
 Geben Sie den Pfad ein, in den Transaktionsprotokollsicherungen zur Wiederherstellung in der sekundären Datenbank kopiert werden sollen. Dies ist in der Regel der lokale Pfad zu einem Ordner auf dem sekundären Server. Wenn sich der Ordner auf einem anderen Server befindet, müssen Sie jedoch einen UNC-Pfad zu dem Ordner angeben. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto der sekundären Serverinstanz muss über Leseberechtigungen für diesen Ordner verfügen. Außerdem müssen Sie für die Proxykonten dieser Netzwerkfreigabe, unter denen die Kopier- und Wiederherstellungsaufträge auf den sekundären Serverinstanzen ausgeführt werden, Lese- und Schreibberechtigungen erteilen. Standardmäßig ist dies das SQL Server Agent-Dienstkonto der sekundären Serverinstanz. Ein Systemadministrator kann jedoch für die Aufträge andere Proxykonten auswählen.  
  
 **Kopierte Dateien löschen nach**  
 Legt fest, wie lange die kopierten Sicherungsdateien der Transaktionsprotokolle im Zielordner verbleiben, bevor sie gelöscht werden.  
  
 **Auftragsname**  
 Zeigt den Namen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agentauftrags an, der verwendet wird, um Sicherungsdateien des Transaktionsprotokolls vom primären Server auf den sekundären Server zu kopieren. Wenn Sie den Auftrag erstmalig erstellen, können Sie den Namen durch Eingabe in das entsprechende Feld ändern.  
  
 **Zeitplan**  
 Zeigt den aktuellen Zeitplan für den Kopierauftrag des SQL Server-Agents an, mit dem die Transaktionsprotokollsicherungen vom primären auf den sekundären Server kopiert werden. Diesen Zeitplan können Sie ändern. Dazu klicken Sie auf **Zeitplan...**.  
  
 **Zeitplan...**  
 Ändert die Parameter des SQL Server-Agentauftrags, von dem die Transaktionsprotokollsicherungen vom primären auf den sekundären Server kopiert werden.  
  
 **Diesen Auftrag deaktivieren**  
 Hält den vom SQL Server-Agent bereitgestellten Kopierauftrag an.  
  
 **Registerkarte Transaktionsprotokoll wiederherstellen**  
 Folgende Optionen stehen zur Verfügung:  
  
 **Beim Wiederherstellen von Sicherungen Verbindungen mit Benutzern in der Datenbank trennen**  
 Trennt Benutzer automatisch von der sekundären Datenbank, solange Transaktionsprotokollsicherungen wiederhergestellt werden.  
  
 **Kein Wiederherstellungsmodus**  
 Belässt die sekundäre Datenbank im NORECOVERY-Modus.  
  
 **Standbymodus**  
 Belässt die sekundäre Datenbank im STANDBY-Modus. In diesem Modus können schreibgeschützte Vorgänge in der Datenbank ausgeführt werden.  
  
> [!IMPORTANT]  
>  Wenn Sie den Wiederherstellungsmodus für eine vorhandene sekundäre Datenbank von beispielsweise **Kein Wiederherstellungsmodus** in **Standbymodus** ändern, wird diese Änderung erst umgesetzt, nachdem die nächste Protokollsicherung in der Datenbank wiederhergestellt wurde.  
  
 **Wiederherstellen von Sicherungen verzögern um mindestens**  
 Wählen Sie ggf. die Wartezeit vor der Wiederherstellung von Transaktionsprotokollsicherungen in der sekundären Datenbank.  
  
 **Warnen, wenn keine Wiederherstellung erfolgt in**  
 Wählen Sie die Zeitspanne, die beim Protokollversand gewartet werden soll, bevor eine Warnung ausgelöst wird, weil keine Wiederherstellung von Transaktionsprotokollen erfolgt ist.  
  
 **Auftragsname**  
 Zeigt den Namen des SQL Server-Agentauftrags an, von dem die Transaktionsprotokollsicherungen in der sekundären Datenbank wiederhergestellt werden sollen. Wenn Sie den Auftrag erstmalig erstellen, können Sie den Namen durch Eingabe in das entsprechende Feld ändern.  
  
 **Zeitplan**  
 Zeigt den aktuellen Zeitplan für den SQL Server-Agentauftrag an, von dem die Transaktionsprotokollsicherungen in der sekundären Datenbank wiederhergestellt werden. Diese Option können Sie ändern. Dazu klicken Sie auf **Zeitplan...**.  
  
 **Zeitplan...**  
 Ändert die Parameter, die dem SQL Server-Agentwiederherstellungsauftrag zugeordnet sind.  
  
 **Diesen Auftrag deaktivieren**  
 Unterdrückt Wiederherstellungsvorgänge in der sekundären Datenbank.  
  
## Siehe auch  
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  