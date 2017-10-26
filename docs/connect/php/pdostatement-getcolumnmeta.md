---
title: 'Pdostatement:: Getcolumnmeta | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 98925f324725be6c061c0baed6a3df320d1b39e2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ruft die Metadaten für eine Spalte ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>Parameter  
*$conn*: (ganze Zahl) die nullbasierte Nummer der Spalte, deren Metadaten Sie abrufen möchten.  
  
## <a name="return-value"></a>Rückgabewert  
Ein assoziatives Array (Schlüssel und Wert), das die Metadaten für die Spalte enthält. Im Abschnitt „Anmerkungen“ finden Sie eine Beschreibung für die Felder im Array.  
  
## <a name="remarks"></a>Hinweise  
Die folgende Tabelle beschreibt die Felder im durch „getColumnMeta“ zurückgegebenen Array.  
  
|NAME|VALUES|  
|--------|----------|  
|native_type|Gibt den PHP-Typ der Spalte an Immer Zeichenfolge.|  
|driver:decl_type|Gibt den SQL-Typ an, der verwendet wird, um den Spaltenwert in der Datenbank darzustellen Falls die Spalte im Resultset das Ergebnis einer Funktion ist, wird dieser Wert nicht von PDOStatement::getColumnMeta zurückgegeben.|  
|flags|Gibt die Flags (Kennzeichnungen), die für diese Spalte eingerichtet wurden, an Immer 0.|  
|NAME|Gibt den Namen der Spalte in der Datenbank an|  
|table|Gibt den Namen derjenigen Tabelle in der Datenbank an, welche die Spalte enthält Immer leer.|  
|Länge|Gibt die Länge der Spalte an|  
|precision|Gibt die numerische Genauigkeit dieser Spalte an|  
|pdo_type|Gibt den Typ dieser Spalte an, wie durch die PDO::PARAM_* Konstanten widergespiegelt. Immer PDO::PARAM_STR (2).|  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

