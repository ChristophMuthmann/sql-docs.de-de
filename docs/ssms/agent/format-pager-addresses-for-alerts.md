---
title: "Formatieren von Pageradressen für Warnungen | Microsoft-Dokumentation"
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
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f202f1e48ca7c9ef030b5434514c4c5d6a93300b
ms.lasthandoff: 04/11/2017

---
# <a name="format-pager-addresses-for-alerts"></a>Format Pager Addresses for Alerts
In diesem Thema wird beschrieben, wie Pageradressen für [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Warnungen in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]formatiert werden.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So formatieren Sie Pageradressen mit**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** Information über eine Warnung anzeigen. Andere Benutzer müssen Mitglieder der festen Datenbankrolle **SQLAgentOperatorRole** in der **msdb** -Datenbank sein.  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-format-pager-addresses"></a>So formatieren Sie Pageradressen  
  
1.  Klicken Sie im Objekt-Explorer ****auf das Pluszeichen, um den Server zu erweitern, der die Warnung enthält, die Sie an einen Pager senden möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent** , und wählen Sie **Eigenschaften**aus.  
  
3.  Wählen Sie unter **Seite auswählen**die Option **Warnungssystem**aus.  
  
4.  Geben Sie in die Felder **An-Zeile** und **Cc-Zeile** des Felds **Adressformatierung für Pager-E-Mails:** das Präfix oder das Suffix der Pageradresse ein. Die eigentliche Pageradresse des Operators wird beim Senden einer Benachrichtigung eingefügt.  
  
5.  Geben Sie in das Feld **Betreff** das Präfix oder Suffix der Betreffzeile ein.  
  
6.  Aktivieren Sie das Kontrollkästchen **Nachrichtenbereich der E-Mail in Benachrichtigungsseite aufnehmen** , um die vollständige E-Mail-Nachricht in die Pagernachricht einzuschließen (statt lediglich die Betreffzeile).  
  
7.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  

