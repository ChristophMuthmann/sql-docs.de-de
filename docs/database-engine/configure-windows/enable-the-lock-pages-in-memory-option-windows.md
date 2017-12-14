---
title: "Aktivieren der Option „Sperren von Seiten im Speicher“ (Windows) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3278e9eaf53426fef36b42c47e63cdf049de4266
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Aktivieren der Option Sperren von Seiten im Speicher (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mit dieser Windows-Richtlinie werden die Konten bestimmt, die einen Prozess zum Speichern von Daten im physischen Speicher verwenden können, um das systemgesteuerte Auslagern der Daten in den virtuellen Arbeitsspeicher zu vermeiden.  
  
> [!NOTE]  
>  Durch Sperren von Seiten im Arbeitsspeicher kann die Leistung bei der Auslagerung von Arbeitsspeicherdaten auf die Festplatte gesteigert werden.  
  
 Verwenden Sie das Windows-Tool für Gruppenrichtlinien (gpedit.msc), um diese Richtlinie für das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendete Konto zu aktivieren. Diese Richtlinie können Sie nur ändern, wenn Sie als Systemadministrator angemeldet sind.  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>So aktivieren Sie die Option "Sperren von Seiten im Speicher"  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**. Geben Sie **gpedit.msc** im Feld **Öffnen**ein.  
  
2.  Erweitern Sie in der Konsole **Editor für lokale Gruppenrichtlinien** die Option **Computerkonfiguration**und dann **Windows-Einstellungen**.  
  
3.  Erweitern Sie **Sicherheitseinstellungen**und dann **Lokale Richtlinien**.  
  
4.  Wählen Sie den Ordner **Zuweisen von Benutzerrechten** aus.  
  
     Die Richtlinien werden im Detailbereich angezeigt.  
  
5.  Doppelklicken Sie im Detailbereich auf **Sperren von Seiten im Speicher**.  
  
6.  Klicken Sie im Dialogfeld **Lokale Sicherheitseinstellung – Sperren von Seiten im Speicher** auf **Benutzer oder Gruppe hinzufügen**.  
  
7.  Fügen Sie im Dialogfeld zum Auswählen von Benutzern, Dienstkonten oder Gruppen ein Konto mit Privilegien zum Ausführen von **sqlservr.exe** hinzu.  
  
8.  Melden Sie sich ab und anschließend erneut an, damit die Änderung wirksam wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
