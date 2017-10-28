---
title: SQL Server-Agent-Eigenschaften (Seite Warnungssystem)|Microsoft-Dokumente
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.agent.alert.f1
ms.assetid: 3e6d3bfd-20ee-4593-86cc-f65b1c08c69d
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 334a1025cca8100f1ba6bcc0855712a7e5fe0ef0
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-agent-properties-alert-system-page"></a>SQL Server-Agent-Eigenschaften (Seite Warnungssystem)
Auf dieser Seite können Sie die Einstellungen für die vom [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent versandten Warnmeldungen anzeigen und ändern.  
  
## <a name="options"></a>enthalten  
**Mailsitzung**  
Mithilfe der Optionen in diesem Abschnitt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Mail konfiguriert.  
  
**Mailprofil aktivieren**  
Aktiviert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Mail. Standardmäßig ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Mail nicht aktiviert.  
  
**Mailsystem**  
Legt das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent zu verwendende Mailsystem fest. Datenbank-E-Mail  
  
> [!NOTE]  
> Nach der Änderung des E-Mail-Systems müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst neu starten, damit die Änderung wirksam wird.  
  
**Mailprofil**  
Legt das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent zu verwendende Profil fest. Sie können auch **\< neues Profil für Datenbank-E-Mail...>** wählen, um ein neues Profil zu erstellen.  
  
**Pager-E-Mails**  
Mithilfe der Optionen in diesem Abschnitt können Sie die an Pageradressen zu versendenden E-Mail-Nachrichten so konfigurieren, dass eine Kommunikation mit Ihrem Pagingsystem möglich ist.  
  
**Adressformatierung für Pager-E-Mails**  
In diesem Abschnitt können Sie das in Pager-E-Mails verwendete Format für Adressen und Betreffzeile angeben.  
  
**An-Zeile**  
Bestimmt die Optionen für die Zeile **An** der Nachricht.  
  
**Prfix**  
Geben Sie einen beliebigen festgelegten Text ein, den das System bei Nachrichten, die an Pager gesendet werden, am Anfang der Zeile **An** verlangt.  
  
**Pager**  
Enthält die E-Mail-Adresse der Nachricht zwischen Präfix und Suffix.  
  
**Suffix**  
Geben Sie einen beliebigen festgelegten Text ein, den das Pagingsystem bei Nachrichten, die an Pager gesendet werden, am Ende der Zeile **An** verlangt.  
  
**Cc-Zeile**  
Bestimmt Optionen für die Zeile **Cc** der Nachricht.  
  
**Prfix**  
Geben Sie einen beliebigen festgelegten Text ein, den das System bei Nachrichten, die an Pager gesendet werden, am Anfang der Zeile **Cc** verlangt.  
  
**Pager**  
Enthält die E-Mail-Adresse der Nachricht zwischen Präfix und Suffix.  
  
**Suffix**  
Geben Sie einen beliebigen festgelegten Text ein, den das Pagingsystem bei Nachrichten, die an Pager gesendet werden, am Ende der Zeile **Cc** verlangt.  
  
**Betreff**  
Bestimmt die Optionen für den Betreff der Nachricht.  
  
**Prfix**  
Geben Sie einen beliebigen festgelegten Text ein, den das Pagingsystem bei Nachrichten, die an Pager gesendet werden, am Anfang der Zeile **Betreff** verlangt.  
  
**Suffix**  
Geben Sie einen beliebigen festgelegten Text ein, den das Pagingsystem bei Nachrichten, die an Pager gesendet werden, am Ende der Zeile **Betreff** verlangt.  
  
**E-Mail-Textkörper in Benachrichtigungsmeldung einschließen**  
Schließt den Textkörper der E-Mail-Nachricht in die an den Pager versendete Nachricht ein.  
  
**Ausfallsicherheitsoperator**  
In diesem Abschnitt können Sie die Optionen für den Ausfallsicherheitsoperator angeben.  
  
**Ausfallsicherheitsoperator aktivieren**  
Legt einen Ausfallsicherheitsoperator fest.  
  
**Operator**  
Legt den Namen des Operators fest, der die Ausfallsicherheitsbenachrichtigungen empfängt.  
  
**Benachrichtigen durch**  
Legt die Methode zur Benachrichtigung des Ausfallsicherheitsoperators fest.  
  
**Tokenersetzung**  
In diesem Abschnitt können Sie Tokens für Auftragsschritte aktivieren, die in von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Warnungen ausgeführten Aufträgen verwendet werden können. Weitere Informationen zu Auftragsschritttokens finden Sie unter [Verwenden von Token in Auftragsschritten](../../ssms/agent/use-tokens-in-job-steps.md).  
  
> [!IMPORTANT]  
> Jeder Windows-Benutzer mit Schreibberechtigungen für das Windows-Ereignisprotokoll hat u. U. die Möglichkeit, auf Auftragsschritte zuzugreifen, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Warnungen aktiviert werden. Zur Vermeidung dieses Sicherheitsrisikos sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Tokens, die in von Warnungen aktivierten Aufträgen verwendet werden können, standardmäßig deaktiviert. Hierbei handelt es sich um folgende Token: **$(A-DBN)**, **$(A-SVR)**, **$(A-ERR)**, **$(A-SEV)**und **$(A-MSG)**.  
>   
> Wenn Sie diese Tokens verwenden müssen, können Sie sie aktivieren. Stellen Sie zuvor jedoch sicher, dass nur Mitglieder von vertrauenswürdigen Windows-Sicherheitsgruppen, wie z. B. die Gruppe Administratoren, über Schreibberechtigungen für das Ereignisprotokoll des Computers verfügen, auf dem sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] befindet.  
  
**Token für alle Auftragsantworten auf Warnungen ersetzen**  
Aktivieren Sie dieses Kontrollkästchen, um die Tokenersetzung für Aufträge zu aktivieren, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Warnungen aktiviert werden.  
  
## <a name="see-also"></a>Siehe auch  
[Operatoren](../../ssms/agent/operators.md)  
[Konfigurieren von SQL Server-Agent-Mail zum Verwenden von Datenbank-E-Mails](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
[Datenbank-E-Mail](http://msdn.microsoft.com/en-us/9e4563dd-4799-4b32-a78a-048ea44a44c1)  
  

