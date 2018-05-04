---
title: Sp_dsninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5a9c04611a342f81b6aa0a0b403eb6ff4ce8a643
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu ODBC- oder OLE DB-Datenquellen von dem Verteiler zurück, der dem aktuellen Server zugeordnet ist. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@dsn =**] **"***Dsn***"**  
 Der ODBC-Datenquellenname (Data Source Name, DSN) oder der Name des OLE DB-Verbindungsservers. *DSN* ist **varchar(128)**, hat keinen Standardwert.  
  
 [  **@infotype =**] **"***Infotyp***"**  
 Ist der Typ der zurückzugebenden Informationen. Wenn *Infotyp* nicht angegeben wird oder wenn NULL angegeben ist, werden alle Informationstypen zurückgegeben. *Infotyp* ist **varchar(128)**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**DBMS_NAME**|Gibt den Anbieter der Datenquelle an.|  
|**DBMS_VERSION**|Gibt die Version der Datenquelle an.|  
|**DATABASE_NAME**|Gibt den Datenbanknamen an.|  
|**SQL_SUBSCRIBER**|Gibt an, dass die Datenquelle ein Abonnent sein kann.|  
  
 [ **@login =**] **'***login***'**  
 Der Anmeldename für die Datenquelle. Wenn die Datenquelle einen Anmeldenamen aufweist, geben Sie NULL an, oder lassen Sie den Parameter weg. *Anmeldung*ist **varchar(128)**, hat den Standardwert NULL.  
  
 [  **@password =**] **"***Kennwort***"**  
 Das Kennwort für die Anmeldung. Wenn die Datenquelle einen Anmeldenamen aufweist, geben Sie NULL an, oder lassen Sie den Parameter weg. *Kennwort*ist **varchar(128)**, hat den Standardwert NULL.  
  
 [  **@dso_type=**] *Dso_type*  
 Der Datenquellentyp. *Dso_type* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**1** (Standard)|ODBC-Datenquelle (ODBC data source)|  
|**3**|OLE DB-Datenquelle|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Informationstyp**|**nvarchar(64)**|Informationstypen, wie z. B. DBMS_NAME, DBMS_VERSION, DATABASE_NAME, SQL_SUBSCRIBER.|  
|**Wert**|**nvarchar(512)**|Der Wert der verknüpften Informationstypen.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dsninfo** wird für alle Replikationstypen verwendet.  
  
 **Sp_dsninfo** ruft ODBC- oder OLE DB-Datenquelleninformationen, die anzeigt, ob die Datenbank für Replikationen oder Abfragen verwendet werden kann.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_dsninfo**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_enumdsn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
