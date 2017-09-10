---
title: EXECUTE AS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXECUTE AS
- EXECUTE_AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- WITH NO REVERT clause
- sessions [SQL Server], execution context
- EXECUTE AS
- execution context [SQL Server]
- switching execution context
ms.assetid: 613b8271-7f7d-4378-b7a2-5a7698551dbd
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e389fdc50da662deeab7eba030a367e5fc7e97cb
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="execute-as-transact-sql"></a>EXECUTE AS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Legt den Ausführungskontext einer Sitzung fest.  
  
 Standardmäßig beginnt eine Sitzung, wenn sich ein Benutzer anmeldet, und sie endet mit dem Abmelden. Alle Vorgänge während einer Sitzung hängen von Berechtigungsüberprüfungen für diesen Benutzer ab. Wenn ein **EXECUTE AS** -Anweisung ausgeführt wird, wird der Ausführungskontext der Sitzung zum angegebenen Anmeldenamen oder Benutzer gewechselt. Nach dem Kontextwechsel werden Berechtigungen anhand der Anmelde- und Benutzernamen-Sicherheitstoken für dieses Konto anstatt für die Person Aufrufen überprüft die **EXECUTE AS** Anweisung. Im Wesentlichen wird die Identität des Benutzer- oder Anmeldekontos für die Dauer der Sitzung oder der Modulausführung übernommen, oder der Kontextwechsel wird explizit zurückgesetzt.  
  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
{ EXEC | EXECUTE } AS <context_specification>  
[;]  
  
<context_specification>::=  
{ LOGIN | USER } = 'name'  
    [ WITH { NO REVERT | COOKIE INTO @varbinary_variable } ]   
