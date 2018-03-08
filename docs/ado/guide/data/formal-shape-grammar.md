---
title: "Formale Grammatik für Formen | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9eb99feba381701f7e590add3906cd0285b2720
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="formal-shape-grammar"></a>Formale Grammatik für Formen
Dies ist die formale Grammatik für alle Form-Befehl zu erstellen:  
  
-   Erforderliche grammatische Begriffe sind Textzeichenfolgen, die in spitze Klammern ("<>") als Trennzeichen.  
  
-   Optionale Ausdrücke werden durch eckige Klammern ("[]") getrennt.  
  
-   Alternativen Warnschwellenwerts durch einen Schrägstrich ("&#124;").  
  
-   Wiederholte alternativen werden durch ein Auslassungszeichen ("...") angezeigt.  
  
-   *Alpha* gibt eine Zeichenfolge von Buchstaben.  
  
-   *Ziffer* gibt eine Zeichenfolge von Zahlen.  
  
-   *Unicode-Ziffern* gibt eine Zeichenfolge von Unicode-Ziffern.  
  
 Alle anderen Begriffe sind Literale.  
  
|Begriff|Definition|  
|----------|----------------|  
|\<shape-command>|Form "[\<Tabelle exp > [[AS] \<Alias >]] [\<Form Aktion >]|  
|\<table-exp>|{\<provider-command-text>} &#124;<br /><br /> (\<Shape-Befehl >) &#124;<br /><br /> TABLE \<quoted-name> &#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|APPEND \<aliased-field-list> &#124;<br /><br /> COMPUTE \<Alias Feldliste > [BY \<Feldliste >]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<relation-exp>) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> RELATE \<relation-cond-list>|  
|\<relation-cond-list>|\<Beziehung Cond > [, \<Beziehung Cond >...]|  
|\<relation-cond>|\<field-name> TO \<child-ref>|  
|\<child-ref>|\<field-name> &#124;<br /><br /> PARAMETER \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<Feld-Name > [, \<Feld-Name >]|  
|\<aggregate-exp>|SUM (\<qualified-Feld-Name >) &#124;<br /><br /> AVG (\<qualified-Feld-Name >) &#124;<br /><br /> MIN (\<qualified-Feld-Name >) &#124;<br /><br /> MAX (\<qualified-Feld-Name >) &#124;<br /><br /> COUNT(\<qualified-alias> &#124; \<qualified-name>) &#124;<br /><br /> STDEV (\<qualified-Feld-Name >) &#124;<br /><br /> Alle (\<qualified-Feld-Name >)|  
|\<calculated-exp>|CALC (\<Ausdruck >)|  
|\<qualified-field-name>|\<Alias >. [\<Alias >...] \<Feld-Name >|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias>]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<Name >|  
|\<qualified-name>|Alias [.alias...]|  
|\<Name >|Alpha [Alpha &#124; Ziffer &#124; _ &#124; # &#124;: &#124;...]|  
|\<number>|Ziffer [Ziffer...]|  
|\<new-exp>|NEUE \<Feldtyp > [(\<Anzahl > [, \<Anzahl >])]|  
|\<field-type>|Ein OLE DB oder ADO-Datentyp.|  
|\<string>|Unicode-Zeichen [Unicode-Zeichen...]|  
|\<expression>|Ein Visual Basic für Applikationen-Ausdruck, dessen Operanden andere nicht-CALC-Spalten in der gleichen Zeile sind.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zugreifen auf Zeilen in einem hierarchischen Recordset](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Daten strukturieren (Übersicht)](../../../ado/guide/data/data-shaping-overview.md)   
 [Erforderlichen Anbieter Daten können strukturiert werden.](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Form "APPEND-Klausel](../../../ado/guide/data/shape-append-clause.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape-COMPUTE-Klausel](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications-Funktionen](../../../ado/guide/data/visual-basic-for-applications-functions.md)
