---
title: Operatoren | Microsoft-Dokumentation
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
- operators (users) [Database Engine]
- fail-safe operator [SQL Server]
- aliases [SQL Server], operators
- SQL Server Agent alerts, operators
- contact information [SQL Server Agent]
- net send [SQL Server]
- e-mail [SQL Server], SQL Server Agent operators
- pager notifications [SQL Server Agent]
- mail [SQL Server], SQL Server Agent operators
- operators (users) [Database Engine], defining
- jobs [SQL Server Agent], operators
- alerts [SQL Server], operators
ms.assetid: 38e8488f-2669-4cea-b9c3-5f394a663678
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d3c06760deff418bc01b128b3568cb38b6c77093
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="operators"></a>Operatoren
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Operatoren sind Aliasnamen für Personen oder Gruppen, die elektronische Benachrichtigungen erhalten können, sobald ein Auftrag abgeschlossen oder eine Warnung ausgelöst wird. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst unterstützt die Benachrichtigung der Administratoren durch Operatoren. Durch Operatoren werden Benachrichtigungs- und Überwachungsfunktionen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents aktiviert.  
  
## <a name="operator-attributes-and-concepts"></a>Operatorattribute und -konzepte  
Für Operatoren gelten die folgenden Hauptattribute:  
  
-   Operatorname  
  
-   Kontaktinformationen  
  
### <a name="naming-an-operator"></a>Benennen eines Operators  
Jeder Operator muss einen Namen aufweisen. Operatornamen müssen innerhalb der jeweiligen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eindeutig sein und dürfen nicht länger als **128** Zeichen lang sein.  
  
### <a name="contact-information"></a>Kontaktinformationen  
Die Kontaktinformationen eines Operators definieren, wie der Operator benachrichtigt wird. Operatoren können per E-Mail, per Pager oder über den Befehl **net send** benachrichtigt werden:  
  
> [!IMPORTANT]  
> Die Pager- und **net send** -Optionen werden in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nicht mehr im [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktionen zurzeit verwenden.  
  
-   **E-Mail-Benachrichtigung**  
  
    Der Operator wird per E-Mail benachrichtigt. Für die E-Mail-Benachrichtigung geben Sie die E-Mail-Adresse des Operators an.  
  
-   **Pagerbenachrichtigung**  
  
    Die Pagingfunktionen werden mithilfe von E-Mail implementiert. Für die Pagerbenachrichtigung geben Sie die E-Mail-Adresse an, unter der der Operator die Pagernachrichten empfängt. Zum Einrichten der Pagerbenachrichtigung müssen Sie Software auf dem Mailserver installieren, auf dem eingehende E-Mails verarbeitet und in eine Pagernachricht konvertiert werden. Mit der Software können unterschiedliche Methoden genutzt werden:  
  
    -   Weiterleiten der E-Mail an einen Remotemailserver am Standort des Pageranbieters.  
  
        Der Pageranbieter muss diesen Dienst anbieten, obwohl die erforderliche Software gewöhnlich als Teil des lokalen Mailsystems zur Verfügung steht. Weitere Informationen finden Sie in der Pager-Dokumentation.  
  
    -   Weiterleiten der E-Mail über das Internet an einen Mailserver am Standort des Pageranbieters.  
  
        Es handelt sich hierbei um eine Variation der ersten Methode.  
  
    -   Verarbeiten der eingehenden E-Mail und Anwählen des Pagers mithilfe eines angeschlossenen Modems.  
  
        Diese Software wird vom Pagerdienstanbieter bereitgestellt. Die Software agiert als Mailclient, der den Inhalt des Posteingangs in regelmäßigen Abständen verarbeitet, indem entweder alle oder Teile der E-Mail-Adressinformationen als Pagernummern interpretiert werden oder indem E-Mail-Namen einer Pagernummer in einer Übersetzungstabelle zugeordnet werden.  
  
        Wenn der gleiche Pageranbieter für alle Operatoren freigegeben wird, können Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] spezielle E-Mail-Formatierungen angeben, die das Umwandlungssystem vom E-Mail-Format zum Pagerformat benötigt. Die spezielle Formatierung kann dabei aus einem Präfix oder einem Suffix bestehen und in die folgenden Zeilen der E-Mail eingefügt werden:  
  
        **Betreff:**  
  
        **Cc**:  
  
        **An**:  
  
    > [!NOTE]  
    > Bei Verwendung eines alphanumerischen Pagingsystems mit niedriger Kapazität können Sie den gesendeten Text kürzen, indem Sie den Fehlertext aus der Pagerbenachrichtigung ausschließen. Dies empfiehlt sich beispielsweise für Systeme, die auf 64 Zeichen pro Seite begrenzt sind.  
  
