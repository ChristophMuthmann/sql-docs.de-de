---
title: Sp_copysubscription (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9feaac9bb5dfd23bbdd4422f3ad9908663bc64c7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spcopysubscription-transact-sql"></a>sp_copysubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  Die Funktion für anfügbare Abonnements ist als veraltet markiert und wird in einer zukünftigen Version entfernt. Diese Funktion sollte bei neuen Entwicklungen nicht verwendet werden. Für Mergeveröffentlichungen, die mithilfe von parametrisierten Filtern partitioniert werden, ist es empfehlenswert, die neuen Funktionen von partitionierten Momentaufnahmen zu verwenden. Diese vereinfachen die Initialisierung zahlreicher Abonnements. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md). Für nicht partitionierte Veröffentlichungen können Sie ein Abonnement mit einer Sicherung initialisieren. Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird.  
  
 Kopiert eine Abonnementdatenbank, die über Pullabonnements, nicht jedoch über Pushabonnements verfügt. Es können nur einzelne Dateidatenbanken kopiert werden. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@filename =**] **"***File_name***"**  
 Der Zeichenfolgenwert, der den vollständigen Pfad einschließlich des Dateinamens angibt, in dem eine Kopie der Datendatei (.mdf) gespeichert wird. *Dateiname* ist **nvarchar(260)**, hat keinen Standardwert.  
  
 [  **@temp_dir=**] **"***Temp_dir***"**  
 Der Name des Verzeichnisses, das die temporären Dateien enthält. *Temp_dir* ist **nvarchar(260)**, hat den Standardwert NULL. Bei NULL wird die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standarddatenverzeichnis verwendet werden. Das Verzeichnis sollte über ausreichenden Speicherplatz verfügen, um eine Datei aufzunehmen, die der Größe aller Datenbankdateien auf dem Abonnenten zusammen entspricht.  
  
 [  **@overwrite_existing_file=**] **"***Overwrite_existing_file***"**  
 Ist ein optionales boolesches Flag, das angibt, ob eine vorhandene Datei mit demselben Namen im angegebenen überschrieben werden soll oder nicht  **@filename** . *Overwrite_existing_file*ist **Bit**, hat den Standardwert **0**. Wenn **1**, überschreibt er die angegebene Datei  **@filename** , sofern vorhanden. Wenn **0**, die gespeicherte Prozedur fehlschlägt, wenn die Datei vorhanden ist, und die Datei nicht überschrieben wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_copysubscription** wird in allen Replikationstypen zum Kopieren einer Abonnementdatenbank in eine Datei als Alternative zum Anwenden einer Momentaufnahme auf dem Abonnenten verwendet. Die Datenbank muss so konfiguriert sein, dass ausschließlich Pullabonnements unterstützt werden. Benutzer mit entsprechenden Berechtigungen können Kopien der Abonnementdatenbank erstellen und die Abonnementdatei (MSF) dann per E-Mail, durch Kopieren oder Übertragen an einen anderen Abonnenten senden. Dort kann die Datei dann als Abonnement angefügt werden.  
  
 Die Größe der kopierten Abonnementdatenbank muss weniger als 2 Gigabyte (GB) betragen.  
  
 **Sp_copysubscription** ist nur für Datenbanken mit Clientabonnements unterstützt und kann nicht ausgeführt werden, wenn die Datenbank serverabonnements hat.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_copysubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Alternative Speicherorte für Momentaufnahmeordner](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
