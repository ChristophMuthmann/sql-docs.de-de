---
title: Verwalten von Ereignissitzungen im Objekt-Explorer | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: extended-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16849e38-d3fb-414d-8dcb-797b5ffce6ee
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 68a7d7a381ece14f87dd7bb25514ba773fd2b27f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="manage-event-sessions-in-the-object-explorer"></a>Verwalten von Ereignissitzungen im Objekt-Explorer
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In diesem Thema werden die Aktionen erläutert, die Sie im **Objekt-Explorer** ausführen können und die sich auf erweiterte Ereignisse auswirken:  
  
-   Erstellen einer Sitzung für erweiterte Ereignisse  
  
-   Starten oder Beenden einer Sitzung für erweiterte Ereignisse  
  
-   Exportieren einer Sitzung für erweiterte Ereignisse  
  
-   Importieren einer Sitzungsvorlage für erweiterte Ereignisse  
  
-   Bearbeiten einer Sitzung für erweiterte Ereignisse  
  
-   Löschen einer Sitzung für erweiterte Ereignisse  
  
## <a name="create-an-extended-events-session"></a>Erstellen einer Sitzung für erweiterte Ereignisse  
 Weitere Informationen zum Erstellen einer Sitzung für erweiterte Ereignisse finden Sie unter [Erstellen einer Sitzung für erweiterte Ereignisse](http://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74).  
  
## <a name="starting-or-stopping-an-extended-events-session"></a>Starten oder Beenden einer Sitzung für erweiterte Ereignisse  
 Sie können eine Sitzung für erweiterte Ereignisse mithilfe des **Abfrage-Editors** starten oder beenden, indem Sie die Anweisung **ALTER EVENT SESSION** oder den Knoten **Erweiterte Ereignisse** des **Objekt-Explorers**verwenden.  
  
 Wenn Sie eine Ereignissitzung beenden, wird die Sitzung in der dynamischen Verwaltungssicht (dynamic management view; DMV) von „sys.dm_xe_sessions“ nicht mehr als aktive Sitzung aufgeführt. Die Sitzungsdefinition bleibt jedoch intakt, und Sie können die Sitzung neu starten. Um eine Sitzungsdefinition vollständig zu entfernen, müssen Sie die Sitzung löschen.  
  
 Zum Starten oder Beenden einer Sitzung für erweiterte Ereignisse müssen Sie über die ALTER ANY EVENT SESSION-Berechtigung verfügen.  
  
 Beim Beenden einer Sitzung, die ein Arbeitsspeicherziel verwendet, z.B. den Ringpuffer, Buckets, Ereignispaarung oder synchrone Ereigniszählerziele, gehen die gesamten im Puffer der Sitzung gespeicherten Informationen (die target_data-Spalte der „sys.dm_xe_session_targets“-DMV) verloren. Um auch nach dem Beenden der Sitzung auf die Ereignisdaten zugreifen zu können, sollten Sie die Daten speichern, bevor Sie die Sitzung beenden, oder die Sitzung so konfigurieren, dass sie das Dateiziel verwendet.  
  
### <a name="start-or-stop-an-extended-events-session-using-query-editor"></a>Starten oder Beenden einer Sitzung für erweiterte Ereignisse mithilfe des Abfrage-Editors  
 Geben Sie die folgenden Anweisungen aus, und ersetzen Sie dabei *Sitzungsname* durch den Namen der Sitzung für erweiterte Ereignisse, um eine Sitzung zu starten:  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = START  
```  
  
 Um eine Sitzung zu beenden, geben Sie die folgenden Anweisungen aus, und ersetzen Sie dabei *Sitzungsname* durch den Namen der Sitzung für erweiterte Ereignisse:  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = STOP  
```  
  
### <a name="start-or-stop-an-extended-events-session-in-object-explorer"></a>Starten oder Beenden einer Sitzung für erweiterte Ereignisse mittels Objekt-Explorer  
 Erweitern Sie die Knoten **Verwaltung**, **Erweiterte Ereignisse**und **Sitzungen**, klicken mit der rechten Maustaste auf eine Sitzung und klicken anschließend auf **Sitzung starten** oder **Sitzung beenden** , um im **Objekt-Explorer**eine Sitzung für erweiterte Ereignisse zu starten oder zu beenden.  
  
## <a name="export-an-extended-events-session-template"></a>Exportieren einer Sitzungsvorlage für erweiterte Ereignisse  
 Sie können mit dem **Objekt-Explorer**eine Sitzung für erweiterte Ereignisse exportieren und diese als XML-Vorlage speichern. Beispielsweise können Sie eine Sitzung exportieren und anschließend mithilfe des **Assistenten für neue Sitzungen** die Vorlage auf eine **neue Ereignissitzung** anwenden.  
  
 Stellen Sie beim Exportieren einer Sitzung sicher, dass Sie die Vorlagendatei an einem Speicherort speichern, der das NTFS-Dateisystem verwendet. Schränken Sie zudem den Zugriff auf Benutzer ein, die zum Anzeigen der Informationen autorisiert sind.  
  
 So exportieren Sie mit dem **Objekt-Explorer**eine Sitzung für erweiterte Ereignisse:  
  
1.  Erweitern Sie die Knoten **Verwaltung**, **Erweiterte Ereignisse**und anschließend **Sitzungen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die zu exportierende Sitzung, und wählen Sie anschließend **Sitzung exportieren**aus.  
  
3.  Wählen Sie im Dialogfeld **Speichern unter** einen Speicherort zum Speichern der Datei aus, geben Sie den Dateinamen in das Feld **Dateiname** ein, und klicken Sie auf **Speichern**.  
  
     Wenn Sie die Datei am Standardspeicherort für [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Vorlagen speichern, wird die Vorlage in der Dropdownliste vordefinierter Vorlagen angezeigt, wenn Sie das Dialogfeld **Assistent für neue Sitzungen** und **Neue Sitzung** verwenden.  
  
## <a name="import-an-extended-events-session-template"></a>Importieren einer Sitzungsvorlage für erweiterte Ereignisse  
 Sie können mit dem **Objekt-Explorer**eine Vorlage für eine Sitzung für erweiterte Ereignisse importieren. Dies ist beispielsweise hilfreich, um eine Sitzung aus einer Vorlage zu erstellen, die aus einer anderen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]exportiert wurde.  
  
 Zum Löschen einer Sitzung für erweiterte Ereignisse müssen Sie über die **ALTER ANY EVENT SESSION** -Berechtigung verfügen.  
  
 Bevor Sie eine Vorlagendatei importieren, stellen Sie sicher, dass die Datei aus einer vertrauenswürdigen Quelle stammt. Die Vorlagendateien sollten an einem Speicherort gespeichert werden, bei dem das NTFS-Dateisystem verwendet und der Zugriff auf Benutzer eingeschränkt wird, die zum Anzeigen der Informationen autorisiert sind.  
  
 So importieren Sie eine Sitzung für erweiterte Ereignisse:  
  
1.  Erweitern Sie im **Objekt-Explorer**die Knoten **Verwaltung**und **Erweiterte Ereignisse** .  
  
2.  Klicken Sie mit der rechten Maustaste auf **Sitzungen** , und wählen Sie anschließend **Neue Sitzung**.  
  
3.  Geben Sie einen Namen für die Sitzung an.  
  
4.  Erweitern Sie das Dropdownfeld **Vorlage** .  
  
5.  Klicken Sie auf **\<Aus Datei…>Öffnen** und suchen Sie nach der Sitzung (XML-Datei), die Sie importieren möchten.  
  
 Die Sitzung wird unter dem Knoten **Sitzungen** angezeigt. Standardmäßig die Sitzung nicht gestartet.  
  
## <a name="edit-an-extended-events-session"></a>Bearbeiten einer Sitzung für erweiterte Ereignisse  
 Sie können eine Sitzung für erweiterte Ereignisse in Objekt-Explorer bearbeiten.  
  
 So bearbeiten Sie eine Sitzung für erweiterte Ereignisse:  
  
1.  Erweitern Sie im **Objekt-Explorer**die Knoten **Verwaltung**, **Erweiterte Ereignisse**und **Sitzungen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf eine Sitzung, und wählen Sie **Eigenschaften**aus.  
  
3.  Wählen Sie im Abschnitt **Seite auswählen** die Seite oder Seiten aus, die Sie bearbeiten möchten.  
  
4.  Klicken Sie nach der Überarbeitung der Ereignissitzung auf **OK**.  
  
## <a name="script-an-event-session-definition-using-includetsqlincludestsql-mdmd"></a>Skript für eine Ereignissitzung als Definition mit [!INCLUDE[tsql](../../includes/tsql-md.md)]  
 Sowohl der Assistent für neue Sitzungen als auch das Dialogfeld "Neue Sitzung" verfügen über eine Skriptoption, die den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code generiert, der die Sitzung für erweiterte Ereignisse definiert.  
  
 Sie können auf den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code für eine vorhandene Sitzung für erweiterte Ereignisse zugreifen, indem Sie mit der rechten Maustaste auf den Sitzungsnamen klicken, die Option **Skript für Sitzung als**und dann **Erstellen in**auswählen.  
  
## <a name="delete-an-extended-events-session"></a>Löschen einer Sitzung für erweiterte Ereignisse  
 Sie können eine Sitzung für erweiterte Ereignisse löschen:  
  
-   Im Abfrage-Editor mit **DROP EVENT SESSION**  
  
-   Im **Objekt-Explorer**  
  
 Wenn Sie eine Ereignissitzung löschen, werden alle Konfigurationsinformationen entfernt, und die Sitzungsdefinition wird nicht mehr in der „sys.server_event_sessions“-Katalogsicht angezeigt.  
  
> [!NOTE]  
>  system_health und AlwaysOn_health sind in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthalten. Löschen Sie sie auf keinen Fall. system_health ist standardmäßig aktiviert (weitere Informationen finden Sie unter [Verwenden der system_health-Sitzung](../../relational-databases/extended-events/use-the-system-health-session.md)). AlwaysOn_health ist standardmäßig deaktiviert. Diese Sitzungen erfassen Daten, die für das Diagnostizieren von Leistungsproblemen hilfreich sein können.  
  
 Zum Löschen einer Sitzung für erweiterte Ereignisse müssen Sie über die ALTER ANY EVENT SESSION-Berechtigung verfügen.  
  
 So löschen Sie eine Sitzung für erweiterte Ereignisse im **Objekt-Explorer**:  
  
1.  Erweitern Sie die Knoten **Verwaltung**, **Erweiterte Ereignisse**und anschließend **Sitzungen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf eine Sitzung, und wählen Sie **Löschen**aus.  
  
3.  Klicken Sie im Dialogfeld **Objekt löschen** auf **OK**.  
  
4.  Klicken Sie nach der Überarbeitung der Ereignissitzung auf **OK**.  
  
 Geben Sie die folgenden Anweisungen ein, und ersetzen Sie dabei **Sitzungsname**durch den Namen der Sitzung für erweiterte Ereignisse, die Sie löschen möchten, um eine Sitzung für erweiterte Ereignisse im *Abfrage-Editor* zu löschen:  
  
```  
DROP EVENT SESSION [session_name]  
ON SERVER  
```  
  
  
