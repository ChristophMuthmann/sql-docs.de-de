---
title: GetFileNamespacePath (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GetFileNamespacePath
- GetFileNamespacePath_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetFileNamespacePath function
ms.assetid: b393ecef-baa8-4d05-a268-b2f309fce89a
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f568c1743c229ea3b0a5978510ee699e128ab033
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getfilenamespacepath-transact-sql"></a>GetFileNamespacePath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt den UNC-Pfad für eine Datei bzw. ein Verzeichnis in einer FileTable zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<column-name>.GetFileNamespacePath(is_full_path, @option)  
```  
  
## <a name="arguments"></a>Argumente  
 *Spaltenname*  
 Der Spaltenname der VARBINARY(MAX) **file_stream** -Spalte in einer FileTable.  
  
 Der Wert von *column-name* muss ein gültiger Spaltenname sein. Es kann sich hierbei weder um einen Ausdruck noch um einen Wert handeln, der von einer Spalte eines anderen Datentyps konvertiert oder umgewandelt wurde.  
  
 *is_full_path*  
 Ein ganzzahliger Ausdruck, der angibt, ob ein relativer oder ein absoluter Pfad zurückgegeben werden soll. *is_full_path* kann einen der folgenden Werte aufweisen:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Gibt den relativen Pfad innerhalb des Verzeichnisses auf Datenbankebene zurück.<br /><br /> Standardwert|  
|**1**|Gibt den vollständigen UNC-Pfad zurück, der mit `\\computer_name`beginnt.|  
  
 *@option*  
 Ein ganzzahliger Ausdruck, der definiert, wie die Serverkomponente des Pfads formatiert werden soll. *@option* Dabei kann es sich um einen der folgenden Werte aufweisen:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Gibt den in ein NetBIOS-Format konvertierten Servernamen zurück. Beispiel:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> Dies ist der Standardwert.|  
|**1**|Gibt den Servernamen ohne Konvertierung zurück. Beispiel:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|Gibt den vollständigen Serverpfad zurück. Beispiel:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>Rückgabetyp  
 **nvarchar(max)**  
  
 Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz in einem Failovercluster gruppiert ist, dann ist der Name des Computers, der als Teil dieses Pfads zurückgegeben wird der virtuelle Hostname für die gruppierte Instanz.  
  
 Wenn die Datenbank zu einer Always On-verfügbarkeitsgruppe gehört die **FileTableRootPath** Funktion gibt den virtuellen Netzwerknamen (VNN) statt des Computernamens zurück.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Der von der **GetFileNamespacePath** -Funktion zurückgegebene Pfad ist ein logischer Verzeichnis- oder Dateipfad im folgenden Format:  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\...`  
  
 Dieser logische Pfad ist keine direkte Entsprechung eines physischen NTFS-Pfads. Er wird vom Dateisystem-Filtertreiber von FILESTREAM und vom FILESTREAM-Agent in den physischen Pfad übersetzt. Durch diese Unterscheidung zwischen dem logischen und dem physischen Pfad kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten intern neu organisieren, ohne die Gültigkeit des Pfads zu beeinträchtigen.  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Um Code und Anwendungen vom aktuellen Computer und von der Datenbank unabhängig zu halten, sollten Sie keinen Code schreiben, der auf absoluten Dateipfaden basiert. Rufen Sie stattdessen den vollständigen Pfad für eine Datei mit der Funktion **FileTableRootPath** und der Funktion **GetFileNamespacePath** zur Laufzeit ab, wie im folgenden Beispiel gezeigt. Die **GetFileNamespacePath** -Funktion gibt standardmäßig den relativen Pfad der Datei unter dem Stammpfad der Datenbank zurück.  
  
```sql  
USE MyDocumentDatabase;  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
  
@fullPath = varchar(1000);  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath() FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen wird gezeigt, wie die **GetFileNamespacePath** -Funktion aufgerufen wird, um den UNC-Pfad für eine Datei oder ein Verzeichnis in einer FileTable abzurufen.  
  
```  
-- returns the relative path of the form “\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath() AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
  
-- returns “\\MyServer\MSSQLSERVER\MyDocumentDatabase\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath(1, Null) AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit Verzeichnissen und Pfaden in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
