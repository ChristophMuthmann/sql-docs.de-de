---
title: 'GRANT-, DENY-, REVOKE-Berechtigungen: Azure SQL Data Warehouse und Parallel Data Warehouse | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 45026cd63aa7461db65cb1927738cc1cc71295e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>Berechtigungen: GRANT, DENY, REVOKE (Azure SQL Data Warehouse, Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Verwenden Sie die Anweisungen **GRANT** und **DENY** von [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], um einem Sicherheitsprinzipal (ein Anmeldename, ein Datenbankbenutzer oder eine Datenbankrolle) eine Berechtigung (z.B. **UPDATE**) eines sicherungsfähigen Elements (z.B. Datenbank, Tabelle, Sicht, usw.) zu erteilen oder zu verweigern. Verwenden Sie **REVOKE** um die Erteilung oder Verweigerung einer Berechtigung zu widerrufen.  
  
 Berechtigungen auf Serverebene werden auf Anmeldenamen angewendet. Berechtigungen auf Datenbankebene werden auf Datenbankbenutzer und Datenbankrollen angewendet.  
  
 Fragen Sie die Sichten „sys.server_permissions“ und „sys.database_permissions“ ab, um festzustellen, welche Berechtigungen erteilt und verweigert wurden. Berechtigungen, die einem Sicherheitsprinzipal nicht explizit erteilt oder verweigert wurden, können geerbt werden, wenn eine Mitgliedschaft einer Rolle mit Berechtigung besteht. Die Berechtigungen der festen Datenbankrollen können nicht geändert werden und werden nicht in den Sichten „sys.server_permissions“ und „sys.database_permissions“ angezeigt.  
  
-   **GRANT** erteilt explizit mindestens eine Berechtigung.  
  
-   **DENY** verweigert dem Prinzipal explizit mindestens eine Berechtigung.  
  
-   **REVOKE** entfernt vorhandene **GRANT**- oder **DENY**-Berechtigungen.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 \<permission>[ **,**...*n*]  
 Mindestens eine Berechtigung, die zu erteilen, verweigern oder widerrufen ist.  
  
 ON [ \<class_type> :: ] *securable* Die **ON**-Klausel beschreibt den sicherungsfähigen Parameter, für den Berechtigungen erteilt, verweigert oder widerrufen werden sollen.  
  
 \<class_type> Der Klassentyp des sicherungsfähigen Elements. Dies kann eins der folgenden Elemente sein: **LOGIN**, **DATABASE**, **OBJECT**, **SCHEMA**, **ROLE** oder **USER**. Berechtigungen können auch für **SERVER***class_type* erteilt werden, jedoch wird **SERVER** für diese Berechtigungen nicht angegeben. **DATABASE** wird nicht angegeben, wenn die Berechtigung das Wort **DATABASE** enthält (z.B. **ALTER ANY DATABASE**). Wenn *class_type* nicht angegeben ist und der Berechtigungstyp nicht auf die Server- oder Datenbankklassen beschränkt ist, wird von der Klasse **OBJECT** ausgegangen.  
  
 *securable*  
 Der Name für die Anmeldung, die Datenbank, die Tabelle, die Sicht, das Schema, die Prozedur, die Rolle oder den Benutzer, dem Berechtigungen erteilt, verweigert oder widerrufen werden sollen. Der Objektname kann mit den dreiteiligen Benennungsregeln angegeben werden, die unter [Transact-SQL-Syntaxkonventionen &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md) beschrieben sind.  
  
 TO *principal* [ **,**...*n*]  
 Mindestens ein Prinzipal, dem Berechtigungen erteilt, verweigert oder widerrufen werden sollen. Ein Prinzipal ist der Anmeldename, der Datenbankbenutzer oder die Datenbankrolle.  
  
 FROM *principal* [ **,**...*n*]  
 Mindestens ein Prinzipal, für den Berechtigungen widerrufen werden sollen.  Ein Prinzipal ist der Anmeldename, der Datenbankbenutzer oder die Datenbankrolle. **FROM** kann nur mit der Anweisung **REVOKE** verwendet werden. **TO** kann mit **GRANT**, **DENY** oder **REVOKE** verwendet werden.  
  
 WITH GRANT OPTION  
 Gibt an, dass der Empfänger die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
 CASCADE  
 Gibt an, dass die Berechtigung für den angegebenen Prinzipal und für alle anderen Prinzipale verweigert oder widerrufen wird, denen diese Berechtigung von diesem Prinzipal erteilt wurde. Dies ist erforderlich, wenn der Prinzipal die Berechtigung mit dem Argument **GRANT OPTION** besitzt.  
  
 GRANT OPTION FOR  
 Gibt an, dass die Fähigkeit, die angegebene Berechtigung zu erteilen, aufgehoben wird. Dies ist bei Verwendung des Arguments **CASCADE** erforderlich.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne das Argument **GRANT OPTION** besitzt, wird die Berechtigung selbst aufgehoben.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Erteilen einer Berechtigung muss der Berechtigende entweder über die Berechtigung selbst mit dem Argument **WITH GRANT OPTION** oder über eine höhere Berechtigung verfügen, in der die erteilte Berechtigung impliziert ist.  Objektbesitzer können Berechtigungen für die Objekte erteilen, die sie besitzen. Prinzipale mit der Berechtigung **CONTROL** für ein sicherungsfähiges Element können die Berechtigung für dieses sicherungsfähige Element erteilen.  Mitglieder der festen Datenbankrollen **db_owner** und **db_securityadmin** können jegliche Berechtigungen in der Datenbank erteilen.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Das Verweigern oder Widerrufen von Berechtigungen für ein Prinzipal hat keine Auswirkungen auf Anforderungen, die bereits autorisiert wurden und derzeit ausgeführt werden. Zum sofortigen Einschränken des Zugriffs müssen Sie aktive Anforderungen abbrechen oder aktuelle Sitzungen beenden.  
  