-   **net sendnotification**  
  
    Hiermit senden Sie dem Operator eine Nachricht über den Befehl **NET SEND** . Bei **NET SEND**geben Sie den Empfänger (Computer oder Benutzer) einer Netzwerknachricht an.  
  
    > [!NOTE]  
    > Der Befehl **NET SEND** greift auf Microsoft Windows Messenger zurück. Um Warnungen fehlerfrei senden zu können, muss dieser Service sowohl auf dem Computer ausgeführt werden, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgeführt wird, als auch auf dem Computer, den der Operator verwendet.  
  
## <a name="alerting-and-fail-safe-operators"></a>Warn- und Ausfallsicherheitsoperatoren  
Sie können die Operatoren auswählen, die als Reaktion auf eine Warnung benachrichtigt werden sollen. So können Sie beispielsweise die Zuständigkeiten bei der Operatorbenachrichtigung abwechselnd zuweisen, indem Sie Zeitpläne für Warnungen verwenden. Auf diese Weise wird z. B. Person A über Warnungen benachrichtigt, die am Montag, Mittwoch oder Freitag auftreten, und Person B ist für Warnungen am Dienstag, Donnerstag oder Samstag zuständig.  
  
Der Ausfallsicherheitsoperator erhält eine Warnung, nachdem alle Pagerbenachrichtigungen an die angegebenen Operatoren fehlgeschlagen sind. Wenn Sie beispielsweise drei Operatoren für die Pagerbenachrichtigungen definiert haben und keiner dieser Operatoren per Pager benachrichtigt werden kann, wird der Ausfallsicherheitsoperator benachrichtigt.  
  
Der Ausfallsicherheitsoperator wird in den folgenden Fällen benachrichtigt:  
  
-   Die für die Warnung verantwortlichen Operatoren können per Pager nicht benachrichtigt werden.  
  
    Die primären Operatoren sind nicht erreichbar, weil beispielsweise die Pageradresse fehlerhaft ist oder die betreffenden Operatoren möglicherweise gerade außer Dienst sind.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent kann nicht auf Systemtabellen in der **msdb** -Datenbank zugreifen.  
  
    In der **sysnotifications** -Systemtabelle werden die Aufgaben der Operatoren bei Warnungen angegeben.  
  
Der Ausfallsicherheitsoperator ist eine Sicherheitsfunktion. Sie können den Operator, dem der Ausfallsicherheitsdienst zugewiesen wurde, nicht löschen, ohne zuvor die Ausfallsicherheitsaufgabe einem anderen Operator zuzuweisen oder die Ausfallsicherheitszuweisung zu löschen.  
  
## <a name="notifying-an-operator"></a>Benachrichtigen eines Operators  
Sie müssen mindestens eines der folgenden Elemente einrichten, um einen Operator benachrichtigen zu können:  
  
-   Um E-Mails mit den Funktionen von Datenbank-E-Mail senden zu können, benötigen Sie den Zugriff auf einen E-Mail-Server, der SMTP unterstützt.  
  
-   Für Pagerbenachrichtigungen benötigen Sie Software für Pager-zu-E-Mail von Drittanbietern und/oder die entsprechende Hardware.  
  
-   Für den Befehl **NET SEND**muss der Bediener am angegebenen Computer angemeldet sein, und der angegebene Computer muss Nachrichten von Windows Messenger zulassen.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Aufgaben**|**Thema**|  
|Tasks beim Erstellen eines Operators|[Erstellen eines Operators](../../ssms/agent/create-an-operator.md)<br /><br />[Designate a Fail-Safe Operator](../../ssms/agent/designate-a-fail-safe-operator.md)|  
|Tasks beim Zuordnen von Warnungen|[Zuweisen von Warnungen zu einem Operator](../../ssms/agent/assign-alerts-to-an-operator.md)<br /><br />[Definieren der Antwort auf eine Warnung &#40;SQL Server Management Studio&#41;](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)<br /><br />[sp_add_notification (Transact-SQL)](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)<br /><br />[Zuweisen von Warnungen zu einem Operator](../../ssms/agent/assign-alerts-to-an-operator.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Datenbank-E-Mail](http://msdn.microsoft.com/en-us/9e4563dd-4799-4b32-a78a-048ea44a44c1)  
  
