---
title: Sortierungen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9154d293ca5b7737a9c80fef0754dcec6e461a46
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="collations"></a>Sortierungen
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Eine Klausel, die auf eine Datenbankdefinition oder eine Spaltendefinition angewendet werden kann, um die Sortierung zu definieren, oder auf einen Zeichenfolgenausdruck, um eine Sortierungsumwandlung anzuwenden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
COLLATE { <collation_name> | database_default }  
<collation_name> :: =   
     { Windows_collation_name } | { SQL_collation_name }  
```  
  
## <a name="arguments"></a>Argumente  
 *Sortierungsname*  
 Der Name der Sortierung, die auf den Ausdruck, die Spaltendefinition oder die Datenbankdefinition angewendet werden soll. *Collation_name* kann nur ein bestimmter *Windows_collation_name* oder ein *SQL_collation_name*. *Collation_name* muss ein Literalwert sein. *Collation_name* kann nicht durch eine Variable oder einen Ausdruck dargestellt werden.  
  
 *Windows_collation_name* ist der Name für eine [Windows-Sortierungsname](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 *SQL_collation_name* ist der Name für eine [SQL Server-Sortierungsname](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Bei Anwendung einer Sortierung auf Datenbankdefinitionsebene können Nur-Unicode-Windows-Sortierungen nicht mit der COLLATE-Klausel verwendet werden.  
  
 **database_default**  
 Bewirkt, dass die COLLATE-Klausel die Sortierung der aktuellen Datenbank erbt.  
  
## <a name="remarks"></a>Hinweise  
 Die COLLATE-Klausel kann auf mehreren Ebenen angegeben werden. Dabei handelt es sich z. B. um:  
  
1.  Erstellen oder Ändern einer Datenbank.  
  
     Sie können die COLLATE-Klausel der CREATE DATABASE- oder ALTER DATABASE-Anweisung verwenden, um die Standardsortierung der Datenbank anzugeben. Sie können eine Sortierung auch dann angeben, wenn Sie eine Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen. Wenn Sie keine Sortierung angeben, wird der Datenbank die Standardsortierung der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugewiesen.  
  
    > [!NOTE]  
    >  Windows-nur-Unicode-Sortierungen können nur mit der COLLATE-Klausel verwendet werden, zum Anwenden von Sortierungen auf die **Nchar**, **Nvarchar**, und **Ntext** Datentypen auf Spaltenebene und Ausdrucksebene Daten. Sie können mit der COLLATE-Klausel verwendet werden, um die Sortierung einer Datenbank oder Serverinstanz zu ändern.  
  
2.  Erstellen oder Ändern einer Tabellenspalte.  
  
     Sie können mithilfe der COLLATE-Klausel der CREATE TABLE oder ALTER TABLE-Anweisung für jede Zeichenfolgenspalte eine Sortierung angeben. Sie können eine Sortierung auch dann angeben, wenn Sie eine Tabelle mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen. Wenn Sie keine Sortierung angeben, wird der Spalte die Standardsortierung der Datenbank zugewiesen.  
  
     Sie können auch die `database_default` Option in der COLLATE-Klausel aus, um anzugeben, dass eine Spalte in einer temporären Tabelle die standardsortierung der aktuellen Benutzerdatenbank für die Verbindung verwenden **Tempdb**.  
  
3.  Umwandeln der Sortierung eines Ausdrucks.  
  
     Sie können die COLLATE-Klausel verwenden, um einen Zeichenausdruck auf eine bestimmte Sortierung anzuwenden. Zeichenliteralen und Variablen wird die Standardsortierung der aktuellen Datenbank zugewiesen. Spaltenverweisen wird die Definitionssortierung der Spalte zugewiesen.  
  
 Die Sortierung eines Bezeichners hängt von der Ebene ab, auf der er definiert ist. Bezeichnern von Objekten auf Instanzebene, wie z. B. Anmeldenamen und Datenbanknamen, wird die Standardsortierung der Instanz zugewiesen. Bezeichnern von Objekten innerhalb einer Datenbank, wie z. B. Tabellen, Sichten und Spaltennamen, wird die Standardsortierung der Datenbank zugewiesen. Beispielsweise können in einer Datenbank mit einer Sortierung mit Unterscheidung nach Groß-/Kleinschreibung zwei Tabellen mit gleichen Namen, die sich nur durch verschiedene Groß-/Kleinschreibung unterscheiden, erstellt werden; in einer Datenbank mit einer Sortierung ohne Unterscheidung nach Groß-/Kleinschreibung ist dies jedoch nicht möglich. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 Variablen, GOTO-Marken, temporär gespeicherte Prozeduren und temporäre Tabellen können erstellt werden, wenn der Verbindungskontext einer Datenbank zugeordnet ist. Anschließend kann darauf verwiesen werden, wenn zum Kontext einer anderen Datenbank gewechselt wurde. Die Bezeichner von Variablen, GOTO-Marken, temporär gespeicherten Prozeduren und temporären Tabellen befinden sich in der Standardsortierung der Serverinstanz.  
  
 Die COLLATE-Klausel angewendet werden kann, nur für die **Char**, **Varchar**, **Text**, **Nchar**, **Nvarchar** , und **Ntext** Datentypen.  
  
 COLLATE verwendet *Collate_name* zum Verweisen auf den Namen des SQL Server-Sortierung oder der Windows-Sortierung auf den Ausdruck, die Spaltendefinition oder die Datenbankdefinition angewendet werden soll. *Collation_name* kann nur ein bestimmter *Windows_collation_name* oder ein *SQL_collation_name* und der Parameter muss einen Literalwert enthalten. *Collation_name* kann nicht durch eine Variable oder einen Ausdruck dargestellt werden.  
  
 Sortierungen werden außer beim Setup in der Regel durch den Sortierungsnamen identifiziert. Beim Setup geben Sie stattdessen den Sortierungskennzeichner (das Gebietsschema) für Windows-Sortierungen und dann die Sortierungsoptionen an, z. B. Unterscheidung nach Groß- und Kleinschreibung und Akzenten.  
  
 Sie können die Systemfunktion ausführen [Fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) auf eine Liste mit allen gültigen Namen für Windows- und SQL Server-Sortierungen abzurufen:  
  
```  
SELECT name, description  
FROM fn_helpcollations();  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt nur Codepages, die vom zugrunde liegenden Betriebssystem unterstützt werden. Wenn Sie eine Aktion ausführen, die von Sortierungen abhängt, muss die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierung, die von dem Objekt verwendet wird, auf das verwiesen wird, eine Codepage verwenden, die vom Betriebssystem des Computers unterstützt wird. Mögliche Aktionen sind:  
  
