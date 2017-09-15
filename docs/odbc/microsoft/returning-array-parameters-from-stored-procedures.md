---
title: "Zurückgeben der Arrayparameter von gespeicherten Systemprozeduren | Microsoft Docs"
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
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 2018069b-da5d-4cee-a971-991897d4f7b5
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 23b57350ae1abccf39e20f6b8ed6d14fa7d04a7b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="returning-array-parameters-from-stored-procedures"></a>Zurückgeben von Arrayparameter von gespeicherten Prozeduren
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 In Oracle 7.3 ist es keine Möglichkeit, ein PL/SQL-Programm einen PL/SQL-Datensatztyp außer zuzugreifen. Weist eine gepackte Prozedur oder Funktion ein formales Argument als einen PL/SQL-Datensatztyp definiert, ist es nicht möglich, formalen Arguments als Parameter gebunden. Verwenden Sie den Typ der PL/SQL-Tabelle in der Microsoft ODBC-Treiber für Oracle, um Arrayparametern aus, die die richtigen Escapesequenzen enthält Prozeduren aufzurufen.  
  
 Verwenden Sie die folgende Syntax zum Aufrufen der Prozedur:  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  Die \<Max angeforderten Datensätze >-Parameter muss größer als oder gleich der Anzahl der Zeilen im Resultset vorhanden sein. Oracle zurückgibt, andernfalls einen Fehler, der vom Treiber an dem Benutzer übergeben wird.  
>   
>  PL/SQL-Datensätze können nicht als Arrayparametern verwendet werden. Jedes Arrayparameter kann nur eine Spalte einer Datenbanktabelle darstellen.  
  
 Im folgende Beispiel definiert ein Paket enthält zwei Prozeduren, die verschiedenen Resultsets zurückgeben, und klicken Sie dann bietet zwei Möglichkeiten zum Zurückgeben von Resultsets aus dem Paket.  
  
## <a name="package-definition"></a>Paketdefinition:  
  
```  
CREATE OR REPLACE PACKAGE SimplePackage AS  
  
TYPE t_id is TABLE of  NUMBER(5)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Course is TABLE of VARCHAR2(10)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Dept is TABLE of VARCHAR2(5)  
    INDEX BY BINARY_INTEGER;  
  
PROCEDURE proc1  
   (  
   o_id             OUT    t_id,  
   ao_course       OUT    t_Course,  
   ao_dept         OUT    t_Dept  
   );  
  
TYPE t_pk1Type1 IS TABLE OF VARCHAR2(100) INDEX BY BINARY_INTEGER;  
TYPE t_pk1Type2 IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   );  
  
END SimplePackage;  
  
CREATE OR REPLACE PACKAGE BODY SimplePackage AS  
    PROCEDURE  proc1 ( o_id OUT t_id,  
    ao_course OUT t_Course, ao_dept OUT t_Dept   ) AS  
    BEGIN  
          o_id(1):= 200;  
          ao_course(1) :=  'M101';  
          ao_dept(1) :=  'EEE' ;  
  
          o_id(2) := 201;  
          ao_course(2) :=  'PHY320';  
          ao_dept(2) :=  'ECE' ;  
  
     END proc1;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   )  
AS  
   i   NUMBER;  
BEGIN  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg2(i) := 'Row Number ' || to_char(i);  
   END LOOP;  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg3(i) := i;  
   END LOOP;  
END proc2;  
END SimplePackage;  
```  
  
#### <a name="to-invoke-procedure-proc1"></a>Zum Aufrufen der Prozedur PROC1  
  
1.  Gibt alle Spalten in ein einzelnes Resultset zurück:  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  Geben Sie jede Spalte als ein einzelnes Resultset zurück:  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     Dies gibt drei Resultsets, eine für jede Spalte zurück.  
  
#### <a name="to-invoke-procedure-proc2"></a>Zum Aufrufen der Prozedur PROC2  
  
1.  Gibt alle Spalten in ein einzelnes Resultset zurück:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  Geben Sie jede Spalte als ein einzelnes Resultset zurück:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 Stellen Sie sicher, dass Ihre Anwendungen alle fetch die Resultsets mithilfe der [SQLMoreResults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API. Weitere Informationen finden Sie unter der *ODBC Programmer's Reference*.  
  
> [!NOTE]  
>  In der ODBC-Treiber für Oracle, Version 2.0 können Oracle-Funktionen, die PL/SQL-Arrays zurückgeben verwendet werden, um Resultsets zurückzugeben.
