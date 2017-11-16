---
title: "Verwalten von Änderungen an Datenquellensichten und Datenquellen | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data sources
- modifying data source views
- data source views [Analysis Services], schema updates
- data sources [Analysis Services], schema updates
ms.assetid: 928c9f63-365a-43fd-9bbd-78828cc7e54d
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3b1913d392467f4ba78976d9ab73919e7ac06051
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>Verwalten von Änderungen an Datenquellensichten und Datenquellen
  Wird der Schemagenerierungs-Assistent erneut ausgeführt, verwendet er dieselbe Datenquelle und Datenquellensicht wie für die ursprüngliche Generierung. Wenn Sie eine Datenquelle oder Datenquellensicht hinzufügen, wird diese vom Assistenten nicht verwendet. Wenn Sie die ursprüngliche Datenquelle oder Datenquellensicht nach der Anfangsgenerierung löschen, müssen Sie den Assistenten von Anfang an ausführen. Alle bisherigen Einstellungen im Assistenten werden ebenfalls gelöscht. Alle vorhandenen Objekte in einer zugrunde liegenden Datenbank, die mit einer gelöschten Datenquelle oder Datenquellensicht verbunden waren, werden bei dem nächsten Ausführen des Schemagenerierungs-Assistenten als vom Benutzer erstellte Objekte behandelt.  
  
 Gibt die Datenquellensicht nicht den tatsächlichen Status der zugrunde liegenden Datenbank zum Zeitpunkt der Generierung wieder, ist es möglich, dass bei der Generierung des Schemas für die Themenbereichsdatenbank durch den Schemagenerierungs-Assistenten Fehler auftreten. Wenn die Datenquellensicht beispielsweise angibt, dass der Datentyp einer Spalte **int**ist, der Datentyp der Spalte tatsächlich aber auf **string**festgelegt wurde, legt der Schemagenerierungs-Assistent den Datentyp für den Fremdschlüssel in Übereinstimmung mit der Datenquellensicht auf **INT** fest und erzeugt dann beim Erstellen der Beziehung einen Fehler, da der tatsächliche Datentyp **string**ist.  
  
 Wenn Sie allerdings die Datenquellen-Verbindungszeichenfolge auf eine andere Datenbank aus der vorherigen Generierung ändern, wird kein Fehler generiert. Es wird die neue Datenbank verwendet und keine Änderung an der vorherigen Datenbank vorgenommen.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zur inkrementellen Generierung](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)  
  
  

