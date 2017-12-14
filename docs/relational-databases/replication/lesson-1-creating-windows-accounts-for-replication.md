---
title: "Lektion 1: Erstellen von Windows-Konten für die Replikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
- replication [SQL Server], administering
ms.assetid: 65c3816b-47f0-448c-a4a4-ebd3e2a58820
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9688b2bac34a38ea667557b997adfed3e7cf37d3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-1-creating-windows-accounts-for-replication"></a>Lektion 1: Erstellen von Windows-Konten für die Replikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In dieser Lektion erstellen Sie Windows-Konten zum Ausführen von Replikations-Agents. Sie erstellen für die folgenden Agents ein separates Windows-Konto auf dem lokalen Server:  
  
|Agent|Speicherort|Kontoname|  
|---------|------------|----------------|  
|Momentaufnahme-Agent|Verleger|\<*machine_name*>\repl_snapshot|  
|Protokolllese-Agent|Verleger|\<*machine_name*>\repl_logreader|  
|Verteilungs-Agent|Verleger und Abonnent|\<*machine_name*>\repl_distribution|  
|Merge-Agent|Verleger und Abonnent|\<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> In den Replikationslernprogrammen wird für Verleger und Verteiler dieselbe Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gemeinsam verwendet. Verleger und Abonnent können dieselbe Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gemeinsam verwenden; dies ist jedoch keine Anforderung. Wenn der Verleger und Abonnent dieselbe Instanz verwenden, sind die Schritte zum Erstellen von Konten auf dem Verleger nicht erforderlich.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>So erstellen Sie lokale Windows-Konten für Replikations-Agents auf dem Verleger  
  
1.  Öffnen Sie auf dem Verleger in der Systemsteuerung in **Verwaltung** das Tool **Computerverwaltung** .  
  
2.  Erweitern Sie unter **System**den Eintrag **Lokale Benutzer und Gruppen**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Benutzer** und anschließend auf **Neuer Benutzer**.  
  
4.  Geben Sie **repl_snapshot** im Feld **Benutzername** ein, geben Sie das Kennwort und weitere relevante Informationen an, und klicken Sie anschließend auf **Erstellen** , um das Konto repl_snapshot zu erstellen.  
  
5.  Wiederholen Sie den letzten Schritt, um die Konten repl_logreader, repl_distribution und repl_merge zu erstellen.  
  
6.  Klicken Sie auf **Schließen**.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>So erstellen Sie lokale Windows-Konten für Replikations-Agents auf dem Abonnenten  
  
1.  Öffnen Sie auf dem Abonnenten in der Systemsteuerung in **Verwaltung** das Tool **Computerverwaltung** .  
  
2.  Erweitern Sie unter **System**den Eintrag **Lokale Benutzer und Gruppen**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Benutzer** und anschließend auf **Neuer Benutzer**.  
  
4.  Geben Sie **repl_distribution** im Feld **Benutzername** ein, geben Sie das Kennwort und weitere relevante Informationen an, und klicken Sie anschließend auf **Erstellen** , um das Konto repl_distribution zu erstellen.  
  
5.  Wiederholen Sie den letzten Schritt, um das Konto repl_merge zu erstellen.  
  
6.  Klicken Sie auf **Schließen**.  
  
## <a name="next-steps"></a>Nächste Schritte  
Sie haben Windows-Konten für Replikations-Agents erfolgreich erstellt. Als Nächstes konfigurieren Sie den Momentaufnahmeordner. Weitere Informationen finden Sie unter [Lektion 2: Vorbereiten des Momentaufnahmeordners](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Siehe auch  
[Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
  
