---
title: Sp_addlinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addlinkedsrvlogin_TSQL
- sp_addlinkedsrvlogin
dev_langs: TSQL
helpviewer_keywords: sp_addlinkedsrvlogin
ms.assetid: eb69f303-1adf-4602-b6ab-f62e028ed9f6
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a4a55d2128cdba654ce9e753ac1cdcebd8f0ad8d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spaddlinkedsrvlogin-transact-sql"></a>sp_addlinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt oder aktualisiert eine Zuordnung zwischen einem Anmeldenamen in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und einem Sicherheitskonto auf einem Remoteserver.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addlinkedsrvlogin [ @rmtsrvname = ] 'rmtsrvname'   
     [ , [ @useself = ] 'TRUE' | 'FALSE' | NULL ]   
     [ , [ @locallogin = ] 'locallogin' ]   
     [ , [ @rmtuser = ] 'rmtuser' ]   
     [ , [ @rmtpassword = ] 'rmtpassword' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ @rmtsrvname  **=**  ] **"***Rmtsrvname***"**  
 Der Name eines Verbindungsservers, für den die Anmeldenamenzuordnung gilt. *Rmtsrvname* ist **Sysname**, hat keinen Standardwert.  
  
 [ @useself  **=**  ] **"**" TRUE "**"** | 'FALSE' | 'NULL'  
 Bestimmt, ob für die Verbindung *Rmtsrvname* Identität lokaler Anmeldenamen angenommen oder explizit Senden von Anmeldenamen und ein Kennwort. Der Datentyp ist **Varchar (**8**)**, Standardwert ist "true".  
  
 Der Wert "true" gibt an, dass Anmeldungen ihre eigenen Anmeldeinformationen verwenden, für die Verbindung *Rmtsrvname*, mit der *Rmtuser* und *Rmtpassword* Argumente ignoriert. "False" gibt an, dass die *Rmtuser* und *Rmtpassword* Argumente werden verwendet, um die Verbindung mit *Rmtsrvname* für den angegebenen *Locallogin* . Wenn *Rmtuser* und *Rmtpassword* sind auch auf NULL, kein Anmeldename oder ein Kennwort festgelegt ist für die Verbindung mit dem Verbindungsserver verwendet.  
  
 [ @locallogin  **=**  ] **"***Locallogin***"**  
 Ein Anmeldename auf dem lokalen Server. *Locallogin* ist **Sysname**, hat den Standardwert NULL. NULL gibt an, dass dieser Eintrag für alle lokalen Anmeldenamen gilt, die Verbindung *Rmtsrvname*. Falls ungleich NULL, *Locallogin* kann eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder eine Windows-Anmeldung. Dem Windows-Anmeldenamen muss das Recht zum Zugreifen auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erteilt worden sein. Dies kann entweder direkt oder über die Mitgliedschaft in einer Windows-Gruppe erfolgen, der das Zugriffsrecht erteilt wurde.  
  
 [ @rmtuser  **=**  ] **"***Rmtuser***"**  
 Der remoteanmeldename für die Verbindung verwendete *Rmtsrvname* Wenn @useself ist "false". Wenn der Remoteserver ist eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, die keine Windows-Authentifizierung *Rmtuser* ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung. *Rmtuser* ist **Sysname**, hat den Standardwert NULL.  
  
 [ @rmtpassword  **=**  ] **"***Rmtpassword***"**  
 Das Kennwort zugeordnet ist *Rmtuser*. *Rmtpassword* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn sich ein Benutzer beim lokalen Server anmeldet und eine verteilte Abfrage ausführt, die auf eine Tabelle auf dem Verbindungsserver zugreift, muss sich der lokale Server beim Verbindungsserver im Auftrag des Benutzers anmelden, um auf diese Tabelle zugreifen zu können. Geben Sie mithilfe von sp_addlinkedsrvlogin die Anmeldeinformationen an, die der lokale Server zum Anmelden beim Verbindungsserver verwendet.  
  
