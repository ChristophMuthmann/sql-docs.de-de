---
title: Benutzerdefinierte Attribute für CLR-Routinen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
caps.latest.revision: 82
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f21dd7eff0767eb38da21720585e01fe9bb7b1d0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR-Integration, benutzerdefinierte Attribute für CLR-Routinen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die aufgeführten Attribute können angewendet werden, common Language Runtime (CLR)-Routinen, benutzerdefinierte Typen und benutzerdefinierte Aggregate, die in registriert sind [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Wenn das Attribut nicht angewendet wird, nimmt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] den Standardwert an. Die aufgeführten Attribute sind definiert, der **Microsoft.SqlServer.Server** Namespace.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Das 'SqlUserDefinedAggregate'-Attribut  
 Die **SqlUserDefinedAggregate** Attribut gibt an, dass die Methode als benutzerdefiniertes Aggregat registriert werden soll. Jedem benutzerdefinierten Aggregat muss dieses Attribut angefügt werden.  
  
 Weitere Informationen finden Sie unter [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Das 'SqlFunction'-Attribut  
 Die **SqlFunction** Attribut gibt an, die Methode als eine Funktion mit den entsprechend festgelegten Funktionsattributen registriert werden soll.  
  
 Weitere Informationen finden Sie unter ["SqlFunctionAttribute"](http://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Das 'SqlFacet'-Attribut  
 Die **' sqlfacet '** Attribut wird verwendet, um Informationen über den Rückgabetyp eines Ausdrucks den benutzerdefinierten Typ (UDT) zurückgegeben.  
  
 Weitere Informationen finden Sie unter [SqlFacetAttribute](http://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Das 'SqlProcedure'-Attribut  
 Die **SqlProcedure** Attribut gibt an, die Methode als gespeicherte Prozedur registriert werden soll. Dieses Attribut wird nur von Visual Studio verwendet, um die angegebene Methode automatisch als gespeicherte Prozedur zu registrieren. Sie wird nicht von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet.  
  
 Weitere Informationen finden Sie unter [SqlProcedureAttribute](http://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Das 'SqlTrigger'-Attribut  
 Die **SqlTrigger** Attribut gibt an, die Methode als Trigger registriert werden soll.  
  
 Weitere Informationen finden Sie unter [SqlTriggerContext](http://go.microsoft.com/fwlink/?LinkId=128022) und [SqlTriggerAttribute](http://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Das 'SqlUserDefinedTypeAttribute'-Attribut  
 Sie können das SqlUserDefinedTypeAttribute-Attribut in eine Klassendefinition in der Assembly übernehmen. Es bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] einen benutzerdefinierten Typ erstellt, der an die Klassendefinition mit diesem benutzerdefinierten Attribut gebunden ist.  
  
 Weitere Informationen finden Sie unter [SqlUserDefinedTypeAttribute](http://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Das 'SqlMethod'-Attribut  
 Die **SqlMethod** Attribut wird verwendet, um die Determinismus und Data Access-Eigenschaften einer Methode oder Eigenschaft in einen UDT anzugeben.  
  
 Weitere Informationen finden Sie unter [SqlMethodAttribute](http://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Siehe auch  
 [CLR User-Defined Aggregate](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Benutzerdefinierte CLR-Funktionen](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Benutzerdefinierte CLR-Typen](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR-gespeicherte Prozeduren](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [CLR-Trigger](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
