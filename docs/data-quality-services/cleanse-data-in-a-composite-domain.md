---
title: "Bereinigen von Daten in einer Verbunddomäne | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7d1076e0-7710-469a-9107-e293e4bd80ac
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b823b710ca928769db6ecc64b60abc714f41de5
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="cleanse-data-in-a-composite-domain"></a>Bereinigen von Daten in einer Verbunddomäne
  Dieses Thema enthält Informationen zur Bereinigung von Verbunddomänen in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Eine Verbunddomäne besteht aus einer oder mehreren Einzeldomänen und ist einem Datenfeld zugeordnet, das sich aus mehreren verwandten Begriffen zusammensetzt. Die einzelnen Domänen in einer Verbunddomäne müssen einen gemeinsamen Wissensbereich haben. Ausführliche Informationen zu Verbunddomänen finden Sie unter [Managing a Composite Domain](../data-quality-services/managing-a-composite-domain.md).  
  
##  <a name="Mapping"></a> Zuordnen einer Verbunddomäne zu den Quelldaten  
 Es gibt zwei Methoden, mit denen Sie die Quelldaten einer Verbunddomäne zuordnen können:  
  
-   Bei den Quelldaten handelt es sich um ein einzelnes Feld (beispielsweise „Vollständiger Name“), das einer Verbunddomäne zugeordnet wird.  
  
    -   Wenn die Verbunddomäne einem Verweisdatendienst zugeordnet wird, werden die Quelldaten zur Korrektur und Analyse unverändert an den Verweisdatendienst gesendet.  
  
    -   Wenn die Verbunddomäne keinem Verweisdatendienst zugeordnet wird, werden die Quelldaten basierend auf der für die Verbunddomäne definierten Methode analysiert. Weitere Informationen zum Angeben einer Analysemethode für Verbunddomänen finden Sie unter [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)  
  
-   Die Quelldaten bestehen aus mehreren Feldern (z. B. „Vorname“, „Weitere Vornamen“ und „Nachname“), die einzelnen Domänen innerhalb einer Verbunddomäne zugeordnet werden.  
  
 Ein Beispiel zum Zuordnen von Verbunddomänen zu Quelldaten finden Sie unter [Anfügen einer Domäne oder Verbunddomäne an Verweisdaten](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
##  <a name="CDCorrection"></a> Datenkorrektur mit definitiven domänenübergreifenden Regeln  
 Domänenübergreifende Regeln in Verbunddomänen ermöglichen es Ihnen, Regeln zu erstellen, die die Beziehung zwischen einzelnen Domänen in einer Verbunddomäne angeben. Domänenübergreifende Regeln werden berücksichtigt, wenn Sie die Bereinigungsaktivität für die Quelldaten von Verbunddomänen ausführen. Abgesehen davon, dass Sie erfahren, ob eine domänenübergreifenden Regel gültig ist, korrigiert die definitive domänenübergreifende *Then* -Regel **Wert ist gleich**auch die Daten während der Datenbereinigungsaktivität.  
  
 Beachten Sie das folgende Beispiel: Es gibt eine Verbunddomäne namens „Product“ mit drei einzelnen Domänen: ProductName, CompanyName und ProductVersion. Erstellen Sie die folgende definitive domänenübergreifende Regel:  
  
 IF Domain ‘CompanyName’ Value contains *Microsoft* and Domain ‘ProductName’ Value is equal to *Office* and ‘ProductVersion’ Value is equal to *2010* THEN Domain ‘ProductName’ Value is equal to *Microsoft Office 2010*.  
  
 Wenn diese domänenübergreifende Regel ausgeführt wird, werden die Quelldaten (ProductName) nach der Bereinigungsaktivität wie folgt korrigiert:  
  
 **Quelldaten**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Office|Microsoft Inc.|2010|  
  
 **Ausgabedaten**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Microsoft Office 2010|Microsoft Inc.|2010|  
  
 Wenn Sie die definitive domänenübergreifende *Then* -Regel **Wert ist gleich**testen, enthält das Dialogfeld **Verbunddomänenregel testen** eine neue Spalte namens **Korrigieren in**, in der die korrigierten Daten angezeigt werden. In einem Data Quality-Bereinigungsprojekt ändert diese definitive domänenübergreifende Regel die Daten mit 100%iger Vertraulichkeit, und die Spalte **Grund** zeigt die folgende Meldung an: Korrigiert von Regel ‚*\<Name der domänenübergreifenden Regel>*‘. Weitere Informationen zu domänenübergreifenden Regeln finden Sie unter [Create a Cross-Domain Rule](../data-quality-services/create-a-cross-domain-rule.md).  
  
> [!NOTE]  
>  Die definitive domänenübergreifende Regel funktioniert nicht für Verbunddomänen, die an einen Verweisdatendienst angefügt wurden.  
  
##  <a name="DataProfiling"></a> Datenprofilerstellung für Verbunddomänen  
 Die Profilerstellung in DQS bietet während der Bereinigungsaktivität zwei Data Quality-Dimensionen: *Vollständigkeit* (das Ausmaß des Vorhandenseins von Daten) und *Genauigkeit* (das Ausmaß, in dem Daten für den beabsichtigten Zweck verwendet werden können). Die Profilerstellung kann keine zuverlässigen Vollständigkeitsstatistiken für Verbunddomänen bereitstellen. Wenn Sie Vollständigkeitsstatistiken benötigen, verwenden Sie Einzeldomänen anstatt Verbunddomänen. Wenn Sie Verbunddomänen verwenden möchten, sollten Sie eine Wissensdatenbank mit Einzeldomänen für die Profilerstellung erstellen, um die Vollständigkeit zu bestimmen, und eine weitere Domäne mit einer Verbunddomäne für die Bereinigungsaktivität erstellen. Die Profilerstellung kann z. B. 95 % Vollständigkeit für Adressendatensätze anzeigen, die eine Verbunddomäne verwenden, aber es kann einen viel höheren Grad der Unvollständigkeit für eine der Spalten geben, z. B. für eine Postleitzahlspalte. In diesem Beispiel möchten Sie die Vollständigkeit der Postleitzahlspalte mit einer Einzeldomäne messen.  
  
 Die Profilerstellung stellt wahrscheinlich zuverlässige Genauigkeitsstatistiken für Verbunddomänen bereit, da Sie die Genauigkeit für mehrere Spalten gemeinsam messen können. Der Wert dieser Daten liegt in der zusammengesetzten Aggregation, daher sollten Sie die Genauigkeit mit einer Verbunddomäne messen.  
  
 Ausführliche Informationen zur Datenprofilerstellung während der Bereinigungsaktivität finden Sie unter [Profiler-Statistik](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Profiler) in [Bereinigen von Daten mit &#40;internem&#41; DQS-Wissen](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
  
