---
title: Warnungseigenschaften – Neue Warnung (Seite „Antwort“) | Microsoft-Dokumentation
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
- sql13.ag.alert.response.f1
ms.assetid: 72daf008-f9ea-4077-b217-5048e7759d3e
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4c5882dec04bebe4cebddfeae4bb61d5b12a130
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="alert-properties---new-alert-response-page"></a>Warnungseigenschaften – Neue Warnung (Seite „Antwort“)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Verwenden Sie diese Seite, um einen Auftrag, den Sie ausführen möchten, festzulegen und um eine Liste der Operatoren abzurufen, die bei einer [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Warnung benachrichtigt werden sollen.  

## <a name="options"></a>Tastatur  
**Auftrag ausführen**  
Aktiviert die Optionen **Auftragsliste**, **Neuer Auftrag** und **Auftrag anzeigen** .  
  
**Neuer Auftrag**  
Öffnet das Dialogfeld **Neuer Auftrag** . Diese Schaltfläche ist nicht verfügbar, wenn **Auftrag ausführen** nicht ausgewählt ist.  
  
**Auftrag anzeigen**  
Zeigen Sie den ausgewählten Auftrag an oder ändern Sie ihn. Diese Option ist nicht verfügbar, wenn **Auftrag ausführen** nicht ausgewählt ist.  
  
**Operatoren benachrichtigen**  
Aktiviert die Steuerelemente, mit denen Sie Operatoren hinzufügen, entfernen oder ändern können.  
  
**Operatorliste**  
Enthält die Operatoren, die benachrichtigt werden, wenn eine Warnung auftritt. Aktivieren Sie das Kontrollkästchen **E-Mail**, **Pager**oder **NET SEND** hinter dem Operatornamen, um eine Benachrichtigungsmethode festzulegen. Diese Option ist nicht verfügbar, wenn **Operatoren benachrichtigen** nicht ausgewählt ist.  
  
**E-Mail**  
Verwenden Sie E-Mail zum Benachrichtigen des Operators.  
  
**Pager**  
Verwenden Sie die Pager-E-Mail-Adresse zum Benachrichtigen des Operators.  
  
**NET SEND**  
Verwenden Sie zum Benachrichtigen des Operators die Option **NET SEND** .  
  
**Neuer Operator**  
Zeigt das Dialogfeld **Neuer Operator** an, in dem Sie einen neuen Operator erstellen können.  
  
**Operator anzeigen**  
Zeigt das Dialogfeld **Eigenschaften** für den derzeit ausgewählten Operator an. Über das Dialogfeld **Operator-Eigenschaften** können Sie die Operator-Eigenschaften anzeigen und ändern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Warnungen](../../ssms/agent/alerts.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
[Warnungen](../../ssms/agent/alerts.md)  
[Edit an Alert](../../ssms/agent/edit-an-alert.md)  
[Delete an Alert](../../ssms/agent/delete-an-alert.md)  
  