> [!NOTE]  
>  Um bei Verwendung einer Tabelle auf einem Verbindungsserver die besten Abfragepläne zu erstellen, muss der Abfrageprozessor Datenverteilungsstatistiken vom Verbindungsserver aufweisen. Benutzer, die über eingeschränkte Berechtigungen für beliebige Tabellenspalten verfügen, haben möglicherweise nicht die erforderlichen Berechtigungen, um alle nützlichen Statistiken abzurufen. Der Abfrageplan kann daher weniger effizient und die Leistung beeinträchtigt sein. Zum Anzeigen aller verfügbaren Statistiken muss der Benutzer Besitzer der Tabelle oder Mitglied der festen Serverrolle sysadmin, der festen Datenbankrolle db_owner oder der festen Datenbankrolle db_ddladmin auf dem Verbindungsserver sein, wenn der Verbindungsserver eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist. In SQL Server 2012 SP1 wurden die Berechtigungseinschränkungen zum Abrufen von Statistiken geändert. Benutzer mit der SELECT-Berechtigung können auf Statistiken zugreifen, die über DBCC SHOW_STATISTICS verfügbar sind. Weitere Informationen finden Sie im Abschnitt "Berechtigungen" des [DBCC SHOW_STATISTICS &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
 Eine Standardzuordnung zwischen allen Anmeldenamen auf dem lokalen Server und Remoteanmeldenamen auf dem Verbindungsserver wird durch Ausführen von sp_addlinkedserver automatisch erstellt. Die Standardzuordnung legt fest, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anmeldeinformationen der lokalen Anmeldung für den Zugriff auf den Verbindungsserver im Auftrag des Anmeldenamens verwendet. Dies entspricht dem Ausführen von Sp_addlinkedsrvlogin mit @useself festgelegt **"true"** für den Verbindungsserver, ohne dass ein lokaler Benutzername angegeben. Verwenden Sie sp_addlinkedsrvlogin nur, um die Standardzuordnung zu ändern oder um neue Zuordnungen für bestimmte lokale Anmeldenamen hinzuzufügen. Mithilfe von sp_droplinkedsrvlogin löschen Sie die Standardzuordnung oder eine beliebige andere Zuordnung.  
  
 Anstatt mit sp_addlinkedsrvlogin eine vordefinierte Anmeldenamenzuordnung erstellen zu müssen, kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch die Windows-Anmeldeinformationen für die Sicherheit (Windows-Anmeldename und -Kennwort) eines Benutzers verwenden, der die Abfrage für den Zugriff auf einen Verbindungsserver ausgibt. Dazu müssen die folgenden Bedingungen erfüllt sein:  
  
-   Ein Benutzer ist mithilfe des Windows-Authentifizierungsmodus mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden.  
  
-   Die Sicherheitskontendelegierung ist auf dem Client und dem sendenden Server verfügbar.  
  
-   Der Anbieter unterstützt den Windows-Authentifizierungsmodus (z. B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter Windows).  
  
> [!NOTE]  
>  Die Delegierung muss für Szenarien mit einem einzigen Hop nicht aktiviert werden, bei mehreren Hops ist dies jedoch erforderlich.  
  
 Nachdem die Authentifizierung durch den Verbindungsserver mit den Zuordnungen erfolgt ist, die durch Ausführen von sp_addlinkedsrvlogin auf der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiert wurden, werden die Berechtigungen für die einzelnen Objekte in der Remotedatenbank nicht durch den lokalen Server, sondern durch den Verbindungsserver bestimmt.  
  
 sp_addlinkedsrvlogin kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY LOGIN-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-connecting-all-local-logins-to-the-linked-server-by-using-their-own-user-credentials"></a>A. Verbinden aller lokalen Anmeldenamen mit dem Verbindungsserver mithilfe ihrer eigenen Anmeldeinformationen  
 Das folgende Beispiel erstellt eine Zuordnung, um sicherzustellen, dass bei allen Anmeldungen vom lokalen Server auf den Verbindungsserver `Accounts` die Anmeldeinformationen des jeweiligen Benutzers verwendet werden.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts';  
```  
  
 oder  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'true';  
```  
  
> [!NOTE]  
>  Falls für einzelne Anmeldenamen explizite Zuordnungen erstellt werden, haben diese Vorrang vor globalen Zuordnungen, die für diesen Verbindungsserver vorhanden sind.  
  
### <a name="b-connecting-a-specific-login-to-the-linked-server-by-using-different-user-credentials"></a>B. Verbinden eines bestimmten Anmeldenamens mit dem Verbindungsserver mithilfe anderer Anmeldeinformationen  
 Das folgende Beispiel erstellt eine Zuordnung, um sicherzustellen, dass die Windows-Benutzerin `Domain\Mary` auf den Verbindungsserver `Accounts` mit dem Anmeldenamen `MaryP` und dem Kennwort `d89q3w4u` zugreifen kann.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'false', 'Domain\Mary', 'MaryP', 'd89q3w4u';  
```  
  
> [!IMPORTANT]  
>  Für dieses Beispiel wird nicht die Windows-Authentifizierung verwendet. Kennwörter werden unverschlüsselt übertragen. Kennwörter möglicherweise in Datenquellendefinitionen und Skripts, die gespeichert werden auf den Datenträger, die in Sicherungen und in Protokolldateien. Verwenden Sie für diese Art von Verbindung auf keinen Fall ein Administratorkennwort. Wenden Sie sich wegen Sicherheitshinweisen speziell für Ihre Umgebung an Ihren Netzwerkadministrator.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindungsserver-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Sp_droplinkedsrvlogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