-   Angeben einer Standardsortierung für eine Datenbank, wenn Sie die Datenbank erstellen oder ändern.  
  
-   Angeben einer Sortierung für eine Spalte, wenn Sie eine Tabelle erstellen oder ändern.  
  
-   Beim Wiederherstellen oder Anfügen einer Datenbank, die standardsortierung der Datenbank und die Sortierungen aller **Char**, **Varchar**, und **Text** Spalten oder Parameter in der Datenbank muss vom Betriebssystem unterstützt werden.  
  
     Codepageübersetzungen werden für unterstützt **Char** und **Varchar** Datentypen, jedoch nicht für **Text** -Datentyp. Datenverlust während der Codepageübersetzung wird nicht gemeldet.  
  
 Wenn die angegebene Sortierung oder die von dem referenzierten Objekt verwendete Sortierung eine Codepage, die nicht von Windows unterstützt verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird eine Fehlermeldung angezeigt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-specifying-collation-during-a-select"></a>A. Angeben einer Sortierung während einer Auswahl  
 Im folgenden Beispiel wird eine einfache Tabelle erstellt, und 4 Zeilen werden eingefügt. Dann werden im Beispiel zwei Sortierungen bei der Auswahl von Daten aus der Tabelle angewendet, um zu zeigen, wie `Chiapas` unterschiedlich sortiert wird.  
  
```tsql  
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
 Für zusätzliche Beispiele, in denen **COLLATE**, finden Sie unter [CREATE DATABASE &#40; SQL Server Transact-SQL &#41; ](../../t-sql/statements/create-database-sql-server-transact-sql.md) Beispiel **G. Erstellen einer Datenbank und Angeben eines sortierungsnamens und Optionen**, und [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) Beispiel **V. Ändern der spaltensortierung**.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)   
 [Rangfolge von Sortierungen &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [Konstanten &#40; Transact-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Table &#40; Transact-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)  
  
  

