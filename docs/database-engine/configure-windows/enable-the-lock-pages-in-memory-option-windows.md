---
title: "Aktivieren der Option Sperren von Seiten im Speicher (Windows) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sperren von Seiten im Speicher (Option)"
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Aktivieren der Option Sperren von Seiten im Speicher (Windows)
  Mit dieser Windows-Richtlinie werden die Konten bestimmt, die einen Prozess zum Speichern von Daten im physischen Speicher verwenden können, um das systemgesteuerte Auslagern der Daten in den virtuellen Arbeitsspeicher zu vermeiden.  
  
> [!NOTE]  
>  Durch Sperren von Seiten im Arbeitsspeicher kann die Leistung bei der Auslagerung von Arbeitsspeicherdaten auf die Festplatte gesteigert werden.  
  
 Verwenden Sie das Windows-Tool für Gruppenrichtlinien (gpedit.msc), um diese Richtlinie für das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendete Konto zu aktivieren. Diese Richtlinie können Sie nur ändern, wenn Sie als Systemadministrator angemeldet sind.  
  
### So aktivieren Sie die Option "Sperren von Seiten im Speicher"  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**. Geben Sie **gpedit.msc** im Feld **Öffnen**ein.  
  
2.  Erweitern Sie in der Konsole **Editor für lokale Gruppenrichtlinien** die Option **Computerkonfiguration**und dann **Windows-Einstellungen**.  
  
3.  Erweitern Sie **Sicherheitseinstellungen**und dann **Lokale Richtlinien**.  
  
4.  Wählen Sie den Ordner **Zuweisen von Benutzerrechten** aus.  
  
     Die Richtlinien werden im Detailbereich angezeigt.  
  
5.  Doppelklicken Sie im Detailbereich auf **Sperren von Seiten im Speicher**.  
  
6.  Klicken Sie im Dialogfeld **Lokale Sicherheitseinstellung – Sperren von Seiten im Speicher** auf **Benutzer oder Gruppe hinzufügen**.  
  
7.  Fügen Sie im Dialogfeld zum Auswählen von Benutzern, Dienstkonten oder Gruppen ein Konto mit Privilegien zum Ausführen von **sqlservr.exe** hinzu.  
  
8.  Melden Sie sich ab und anschließend erneut an, damit die Änderung wirksam wird.  
  
## Siehe auch  
 [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  