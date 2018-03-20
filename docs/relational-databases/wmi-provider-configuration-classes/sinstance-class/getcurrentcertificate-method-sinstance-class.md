---
title: GetCurrentCertificate-Methode (SInstance-Klasse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- GetCurrentCertificate Method (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 9d2b72df-cb21-414a-abef-917f13d4de62
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 950bbea868c04a0c7efc1e0ab1e842a51cb17c46
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="getcurrentcertificate-method-sinstance-class"></a>GetCurrentCertificate-Methode (SInstance-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft das aktuelle Sicherheitszertifikat ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.GetCurrentCertificate(SHA)  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [SInstance-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) , das die Servereinstellungen in einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]darstellt.  
  
#### <a name="parameters"></a>Parameter  
  
|Parameter|Description|  
|---------------|-----------------|  
|*SHA*|Ein Zeichenfolgen-Objektwert (Ausgabeparameter), das das aktuelle Sicherheitszertifikat nach Abschluss der Methode angibt.|  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein **uint32** -Wert, der 0 beträgt, wenn der Dienst erfolgreich geändert wurde. Der Wert beträgt 1, wenn die Anforderung nicht unterstützt wird; jede andere Zahl gibt einen Fehler an.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Servernetzwerkprotokollen und Netzwerkbibliotheken](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
