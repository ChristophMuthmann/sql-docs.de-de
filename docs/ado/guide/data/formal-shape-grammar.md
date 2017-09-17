---
title: "Formale Grammatik für Formen | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae47b751e9e62d84188927186f186c6c9d344ce0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
|\<Form "-Command >|Form "[\<Tabelle exp > [[AS] \<Alias >]] [\<Form Aktion >]|  
|\<Tabelle exp >|{\<Anbieter Befehlstext >} &#124;<br /><br /> (\<Shape-Befehl >) &#124;<br /><br /> Tabelle \<quoted-Name > &#124;<br /><br /> \<in Anführungszeichen-Name >|  
|\<Shape-Action >|APPEND \<Alias Feldliste > &#124;<br /><br /> COMPUTE \<Alias Feldliste > [BY \<Feldliste >]|  
|\<Alias-Feld-List >|\<Alias-Field > [, \<Alias-Field >]|  
|\<Alias-Field >|\<Feld exp > [[AS] \<Alias >]|  
|\<Feld exp >|(\<Beziehung exp >) &#124;<br /><br /> \<berechnet exp > &#124;<br /><br /> \<Aggregat-exp > &#124;<br /><br /> \<neue exp >|  
|< Relation_exp >|\<Tabelle exp > [[AS] \<Alias >]<br /><br /> RELATE \<Relation-Cond-List >|  
|\<Relation-Cond-List >|\<Beziehung Cond > [, \<Beziehung Cond >...]|  
|\<Beziehung Cond >|\<Feld-Name > TO \<untergeordneten Ref >|  
|\<untergeordnete Ref >|\<Feld-Name > &#124;<br /><br /> PARAMETER \<Param-Ref >|  
|\<Param-Ref >|\<Anzahl >|  
|\<Feld-List >|\<Feld-Name > [, \<Feld-Name >]|  
|\<Aggregat-exp >|SUM (\<qualified-Feld-Name >) &#124;<br /><br /> AVG (\<qualified-Feld-Name >) &#124;<br /><br /> MIN (\<qualified-Feld-Name >) &#124;<br /><br /> MAX (\<qualified-Feld-Name >) &#124;<br /><br /> COUNT (\<qualifiziert Alias > &#124; \<qualifizierte Name >) &#124;<br /><br /> STDEV (\<qualified-Feld-Name >) &#124;<br /><br /> Alle (\<qualified-Feld-Name >)|  
|\<berechnet exp >|CALC (\<Ausdruck >)|  
|\<Qualified-Feld-Name >|\<Alias >. [\<Alias >...] \<Feld-Name >|  
|\<Alias >|\<in Anführungszeichen-Name >|  
|\<Feld-Name >|\<in Anführungszeichen-Name > [[AS] \<Alias >]|  
|\<in Anführungszeichen-Name >|"\<Zeichenfolge >" &#124;<br /><br /> "\<Zeichenfolge >" &#124;<br /><br /> [\<Zeichenfolge >] &#124;<br /><br /> \<Name >|  
|\<qualifizierte Name >|Alias [.alias...]|  
|\<Name >|Alpha [Alpha &#124; Ziffer &#124; _ &#124; # &#124;: &#124;...]|  
|\<Anzahl >|Ziffer [Ziffer...]|  
|\<neue exp >|NEUE \<Feldtyp > [(\<Anzahl > [, \<Anzahl >])]|  
|\<Typ des Felds >|Ein OLE DB oder ADO-Datentyp.|  
|\<Zeichenfolge >|Unicode-Zeichen [Unicode-Zeichen...]|  
|\<Ausdruck >|Ein Visual Basic für Applikationen-Ausdruck, dessen Operanden andere nicht-CALC-Spalten in der gleichen Zeile sind.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zugreifen auf Zeilen in einem hierarchischen Recordset](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Daten strukturieren (Übersicht)](../../../ado/guide/data/data-shaping-overview.md)   
 [Erforderlichen Anbieter Daten können strukturiert werden.](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Form "APPEND-Klausel](../../../ado/guide/data/shape-append-clause.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape-COMPUTE-Klausel](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic für Applikationen-Funktionen](../../../ado/guide/data/visual-basic-for-applications-functions.md)
