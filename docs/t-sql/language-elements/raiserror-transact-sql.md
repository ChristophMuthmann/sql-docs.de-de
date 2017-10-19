---
title: RAISERROR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/21/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RAISERROR
- RAISERROR_TSQL
- RAISEERROR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- errors [SQL Server], RAISERROR statement
- user-defined error messages [SQL Server]
- system flags
- generating errors [SQL Server]
- TRY block [SQL Server]
- recording errors
- ad hoc messages
- RAISERROR statement
- CATCH block
- messages [SQL Server], RAISERROR statement
ms.assetid: 483588bd-021b-4eae-b4ee-216268003e79
caps.latest.revision: 73
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 4fe1477de1f1aa087d622d687249ee4a10ad2524
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="raiserror-transact-sql"></a>RAISERROR-Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Generiert eine Fehlermeldung und initiiert die Verarbeitung von Fehlern für die Sitzung. RAISERROR kann entweder eine benutzerdefinierte Meldung in sys.messages-Katalogsicht gespeicherte verweisen oder eine Meldung dynamisch erstellen. Die Meldung wird als Serverfehlermeldung an die aufrufende Anwendung oder an einen zugeordneten CATCH-Block eines TRY…CATCH-Konstrukts zurückgegeben. Neue Anwendungen sollten verwenden [AUSLÖSEN](../../t-sql/language-elements/throw-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
RAISERROR ( { msg_id | msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
RAISERROR ( { msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
## <a name="arguments"></a>Argumente  
 *msg_id*  
 Eine benutzerdefinierte Meldung Fehlernummer ist in der sys.messages-Katalogsicht mit Sp_addmessage gespeichert werden. Fehlernummern für benutzerdefinierte Fehlermeldungen müssen größer als 50000 sein. Wenn *Msg_id* nicht angegeben wird, löst RAISERROR eine Fehlermeldung mit einer der Fehlernummer 50000.  
  
 *msg_str*  
 Ist eine benutzerdefinierte Meldung mit einer Formatierung ähnelt der **Printf** Funktion in der C-Standardbibliothek. Die Fehlermeldung kann maximal 2.047 Zeichen enthalten. Wenn die Meldung mehr als 2.048 Zeichen enthält, werden nur die ersten 2.044 angezeigt und Auslassungspunkte angefügt, die anzeigen, dass die Meldung abgeschnitten wurde. Aufgrund des internen Speicherverhaltens beanspruchen Ersetzungsparameter mehr Zeichen als in der Ausgabe angezeigt werden. Beispielsweise der Ersetzungsparameter *%d* auch intern nimmt drei zusätzliche Zeichen Speicher jedoch mit einem zugewiesenen Wert 2 tatsächlich ein Zeichen in der Nachrichtenzeichenfolge erzeugt. Durch diese Speicheranforderung wird die Anzahl von verfügbaren Zeichen für die Meldungsausgabe gesenkt.  
  
 Wenn *Msg_str* angegeben wird, löst RAISERROR eine Fehlermeldung mit einer der Fehlernummer 50000.  
  
 *Msg_str* ist eine Zeichenfolge mit optional eingebetteten Konvertierungsspezifikationen. Jede Konvertierungsspezifikation definiert, wie ein Wert in der Argumentliste formatiert und in ein Feld an der Position der Konvertierungsspezifikation in versetzt *Msg_str*. Konvertierungsspezifikationen weisen das folgende Format auf:  
  
 % [[*Flag*] [*Breite*] [. *Genauigkeit*] [{h | l}]] *Typ*  
  
 Die Parameter, die in zu verwendenden *Msg_str* sind:  
  
 *Kennzeichen*  
  
 Ist ein Code, der den Abstand und die Ausrichtung des ersetzten Werts bestimmt.  
  
|Code|Präfix oder Ausrichtung|Description|  
|----------|-----------------------------|-----------------|  
|- (Minus)|Linksbündig|Der Argumentwert wird innerhalb der angegebenen Feldbreite linksbündig ausgegeben.|  
|+ (Plus)|Zeichenpräfix|Dem Argumentwert wird ein Plus- (+) oder Minuszeichen (-) vorangestellt, wenn der Wert einen Datentyp mit Vorzeichen aufweist.|  
|0 (Null)|Auffüllung mit Nullen|Der Ausgabe wird 0 vorangestellt, bis die Mindestbreite erreicht ist. Wenn 0 und das Minuszeichen (-) auftreten, wird 0 ignoriert.|  
|# (Nummer)|0x-Präfix für Hexadezimaltyp von x oder X|Das Nummernzeichenflag (#) wird jedem Wert ungleich 0 mit 0, 0x bzw. 0X vorangestellt, wenn es mit dem Format o, x oder X verwendet wird. Wenn das Nummernzeichenflag (#) vor d, i oder u steht, wird das Flag ignoriert.|  
|" " (Leerzeichen)|Auffüllung mit Leerstellen|Dem Ausgabewert werden Leerzeichen vorangestellt, wenn der Wert ein Vorzeichen aufweist und positiv ist. Dies wird ignoriert, wenn er mit dem Pluszeichenflag (+) versehen ist.|  
  
 *Breite*  
  
 Ist eine ganze Zahl, die die Mindestbreite des Felds definiert, in das der Argumentwert platziert werden soll. Wenn die Länge des Argumentwerts gleich oder länger als *Breite*, ist der Wert ohne Auffüllung ausgegeben. Wenn der Wert kürzer als *Breite*, der Wert wird auf die im angegebenen Länge aufgefüllt *Breite*.  
  
 Ein Sternchen (*) bedeutet, dass die Breite durch das zugeordnete Argument in der Argumentliste angegeben wird, welches ein Wert für eine ganze Zahl sein muss.  
  
 *precision*  
  
 Ist die maximale Anzahl von Zeichen aus dem Argumentwert für Zeichenfolgenwerte. Wenn beispielsweise eine Zeichenfolge über fünf Zeichen verfügt und die Genauigkeit 3 beträgt, werden nur die ersten drei Zeichen des Zeichenfolgenwerts verwendet.  
  
 Bei Ganzzahlwerten *Genauigkeit* ist die Mindestanzahl von Ziffern gedruckt.  
  
 Ein Sternchen (*) bedeutet, dass die Genauigkeit durch das zugeordnete Argument in der Argumentliste angegeben wird, welches ein Wert für eine ganze Zahl sein muss.  
  
 {h | l} *Typ*  
  
 Wird verwendet, mit den Zeichentypen d, i, o, s, X, X oder u verwendet und erstellt **Shortint** (h) oder **Longint** (l)-Werte.  
  
|Typspezifikation|Darstellt|  
|------------------------|----------------|  
|d oder i|Ganze Zahl mit Vorzeichen|  
|o|Oktal ohne Vorzeichen|  
|s|String|  
|u|Ganze Zahl ohne Vorzeichen|  
|x oder X|Hexadezimal ohne Vorzeichen|  
  
> [!NOTE]  
>  Diese Typspezifikationen basieren auf den ursprünglich für die **Printf** Funktion in der C-Standardbibliothek. Der in RAISERROR Zeichenfolgen meldungszuordnung zum verwendeten Typspezifikationen [!INCLUDE[tsql](../../includes/tsql-md.md)] Datentypen, während die Spezifikationen **Printf** Zuordnung in C-Datentypen. Geben Sie im verwendeten Spezifikationen **Printf** werden nicht von RAISERROR unterstützt beim [!INCLUDE[tsql](../../includes/tsql-md.md)] keinen Datentyp ähnlich dem zugeordneten C-Datentyp. Z. B. die *%p* -Spezifikation für Zeiger nicht in RAISERROR unterstützt, da [!INCLUDE[tsql](../../includes/tsql-md.md)] verfügt nicht über einen Zeigerdatentyp.  
  
> [!NOTE]  
>  Konvertieren eines Werts, der [!INCLUDE[tsql](../../includes/tsql-md.md)] **"bigint"** -Datentyp geben **% I64d**.  
  
 **@***Local_variable*  
 Ist eine Variable eines beliebigen gültigen Zeichendatentyps, die eine Zeichenfolge, die auf die gleiche Weise wie formatiert enthält *Msg_str*. **@***Local_variable* muss **Char** oder **Varchar**, oder werden implizit in diese Datentypen konvertiert werden können.  
  
 *Schweregrad*  
 Ist der benutzerdefinierte Schweregrad, der dieser Meldung zugeordnet ist. Bei Verwendung *Msg_id* zum Auslösen einer benutzerdefinierten Meldung mit Sp_addmessage erstellt, überschreibt in RAISERROR angegebene Schweregrad der Schweregrad den Schweregrad in Sp_addmessage angegeben.  
  
 Schweregrade von 0 bis 18 können von jedem Benutzer angegeben werden. Schweregrade von 19 bis 25 können nur von Mitgliedern der festen Sysadmin-Serverrolle oder Benutzer mit ALTER TRACE-Berechtigungen angegeben werden. Für Schweregrade von 19 bis 25 ist die Option WITH LOG erforderlich. Geringere Schweregrade als 0 werden als 0 interpretiert. Höhere Schweregrade als 25 werden als 25 interpretiert.  
  
> [!CAUTION]  
>  Die Schweregrade von 20 bis 25 werden als schwerwiegend angesehen. Wird ein schwerwiegender Schweregrad ermittelt, so wird die Clientverbindung nach Empfang der Meldung beendet und der Fehler in den Fehler- und Anwendungsprotokollen protokolliert.  
  
 Sie können -1 angeben, um den Wert für den Schweregrad des Fehlers zurückzugeben, wie im folgenden Beispiel veranschaulicht.  
  
```  
RAISERROR (15600,-1,-1, 'mysp_CreateCustomer');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 15600, Level 15, State 1, Line 1   
 An invalid parameter or option was specified for procedure 'mysp_CreateCustomer'.
 ```  
  
 *Status*  
 Eine ganze Zahl zwischen 0 und 255. Negative Werte werden standardmäßig auf 1. Werte größer als 255 sollte nicht verwendet werden. 
  
 Wird derselbe benutzerdefinierte Fehler an mehreren Stellen ausgelöst, kann durch Verwenden einer eindeutigen Statusnummer für die einzelnen Positionen der Codeabschnitt ermittelt werden, der die Fehler auslöst.  
  
 *Argument*  
 Sind die im Ersatz für Variablen, die in definierten verwendeten Parameter *Msg_str* oder entsprechende Meldung *Msg_id*. Es können 0 oder mehr Ersetzungsparameter vorhanden sein, jedoch nicht mehr als 20. Jeder Ersetzungsparameter kann eine lokale Variable oder einen der folgenden Datentypen aufweisen: **"tinyint"**, **"smallint"**, **Int**, **Char**, **Varchar**, **Nchar**, **Nvarchar**, **binäre**, oder **Varbinary**. Es werden keine weiteren Datentypen unterstützt.  
  
 *Option*  
 Ist eine benutzerdefinierte Option für den Fehler und kann einer der Werte in der folgenden Tabelle sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|LOG|Protokolliert den Fehler in das Fehlerprotokoll und das Anwendungsprotokoll für die Instanz von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Im Fehlerprotokoll protokollierte Fehler sind derzeit auf maximal 440 Bytes beschränkt. Nur ein Mitglied der festen Serverrolle "Sysadmin" oder ein Benutzer mit ALTER TRACE-Berechtigungen kann WITH LOG angeben.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|NOWAIT|Sendet Meldungen sofort an den Client.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|SETERROR|Legt die @@ERROR und ERROR_NUMBER Werte *Msg_id* oder 50000, unabhängig vom Schweregrad.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
  
## <a name="remarks"></a>Hinweise  
 Die von RAISERROR generierten Fehler sind mit Fehlern vergleichbar, die durch den [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Code generiert werden. Die angegebenen Werte von RAISERROR gemeldet werden, durch die ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY, ERROR_STATE und @@ERROR Systemfunktionen. Wird RAISERROR mit einem Schweregrad von 11 oder höher in einem TRY-Block ausgeführt, wird die Steuerung an den zugeordneten CATCH-Block übertragen. Der Fehler wird an den Aufrufer zurückgegeben, wenn RAISERROR ausgeführt wird:  
  
-   Außerhalb des Bereichs eines beliebigen TRY-Blocks.  
  
-   Mit einem Schweregrad von 10 oder tiefer in einem TRY-Block.  
  
-   Mit einem Schweregrad von 20 oder höher, der die Datenbankverbindung beendet.  
  
 CATCH-Blöcke können mithilfe von RAISERROR den Fehler erneut auslösen, der den CATCH-Block mithilfe von Systemfunktionen wie ERROR_NUMBER und ERROR_MESSAGE aufgerufen hat, um die ursprünglichen Fehlerinformationen abzurufen. @@ERROR ist auf 0 festgelegt, wird standardmäßig für Meldungen mit einem Schweregrad von 1 bis 10.  
  
 Wenn *Msg_id* gibt einer benutzerdefinierte Meldung aus der sys.messages-Katalogsicht RAISERROR Prozesse verfügbaren die Nachricht aus der Textspalte mithilfe derselben Regeln auf den Text einer angegebenen benutzerdefinierten Meldung angewendet werden mit *Msg_str*. Der Text der benutzerdefinierten Meldung kann Konvertierungsspezifikationen enthalten, und RAISERROR ordnet den Konvertierungsspezifikationen Argumentwerte zu. Verwenden Sie Sp_addmessage, zum Hinzufügen von benutzerdefinierten Fehlermeldungen und Sp_dropmessage, um benutzerdefinierte Fehlermeldungen gelöscht.  
  
 RAISERROR kann alternativ zu PRINT für die Rückgabe von Meldungen an aufrufende Anwendungen verwendet werden. RAISERROR unterstützt das Ersetzen von Zeichen ähnlich den Funktionen von der **Printf** -Funktion in der C-Standardbibliothek, während die [!INCLUDE[tsql](../../includes/tsql-md.md)] PRINT-Anweisung nicht. Die PRINT-Anweisung ist von TRY-Blöcken nicht betroffen. Wird jedoch RAISERROR mit einem Schweregrad von 11 bis 19 in einem TRY-Block ausgeführt, wird die Steuerung an den zugeordneten CATCH-Block übertragen. Geben Sie einen Schweregrad von 10 oder niedriger an, um RAISERROR für die Rückgabe einer Meldung aus einem TRY-Block ohne Aufrufen des CATCH-Blocks zu verwenden.  
  
 In der Regel ersetzen aufeinander folgende Argumente aufeinander folgende Konvertierungsspezifikationen. Das erste Argument ersetzt die erste Konvertierungsspezifikation, das zweite Argument ersetzt die zweite Konvertierungsspezifikation usw. In der folgenden `RAISERROR`-Anweisung ersetzt beispielsweise das erste Argument von `N'number'` die erste Konvertierungsspezifikation von `%s`, und das zweite Argument von `5` ersetzt die zweite Konvertierungsspezifikation von `%d.`.  
  
```  
RAISERROR (N'This is message %s %d.', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'number', -- First argument.  
           5); -- Second argument.  
-- The message text returned is: This is message number 5.  
GO  
```  
  
 Wird ein Sternchen (*) entweder für die Breite oder die Genauigkeit einer Konvertierungsspezifikation angegeben, wird der für die Breite oder Genauigkeit zu verwendende Wert als ein ganzzahliger Argumentwert angegeben. In diesem Fall kann eine Konvertierungsspezifikation bis zu drei Argumente verwenden - jeweils eines für den Breiten-, Genauigkeits- und den Ersetzungswert.  
  
 So geben beispielsweise beide folgenden `RAISERROR`-Anweisungen dieselbe Zeichenfolge zurück. Eine gibt die Breiten- und Genauigkeitswerte in der Argumentliste an, während die andere die Werte in der Konvertierungsspezifikation angibt.  
  
```  
RAISERROR (N'<\<%*.*s>>', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           7, -- First argument used for width.  
           3, -- Second argument used for precision.  
           N'abcde'); -- Third argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
RAISERROR (N'<\<%7.3s>>', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-error-information-from-a-catch-block"></a>A. Zurückgeben von Fehlerinformationen aus einem CATCH-Block  
 Im folgenden Codebeispiel wird dargestellt, wie `RAISERROR` in einem `TRY`-Block verwendet wird, sodass die Ausführung zum zugeordneten `CATCH`-Block springt. Darüber hinaus wird dargestellt, wie `RAISERROR` verwendet wird, um Informationen zu dem Fehler zurückzugeben, der den `CATCH`-Block aufgerufen hat.  
  
> [!NOTE]  
>  RAISERROR generiert nur Fehler mit dem Status 1 bis 127. Da [!INCLUDE[ssDE](../../includes/ssde-md.md)] u. U. Fehler mit dem Status 0 ausgibt, wird empfohlen, den von ERROR_STATE zurückgegebenen Fehlerzustand zu überprüfen, bevor Sie ihn als Wert an den Statusparameter von RAISERROR weitergeben.  
  
```  
BEGIN TRY  
    -- RAISERROR with severity 11-19 will cause execution to   
    -- jump to the CATCH block.  
    RAISERROR ('Error raised in TRY block.', -- Message text.  
               16, -- Severity.  
               1 -- State.  
               );  
END TRY  
BEGIN CATCH  
    DECLARE @ErrorMessage NVARCHAR(4000);  
    DECLARE @ErrorSeverity INT;  
    DECLARE @ErrorState INT;  
  
    SELECT   
        @ErrorMessage = ERROR_MESSAGE(),  
        @ErrorSeverity = ERROR_SEVERITY(),  
        @ErrorState = ERROR_STATE();  
  
    -- Use RAISERROR inside the CATCH block to return error  
    -- information about the original error that caused  
    -- execution to jump to the CATCH block.  
    RAISERROR (@ErrorMessage, -- Message text.  
               @ErrorSeverity, -- Severity.  
               @ErrorState -- State.  
               );  
END CATCH;  
```  
  
### <a name="b-creating-an-ad-hoc-message-in-sysmessages"></a>B. Erstellen einer Ad-hoc-Meldung in sys.messages  
 Im folgende Beispiel wird gezeigt, wie eine in der sys.messages-Katalogsicht gespeicherte Meldung ausgelöst wird. Die Meldung wurde der sys.messages-Katalogsicht hinzugefügt, mit der `sp_addmessage` System gespeicherte Prozedur als Meldungsnummer `50005`.  
  
```  
sp_addmessage @msgnum = 50005,  
              @severity = 10,  
              @msgtext = N'<\<%7.3s>>';  
GO  
RAISERROR (50005, -- Message id.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
sp_dropmessage @msgnum = 50005;  
GO  
```  
  
### <a name="c-using-a-local-variable-to-supply-the-message-text"></a>C. Verwenden einer lokalen Variable zum Angeben des Meldungstexts  
 Im folgenden Codebeispiel wird die Verwendung einer lokalen Variablen zum Bereitstellen des Meldungstexts für eine `RAISERROR`-Anweisung dargestellt.  
  
```  
DECLARE @StringVariable NVARCHAR(50);  
SET @StringVariable = N'<\<%7.3s>>';  
  
RAISERROR (@StringVariable, -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Deklarieren Sie @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md) [integrierte Funktionen &#40; Transact-SQL &#41;](~/t-sql/functions/functions.md)   
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [Sp_addmessage &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [Sp_dropmessage &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [Xp_logevent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logevent-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  


