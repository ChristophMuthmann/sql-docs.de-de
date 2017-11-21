---
title: Erstellen eines Datenbankbenutzers | Microsoft Docs
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.user.securables.f1
- SQL13.SWB.DATABASEUSER.GENERAL.F1
helpviewer_keywords:
- database users, creating
- creating users with Management Studio
- mapping users
- users [SQL Server], creating
- database user additions [SQL Server]
- database users, mapping
- CREATE USER [Management Studio]
- users [SQL Server], adding
- mapping database users
ms.assetid: 782798d3-9552-4514-9f58-e87be4b264e4
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.openlocfilehash: 3459cbe5b6e141af32ba7e8f29f0da6e3a34819d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-database-user"></a>Erstellen eines Datenbankbenutzers
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  In diesem Thema wird beschrieben, wie Sie die am weitesten verbreiteten Typen von Datenbankbenutzern erstellen. Es gibt elf Typen von Benutzern. Eine vollständige Liste finden Sie im Thema [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md). Alle Ausführungen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützen Datenbankbenutzer, aber nicht unbedingt alle Benutzertypen.  
  
 Sie können einen Datenbankbenutzer erstellen, entweder mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
##  <a name="Understanding"></a> Grundlegendes zu den Benutzertypen  
 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] bietet sechs Optionen für die Erstellung eines Datenbankbenutzers. Die folgenden Grafik zeigt die sechs Optionen im grünen Kasten, und gibt an, wofür sie stehen.  
  
 ![TypesOfUsers](../../../relational-databases/security/authentication-access/media/typesofusers.png "TypesOfUsers")  
  
