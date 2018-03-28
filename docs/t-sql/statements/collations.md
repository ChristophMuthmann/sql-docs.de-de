---
title: Sortierungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COLLATE
- COLLATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
caps.latest.revision: ''
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a59320941ecd488abbaa728968a1326525682839
ms.sourcegitcommit: 3ed9be04cc7fb9ab1a9ec230c298ad2932acc71b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/17/2018
---
# <a name="collations"></a>Sortierungen
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Eine Klausel, die auf eine Datenbankdefinition oder eine Spaltendefinition angewendet werden kann, um die Sortierung zu definieren, oder auf einen Zeichenfolgenausdruck, um eine Sortierungsumwandlung anzuwenden.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
COLLATE { <collation_name> | database_default }  
<collation_name> :: =   
     { Windows_collation_name } | { SQL_collation_name }  
```  
  
## <a name="arguments"></a>Argumente  
 *collation_name*  
 Der Name der Sortierung, die auf den Ausdruck, die Spaltendefinition oder die Datenbankdefinition angewendet werden soll. *collation_name* kann nur ein bestimmter *Windows_collation_name* oder ein *SQL_collation_name* sein. *collation_name* muss ein Literalwert sein. *collation_name* kann nicht durch eine Variable oder einen Ausdruck dargestellt werden.  
  
 *Windows_collation_name* ist der Name für einen [Windows-Sortierungsnamen](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 *SQL_collation_name* ist der Name für einen [SQL Server-Sortierungsnamen](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Bei Anwendung einer Sortierung auf Datenbankdefinitionsebene können Nur-Unicode-Windows-Sortierungen nicht mit der COLLATE-Klausel verwendet werden.  
  
 **database_default**  
 Bewirkt, dass die COLLATE-Klausel die Sortierung der aktuellen Datenbank erbt.  
  
## <a name="remarks"></a>Remarks  
 Die COLLATE-Klausel kann auf mehreren Ebenen angegeben werden. Dabei handelt es sich z. B. um:  
  
1.  Erstellen oder Ändern einer Datenbank.  
  
     Sie können die COLLATE-Klausel der CREATE DATABASE- oder ALTER DATABASE-Anweisung verwenden, um die Standardsortierung der Datenbank anzugeben. Sie können eine Sortierung auch dann angeben, wenn Sie eine Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen. Wenn Sie keine Sortierung angeben, wird der Datenbank die Standardsortierung der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugewiesen.  
  
    > [!NOTE]  
    >  Nur-Unicode-Sortierungen von Windows können nur mit der COLLATE-Klausel verwendet werden, um Sortierungen auf die Datentypen **nchar**, **nvarchar** und **ntext** bei Daten auf Spalten- und Ausdrucksebene anzuwenden. Sie können nicht mit der COLLATE-Klausel verwendet werden, um die Sortierung einer Datenbank oder Serverinstanz zu ändern.  
  
2.  Erstellen oder Ändern einer Tabellenspalte.  
  
     Sie können mithilfe der COLLATE-Klausel der CREATE TABLE oder ALTER TABLE-Anweisung für jede Zeichenfolgenspalte eine Sortierung angeben. Sie können eine Sortierung auch dann angeben, wenn Sie eine Tabelle mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen. Wenn Sie keine Sortierung angeben, wird der Spalte die Standardsortierung der Datenbank zugewiesen.  
  
     Sie können außerdem die Option `database_default` in der COLLATE-Klausel verwenden, um anzugeben, dass für eine Spalte einer temporären Tabelle anstelle von **tempdb** die Standardsortierung der aktuellen Benutzerdatenbank für die Verbindung verwendet wird.  
  
3.  Umwandeln der Sortierung eines Ausdrucks.  
  
     Sie können die COLLATE-Klausel verwenden, um einen Zeichenausdruck auf eine bestimmte Sortierung anzuwenden. Zeichenliteralen und Variablen wird die Standardsortierung der aktuellen Datenbank zugewiesen. Spaltenverweisen wird die Definitionssortierung der Spalte zugewiesen.  
  
 Die Sortierung eines Bezeichners hängt von der Ebene ab, auf der er definiert ist. Bezeichnern von Objekten auf Instanzebene, wie z. B. Anmeldenamen und Datenbanknamen, wird die Standardsortierung der Instanz zugewiesen. Bezeichnern von Objekten innerhalb einer Datenbank, wie z. B. Tabellen, Sichten und Spaltennamen, wird die Standardsortierung der Datenbank zugewiesen. Beispielsweise können in einer Datenbank mit einer Sortierung mit Unterscheidung nach Groß-/Kleinschreibung zwei Tabellen mit gleichen Namen, die sich nur durch verschiedene Groß-/Kleinschreibung unterscheiden, erstellt werden; in einer Datenbank mit einer Sortierung ohne Unterscheidung nach Groß-/Kleinschreibung ist dies jedoch nicht möglich. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 Variablen, GOTO-Marken, temporär gespeicherte Prozeduren und temporäre Tabellen können erstellt werden, wenn der Verbindungskontext einer Datenbank zugeordnet ist. Anschließend kann darauf verwiesen werden, wenn zum Kontext einer anderen Datenbank gewechselt wurde. Die Bezeichner von Variablen, GOTO-Marken, temporär gespeicherten Prozeduren und temporären Tabellen befinden sich in der Standardsortierung der Serverinstanz.  
  
 Die COLLATE-Klausel gilt nur für die Datentypen **char**, **varchar**, **text**, **nchar**, **nvarchar** und **ntext**.  
  
 COLLATE verwendet *collate_name*, um den Namen der SQL Server-Sortierung oder der Windows-Sortierung anzugeben, die auf den Ausdruck, die Spaltendefinition oder die Datenbankdefinition angewendet werden soll. *collation_name* kann nur ein bestimmter *Windows_collation_name* oder ein *SQL_collation_name* sein und der Parameter muss einen Literalwert enthalten. *collation_name* kann nicht durch eine Variable oder einen Ausdruck dargestellt werden.  
  
 Sortierungen werden außer beim Setup in der Regel durch den Sortierungsnamen identifiziert. Geben Sie beim Setup stattdessen den Sortierungskennzeichner (das Gebietsschema) für Windows-Sortierungen und dann die Sortierungsoptionen an, z.B. Unterscheidung nach Groß-/Kleinschreibung oder Akzenten.  
  
 Sie können die [fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)-Systemfunktion ausführen, um eine Liste aller gültigen Namen für Windows- und SQL Server-Sortierungen abzurufen:  
  
```sql  
SELECT name, description  
FROM fn_helpcollations();  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt nur Codepages, die vom zugrunde liegenden Betriebssystem unterstützt werden. Wenn Sie eine Aktion ausführen, die von Sortierungen abhängt, muss die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierung, die von dem Objekt verwendet wird, auf das verwiesen wird, eine Codepage verwenden, die vom Betriebssystem des Computers unterstützt wird. Mögliche Aktionen sind:  
  
