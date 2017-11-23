---
title: Arbeiten mit Datenbankobjekten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9b2565474a777bbaddc6b659227a88bc1d2d609
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="creating-altering-and-removing-database-objects"></a>Erstellen, ändern und Löschen von Datenbankobjekten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Die Phasen der SMO-objekterstellung sind wie folgt aus:  
  
1.  Erstellen einer Instanz des Objekts  
  
2.  Festlegen der Objekteigenschaften  
  
3.  Erstellen von Instanzen der untergeordneten Objekte  
  
4.  Festlegen der Eigenschaften des untergeordneten Objekts  
  
5.  Erstellen des Objekts  
  
 Wenn Instanzen von SMO-Objekten in einer SMO-Anwendung erstellt werden, sind sie auf der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz erst vorhanden, wenn die **Create** -Methode ausgegeben wird. Allerdings ist es nicht notwendig, eine **Create** -Methode für jedes einzelne Objekt auszugeben. Wenn ein Objekt über einen Satz untergeordneter Objekte verfügt, muss nur das übergeordnete Objekt die **Create** -Methode ausführen. Zum Beispiel erfordert die Definition einer Tabelle, dass mindestens eine Spalte darin enthalten ist. Auch kann eine Spalte nicht ohne eine Tabelle erstellt werden. Es besteht eine Abhängigkeitsbeziehung zwischen der Tabelle und ihren Spalten.  
  
 Die <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A>-Methode ermöglicht es Ihnen, Änderungen an einem Objekt vorzunehmen. Mehrere Änderungen an einem Objekt, wie beispielsweise das Hinzufügen untergeordneter Objekte zu einer der Auflistungen des Objekts oder das Ändern eines Eigenschaftswerts, werden zu einem Batch zusammengefasst und in einem Durchgang ausgeführt. Die **Alter** -Methode reduziert den Netzwerkdatenverkehr und verbessert die Gesamtleistung.  
  
 Die **Drop** -Anweisung wird dazu verwendet, ein Objekt und alle seine abhängigen untergeordneten Objekte zu entfernen, die anfänglich zur Objekterstellung erforderlich waren.  
  
## <a name="see-also"></a>Siehe auch  
 [SMO-Objektmodell](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
