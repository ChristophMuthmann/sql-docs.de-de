---
title: Elemente, die in SQL-Anweisungen verwendet | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60e0bf5d464b85aeca56d89fa130553f8114b813
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="elements-used-in-sql-statements"></a>Elemente, die in SQL­Anweisungen verwendet werden
Die folgenden Elemente werden in der SQL-Anweisungen, die zuvor aufgeführten verwendet.  
  
## <a name="element"></a>Element  
 *Base Tabellenbezeichner* :: = *definiert-Benutzernamens*  
  
 *Basis-Tabellenname* :: = *Base Tabellenbezeichner*  
  
 *Boolean-Faktor* :: = [NOT] *primäre boolescher Wert*  
  
 *boolescher Wert primäre* :: = Vergleich*-Prädikat* &#124; ( *Suchbedingung* )  
  
 *Boolean-Begriff* :: = *Boolean-Faktor* [AND *booleschen Ausdruck*]  
  
 *Zeichenfolge-Zeichenliterale* :: = "{*Zeichen*}..." (*Zeichen* ist ein beliebiges Zeichen im Zeichensatz der Treiber /-Datenquelle. Um ein einfaches literales Anführungszeichen (") in ein Zeichen-Zeichenfolgenliteral einzuschließen, verwenden Sie zwei literales Anführungszeichen [" "].)  
  
 *Spaltenbezeichner* :: = *definiert-Benutzernamens*  
  
 *Spaltennamen* :: = [*Tabellenname*.] *Spaltenbezeichner*  
  
 *Vergleichsoperator* :: = < &#124; > &#124; \<= &#124; > = &#124; = &#124; <>  
  
 *Vergleichsprädikat* :: = *Ausdruck* Vergleichsoperator Ausdruck  
  
 *Datentyp* :: = *-Zeichenfolgen-Datentyp* (*-Zeichenfolgen-Datentyp* ist einen beliebigen Datentyp aufweisen, die für die "" DATA_TYPE""-Spalte in der von ' SQLGetTypeInfo ' zurückgegebene Resultset entweder SQL_CHAR ist oder SQL_VARCHAR.)  
  
 *Ziffer* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *Dynamische Parameter* :: =?  
  
 *Ausdruck* :: = Begriff &#124; Ausdruck {+&#124;–} Begriff  
  
 *Faktor* :: = [*+*&#124;*–*]*primären*  
  
 *INSERT-Wert* :: =  
  
 *Dynamische parameter*  
  
 &#124;*literal*  
  
 &AMP;#124;NULL  
  
 &AMP;#124;BENUTZER  
  
 *Buchstabe* :: = *Kleinbuchstaben Fall Buchstaben &#124; oberen Groß-/Kleinschreibung der Buchstaben*  
  
 *Literal* :: = *Zeichenfolge Zeichenliterale*  
  
 *Kleinbuchstaben Fall Buchstaben* :: = eine &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; ich &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *Order by-Klausel* :: ORDER BY = *sortierspezifikation* [, *sortierspezifikation*]...  
  
 *primäre* :: = *Spaltenname*  
  
 &#124;*dynamische Parameter*  
  
 &#124;*literal*  
  
 &#124;( *Ausdruck* )  
  
 *Suchbedingung* :: = *booleschen Ausdruck* [oder *Suchbedingung*]  
  
 *SELECT-Liste* :: = \* &#124; *wählen Unterliste* [, *wählen Unterliste*]...  (*Select-Liste* darf keine Parameter enthalten.)  
  
 *Wählen Sie Unterliste* :: = *Ausdruck*  
  
 *Sort-Spezifikation* :: = {*unsigned Integer &#124; Spaltennamen*} [*ASC &#124; "DESC"*]  
  
 *Tabellenbezeichner* :: = *definiert-Benutzernamens*  
  
 *Tabellenname* :: = *Tabellenbezeichner*  
  
 *Tabellenverweis* :: = *Tabellenname*  
  
 *Tabelle der Verweisliste* :: = *Tabellenverweis* [,*Tabellenverweis*]...  
  
 *Begriff* :: = *Faktor* &#124; *Begriff* {\*&#124;*/*} *Faktor*  
  
 *unsigned Integer* :: = {*Ziffer*}  
  
 *obere Groß-/Kleinschreibung der Buchstaben* :: = *ein &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; ich &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; P &#124;Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *Benutzernamen definiert ein* :: = *Buchstaben*[*Ziffer* &#124; *Buchstaben* &#124; *_*]...
