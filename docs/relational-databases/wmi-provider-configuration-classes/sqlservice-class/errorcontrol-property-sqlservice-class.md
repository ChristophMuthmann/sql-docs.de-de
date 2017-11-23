---
title: ErrorControl-Eigenschaft (SqlService-Klasse) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ErrorControl Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58f1064b96d21a6361d122fc5c92f945bea46dce
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl-Eigenschaft (SqlService-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Ruft ab oder legt den Schweregrad des Fehlers, wenn der Dienst beim Systemstart nicht gestartet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [SqlService-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) , das den Dienst darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein Zeichenfolgenwert der den gemeldeten Schweregrad des Fehlers angibt, wenn der beim Hochfahren des Diensts ein Fehler auftritt. In der folgenden Tabelle sind die möglichen Werte aufgeführt.  
  
 Ignorieren  
 Der Benutzer wird nicht benachrichtigt.  
  
 Normal  
 Der Benutzer wird benachrichtigt.  
  
 Schwer  
 Das System wird mit der letzten bekannten, fehlerfreien Konfiguration neu gestartet.  
  
 Kritisch  
 Das System versucht, mit einer fehlerfreien Konfiguration zu neu starten.  
  
 Unknown  
 Der Schweregrad ist unbekannt.  
  
## <a name="remarks"></a>Hinweise  
 Der Wert gibt die vom Startprogramm ausgeführte Aktion an, wenn ein Fehler auftritt. Alle Fehler werden vom Computersystem protokolliert.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten und Beenden von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
