---
title: "Aggregieren von Funktionen, die CALC-Funktion und das NEW-Schlüsselwort | Microsoft Docs"
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
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f24280f155fd5ec6bd86b8486b0f8f77338d8eb6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>Aggregatfunktionen, die CALC-Funktion und das NEW-Schlüsselwort
Strukturieren von Daten unterstützt die folgenden Funktionen: Ist im Kapitel über das mit der Spalte verarbeitet werden sollen zugewiesene Name der *Kapitel-Alias*.  
  
 Ein Kapitel-Alias kann entweder vollständig qualifiziert, bestehend aus jeder führende zum Kapitel mit Kapitel-Spaltenname der *Spaltenname,* durch Punkte voneinander getrennt. Beispielsweise enthält das übergeordnete Kapitel Kap1, untergeordnete Kapitel Kap2, besitzt eine Mengenspalte "Amt" und dann der qualifizierte Namen wäre chap1.chap2.amt.  
  
|Aggregatfunktionen|Description|  
|-------------------------|-----------------|  
|SUM (*Kapitel-Alias*.* Spaltennamen*)|Berechnet die Summe aller Werte in der angegebenen Spalte.|  
|AVG (*Kapitel-Alias*.* Spaltennamen*)|Berechnet den Durchschnitt aller Werte in der angegebenen Spalte.|  
|MAX (*Kapitel-Alias*.* Spaltennamen*)|Berechnet den maximalen Wert in der angegebenen Spalte.|  
|MIN (*Kapitel-Alias*.* Spaltennamen*)|Berechnet den minimalen Wert in der angegebenen Spalte.|  
|COUNT (*Kapitel-Alias*[.* Spaltennamen*])|Zählt die Anzahl der Zeilen in den angegebenen Alias. Wenn eine Spalte angegeben wird, werden nur Zeilen, die für die diese Spalte ungleich Null ist in der Zählung enthalten.|  
|STDEV (*Kapitel-Alias*.* Spaltennamen*)|Berechnet die Standardabweichung in der angegebenen Spalte.|  
|Alle (*Kapitel-Alias*.* Spaltennamen*)|Ein Wert der angegebenen Spalte. Alle hat einen vorhersagbaren Wert nur, wenn der Wert der Spalte für alle Zeilen im Kapitel identisch ist.<br /><br /> **Hinweis** enthält die Spalte nicht den gleichen Wert für alle Zeilen im Kapitel, gibt der SHAPE-Befehl nach dem Zufallsprinzip einen der Werte der Wert der eine beliebige Funktion sein.|  
  
|berechneter Ausdruck|Description|  
|---------------------------|-----------------|  
|CALC (*Ausdruck*)|Berechnet einen beliebigen Ausdruck verwenden, jedoch nur in der Zeile die **Recordset** , die den CALC-Funktion enthält. Jeder Ausdruck mit diesen [Visual Basic for Applications (VBA) Funktionen](../../../ado/guide/data/visual-basic-for-applications-functions.md) ist zulässig.|  
  
|NEW-Schlüsselwort|Description|  
|-----------------|-----------------|  
|NEUE *Feldtyp* [(*Breite* &#124; *Skalierung* &#124; *Genauigkeit* &#124; *Fehler* [, *Skalierung* &#124; *Fehler*])]|Fügt eine leere Spalte des angegebenen Typs, der **Recordset**.|  
  
 Die *Feldtyp* mit dem NEW-Schlüsselwort übergeben werden können, eine der folgenden Datentypen.  
  
|OLE DB-Datentypen|ADO-Datentyp equivalent(s)|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|AdBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|AdBinary AdVarBinary, adLongVarBinary|  
|DBTYPE_STR|AdChar, AdVarChar, adLongVarChar|  
|DBTYPE_WSTR|AdWChar, AdVarWChar, adLongVarWChar|  
|DBTYPE_NUMERIC|Type|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 Wenn das neue Feld vom Typ Decimal (um in OLE DB DBTYPE_DECIMAL oder in ADO AdDecimal) ist, müssen Sie die Genauigkeit und Dezimalstellenanzahl Werte angeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Daten strukturiert werden, Beispiel](../../../ado/guide/data/data-shaping-example.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)

