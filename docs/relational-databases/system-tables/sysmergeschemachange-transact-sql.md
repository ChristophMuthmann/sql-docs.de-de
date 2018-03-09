---
title: Sysmergeschemachange (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f42fbeba8639216d5a95414430099fbd5bde0b07
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält Informationen zu den vom Momentaufnahme-Agent generierten veröffentlichten Artikeln. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**pubid**|**uniqueidentifier**|Die ID der Veröffentlichung.|  
|**artid**|**uniqueidentifier**|Die ID des Artikels.|  
|**Schemaversion**|**int**|Die Nummer der letzten Schemaänderung|  
|**SchemaGuid**|**uniqueidentifier**|Die eindeutige ID des letzten Schemas|  
|**SchemaType**|**int**|Der Typ der Schemaänderung:<br /><br /> **-1** = ungültig.<br /><br /> **1** = SQL-Befehl.<br /><br /> **2** = Schemaskript.<br /><br /> **3** = native Massenkopierprogramm-Hilfsprogramm (BCP).<br /><br /> **4** = BCP-Zeichenmodus.<br /><br /> **5** = zuletzt erfasste Generierung.<br /><br /> **6** = zuletzt gesendete Generierung.<br /><br /> **7** = Verzeichnis.<br /><br /> **8** = Priorität.<br /><br /> **9** = Beibehaltungsdauer.<br /><br /> **10** = Triggerskript.<br /><br /> **11** = Alter Table-Anweisung.<br /><br /> **12** = alle erneut initialisieren.<br /><br /> **13** = ALTER TABLE (nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).<br /><br /> **14** = Sie beim Hochladen erneut initialisieren.<br /><br /> **15** = einschränkungs- und indexskript.<br /><br /> **16** = Metadatencleanup.<br /><br /> **17** = zuletzt gesendete Generierung aktualisieren.<br /><br /> **18** = abwärtskompatibilitätsgrad.<br /><br /> **19** = Abonnenteninformationen überprüfen.<br /><br /> **20** = ordnungsgemäß partitioniert.<br /><br /> **21** = benutzerdefinierter Konfliktlöser.<br /><br /> **22** = Verarbeitungsreihenfolge von Artikeln.<br /><br /> **23** = veröffentlicht in transaktionsveröffentlichung.<br /><br /> **24** = Fehlerkompensation.<br /><br /> **25** = alternativer momentaufnahmeordner.<br /><br /> **26** = nur herunterladbar.<br /><br /> **27** = nachverfolgung löschen.<br /><br /> **40** = momentaufnahmeskript vor Erstellung.<br /><br /> **45** = momentaufnahmeskript nach Erstellung.<br /><br /> **46** = on-Demand-Benutzerskript.<br /><br /> **50** = Momentaufnahme beginnen.<br /><br /> **51** = Momentaufnahme-headerende.<br /><br /> **52** = momentaufnahmeachspann.<br /><br /> **53** = Protokoll FTP (File Transfer)-Adresse.<br /><br /> **54** = FTP-Port.<br /><br /> **55** = FTP-Unterverzeichnis.<br /><br /> **56** = komprimierte Momentaufnahme.<br /><br /> **57** = FTP-Anmeldung.<br /><br /> **58** = FTP-Kennwort.<br /><br /> **60** = Systemskript vor Erstellung.<br /><br /> **61** = gespeichertes prozedurschema.<br /><br /> **62** = sichtschema.<br /><br /> **63** = benutzerdefiniertes funktionsschema.<br /><br /> **64** = Sichtindizes.<br /><br /> **65** = erweiterte Eigenschaften.<br /><br /> **66** = überprüfen.<br /><br /> **67** = vor der Momentaufnahme-SQL-Befehl.<br /><br /> **71** = dynamische momentaufnahmeüberprüfung.<br /><br /> **80** = System systemeigenes BCP 9.0.<br /><br /> **81** = Systemtabelle, BCP 9.0 im Zeichenmodus.<br /><br /> **82** = System systemeigenes BCP 9.0 (nur global).<br /><br /> **83** = Systemtabelle, BCP 9.0 im (Zeichenmodus nur global).<br /><br /> **84** = System systemeigenes BCP 9.0 (Lightweight).<br /><br /> **85** = Systemtabelle, BCP 9.0 (Lightweight).<br /><br /> **128** = dynamisches BCP (Bit).<br /><br /> **131** = dynamisches systemeigenes BCP.<br /><br /> **132** = dynamisches BCP im Zeichenmodus.<br /><br /> **208** = dynamische Systemtabelle, systemeigenes BCP 9.0.<br /><br /> **209** = dynamische Systemtabelle, BCP 9.0 im Zeichenmodus.<br /><br /> **210** = dynamische Systemtabelle, systemeigenes BCP 9.0 (nur global).<br /><br /> **211** = dynamische Systemtabelle, BCP 9.0 im (Zeichenmodus nur global).<br /><br /> **212** = dynamische Systemtabelle, systemeigenes BCP 9.0 (Lightweight).<br /><br /> **213** = dynamische Systemtabelle, BCP 9.0 (Lightweight).<br /><br /> **300** = Aktionen (Data Definition Language, Datendefinitionssprache).<br /><br /> **1024** = inkrementelle momentaufnahmesteuerung.<br /><br /> **1049** = inkrementeller momentaufnahmeordner.<br /><br /> **1074** = inkrementeller Momentaufnahme-headeranfang.<br /><br /> **1075** = inkrementelles Momentaufnahme-headerende.<br /><br /> **1076** = inkrementeller momentaufnahmeachspann.<br /><br /> **1077** = inkrementelles FTP-Adresse.<br /><br /> **1078** = inkrementelle FTP-Port.<br /><br /> **1079** = inkrementelles FTP-Unterverzeichnis.<br /><br /> **1080** = inkrementelle komprimierte Momentaufnahme.<br /><br /> **1081** = inkrementelle FTP-Anmeldung.<br /><br /> **1082** = inkrementelles FTP-Kennwort.|  
|**Schematext**|**Datentyp nvarchar(2000)**|Der Name der Skriptdatei oder eines Befehls, der einen Dateinamen einschließt.|  
|**Schemastatus**|**tinyint**|Gibt ab, ob eine Schemaänderung für den Artikel aussteht, die einen der folgenden Werte haben kann:<br /><br /> **0** = inaktiv.<br /><br /> **1** = aktiv.<br /><br /> Wenn eine schemaänderung aussteht, wird dieser Wert festgelegt, um **1**.|  
|**schemasubtype**|**int**|Der Untertyp der Schemaänderung:<br /><br /> **1** = ADDCOLUMN<br /><br /> **2** = DROPCOLUMN<br /><br /> **3** = ALTERCOLUMN<br /><br /> **4** = ADDPRIMARYKEY<br /><br /> **5** ADDUNIQUE =<br /><br /> **6** = VERWEIS HINZUFÜGEN<br /><br /> **7** = DROPCONSTRAINT<br /><br /> **8** = ADDDEFAULT<br /><br /> **9** = ADDCHECK<br /><br /> **10** = DISABLETRIGGER<br /><br /> **11** = ENABLETRIGGER<br /><br /> **12** = DISABLETRIGGER<br /><br /> **13** = ENABLETRIGGER<br /><br /> **14** = ENABLECONSTRAINT<br /><br /> **15** = DISABLECONSTRAINT<br /><br /> **16** = ENABLECONSTRAINT<br /><br /> **17** = DISABLECONSTRAINT|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
