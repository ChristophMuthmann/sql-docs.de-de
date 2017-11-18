---
title: 'Vorgehensweise: Herstellen einer Verbindung mithilfe von SQL Server-Authentifizierung | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to the server, SQL Server Authentication
ms.assetid: 8d298830-3186-47e7-aef6-586b457901c1
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8d4305d3b6dd25f3a06cda56db8e69fcd5d09972
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-connect-using-sql-server-authentication"></a>Vorgehensweise: Herstellen einer Verbindung mithilfe der SQL Server-Authentifizierung
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] unterstützt SQL Server-Authentifizierung beim Herstellen einer Verbindung mit SQL Server.  
  
SQL Server-Authentifizierung sollte nur verwendet werden, wenn Windows-Authentifizierung nicht möglich ist. Informationen zum Herstellen einer Verbindung mit Windows-Authentifizierung finden Sie unter [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Wenn Sie SQL Server-Authentifizierung verwenden, um die Verbindung mit SQL Server herzustellen, müssen die folgenden Punkte berücksichtigt werden:  
  
-   SQL Server-Authentifizierung im gemischten Modus muss auf dem Server aktiviert sein.  
  
-   Benutzer-ID und Kennwort (*UID* und *PWD* Verbindungsattribute im SQLSRV-Treiber) müssen festgelegt werden, wenn Sie versuchen, eine Verbindung herzustellen. Benutzer-ID und Kennwort müssen einem gültigen SQL Server-Benutzer und einem Kennwort zugeordnet sein.  
  
> [!NOTE]  
> Kennwörter, die eine schließende geschweifte Klammer (}) enthalten, müssen mit einer zweiten schließenden geschweiften Klammer escaped werden. Wenn das SQL Server-Kennwort z. B. „pass}word“ ist, muss der Wert des *PWD* -Verbindungsattributs auf „pass}}word“ festgelegt werden.  
  
Wenn Sie SQL Server-Authentifizierung verwenden, um die Verbindung mit SQL Server herzustellen, sollen folgende Vorsichtsmaßnahmen getroffen werden:  
  
-   Schützen (verschlüsseln) Sie die Anmeldeinformationen, die über das Netzwerk vom Webserver an die Datenbank übergeben werden. Anmeldeinformationen werden standardmäßig ab SQL Server 2005 verschlüsselt. Setzen Sie zur Erhöhung der Sicherheit das Encrypt-Verbindungsattribut auf „on“, um alle Daten zu verschlüsseln, die an den Server gesendet werden.  
  
> [!NOTE]  
> Das Encrypt-Verbindungsattribut auf „on“ zu setzen, kann zu Leistungseinbußen führen, da Datenverschlüsselung rechenintensiv sein kann.  
  
-   Schließen Sie nicht die Werte für die Verbindungsattribute *UID* und *PWD* in Klartext in PHP-Skripts ein. Diese Werte sollten in einem anwendungsspezifischen Verzeichnis mit den entsprechenden eingeschränkten Berechtigungen gespeichert werden.  
  
-   Vermeiden Sie die Verwendung des *sa* -Kontos. Ordnen Sie die Anwendung einem Datenbankbenutzer zu, der über die erforderlichen Berechtigungen verfügt und weisen Sie ihm ein sicheres Kennwort zu.  
  
> [!NOTE]  
> Außer Benutzer-ID und Kennwort können weitere Verbindungsattribute gesetzt werden, wenn Sie eine Verbindung herstellen. Eine vollständige Liste der unterstützten Verbindungsattribute finden Sie unter [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird der SQLSRV-Treiber mit SQL Server-Authentifizierung für die Verbindung mit einer lokalen Instanz von SQL Server verwendet. Die Werte für die erforderlichen *UID* und *PWD* Verbindungsattribute stammen aus anwendungsspezifischen Textdateien, *uid.txt* und *pwd.txt*in der *C:\AppData* Verzeichnis. Nachdem die Verbindung hergestellt wurde, wird der Server abgefragt, um die Anmeldung des Benutzers zu überprüfen.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über den Browser ausgeführt wird, werden alle Ausgaben im Browser geschrieben.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
  
/* Get UID and PWD from application-specific files.  */  
$uid = file_get_contents("C:\AppData\uid.txt");  
$pwd = file_get_contents("C:\AppData\pwd.txt");  
$connectionInfo = array( "UID"=>$uid,  
                         "PWD"=>$pwd,  
                         "Database"=>"AdventureWorks");  
  
/* Connect using SQL Server Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Dieses Beispiel verwendet den PDO_SQLSRV- Treiber, um zu veranschaulichen, wie Sie eine Verbindung mit SQL Server-Authentifizierung herstellen.  
  
```  
<?php  
   $serverName = "(local)";   
   $database = "AdventureWorks";  
  
   // Get UID and PWD from application-specific files.   
   $uid = file_get_contents("C:\AppData\uid.txt");  
   $pwd = file_get_contents("C:\AppData\pwd.txt");  
  
   try {  
      $conn = new PDO( "sqlsrv:server=$serverName;Database = $database", $uid, $pwd);   
      $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
   }  
  
   catch( PDOException $e ) {  
      die( "Error connecting to SQL Server" );   
   }  
  
   echo "Connected to SQL Server\n";  
  
   $query = 'select * from Person.ContactType';   
   $stmt = $conn->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
      print_r( $row );   
   }  
  
   // Free statement and connection resources.   
   $stmt = null;   
   $conn = null;   
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
[SUSER_SNAME (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=106382)  
[Vorgehensweise: Erstellen einer SQL Server-Anmeldung](http://go.microsoft.com/fwlink/?LinkId=106325)  
[Vorgehensweise: Erstellen eines Datenbankbenutzers](http://go.microsoft.com/fwlink/?LinkId=106327)  
[Verwalten von Benutzern, Rollen und Anmeldungen](http://go.microsoft.com/fwlink/?LinkId=106329)  
[Trennung von Benutzer und Schema](http://go.microsoft.com/fwlink/?LinkId=106330)  
[GRANT-Objektberechtigungen (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=106332)  
  

