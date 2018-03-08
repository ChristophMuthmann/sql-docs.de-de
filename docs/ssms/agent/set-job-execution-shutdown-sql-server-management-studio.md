---
title: "Festlegen des Herunterfahrens der Auftragsausführung (SQL Server Management Studio) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50e6b465dc2d4e3b49239a1ed247395d5e513584
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Set Job Execution Shutdown (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] festlegen, wie lange der [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent auf die Beendigung von ausführenden Aufträgen wartet, bevor der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent selbst beendet wird.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So legen Sie eine Zeit für das Herunterfahren für einen SQL Server-Agent-Auftrag fest mit**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Standardmäßig können Mitglieder der festen Serverrolle **sysadmin** die Zeit festlegen, in welcher der [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent auf die Beendigung von ausgeführten Aufträgen wartet, bevor der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent selbst beendet wird. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>So legen Sie das Herunterfahren der Auftragsausführung fest  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, auf dem Sie ein Intervall für das Herunterfahren der Auftragsausführung festlegen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent** , und wählen Sie **Eigenschaften**aus.  
  
3.  Wählen Sie unter **Seite auswählen**die Option **Auftragssystem**aus.  
  
4.  Erhöhen oder reduzieren Sie den Wert für **Timeoutintervall beim Herunterfahren (Sekunden)** . Damit wird bestimmt, wie lange der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent auf die Beendigung von ausführenden Aufträgen wartet, bevor der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent selbst beendet wird.  
  
