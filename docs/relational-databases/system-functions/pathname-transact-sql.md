---
title: Pfadname (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PathName_TSQL
- PathName
dev_langs:
- TSQL
helpviewer_keywords:
- PathName FILESTREAM [SQL Server]
ms.assetid: 6b95ad90-6c82-4a23-9294-a2adb74934a3
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 880ee799e833a3181d3ee1a6eaa51b25f1456a58
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="pathname-transact-sql"></a>PathName (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Pfad eines FILESTREAM BLOB (Binary Large Object) zurück. Die OpenSqlFilestream-API verwendet diesen Pfad ein Handle zurück, die eine Anwendung zum Arbeiten mit BLOB-Daten mithilfe von Win32-APIs verwenden kann. PathName ist schreibgeschützt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
column_name.PathName ( @option [ , use_replica_computer_name ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *column_name*  
 Der Spaltenname einer **varbinary(max)** FILESTREAM-Spalte. *column_name* muss ein Spaltenname sein. Es kann sich hierbei weder um einen Ausdruck noch um das Ergebnis einer CAST- oder CONVERT-Anweisung handeln.  
  
 Des Pfadnamens für eine Spalte des anderen Datentyps oder für eine **varbinary(max)** Columnthat verfügt nicht über die FILESTREAM-Speicher-Attribut wird dazu führen, dass eine Abfrage-Kompilierzeitfehler.  
  
 *@option*  
 Eine ganze Zahl [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) , der definiert, wie die Serverkomponente des Pfads formatiert werden soll. *@option*einer der folgenden Werte ist möglich. Die Standardeinstellung ist 0.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Gibt den Servernamen in ein BIOS-Format konvertiert zurück, z. B.: `\\SERVERNAME\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F19F7-38EA-4AB0-BB89-E6C545DBD3F9`|  
|1|Gibt den Servernamen ohne Konvertierung, z. B. an:`\\ServerName\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F1`|  
|2|Gibt den vollständigen Serverpfad, z. B. an:`\\ServerName.MyDomain.com\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F19F7-38EA-4AB0-BB89-E6C545DBD3F9`|  
  
 *use_replica_computer_name*  
 Ein Bitwert, der definiert, wie den Namen des Servers in einer Always On-verfügbarkeitsgruppe zurückgegeben werden soll.  
  
 Wenn die Datenbank nicht zu einer Always On-verfügbarkeitsgruppe gehört, wird der Wert dieses Arguments ignoriert. Der Computername wird immer im Pfad verwendet.  
  
 Wenn die Datenbank zu einer Always On-verfügbarkeitsgruppe gehört zu gruppieren, klicken Sie dann den Wert der *Use_replica_computer_name* hat folgenden Effekt auf das Ergebnis der **PathName** Funktion:  
  
|Wert|Description|  
|-----------|-----------------|  
|Nicht angegeben.|Die Funktion gibt den virtuellen Netzwerknamen in (VNN) im Pfad zurück.|  
|0|Die Funktion gibt den virtuellen Netzwerknamen in (VNN) im Pfad zurück.|  
|1|Die Funktion gibt den Computernamen im Pfad zurück.|  
  
## <a name="return-type"></a>Rückgabetyp  
 **nvarchar(max)**  
  
## <a name="return-value"></a>Rückgabewert  
 Der zurückgegebene Wert ist der vollqualifizierte logische oder NETBIOS-Pfad des BLOB. Pfadname gibt keine IP-Adresse zurück. NULL wird zurückgegeben, wenn das FILESTREAM BLOB nicht erstellt wurde.  
  
## <a name="remarks"></a>Hinweise  
 Die Spalte ROWGUID muss in jeder Abfrage sichtbar sein, die PathName aufruft.  
  
 Ein FILESTREAM BLOB kann nur mit [!INCLUDE[tsql](../../includes/tsql-md.md)] erstellt werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-reading-the-path-for-a-filestream-blob"></a>A. Lesen des Pfads für einen FILESTREAM-BLOB  
 Im folgenden Beispiel wird `PathName` der Variablen `nvarchar(max)` zugewiesen.  
  
```sql  
DECLARE @PathName nvarchar(max);  
SET @PathName = (  
    SELECT TOP 1 photo.PathName()  
    FROM dbo.Customer  
    WHERE LastName = 'CustomerName'  
    );  
```  
  
### <a name="b-displaying-the-paths-for-filestream-blobs-in-a-table"></a>B. Anzeigen der Pfade für FILESTREAM-BLOBs in einer Tabelle  
 Im folgenden Beispiel werden die Pfade für drei FILESTREAM BLOBs erstellt und angezeigt.  
  
```sql  
-- Create a FILESTREAM-enabled database.  
-- The c:\data directory must exist.  
CREATE DATABASE PathNameDB  
ON  
PRIMARY ( NAME = ArchX1,  
    FILENAME = 'c:\data\archdatP1.mdf'),  
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = ArchX3,  
    FILENAME = 'c:\data\filestreamP1')  
LOG ON  ( NAME = ArchlogX1,  
    FILENAME = 'c:\data\archlogP1.ldf');  
GO  
  
USE PathNameDB;  
GO  
  
-- Create a table, add some records, and  
-- create the associated FILESTREAM  
-- BLOB files.  
  
CREATE TABLE TABLE1  
    (  
        ID int,  
        RowGuidColumn UNIQUEIDENTIFIER  
                      NOT NULL UNIQUE ROWGUIDCOL,  
        FILESTREAMColumn varbinary(MAX) FILESTREAM  
    );  
GO  
  
INSERT INTO TABLE1 VALUES  
 (1, NEWID(), 0x00)  
,(2, NEWID(), 0x00)  
,(3, NEWID(), 0x00);  
GO  
  
SELECT FILESTREAMColumn.PathName() AS 'PathName' FROM TABLE1;  
  
--Results  
--PathName  
------------------------------------------------------------------------------------------------------------  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\DD67C792-916E-4A76-8C8A-4A85DC5DB908  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\2907122B-2560-4CB9-86DC-FBE7ABA1843B  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\922BE0E0-CAB9-4403-90BF-945BD258E4BC  
--  
--(3 row(s) affected)  
GO  
  
--Drop the database to clean up.  
USE master;  
GO  
DROP DATABASE PathNameDB;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Binary Large Object &#40;BLOB&#41;-Daten &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [GET_FILESTREAM_TRANSACTION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md)   
 [ZUgreifen auf FILESTREAM-Daten mit OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
  
