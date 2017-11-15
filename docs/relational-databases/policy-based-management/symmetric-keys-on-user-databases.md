---
title: "Symmetrische Schlüssel für Benutzerdatenbanken | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5ce3ca1c947a5393337ce75c4030182971c355d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="symmetric-keys-on-user-databases"></a>Symmetrische Schlüssel für Benutzerdatenbanken
  Diese Regel überprüft, ob Schlüssel mit einer Länge von weniger als 128 Bytes den RC2- oder RC4-Verschlüsselungsalgorithmus verwenden.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Verwenden Sie die AES-128-Bit-Verschlüsselung oder eine stärkere Verschlüsselung, um symmetrische Schlüssel für die Datenverschlüsselung zu erstellen. Wenn AES nicht vom Betriebssystem unterstützt wird, verwenden Sie 3DES.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
