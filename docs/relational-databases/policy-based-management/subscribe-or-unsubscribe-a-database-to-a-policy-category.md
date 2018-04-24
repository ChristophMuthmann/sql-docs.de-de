---
title: Abonnieren einer Richtlinienkategorie für eine Datenbank bzw. Kündigen des Abonnements | Microsoft Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.dmf.groupsubscription.f1
ms.assetid: d2c31769-7098-428e-ad9c-ef56541b7c52
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cbdd1525345522289bc2714191d96f10a1fb99dd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="subscribe-or-unsubscribe-a-database--to-a-policy-category"></a>Abonnieren einer Richtlinienkategorie für eine Datenbank bzw. Kündigen des Abonnements
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Richtlinienkategorie für eine Datenbank in [!INCLUDE[tsql](../../includes/tsql-md.md)]abonniert bzw. das Abonnement gekündigt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **Abonnieren einer Richtlinienkategorie für eine Datenbank bzw. Kündigen des Abonnements mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle "db_owner".  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-subscribe-or-unsubscribe-a-database-to-a-policy-category"></a>So abonnieren Sie eine Richtlinienkategorie für eine Datenbank bzw. kündigen das Abonnement  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, der die Datenbank enthält, in der Sie Kategorieabonnements verwalten möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Datenbanken** zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, in der Sie Kategorieabonnements verwalten möchten, zeigen Sie auf **Richtlinien**, und wählen Sie **Kategorien**aus.  
  
     Die folgenden Optionen sind im Dialogfeld **Kategorien** verfügbar:  
  
     Spalte erweitern  
     Klicken Sie, um eine Richtlinienkategorie zu erweitern. Dadurch werden alle in der Kategorie enthaltenen Richtlinien aufgelistet.  
  
     **Name**  
     Der Name der Richtlinienkategorie.  
  
     **Abonniert**  
     Gibt an, ob das Ziel die Richtlinienkategorie abonniert hat. Wenn dieses Kontrollkästchen deaktiviert ist, wird die Richtlinienkategorie für **Datenbankabonnements beauftragen**festgelegt. Dies bedeutet, dass die Richtlinienkategorie für alle Datenbanken auf dem Server gilt.  
  
     **Richtlinie**  
     Wenn Richtliniengruppen erweitert werden, werden die Richtlinien in der Richtlinienkategorie angezeigt.  
  
     **Enabled**  
     Gibt an, ob die Richtlinien aktiviert oder deaktiviert sind.  
  
     **Ausführungsmodus**  
     Zeigt den Ausführungsmodus der Richtlinie an.  
  
     **Verlauf**  
     Klicken Sie auf den Link Verlauf anzeigen, um den Protokolldatei-Viewer zu öffnen und den Richtlinienverlauf anzuzeigen.  
  
4.  Um eine Kategorie der richtlinienbasierten Verwaltung zu abonnieren, aktivieren Sie das Kontrollkästchen der Kategorie unter der Spalte **Abonniert** . Um das Abonnement einer Kategorie zu kündigen, deaktivieren Sie das Kontrollkästchen.  
  
5.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-subscribe-a-database-to-a-policy-category"></a>So abonnieren Sie eine Richtlinienkategorie für eine Datenbank  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    -- Adds a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sp_syspolicy_subscribe_to_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql.md).  
  
#### <a name="to-unsubscribe-a-database-to-a-policy-category"></a>So kündigen Sie das Abonnement einer Richtlinienkategorie für eine Datenbank  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    -- Deletes a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md).  
  
  
