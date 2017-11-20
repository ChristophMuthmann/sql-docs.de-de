---
title: Elemente, die in SQL-Anweisungen verwendet | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c29dcd40090a380c124a0c72b07d5993d4295829
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
 *Datentyp* :: = *-Zeichenfolgen-Datentyp* (*-Zeichenfolgen-Datentyp* einen beliebigen Datentyp aufweisen, die für die "" DATA_TYPE""-Spalte in der von ' SQLGetTypeInfo ' zurückgegebene Resultset entweder SQL_CHAR ist ist oder SQL_VARCHAR sein.)  
  
 *Ziffer* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *Dynamische Parameter* :: =?  
  
 *Ausdruck* :: = Begriff &#124; Ausdruck {+ &#124; –} Begriff  
  
 *Faktor* :: = [*+*&#124; *–*]*primären*  
  
 *INSERT-Wert* :: =  
  
 *Dynamische parameter*  
  
 &#124; *literal*  
  
 &#124; NULL  
  
 &#124; BENUTZER  
  
 *Buchstabe* :: = *Kleinbuchstaben Fall Buchstaben &#124; oberen Groß-/Kleinschreibung der Buchstaben*  
  
 *Literal* :: = *Zeichenfolge Zeichenliterale*  
  
 *Kleinbuchstaben Fall Buchstaben* :: = eine &#124; b &#124; c &#124; d &#124; e &#124; f &#124; Zeitpunkt der warnungsg &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; Q &#124; R &#124; s &#124; t &#124; u &#124; V &#124; w &#124; X &#124; j &#124; z  
  
 *Order by-Klausel* :: ORDER BY = *sortierspezifikation* [, *sortierspezifikation*]...  
  
 *primäre* :: = *Spaltenname*  
  
 &#124; *dynamische Parameter*  
  
 &#124; *literal*  
  
 &#124; ( *Ausdruck* )  
  
 *Suchbedingung* :: = *booleschen Ausdruck* [oder *Suchbedingung*]  
  
 *SELECT-Liste* :: = \* &#124; *wählen Unterliste* [, *wählen Unterliste*]...  (*Select-Liste* darf keine Parameter enthalten.)  
  
 *Wählen Sie Unterliste* :: = *Ausdruck*  
  
 *Sort-Spezifikation* :: = {*unsigned Integer &#124; Spaltenname*} [*ASC &#124; "DESC"*]  
  
 *Tabellenbezeichner* :: = *definiert-Benutzernamens*  
  
 *Tabellenname* :: = *Tabellenbezeichner*  
  
 *Tabellenverweis* :: = *Tabellenname*  
  
 *Tabelle der Verweisliste* :: = *Tabellenverweis* [,*Tabellenverweis*]...  
  
 *Begriff* :: = *Faktor* &#124; *Begriff* {\*&#124; */* } *Faktor*  
  
 *unsigned Integer* :: = {*Ziffer*}  
  
 *obere Groß-/Kleinschreibung der Buchstaben* :: = *A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; Ich &#124; J &#124; K &#124; L &#124; Übe &#124; N &#124; O &#124; P &#124; Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; J &#124; Z*  
  
 *Benutzernamen definiert ein* :: = *Buchstaben*[*Ziffer* &#124; *Buchstaben* &#124; *_*]...

