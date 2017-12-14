---
title: "Festlegen des Einzelbenutzermodus für eine Datenbank | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: single-user mode [SQL Server], database option
ms.assetid: fb5254eb-b635-4b39-8361-136fd36f2b1f
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ef9771cb0d6bdf63ddc51602f316f7cf3081e118
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="set-a-database-to-single-user-mode"></a>Festlegen des Einzelbenutzermodus für eine Datenbank
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie für eine benutzerdefinierte Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] der Einzelbenutzermodus festgelegt wird. Der Einzelbenutzermodus gibt an, dass jeweils nur ein Benutzer auf die Datenbank zugreifen kann. Er wird im Allgemeinen für Wartungsaktionen verwendet.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **So legen Sie den Einzelbenutzermodus für eine Datenbank fest mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn zu dem Zeitpunkt, an dem Sie den Einzelbenutzermodus für die Datenbank festlegen, andere Benutzer mit der Datenbank verbunden sind, werden ihre Verbindungen mit der Datenbank ohne Warnung geschlossen.  
  
-   Die Datenbank verbleibt im Einzelbenutzermodus, selbst wenn sich der Benutzer, der die Option festgelegt hat, abmeldet. Dadurch kann ein anderer Benutzer (aber nur einer) eine Verbindung mit der Datenbank herstellen.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Bevor Sie die Datenbank auf SINGLE_USER festlegen, müssen Sie überprüfen, ob die AUTO_UPDATE_STATISTICS_ASYNC-Option auf OFF festgelegt ist. Wenn diese Option auf ON festgelegt ist, stellt der Hintergrundthread, der zum Aktualisieren von Statistiken verwendet wird, eine Verbindung mit der Datenbank her, und Sie können im Einzelbenutzermodus nicht auf die Datenbank zugreifen. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>So legen Sie den Einzelbenutzermodus für eine Datenbank fest  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf die zu ändernde Datenbank, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Datenbankeigenschaften** auf die Seite **Optionen** .  
  
4.  Wählen Sie unter der Option **Zugriff beschränken** den Eintrag **Single**aus.  
  
5.  Wenn andere Benutzer mit der Datenbank verbunden sind, wird die Meldung **Geöffnete Verbindungen** angezeigt. Klicken Sie zum Ändern der Eigenschaft und Schließen aller anderen Verbindungen auf **Ja**.  
  
 Mit dieser Prozedur können Sie für die Datenbank auch einen Mehrbenutzer- oder beschränkten Zugriff festlegen. Weitere Informationen zu den Optionen von „Zugriff beschränken“ finden Sie unter [Datenbankeigenschaften &#40;Seite Optionen&#41;](../../relational-databases/databases/database-properties-options-page.md).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>So legen Sie den Einzelbenutzermodus für eine Datenbank fest  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die Datenbank auf den `SINGLE_USER` -Modus festgelegt, um exklusiven Zugriff zu erhalten. Anschließend wird in dem Beispiel der Status der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank auf `READ_ONLY` festgelegt und der Zugriff auf die Datenbank an alle Benutzer zurückgegeben. Die Beendigungsoption `WITH ROLLBACK IMMEDIATE` wird in der ersten `ALTER DATABASE` -Anweisung angegeben. Dies führt dazu, dass für alle unvollständigen Transaktionen ein Rollback ausgeführt wird und alle anderen Verbindungen zur [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank sofort getrennt werden.  
  
 [!code-sql[DatabaseDDL#AlterDatabase8](../../relational-databases/databases/codesnippet/tsql/set-a-database-to-single_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
