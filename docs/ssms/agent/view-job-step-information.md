---
title: Anzeigen von Auftragsschrittinformationen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying job step information
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- viewing job step information
ms.assetid: e3f06492-dc86-4e06-b186-ea58aff6d591
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e9fde8db3e733999869a0f36789475c1fb6c2902
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="view-job-step-information"></a>View Job Step Information
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie die Auftragsschrittdetails im Auftragsschritt-Eigenschaftendialogfeld anzeigen. Es enthält auch Informationen zum Anzeigen der Auftragsschrittausgabe.  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So zeigen Sie Auftragsschrittinformationen an mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
Wenn der Auftragsschritt so konfiguriert wurde, dass seine Ausgabe in eine Tabelle oder Datei geschrieben wird, und der Auftrag wurde mindestens einmal ausgeführt, können Sie die Ausgabe auf der Seite **Erweitert** des Dialogfelds **Auftragsschritt-Eigenschaften** anzeigen. Beim Löschen eines Auftrags oder Auftragsschritts wird das Ausgabeprotokoll automatisch gelöscht.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Sie können nur die Aufträge anzeigen, die Sie besitzen, es sei denn, Sie sind ein Mitglied der festen Serverrolle **sysadmin** . Mitglieder dieser Rolle können alle Aufträge und Auftragsschrittdetails anzeigen.  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-job-step-information"></a>So zeigen Sie Auftragsschrittinformationen an  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**, erweitern Sie **Aufträge**, klicken Sie mit der rechten Maustaste auf den Auftrag, dessen Auftragsschritte Sie anzeigen möchten, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie im Dialogfeld **Auftragseigenschaften** die Seite **Schritte** aus.  
  
4.  Klicken Sie auf den anzuzeigenden Auftragsschritt, und klicken Sie auf **Bearbeiten**.  
  
5.  Sie können auf der Seite **Allgemein** des Dialogfelds **Auftragsschritt-Eigenschaften** den Typ des Auftragsschritts anzeigen und welche Aktion er ausführt.  
  
6.  Klicken Sie auf die Seite **Erweitert** , um die Aktionen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents anzuzeigen wenn der Auftragsschritt erfolgreich ausgeführt wird oder einen Fehler erzeugt, wie oft der Auftragsschritt wiederholt werden sollte, wohin die Auftragsschrittausgabe geschrieben wird und welcher Benutzer den Auftragsschritt ausführt.  
  
#### <a name="to-view-job-step-output"></a>So zeigen Sie die Auftragsschrittausgabe an  
  
1.  Klicken Sie im Dialogfeld **Auftragsschritt-Eigenschaften** auf die Seite **Erweitert** .  
  
2.  Abhängig von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Version, mit der Sie verbunden sind, können Sie entweder die Auftragsschritt-Ausgabedatei oder die Auftragsschritt-Ausgabetabelle wie folgt anzeigen:  
  
    -   Wenn Sie mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder einer höheren Version verbunden sind, können Sie nur dann auf **Anzeigen** klicken, wenn **In Tabelle protokollieren** aktiviert ist. In diesem Fall wird die Auftragsschrittausgabe in die **sysjobstepslogs** -Tabelle der **msdb** -Datenbank geschrieben.  
  
    -   Die Schaltfläche **Anzeigen** ist deaktiviert, wenn die Auftragsschrittausgabe in eine Datei geschrieben wird. Verwenden Sie den Editor zum Anzeigen der Auftragsschritt-Ausgabedatei.  
  
