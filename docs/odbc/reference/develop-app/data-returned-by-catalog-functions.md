---
title: "Von Katalogfunktionen zurückgegebenen Daten | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 39d795314d2333c5d33cb55057b68e652082ae89
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-returned-by-catalog-functions"></a>Daten, die von Katalogfunktionen zurückgegeben werden.
Jeder Katalogfunktion gibt die Daten als Resultset zurück. Dieses Resultset unterscheidet sich nicht von anderen Resultsets. Er wird in der Regel generiert durch eine vordefinierte parametrisiert **wählen** -Anweisung, die im Treiber fest programmiert oder in einer Prozedur in der Datenquelle gespeichert ist. Informationen zum Abrufen von Daten aus einem Resultset, finden Sie unter [Ergebnis festgelegt erstellt wurde?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 Das Resultset für jede Katalogfunktion wird in der Referenz-Eintrag für diese Funktion beschrieben. Zusätzlich zu den aufgelisteten Spalten kann das Resultset treiberspezifischen Spalten nach der letzten vordefinierte Spalte enthalten. Diese Spalten (sofern vorhanden) werden in der Treiberdokumentation beschrieben.  
  
 Anwendungen sollten treiberspezifischen Spalten relativ zum Ende des Resultsets binden. Sie sollten also die Nummer einer Spalte treiberspezifische berechnen, als die Anzahl der letzten Spalte – mit abgerufen **SQLNumResultCols** – abzüglich der Anzahl der Spalten, die nach der erforderlichen Spalte auftreten. Dies spart müssen die Anwendung zu ändern, wenn neue Spalten, auf das Ergebnis hinzugefügt werden festgelegt in zukünftigen Versionen von ODBC oder dem Treiber. Für dieses Schema zu arbeiten müssen Treiber neue treiberspezifische Spalten vor dem alten treiberspezifischen Spalten hinzufügen, sodass Spaltennummern relativ zum Ende des Resultsets nicht geändert werden.  
  
 Bezeichner, die im Resultset zurückgegeben werden sind nicht angeführten, auch wenn sie Sonderzeichen enthalten. Nehmen wir beispielsweise an den Bezeichner Anführungszeichen (d. h. treiberspezifische und die zurückgegebenen über **SQLGetInfo**) ist ein doppeltes Anführungszeichen (") und" Accounts Payable "Tabelle enthält eine Spalte mit dem Namen Customer Name. In der Zeile zurückgegebenes **SQLColumns** für diese Spalte ist der Wert der Spalte TABLE_NAME "Accounts Payable", nicht "Accounts Payable", und der Wert der COLUMN_NAME-Spalte Kundennamen, nicht "Kundenname". Um die Namen der Kunden in der Tabelle "Accounts Payable" abzurufen, würde die Anwendung diese Namen Zitat:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Weitere Informationen finden Sie unter [Bezeichner in Anführungszeichen](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 Die Katalogfunktionen basieren auf einer SQL-ähnlichen Autorisierungsmodell, in dem basierend auf einem Benutzernamen und Kennwort eine Verbindung hergestellt, und nur Daten, die für die der Benutzer eine Berechtigung besitzt, werden zurückgegeben. Der Kennwortschutz für einzelne Dateien, die nicht in dieses Modell passt, wird die Treiber definiert.  
  
 Durch die Katalogfunktionen zurückgegebenen Resultsets können fast nie aktualisiert werden, und Anwendungen sollten nicht erwarten, damit die Struktur der Datenbank zu ändern, indem Sie Daten in diesen Resultsets geändert werden.
