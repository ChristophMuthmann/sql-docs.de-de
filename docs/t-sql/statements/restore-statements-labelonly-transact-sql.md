---
title: RESTORE LABELONLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LABELONLY
- RESTORE_LABELONLY_TSQL
- LABELONLY_TSQL
- RESTORE LABELONLY
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE LABELONLY statement
- backup media [SQL Server], content information
ms.assetid: 7cf0641e-0d55-4ffb-9500-ecd6ede85ae5
caps.latest.revision: 46
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f69efb096931108fdaea084b337fcb319f7cfb6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="restore-statements---labelonly-transact-sql"></a>RESTORE-Anweisungen - LABELONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt ein Resultset mit Informationen zu den durch das gegebene Sicherungsmedium identifizierten Sicherungsmedien zurück.  
  
> [!NOTE]  
>  Die Beschreibungen der Argumente finden Sie [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RESTORE LABELONLY   
FROM <backup_device>   
[ WITH   
 {  
--Media Set Options  
   MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 Beschreibungen der RESTORE LABELONLY-Argumente finden Sie unter [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>Resultsets  
 Das Resultset von RESTORE LABELONLY besteht aus einer Zeile mit diesen Informationen.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**MediaName**|**vom Datentyp nvarchar(128)**|Name des Mediums.|  
|**MediaSetId**|**uniqueidentifier**|Eindeutige ID des Mediensatzes.|  
|**FamilyCount**|**int**|Die Anzahl der Medienfamilien im Mediensatz.|  
|**FamilySequenceNumber**|**int**|Sequenznummer dieser Familie.|  
|**MediaFamilyId**|**uniqueidentifier**|Eindeutige ID für die Medienfamilie.|  
|**MediaSequenceNumber**|**int**|Sequenznummer dieses Mediums in der Medienfamilie.|  
|**MediaLabelPresent**|**tinyint**|Gibt an, ob die Medienbeschreibung Folgendes enthält:<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] medienbezeichnung von Tape Format<br /><br /> **0** = medienbeschreibung|  
|**MediaDescription**|**nvarchar(255)**|Medienbeschreibung als Text oder die Medienbezeichnung von Tape Format.|  
|**SoftwareName**|**vom Datentyp nvarchar(128)**|Name der Sicherungssoftware, die die Bezeichnung geschrieben hat.|  
|**SoftwareVendorId**|**int**|Eindeutige ID des Softwareanbieters, der die Sicherung geschrieben hat.|  
|**MediaDate**|**datetime**|Datum und Uhrzeit des Zeitpunkts, an dem die Bezeichnung geschrieben wurde.|  
|**Mirror_Count**|**int**|Die Anzahl von Spiegeln in einem Spiegelsatz (1-4).<br /><br /> Hinweis: Die Bezeichnungen für verschiedene Spiegel in einem Satz geschrieben sind identisch.|  
|**IsCompressed**|**bit**|Gibt an, ob die Sicherung komprimiert ist:<br /><br /> 0 = nicht komprimiert<br /><br /> 1 = komprimierte|  
  
> [!NOTE]  
>  Wenn für den Mediensatz Kennwörter definiert sind, gibt RESTORE LABELONLY nur dann Informationen zurück, wenn im Befehl in der Option MEDIAPASSWORD das richtige Kennwort angegeben ist.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die Ausführung von RESTORE LABELONLY stellt eine schnelle Möglichkeit dar, den Inhalt des Sicherungsmediums herauszufinden. Da RESTORE LABELONLY nur den Medienheader liest, wird diese Anweisung schnell abgeschlossen, auch wenn Bandmedien mit hoher Kapazität verwendet werden.  
  
## <a name="security"></a>Sicherheit  
 In einem Sicherungsvorgang können optional Kennwörter für einen Mediensatz angegeben werden. Wenn ein Kennwort für einen Mediensatz definiert wurde, müssen Sie in der RESTORE-Anweisung das richtige Kennwort angeben. Das Kennwort verhindert nicht autorisierte Wiederherstellungsoptionen und Unbefugtes Anfügen von Sicherungssätzen an Medien mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tools. Mit einem Kennwort kann jedoch das Überschreiben eines Mediums mithilfe der Option FORMAT der BACKUP-Anweisung nicht verhindert werden.  
  
> [!IMPORTANT]  
>  Dieses Kennwort bietet also nur unzureichenden Schutz. Es soll vermeiden, dass autorisierte wie nicht autorisierte Benutzer mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tools fehlerhafte Wiederherstellungen durchführen. Es verhindert jedoch nicht das Lesen der Sicherungsdaten mit anderen Mitteln oder das Ersetzen des Kennworts. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Die bewährte Methode für den Schutz von Sicherungen werden verwahren von Sicherungsbändern an einem sicheren Ort oder Sichern in Datenträgerdateien, die durch ausreichend Zugriffssteuerungslisten (ACLs) geschützt sind. Die ACLs sollten für den Verzeichnisstamm eingerichtet werden, unter dem die Sicherungen erstellt werden.  
  
### <a name="permissions"></a>Berechtigungen  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen benötigen Sie die CREATE DATABASE-Berechtigung, um Informationen zu Sicherungssätzen oder Sicherungsmedien abzurufen. Weitere Informationen finden Sie unter [GRANT (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  

