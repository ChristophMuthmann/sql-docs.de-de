---
title: "Anzeigen oder Konfigurieren der Serverkonfigurationsoption „Standardeinstellung für die Sicherungskomprimierung“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], backup compression default option
- backup compression [SQL Server], backup compression default Option
ms.assetid: 23029395-3e93-4c29-b7d6-e5a47a3526ff
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a6cbf2bc726dce79d1076ff7b2c1f2606c9b951e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="view-or-configure-the-backup-compression-default-server-configuration-option"></a>Anzeigen oder Konfigurieren der Serverkonfigurationsoption Standardeinstellung für die Sicherungskomprimierung
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **backup compression default** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]angezeigt oder konfiguriert wird. Mit der Option **backup compression default** wird bestimmt, ob die Serverinstanz standardmäßig komprimierte Sicherungen erstellt. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist, ist die Option **backup compression default** deaktiviert.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So zeigen Sie die Option backup compression default an und konfigurieren sie mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option „Komprimierungsstandard für Sicherung“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Sicherungskomprimierung ist nicht in allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Weitere Informationen finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   Standardmäßig steigt die CPU-Nutzung durch die Komprimierung erheblich, und die bei der Komprimierung zusätzlich verbrauchten CPU-Ressourcen können sich negativ auf gleichzeitige Vorgänge auswirken. Daher ist es u. U. sinnvoll, in einer Sitzung, bei der die CPU-Nutzung durch die [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md) eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen. Weitere Informationen finden Sie unter [Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn Sie eine einzelne Sicherung, eine Protokollversandkonfiguration oder einen Wartungsplan erstellen, können Sie die Standardeinstellung auf Serverebene überschreiben.  
  
-   Die Komprimierung von Sicherungen wird sowohl bei Datenträgersicherungsmedien als auch bei Bandsicherungsgeräten unterstützt.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-view-or-configure-the-backup-compression-default-option"></a>So zeigen Sie die Option 'backup compression default' an und konfigurieren sie  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den Knoten **Datenbankeinstellungen** .  
  
3.  Unter **Sichern und Wiederherstellen**wird für **Sicherung komprimieren** die aktuelle Einstellung der Option **backup compression default** angezeigt. Durch diese Einstellung wird die Standardeinstellung für die Sicherungskomprimierung auf Serverebene wie folgt festgelegt:  
  
    -   Wenn das Feld **Sicherung komprimieren** leer ist, werden neue Sicherungen nicht komprimiert.  
  
    -   Wenn das Kontrollkästchen **Sicherung komprimieren** aktiviert ist, werden neue Sicherungen standardmäßig komprimiert.  
  
     Wenn Sie Mitglied der festen Serverrolle **sysadmin** bzw. **serveradmin** sind, können Sie die Standardeinstellung auch durch Klicken auf das Kontrollkästchen **Sicherung komprimieren** ändern.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-view-the-backup-compression-default-option"></a>So zeigen Sie die Option backup compression default an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die Katalogsicht [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) abgefragt, um den Wert für `backup compression default`zu bestimmen. Der Wert 0 bedeutet, dass die Sicherungskomprimierung deaktiviert ist, und der Wert 1 bedeutet, dass die Sicherungskomprimierung aktiviert ist.  
  
```tsql  
SELECT value   
FROM sys.configurations   
WHERE name = 'backup compression default' ;  
GO  
```  
  
#### <a name="to-configure-the-backup-compression-default-option"></a>So konfigurieren Sie die Option backup compression default  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie die Serverinstanz mithilfe von [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) so konfiguriert wird, dass standardmäßig komprimierte Sicherungen erstellt werden.  
  
```tsql  
EXEC sp_configure 'backup compression default', 1 ;  
RECONFIGURE WITH OVERRIDE ;  
GO 
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)angezeigt oder konfiguriert wird.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option backup compression default  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  


