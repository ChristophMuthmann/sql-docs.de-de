---
title: Sichern und Wiederherstellen eine Datenbank mithilfe von SQL Operations Studio (preview) | Microsoft Docs
description: Weitere Informationen Sie zum Sichern und Wiederherstellen einer Datenbank mithilfe von SQL Operations Studio (preview)
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46ef55aa54275e356eff9674aac10a27b36d758e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>Sicherung und Wiederherstellung verwendet[!INCLUDE[name-sos](../includes/name-sos-short.md)]

In diesem Lernprogramm erfahren Sie, wie Sie [!INCLUDE[name-sos](../includes/name-sos-short.md)] an:
> [!div class="checklist"]
> * Sichern einer Datenbank 
> * Zeigen Sie den Sicherungsstatus an
> * Generiert das Skript verwendet, um die Sicherung auszuführen.
> * Wiederherstellen einer Datenbank
> * Anzeigen des Status des Tasks "Wiederherstellung"

## <a name="prerequisites"></a>Voraussetzungen

Dieses Lernprogramm erfordert SQL Server *TutorialDB*. Zum Erstellen der *TutorialDB* Datenbank, führen Sie eines der folgenden Schnellstarts:

- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des SQL Server ab[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)


## <a name="backup-a-database"></a>Sichern einer Datenbank

1. Öffnen Sie das Datenbank-Dashboard TutorialDB (Öffnen Sie die **Server** Randleiste (**STRG + G**), erweitern Sie **Datenbanken**, mit der rechten Maustaste **TutorialDB**, und wählen Sie **verwalten**). 

2. Öffnen der **Backup Database** Dialogfeld (klicken Sie auf **Sicherung** auf die **Aufgaben** Widget).

   ![Aufgaben-widget](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Dieses Lernprogramm verwendet die Standard-Sicherungsoptionen, klicken Sie also **Backup**.
   ![Das Dialogfeld Sicherung](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Nach dem Klicken auf **Backup**, **Backup Database** Dialogfeld ausgeblendet, und im Rahmen des Sicherungsvorgangs beginnt.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Anzeigen des Sicherungsstatus und das Sicherungsskript anzeigen

1. Öffnen der **Taskverlauf** Randleiste, indem Sie auf das Symbol "Format" auf die *Aktionsleiste* oder drücken Sie **STRG + T**.

   ![Taskverlauf](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Um das Sicherungsskript im Editor anzuzeigen, Maustaste **Sicherungsdatenbank erfolgreich** , und wählen Sie **Skript**.

   ![Sicherungsskript](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>Stellen Sie eine Datenbank aus einer Sicherungsdatei wieder her.


1. Öffnen der **Server** Randleiste (**STRG + G**) mit der rechten Maustaste auf den Server, und wählen Sie **verwalten**. 

2. Öffnen der **datenbankwiederherstellungs-** Dialogfeld (klicken Sie auf **wiederherstellen** auf die **Aufgaben** Widget).

2. Wählen Sie **Sicherungsdatei** in der **Wiederherstellen von** Feld. 

3. Klicken Sie auf die Auslassungspunkte (...) in der **Dateipfad der Zertifikatsicherung** Feld, und wählen Sie die neueste Sicherungsdatei für *TutorialDB*.

3. Typ **TutorialDB_Restored** in der **Zieldatenbank** -Feld in der **Ziel** Abschnitt aus, um die Sicherungsdatei in einer neuen Datenbank wiederherstellen.

   ![Wiederherstellungsprozess](./media/tutorial-backup-restore-sql-server/restore.png)

4. Klicken Sie auf **wiederherstellen**

5. Klicken Sie zum Anzeigen des Status des Wiederherstellungsvorgangs auf **STRG + T** So öffnen die **Taskverlauf** Randleiste.

   ![Wiederherstellungsprozess](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


In diesem Lernprogramm haben Sie gelernt, wie:
> [!div class="checklist"]
> * Sichern einer Datenbank 
> * Zeigen Sie den Sicherungsstatus an
> * Generiert das Skript verwendet, um die Sicherung auszuführen.
> * Wiederherstellen einer Datenbank
> * Anzeigen des Status des Tasks "Wiederherstellung"

