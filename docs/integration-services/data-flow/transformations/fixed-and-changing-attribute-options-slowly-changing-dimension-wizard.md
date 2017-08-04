---
title: "Optionen für feste und veränderliche Attribute (Dimensions-Assistent für langsam veränderliche | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e248bb1fc4e5f4d638f1cbd417cc243c59bbd5d4
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>Optionen für feste und veränderliche Attribute (Assistent für langsam veränderliche Dimensionen)
  Geben Sie mithilfe des Dialogfelds **Optionen für feste und veränderliche Attribute** an, wie auf Änderungen bei festen und veränderlichen Attributen reagiert werden soll.  
  
 Weitere Informationen zu diesem Assistenten finden Sie unter [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>enthalten  
 **Feste Attribute**  
 Geben Sie für feste Attribute an, ob der Task fehlschlagen soll, wenn bei einem festen Attribut eine Änderung festgestellt wird.  
  
 **Veränderliche Attribute**  
 Geben Sie für veränderliche Attribute an, ob der Task zusätzlich zu aktuellen Datensätzen veraltete oder abgelaufene Datensätze ändern soll, wenn bei einem veränderlichen Attribut eine Änderung erkannt wird. Ein abgelaufener Datensatz ist ein Datensatz, der durch eine Änderung in einem Verlaufsattribut (eine Änderung vom Typ 2) durch einen neueren Datensatz ersetzt wurde. Das Auswählen dieser Option verursacht möglicherweise zusätzliche Verarbeitungsanforderungen für ein im relationalen Data Warehouse erstelltes mehrdimensionales Objekt.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration von Ausgaben mithilfe des Assistenten für langsam veränderliche](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
