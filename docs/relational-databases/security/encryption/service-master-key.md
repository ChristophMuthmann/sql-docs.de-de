---
title: Diensthauptschlüssel | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- service master key [SQL Server]
- service master key [SQL Server], about service master key
ms.assetid: 85f2095d-2590-4f59-8a29-7e100edd02bb
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8482c51541a4ffdc2475b6871f150f560581b179
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="service-master-key"></a>Diensthauptschlüssel
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Diensthauptschlüssel ist der Stamm der Verschlüsselungshierarchie von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Er wird automatisch dann generiert, wenn er erstmals zum Verschlüsseln eines anderen Schlüssels benötigt wird. Standardmäßig wird der Diensthauptschlüssel mit der Windows-Datenschutz-API und dem Schlüssel für den lokalen Computer verschlüsselt. Der Diensthauptschlüssel kann nur durch das Windows-Dienstkonto geöffnet werden, unter dem er erstellt wurde, oder durch einen Prinzipal mit Zugriff auf den Namen des Dienstkontos und sein Kennwort.  
  
 Das erneute Generieren oder Wiederherstellen des Diensthauptschlüssels umfasst das Entschlüsseln und erneute Verschlüsseln der gesamten Verschlüsselungshierarchie. Wenn der Schlüssel nicht beschädigt wurde, sollte dieser ressourcenintensive Vorgang für einen Zeitraum mit geringem Bedarf geplant werden.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] SQL Server 2016 schützt den Diensthauptschlüssel (Service Master Key, SMK) und den Datenbank-Hauptschlüssel (Database Master Key, DMK) mithilfe des AES-Verschlüsselungsalgorithmus. AES ist ein neuerer Verschlüsselungsalgorithmus als der in früheren Versionen verwendete 3DES-Algorithmus. Nach dem Aktualisieren einer Instanz von [!INCLUDE[ssDE](../../../includes/ssde-md.md)] auf [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] sollten SMK und DMK erneut generiert werden, um die Hauptschlüssel auf AES zu aktualisieren. Weitere Informationen zum Neugenerieren des SMK finden Sie unter [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-service-master-key-transact-sql.md) und [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-master-key-transact-sql.md).  
  
## <a name="best-practice"></a>Bewährte Methoden  
 Sichern Sie den Diensthauptschlüssel, und lagern Sie die Sicherungskopie an einem separaten, sicheren Ort.  
  
## <a name="related-tasks"></a>Related Tasks  
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-service-master-key-transact-sql.md)  
  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-service-master-key-transact-sql.md)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-service-master-key-transact-sql.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verschlüsselungshierarchie](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