> [!NOTE]  
>  Die meisten festen Serverrollen sind in diesem Release nicht verfügbar. Verwenden Sie stattdessen benutzerdefinierte Datenbankrollen. Anmeldenamen können der festen Serverrolle **sysadmin** nicht hinzugefügt werden. Das Erteilen der Berechtigung **CONTROL SERVER** gleicht der Mitgliedschaft in der festen Serverrolle **sysadmin**.  
  
 Einige Anweisungen erfordern mehrere Berechtigungen. Beispielsweise erfordert das Erstellen einer Tabelle die Berechtigungen **CREATE TABLE** in der Datenbank und **ALTER SCHEMA** für die Tabelle, die die Tabelle enthalten soll.  
  
 In SQL Server PDW werden gespeicherte Prozeduren manchmal ausgeführt, um Benutzeraktionen an die Computeknoten zu verteilen. Aus diesem Grund kann die Berechtigung EXECUTE nicht für eine gesamte Datenbank verweigert werden. (Z.B. schlägt `DENY EXECUTE ON DATABASE::<name> TO <user>;` fehl.) Sie können dies umgehen, indem Sie die EXECUTE-Berechtigung für Benutzerschemas oder spezifische Objekte (Prozeduren) verweigern.  
  
### <a name="implicit-and-explicit-permissions"></a>Implizite und explizite Berechtigungen  
 Eine *explizite Berechtigung* ist eine **GRANT**- oder **DENY**-Berechtigung, die einem Prinzipal durch eine **GRANT**- oder **DENY**-Anweisung zugewiesen wurde.  
  
 Eine *implizite Berechtigung* ist eine **GRANT**- oder **DENY**-Berechtigung, die ein Prinzipal (Anmeldename, Benutzer oder Datenbankrolle) von einer anderen Datenbankrolle geerbt hat.  
  
 Eine implizite Berechtigung kann auch von einer abdeckenden oder übergeordneten Berechtigung geerbt werden. Beispielsweise kann die Berechtigung **UPDATE** von einer Tabelle geerbt werden, wenn die Berechtigung **UPDATE** für das Schema, das die Tabelle enthält, oder die Berechtigung **CONTROL** für die Tabelle vorhanden ist.  
  
