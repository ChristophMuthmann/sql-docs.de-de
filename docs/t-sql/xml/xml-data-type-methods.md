---
title: XML-Datentypmethoden | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3a08e2e0c49c707150df9f350cb9060203fd6f62
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="xml-data-type-methods"></a>xml-Datentypmethoden
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Sie können die **Xml** -Datentypmethoden Abfragen eine XML-Instanz, die in einer Variable oder Spalte gespeichert **Xml** Typ. Die Themen in diesem Abschnitt wird beschrieben, wie mithilfe der **Xml** -Datentypmethoden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Abfrage &#40; &#41; -Methode &#40; Xml-Datentyp &#41;](../../t-sql/xml/query-method-xml-data-type.md)|Beschreibt das Verwenden der query()-Methode zum Ausführen einer Abfrage über eine XML-Instanz.|  
|[Wert &#40; &#41; -Methode &#40; Xml-Datentyp &#41;](../../t-sql/xml/value-method-xml-data-type.md)|Beschreibt das Verwenden der value()-Methode zum Abrufen eines Werts eines SQL-Typs aus einer XML-Instanz.|  
|[vorhanden &#40; &#41; -Methode &#40; Xml-Datentyp &#41;](../../t-sql/xml/exist-method-xml-data-type.md)|Beschreibt das Verwenden der exist()-Methode, um zu bestimmen, ob eine Abfrage ein nicht leeres Ergebnis zurückgibt.|  
|[Ändern Sie &#40; &#41; -Methode &#40; Xml-Datentyp &#41;](../../t-sql/xml/modify-method-xml-data-type.md)|Beschreibt, wie die Modify()-Methode an [XML Data Modification Language &#40; XML DML &#41; ](../../t-sql/xml/xml-data-modification-language-xml-dml.md)Anweisungen zum Durchführen von Aktualisierungen.|  
|[Knoten &#40; &#41; -Methode &#40; Xml-Datentyp &#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|Beschreibt das Verwenden nodes()-Methode, um XML in mehrere Zeilen aufzuteilen, wodurch Teile von XML-Dokumenten in Rowsets übertragen werden.|  
|[Binding Relational Data Inside XML Data (Einbinden relationaler Daten in XML-Daten)](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|Beschreibt, wie Sie Nicht-XML-Daten in XML binden können.|  
|[Guidelines for Using xml Data Type Methods (Richtlinien zum Verwenden von Methoden des xml-Datentyps)](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|Enthält Richtlinien zum Verwenden der **Xml** -Datentypmethoden.|  
  
 Der Aufruf dieser Methoden erfolgt mit der benutzerdefinierten Typmethodenaufrufsyntax. Beispiel:  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  Die **Xml** -Datentypmethoden **query()**, **value()**, und **exist()** gibt NULL zurück, wenn für eine NULL XML-Instanz ausgeführt. Darüber hinaus **modify()** keine zurückgibt, aber **nodes()** Rowsets und ein leeres Rowset zurückgegeben, mit einem NULL-Eingabe.  
  
## <a name="see-also"></a>Siehe auch  
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
