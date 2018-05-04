---
title: Formale Grammatik für Formen | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3658526e3b63069f3fce0dc1431804b5304070b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
|\<table-exp>|{\<Anbieter Befehlstext >}&#124;<br /><br /> (\<Shape-Befehl >)&#124;<br /><br /> Tabelle \<quoted-Name >&#124;<br /><br /> \<in Anführungszeichen-Name >|  
|\<Shape-Action >|APPEND \<Alias Feldliste >&#124;<br /><br /> COMPUTE \<Alias Feldliste > [BY \<Feldliste >]|  
|\<aliased-field-list>|\<Alias-Field > [, \<Alias-Field >]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<Beziehung exp >)&#124;<br /><br /> \<berechnet exp >&#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> RELATE \<Relation-Cond-List >|  
|\<relation-cond-list>|\<Beziehung Cond > [, \<Beziehung Cond >...]|  
|\<relation-cond>|\<Feld-Name > TO \<untergeordneten Ref >|  
|\<child-ref>|\<Feld-Name >&#124;<br /><br /> PARAMETER \<Param-Ref >|  
|\<param-ref>|\<Anzahl >|  
|\<field-list>|\<Feld-Name > [, \<Feld-Name >]|  
|\<aggregate-exp>|SUM (\<qualified-Feld-Name >)&#124;<br /><br /> AVG (\<qualified-Feld-Name >)&#124;<br /><br /> MIN (\<qualified-Feld-Name >)&#124;<br /><br /> MAX (\<qualified-Feld-Name >)&#124;<br /><br /> COUNT (\<qualifiziert Alias > &#124; \<qualifizierte Name >)&#124;<br /><br /> STDEV (\<qualified-Feld-Name >)&#124;<br /><br /> Alle (\<qualified-Feld-Name >)|  
|\<calculated-exp>|CALC (\<Ausdruck >)|  
|\<Qualified-Feld-Name >|\<Alias >. [\<Alias >...] \<Feld-Name >|  
|\<alias>|\<in Anführungszeichen-Name >|  
|\<Feld-Name >|\<in Anführungszeichen-Name > [[AS] \<Alias >]|  
|\<in Anführungszeichen-Name >|"\<Zeichenfolge >"&#124;<br /><br /> "\<Zeichenfolge >"&#124;<br /><br /> [\<Zeichenfolge >]&#124;<br /><br /> \<Name >|  
|\<qualifizierte Name >|Alias [.alias...]|  
|\<Name >|Alpha [Alpha &#124; Ziffer &#124; _ &#124; # &#124; : &#124; ...]|  
|\<Anzahl >|Ziffer [Ziffer...]|  
|\<new-exp>|NEUE \<Feldtyp > [(\<Anzahl > [, \<Anzahl >])]|  
|\<field-type>|Ein OLE DB oder ADO-Datentyp.|  
|\<Zeichenfolge >|Unicode-Zeichen [Unicode-Zeichen...]|  
|\<Ausdruck >|Ein Visual Basic für Applikationen-Ausdruck, dessen Operanden andere nicht-CALC-Spalten in der gleichen Zeile sind.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zugreifen auf Zeilen in einem hierarchischen Recordset](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Daten strukturieren (Übersicht)](../../../ado/guide/data/data-shaping-overview.md)   
 [Erforderlichen Anbieter Daten können strukturiert werden.](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Form "APPEND-Klausel](../../../ado/guide/data/shape-append-clause.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape-COMPUTE-Klausel](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications-Funktionen](../../../ado/guide/data/visual-basic-for-applications-functions.md)
