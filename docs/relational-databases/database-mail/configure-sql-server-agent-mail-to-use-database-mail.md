---
title: Konfigurieren von SQL Server-Agent-Mail zum Verwenden von Datenbank-E-Mails | Microsoft Dokumentation
ms.custom: ''
ms.date: 08/05/2016
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
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: dd0b4ebffd6d2a87044994bcbb35936d1a198575
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>Konfigurieren von SQL Server-Agent-Mail zum Verwenden von Datenbank-E-Mails
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zur Verwendung von Datenbank-E-Mails konfiguriert wird, damit Benachrichtigungen und Warnungen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]versendet werden.  Weitere Informationen zum Konfigurieren der Funktion für Datenbank-E-Mail finden Sie unter [Konfigurieren von Datenbank-E-Mail](../../relational-databases/database-mail/configure-database-mail.md).  Ein Beispiel zur Verwendung von [!INCLUDE[tsql](../../includes/tsql-md.md)]finden Sie unter [Erstellen eines Profils für Datenbank-E-Mail](../../relational-databases/database-mail/create-a-database-mail-profile.md).
  
-   **Vorbereitungen:**  
  
-   [Erforderliche Komponenten](#Prerequisites)  
  
-   [Security](#Security)  
  
-   [So konfigurieren Sie mithilfe von SQL Server Management Studio den SQL Server-Agent zur Verwendung von Datenbank-E-Mail](#SSMSProcedure)  
  
-   [Anschlussaufgaben](#Follow_Up)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   [Aktivieren von Datenbank-E-Mail](../../relational-databases/database-mail/configure-database-mail.md).  
  
-    [Erstellen Sie ein Konto für Datenbank-E-Mail](../../relational-databases/database-mail/create-a-database-mail-account.md) zur Nutzung durch das Dienstkonto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents.  
  
-   [Erstellen Sie ein Datenbank-E-Mail-Profil](../../relational-databases/database-mail/create-a-database-mail-profile.md) für das zu verwendende Konto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstes, und fügen Sie den Benutzer zur **DatabaseMailUserRole** in der **msdb** -Datenbank hinzu.  
  
-   Legen Sie das Profil als Standardprofil für die **msdb** -Datenbank fest.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Der Benutzer, der die Profilkonten erstellt und gespeicherte Prozeduren ausführt, sollte Mitglied der festen Serverrolle "sysadmin" sein.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 **So konfigurieren Sie den SQL Server-Agent zum Verwenden von Datenbank-E-Mail**  
  
-   Erweitern Sie im Objekt-Explorer eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz.  
  
-   Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, und klicken Sie anschließend auf **Eigenschaften**.  
  
-   Klicken Sie auf **Warnungssystem**.  
  
-   Wählen Sie **Mailprofil aktivieren**aus.  
  
-   Wählen Sie in der Liste **Mailsystem** die Option **Datenbank-E-Mail**aus.  
  
-   Wählen Sie in der Liste **Mailprofil**ein Mailprofil für Datenbank-E-Mail aus.  
  
-   Starten Sie SQL Server-Agent neu.  
  
##  <a name="Follow_Up"></a> Anschlussaufgaben  
 Die folgenden Aufgaben sind zum Abschließen der Konfiguration des Agents zum Senden von Warnungen und Benachrichtigungen erforderlich:  
  
-   [Warnungen](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef)  
  
     Warnungen können zum Benachrichtigen eines Operators über ein bestimmtes Datenbankereignis oder eine Betriebssystembedingung konfiguriert werden.  
  
-   [Operatoren](http://msdn.microsoft.com/library/38e8488f-2669-4cea-b9c3-5f394a663678)  
  
     Operatoren sind Aliase für Personen oder Gruppen, die elektronische Benachrichtigung empfangen können.  
  
  
