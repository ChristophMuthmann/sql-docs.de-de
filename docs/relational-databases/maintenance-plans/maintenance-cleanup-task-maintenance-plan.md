---
title: "Task &#39;Wartungscleanup&#39; (Wartungsplan) | Microsoft Docs"
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
  - "sql13.swb.maint.cleanup.f1"
helpviewer_keywords: 
  - "Wartungscleanup (Dialogfeld für den Task)"
ms.assetid: 022b679c-6799-4c13-9185-814224a20412
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# Task &#39;Wartungscleanup&#39; (Wartungsplan)
  Mit dem **Task 'Wartungscleanup'** können Sie alte Dateien für Wartungspläne löschen, u. a. von Wartungsplänen und Datenbanksicherungsdateien erstellte Textberichte.  
  
> [!NOTE]  
>  Dateien in den Unterordnern des angegebenen Verzeichnisses werden vom Task Wartungscleanup nicht automatisch gelöscht. Diese Funktion reduziert die Möglichkeit eines bösartigen Angriffs, der den Task Wartungscleanup zum Löschen von Dateien verwendet. Wenn Sie Dateien in Unterordnern auf oberster Ebene löschen möchten, müssen Sie **Unterordner auf oberster Ebene einschließen** auswählen.  
  
## Optionen  
 **Verbindung**  
 Zeigt die aktuelle Verbindung an.  
  
 **Neu**  
 Erstellen Sie eine neue Serververbindung, die bei der Ausführung dieses Tasks verwendet werden soll. Das Dialogfeld **Neue Verbindung** wird im Folgenden beschrieben.  
  
 **Sicherungsdateien**  
 Löscht Sicherungsdateien.  
  
 **Textberichte für Wartungsplan**  
 Löscht Textberichte über zuvor ausgeführte Wartungspläne.  
  
 **Bestimmte Datei löschen**  
 Löscht die im Feld **Dateiname** angegebene Datei.  
  
 **Dateiname**  
 Pfad und Name der zu löschenden Datei.  
  
 **Ordner durchsuchen und Dateien anhand einer Erweiterung löschen**  
 Löscht alle Dateien mit der angegebenen Erweiterung im angegebenen Ordner. Mithilfe dieser Option können Sie mehrere Dateien gleichzeitig löschen, z. B. alle Sicherungsdateien mit der Erweiterung .bak im ausgewählten Ordner.  
  
 **Ordner**  
 Pfad und Name des Ordners, in dem die zu löschenden Dateien enthalten sind.  
  
 **Dateierweiterung**  
 Geben Sie die Dateierweiterung der zu löschenden Dateien an.  
  
 **Unterordner auf oberster Ebene einschließen**  
 Löscht Dateien mit der für **Dateierweiterung** angegebenen Erweiterung aus den Unterordnern der obersten Ebene unter **Ordner**.  
  
 **Dateien anhand ihres Alters zur Tasklaufzeit löschen**  
 Geben Sie das Mindestalter der zu löschenden Dateien an, indem Sie im Feld **Dateien löschen, die älter sind als** eine Zahl und eine Zeiteinheit festlegen.  
  
 **Dateien löschen, die älter sind als**  
 Geben Sie das Mindestalter der zu löschenden Dateien an, in dem Sie eine Nummer und eine Zeiteinheit (Tag, Woche, Monat oder Jahr) festlegen. Dateien, die älter sind als der angegebene Zeitrahmen, werden gelöscht.  
  
 **T-SQL anzeigen**  
 Zeigt die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen an, die für diesen Task auf dem Server auf Basis der ausgewählten Optionen ausgeführt werden.  
  
> [!NOTE]  
>  Wenn die Anzahl der betroffenen Objekte groß ist, kann die Anzeige erhebliche Zeit in Anspruch nehmen.  
  
## Neue Verbindung (Dialogfeld)  
 **Verbindungsname**  
 Geben Sie einen Namen für die neue Verbindung ein.  
  
 **Wählen Sie einen Servernamen aus, oder geben Sie ihn ein.**  
 Wählen Sie den Server aus, zu dem bei der Ausführung dieses Tasks eine Verbindung hergestellt werden soll.  
  
 **…**  
 Wählen Sie diese Option aus, um die Liste der verfügbaren Server anzuzeigen.  
  
 **Geben Sie Informationen zum Anmelden am Server ein**  
 Legt fest, wie die Authentifizierung gegenüber dem Server stattfindet.  
  
 **Integrierte Sicherheit von Windows NT verwenden**  
 Stellt mithilfe der Microsoft Windows-Authentifizierung eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her.  
  
 **Bestimmten Benutzernamen und bestimmtes Kennwort verwenden**  
 Stellt mithilfe der SQL Server-Authentifizierung eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her. Diese Option ist nicht verfügbar.  
  
 **Benutzername**  
 Stellt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung für den Gebrauch bei der Authentifizierung bereit. Diese Option ist nicht verfügbar.  
  
 **Kennwort**  
 Stellt ein Kennwort für den Gebrauch bei der Authentifizierung bereit. Diese Option ist nicht verfügbar.  
  
## Siehe auch  
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  