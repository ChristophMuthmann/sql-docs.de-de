---
title: "Löschen von Aufträgen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f5e08e59ade5619787882695f6183bf1526dc557
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="delete-jobs"></a>Löschen von Aufträgen
Ein Auftrag besteht aus einer festgelegten Folge von Operationen, die der SQL Server-Agent der Reihenfolge nach ausführt. Standardmäßig werden Aufträge nicht gelöscht, wenn die Ausführung beendet wird. Sie können einen oder mehrere [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agentaufträge unabhängig davon löschen, ob der Auftrag erfolgreich war. Außerdem können Sie den [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent zum automatischen Löschen von Aufträgen konfigurieren, wenn diese erfolgreich sind, einen Fehler erzeugen oder abgeschlossen werden.  
  
Standardmäßig können Mitglieder der festen Serverrolle **sysadmin** die gespeicherte Systemprozedur [sp_delete_job (Transact-SQL)](http://msdn.microsoft.com/en-us/b85db6e4-623c-41f1-9643-07e5ea38db09) ausführen, um einen Auftrag zu löschen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Nur Mitglieder der festen Serverrolle **sysadmin** können **sp_delete_job** ausführen, um einen beliebigen Auftrag zu löschen. Ein Benutzer, der kein Mitglied der festen Serverrolle **sysadmin** ist, kann nur Aufträge löschen, deren Besitzer er ist.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|**Description**|**Thema**|  
|Es wird beschrieben, wie Sie einen oder mehrere [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agentaufträge löschen.|[Löschen eines oder mehrerer Aufträge](../../ssms/agent/delete-one-or-more-jobs.md)|  
|Es wird die Vorgehensweise zum Konfigurieren des [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents für das automatische Löschen von Aufträgen beschrieben, wenn diese erfolgreich sind, einen Fehler erzeugen oder abgeschlossen werden.|[Automatisches Löschen eines Auftrags](../../ssms/agent/automatically-delete-a-job.md)|  
  

