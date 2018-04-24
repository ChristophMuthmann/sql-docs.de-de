---
title: Auswählen eines Authentifizierungsmodus | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ins.instwizard.authenticationmode.f1
- sql13.swb.passwordexpired.f1
helpviewer_keywords:
- sa account
- authentication modes
- trusted connection
- SQL Server Installation Wizard, Authentication Mode page
- choose authentication mode
- authentication [SQL Server], choosing a mode
- Windows authentication [SQL Server]
- mixed mode authentication
- mixed authentication mode
- SQL authentication mode
- Password Expired dialog box
ms.assetid: ff7a6a48-3d38-4209-aa0f-7d6c0a8c64ef
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: efed26ea51f00df312711083423bb86632a72544
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="choose-an-authentication-mode"></a>Auswählen eines Authentifizierungsmodus
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Während des Setups müssen Sie einen Authentifizierungsmodus für [!INCLUDE[ssDE](../../includes/ssde-md.md)]auswählen. Es gibt zwei mögliche Modi: den Windows-Authentifizierungsmodus und den gemischten Modus. Der Windows-Authentifizierungsmodus aktiviert die Windows-Authentifizierung und deaktiviert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung. Der gemischte Modus aktiviert sowohl die Windows-Authentifizierung als auch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung. Die Windows-Authentifizierung ist immer verfügbar und kann nicht deaktiviert werden.  
  
## <a name="configuring-the-authentication-mode"></a>Konfigurieren des Authentifizierungsmodus  
 Bei Auswahl der Authentifizierung im gemischten Modus während des Setups müssen Sie ein sicheres Kennwort für das vordefinierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministratorkonto mit der Bezeichnung sa angeben und dann bestätigen. Das sa-Konto stellt eine Verbindung mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung her.  
  
 Wenn Sie während des Setups Windows-Authentifizierung auswählen, erstellt Setup das sa-Konto für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung, die aber deaktiviert ist. Wenn Sie später zur Authentifizierung im gemischten Modus wechseln und das sa-Konto verwenden möchten, müssen Sie es aktivieren. Jedes Windows- oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto kann als Systemadministrator konfiguriert werden. Da das sa-Konto bekannt und oft das Ziel böswilliger Benutzer ist, aktivieren Sie das sa-Konto nur, wenn Ihre Anwendung dies erfordert. Legen Sie auf keinen Fall ein leeres oder unsicheres Kennwort für das sa-Konto fest. Informationen zum Wechseln vom Windows-Authentifizierungsmodus zur Authentifizierung im gemischten Modus und zum Verwenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung finden Sie unter [Ändern des Serverauthentifizierungsmodus](../../database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="connecting-through-windows-authentication"></a>Herstellen von Verbindungen mithilfe der Windows-Authentifizierung  
 Wenn ein Benutzer eine Verbindung über ein Windows-Benutzerkonto herstellt, überprüft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Kontonamen und Kennwort mithilfe des Tokens für den Windows-Prinzipal im Betriebssystem. Dies bedeutet, dass die Benutzeridentität von Windows bestätigt wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Sie nicht nach dem Kennwort gefragt, und es wird keine Identitätsüberprüfung ausgeführt. Die Windows-Authentifizierung ist der Standardauthentifizierungsmodus und bietet eine höhere Sicherheit als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung. Die Windows-Authentifizierung verwendet das Kerberos-Sicherheitsprotokoll, stellt Maßnahmen zur Durchsetzung von Kennwortrichtlinien, z. B. zur Überprüfung der Komplexität sicherer Kennwörter, bereit und bietet Unterstützung für Kontosperrungen und Ablauf von Kennwörtern. Eine mit Windows-Authentifizierung hergestellte Verbindung wird manchmal als vertrauenswürdige Verbindung bezeichnet, da die von Windows bereitgestellten Anmeldeinformationen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als vertrauenswürdig angesehen werden.  
  
 Durch die Verwendung der Windows-Authentifizierung können Windows-Gruppen auf Domänenebene und eine Anmeldung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die gesamte Gruppe erstellt werden. Die Zugriffsverwaltung auf Domänenebene kann die Kontoverwaltung vereinfachen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="connecting-through-sql-server-authentication"></a>Herstellen von Verbindungen mithilfe der SQL Server-Authentifizierung  
 Bei Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung werden Anmeldungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt, die nicht auf Windows-Benutzerkonten basieren. Sowohl der Benutzername als auch das Kennwort werden mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert. Benutzer, die mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung eine Verbindung herstellen, müssen jedes Mal ihre Anmeldeinformationen (Anmeldename und Kennwort) bereitstellen, wenn sie eine Verbindung herstellen. Bei der Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung müssen Sie sichere Kennwörter für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konten festlegen. Richtlinien zu sicheren Kennwörtern finden Sie unter [Strong Passwords](../../relational-databases/security/strong-passwords.md).  
  
 Es sind drei optionale Kennwortrichtlinien für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen verfügbar.  
  
-   Benutzer muss das Kennwort bei der nächsten Anmeldung ändern  
  
     Erfordert das Ändern des Kennworts durch den Benutzer beim nächsten Herstellen einer Verbindung. Die Möglichkeit, das Kennwort zu ändern, wird von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]bereitgestellt. Softwareentwickler von Drittanbietern sollten diese Funktion bereitstellen, wenn diese Option verwendet wird.  
  
