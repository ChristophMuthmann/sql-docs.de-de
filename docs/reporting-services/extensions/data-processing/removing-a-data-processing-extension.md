---
title: Entfernen eine Datenverarbeitungserweiterung | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: f16194ee794cfeacd6ba7902a42be6f970eddf1a
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="removing-a-data-processing-extension"></a>Entfernen von Datenverarbeitungserweiterungen
  Um eine datenverarbeitungserweiterung zu entfernen, entfernen Sie einfach die **Erweiterung** -Element für die datenverarbeitungserweiterung aus der Konfigurationsdatei. Wenn Sie Einträge für einen Berichtsserver sowie die Berichts-Designer vorgenommen haben, entfernen Sie die **Erweiterung** Element aus RSReportServer.config und RSReportDesigner.config Dateien. Nachdem Sie die Konfigurationsdaten entfernt haben, steht Ihre Datenverarbeitungserweiterung nicht mehr für die Komponente zur Verfügung.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
