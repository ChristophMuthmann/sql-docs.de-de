---
title: Erstellen von Anmeldeinformationen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- credentials [SQL Server], creating
- authentication [SQL Server], credentials
- logins [SQL Server], credentials
ms.assetid: c1e77e91-2a69-40d9-b8b3-97cffc710586
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 80dba3f156735179c0fb016e39f3065acd6f5ac1
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-credential"></a>Erstellen von Anmeldeinformationen
  In diesem Thema wird beschrieben, wie Anmeldeinformationen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]erstellt werden.  
  
 Anmeldeinformationen ermöglichen Benutzern der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung eine Identität außerhalb von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Hauptsächlich wird dies für die Ausführung von Code in Assemblys mit dem Berechtigungssatz EXTERNAL_ACCESS verwendet. Anmeldeinformationen können auch verwendet werden, wenn ein Benutzer der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung Zugriff auf eine Domänenressource (z. B. auf einen Dateispeicherort zum Speichern einer Sicherung) benötigt.  
  
 Anmeldeinformationen können verschiedenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldungen gleichzeitig zugeordnet werden. Eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung kann nur einer Anmeldeinformation zugeordnet werden. Verwenden Sie nach dem Erstellen einer Anmeldeinformation das Dialogfeld **Anmeldungseigenschaften (Seite „Allgemein“)** , um einer Anmeldung eine Anmeldeinformation zuzuordnen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **Erstellen von Anmeldeinformationen mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Falls für den Anbieter kein mit einem Anmeldenamen verknüpfter Identitätsnachweis vorliegt, werden die dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonto zugeordneten Anmeldeinformationen verwendet.  
  
-   Einem Anmeldenamen können mehrere Anmeldeinformationen zugeordnet werden, solange sie für unterschiedliche Anbieter verwendet werden. Pro Anbieter und Anmeldung darf es jedoch nur einen zugeordneten Identitätsnachweis geben. Die gleichen Anmeldeinformationen können jedoch auch anderen Anmeldenamen zugeordnet werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Zum Erstellen oder Ändern von Anmeldeinformationen ist eine ALTER ANY CREDENTIAL-Berechtigung erforderlich. Damit eine Anmeldung Anmeldeinformationen zugeordnet werden kann, ist die ALTER ANY LOGIN-Berechtigung erforderlich.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-create-a-credential"></a>Erstellen von Anmeldeinformationen  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner **Sicherheit** .  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Anmeldeinformationen** , und wählen Sie **Neue Anmeldeinformationen**aus.  
  
3.  Geben Sie im Dialogfeld **Neue Anmeldeinformationen** im Feld **Anmeldungsname** einen Namen für die Anmeldeinformationen ein.  
  
4.  Geben Sie im Feld **Identität** den Namen des für ausgehende Verbindungen verwendeten Kontos ein (das beim Verlassen des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Kontexts verwendet wird). In der Regel ist dies ein Windows-Benutzerkonto, aber die Identität kann ein Konto eines anderen Typs sein.  
  
     Klicken Sie alternativ auf die Auslassungspunkte **(…)** , um das Dialogfeld **Benutzer oder Gruppe auswählen** zu öffnen.  
  
5.  Geben Sie in den Feldern **Kennwort** und **Kennwort bestätigen** das Kennwort für das im Feld **Identität** festgelegte Konto ein. Falls **Identität** ein Windows-Benutzerkonto ist, handelt es sich dabei um das Windows-Kennwort. Falls kein Kennwort erforderlich ist, können Sie das Feld **Kennwort** leer lassen.  
  
6.  Wählen Sie **Verschlüsselungsanbieter verwenden** aus, um festzulegen, dass die Anmeldeinformationen von einem Anbieter für die erweiterbare Schlüsselverwaltung (Extensible Key Management, EKM) überprüft werden. Weitere Informationen über die erweiterbare Schlüsselverwaltung finden Sie unter [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-credential"></a>Erstellen von Anmeldeinformationen  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Creates the credential called "AlterEgo.".   
    -- The credential contains the Windows user "Mary5" and a password.  
    CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
        SECRET = '<EnterStrongPasswordHere>';  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md).  
  
  
