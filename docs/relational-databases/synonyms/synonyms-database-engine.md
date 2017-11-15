---
title: Synonyme (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords: synonyms [SQL Server], about synonyms
ms.assetid: 6210e1d5-075f-47e4-ac8d-f84bcf26fbc0
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 86fb16833f248731becb9e40f7525281a8b52e94
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="synonyms-database-engine"></a>Synonyme (Datenbankmodul)
  Ein Synonym ist ein Datenbankobjekt, das zu folgenden Zwecken dient:  
  
-   Ein Synonym stellt einen alternativen Namen für ein anderes Datenbankobjekt bereit, das als Basisobjekt bezeichnet wird und auf einem lokalen Server oder Remoteserver gespeichert sein kann.  
  
-   Ein Synonym stellt eine Abstraktionsschicht bereit, die eine Clientanwendung vor Änderungen schützt, die am Namen oder Speicherort des Basisobjekts vorgenommen werden.  
  
 Nehmen Sie z. B. die **Employee** -Tabelle von [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], die auf dem Server **Server1**gespeichert ist. Eine Clientanwendung müsste, um von einem anderen Server, **Server2**, auf diese Tabelle zu verweisen, den vierteiligen Namen **Server1.AdventureWorks.Person.Employee**verwenden. Die Clientanwendung müsste außerdem geändert werden, wenn sich der Speicherort der Tabelle ändert, z. B. in einen anderen Server.  
  
 Um diese beiden Probleme zu vermeiden, können Sie das Synonym **EmpTable**auf **Server2** für die **Employee** -Tabelle auf **Server1**erstellen. Nun muss die Clientanwendung nur den einteiligen Namen **EmpTable**verwenden, um auf die **Employee** -Tabelle zu verweisen. Wenn sich außerdem der Speicherort der **Employee** -Tabelle ändert, müssen Sie das Synonym **EmpTable**ändern, um auf den neuen Speicherort der **Employee** -Tabelle zu verweisen. Da es keine ALTER SYNONYM-Anweisung gibt, müssen Sie zuerst das Synonym **EmpTable**löschen und anschließend mit dem gleichen Namen neu erstellen, aber das Synonym auf den neuen Speicherort der **Employee**-Tabelle verweisen lassen.  
  
 Ein Synonym gehört zu einem Schema, und der Name eines Schemas muss wie andere Objekte in einem Schema eindeutig sein. Sie können Synonyme für die folgenden Datenbankobjekte erstellen:  
  
|||  
|-|-|  
|Gespeicherte Assemblyprozedur (CLR)|Assembly-Tabellenwertfunktion (CLR)|  
|Assemblyskalarfunktion (CLR)|Assemblyaggregatfunktion (CLR)|  
|Replikationsfilterprozedur|Erweiterte gespeicherte Prozedur|  
|SQL-Skalarfunktion|SQL-Tabellenwertfunktion|  
|SQL-Inline-Tabellenwertfunktion|Gespeicherte SQL-Prozedur|  
|Sicht|Tabelle* (benutzerdefiniert)|  
  
 *Enthält lokale und globale temporäre Tabellen  
  
> [!NOTE]  
>  Vierteilige Namen für Funktionsbasisobjekte werden nicht unterstützt.  
  
 Ein Synonym kann nicht das Basisobjekt für ein anderes Synonym sein. Außerdem kann ein Synonym nicht auf eine benutzerdefinierte Aggregatfunktion verweisen.  
  
 Die Bindung zwischen einem Synonym und dem zugehörigen Basisobjekt erfolgt nur mit dem Namen. Alle Überprüfungen auf das Vorhandensein, den Typ und die Berechtigungen für das Basisobjekt werden bis zur Laufzeit verschoben. Deshalb kann das Basisobjekt geändert, gelöscht oder gelöscht und durch ein anderes Objekt, das den gleichen Namen wie das ursprüngliche Basisobjekt hat, ersetzt werden. Betrachten wir als Beispiel das Synonym **MyContacts**, das auf die **Person.Contact** -Tabelle in [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]verweist. Wenn die **Contact** -Tabelle gelöscht und durch die **Person.Contact**-Sicht ersetzt wird, verweist **MyContacts** nun auf die **Person.Contact** -Sicht.  
  
 Verweise auf Synonyme sind nicht schemagebunden. Deshalb kann ein Synonym jederzeit gelöscht werden. Durch das Löschen eines Synonyms besteht jedoch die Gefahr, dass Verweise auf das gelöschte Synonym zurückbleiben. Diese Verweise werden erst zur Laufzeit gefunden.  
  
## <a name="synonyms-and-schemas"></a>Synonyme und Schemas  
 Wenn Sie über ein Standardschema verfügen, das nicht Ihnen gehört, und Sie ein Synonym erstellen möchten, müssen Sie den Synonymnamen mit dem Namen eines Schemas, das Ihnen gehört, qualifizieren. Angenommen, Ihnen gehört ein Schema **x**, aber **y** ist Ihr Standardschema und Sie verwenden die CREATE SYNONYM-Anweisung. In diesem Fall müssen Sie dem Namen des Synonyms das Schema **x**als Präfix voranstellen, anstatt dem Synonym einen einteiligen Namen zu geben. Weitere Informationen zum Erstellen von Synonymen finden Sie unter [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)gespeichert ist.  
  
## <a name="granting-permissions-on-a-synonym"></a>Erteilen von Berechtigungen für Synonyme  
 Nur Besitzer eines Synonyms, Mitglieder der Rollen **db_owner**oder **db_ddladmin** können Berechtigungen für ein Synonym erteilen.  
  
 Sie können eine GRANT-, DENY-, REVOKE-Anweisung für alle oder einige der folgenden Berechtigungen für ein Synonym ausführen:  
  
|||  
|-|-|  
|CONTROL|DELETE|  
|EXECUTE|INSERT|  
|SELECT|TAKE OWNERSHIP|  
|UPDATE|VIEW DEFINITION|  
  
## <a name="using-synonyms"></a>Verwenden von Synonymen  
 Synonyme können anstelle des Basisobjekts, auf das verwiesen wird, in mehreren SQL-Anweisungen und Ausdruckskontexten verwendet werden. Die folgende Tabelle enthält eine Liste dieser Anweisungen und Ausdruckskontexte:  
  
|||  
|-|-|  
|SELECT|INSERT|  
|UPDATE|DELETE|  
|EXECUTE|Untergeordnete SELECT-Anweisungen|  
  
 Wenn Sie Synonyme in den vorher beschriebenen Kontexten verwenden, ist das Basisobjekt davon betroffen. Angenommen, ein Synonym verweist auf ein Basisobjekt, das eine Tabelle darstellt, und Sie fügen eine Zeile in das Synonym ein. In Wirklichkeit fügen Sie dann eine Zeile in die Tabelle ein, auf die verwiesen wird.  
  
> [!NOTE]  
>  Auf ein Synonym, das auf einem Verbindungsserver gespeichert ist, kann nicht verwiesen werden.  
  
 Sie können ein Synonym als Parameter für die OBJECT_ID-Funktion verwenden; die Funktion gibt jedoch die Objekt-ID des Synonyms und nicht das Basisobjekt zurück.  
  
 Sie können in einer DDL-Anweisung nicht auf ein Synonym verweisen. So generieren beispielsweise die folgenden Anweisungen, die auf ein Synonym namens `dbo.MyProduct`verweisen, einen Fehler:  
  
```  
ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null;  
EXEC ('ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null');  
```  
  
 Die folgenden Berechtigungsanweisungen beziehen sich nur auf das Synonym, nicht auf das Basisobjekt.  
  
|||  
|-|-|  
|GRANT|DENY|  
|REVOKE||  
  
 Synonyme sind nicht schemagebunden. Deshalb kann von den folgenden schemagebundenen Ausdruckskontexten nicht auf Synonyme verwiesen werden:  
  
|||  
|-|-|  
|CHECK-Einschränkungen|Berechnete Spalten|  
|Standardausdrücke|Regelausdrücke|  
|Schemagebundene Sichten|Schemagebundene Funktionen|  
  
 Weitere Informationen zu schemagebundenen Funktionen finden Sie unter [Erstellen von benutzerdefinierten Funktionen &#40;Datenbankmodul&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  
## <a name="getting-information-about-synonyms"></a>Abrufen von Informationen zu Synonymen  
 Die sys.synonyms-Katalogsicht enthält einen Eintrag für jedes Synonym in einer bestimmten Datenbank. Diese Katalogsicht macht Synonymmetadaten verfügbar, wie z. B. den Namen des Synonyms und den Namen des Basisobjekts. Weitere Informationen zur **sys.synonyms**-Katalogsicht finden Sie unter [sys.synonyms &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md).  
  
 Mithilfe erweiterter Eigenschaften können Sie Beschreibungs- oder Anweisungstext, Eingabeformate und Formatierungsregeln als Eigenschaften eines Synonyms hinzufügen. Da die Eigenschaft in der Datenbank gespeichert wird, können alle Anwendungen, die die Eigenschaft lesen, das Objekt auf die gleiche Weise auswerten. Weitere Informationen finden Sie unter [sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md).  
  
 Verwenden Sie die OBJECTPROPERTYEX-Funktion, um den Basistyp des Basisobjekts eines Synonyms zu suchen. Weitere Informationen finden Sie unter [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
### <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt den Basistyp des Basisobjekts eines Synonyms zurück, das ein lokales Objekt ist.  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee   
FOR AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyEmployee'), 'BaseType') AS BaseType;  
```  
  
 Das folgende Beispiel gibt den Basistyp des Basisobjekts eines Synonyms zurück, das ein Remoteobjekt auf einem Server mit dem Namen `Server1`ist.  
  
```  
EXECUTE sp_addlinkedserver Server1;  
GO  
CREATE SYNONYM MyRemoteEmployee  
FOR Server1.AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyRemoteEmployee'), 'BaseType') AS BaseType;  
GO  
```  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Erstellen von Synonymen](../../relational-databases/synonyms/create-synonyms.md)  
  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)  
  
 [DROP SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/drop-synonym-transact-sql.md)  
  
  
