---
title: 'PDO:: __construct | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0161c9ac0fdb75848e045fa49025270e3c475501
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Stellt eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbank her.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>Parameter  
*$dsn*: eine Zeichenfolge, die dem Präfixnamen (immer `sqlsrv`), einem Doppelpunkt und dem Server-Schlüsselwort. Beispiel: `"sqlsrv:server=(local)"`. Sie können optional auch andere Schlüsselwörter angeben. Unter [Connection Options](../../connect/php/connection-options.md) finden Sie eine Beschreibung des Server-Schlüsselworts und anderer Verbindungsschlüsselwörter. Die gesamte *$dsn* wird in Anführungszeichen gesetzt, daher sollten die einzelnen Verbindungsschlüsselwörter nicht in separate Anführungszeichen gesetzt werden.  
  
*$username*: Optional. Eine Zeichenfolge, die den Namen des Benutzers enthält. Um eine Verbindung mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung herzustellen, geben Sie die Anmelde-ID an. Um eine Verbindung mithilfe der Windows-Authentifizierung herzustellen, geben Sie `""`an.  
  
*$password*: Optional. Eine Zeichenfolge, die das Kennwort des Benutzers enthält. Um eine Verbindung mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung herzustellen, geben Sie das Kennwort an. Um eine Verbindung mithilfe der Windows-Authentifizierung herzustellen, geben Sie `""`an.  
  
*$Driver_options*: Dies ist Optional. Sie können PDO-Treiber-Manager-Attribute angeben und [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] bestimmte Treiber-Attribute – PDO:: sqlsrv_attr_encoding, PDO:: sqlsrv_attr_direct_query. Ein ungültiges Attribut generiert keine Ausnahme. Ungültige Attribute generieren Ausnahmen, wenn sie mit [PDO::setAttribute](../../connect/php/pdo-setattribute.md)spezifiziert werden.  
  
## <a name="return-value"></a>Rückgabewert  
Gibt ein PDO-Objekt zurück. Wenn der Fehler auftritt, wird ein PDOException-Objekt zurückgegeben.  
  
## <a name="exceptions"></a>Ausnahmen  
PDOException  
  
## <a name="remarks"></a>Hinweise  
Sie können ein Verbindungsobjekt schließen, indem Sie die Instanz auf NULL setzen.  
  
Nachdem eine Verbindung wird PDO:: ErrorCode 01000 anstelle von 00000 angezeigt.  
  
Wenn PDO:: __construct aus irgendeinem Grund fehlschlägt, wird eine Ausnahme ausgelöst, selbst wenn PDO:: attr_errmode auf PDO:: errmode_silent festgelegt ist.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
Dieses Beispiel zeigt, wie Sie eine Verbindung mit einem Server mithilfe der Windows-Authentifizierung herstellen und eine Datenbank angeben.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example"></a>Beispiel  
Dieses Beispiel zeigt, wie Sie eine Verbindung mit einem Server herstellen und später die Datenbank festlegen.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
