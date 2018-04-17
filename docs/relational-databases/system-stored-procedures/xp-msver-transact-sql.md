---
title: Xp_msver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_msver_TSQL
- xp_msver
dev_langs:
- TSQL
helpviewer_keywords:
- xp_msver
ms.assetid: 9264cf8c-92ba-45ad-b2d6-15d26d805a16
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 24f21887156b2c9fef1811ef5268887efd59bfe5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="xpmsver-transact-sql"></a>xp_msver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Versionsinformationen zu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Xp_msver** gibt auch Informationen zur Buildnummer des Servers und Informationen zur serverumgebung zurück. Die Informationen, die **Xp_msver** gibt können verwendet werden, in [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, Batches, gespeicherten Prozeduren und So weiter, um Logik für plattformunabhängigen Code zu verbessern.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
xp_msver [ optname ]  
```  
  
## <a name="arguments"></a>Argumente  
 *optname*  
 Der Name einer Option. Die folgenden Werte sind möglich.  
  
|Options-/Spaltenname|Description|  
|-------------------------|-----------------|  
|**ProductName**|Produktname; beispielsweise [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ProductVersion**|Die Produktversion.|  
|**Sprache**|Die Sprachversion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Platform**|Der Name des Betriebssystems, des Herstellers und der Chipfamilie für den Computer, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.|  
|**Kommentare**|Verschiedene Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Firmenname**|Der Name der Firma, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellt. Beispiel: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation.|  
|**FileDescription**|Das Betriebssystem.|  
|**FileVersion**|Version der ausführbaren Datei von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**InternalName**|Von [!INCLUDE[msCoName](../../includes/msconame-md.md)] verwendeter interner Name für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Beispiel: SQLSERVR.|  
|**LegalCopyright**|Urheberrechtliche Informationen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Beispiel: Copyright© [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corp. 1988-2005.|  
|**LegalTrademarks**|Markeninformationen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[msCoName](../../includes/msconame-md.md)] ist z. B. eine eingetragene Marke der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation.|  
|**Originaldateiname**|Der Name der Datei, die beim Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Beispiel: Sqlservr.exe.|  
|**PrivateBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**SpecialBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**"WindowsVersion"**|Version von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, die auf dem Computer installiert ist, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.|  
|**ProcessorCount**|Die Anzahl der Prozessoren in dem Computer, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.|  
|**ProcessorActiveMask**|Gibt die Prozessoren in dem Computer an, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, die gestartet werden und von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows verwendet werden können.|  
|**ProcessorType**|Der Prozessortyp. Ähnlich wie **Plattform**.|  
|**PhysicalMemory**|Die Menge an Arbeitsspeicher (RAM) in Megabyte (MB), die auf dem Computer installiert ist, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.|  
|**Produkt-ID**|Product ID (PID). Wird bei der Installation angegeben. Diese Nummer finden Sie auf dem Aufkleber der Hülle der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Original-CD.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 1 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 **Xp_msver**, ohne Parameter gibt ein Resultset mit vier Spalten, die alle Optionswerte aufgelistet sind. **Xp_msver**, gibt Sie für die einzelnen Parameter das vierspaltige Resultset mit Werten für diese Option.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte allgemeine erweiterte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [@@VERSION &#40;Transact-SQL&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)  
  
  
