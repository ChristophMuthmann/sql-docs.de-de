---
title: Informationen zu den Codebeispielen in der Dokumentation | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d24d29aba9db9d3626a456f87f799e00da1b42cc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="about-code-examples-in-the-documentation"></a>Informationen zu den Codebeispielen in der Dokumentation
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Es gibt einige Punkte zu beachten, wenn Sie die Codebeispiele in der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] -Dokumentation ausführen:  
  
-   In fast allen Beispielen wird davon ausgegangen, dass SQL Server 2005 oder höher (SQL Server 2008 oder höher bei Version 3.1) und die AdventureWorks-Datenbank auf dem lokalen Computer installiert sind.  
  
    Informationen zur Vorgehensweise beim Herunterladen der kostenlosen Editionen und Testversionen von SQL Server finden Sie unter [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Informationen zum Herunterladen der AdventureWorks-Datenbank finden Sie unter [Microsoft SQL Server-Beispiele und Communityprojekte](http://go.microsoft.com/fwlink/?LinkID=67739).  
  
    Weitere Informationen zum Installieren der AdventureWorks-Datenbank finden Sie unter [Anleitung: Installieren der AdventureWorks-Datenbank](http://go.microsoft.com/fwlink/?LinkID=65819).  
  
-   Fast alle Codebeispiele in dieser Dokumentation sollen über die Befehlszeile ausgeführt werden, die das automatische Testen aller Codebeispiele ermöglicht. Informationen über das Ausführen von PHP über die Befehlszeile finden Sie unter [PHP über die Befehlszeile](http://php.net/manual/en/features.commandline.php).  
  
-   Obwohl Beispiele dafür geschrieben sind, von der Befehlszeile ausgeführt zu werden, kann jedes Beispiel auch ausgeführt werden, indem Sie es in einem Browser aufrufen, ohne Änderungen am Skript vorzunehmen. Um zu erreichen, schöne Formatierung der Ausgabe, ersetzen Sie jeden "\n" durch "\<\/Br >" in jedem Beispiel, bevor Sie es in einem Browser aufrufen.  
  
-   Um jedes Beispiel auf das Wesentliche zu beschränken, wird die richtige Fehlerbehandlung nicht in allen Beispielen durchgeführt. Es wird empfohlen, dass jeder Aufruf einer **sqlsrv** -Funktion oder PDO-Methode auf Fehler überprüft wird und gemäß den Anforderungen der Anwendung behandelt wird.  
  
    Eine einfache Möglichkeit, Fehlerinformationen abzurufen, wenn ein Fehler aufgetreten ist, ist das Beenden des Skripts mit der folgenden Codezeile:  
  
    ```  
    die( print_r( sqlsrv_errors(), true));  
    ```  
  
    Oder falls Sie PDO verwenden,  
  
    ```  
    print_r ($stmt->errorInfo());  
    die();  
    ```  
  
    Weitere Informationen zum Behandeln von Fehlern und Warnungen finden Sie unter [Handhabung von Fehlern und Warnungen](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="see-also"></a>Siehe auch  
[Übersicht zum PHP-SQL-Treiber](../../connect/php/overview-of-the-php-sql-driver.md)
  

