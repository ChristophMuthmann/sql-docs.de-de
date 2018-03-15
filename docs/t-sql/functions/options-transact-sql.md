---
title: '@@OPTIONS (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75919b6d27b2a81a9aba3575d3a9f3c54f0e0850
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;OPTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu den aktuellen SET-Optionen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 Die Optionen werden zurückgegeben, wenn Sie den **SET**-Befehl oder die **sp_configure-Benutzeroptionen** verwenden. Mithilfe des **SET**-Befehls konfigurierte Sitzungswerte überschreiben die **sp_configure**-Optionen. Viele Tools (beispielsweise [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) konfigurieren SET-Optionen automatisch. Jeder Benutzer verfügt über eine @@OPTIONS-Funktion, die die Konfiguration darstellt.  
  
 Sie können die Sprache und die Abfrageverarbeitungsoptionen für eine bestimmte Benutzersitzung mithilfe der SET-Anweisung ändern. **@@OPTIONS** kann nur die Optionen erkennen, die auf ON oder OFF festgelegt sind.  
  
 Die **@@OPTIONS**-Funktion gibt eine Bitmap der Optionen zurück, konvertiert in einen Integer zur Basis 10 (dezimal). Die Biteinstellungen werden an den in einer Tabelle im Artikel [Konfigurieren der Benutzeroptionen für die Serverkonfigurationsoption](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) beschriebenen Orten gespeichert.  
  
 Konvertieren Sie den von **@@OPTIONS** zurückgegebenen Integer in das Binärformat, und suchen Sie in der unter [Konfigurieren der Benutzeroptionen für die Serverkonfigurationsoption](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) aufgeführten Tabelle nach den Werten, um den **@@OPTIONS**-Wert zu decodieren. Wenn beispielsweise `SELECT @@OPTIONS;` den Wert `5496` zurückgibt, verwenden Sie den Windows-Rechner (**calc.exe**), um die Dezimalzahl `5496` ins Binärformat zu konvertieren. Das Ergebnis ist `1010101111000`. Die am weitesten rechts stehenden Zeichen (Binärwerte 1, 2 und 4) haben den Wert 0 (null), was darauf hindeutet, dass die ersten drei Elemente in der Tabelle deaktiviert sind. In der Tabelle sehen Sie, dass die Elemente **DISABLE_DEF_CNST_CHK**, **IMPLICIT_TRANSACTIONS** und **CURSOR_CLOSE_ON_COMMIT** lauten. Das nächste Element (**ANSI_WARNINGS** an der Position `1000`) ist aktiviert. Fahren Sie auf der linken Seite mit der Bitmap und der Liste der Optionen fort. Wenn die ganz links stehenden Optionen einen Wert von 0 (null) aufweisen, wurden sie durch die Typkonvertierung abgeschnitten. Bei der Bitmap `1010101111000` handelt es sich tatsächlich um `001010101111000`, um alle 15 Optionen darzustellen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. So wirken sich Änderungen auf das Verhalten aus  
 Das folgende Beispiel veranschaulicht die Unterschiede im Verkettungsverhalten bei Verwendung zweier verschiedener Einstellungen für die Option **CONCAT_NULL_YIELDS_NULL**.  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. Testen einer NOCOUNT-Clienteinstellung  
 Das folgende Beispiel legt `NOCOUNT``ON` fest und testet dann den Wert von `@@OPTIONS`. Die Option `NOCOUNT``ON` verhindert, dass die Nachricht über die Anzahl von betroffenen Zeilen an den anfordernden Client für jede Anweisung in einer Sitzung zurückgegeben wird. Für den Wert von `@@OPTIONS` wird `512` (0x0200) festgelegt. Dies stellt die Option NOCOUNT dar. Dieses Beispiel testet, ob die Option NOCOUNT auf dem Client aktiviert wurde. Dadurch können beispielsweise Leistungsunterschiede auf einem Client nachverfolgt werden.  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Konfigurieren der Benutzeroptionen (Serverkonfigurationsoption)](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  
