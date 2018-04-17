---
title: Sys. fulltext_languages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fulltext_languages
- sys.fulltext_languages_TSQL
- fulltext_languages
- fulltext_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- languages [full-text search]
- sys.fulltext_languages catalog view
ms.assetid: 2ed6b53d-1cf2-4763-9d58-36ea24a610ef
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 812217f478e8574aac2d2066df6ab87d9b117a0c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysfulltextlanguages-transact-sql"></a>sys.fulltext_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Diese Katalogsicht enthält eine Zeile pro Sprache, deren Wörtertrennungen bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registriert werden. Jede Zeile zeigt die LCID und den Namen der Sprache an. Wenn Wörtertrennungen für eine Sprache registriert werden, werden ihre übrigen sprachlichen Ressourcen – Wortstammerkennung, Füllwörter (Stoppwörter) und Thesaurusdateien – für Volltextindizierungs- oder Volltextabfragevorgänge verfügbar. Der Wert der **Namen** oder **Lcid** kann angegeben werden, in der Volltextabfragen und der Volltextindex [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen.  
   
|Column|Datentyp|Description|  
|------------|---------------|-----------------|  
|**lcid**|**int**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Gebietsschemabezeichner (Locale Identifier, LCID) für die Sprache.|  
|**name**|**sysname**|Der Wert des Alias in [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) entsprechend dem Wert der **Lcid** oder die Zeichenfolgendarstellung des numerischen LCID-WERTS.|  
  
## <a name="values-returned-for-default-languages"></a>Werte, die für Standardsprachen zurückgegeben wurden  
 In der folgenden Tabelle sind Werte für die Sprachen aufgeführt, deren Wörtertrennungen standardmäßig registriert werden.  
  
|Sprache|LCID|  
|--------------|----------|  
|Arabisch|1025|  
|Bangla (Indien)|1093|  
|Englisch (britisch)|2057|  
|Bulgarisch|1026|  
|Katalanisch|1027|  
|Chinesisch (Hongkong SAR, VR China)|3076|  
|Chinesisch (Macao SAR)|5124|  
|Chinesisch (Singapur)|4100|  
|Kroatisch|1050|  
|Tschechisch|1029|  
|Dänisch|1030|  
|Niederländisch|1043|  
|Englisch|1033|  
|Französisch|1036|  
|Deutsch|1031|  
|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Griechisch|1032|  
|Gujarati|1095|  
|Hebräisch|1037|  
|Hindi|1081|  
|Isländisch|1039|  
|Indonesisch|1057|  
|Italienisch|1040|  
|Japanisch|1041|  
|Kannada|1099|  
|Koreanisch|1042|  
|Lettisch|1062|  
|Litauisch|1063|  
|Malaiisch (Malaysia)|1086|  
|Malayalam|1100|  
|Marathi|1102|  
|Neutral|0|  
|Norwegisch (Bokmål)|1044|  
|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Polnisch|1045|  
|Portugiesisch (Brasilien)|1046|  
|Portugiesisch (Portugal)|2070|  
|Punjabi|1094|  
|Rumänisch|1048|  
|Russisch|1049|  
|Serbisch (Kyrillisch)|3098|  
|Serbisch (Lateinisch)|2074|  
|Chinesisch (vereinfacht)|2052|  
|Slowakisch|1051|  
|Slowenisch|1060|  
|Spanisch|3082|  
|Schwedisch|1053|  
|Tamil|1097|  
|Telugu|1098|  
|Thai|1054|  
|Chinesisch (traditionell)|1028|  
|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Türkisch|1055|  
|Ukrainisch|1058|  
|Urdu|1056|  
|Vietnamesisch|1066|  
  
## <a name="remarks"></a>Hinweise  
 Um die Liste der mit der Volltextsuche registrierte Sprachenliste zu aktualisieren, verwenden [Sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)"**Update_languages**".  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
