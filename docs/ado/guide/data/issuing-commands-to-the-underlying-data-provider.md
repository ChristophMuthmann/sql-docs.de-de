---
title: Ausgeben von Befehlen an den zugrunde liegenden Datenanbieter | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 394e317bc3f91809a36451a1458d1c33a08128cf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Ausgeben von Befehlen an den zugrunde liegenden Datenanbieter
Solche Befehle, die nicht mit der Form beginnt wird an den Datenanbieter übergeben. Dies ist gleichbedeutend mit dem ein Shape-Befehl in der Form "Form" {Anbieterbefehl}". Diese Befehle führen *nicht* erzeugen eine **Recordset**. Ist z. B. "Form" {DROP TABLE MyTable} "einen Befehl uneingeschränkt Form vorausgesetzt, dass der Datenanbieter DROP TABLE unterstützt.  
  
 Dies ermöglicht die normalen Anbieterbefehlen und Form Befehle aus, um die Verbindung und die Transaktion freigeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Daten strukturiert werden, Beispiel](../../../ado/guide/data/data-shaping-example.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)
