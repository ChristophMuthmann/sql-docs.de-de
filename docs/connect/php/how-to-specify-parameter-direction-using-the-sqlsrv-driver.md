---
title: 'Vorgehensweise: Angeben der Parameterrichtung mit dem SQLSRV-Treiber | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4004fa498c01e73c99204bb0d36ac4bded66a9b
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>Vorgehensweise: Angeben der Parameterrichtung mit dem SQLSRV-Treiber
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Thema wird beschrieben, wie der SQLSRV-Treiber verwendet wird, um die Parameterrichtung anzugeben, wenn Sie eine gespeicherte Prozedur aufrufen. Die Richtung des Parameters angegeben ist, wenn Sie ein Parameterarray (Schritt 3) erstellen, die an [Sqlsrv_query](../../connect/php/sqlsrv-query.md) oder [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
### <a name="to-specify-parameter-direction"></a>Gehen Sie wie folgt vor, um die Parameterrichtung anzugeben:  
  
1.  Definieren Sie eine Transact-SQL-Abfrage, die eine gespeicherte Prozedur aufruft. Verwenden Sie Fragezeichen („?“) anstelle der Parameter, die an die gespeicherte Prozedur übergeben werden sollen. Diese Zeichenfolge z. B. ruft eine gespeicherte Prozedur auf (UpdateVacationHours), die zwei Parameter akzeptiert:Die Verwendung kanonischer Syntax stellt die empfohlene Vorgehensweise für das Abrufen gespeicherter Prozeduren dar.  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > Die Verwendung kanonischer Syntax stellt die empfohlene Vorgehensweise für das Abrufen gespeicherter Prozeduren dar. Weitere Informationen zur kanonischen Syntax finden Sie unter [Aufrufen einer gespeicherten Prozedur](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md).  
  
2.  Initialisieren oder aktualisieren Sie PHP-Variablen, die den Platzhaltern in der Transact-SQL-Abfrage entsprechen. Zum Beispiel aktualisiert folgender Code die zwei in der Prozedur UpdateVacationHours gespeicherten Parameter.  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > Variablen, die auf **NULL**, **DateTime**oder Streamtypen aktualisiert oder initialisiert werden, können nicht als Ausgabeparameter verwendet werden.  
  
3.  Verwenden Sie Ihre PHP-Variablen aus Schritt 2, um ein Array von Parameterwerten zu erstellen oder zu aktualisieren. Dieses soll der Reihenfolge der Parameterplatzhalter in der Transact-SQL-Zeichenfolge entsprechen. Geben Sie die Richtung  jedes Parameters im Array an. Die Richtung jedes Parameters wird bestimmt, auf zwei Arten: standardmäßig (für Eingabeparameter) oder mithilfe von **SQLSRV_PARAM_\***  -Konstanten (für Ausgabeparameter und bidirektionale Parameter). Der folgende Code gibt beispielsweise den *$employeeId* -Parameter als Eingabeparameter und den *$usedVacationHours* -Parameter als bidirektionaler Parameter an:  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    Um die Syntax zum Angeben der Parameterrichtung im Allgemeinen zu verstehen, nehmen Sie an, dass *$var1*, *$var2*, und *$var3* jeweils den Eingabe-, Ausgabe- und bidirektionalen Parametern entsprechen. Sie können die Richtung des Parameters in einer der folgenden Arten angeben:  
  
    -   Geben Sie den Eingabeparameter implizit und geben Sie einen bidirektionalen Parameter explizit Geben Sie Output-Parameters explizit an:  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   Input-Parameters explizit angeben, die Output-Parameter explizit angeben und einen bidirektionalen Parameter explizit angeben:  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  Führen Sie die Abfrage mit [Sqlsrv_query](../../connect/php/sqlsrv-query.md) oder mit [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) und [Sqlsrv_execute](../../connect/php/sqlsrv-execute.md). Der folgende Code verwendet beispielsweise die Verbindung *$conn* zum Ausführen der Abfrage *$tsql* mit Parameterwerten, die in *$params*angegeben sind:  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>Siehe auch  
[Gewusst wie: Abrufen von Eingabe-/Ausgabeparametern mit dem SQLSRV-Treiber](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