-   Ablauf des Kennworts erzwingen  
  
     Die Richtlinie des Computers für das maximale Kennwortalter wird für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen erzwungen.  
  
-   Kennwortrichtlinie erzwingen  
  
     Die Windows-Kennwortrichtlinien des Computers werden für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen erzwungen. Dies schließt Kennwortlänge und -komplexität ein. Diese Funktionalität hängt von der `NetValidatePasswordPolicy` -API ab, die nur unter [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] oder höher verfügbar ist.  
  
#### <a name="to-determine-the-password-policies-of-the-local-computer"></a>So bestimmen Sie die Kennwortrichtlinien für den lokalen Computer  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**.  
  
2.  Geben Sie **secpol.msc** im Dialogfeld **Ausführen**ein, und klicken Sie dann auf **OK**.  
  
3.  Erweitern Sie in der Anwendung **Lokale Sicherheitseinstellung** die **Sicherheitseinstellungen**, erweitern Sie **Kontorichtlinien**, und klicken Sie dann auf **Kennwortrichtlinie**.  
  
     Die Kennwortrichtlinien werden im Ergebnisbereich beschrieben.  
  
### <a name="disadvantages-of-sql-server-authentication"></a>Nachteile der SQL Server-Authentifizierung  
  
-   Wenn ein Benutzer ein Windows-Domänenbenutzer ist und über einen Anmeldenamen und ein Kennwort für Windows verfügt, muss er trotzdem einen weiteren ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])-Anmeldenamen und ein weiteres Kennwort angeben, um eine Verbindung herzustellen. Das Nachverfolgen mehrerer Namen und Kennwörter ist für viele Benutzer schwierig. Bei jedem Herstellen einer Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldeinformationen angeben zu müssen, kann ärgerlich sein.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung kann kein Kerberos-Sicherheitsprotokoll verwenden.  
  
-   Windows bietet zusätzliche Kennwortrichtlinien, die für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen nicht verfügbar sind.  
  
-   Das verschlüsselte Anmeldekennwort für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung muss beim Herstellen der Verbindung über das Netzwerk übergeben werden. Einige Anwendungen, die automatisch eine Verbindung herstellen, speichern das Kennwort auf dem Client. So entstehen zusätzliche Angriffspunkte.  
  
### <a name="advantages-of-sql-server-authentication"></a>Vorteile der SQL Server-Authentifizierung  
  
-   Ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Unterstützung von Anwendungen, die älter sind oder von Drittanbietern bereitgestellt werden und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung erfordern.  
  
-   Ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Umgebungen mit gemischten Betriebssystemen zu unterstützen, in denen nicht alle Benutzer von einer Windows-Domäne authentifiziert werden.  
  
-   Ermöglicht es Benutzern, eine Verbindung von unbekannten oder nicht vertrauenswürdigen Domänen herzustellen. Zum Beispiel von einer Anwendung, bei der bestehende Kunden Verbindungen mit zugewiesenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldeinformationen herstellen, um den Status Ihrer Bestellungen abzufragen.  
  
-   Ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , webbasierte Anwendungen zu unterstützen, bei denen Benutzer ihre eigenen Identitäten erstellen.  
  
-   Ermöglicht es Softwareentwicklern, ihre Anwendungen mit einer komplexen Berechtigungshierarchie auf der Basis von bekannten, voreingestellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldeinformationen zu verteilen.  
  
    > [!NOTE]  
    >  Das Verwenden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung schränkt die Berechtigungen lokaler Administratoren für den Computer nicht ein, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überlegungen zur Sicherheit bei SQL Server-Installationen](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