-   Angeben einer Standardsortierung für eine Datenbank, wenn Sie die Datenbank erstellen oder ändern.  
  
-   Angeben einer Sortierung für eine Spalte, wenn Sie eine Tabelle erstellen oder ändern.  
  
-   Beim Wiederherstellen oder Anfügen einer Datenbank müssen die Standardsortierung der Datenbank und die Sortierungen aller Spalten und Parameter, die zur Datenbank gehören und den Datentyp **char**, **varchar** oder **text** aufweisen, vom Betriebssystem unterstützt werden.  
  
> [!NOTE]
> Die Serversortierung der verwalteten Azure SQL-Datenbank-Instanz lautet **SQL_Latin1_General_CP1_CI_AS** und kann nicht geändert werden.

> [!NOTE]
> Codepageübersetzungen werden für die Datentypen **char** und **varchar**, nicht jedoch für den **text**-Datentyp unterstützt. Datenverlust während der Codepageübersetzung wird nicht gemeldet.  
  
> [!NOTE]
> Wenn die angegebene Sortierung oder die Sortierung, die von dem Objekt verwendet wird, auf das verwiesen wird, eine Codepage verwendet, die nicht von Windows unterstützt wird, zeigt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler an.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-specifying-collation-during-a-select"></a>A. Angeben einer Sortierung während einer Auswahl  
 Im folgenden Beispiel wird eine einfache Tabelle erstellt, und 4 Zeilen werden eingefügt. Dann werden im Beispiel zwei Sortierungen bei der Auswahl von Daten aus der Tabelle angewendet, um zu zeigen, wie `Chiapas` unterschiedlich sortiert wird.  
  
```sql  
CREATE TABLE Locations  
(Place varchar(15) NOT NULL);  
GO  
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')  
                             , ('Cinco Rios'), ('California');  
GO  
--Apply an typical collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Latin1_General_CS_AS_KS_WS ASC;  
GO  
-- Apply a Spanish collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Traditional_Spanish_ci_ai ASC;  
GO  
```  

Dies sind die Ergebnisse der ersten Abfrage.  
  
```
Place 
------------- 
California 
Chiapas 
Cinco Rios 
Colima
```  
  
Dies sind die Ergebnisse der zweiten Abfrage.  
 
```
Place 
------------- 
California 
Cinco Rios 
Colima 
Chiapas
```  
  
### <a name="b-additional-examples"></a>B. Zusätzliche Beispiele  
 Zusätzliche Beispiele zur Verwendung von **COLLATE** finden Sie unter [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md#examples) in Beispiel **G. Erstellen einer Datenbank, Angeben eines Sortierungsnamens und Optionen**, und unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md#alter_column) in Beispiel **V. Ändern der Spaltensortierung**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)    
 [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)    
 [Rangfolge von Sortierungen &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)     
 [Constants &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)     
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)     
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)     
 [DEKLARIEREN SIE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)     
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)     
  
  
