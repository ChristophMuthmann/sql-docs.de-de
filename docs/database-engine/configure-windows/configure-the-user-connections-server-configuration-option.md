---
title: "Konfigurieren der Serverkonfigurationsoption „Benutzerverbindungen“ | Microsoft-Dokumentation"
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
- simultaneous connections [SQL Server]
- user connections option [SQL Server]
- users [SQL Server], simultaneous connections
- maximum number of simultaneous user connections
- connections [SQL Server], simultaneous
ms.assetid: 53beee6e-59fe-4276-9abb-8f1cec2a3508
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 64d4e5e4e8cf6a2c278c9c7dc51443a28eaeedcf
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="configure-the-user-connections-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Benutzerverbindungen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Benutzerverbindungen** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]festgelegt wird. Die Option **Benutzerverbindungen** gibt die maximale Anzahl gleichzeitiger Benutzerverbindungen an, die für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zulässig sind. Die tatsächliche Anzahl von zulässigen Benutzerverbindungen ist auch abhängig von der verwendeten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sowie von den Einschränkungen der Anwendung bzw. Anwendungen und der Hardware. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lässt maximal 32.767 Benutzerverbindungen zu. Da **Benutzerverbindungen** eine dynamische (selbstkonfigurierende) Option ist, passt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die maximale Anzahl der Benutzerverbindungen automatisch nach Bedarf bis zum zulässigen Höchstwert an. Wenn beispielsweise nur 10 Benutzer angemeldet sind, werden 10 Benutzerverbindungsobjekte reserviert. In den meisten Fällen ist es nicht erforderlich, dass Sie den Wert für diese Option ändern. Der Standardwert ist null (0), womit die maximale Anzahl (32.767) Benutzerverbindungen zulässig ist.  
  
 Um die maximale Anzahl von Benutzerverbindungen zu bestimmen, die im System zulässig sind, können Sie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) ausführen oder die Katalogsicht [sys.configuration](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) abfragen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Option Benutzerverbindungen mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option Benutzerverbindungen](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Techniker geändert werden.  
  
-   Durch die Option **Benutzerverbindungen** kann eine Überlastung des Servers durch zu viele gleichzeitige Verbindungen vermieden werden. Sie können die Anzahl der Verbindungen anhand der System- und Benutzeranforderungen schätzen. So ist es beispielsweise bei einem System mit vielen Benutzern nicht notwendig, dass jeder Benutzer über eine eindeutige Verbindung verfügt. Verbindungen können von Benutzern gemeinsam genutzt werden. Benutzer, die OLE DB-Anwendungen ausführen, benötigen eine Verbindung für jedes geöffnete Verbindungsobjekt. Benutzer, die ODBC-Anwendungen (Open Database Connectivity) ausführen, benötigen eine Verbindung für jedes aktive Verbindungshandle in der Anwendung. Benutzer, die DB-Library-Anwendungen ausführen, benötigen eine Verbindung für jeden gestarteten Prozess, der die **dbopen** -Funktion von DB-Library aufruft.  
  
    > [!IMPORTANT]  
    >  Wenn Sie diese Option verwenden müssen, sollten Sie den Wert nicht zu hoch festlegen, da jede Verbindung Aufwand benötigt, unabhängig davon, ob die Verbindung tatsächlich verwendet wird. Wenn Sie die maximale Anzahl der Benutzerverbindungen überschreiten, erhalten Sie eine Fehlermeldung und können erst eine neue Verbindung herstellen, wenn eine andere Verbindung verfügbar wird.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-configure-the-user-connections-option"></a>So konfigurieren Sie die Option Benutzerverbindungen  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Klicken Sie auf den Knoten **Verbindungen** .  
  
3.  Geben Sie unter **Verbindungen**im Feld **Maximum der gleichzeitigen Benutzerverbindungen** einen Wert zwischen 0 und 32.767 ein, oder wählen Sie einen Wert aus, um für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die maximale Anzahl gleichzeitig zulässiger Benutzerverbindungen festzulegen.  
  
4.  Starten Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-user-connections-option"></a>So konfigurieren Sie die Option Benutzerverbindungen  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `user connections` auf `325` Benutzer festzulegen.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'user connections', 325 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)festgelegt wird.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Benutzerverbindungen  
 Der Server muss neu gestartet werden, bevor die Einstellung wirksam werden kann.  
  
## <a name="see-also"></a>Siehe auch  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

