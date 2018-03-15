---
title: CREATE SEQUENCE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SEQUENCE
- CREATE SEQUENCE
- SEQUENCE_TSQL
- CREATE_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SEQUENCE statement
- sequence number object, creating
- sequence object
- number, sequence
ms.assetid: 419f907b-8a72-4d6c-80cb-301df44c24c1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ab2f4258d60f1653a102f5f9cc51d4263fcafc93
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-sequence-transact-sql"></a>CREATE SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Erstellt ein Sequenzobjekt und gibt dessen Eigenschaften an. Als Sequenz wird ein benutzerdefiniertes schemagebundenes Objekt bezeichnet, das eine Sequenz numerischer Werte anhand der Spezifikation generiert, mit der die Sequenz erstellt wurde. Die Sequenz numerischer Werte wird in aufsteigender oder absteigender Reihenfolge in einem definierten Intervall generiert und kann so konfiguriert werden, dass sie beim Erreichen des Endes neu gestartet wird (Zyklus). Sequenzen werden anders als Identitätsspalten keinen bestimmten Tabellen zugeordnet. Anwendungen verweisen auf ein Sequenzobjekt, um dessen nächsten Wert abzurufen. Die Beziehung zwischen Sequenzen und Tabellen wird von der Anwendung gesteuert. Benutzeranwendungen können auf ein Sequenzobjekt verweisen und die Werte in mehreren Zeilen und Tabellen koordinieren.  
  
 Im Unterschied zu Identitätsspaltenwerten, die beim Einfügen von Zeilen generiert werden, kann eine Anwendung durch Aufrufen der [NEXT VALUE FOR-Funktion](../../t-sql/functions/next-value-for-transact-sql.md) die nächste Sequenznummer abrufen, ohne die Zeile einzufügen. Mit [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) können Sie mehrere Sequenznummern gleichzeitig abrufen.  
  
 Informationen und Szenarien, in denen die **CREATE SEQUENCE** -Funktion und die **NEXT VALUE FOR** -Funktion verwendet werden, finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE SEQUENCE [schema_name . ] sequence_name  
    [ AS [ built_in_integer_type | user-defined_integer_type ] ]  
    [ START WITH <constant> ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE [ <constant> ] } | { NO MINVALUE } ]  
    [ { MAXVALUE [ <constant> ] } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *sequence_name*  
 Gibt den eindeutigen Namen der Sequenz in der Datenbank an. Der Typ ist **sysname**.  
  
 [ built_in_integer_type | user-defined_integer_type  
 Eine Sequenz kann als beliebiger ganzzahliger Typ definiert werden. Die folgenden Typen sind zulässig.  
  
-   **tinyint**: von 0 bis 255  
  
-   **smallint**: von –32.768 bis 32.767  
  
-   **int**: von –2.147.483.648 bis 2.147.483.647  
  
-   **bigint**: von –9.223.372.036.854.775.808 bis 9.223.372.036.854.775.807  
  
-   **decimal** und **numeric** mit einem Bereich von 0.  
  
-   Ein beliebiger benutzerdefinierter Datentyp (Aliastyp), der auf einem der zulässigen Typen basiert.  
  
 Wird kein Datentyp bereitgestellt, wird der **bigint**-Datentyp als Standardtyp verwendet.  
  
 START WITH \<constant>  
 Der erste Wert, der vom Sequenzobjekt zurückgegeben wird. Der **START**-Wert muss kleiner oder gleich dem maximalen und größer oder gleich dem minimalen Wert des Sequenzobjekts sein. Der Standardstartwert eines neuen Sequenzobjekts ist gleich dem minimalen Wert eines aufsteigenden Sequenzobjekts und dem maximalen Wert eines absteigenden Sequenzobjekts.  
  
 INCREMENT BY \<constant>  
 Der Wert, mit dem der Wert des Sequenzobjekts bei jedem Aufruf der **NEXT VALUE FOR**-Funktion inkrementiert (oder bei negativem Wert dekrementiert) wird. Wenn als Inkrement ein negativer Wert verwendet wird, ist der Wert des Sequenzobjekts absteigend, andernfalls ist er aufsteigend. Das Inkrement kann nicht 0 sein. Das Standardinkrement für ein neues Sequenzobjekt ist 1.  
  
 [ MINVALUE \<constant> | **NO MINVALUE** ]  
 Gibt die Grenzen für das Sequenzobjekt an. Der minimale Standardwert eines neuen Sequenzobjekts ist gleich dem minimalen Wert für den Datentyp des Sequenzobjekts. Dieser ist für den **tinyint** -Datentyp 0 und für alle anderen Datentypen eine negative Zahl.  
  
 [ MAXVALUE \<constant> | **NO MAXVALUE**  
 Gibt die Grenzen für das Sequenzobjekt an. Der maximale Standardwert eines neuen Sequenzobjekts ist gleich dem maximalen Wert für den Datentyp des Sequenzobjekts.  
  
 [ CYCLE | **NO CYCLE** ]  
 Eigenschaft, die angibt, ob das Sequenzobjekt vom minimalen Wert (oder bei absteigenden Sequenzobjekten vom maximalen Wert) neu gestartet oder ob eine Ausnahme ausgelöst werden soll, wenn der minimale oder maximale Wert überschritten wird. Die Standardzyklusoption für neue Sequenzobjekte ist NO CYCLE.  
  
 Beachten Sie, dass der Durchlauf ab dem minimalen oder maximalen Wert neu startet, und nicht ab dem Startwert.  
  
 [ **CACHE** [\<constant> ] | NO CACHE ]  
 Erhöht die Leistung für Anwendungen, die Sequenzobjekte verwenden, indem die Anzahl der Datenträger-E/As verringert wird, die zum Generieren von Sequenznummern erforderlich sind. Der Standardwert ist CACHE.  
  
 Wenn beispielsweise die Cachegröße 50 ausgewählt wird, werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht 50 einzelne Werte zwischengespeichert. Es werden lediglich der aktuelle Wert und die Anzahl der im Cache verbleibenden Werte zwischengespeichert. Daher ist der zum Speichern des Caches erforderliche Arbeitsspeicher immer doppelt so groß wie zwei Instanzen des Sequenzobjekt-Datentyps.  
  
> [!NOTE]  
>  Wenn die Cacheoption aktiviert wird, ohne eine Cachegröße anzugeben, wählt das Datenbankmodul eine Größe aus. Benutzer sollten sich jedoch nicht darauf verlassen, dass die Auswahl konsistent ist. [!INCLUDE[msCoName](../../includes/msconame-md.md)] könnte die Methode zur Berechnung der Cachegröße ohne vorherige Ankündigung ändern.  
  
 Bei Erstellung mit der **CACHE**-Option kann ein unerwartetes Herunterfahren (z.B. durch einen Stromausfall) möglicherweise zum Verlust der im Cache verbleibenden Sequenznummern führen.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Sequenznummern werden außerhalb des Bereichs der aktuellen Transaktion generiert. Sie werden unabhängig davon genutzt, ob ein Commit oder ein Rollback für die Transaktion ausgeführt wird, die die Sequenznummer verwendet.  
  
### <a name="cache-management"></a>Cacheverwaltung  
 Um die Leistung zu verbessern, ordnet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anzahl der durch das **CACHE**-Argument angegebenen Sequenznummern zu.  
  
 Beispielsweise wird eine neue Sequenz mit dem Startwert 1 und einer Cachegröße von 15 erstellt. Wenn der erste Wert benötigt wird, werden die Werte 1 bis 15 vom Arbeitsspeicher verfügbar gemacht. Der letzte zwischengespeicherte Wert (15) wird in die Systemtabellen auf dem Datenträger geschrieben. Wenn alle 15 Zahlen verwendet werden, verursacht die nächste Anforderung (für den Wert 16), dass der Cache erneut zugeordnet wird. Der neue zuletzt zwischengespeicherte Wert (30) wird in die Systemtabellen geschrieben.  
  
 Wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] nach der Verwendung von 22 Zahlen beendet wird, wird die nächste beabsichtigte Sequenznummer im Arbeitsspeicher (23) in die Systemtabellen geschrieben und ersetzt die zuvor gespeicherte Zahl.  
  
 Nachdem SQL Server neu gestartet wurde und eine Sequenznummer benötigt wird, wird die Startzahl aus den Systemtabellen (23) gelesen. Die Cacheanzahl von 15 Zahlen (23 - 38) wird dem Arbeitsspeicher zugeordnet, und die nächste Nicht-Cache-Zahl (39) wird in die Systemtabellen geschrieben.  
  
 Wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] bei einem Ereignis unerwartet beendet wird, z.B. bei einem Stromausfall, startet die Sequenz mit der aus den Systemtabellen gelesenen Zahl (39) neu. Alle dem Arbeitsspeicher zugeordneten Sequenznummern (die nie von einem Benutzer oder einer Anwendung angefordert wurden) gehen verloren. Diese Funktion verursacht möglicherweise Lücken, garantiert aber, dass ein Wert nie zweimal für ein einzelnes Sequenzobjekt ausgegeben wird, sofern er nicht als **CYCLE** definiert ist oder manuell neu gestartet wird.  
  
 Der Cache wird im Arbeitsspeicher verwaltet, indem der aktuelle Wert (der letzte ausgegebene Wert) und die Anzahl der Werte im Cache nachverfolgt werden. Daher ist der vom Cache verwendete Arbeitsspeicher immer doppelt so groß wie zwei Instanzen des Sequenzobjekt-Datentyps.  
  
 Wenn das CACHE-Argument auf **NO CACHE** festgelegt wird, wird der aktuelle Sequenzwert bei jeder Verwendung einer Sequenz in die Systemtabellen geschrieben. Dies könnte die Leistung verlangsamen, da der Datenträgerzugriff erhöht wird. Die Möglichkeit unbeabsichtigter Lücken wird aber verringert. Lücken können weiterhin auftreten, wenn Zahlen mit der **NEXT VALUE FOR**-Funktion oder der **sp_sequence_get_range**-Funktion angefordert werden. In diesem Fall werden die Zahlen aber entweder gar nicht oder nur in Transaktionen verwendet, für die kein Commit ausgeführt wurde.  
  
 Wenn ein Sequenzobjekt die **CACHE**-Option verwendet, wird der Cache in die Systemtabellen geschrieben, bevor die Änderung übernommen wird,wenn Sie das Sequenzobjekt neu starten oder **INCREMENT**, **CYCLE**, **MINVALUE**, **MAXVALUE** oder die Eigenschaften der Cachegröße ändern. Dann wird der Cache erneut geladen, wobei mit dem aktuellen Wert begonnen wird (d. h., es werden keine Zahlen übersprungen). Die Änderung der Cachegröße wird sofort wirksam.  
  
 **CACHE-Option, wenn zwischengespeicherte Werte verfügbar sind**  
  
 Der folgende Prozess tritt immer dann auf, wenn von einem Sequenzobjekt angefordert wird, den nächsten Wert für die **CACHE**-Option zu erstellen, wenn im In-Memory-Cache für das Sequenzobjekt nicht verwendete Werte verfügbar sind.  
  
1.  Der nächste Wert für das Sequenzobjekt wird berechnet.  
  
2.  Der neue aktuelle Wert für das Sequenzobjekt wird im Arbeitsspeicher aktualisiert.  
  
3.  Der berechnete Wert wird an die aufrufende Anweisung zurückgegeben.  
  
 **CACHE-Option, wenn kein Platz im Cache mehr verfügbar ist**  
  
 Der folgende Prozess tritt immer dann auf, wenn von einem Sequenzobjekt angefordert wird, den nächsten Wert für die **CACHE**-Option zu generieren, wenn im Cache kein Platz mehr vorhanden ist:  
  
1.  Der nächste Wert für das Sequenzobjekt wird berechnet.  
  
2.  Der letzte Wert für den neuen Cache wird berechnet.  
  
3.  Die Systemtabellenzeile für das Sequenzobjekt wird gesperrt, und der in Schritt 2 berechnete Wert (der letzte Wert) wird in die Systemtabelle geschrieben. Ein cache-exhausted-Xevent wird ausgelöst, um den Benutzer über den neuen beibehaltenen Wert zu benachrichtigen.  
  
 **NO CACHE-Option**  
  
 Der folgende Prozess tritt immer dann auf, wenn von einem Sequenzobjekt angefordert wird, den nächsten Wert für die **NO CACHE**-Option zu generieren:  
  
1.  Der nächste Wert für das Sequenzobjekt wird berechnet.  
  
2.  Der neue aktuelle Wert für das Sequenzobjekt wird in die Systemtabelle geschrieben.  
  
3.  Der berechnete Wert wird an die aufrufende Anweisung zurückgegeben.  
  
## <a name="metadata"></a>Metadaten  
 Weitere Informationen zu Sequenzen erhalten Sie durch Abfragen von [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigung **CREATE SEQUENCE**, **ALTER**oder **CONTROL** für das SCHEMA.  
  
-   Mitglieder der festen Datenbankrollen db_owner und db_ddladmin können Sequenzobjekte erstellen, ändern und löschen.  
  
-   Mitglieder der festen Datenbankrollen db_owner und db_datawriter können Sequenzobjekte aktualisieren, indem sie sie veranlassen, Zahlen zu generieren.  
  
 Im folgenden Beispiel wird dem Benutzer die Berechtigung „AdventureWorks\Larry“ erteilt, um Sequenzen im Test-Schema zu erstellen.  
  
```  
GRANT CREATE SEQUENCE ON SCHEMA::Test TO [AdventureWorks\Larry]  
```  
  
 Der Besitz eines Sequenzobjekts kann mit der **ALTER AUTHORIZATION**-Anweisung übertragen werden.  
  
 Wenn eine Sequenz einen benutzerdefinierten Datentyp verwendet, muss der Ersteller der Sequenz über die REFERENCES-Berechtigung für den Typ verfügen.  
  
### <a name="audit"></a>Überwachen von  
 Überwachen Sie die **SCHEMA_OBJECT_CHANGE_GROUP**, um **CREATE SEQUENCE** zu überwachen.  
  
## <a name="examples"></a>Beispiele  
 Beispiele zum Erstellen von Sequenzen und Verwenden der **NEXT VALUE FOR**-Funktion für das Generieren von Sequenznummern finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 In den meisten der folgenden Beispiele werden Sequenzobjekte in einem Schema namens „Test“ erstellt.  
  
 Um das Test-Schema zu erstellen, führen Sie die folgende Anweisung aus.  
  
```  
CREATE SCHEMA Test ;  
GO  
```  
  
### <a name="a-creating-a-sequence-that-increases-by-1"></a>A. Erstellen einer Sequenz, die sich um 1 vergrößert  
 Im folgenden Beispiel erstellt Thierry eine Sequenz namens „CountBy1“, die sich bei jeder Verwendung um 1 vergrößert.  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="b-creating-a-sequence-that-decreases-by-1"></a>B. Erstellen einer Sequenz, die sich um 1 verkleinert  
 Das folgende Beispiel startet bei 0 und zählt bei jeder Verwendung um 1 zurück in negative Zahlen.  
  
```  
CREATE SEQUENCE Test.CountByNeg1  
    START WITH 0  
    INCREMENT BY -1 ;  
GO  
```  
  
### <a name="c-creating-a-sequence-that-increases-by-5"></a>C. Erstellen einer Sequenz, die sich um 5 vergrößert  
 Im folgenden Beispiel wird eine Sequenz erstellt, die sich bei jeder Verwendung um 5 vergrößert.  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 5  
    INCREMENT BY 5 ;  
GO  
```  
  
### <a name="d-creating-a-sequence-that-starts-with-a-designated-number"></a>D. Erstellen einer Sequenz, die mit einer festgelegten Zahl beginnt  
 Nachdem Thierry eine Tabelle importiert hat, stellt er fest, dass die höchste verwendete ID-Nummer 24,328 ist. Thierry benötigt eine Sequenz, die Zahlen generiert, die mit 24,329 starten. Im folgenden Code wird eine Sequenz erstellt, die mit 24,329 startet und um 1 inkrementiert wird.  
  
```  
CREATE SEQUENCE Test.ID_Seq  
    START WITH 24329  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="e-creating-a-sequence-using-default-values"></a>E. Erstellen einer Sequenz mit Standardwerten  
 Im folgenden Beispiel wird eine Sequenz mit den Standardwerten erstellt.  
  
```  
CREATE SEQUENCE Test.TestSequence ;  
```  
  
 Führen Sie die folgende Anweisung aus, um die Eigenschaften der Sequenz anzuzeigen.  
  
```  
SELECT * FROM sys.sequences WHERE name = 'TestSequence' ;  
```  
  
 Eine Teilliste der Ausgabe veranschaulicht die Standardwerte.  
  
|||  
|-|-|  
|`start_value`|`-9223372036854775808`|  
|`increment`|`1`|  
|`mimimum_value`|`-9223372036854775808`|  
|`maximum_value`|`9223372036854775807`|  
|`is_cycling`|`0`|  
|`is_cached`|`1`|  
|`current_value`|`-9223372036854775808`|  
  
### <a name="f-creating-a-sequence-with-a-specific-data-type"></a>F. Erstellen einer Sequenz mit einem bestimmten Datentyp  
 Im folgenden Beispiel wird eine Sequenz erstellt, die den **smallint**-Datentyp mit einem Bereich von –32.768 bis 32.767 verwendet.  
  
```  
CREATE SEQUENCE SmallSeq  
    AS smallint ;  
```  
  
### <a name="g-creating-a-sequence-using-all-arguments"></a>G. Erstellen einer Sequenz, die alle Argumente verwendet  
 Im folgenden Beispiel wird eine Sequenz namens „DecSeq“ erstellt, die den **decimal**-Datentyp verwendet und einen Bereich von 0 bis 255 aufweist. Die Sequenz beginnt mit 125 und wird immer um 25 inkrementiert, wenn eine Zahl generiert wurde. Da die Sequenz zum Durchlaufen konfiguriert wurde, wird sie beim Überschreiten des maximalen Werts von 200 beim minimalen Wert von 100 neu gestartet.  
  
```  
CREATE SEQUENCE Test.DecSeq  
    AS decimal(3,0)   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
```  
  
 Führen Sie die folgende Anweisung aus, um den ersten Wert anzuzeigen; die `START WITH`-Option mit 125.  
  
```  
SELECT NEXT VALUE FOR Test.DecSeq;  
```  
  
 Führen Sie die Anweisung drei weitere Male aus, um 150, 175 und 200 zurückzugeben.  
  
 Führen Sie die Anweisung erneut aus, um zu sehen, wie der Startwert zurück zur `MINVALUE`-Option 100 durchläuft.  
  
 Führen Sie den folgenden Code aus, um die Cachegröße zu bestätigen und den aktuellen Wert anzuzeigen.  
  
```  
SELECT cache_size, current_value   
FROM sys.sequences  
WHERE name = 'DecSeq' ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
