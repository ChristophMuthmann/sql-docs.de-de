---
title: ASSEMBLYPROPERTY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ASSEMBLYPROPERTY_TSQL
- ASSEMBLYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASSEMBLYPROPERTY statement
- assemblies [CLR integration], properties
ms.assetid: cf03d1b1-724c-48bf-a8df-3fe2586b150a
caps.latest.revision: 40
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 911459eec04d6ed2f20c0b6365b493bf938643df
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Diese Funktion gibt Informationen zu einer Eigenschaft einer Assembly zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
## <a name="arguments"></a>Argumente  
*assembly_name*  
Der Name der Assembly.
  
*property_name*  
Der Name einer Eigenschaft, zu der Informationen abgerufen werden sollen. *property_name* kann einen der folgenden Werte enthalten:
  
|value|Description|  
|---|---|
|**CultureInfo**|Gebietsschema der Assembly.|  
|**PublicKey**|Öffentlicher Schlüssel oder öffentlicher Schlüsseltoken der Assembly.|  
|**MvID**|Vollständige, vom Compiler generierte Versions-ID der Assembly.|  
|**VersionMajor**|Komponente für die Angabe der Hauptversion (erster Teil) der aus vier Teilen bestehenden Versions-ID der Assembly.|  
|**VersionMinor**|Komponente für die Angabe der Nebenversion (zweiter Teil) der aus vier Teilen bestehenden Versions-ID der Assembly.|  
|**VersionBuild**|Komponente für die Angabe der Buildnummer (dritter Teil) der aus vier Teilen bestehenden Versions-ID der Assembly.|  
|**VersionRevision**|Komponente für die Angabe der Revisionsnummer (vierter Teil) der aus vier Teilen bestehenden Versions-ID der Assembly.|  
|**SimpleName**|Einfacher Name der Assembly.|  
|**Aufbau**|Prozessorarchitektur der Assembly.|  
|**CLRName**|Kanonische Zeichenfolge, die den einfachen Namen, die Versionsnummer, die Kultur, den öffentlichen Schlüssel und die Architektur der Assembly codiert. Durch diesen Wert wird die CLR-seitige Assembly (Common Language Runtime) eindeutig identifiziert.|  
  
## <a name="return-type"></a>Rückgabetyp
**sql_variant**
  
## <a name="examples"></a>Beispiele  
In diesem Beispiel wird von einer `HelloWorld`-Assembly ausgegangen, die in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank registriert ist. Weitere Informationen finden Sie unter [Beispiel „Hello World“](http://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7).
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>Siehe auch
[CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)
  
  