### <a name="selecting-the-type-of-user"></a>Auswählen des Benutzertypen  
 **Anmeldenamen oder Benutzer, der keinem Anmeldenamen zugeordnet ist**  
  
 Falls [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]für Sie neu ist, kann es schwer sein, festzustellen, was für einen Benutzertyp Sie erstellen wollen. Fragen Sie sich zunächst, ob die Person oder Gruppe, die Zugriff auf die Datenbank benötigt, über einen Anmeldenamen verfügt. Anmeldenamen in der Masterdatenbank sind weit verbreitet für die Personen, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwalten und für Personen, die Zugriff auf viele oder alle Datenbanken auf der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]benötigen. Für diese Situation erstellen Sie einen **SQL-Benutzer mit Anmeldename**. Der Datenbankbenutzer ist die Identität der Anmeldung, wenn er mit einer Datenbank verbunden ist. Der Datenbankbenutzer kann den gleichen Namen verwenden wie die Anmeldung, dies ist jedoch nicht erforderlich. In diesem Thema wird davon ausgegangen, dass in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]bereits eine Anmeldung vorhanden ist. Informationen zum Erstellen eines Anmeldenamens finden Sie unter [Erstellen eines Anmeldenamens](../../../relational-databases/security/authentication-access/create-a-login.md).  
  
 Erstellen Sie einen **Windows-Benutzer** oder einen **SQL-Benutzer mit Kennwort**, falls die Person oder Gruppe, die Zugriff auf die Datenbank benötigt, über keinen Anmeldenamen verfügt, und wenn sie nur Zugriff auf eine oder einige wenige Datenbanken benötigen. Auch als eigenständiger Datenbankbenutzer bezeichnet, ist er keinem Anmeldenamen in der Masterdatenbank zugeordnet. Das ist eine hervorragende Wahl, wenn Sie die Möglichkeit haben möchten, Ihre Datenbank einfach zwischen Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu verschieben. Um diese Option in [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]verwenden zu können, muss ein Administrator zunächst eigenständige Datenbanken für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]aktivieren, und die Datenbanken müssen für die Verwendung dieser Funktion aktiviert sein. Weitere Informationen finden Sie unter [Eigenständige Datenbankbenutzer – machen Sie Ihre Datenbank portabel](../../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
> **WICHTIG!** Beim Herstellen einer Verbindung als ein eigenständigen Datenbankbenutzer, müssen Sie den Namen der Datenbank als Teil der Verbindungszeichenfolge bereitstellen. Klicken Sie im Dialogfeld [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]Verbinden mit **auf** Optionen **, und klicken Sie dann auf die Registerkarte**Verbindungseigenschaften **, um die Datenbank in** anzugeben.  
  
 Wählen Sie **SQL-Benutzer mit Kennwort** oder einen **SQL-Benutzer mit Anmeldename** basierend auf einer **SQL Server-Authentifizierungsanmeldung**aus, wenn die Person, die die Verbindung herstellt, keine Authentifizierung mit Windows ausführen kann. Dies ist häufig der Fall, wenn Personen außerhalb Ihrer Organisation (z.B. Kunden) sich mit Ihrem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verbinden.  
  
> **TIPP:** Für Personen innerhalb Ihrer Organisation ist die Windows-Authentifizierung eine bessere Wahl, da sie sich kein zusätzliches Kennwort merken müssen, und weil die Windows-Authentifizierung zusätzliche Sicherheitsfeatures, wie z.B. Kerberos bietet.  
  
##  <a name="Restrictions"></a> Hintergrund  
 Ein Benutzer ist ein Sicherheitsprinzipal auf Datenbankebene. Anmeldungen müssen einem Datenbankbenutzer zugeordnet werden, damit eine Verbindung zu einer Datenbank hergestellt werden kann. Eine Anmeldung kann unterschiedlichen Datenbanken als unterschiedliche Benutzer zugeordnet werden, aber kann nur als ein Benutzer in jeder Datenbank zugeordnet werden. In einer teilweise eigenständigen Datenbank kann ein Benutzer erstellt werden, der über keinen Anmeldenamen verfügt. Weitere Informationen zu eigenständigen Datenbankbenutzern finden Sie unter [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md). Wenn in einer Datenbank Gastbenutzer aktiviert sind, kann eine Anmeldung, die keinem Datenbankbenutzer zugeordnet ist, als Gastbenutzer auf die Datenbank zugreifen.  
  
> **WICHTIG!** Gastbenutzer sind normalerweise deaktiviert. Aktivieren Sie Gastbenutzer nur, wenn es notwendig ist.  
  
 Als Sicherheitsprinzipalen können Benutzern Berechtigungen gewährt werden. Die Datenbank ist der Bereich eines Benutzers. Um eine bestimmte Datenbank mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu verbinden, muss ein Anmeldename einem Datenbankbenutzer zugeordnet werden. Die Berechtigungen innerhalb der Datenbank werden dem Datenbankbenutzer, nicht dem Anmeldenamen, gewährt bzw. verweigert.  
  
##  <a name="Permissions"></a> Berechtigungen  
 Erfordert die **ALTER ANY USER** -Berechtigung in der Datenbank.  
  
##  <a name="SSMSProcedure"></a> Erstellen eines Benutzers ohne Kennwort  
  
 
1.  Erweitern Sie im Objekt-Explorer den Ordner **Datenbanken** .  
  
2.  Erweitern Sie die Datenbank, in der der neue Datenbankbenutzer erstellt werden soll.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Sicherheit** , zeigen Sie auf **Neu**, und klicken Sie dann auf **Benutzer**.  
  
4.  Wählen Sie im Dialogfeld **Datenbankbenutzer – Neu** auf der Seite **Allgemein** einen der folgenden Benutzertypen aus der Liste **Benutzertyp** aus:  
  
    -   **SQL-Benutzer mit Anmeldename**  
  
    -   **SQL-Benutzer mit Kennwort**  
  
    -   **SQL-Benutzer ohne Anmeldename**  
  
    -   **Benutzer der einem Zertifikat zugeordnet ist**  
  
    -   **Benutzer, der einem asymmetrischen Schlüssel zugeordnet ist**  
  
    -   **Windows-Benutzer**  
  
5.  Wenn Sie eine Option auswählen, ändern sich möglicherweise die verbleibenden Optionen im Dialog. Einige Optionen gelten nur für bestimmte Typen von Datenbankbenutzer. Einige Optionen können leer gelassen werden und verwenden dann einen Standardwert.  
  
     **Benutzername**  
     Geben Sie einen Namen für den Benutzer ein. Wenn Sie **Windows-Benutzer** aus der Liste **Benutzertyp** ausgewählt haben, können Sie zudem auf die Auslassungszeichen **(…)** klicken, um das Dialogfeld **Benutzer oder Gruppe auswählen** zu öffnen.  
  
     **Anmeldename**  
     Geben Sie den Anmeldenamen des Benutzers ein. Klicken Sie alternativ auf die Auslassungspunkte **(…)** , um das Dialogfeld **Anmeldenamen auswählen** zu öffnen. **Anmeldename** ist verfügbar, wenn Sie entweder **SQL-Benutzer mit Anmeldename** oder **Windows-Benutzer** aus der Liste **Benutzertyp** auswählen.  
  
     **Kennwort** und **Kennwort bestätigen**  
     Geben Sie für Benutzer, die sich an der Datenbank authentifizieren, ein Kennwort ein.  
  
     **Standardsprache**  
     Geben Sie die Standardsprache des Benutzers ein.  
  
     **Standardschema**  
     Geben Sie das Schema ein, das die Objekte besitzen wird, die von diesem Benutzer erstellt werden. Klicken Sie alternativ auf die Auslassungspunkte **(…)** , um das Dialogfeld **Schema auswählen** zu öffnen. **Standardschema** ist verfügbar, wenn Sie entweder **SQL-Benutzer mit Anmeldename**, **SQL-Benutzer ohne Anmeldename**oder **Windows-Benutzer** aus der Liste **Benutzertyp** auswählen.  
  
     **Zertifikatsname**  
     Geben Sie das Zertifikat ein, das für den Datenbankbenutzer verwendet werden soll. Klicken Sie alternativ auf die Auslassungspunkte **(…)** , um das Dialogfeld **Zertifikat auswählen** zu öffnen. **Zertifikatname** ist verfügbar, wenn Sie die Option **Benutzer, der einem Zertifikat zugeordnet ist** aus der Liste **Benutzertyp** auswählen.  
  
     **Name des asymmetrischen Schlüssels**  
     Geben Sie den Schlüssel ein, der für den Datenbankbenutzer benutzt werden soll. Klicken Sie alternativ auf die Auslassungspunkte **(…)** , um das Dialogfeld **Asymmetrischen Schlüssel auswählen** zu öffnen. Die Option für den **asymmetrischen Schlüsselnamen** ist verfügbar, wenn Sie die Option **Benutzer, der einem asymmetrischen Schlüssel zugeordnet ist** aus der Liste **Benutzertyp** auswählen.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Zusätzliche Optionen  
 Im Dialogfeld **Datenbankbenutzer - Neu** sind auch Optionen auf vier zusätzlichen Seiten verfügbar: **Schemas im Besitz**, **Mitgliedschaft**, **Sicherungsfähige Elemente**und **Erweiterte Eigenschaften**.  
  
-   Auf der Seite **Schemas im Besitz** werden alle möglichen Schemas aufgelistet, die dem neuen Datenbankbenutzer gehören können. Aktivieren oder deaktivieren Sie unter **Schemas im Besitz dieses Benutzers**die Kontrollkästchen, die sich neben den Schemas befinden, um einem Datenbankbenutzer Schemas hinzuzufügen oder diese von diesem zu entfernen.  
  
-   Auf der Seite **Mitgliedschaft** werden alle möglichen Datenbank-Mitgliedschaftsrollen aufgelistet, die dem neuen Datenbankbenutzer gehören können. Aktivieren oder deaktivieren Sie unter **Mitgliedschaft in Datenbankrolle**die Kontrollkästchen, die sich neben den Rollen befinden, um einem Datenbankbenutzer Rollen hinzuzufügen oder diese von diesem zu entfernen.  
  
-   Auf der Seite **Sicherungsfähige Elemente** werden alle möglichen sicherungsfähigen Elemente und die Berechtigungen für diese sicherungsfähigen Elemente aufgelistet, die für die Anmeldung gewährt werden können.  
  
-   Mithilfe der Seite **Erweiterte Eigenschaften** können Sie Datenbankbenutzern benutzerdefinierte Eigenschaften hinzufügen. Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     **Datenbank**  
     Zeigt den Namen der ausgewählten Datenbank an. Dieses Feld ist schreibgeschützt.  
  
     **Sortierung**  
     Zeigt die für die ausgewählte Datenbank verwendete Sortierung an. Dieses Feld ist schreibgeschützt.  
  
     **Eigenschaften**  
     Zeigt bzw. gibt die erweiterten Eigenschaften für das Objekt an. Jede erweiterte Eigenschaft besteht aus einem aus Name und Wert bestehenden Paar von Metadaten, das dem Objekt zugeordnet ist.  
  
     **Auslassungspunkte (…)**  
     Klicken Sie auf die Auslassungszeichen **(…)** hinter **Wert** , um das Dialogfeld **Wert für erweiterte Eigenschaft** zu öffnen. Geben Sie den Wert der erweiterten Eigenschaft an diesem größeren Speicherort ein, bzw. zeigen Sie ihn an. Weitere Informationen finden Sie unter [Wert für erweiterte Eigenschaft (Dialogfeld)](http://msdn.microsoft.com/library/ms189353.aspx).  
  
     **Delete**  
     Entfernt die ausgewählte erweiterte Eigenschaft.  
  
##  <a name="TsqlProcedure"></a> Erstellen eines Benutzers mit T-SQL  
    
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der **Standardleiste** auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Creates the login AbolrousHazem with password '340$Uuxwp7Mcxo7Khy'.  
    CREATE LOGIN AbolrousHazem   
        WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
    GO  
  
    -- Creates a database user for the login created above.  
    CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md) Dort finden Sie weitere [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Beispiele.  
  
## <a name="see-also"></a>Siehe auch  
 [Prinzipale &#40;Datenbankmodul&#41;](../../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Erstellen eines Anmeldenamens](../../../relational-databases/security/authentication-access/create-a-login.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
  
