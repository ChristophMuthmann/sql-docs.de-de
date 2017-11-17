---
title: '@@OPTIONS (Transact-SQL) | Microsoft Docs'
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
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 9480ffeffa83650b5cf44ad51547c36d5563b13b
ms.contentlocale: de-de
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;Optionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu den aktuellen SET-Optionen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Hinweise  
 Die Optionen können von der Verwendung von stammen die **festgelegt** Befehl oder aus der **Sp_configure Benutzeroptionen** Wert. Konfigurierte Sitzungswerte der **festgelegt** Befehl Außerkraftsetzung der **Sp_configure** Optionen. Viele Tools (beispielsweise [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) konfigurieren SET-Optionen automatisch. Jeder Benutzer verfügt über ein @@OPTIONS -Funktion, die die Konfiguration darstellt.  
  
 Sie können die Sprache und die Abfrageverarbeitungsoptionen für eine bestimmte Benutzersitzung mithilfe der SET-Anweisung ändern. **@@OPTIONS**  kann nur erkennen, die Optionen, die auf ON festgelegt werden oder OFF.  
  
 Die **@@OPTIONS**  Funktion gibt ein Bitmuster der Optionen, um eine Basis 10 (dezimal) ganze Zahl konvertiert. Die biteinstellungen werden in einer Tabelle in diesem Thema beschriebenen Orten gespeichert [Konfigurieren von Benutzeroptionen Serverkonfigurationsoption](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md).  
  
 Zum Decodieren der **@@OPTIONS**  Wert, konvertieren Sie die zurückgegebene Ganzzahl **@@OPTIONS**  in das Binärformat, und suchen Sie nach den Werten für die Tabelle am [Konfigurieren von Benutzeroptionen Server Konfigurationsoption](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md). Z. B. wenn `SELECT @@OPTIONS;` gibt den Wert `5496`, verwenden Sie die Windows-Rechner (**calc.exe**) zum Konvertieren von Decimal `5496` in das Binärformat. Das Ergebnis ist `1010101111000`. Die Zeichen nach rechts die meisten (binär 1, 2 und 4) sind 0 (null), der angibt, die die ersten drei Elemente in der Tabelle deaktiviert sind. Lesen die Tabelle, sehen Sie, dass diese sind **DISABLE_DEF_CNST_CHK** und **"IMPLICIT_TRANSACTIONS"**, und **CURSOR_CLOSE_ON_COMMIT**. Das nächste Element (**ANSI_WARNINGS** in der `1000` Position) befindet sich auf. Weiterarbeiten, links über die Bitmap und nach unten in der Liste der Optionen. Wenn die Optionen für die am weitesten links 0 sind, werden sie durch die typkonvertierung abgeschnitten. Bei der Bitmap `1010101111000` handelt es sich tatsächlich um `001010101111000`, um alle 15 Optionen darzustellen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. So wirken sich Änderungen auf das Verhalten aus  
 Das folgende Beispiel veranschaulicht den Unterschied im verkettungsverhalten bei Verwendung zwei verschiedener Einstellungen für die **CONCAT_NULL_YIELDS_NULL** Option.  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. Testen einer NOCOUNT-Clienteinstellung  
 Im folgenden Beispiel wird `NOCOUNT``ON` und testet dann den Wert des `@@OPTIONS`. Die `NOCOUNT``ON` Option wird verhindert, dass die Nachricht über die Anzahl der betroffenen zurück an den anfordernden Client für jede Anweisung in einer Sitzung gesendeten Zeilen. Für den Wert von `@@OPTIONS` wird `512` (0x0200) festgelegt. Dies stellt die Option NOCOUNT dar. Dieses Beispiel testet, ob die Option NOCOUNT auf dem Client aktiviert wurde. Dadurch können beispielsweise Leistungsunterschiede auf einem Client nachverfolgt werden.  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Konfigurieren der Benutzeroptionen (Serverkonfigurationsoption)](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  

