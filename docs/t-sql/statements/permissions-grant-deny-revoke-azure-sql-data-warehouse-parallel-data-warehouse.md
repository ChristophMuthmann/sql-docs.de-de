---
title: "GRANT DENY REVOKE Perms – Azure SQL-Daten und Parallel Datawarehouses | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c46d4df3d19b2c548b203f62a14ea4ebc0226296
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>Berechtigungen: GRANT, DENY oder REVOKE (Azure SQL Datawarehouse, Parallel Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Verwendung [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **GRANT** und **DENY** Anweisungen zu erteilen oder Verweigern einer Berechtigung (z. B. **UPDATE**) für ein sicherungsfähiges Element (z. B. eine Datenbank, Tabelle, Sicht usw..) können einem Sicherheitsprinzipal (eine Anmeldung, ein Datenbankbenutzer oder eine Datenbankrolle). Verwendung **widerrufen** zum Entfernen der erteilen oder Verweigern einer Berechtigung.  
  
 Berechtigungen auf Serverebene werden Anmeldungen angewendet. Berechtigungen auf Datenbankebene werden Datenbankbenutzer und Datenbankrollen angewendet.  
  
 Um festzustellen, welche Berechtigungen erteilt und verweigert wurde, können Fragen Sie die Sys. server_permissions und database_permissions-Sichten ab. Berechtigungen, die nicht explizit erteilt oder verweigert wurden, zu einem Sicherheitsprinzipal können von, die Mitglied einer Rolle mit den Berechtigungen geerbt werden. Die Berechtigungen einer festen Datenbankrolle können nicht geändert werden und werden nicht in den Ansichten Sys. server_permissions und database_permissions angezeigt.  
  
-   **GRANT** explizit eine oder mehrere Berechtigungen erteilt.  
  
-   **DENY** explizit verweigert den Prinzipal über eine oder mehrere Berechtigungen verfügen.  
  
-   **WIDERRUFEN** entfernt vorhandene **GRANT** oder **DENY** Berechtigungen.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
REVOKE   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    [ FROM | TO ] principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>Argumente  
 \<Berechtigung > [ **,**... *n* ]  
 Eine oder mehrere Berechtigungen zu gewähren, verweigern oder widerrufen.  
  
 ON [ \<Class_type >::] *sicherungsfähigen* der **ON** -Klausel beschreibt die sicherungsfähigen Parameter für das erteilen, verweigern oder widerrufen von Berechtigungen.  
  
 \<Class_type > den Klassentyp des sicherungsfähigen Elements. Dies kann **Anmeldung**, **Datenbank**, **Objekt**, **SCHEMA**, **Rolle**, oder **Benutzer** . Berechtigungen können auch erteilt werden, um die **SERVER *** Class_type*, aber **SERVER** für diese Berechtigungen nicht angegeben ist. **Datenbank** ist nicht angegeben, wenn die Berechtigung für das Wort enthält **Datenbank** (z. B. **ALTER ANY DATABASE**). Wenn kein *Class_type* angegeben ist und der Berechtigungstyp ist nicht beschränkt auf den Server oder Datenbankklasse, die Klasse wird davon ausgegangen, dass werden **Objekt**.  
  
 *securable*  
 Der Name der Anmeldung, Datenbank, Tabelle, Sicht, Schema, Prozedur, Funktion oder Benutzer, auf denen erteilt, verweigert oder widerrufen von Berechtigungen. Der Objektname kann angegeben werden, mit den dreiteiligen Benennungsregeln, die in beschriebenen [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 UM *principal* [ **,**... *n* ]  
 Einen oder mehrere Prinzipale wird erteilt, verweigert oder widerrufen von Berechtigungen. Prinzipal ist der Name einer Anmeldung, den Datenbankbenutzer oder die Datenbankrolle.  
  
 VON *principal* [ **,**... *n* ]  
 Eine oder mehrere Prinzipale Widerrufen von Berechtigungen aus.  Prinzipal ist der Name einer Anmeldung, den Datenbankbenutzer oder die Datenbankrolle. **VON** kann nur verwendet werden, mit einem **widerrufen** Anweisung. **UM** genutzt werden **GRANT**, **DENY**, oder **widerrufen**.  
  
 WITH GRANT OPTION  
 Gibt an, dass der Empfänger die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
 CASCADE  
 Gibt an, dass die Berechtigung verweigert oder aufgehoben wird, die dem angegebenen Prinzipal und für alle anderen Prinzipale, die der Prinzipal die Berechtigung gewährt. Erforderlich, wenn der Prinzipal die Berechtigung mit besitzt **GRANT OPTION**.  
  
 GRANT OPTION FOR  
 Gibt an, dass die Fähigkeit, die angegebene Berechtigung zu erteilen, aufgehoben wird. Dies ist erforderlich, bei der Verwendung der **CASCADE** Argument.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne besitzt die **GRANT** Option, die Berechtigung selbst aufgehoben werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Um eine Berechtigung zu erteilen, muss der berechtigende (Grantor) haben entweder die Berechtigung selbst mit den **WITH GRANT OPTION**, oder Sie benötigen eine höhere Berechtigung, die die erteilte Berechtigung impliziert.  Objektbesitzer können Berechtigungen für die Objekte erteilen, die sie besitzen. Prinzipale mit **Steuerelement** -Berechtigung für ein sicherungsfähiges Element kann Berechtigung für dieses sicherungsfähige Element.  Mitglieder der **Db_owner** und **Db_securityadmin** festen Datenbankrollen können beliebige Berechtigungen in der Datenbank erteilen.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Durch das verweigern oder Aufheben von Berechtigungen für einen Prinzipal wirkt Anforderungen sich nicht, die Autorisierung übergeben wurden, und zurzeit ausgeführt werden. Zum Einschränken des Zugriffs müssen Sie sofort, "Abbrechen" aktive Anforderungen oder aktuelle Sitzungen beenden.  
  
> [!NOTE]  
>  Die meisten feste Serverrollen sind nicht in dieser Version verfügbar. Verwenden Sie stattdessen eine benutzerdefinierte Datenbankrollen. Anmeldungen können nicht hinzugefügt werden, um die **Sysadmin** festen Serverrolle "". Erteilen der **CONTROL SERVER** Berechtigung entspricht in etwa die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".  
  
 Einige Anweisungen sind mehrere Berechtigungen erforderlich. Beispielsweise zum Erstellen einer Tabelle erfordert die **CREATE TABLE** Berechtigungen in der Datenbank und die **ALTER SCHEMA** -Berechtigung für die Tabelle, die die Tabelle enthalten wird.  
  
 PDW führt Manchmal gespeicherte Prozeduren, um die Benutzeraktionen für die Serverknoten zu verteilen. Aus diesem Grund kann nicht die Execute-Berechtigung für eine ganze Datenbank verweigert werden. (Z. B. `DENY EXECUTE ON DATABASE::<name> TO <user>;` schlägt fehl.) Verweigern Sie umgehen die Execute-Berechtigung für die Benutzer-Schemas oder bestimmte Objekte (Prozeduren).  
  
### <a name="implicit-and-explicit-permissions"></a>Implizite und explizite Berechtigungen  
 Ein *explizite Berechtigung* ist ein **GRANT** oder **DENY** Berechtigung erhält, die einem Prinzipal durch eine **GRANT** oder **DENY**Anweisung.  
  
 Ein *implizite Berechtigung* ist ein **GRANT** oder **DENY** Berechtigung, die ein Prinzipal (Anmeldung, Benutzer oder Datenbankrolle "") von einer anderen Datenbankrolle geerbt hat.  
  
 Eine implizite Berechtigung kann auch von einem abdeckenden oder die übergeordnete Berechtigung geerbt werden. Beispielsweise **UPDATE** Berechtigung für eine Tabelle geerbt werden kann, indem Sie **UPDATE** -Berechtigung für das Schema, das die Tabelle enthält oder **Steuerelement** Berechtigung für die Tabelle.  
  
### <a name="ownership-chaining"></a>Besitzverkettung  
 Wenn mehrere Datenbankobjekte gegenseitig aufeinander sequenziell zugreifen, wird diese Sequenz als bezeichnet eine *Kette*. Obwohl solche Ketten nicht unabhängig voneinander vorhanden sind, werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Traversieren der Links in einer Kette durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Berechtigungen für die einzelnen Objekte anders ausgewertet als beim getrennten Zugriff auf die Objekte. Besitzverkettung hat erhebliche Auswirkungen für die Verwaltung der Sicherheit. Weitere Informationen zu Besitzketten finden Sie unter [Besitzketten](http://msdn.microsoft.com/en-us/library/ms188676\(v=sql11\).aspx) und [Lernprogramm: Besitzketten und Kontextwechsel](http://msdn.microsoft.com/en-us/library/bb153640\(v=sql11\).aspx).  
  
## <a name="permission-list"></a>Berechtigungsliste  
  
### <a name="server-level-permissions"></a>Berechtigungen auf Serverebene  
 Berechtigungen auf Serverebene können gewährt, verweigert, und Anmeldungen aufgehoben.  
  
 **Berechtigungen, die auf Server anwenden**  
  
-   CONTROL SERVER  
  
-   ADMINISTER BULK OPERATIONS  
  
-   ALTER ANY CONNECTION  
  
-   ALTER ANY DATABASE  
  
-   CREATE ANY DATABASE  
  
-   ALTER ANY EXTERNAL DATA SOURCE  
  
-   ALTER ANY EXTERNAL FILE FORMAT  
  
-   ALTER ANY LOGIN  
  
-   ALTER SERVER STATE  
  
-   CONNECT SQL  
  
-   VIEW ANY DEFINITION  
  
-   VIEW ANY DATABASE  
  
-   VIEW SERVER STATE  
  
 **Berechtigungen, die Anmeldungen angewendet werden soll.**  
  
-   CONTROL FÜR LOGIN  
  
-   ALTER FÜR LOGIN  
  
-   BEI DER ANMELDUNG DIE IDENTITÄT ANNEHMEN  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>Berechtigungen auf Datenbankebene  
 Berechtigungen auf Datenbankebene können, abgelehnte und gesperrte aus Datenbankbenutzer und benutzerdefinierte Datenbankrollen erteilt werden.  
  
 **Berechtigungen, die gelten für alle Datenbankklassen**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **Berechtigungen, die für alle Datenbankklassen, mit Ausnahme von Benutzern angewendet werden soll.**  
  
-   TAKE OWNERSHIP  
  
 **Berechtigungen, die nur für Datenbanken angewendet werden soll.**  
  
-   ALTER ANY DATABASE  
  
-   ALTER FÜR DATABASE  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   IN DER DATENBANK VERBINDEN  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **Berechtigungen, die gelten nur für Benutzer**  
  
-   IMPERSONATE  
  
 **Berechtigungen, die für Datenbanken, Schemas und Objekte gelten**  
  
-   ALTER  
  
-   DELETE  
  
-   Führen Sie  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   REFRENCES  
  
 Eine Definition für jede Art der Berechtigung, finden Sie unter [Berechtigungen (Datenbankmodul)](http://msdn.microsoft.com/library/ms191291.aspx).  
  
### <a name="chart-of-permissions"></a>Diagramm der Berechtigungen  
 Alle Berechtigungen werden auf dieses Poster grafisch dargestellt. Dies ist die einfachste Möglichkeit, eine geschachtelte Hierarchie von Berechtigungen finden Sie unter. Z. B. die **ALTER ON LOGIN** Berechtigung erteilt werden kann, indem selbst, aber sie ist auch aus, wenn eine Anmeldung erteilt wird die **Steuerelement** Berechtigung für diesen Anmeldenamen oder wenn eine Anmeldung erteilt wird die **ALTER ANY Anmeldung** Berechtigung.  
  
 ![Poster der APS Sicherheit Berechtigungen](../../t-sql/statements/media/aps-security-perms-poster.png "Poster der APS-Sicherheit-Berechtigungen")  
  
 Informationen zum Herunterladen einer Vollbildgröße Version dieses Posters finden Sie unter [SQL Server PDW-Berechtigungen](http://go.microsoft.com/fwlink/?LinkId=244249)im Abschnitt "Dateien" der APS Yammer-Website (oder -Anforderung per E-mail von  **apsdoc@microsoft.com** .  
  
## <a name="default-permissions"></a>Standardberechtigungen  
 Die folgende Liste beschreibt die Standardberechtigungen an:  
  
-   Erstellung ein Anmeldenamens mit dem **CREATE LOGIN** Anweisung, die der neue Anmeldenamen empfängt die **CONNECT SQL** Berechtigung.  
  
-   Alle Anmeldenamen sind Mitglied der **öffentlichen** -Serverrolle und kann nicht entfernt werden, von **öffentlichen**.  
  
-   Wenn ein Datenbankbenutzer erstellt wird, mithilfe der **CREATE USER** Berechtigung für der Datenbankbenutzer empfängt die **verbinden** Berechtigung in der Datenbank.  
  
-   Alle Prinzipale, einschließlich der **öffentlichen** Rolle verfügen standardmäßig über keine expliziten oder impliziten Berechtigungen.  
  
-   Wenn Sie einen Anmeldenamen oder Benutzer der Besitzer einer Datenbank oder das Objekt ist, hat den Anmeldenamen oder Benutzer immer alle Berechtigungen für die Datenbank oder des Objekts. Die Besitzerrechte können nicht geändert werden und sind nicht als explizite Berechtigungen sichtbar. Die **GRANT**, **DENY**, und **widerrufen** Anweisungen wirken sich nicht auf Besitzer.  
  
-   Die **sa** Anmeldung verfügt über alle Berechtigungen auf dem Gerät. Besitzerrechte, ähnelt der **sa** Berechtigungen kann nicht geändert werden und sind nicht als explizite Berechtigungen sichtbar. Die **GRANT**, **DENY**, und **widerrufen** Anweisungen haben keine Auswirkung auf **sa** Anmeldung. Die **sa** Anmeldung kann nicht umbenannt werden.  
  
-   Die **verwenden** Anweisung erfordert keine Berechtigungen. Alle Prinzipale Ausführungsdauer der **verwenden** Anweisung für jede Datenbank.  
  
##  <a name="Examples"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. Erteilen einer Berechtigung auf Serverebene für einen Anmeldenamen  
 Die folgenden beiden Anweisungen erteilen eine Berechtigung auf Serverebene für einen Anmeldenamen.  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. Erteilen einer Berechtigung auf Serverebene für einen Anmeldenamen  
 Im folgenden Beispiel wird gewährt eine Berechtigung auf Serverebene für einen Anmeldenamen mit einem Server principal (einen anderen Anmeldenamen).  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. Einem Benutzer erteilen eine Berechtigung auf Datenbankebene  
 Im folgenden Beispiel wird gewährt eine Berechtigung auf Datenbankebene für einen Benutzer an einen Datenbankprinzipal (ein anderer Benutzer).  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. Erteilen, verweigern und Aufheben einer schemaberechtigung für  
 Die folgenden **GRANT** Anweisung erteilt eröffnet die Möglichkeit zur Auswahl von Daten aus einer Tabelle oder Sicht im Dbo-Schema.  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 Die folgenden **DENY** Anweisung verhindert, dass eröffnet auswählen von Daten aus einer Tabelle oder Sicht im Dbo-Schema. Eröffnet kann nicht Daten gelesen werden, auch wenn er die Berechtigung auf andere Weise, wie z. B. über eine Mitgliedschaft in Datenbankrolle besitzt.  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 Die folgenden **widerrufen** -Anweisung entfernt die **DENY** Berechtigung. Jetzt sind die expliziten Berechtigungen des eröffnet neutrale. Eröffnet möglicherweise Daten aus jeder Tabelle über eine andere implizite Berechtigung wie z. B. eine Mitgliedschaft in Datenbankrolle auswählen können.  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. Optionale Objekt demonstrieren:: Klausel  
 Da das Objekt die Standardklasse für die berechtigungsanweisung eine ist, sind die folgenden beiden Anweisungen identisch. Die **Objekt::** -Klausel ist optional.  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  

