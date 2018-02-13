---
title: Literale (SSIS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- string literals
- numeric literals [Integration Services]
- Boolean literals
- expressions [Integration Services], literals
- literals [Integration Services]
- mapping literals [Integration Services]
ms.assetid: a980cd52-54ef-4b9c-b00c-e6807cf8e01f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a89f9c1fde9d4a14776d37bc648341a5b5fa4aad
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="numeric-string-and-boolean-literals"></a>Numerische, Zeichenfolgen- und boolesche Literale
 Ausdrücke können numerische und boolesche Literale sowie Zeichenfolgenliterale einschließen. Die Ausdrucksauswertung unterstützt eine Reihe von numerischen Literalen, wie z. B. ganze Zahlen, Dezimalzeichen und Gleitkommakonstanten. Außerdem unterstützt die Ausdrucksauswertung die long- und float-Suffixe, die die Behandlung von Werten durch die Ausdrucksauswertung angeben, sowie die wissenschaftliche Schreibweise bei numerischen Literalen.  
  
## <a name="numeric-literals"></a>Numerische Literale  
 Die Ausdrucksauswertung unterstützt integrale und nicht integrale numerische Datentypen. Außerdem werden Herkunftsbezeichner unterstützt (die eindeutigen numerischen Bezeichner für Paketelemente). Herkunftsbezeichner sind Zahlen, können aber nicht in mathematischen Operationen verwendet werden.  
  
 Die Ausdrucksauswertung unterstützt Suffixe, mit denen Sie angeben können, wie die numerischen Literale behandelt werden sollen. Beispielsweise können Sie angeben, dass die ganze Zahl 37 als lange ganze Zahl behandelt wird, indem Sie 37L oder 37l eingeben.  
  
 In der folgenden Tabelle sind Suffixe für numerische Literale aufgeführt.  
  
|Suffix|Description|  
|------------|-----------------|  
|L oder l|Ein langes numerisches Literal.|  
|U oder u|Ein numerisches Literal ohne Vorzeichen.|  
|E oder e|Der Exponent in der wissenschaftlichen Schreibweise.|  
  
 In der folgenden Tabelle sind numerische Ausdruckselemente und deren reguläre Ausdrücke aufgeführt.  
  
|Ausdruckselement|Regulärer Ausdruck|Description|  
|------------------------|------------------------|-----------------|  
|Ziffern, ausgedrückt als D.|[0-9]|Eine beliebige Ziffer.|  
|Wissenschaftliche Schreibweise, ausgedrückt als E.|[Ee][+-]?{D}+|e (Groß- oder Kleinbuchstabe), optional + oder -, und mindestens eine Ziffer gemäß der Definition in D.|  
|Integer-Suffix, ausgedrückt als IS.|(([lL]?[uU]?)&#124;([uU]?[lL]?))|Optional u und l (Groß- oder Kleinbuchstabe) oder eine Kombination von u und l. U oder u bezeichnet einen Wert ohne Vorzeichen. L oder l bezeichnet einen Wert vom long-Datentyp.|  
|Float-Suffix, ausgedrückt als FS.|([f&#124;F]&#124;[l&#124;L])|f oder l (Groß- oder Kleinbuchstabe). F oder f bezeichnet einen Wert vom float-Datentyp (DT_R4-Datentyp). L oder l bezeichnet einen Wert vom long-Datentyp (DT_R8-Datentyp).|  
|Hexadezimale Ziffer, ausgedrückt als H.|[a-fA-F0-9]|Eine beliebige hexadezimale Ziffer.|  
  
 In der folgenden Tabelle sind gültige numerische Literale mithilfe der regulären Ausdruckssprache beschrieben.  
  
|Regulärer Ausdruck|Description|  
|------------------------|-----------------|  
|{D}+{IS}|Ein integrales numerisches Literal mit mindestens einer Ziffer (D) und optional dem Suffix long und/oder unsigned (IS).  Beispiele: 457, 785u, 986L und 7945ul.|  
|{D}+{E}{FS}|Ein integrales numerisches Literal mit mindestens einer Ziffer (D) in wissenschaftlicher Schreibweise und dem Suffix long oder float.  Beispiele: 4E8l, 13e-2f und 5E+L.|  
|{D}*"."{D}+{E}?{FS}|Ein nicht integrales numerisches Literal mit einer Dezimalstelle, einem Dezimalbruch mit mindestens einer Ziffer (D), einem optionalen Exponenten (E) und einem float- oder einem long-Bezeichner (FS). Dieses numerische Literal weist den Datentyp DT_R4 oder DT_R8 auf.  Beispiele: 6,45E3f, 0,89E-2l und 1,05E+7F.|  
|{D}+"."{D}*{E}?{FS}|Ein nicht integrales numerisches Literal mit mindestens einer signifikanten Ziffer (D), einer Dezimalstelle, einem Exponenten (E) und einem float- oder einem long-Bezeichner (FS). Dieses numerische Literal weist den Datentyp DT_R4 oder DT_R8 auf.  Beispiele: 1,E-4f, 4,6E6L und 8,365E+2f.|  
|{D}*.{D}+|Ein nicht integrales numerisches Literal mit Genauigkeit und Dezimalstellenanzahl. Es weist eine Dezimalstelle und einen Dezimalbruch mit mindestens einer Ziffer (D) auf. Dieses numerische Literal weist den Datentyp DT_NUMERIC auf.  Beispiele: 0,9, 5,8 und 0,346.|  
|{D}+.{D}*|Ein nicht integrales numerisches Literal mit Genauigkeit und Dezimalstellenanzahl. Es weist mindestens eine signifikante Ziffer (D) und eine Dezimalstelle auf. Dieses numerische Literal weist den Datentyp DT_NUMERIC auf.  Beispiele: 6,0, 0,2 und 8,0.|  
|#{D}+|Ein Herkunftsbezeichner. Er besteht aus dem Nummernzeichen (#) und mindestens einer Ziffer (D). Beispiele: #123.|  
|0[xX]{H}+{uU}|Ein numerisches Literal im Hexadezimalformat. Es schließt eine Null, ein x (Groß- oder Kleinbuchstabe), mindestens ein H (Großbuchstabe) und optional das unsigned-Suffix ein. Beispiele: 0xFF0A und 0X000010000U.|  
  
 Weitere Informationen zu den von der Ausdrucksauswertung verwendeten Datentypen finden Sie unter [Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Ausdrücke können numerische Literale mit verschiedenen Datentypen einschließen. Wenn die Ausdrucksauswertung diese Ausdrücke auswertet, werden die Daten in kompatible Typen konvertiert. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
 Für die Konvertierung bestimmter Datentypen ist jedoch eine explizite Umwandlung erforderlich. Die Ausdrucksauswertung stellt den Umwandlungsoperator für die explizite Datentypkonvertierung bereit. Weitere Informationen finden Sie unter [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
### <a name="mapping-numeric-literals-to-integration-services-data-types"></a>Zuordnen numerischer Literale zu SQL Server Integration Services-Datentypen  
 Die Ausdrucksauswertung führt beim Auswerten numerischer Literale die folgenden Konvertierungen aus:  
  
-   Ein integrales numerisches Literal wird folgendermaßen einem integer-Datentyp zugeordnet.  
  
    |Suffix|Ergebnistyp|  
    |------------|-----------------|  
    |InclusionThresholdSetting|DT_I4|  
    |U|DT_UI4|  
    |L|DT_I8|  
    |UL|DT_UI8|  
  
    > **WICHTIG!** Wenn das long-Suffix (L oder l) fehlt, weist die Ausdrucksauswertung Werte mit Vorzeichen dem DT_I4-Datentyp sowie Werte ohne Vorzeichen dem DT_UI4-Datentyp zu, auch wenn der Wert bei dem Datentyp zu einem Überlauf führt.  
  
-   Ein numerisches Literal mit einem Exponenten wird in den Datentyp DT_R4 oder DT_R8 konvertiert. Falls der Ausdruck das long-Suffix einschließt, wird er in den DT_R8-Datentyp konvertiert; falls er das float-Suffix einschließt, wird er in den DT_R4-Datentyp konvertiert.  
  
-   Wenn ein nicht integrales numerisches Literal F oder f einschließt, wird es dem DT_R4-Datentyp zugeordnet. Falls das Literal L oder l einschließt und die Zahl eine ganze Zahl ist, wird es dem DT_I8-Datentyp zugeordnet. Wenn es sich um eine reelle Zahl handelt, wird es dem DT_R8-Datentyp zugeordnet. Wenn das Literal das long-Suffix einschließt, wird es in den DT_R8-Datentyp konvertiert.  
  
-   Ein nicht integrales numerisches Literal mit Genauigkeit und Dezimalstellenanzahl wird dem DT_NUMERIC-Datentyp zugeordnet.  
  
## <a name="string-literals"></a>Zeichenfolgenliterale  
 Zeichenfolgenliterale müssen in Anführungszeichen eingeschlossen werden. Die Ausdruckssprache stellt Escapesequenzen für häufig verwendete Zeichen bereit, wie z. B. nicht druckbare Zeichen und Anführungszeichen.  
  
 Ein Zeichenfolgenliteral besteht aus null oder mehr Zeichen, die in Anführungszeichen eingeschlossen sind. Falls eine Zeichenfolge Anführungszeichen enthält, müssen diese als Escapezeichen formatiert werden, damit der Ausdruck analysiert wird. Jedes Zeichen mit einer Länge von zwei Byte, außer \x0000, ist in einer Zeichenfolge zulässig, weil das Zeichen \x0000 das Null-Abschlusszeichen einer Zeichenfolge ist.  
  
 Zeichenfolgen können andere Zeichen einschließen, die eine Escapesequenz erfordern. In der folgenden Tabelle sind Escapesequenzen für Zeichenfolgenliterale aufgeführt.  
  
|Escapesequenz|Description|  
|---------------------|-----------------|  
|\a|Warnung|  
|\b|Rücktaste|  
|\f|Seitenvorschub|  
|\n|Neue Zeile|  
|\r|Wagenrücklauf|  
|\t|Horizontaler Tabstopp|  
|\v|Vertikaler Tabstopp|  
|\\"|Anführungszeichen|  
|\\\|Umgekehrter Schrägstrich|  
|\xhhhh|Unicode-Zeichen in Hexadezimalschreibweise|  
  
## <a name="boolean-literals"></a>Boolesche Literale  
 Die üblichen booleschen Literale werden von der Ausdrucksauswertung unterstützt: **True** und **False**. Die Ausdrucksauswertung unterscheidet nicht nach Groß-/Kleinschreibung, und eine beliebige Kombination von Groß- und Kleinbuchstaben ist zulässig. Beispielsweise TRUE oder True.  
  
> **HINWEIS:** In einem Ausdruck muss ein boolesches Literal durch Leerzeichen getrennt werden.  
  
  
