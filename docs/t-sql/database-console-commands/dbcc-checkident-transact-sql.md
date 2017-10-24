---
title: DBCC CHECKIDENT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKIDENT
- DBCC CHECKIDENT
- CHECKIDENT_TSQL
- DBCC_CHECKIDENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checking identity values
- reseeding identity values
- resetting identity values
- identity values [SQL Server]
- identity values [SQL Server], checking
- modifying identity values
- current identity values
- DBCC CHECKIDENT statement
- identity values [SQL Server], reseeding
- reporting current identity values
ms.assetid: 2c00ee51-2062-4e47-8b19-d90f524c6427
caps.latest.revision: 63
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d81aa2c26cf693d8ed5613c2aceb970a54db5aca
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkident-transact-sql"></a>DBCC CHECKIDENT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Überprüft den aktuellen Identitätswert der angegebenen Tabelle in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und ändert ihn gegebenenfalls. Sie können DBCC CHECKIDENT auch verwenden, um manuell einen neuen aktuellen Identitätswert für die Identitätsspalte festzulegen.  
   
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DBCC CHECKIDENT   
 (   
    table_name  
        [, { NORESEED | { RESEED [, new_reseed_value ] } } ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
 *table_name*  
 Der Name der Tabelle, deren aktueller Identitätswert überprüft werden soll. Die angegebene Tabelle muss eine Identitätsspalte enthalten. Tabellennamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Zwei oder drei Teilnamen müssen begrenzt sein, z. B. "Person.AddressType" oder [Person.AddressType].   
  
 NORESEED  
 Gibt an, dass der aktuelle Identitätswert nicht geändert werden soll.  
  
 RESEED  
 Gibt an, dass der aktuelle Identitätswert geändert werden soll.  
  
 *new_reseed_value*  
 Der neue Wert, der als aktueller Wert der Identitätsspalte verwendet werden soll.  
  
 WITH NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Hinweise  
 Die spezifischen Korrekturen, die am aktuellen Identitätswert vorgenommen werden, sind abhängig von den Parameterangaben.  
  
|DBCC CHECKIDENT-Befehl|Durchgeführte Identitätskorrekturen|  
|-----------------------------|---------------------------------------------|  
|DBCC CHECKIDENT ( *Table_name*, NORESEED)|Der aktuelle Identitätswert wird nicht zurückgesetzt. DBCC CHECKIDENT gibt den aktuellen Identitätswert und den aktuellen maximalen Wert der Identitätsspalte zurück. Wenn die beiden Werte nicht gleich sind, sollten Sie den Identitätswert zurücksetzen, um mögliche Fehler oder Lücken in der Wertesequenz zu vermeiden.|  
|DBCC CHECKIDENT ( *Table_name* )<br /><br /> oder<br /><br /> DBCC CHECKIDENT ( *Table_name*, RESEED)|Wenn der aktuelle Identitätswert für eine Tabelle kleiner ist als der maximale in der Identitätsspalte gespeicherte Identitätswert, wird er auf den maximalen Wert in der Identitätsspalte zurückgesetzt. Weitere Informationen finden Sie im Abschnitt "Ausnahmen" weiter unten.|  
|DBCC CHECKIDENT ( *Table_name*, RESEED, *New_reseed_value* )|Aktueller Identitätswert wird festgelegt, um die *New_reseed_value*. Wenn keine Zeilen, da die Tabelle erstellt wurde, oder die erste Zeile, die nach dem Ausführen von DBCC CHECKIDENT eingefügt wird, wenn alle Zeilen mit TRUNCATE TABLE-Anweisung entfernt wurden verwendet, in die Tabelle eingefügt wurden *New_reseed_value* als Identität.<br /><br /> Wenn Zeilen in der Tabelle vorhanden sind, wird die nächste Zeile eingefügt, mit der *New_reseed_value* Wert. In Version [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] und früher: wird verwendet, die nächste eingefügte Zeile *New_reseed_value* + [aktuelles Inkrement](../../t-sql/functions/ident-incr-transact-sql.md) Wert.<br /><br /> Bei einer nicht leeren Tabelle kann das Festlegen des Identitätswertes auf eine Zahl, die kleiner ist als der maximale Wert in der Identitätsspalte, zu einer der folgenden Bedingungen führen:<br /><br /> – Wenn eine PRIMARY KEY- oder UNIQUE-Einschränkung für die Identitätsspalte vorhanden ist, wird die Fehlermeldung 2627 bei späteren einfügungsvorgängen in die Tabelle generiert werden, da die generierten Identitätswert mit vorhandenen Werten in Konflikt steht.<br /><br /> – Wenn eine PRIMARY KEY- oder UNIQUE-Einschränkung nicht vorhanden ist, führt die spätere einfügungsvorgängen zu doppelten Identitätswerten.|  
  
## <a name="exceptions"></a>Ausnahmen  
 In der folgenden Tabelle sind Bedingungen aufgeführt, unter denen DBCC CHECKIDENT den aktuellen Identitätswert nicht automatisch zurücksetzt. Außerdem werden Methoden für das Zurücksetzen des Wertes bereitgestellt.  
  
|Bedingung|Methoden zum Zurücksetzen|  
|---------------|-------------------|  
|Der aktuelle Identitätswert ist größer als der maximale Wert in der Tabelle.|Führen Sie DBCC CHECKIDENT (*Table_name*, NORESEED) zum Ermitteln der aktuellen maximalen Wert in der Spalte, und geben Sie diesen Wert als den *New_reseed_value* in einem DBCC CHECKIDENT (*Tabelle_ Namen*, RESEED,*New_reseed_value*) Befehl.<br /><br /> -ODER-<br /><br /> Führen Sie DBCC CHECKIDENT (*Table_name*, RESEED,*New_reseed_value*) mit *New_reseed_value* auf einen sehr niedrigen Wert festgelegt, und führen Sie DBCC CHECKIDENT ( *TABLE_NAME*, RESEED) auf den Wert zu korrigieren.|  
|Alle Zeilen werden aus der Tabelle gelöscht.|Führen Sie DBCC CHECKIDENT (*Table_name*, RESEED,*New_reseed_value*) mit *New_reseed_value* auf den gewünschten Anfangswert festgelegt.|  
  
## <a name="changing-the-seed-value"></a>Ändern des Ausgangswerts  
 Der Ausgangswert ist der Wert, der für die erste in die Tabelle geladene Zeile in eine Identitätsspalte eingefügt wird. Alle nachfolgenden Zeilen enthalten den aktuellen Identitätswert zuzüglich des inkrementellen Werts, wobei der aktuelle Identitätswert der letzte Identitätswert ist, der für die Tabelle oder Sicht generiert wurde.  
  
 Mit DBCC CHECKIDENT können Sie folgende Aufgaben nicht ausführen:  
  
-   Ändern des ursprünglichen Ausgangswerts, der für eine Identitätsspalte angegeben wurde, als die Tabelle oder die Sicht erstellt wurde.  
  
-   Zuweisen von neuen Ausgangswerten zu vorhandenen Zeilen in einer Tabelle oder Sicht.  
  
 Um den ursprünglichen Ausgangswert zu ändern und vorhandenen Zeilen neue Ausgangswerte zuzuweisen, müssen Sie die Identitätsspalte löschen und sie unter Angabe des neuen Ausgangswerts neu erstellen. Wenn die Tabelle Daten enthält, werden die ID-Nummern zu den vorhandenen Zeilen mit den angegebenen Ausgangswerten und inkrementellen Werten hinzugefügt. Die Reihenfolge, in der die Zeilen aktualisiert werden, ist nicht sichergestellt.  
  
## <a name="result-sets"></a>Resultsets  
 Unabhängig davon, ob eine der Optionen für eine Tabelle festgelegt ist, die eine Identitätsspalte beinhaltet, gibt DBCC CHECKIDENT die folgende Meldung für alle Vorgänge zurück, sofern kein neuer Ausgangswert angegeben ist.  
  
`Checking identity information: current identity value '\<current identity value>', current column value '\<current column value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
 Wenn DBCC CHECKIDENT verwendet wird, geben Sie einen neuen Ausgangswerts mithilfe von RESEED *New_reseed_value*, wird die folgende Meldung zurückgegeben.  
  
`Checking identity information: current identity value '\<current identity value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Berechtigungen  
 Aufrufer muss Besitzer des Schemas mit der Tabelle oder ein Mitglied der **Sysadmin** festen Serverrolle die **Db_owner** feste Datenbankrolle oder der **Db_ddladmin** behoben die Datenbankrolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-resetting-the-current-identity-value-if-it-is-needed"></a>A. Zurücksetzen des aktuellen Identitätswertes, sofern dies erforderlich ist  
 Im folgenden Beispiel wird, falls erforderlich, der aktuelle Identitätswert der angegebenen Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank zurückgesetzt.  
  
```  
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType');  
GO  
```  
  
### <a name="b-reporting-the-current-identity-value"></a>B. Anzeigen des aktuellen Identitätswertes  
 Im folgenden Beispiel wird der aktuelle Identitätswert in der angegebenen Tabelle der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank angezeigt. Ein fehlerhafter Identitätswert wird jedoch nicht korrigiert.  
  
```  
USE AdventureWorks2012;   
GO  
DBCC CHECKIDENT ('Person.AddressType', NORESEED);   
GO  
  
```  
  
### <a name="c-forcing-the-current-identity-value-to-a-new-value"></a>C. Festlegen des aktuellen Identitätswertes auf einen neuen Wert  
 Im folgenden Beispiel wird der aktuelle Identitätswert in der Spalte `AddressTypeID` in der Tabelle `AddressType` auf den Wert 10 festgelegt. Da die Tabelle vorhandene Zeilen hat, verwendet die nächste eingefügte Zeile 11 als Wert, also den neuen, aktuellen inkrementellen Wert, der für den Spaltenwert plus 1 definiert ist.  
  
```  
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType', RESEED, 10);  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
[Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md)  
[USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
[IDENT_SEED &#40; Transact-SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)  
[IDENT_INCR &#40; Transact-SQL &#41;](../../t-sql/functions/ident-incr-transact-sql.md)  
  
  

