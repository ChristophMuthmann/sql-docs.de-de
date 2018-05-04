---
title: Simulieren von positioniert, Update- und Delete-Anweisungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1448481938ff0ef8e20ba4e6a85801b65024cbcc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simulieren positionierte Update- und Delete-Anweisungen
Wenn die Datenquelle nicht positioniertes Update unterstützt und-Anweisungen DELETE, kann der Treiber diese simulieren. Beispielsweise wird der ODBC-Cursorbibliothek simuliert positioniertes Update und delete-Anweisungen. Die allgemeine Strategie zum Simulieren positionierte Update- und Delete-Anweisungen ist positionierte Anweisungen gesuchte Vorgängen zu konvertieren. Dies erfolgt durch Ersetzen der **WHERE CURRENT OF** -Klausel mit einer durchsuchten **, in dem** -Klausel, die die aktuelle Zeile identifiziert.  
  
 Angenommen, da die Spalte CustID jede Zeile in der Customers-Tabelle eindeutig identifiziert, Löschanweisung die positionierte  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 u. u. in konvertiert werden  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 Der Treiber möglicherweise verwenden Sie eine der folgenden *Zeilenbezeichner* in der **, in denen** Klausel:  
  
-   Spalten, deren Werte dienen, um eindeutig jede Zeile in der Tabelle zu identifizieren. Beispielsweise Aufrufen **SQLSpecialColumns** mit SQL_BEST_ROWID gibt die optimale(n) Spalte(n) oder eine Gruppe von Spalten, die diesen Zweck dienen.  
  
-   Pseudospalten, gebotenen einige Datenquellen, für die, die jede Zeile eindeutig identifiziert. Diese möglicherweise abrufbar durch Aufrufen von **SQLSpecialColumns**.  
  
-   Ein eindeutiger Index, falls verfügbar.  
  
-   Alle Spalten im Resultset.  
  
 Genau die Spalten, die ein Treiber, in verwenden sollte der **, in denen** -Klausel es erstellt hängt vom Treiber. Für einige Daten können Datenquellen verwendet, bestimmen eine Zeilen-ID kostenintensiv sein. Es ist jedoch schneller ausgeführt und wird sichergestellt, dass eine simulierte Anweisung aktualisiert oder löscht jeweils nur eine Zeile. Abhängig von den Funktionen des zugrunde liegenden DBMS kann die mit Zeilen-ID einrichten ressourcenintensiv sein. Es ist jedoch schneller ausgeführt und wird sichergestellt, dass eine simulierte-Anweisung aktualisiert oder löscht nur eine Zeile. Die Möglichkeit, alle Spalten im Resultset ist in der Regel viel einfacher einrichten. Allerdings ist Sie langsamer ausgeführt und, wenn Spalten eine Zeile nicht eindeutig identifiziert, kann dazu führen, wird unbeabsichtigt aktualisierten oder gelöschten Zeilen, insbesondere, wenn die select-Liste für das Ergebnis festgelegt enthält nicht alle Spalten, die in der zugrunde liegenden Tabelle vorhanden.  
  
 Abhängig von dem der genannten Strategien des Treibers unterstützt, wenn eine Anwendung kann auswählen, welche Strategie sie den Treiber für die Verwendung mit der SQL_ATTR_SIMULATE_CURSOR-Anweisungsattribut möchte. Obwohl für eine Anwendung, riskieren Sie unbeabsichtigt aktualisieren oder Löschen einer Zeile ungerade Eindruck entsteht, kann die Anwendung dieses Risiko entfernen, indem Sie sicherstellen, dass die Spalten im Resultset jede Zeile im Resultset eindeutig identifizieren. Dies spart dem Treiber den Aufwand zu diesem Zweck müssen.  
  
 Wenn der Treiber entscheidet, eine Zeilen-ID verwenden, fängt die **SELECT FOR UPDATE** -Anweisung, die das Resultset erstellt. Wenn die Spalten in der select-Liste nicht effektiv eine Zeile identifiziert, fügt der Treiber benötigten Spalten am Ende der select-Liste. Einige Datenquellen haben eine einzelne Spalte, die eine Zeile wie die ROWID-Spalte in Oracle immer eindeutig; Wenn eine solche Spalte verfügbar ist, verwendet der Treiber dies aus. Der Treiber andernfalls ruft **SQLSpecialColumns** für jede Tabelle in der **FROM** -Klausel, um eine Liste der Spalten abzurufen, die jede Zeile eindeutig identifizieren. Eine allgemeine Einschränkung, die durch diese Technik entsteht ist, dass Cursor Simulation schlägt fehl, wenn es mehr als eine Tabelle in der **FROM** Klausel.  
  
 Unabhängig davon, wie der Treiber Zeilen identifiziert, in der Regel entfernt die **FOR UPDATE OF** -Klausel aus der **SELECT FOR UPDATE** Anweisung vor dem Senden an die Datenquelle. Die **FOR UPDATE OF** -Klausel wird verwendet, nur mit, Update positioniert und-Anweisungen DELETE. Datenquellen, die nicht unterstützt werden, positioniert Update und Delete-Anweisungen in der Regel nicht unterstützt wird.  
  
 Wenn die Anwendung eine positionierte Update- oder Delete-Anweisung zur Ausführung übermittelt, wird der Treiber ersetzt die **WHERE CURRENT OF** -Klausel mit einer **, in denen** Klausel, die die Zeilen-ID enthält. Die Werte dieser Spalten werden abgerufen, aus einem Cache beibehalten, die vom Treiber für jede Spalte, die verwendet wird, in der **, in denen** Klausel. Nachdem der Treiber ersetzt hat die **, in dem** -Klausel, sendet er die Anweisung, mit der Datenquelle für die Ausführung.  
  
 Nehmen wir beispielsweise an, dass die Anwendung die folgende Anweisung zum Erstellen eines Resultsets übermittelt:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Wenn die Anwendung SQL_ATTR_SIMULATE_CURSOR eine Garantie der Eindeutigkeit anfordern festgelegt wurde, und wenn die Datenquelle keine Pseudospalte, die eine Zeile immer eindeutig identifiziert bereitstellt, der Treiber ruft **SQLSpecialColumns** für die Customers-Tabelle ermittelt, dass CustID ist der Schlüssel zur Customers-Tabelle und zur Auswahlliste hinzugefügt und entfernt die **FOR UPDATE OF** Klausel:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Wenn die Anwendung keine Garantie dafür Eindeutigkeit angefordert hat, entfernt der Treiber nur die **FOR UPDATE OF** Klausel:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Angenommen Sie, die Anwendung führt einen Bildlauf durch das Resultset und sendet die folgenden positioniertes Update-Anweisung für die Ausführung, dabei ist der Name des Cursors Cust über das Resultset:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Wenn die Anwendung keine Garantie dafür Eindeutigkeit angefordert hat, wird der Treiber ersetzt die **, in denen** Klausel und bindet die CustID-Parameter an die Variable in deren Cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Wenn die Anwendung keine Garantie dafür Eindeutigkeit angefordert hat, wird der Treiber ersetzt die **, in dem** -Klausel und bindet die Parameter Name, Adresse und Telefonnummer in diese Klausel, um die Variablen in seinem Cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