### <a name="ownership-chaining"></a>Besitzverkettung  
 Wenn mehrere Datenbankobjekte aufeinander sequenziell zugreifen, wird diese Sequenz als *Kette* bezeichnet. Obwohl solche Ketten nicht unabhängig voneinander vorhanden sind, werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Traversieren der Links in einer Kette durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Berechtigungen für die einzelnen Objekte anders ausgewertet als beim getrennten Zugriff auf die Objekte. Besitzketten haben erhebliche Auswirkungen auf die Sicherheitsverwaltung. Weitere Informationen zu Besitzketten finden Sie unter [Besitzketten](http://msdn.microsoft.com/en-us/library/ms188676\(v=sql11\).aspx) und [Tutorial: Besitzketten und Kontextwechsel](http://msdn.microsoft.com/en-us/library/bb153640\(v=sql11\).aspx).  
  
## <a name="permission-list"></a>Berechtigungsliste  
  
### <a name="server-level-permissions"></a>Berechtigungen auf Serverebene  
 Berechtigungen auf Serverebene können von Anmeldenamen erteilt, verweigert und widerrufen werden.  
  
 **Für Server geltende Berechtigungen**  
  
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
  
 **Berechtigungen,die für Anmeldenamen gelten**  
  
-   CONTROL ON LOGIN  
  
-   ALTER ON LOGIN  
  
-   IMPERSONATE ON LOGIN  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>Berechtigungen auf Datenbankebene  
 Berechtigungen auf Datenbankebene können von Datenbankbenutzern und benutzerdefinierten Datenbankrollen erteilt, verweigert und widerrufen werden.  
  
 **Für alle Datenbankklassen geltende Berechtigungen**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **Für alle Datenbankklassen außer Benutzer geltende Berechtigungen**  
  
-   TAKE OWNERSHIP  
  
 **Nur für die Datenbank geltende Berechtigungen**  
  
-   ALTER ANY DATABASE  
  
-   ALTER ON DATABASE  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   CONNECT ON DATABASE  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **Nur für Benutzer geltende Berechtigungen**  
  
-   IMPERSONATE  
  
 **Für Datenbanken, Schemas und Objekte geltende Berechtigungen**  
  
-   ALTER  
  
-   Delete  
  
-   Führen Sie  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   REFERENCES  
  
 Eine Definition für jede Art der Berechtigung finden Sie unter [Berechtigungen (Datenbank-Engine)](http://msdn.microsoft.com/library/ms191291.aspx).  
  
### <a name="chart-of-permissions"></a>Diagramm der Berechtigungen  
 Alle Berechtigungen werden auf diesem Poster grafisch dargestellt. Dies ist die einfachste Methode, um die geschachtelte Hierarchie von Berechtigungen zu sehen. Zum Beispiel kann die Berechtigung **ALTER ON LOGIN** von sich selbst erteilt werden, wird jedoch auch enthalten, wenn ein Anmeldename die Berechtigung **CONTROL** für diesen Anmeldenamen erhält, oder wenn einem Anmeldenamen die Berechtigung **ALTER ANY LOGIN** erteilt wird.  
  
 ![APS-Poster über Sicherheitsberechtigungen](../../t-sql/statements/media/aps-security-perms-poster.png "APS security permissions poster")  
  
 Dieses Poster können Sie in voller Größe unter [SQL Server PDW Permissions (SQL Server PDW-Berechtigungen)](http://go.microsoft.com/fwlink/?LinkId=244249) im Abschnitt „Dateien“ der APS-Yammer-Website herunterladen (oder per E-Mail von **apsdoc@microsoft.com** anfragen).  
  
## <a name="default-permissions"></a>Standardberechtigungen  
 In der folgenden Liste werden die Standardberechtigungen beschrieben:  
  
-   Wenn ein Anmeldename mit der Anweisung **CREATE LOGIN** erstellt wird, erhält der neue Anmeldename die Berechtigung **CONNECT SQL**.  
  
-   Alle Anmeldenamen sind Mitglieder der Serverrolle **public** und können nicht aus **public** entfernt werden.  
  
-   Wenn ein Datenbankbenutzer mithilfe der Berechtigung **CREATE USER** erstellt wird, erhält der Datenbankbenutzer die Berechtigung **CONNECT** in der Datenbank.  
  
-   Standardmäßig verfügen alle Prinzipale, einschließlich der Rolle **public**, über keine expliziten oder impliziten Berechtigungen.  
  
-   Wenn ein Anmeldename oder ein Benutzer zum Besitzer einer Datenbank oder eines Objekts werden, erhalten diese alle Berechtigungen für die Datenbank bzw. das Objekt. Die Besitzerrechte können nicht geändert werden und sind nicht als explizite Berechtigungen sichtbar. Die Anweisungen **GRANT**, **DENY** und **REVOKE** haben keine Auswirkungen auf Besitzer.  
  
-   Der **sysadmin**-Anmeldename verfügt über alle Berechtigungen auf dem Gerät. Ähnlich wie Besitzerrechte, können **sa**-Berechtigungen nicht geändert werden und sind nicht als explizite Berechtigungen sichtbar. Die Anweisungen **GRANT**, **DENY** und **REVOKE** haben keine Auswirkungen auf den **sa**-Anmeldenamen. Der **sa**-Anmeldename kann nicht umbenannt werden.  
  
-   Die Anweisung **USE** erfordert keine Berechtigungen. Auf allen Datenbanken können alle Prinzipale die Anweisung **USE** ausführen.  
  
##  <a name="Examples"></a> Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. Erteilen einer Berechtigung auf Serverebene für einen Anmeldenamen  
 Die folgenden zwei Anweisungen erteilen einem Anmeldenamen eine Berechtigung auf Serverebene.  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. Erteilen einer Berechtigung auf Serverebene für einen Anmeldenamen  
 Im folgenden Beispiel wird einem Serverprinzipal (ein anderer Anmeldename) eine Berechtigung auf Serverebene für einen Anmeldenamen zugewiesen.  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. Erteilen einer Berechtigung auf Datenbankebene für einen Benutzer  
 Im folgenden Beispiel wird einem Datenbankprinzipal (ein anderer Benutzer) eine Berechtigung auf Datenbankebene für einen Benutzer zugewiesen.  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. Erteilen, Verweigern und Widerrufen einer Berechtigung für ein Schema  
 Die folgende **GRANT**-Anweisung erteilt dem Benutzer Yuen die Berechtigung, Daten aus einer beliebigen Tabelle oder Sicht im dbo-Schema auszuwählen.  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 Die folgende **DENY**-Anweisung verweigert dem Benutzer Yuen die Berechtigung, Daten aus einer beliebigen Tabelle oder Sicht im dbo-Schema auszuwählen. Yuen kann die Daten nicht lesen, selbst wenn er auf eine andere Weise über die Berechtigung verfügt, z.B. über eine Rollenmitgliedschaft.  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 Die folgende **REVOKE**-Anweisung entfernt die **DENY**-Anweisung. Jetzt sind die expliziten Berechtigungen von Yuen neutral. Yuen könnte über eine andere implizite Berechtigung, wie z.B. eine Rollenmitgliedschaft, über die Berechtigung verfügen, Daten aus einer beliebigen Tabelle auszuwählen.  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. Veranschaulichung der optionalen Klausel OBJECT::  
 Da OBJECT die Standardklasse für eine Berechtigungsanweisung ist, sind die folgenden zwei Anweisungen identisch. Die Klausel **OBJECT::** ist optional.  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  

