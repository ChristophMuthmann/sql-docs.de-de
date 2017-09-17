---
title: 'Schritt 4: Herstellen belastbarer SQL mit PHP | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8013474f-48e9-43d5-ab89-7b0504044468
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f81efd8241edcf1ff437570713f6bb05ca8103f8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="step-4-connect-resiliently-to-sql-with-php"></a>Schritt 4: Herstellen belastbarer SQL-Verbindungen mit PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  
Das Demoprogramm ist so konzipiert, dass ein vorübergehender Fehler beim Versuch, eine Verbindung zu einer Wiederholung führt. Aber ein vorübergehender Fehler während des Abfragebefehls bewirkt, dass das Programm die Verbindung verwirft und erstellen eine neue Verbindung, bevor der Abfragebefehl wiederholt wird. Wird weder empfohlen noch diese Entwurfsoption. Das Demoprogramm veranschaulicht einige Flexibilität des Entwurfs, die Ihnen zur Verfügung steht.  
  
Die Länge der in diesem Codebeispiel ist fällig größtenteils die Logik zum Abfangen der Ausnahme.   
  
Die Main-Methode wird in "Program.cs". Die Aufrufliste wird wie folgt ausgeführt:  
* Main ruft ConnectAndQuery.  
* ConnectAndQuery Aufrufe EstablishConnection.  
* EstablishConnection Aufrufe IssueQueryCommand.  
  
Die [sqlsrv_query()](http://php.net/manual/en/function.sqlsrv-query.php) Funktion kann verwendet werden, um ein Resultset aus einer Abfrage an SQL-Datenbank abzurufen. Diese Funktion ist im Wesentlichen akzeptiert jede Abfrage und das Verbindungsobjekt und gibt ein Resultset, das mit der Verwendung von durchlaufen werden kann [sqlsrv_fetch_array()](http://php.net/manual/en/function.sqlsrv-fetch-array.php).  
  
```php

    <?php  
        // Variables to tune the retry logic.    
        $connectionTimeoutSeconds = 30;  // Default of 15 seconds is too short over the Internet, sometimes.  
        $maxCountTriesConnectAndQuery = 3;  // You can adjust the various retry count values.  
        $secondsBetweenRetries = 4;  // Simple retry strategy.  
        $errNo = 0;  
        $serverName = "tcp:yourdatabase.database.windows.net,1433";  
        $connectionOptions = array("Database"=>"AdventureWorks",  
           "Uid"=>"yourusername", "PWD"=>"yourpassword", "LoginTimeout" => $connectionTimeoutSeconds);  
        $conn;  
        $errorArr = array();  
        for ($cc = 1; $cc <= $maxCountTriesConnectAndQuery; $cc++)  
        {  
            $errorArr = array();  
            $ctr = 0;  
            // [A.2] Connect, which proceeds to issue a query command.  
            $conn = sqlsrv_connect($serverName, $connectionOptions);    
            if( $conn == true)  
            {  
                echo "Connection was established";  
                echo "<br>";  
  
                $tsql = "SELECT [CompanyName] FROM SalesLT.Customer";  
                $getProducts = sqlsrv_query($conn, $tsql);  
                if ($getProducts == FALSE)  
                    die(FormatErrors(sqlsrv_errors()));  
                $productCount = 0;  
                $ctr = 0;  
                while($row = sqlsrv_fetch_array($getProducts, SQLSRV_FETCH_ASSOC))  
                {     
                    $ctr++;  
                    echo($row['CompanyName']);  
                    echo("<br/>");  
                    $productCount++;  
                    if($ctr>10)  
                        break;  
                }  
                sqlsrv_free_stmt($getProducts);  
                break;  
            }  
            // Adds any the error codes from the SQL Exception to an array.  
            else {    
                if( ($errors = sqlsrv_errors() ) != null) {  
                    foreach( $errors as $error ) {  
                        $errorArr[$ctr] = $error['code'];  
                        $ctr = $ctr + 1;  
                    }  
                }  
                $isTransientError = TRUE;  
                // [A.4] Check whether sqlExc.Number is on the whitelist of transients.  
                $isTransientError = IsTransientStatic($errorArr);  
                if ($isTransientError == TRUE)  // Is a static persistent error...  
                {  
                    echo("Persistent error suffered, SqlException.Number==". $errorArr[0].". Program Will terminate.");  
                    echo "<br>";  
                    // [A.5] Either the connection attempt or the query command attempt suffered a persistent SqlException.  
                    // Break the loop, let the hopeless program end.  
                    exit(0);  
                }  
                // [A.6] The SqlException identified a transient error from an attempt to issue a query command.  
                // So let this method reloop and try again. However, we recommend that the new query  
                // attempt should start at the beginning and establish a new connection.  
                if ($cc >= $maxCountTriesConnectAndQuery)  
                {  
                    echo "Transient errors suffered in too many retries - " . $cc ." Program will terminate.";  
                    echo "<br>";  
                    exit(0);  
                }  
                echo("Transient error encountered.  SqlException.Number==". $errorArr[0]. " . Program might retry by itself.");    
                echo "<br>";  
                echo $cc . " Attempts so far. Might retry.";  
                echo "<br>";  
                // A very simple retry strategy, a brief pause before looping. This could be changed to exponential if you want.  
                sleep(1*$secondsBetweenRetries);  
            }  
            // [A.3] All has gone well, so let the program end.  
        }  
        function IsTransientStatic($errorArr) {  
            $arrayOfTransientErrorNumbers = array(4060, 10928, 10929, 40197, 40501, 40613);  
            $result = array_intersect($arrayOfTransientErrorNumber, $errorArr);  
            $count = count($result);  
            if($count >= 0) //change to > 0 later.  
                return TRUE;  
        }  
    ?>
```