| CALLER  
```  
  
## <a name="arguments"></a>Argumente  
 Anmeldung  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass es sich bei dem Ausführungskontext, dessen Identität übernommen werden soll, um einen Anmeldenamen handelt. Der Bereich des Identitätswechsels liegt auf Serverebene.  
  
> [!NOTE]  
>  Diese Option ist nicht verfügbar in einer enthaltenen Datenbank oder in SQL-Datenbank.  
  
 Benutzer  
 Gibt an, dass der Kontext, der als Identität angenommen werden soll, ein Benutzer in der aktuellen Datenbank ist. Der Identitätswechselbereich ist auf die aktuelle Datenbank beschränkt. Bei einem Kontextwechsel zu einem Datenbankbenutzer werden die Berechtigungen auf Serverebene dieses Benutzers nicht geerbt.  
  
> [!IMPORTANT]  
>  Für die Dauer des Kontextwechsels zum Datenbankbenutzer schlägt die Anweisung bei jedem Versuch, auf Ressourcen außerhalb der Datenbank zuzugreifen, fehl. Dies schließt USE *Datenbank* Anweisungen, verteilte Abfragen und Abfragen, die eine andere Datenbank verweisen, die drei- oder vierteiligen Bezeichnern verwendet.  
  
 **"** *Namen* **"**  
 Ein gültiger Benutzer- oder Anmeldename. *Namen* muss ein Mitglied der **Sysadmin** festen Serverrolle oder als Prinzipal in vorhanden [Sys. database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) oder [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md), bzw..  
  
 *Namen* kann als lokale Variable angegeben werden.  
  
 *Namen* muss ein Singleton-Konto sein, und nicht mit einer Gruppe, Rolle, Zertifikat, Schlüssel oder integriertes Konto, z. B. NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService oder NT AUTHORITY\LocalSystem.  
  
 Weitere Informationen finden Sie unter [angeben eines Benutzer- oder Anmeldename](#_user) weiter unten in diesem Thema.  
  
 NO REVERT  
 Gibt an, dass der Kontextwechsel nicht auf den vorherigen Kontext zurückgesetzt werden kann. Die **NO REVERT** Option kann nur auf der Ad-hoc-Ebene verwendet werden.  
  
 Weitere Informationen zu den vorherigen Kontext wiederherstellen, finden Sie unter [REVERT &#40; Transact-SQL &#41; ](../../t-sql/statements/revert-transact-sql.md).  
  
 COOKIE in  **@**  *Varbinary_variable*  
 Gibt an, der Ausführungskontext kann nur auf den vorherigen Kontext zurückgesetzt werden, wenn die aufrufende REVERT WITH COOKIE-Anweisung den richtigen enthält  **@**  *Varbinary_variable* Wert. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] übergibt das Cookie an  **@**  *Varbinary_variable*. Die **COOKIE in** Option kann nur auf der Ad-hoc-Ebene verwendet werden.  
  
 **@***Varbinary_variable* ist **varbinary(8000)**.  
  
> [!NOTE]  
>  Das Cookie **Ausgabe** -Parameter für ist derzeit als dokumentiert **varbinary(8000)** also in der korrekten maximalen Länge. Die aktuelle Implementierung gibt jedoch zurück **varbinary(100)**. Anwendungen sollten reservieren **varbinary(8000)** , damit die Anwendung weiterhin ordnungsgemäß ausgeführt wird, falls die Rückgabegröße des in einer zukünftigen Version erhöht wird.  
  
 CALLER  
 Bei Verwendung innerhalb eines Moduls gibt dieser Wert an, dass die Anweisungen innerhalb des Moduls im Kontext des Modulaufrufers ausgeführt werden.  
  
 Bei Verwendung außerhalb eines Moduls weist die Anweisung keine Aktion auf.  
  
## <a name="remarks"></a>Hinweise  
 Die Änderung des Ausführungskontexts bleibt wirksam, bis eine der folgenden Bedingungen auftritt:  
  
-   Eine andere EXECUTE AS-Anweisung wird ausgeführt.  
  
-   Eine REVERT-Anweisung wird ausgeführt.  
  
-   Die Sitzung wird gelöscht.  
  
-   Die gespeicherte Prozedur oder der Trigger, für die bzw. den der Befehl ausgeführt wurde, wird beendet.  
  
Sie können einen Ausführungskontextstapel erstellen, indem Sie die EXECUTE AS-Anweisung mehrmals für mehrere Prinzipale aufrufen. Bei Aufruf wechselt die REVERT-Anweisung den Kontext zu dem Anmelde- oder Benutzernamen in der nächsten Ebene des Kontextstapels. Eine Demonstration dieses Verhaltens, finden Sie unter [Beispiel A](#_exampleA).  
  
##  <a name="_user"></a>Angeben eines Benutzer- oder Anmeldename  
 Der Benutzer- oder Anmeldename Name, der in EXECUTE AS angegebenen \<Context_specification > muss vorhanden sein, als Prinzipal in **Sys. database_principals** oder **Sys. server_principals**, oder die EXECUTE AS-Anweisung erzeugt einen Fehler. Zudem müssen für den Prinzipal IMPERSONATE-Berechtigungen erteilt worden sein. Wenn der Aufrufer nicht der Datenbankbesitzer oder Mitglied der **Sysadmin** festen Serverrolle, der Prinzipal muss vorhanden sein, auch wenn der Benutzer die Datenbank oder Instanz von zugreift [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] über eine Windows-Gruppenmitgliedschaft. Stellen Sie sich z. B. folgende Bedingungen vor: 
  
-   **Die CompanyDomain\SQLUsers** -Gruppe hat Zugriff auf die **Sales** Datenbank.  
  
-   **CompanyDomain\SqlUser1** Mitglied **SQLUsers** und besitzt daher implizit Zugriff auf die **Sales** Datenbank.  
  
 Obwohl **CompanyDomain\SqlUser1** hat Zugriff auf die Datenbank über die Mitgliedschaft in der **SQLUsers** zu gruppieren, die Anweisung `EXECUTE AS USER = 'CompanyDomain\SqlUser1'` schlägt fehl, da `CompanyDomain\SqlUser1` als Prinzipal in nicht vorhanden die Datenbank.  
  
Wenn der Benutzer verwaist ist (der zugeordnete Anmeldename nicht mehr vorhanden ist), und der Benutzer wurde nicht erstellt, mit **WITHOUT LOGIN**, **EXECUTE AS** schlägt fehl, für den Benutzer.  
  
## <a name="best-practice"></a>Bewährte Methoden  
 Geben Sie einen Anmelde- oder Benutzernamen an, der die geringsten Privilegien besitzt, die zum Ausführen der Vorgänge in der Sitzung erforderlich sind. Geben Sie z. B. keinen Anmeldenamen mit Berechtigungen auf Serverebene an, wenn nur Berechtigungen auf Datenbankebene erforderlich sind. Oder geben Sie nur dann ein Datenbankbesitzerkonto an, wenn diese Berechtigungen tatsächlich erforderlich sind.  
  
> [!CAUTION]  
>  Die EXECUTE AS-Anweisung kann erfolgreich sein, wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Namen auflösen kann. Wenn ein Domänenbenutzer vorhanden ist, kann Windows den Benutzer für [!INCLUDE[ssDE](../../includes/ssde-md.md)] möglicherweise auflösen, obwohl der Windows-Benutzer keinen Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat. Dies kann zu einer Bedingung führen, in der eine Anmeldung ohne Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anscheinend nicht angemeldet ist, obwohl die Anmeldung für den Identitätswechsel nur Berechtigungen besitzt, die public oder guest gewährt wurden.  
  
## <a name="using-with-no-revert"></a>Verwenden von WITH NO REVERT  
 Wenn die EXECUTE AS-Anweisung die optionale WITH NO REVERT-Klausel enthält, kann der Ausführungskontext einer Sitzung nicht mithilfe von REVERT oder durch Ausführen einer anderen EXECUTE AS-Anweisung zurückgesetzt werden. Der von der Anweisung festgelegte Kontext bleibt aktiv, bis die Sitzung gelöscht wird.  
  
 Wenn die WITH NO REVERT COOKIE = @*Varbinary_variabl*e-Klausel angegeben wird, die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] übergibt den Cookiewert an @*Varbinary_variabl*e. Der Ausführungskontext festgelegt, dass die Anweisung nur auf den vorherigen Kontext zurückgesetzt werden kann, wenn die aufrufende REVERT WITH COOKIE = @*Varbinary_variable* -Anweisung enthält die gleiche  *@varbinary_variable*  Wert.  
  
 Diese Option ist in einer Umgebung nützlich, in der Verbindungspools verwendet werden. Mithilfe von Verbindungspools wird eine Gruppe von Datenbankverbindungen verwaltet, die von Anwendungen auf einem Anwendungsserver wiederverwendet werden können. Da der Wert zu übergeben  *@varbinary_variable*  bekannt ist, nur an den Aufrufer der EXECUTE AS-Anweisung, dass der eingerichtete Ausführungskontext von keinem anderen Benutzer geändert werden kann, kann der Aufrufer sicherstellen.  
  
## <a name="determining-the-original-login"></a>Bestimmen des ursprünglichen Anmeldenamens  
 Verwenden der [ORIGINAL_LOGIN](../../t-sql/functions/original-login-transact-sql.md) Funktion, um den Namen der Anmeldung zurück, die Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mit dieser Funktion können Sie die Identität des ursprünglichen Anmeldenamens in Sitzungen zurückgeben, in denen zahlreiche explizite oder implizite Kontextwechsel vorkommen.  
  
## <a name="permissions"></a>Berechtigungen  
 An **EXECUTE AS** der Anrufer muss für einen Anmeldenamen verfügen **IMPERSONATE** Berechtigung für den angegebenen Anmeldenamen benennen und dürfen nicht verweigert werden die **IMPERSONATE ANY LOGIN** Berechtigung . An **EXECUTE AS** für einen Datenbankbenutzer, der Aufrufer benötigen **IMPERSONATE** Berechtigungen für den angegebenen Benutzernamen ein. Wenn **EXECUTE AS CALLER** angegeben wird, **IMPERSONATE** Berechtigungen sind nicht erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
###  <a name="_exampleA"></a> A. Verwenden von EXECUTE AS und REVERT zum Wechseln des Kontexts  
 Im folgenden Beispiel wird ein Kontextausführungsstapel mit mehreren Prinzipalen erstellt. Mit der `REVERT`-Anweisung wird der Ausführungskontext anschließend auf den vorherigen Aufrufer zurückgesetzt. Die `REVERT`-Anweisung wird mehrmals ausgeführt und bewegt sich so durch den Stapel, bis der Ausführungskontext wieder auf den ursprünglichen Aufrufer festgelegt ist.  
  
```  
USE AdventureWorks2012;  
GO  
--Create two temporary principals  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
--Give IMPERSONATE permissions on user2 to user1  
--so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
--Verify the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
--Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1 and login2.  
--The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
--Remove temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. Verwenden der WITH COOKIE-Klausel  
 Im folgenden Beispiel wird den Ausführungskontext einer Sitzung auf einen angegebenen Benutzer und gibt an, die WITH NO REVERT COOKIE = @*Varbinary_variabl*e-Klausel. In der `REVERT`-Anweisung muss der an die `@cookie`-Variable in der `EXECUTE AS`-Anweisung übergebene Wert angegeben sein, damit der Kontext erfolgreich auf den Aufrufer zurückgesetzt werden kann. Zur Ausführung dieses Beispiels müssen der `login1`-Anmeldename und der `user1`-Benutzer, die in Beispiel A erstellt wurden, vorhanden sein.  
  
```  
DECLARE @cookie varbinary(8000);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie in a safe location in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(8000);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Wiederherstellen &#40; Transact-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS-Klausel &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)  
  
  


