---
title: Auftragsaktivitätsmonitor | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.jobactivitymonitor.alljobs.f1
- SQL13.SWB.ACTIVITYMON.F1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a157963a80e17cc718e258c0a32d84be6d71e576
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="job-activity-monitor"></a>Auftragsaktivitätsmonitor
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Mithilfe dieser Seite können Sie die aktuelle Aktivität von Aufträgen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents anzeigen. Klicken Sie auf **Filter** , um die Anzahl der angezeigten Aufträge zu beschränken. Das Raster **Agentauftragsaktivität** ist schreibgeschützt. Klicken Sie auf die Spaltenheader, um das Raster zu sortieren. Sie können einen Auftrag ändern, indem Sie auf den betreffenden Auftrag doppelklicken und das Dialogfeld **Auftragseigenschaften** öffnen. Klicken Sie mit der rechten Maustaste auf einen Auftrag im Raster, um die Ausführung aller Auftragsschritte zu starten, einen speziellen Auftragsschritt zu starten, den Auftrag zu aktivieren oder zu deaktivieren, den Auftrag zu aktualisieren, den Auftrag zu löschen, den Verlauf des Auftrags anzuzeigen oder die Auftragseigenschaften anzuzeigen. Klicken Sie auf **Aktualisieren** , um das Raster mit den aktuellen Informationen zu aktualisieren.  
  
## <a name="options"></a>Tastatur  
**Name**  
Name des Auftrags.  
  
**Enabled**  
Zeigt an, ob der Auftrag aktiviert (**Ja**) oder nicht aktiviert (**Nein**) ist.  
  
**Status***  
Aktueller Status des Auftrags  
  
**Ergebnis der letzten Ausführung**  
Auftragsstatus bei der letzten Ausführung  
  
**Zuletzt ausgeführt**  
Datum und Uhrzeit, an dem bzw. zu der der Auftrag zuletzt ausgeführt wurde (ausgehend vom lokalen Datum und der lokalen Uhrzeit des Servers).  
  
**Nächste Ausführung***  
Datum und Uhrzeit des Zeitpunkts, an dem die nächste Ausführung des Auftrags geplant ist (ausgehend vom lokalen Datum und der lokalen Uhrzeit des Servers).  
  
**Kategorie**  
Die dem Auftrag zugewiesene Auftragskategorie.  
  
**Ausführbar**  
**Ja** , wenn der Auftrag ausgeführt werden kann; **Nein** , wenn der Auftrag nicht ausgeführt werden kann. Ein Auftrag kann nicht ausgeführt werden, wenn er keine Schritte oder keinen Zielserver aufweist.  
  
**Geplant**  
**Ja** , wenn der Auftrag einem Auftragszeitplan zugewiesen ist; **Nein** , wenn für den Auftrag kein Zeitplan vorhanden ist.  
  
* Nur Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Serverrolle „sysadmin“ und die Serveradministratorgruppe können Werte in dieser Spalte sehen. Mitglieder der SQLAgentOperatorRole-Rolle können keine Werte in dieser Spalte sehen.  
  
#### <a name="to-open-the-job-activity-monitor"></a>So öffnen Sie den Auftragsaktivitätsmonitor  
  
-   Erweitern Sie in **Objekt-Explorer**den verwendeten Server und anschließend **SQL Server-Agent**. Klicken Sie mit der rechten Maustaste auf **Auftragsaktivitätsmonitor**, und klicken Sie dann auf **Auftragsaktivitäten anzeigen**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Überwachen der Auftragsaktivität](../../ssms/agent/monitor-job-activity.md)  
  
