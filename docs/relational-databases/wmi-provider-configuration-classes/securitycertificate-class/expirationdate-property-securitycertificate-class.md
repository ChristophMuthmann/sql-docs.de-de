---
title: ExpirationDate-Eigenschaft (SecurityCertificate-Klasse) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ExpirationDate Property (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExpirationDate property
ms.assetid: b7fbb9e9-85c1-475b-8e49-7c82fb3740aa
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fba3e58ec05633ebff63b3153c707a860346e88a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="expirationdate-property-securitycertificate-class"></a>ExpirationDate-Eigenschaft (SecurityCertificate-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft das Datum ab, an dem die Gültigkeit des Sicherheitszertifikats endet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.ExpirationDate [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [SecurityCertificate-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) , das ein Sicherheitszertifikat darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein **uint32** -Wert, der das Ablaufdatum für das Sicherheitszertifikat angibt.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Servernetzwerkprotokollen und Netzwerkbibliotheken](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
