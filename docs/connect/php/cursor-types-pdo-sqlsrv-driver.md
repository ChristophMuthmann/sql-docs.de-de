---
title: Cursortypen (PDO_SQLSRV-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d9757631940208f0f3ded1fe90eec8fbfd1b061
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="cursor-types-pdosqlsrv-driver"></a>Cursortypen (PDO_SQLSRV-Treiber)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Der PDO_SQLSRV-Treiber können Sie die scrollfähigen Resultsets mit mehreren Cursor erstellen.  
  
Informationen zum Angeben eines Cursors, der mit dem PDO_SQLSRV-Treiber und Codebeispiele finden Sie unter [PDO:: Prepare](../../connect/php/pdo-prepare.md).  
  
## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV und serverseitiger Cursor  
Vor, Version 3.0 der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], der PDO_SQLSRV-Treiber erlaubt Ihnen die Erstellung ein Resultsets, die mit einem serverseitigen Forward-only- oder statische Cursor. Ab Version 3.0 von der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], keysetgesteuerte und dynamische Cursor sind ebenfalls verfügbar.  
  
Sie können den Typ des serverseitigen Cursor angeben, mithilfe von PDO:: Prepare oder pdostatement:: setAttribute entweder Cursortyp auswählen:  
  
-   PDO:: ATTR_CURSOR = > PDO:: CURSOR_FWDONLY  
  
-   PDO:: ATTR_CURSOR = > PDO:: CURSOR_SCROLL  
  
Sie können einen Keyset- oder dynamischen Cursor anfordern, durch Angeben von PDO:: attr_cursor = > PDO:: cursor_scroll, und übergeben Sie den entsprechenden Wert zu sqlsrv_attr_cursor_scroll_type. Mögliche Werte, die an sqlsrv_attr_cursor_scroll_type übergeben werden:  
  
-   PDO::SQLSRV_CURSOR_BUFFERED  
  
-   PDO::SQLSRV_CURSOR_DYNAMIC  
  
-   PDO::SQLSRV_CURSOR_KEYSET_DRIVEN  
  
-   PDO::SQLSRV_CURSOR_STATIC  
  
## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV und die clientseitige Cursor  
Die clientseitige Cursor wurden hinzugefügt, Version 3.0 der der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] , mit der Sie ein komplettes Resultset im Arbeitsspeicher zwischengespeichert. Ein Vorteil ist, dass die Zeilenanzahl verfügbar ist, nachdem eine Abfrage ausgeführt wird.  
  
Die clientseitige Cursor sollte für kleine-mittelständische Resultsets verwendet werden. Große Resultsets sollten serverseitige Cursor verwenden.  
  
Eine Abfrage zurückgeben wird "false", wenn der Puffer nicht groß genug für ein komplettes Resultset, wenn Sie einen clientseitigen Cursor zu verwenden ist. Sie können die Größe des Puffers bis hin zur PHP-Speichergrenze erhöhen.  
  
Sie können konfigurieren, dass die Größe des Puffers, das Resultset mit der PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE-Attribut des enthält [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) oder [pdostatement:: setAttribute](../../connect/php/pdostatement-setattribute.md). Sie können auch die maximale Puffergröße festlegen, in der Datei "PHP.ini" mit pdo_sqlsrv.client_buffer_max_kb_size (z. B. pdo_sqlsrv.client_buffer_max_kb_size = 1024).  
  
Sie angeben, dass Sie einen clientseitigen Cursor mithilfe von PDO:: Prepare oder pdostatement:: setAttribute möchten, und wählen Sie die PDO:: attr_cursor = > PDO:: cursor_scroll Cursortyp.  Geben Sie Sie dann sqlsrv_attr_cursor_scroll_type = > PDO::SQLSRV_CURSOR_BUFFERED.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED));  
$stmt->execute();  
print $stmt->rowCount();  
  
echo "\n";  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
echo "\n..\n";  
  
$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );  
print "$row[Name]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );  
print "$row[1]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );  
print "$row[1]..\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );  
print_r($row);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Festlegen eines Cursortyps und Zeilenauswahl](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
