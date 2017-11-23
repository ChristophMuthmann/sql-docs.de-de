---
title: SetServiceAccount-Methode (SqlService-Klasse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SetServiceAccount Method (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c0cec37d97f91da803a7d071aabfdd664878862f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="setserviceaccount-method-sqlservice-class"></a>SetServiceAccount-Methode (SqlService-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Versucht, ändern den Benutzernamen und das Kennwort, das die Dienstinstanz unter ausgeführt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [SqlService-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) , das den Dienst darstellt.  
  
#### <a name="parameters"></a>Parameter  
 *ServiceStartName*  
 Ein Zeichenfolgenwert, der den Kontonamen angibt, unter dem der Dienst ausgeführt wird. Abhängig vom Diensttyp könnte der Kontoname die Form "DomainName\Username" aufweisen. Wenn er ausgeführt wird, wird der Dienstprozess in einer von zwei Formen protokolliert:  
  
-   Wenn das Konto zur integrierten Domäne gehört, kann "\Username" angegeben werden.  
  
-   Wenn NULL angegeben wird, wird der Dienst als **LocalSystem** -Konto angemeldet.  
  
 Bei Kernel- oder Systemtreibern enthält *StartName* den Treiberobjektnamen, entweder "\FileSystem\Rdr" oder "\Driver\Xns", den das E/A-System zum Laden des Gerätetreibers verwendet. Bei Angabe von NULL wird der Treiber mit einem Standardobjektnamen ausgeführt, den das E/A-System auf Basis des Dienstnamens erstellt, zum Beispiel "DWDOM\Admin".  
  
 *ServiceStartPassword*  
 Ein Zeichenfolgenwert, der das Kennwort für den Kontonamen im *StartName* -Parameter angibt. Geben Sie NULL an, wenn Sie das Kennwort nicht ändern. Geben Sie eine leere Zeichenfolge an, wenn der Dienst kein Kennwort besitzt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein **uint32** -Wert, der 0 beträgt, wenn der Dienst erfolgreich geändert wurde. Der Wert beträgt 1, wenn die Anforderung nicht unterstützt wird. Jede andere Zahl gibt einen Fehler an.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Starten und Beenden von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
