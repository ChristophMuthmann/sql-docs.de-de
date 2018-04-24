---
title: Erstellen eines Kontos für die Datenbank-E-Mail | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mail
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Mail [SQL Server], accounts
- accounts [Database Mail]
ms.assetid: c07abbc6-fc6a-470b-8fa3-532f2e06b16a
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5d12abd7f84a6e50851ac6cd434057104d977dd4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-database-mail-account"></a>Erstellen eines Kontos für Datenbank-E-Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Verwenden Sie entweder den **Assistenten zum Konfigurieren von Datenbank-E-Mail** oder [!INCLUDE[tsql](../../includes/tsql-md.md)] , um ein Datenbank-E-Mail-Konto zu erstellen.  
  
-   **Vorbereitungen:**  [Voraussetzungen](#Prerequisites)  
  
-   **Erstellen eines Datenbank-E-Mail-Kontos mit:**  [Assistenten zum Konfigurieren von Datenbank-E-Mail](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nächste Schritte zum Konfigurieren von Datenbank-E-Mail](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Bestimmen Sie den Servernamen und die Portnummer für den SMTP-Server (Simple Mail Transfer Protocol), den Sie zum Senden von E-Mail verwenden. Falls der SMTP-Server eine Authentifizierung erfordert, bestimmen Sie den Benutzernamen und das Kennwort für den SMTP-Server.  
  
-   Optional können Sie auch den Servertyp und die Portnummer für den Server angeben. Der Servertyp ist für ausgehende E-Mails immer 'SMTP'. Die meisten SMTP-Server verwenden standardmäßig Port 25.  
  
##  <a name="SSMSProcedure"></a> Verwenden des Assistenten zum Konfigurieren von Datenbank-E-Mail  
 **So erstellen Sie ein Konto für Datenbank-E-Mail mithilfe eines Assistenten**  
  
-   Stellen Sie im Objekt-Explorer eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, auf der Datenbank-E-Mail konfiguriert werden soll, und erweitern Sie die Serverstruktur.  
  
-   Erweitern Sie den Knoten **Verwaltung** .  
  
-   Doppelklicken Sie auf "Datenbank-E-Mail", um den Assistenten zum Konfigurieren von Datenbank-E-Mail zu öffnen.  
  
-   Aktivieren Sie auf der Seite **Konfigurationsaufgabe auswählen** die Option **Konten und Profile für Datenbank-E-Mail verwalten**, und klicken Sie auf **Weiter**.  
  
-   Wählen Sie auf der Seite **Profile und Konten verwalten** die Option **Neues Konto erstellen** , und klicken Sie dann auf **Weiter**.  
  
-   Geben Sie auf der Seite **Neues Konto** den Kontonamen, eine Beschreibung, Informationen zum Mailserver und den Authentifizierungstyp an. Klicken Sie auf **Weiter**.  
  
-   Überprüfen Sie auf der Seite **Assistenten abschließen** die auszuführenden Aktionen, und klicken Sie auf **Fertig stellen** , um die Erstellung des neuen Kontos abzuschließen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So erstellen Sie ein Konto für Datenbank-E-Mail mithilfe von Transact-SQL**  
  
 Führen Sie die gespeicherte Prozedur **msdb.dbo.sysmail_add_account_sp** aus, um das Konto zu erstellen, und geben Sie die folgenden Informationen an:  
  
-   Den Namen des zu erstellenden Kontos  
  
-   Eine optionale Beschreibung des Kontos  
  
-   Die E-Mail-Adresse, die auf ausgehenden E-Mail-Nachrichten angezeigt werden soll  
  
-   Den Namen, der auf ausgehenden E-Mail-Nachrichten angezeigt werden soll  
  
-   Den Namen des SMTP-Servers  
  
-   Den Benutzernamen, der zum Anmelden am SMTP-Server verwendet werden soll, falls der SMTP-Server eine Authentifizierung erfordert  
  
-   Das Kennwort, das zum Anmelden am SMTP-Server verwendet werden soll, falls der SMTP-Server eine Authentifizierung erfordert  
  
 Im folgenden Beispiel wird ein neues Datenbank-E-Mail-Konto erstellt.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nächste Schritte zum Konfigurieren von Datenbank-E-Mail  
  
-   [Erstellen eines Profils für Datenbank-E-Mail](../../relational-databases/database-mail/create-a-database-mail-profile.md)  
  
  
