---
title: "XML-Sicherheitsüberlegungen | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
caps.latest.revision: "3"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a4e534adf05fdae559c49d978d21c20bae988950
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="xml-security-considerations"></a>XML-Sicherheitsüberlegungen
Speichern von ADO und Open-Methoden für das Recordset-Objekt gelten nicht sichere Operationen in Internet Explorer auszuführen. Wenn diese Methoden in einem Skript verwendet werden, die ausgeführt wird, in einer Anwendung bzw. eines Steuerelements, das in einem Browser gehostet wird, wird die Sicherheitskonfiguration des Browsers daher Auswirkungen auf das Verhalten haben.  
  
 Sicherheitseinschränkungen für solche Vorgänge werden von Internet Explorer 5 standardmäßig in der Internetzone bereitgestellt. Mit dieser Konfiguration kann nicht das Recordset stellen keinen Zugriff auf das lokale Dateisystem auf dem Client oder Zugriff auf Datenquellen außerhalb der Domäne des Servers, von dem die Seite heruntergeladen wurde. Insbesondere kann bei der Ausführung auf dem Browserhost ein Recordset zurück in eine Datei gespeichert werden nur dann, wenn es auf dem gleichen Server wird von dem die Seite heruntergeladen wurde. Auf ähnliche Weise können Sie ein Recordset öffnen, indem Sie aus einer Datei zu laden, nur dann, wenn die Datei auf dem gleichen Server wird von dem die Seite heruntergeladen wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)
