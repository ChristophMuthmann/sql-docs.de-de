---
title: Embedded SQL-Beispiel | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4f0125cda224073eb5357026461b1fc5a0bb955
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="embedded-sql-example"></a>Embedded SQL-Beispiel
Der folgende Code ist eine einfache embedded SQL, geschriebenes Programm in c Das Programm zeigt viele, aber nicht in allen eingebetteten SQL-Techniken. Das Programm fordert den Benutzer für eine Auftragsnummer ein, die Kundennummer, Vertriebsmitarbeiter und Status der Bestellung abgerufen und die abgerufene Informationen auf dem Bildschirm angezeigt.  
  
```  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 Beachten Sie Folgendes im Zusammenhang mit diesem Programm ein:  
  
-   **Hostvariable** die Hostvariablen deklariert werden, in einem Abschnitt eingeschlossen werden, indem Sie die **deklarieren Abschnitt beginnen** und **ENDABSCHNITT deklarieren** Schlüsselwörter. Jeder Variablenname Host wird durch einen Doppelpunkt (:)) vorangestellt, wenn es in einer eingebetteten SQL­Anweisung angezeigt wird. Der Doppelpunkt ermöglicht die vorkompilierten unterschieden Hostvariablen und Datenbankobjekte, z. B. Tabellen und Spalten, die den gleichen Namen haben.  
  
-   **Datentypen** die von einem DBMS und eine Hostsprache unterstützten Datentypen können sehr unterschiedlich sein. Dies wirkt sich auf Hostvariablen aus, da sie über eine duale Rolle spielen. Einerseits werden Hostvariablen Programmvariablen, deklariert und nicht von Host-sprachanweisungen bearbeitet. Andererseits, werden sie in embedded SQL-Anweisungen verwendet, um Datenbankdaten abzurufen. Ist keine Host-Language-Typ, der ein DBMS-Datentyp entspricht, konvertiert das DBMS die Daten automatisch. Da jede DBMS eigene Regeln und eigenheiten der Konvertierungsprozess zugeordnet hat, müssen der Hostvariablentypen sorgfältig gewählt.  
  
-   **Fehlerbehandlung** der DBMS-Laufzeitfehler an das Programm Anwendungen durch eine SQL Communications Area oder SQLCA meldet. Im vorangehenden Codebeispiel wird die erste embedded SQL-Anweisung SQLCA enthalten. Dies teilt die vorkompilierten SQLCA-Struktur in die Anwendung eingeschlossen werden sollen. Dies ist erforderlich, wenn das Programm das DBMS zurückgegebene Fehler verarbeitet werden. Die WHENEVER... GOTO-Anweisung weist die vorkompilierten Fehlerbehandlungscode, die Verzweigungen, um eine bestimmte Bezeichnung, wenn ein Fehler auftritt, generiert.  
  
-   **Singleton-SELECT** die Anweisung verwendet, um die Daten zurückzugeben ist eine Singleton-SELECT-Anweisung; d. h. gibt es nur eine einzelne Zeile mit Daten. Aus diesem Grund im Codebeispiel nicht deklarieren oder Cursor.
