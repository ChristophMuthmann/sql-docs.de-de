---
title: Aktivieren des DirectQuery-Modus in SSMS | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 86bae72aacde357b372e48f83a429e8102553325
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="enable-directquery-mode-in-ssms"></a>Aktivieren des DirectQuery-Modus in SSMS

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Sie können die Datenzugriffseigenschaften eines tabellarischen Modells ändern, das bereits bereitgestellt wurde, und den DirectQuery-Modus aktivieren, bei dem Abfragen auf eine relationale Datenquelle im Back-End anstatt auf im Arbeitsspeicher zwischengespeicherte Daten angewendet werden.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]unterscheiden sich die für die DirectQuery-Konfiguration erforderlichen Schritte je nach Kompatibilitätsgrad des Modells. Nachstehend finden Sie Schritte, die für alle Kompatibilitätsgrade funktionieren.  
  
 In diesem Thema wird davon ausgegangen, dass Sie erstellt und eine in-Memory-tabellarische Modelle auf Kompatibilitätsgrad 1200 oder höher und nur erforderlich überprüft, die DirectQuery-Zugriff aktivieren und Verbindungszeichenfolgen aktualisieren. Wenn Sie mit einem niedrigeren Kompatibilitätsgrad beginnen, müssen Sie ihn zunächst manuell upgraden. Eine Anleitung finden Sie unter [Upgraden von Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) .  
  
> [!IMPORTANT]  
>  Wir empfehlen die Verwendung von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] anstelle von Management Studio zum Ändern des Datenspeichermodus. Wenn Sie  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] zum Ändern des Modells verwenden und anschließend mit der Bereitstellung auf dem Server fortfahren, bleiben Modell und Datenbank synchronisiert. Darüber hinaus können Sie bei einer Änderung des Speichermodus im Modell überprüfen, ob Validierungsfehler auftreten. Wenn [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] wie in diesem Artikel beschrieben verwendet wird, werden Validierungsfehler nicht gemeldet.  
  
## <a name="requirements"></a>Anforderungen  
 Es sind mehrere Schritte nötig, um den DirectQuery-Modus auf ein tabellarisches Modell anwenden zu können:  
  
-   Stellen Sie sicher, dass das Modell keine Features aufweist, die im DirectQuery-Modus Validierungsfehler verursachen, und ändern Sie dann den Datenspeichermodus des Modells von „InMemory“ in „DirectQuery“.  
  
     Eine Liste der Funktionseinschränkungen finden Sie unter [DirectQuery-Modus &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).  
  
-   Überprüfen Sie die Verbindungszeichenfolge und die Anmeldeinformationen, die von der bereitgestellten Datenbank verwendet werden, um Daten aus der externen Datenbank im Back-End abzurufen. Stellen Sie sicher, dass es nur eine Verbindung gibt, und dass die Einstellungen für die Ausführung von Abfragen geeignet sind.  
  
     Tabellarische Datenbanken, die speziell für DirectQuery entworfen wurden, haben möglicherweise mehrere Verbindungen, die jetzt für den DirectQuery-Modus entsprechend auf eine reduziert werden müssen.  
  
     Anmeldeinformationen, die ursprünglich für die Verarbeitung von Daten verwendet wurden, dienen nun zum Abfragen von Daten. Im Rahmen der DirectQuery-Konfiguration müssen Sie das Konto überprüfen und möglicherweise ändern, wenn Sie für bestimmte Vorgänge verschiedene Konten verwenden.  
  
     Der DirectQuery-Modus ist das einzige Szenario, in dem Analysis Services die vertrauenswürdige Delegierung durchführt. Wenn Ihre Lösung die Delegierung zum Abrufen benutzerspezifischer Ergebnisse benötigt, muss das Konto, mit dem eine Verbindung mit der Back-End-Datenbank hergestellt wird, die Identität des Benutzers delegieren können, der die Anforderung stellt. Außerdem benötigen Benutzeridentitäten die Leseberechtigung für die Back-End-Datenbank.  
  
-   Bestätigen Sie im letzten Schritt , dass der DirectQuery-Modus betriebsbereit ist, indem Sie eine Abfrage ausführen.  
  
## <a name="step-1-check-the-compatibility-level"></a>Schritt 1: Überprüfen des Kompatibilitätsgrads  
 Eigenschaften, die den Datenzugriff definieren, sind je nach Kompatibilitätsgrad unterschiedlich. Ein einleitender Schritt ist das Überprüfen des Kompatibilitätsgrads der Datenbank.  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] eine Verbindung mit der Instanz mit dem tabellarischen Modell her.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Datenbank > **Eigenschaften** > **Kompatibilitätsgrad**.  
  
     Der Wert ist entweder **SQL Server 2016 (1200)** oder ein früherer Grad wie **SQL Server 2012 SP1 oder höher (1103)**. Befolgen Sie im nächsten Schritt die Anweisungen für den jeweiligen Kompatibilitätsgrad.  
  
 Wenn Sie ein tabellarisches Modell in den DirectQuery-Modus ändern, wird der neue Datenspeichermodus sofort wirksam.  
  
## <a name="step-2a-switch-a-tabular-1200-database-to-directquery-mode"></a>Schritt 2a: Ändern einer tabellarischen Datenbank mit Kompatibilitätsgrad 1200 in den DirectQuery-Modus  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Datenbank > **Eigenschaften** > **Modell** > **Standardmodus**.  
  
2.  Legen Sie den Modus auf **DirectQuery**fest.  
  
    |||  
    |-|-|  
    |**Gültige Werte**|**Description**|  
    |**DirectQuery**|Abfragen werden auf eine relationale Back-End-Datenbank angewendet, wofür die für das Modell definierte Datenquellenverbindung verwendet wird.<br /><br /> Abfragen des Modells werden in native Datenbankabfragen konvertiert und an die Datenquelle umgeleitet.<br /><br /> Bei der Verarbeitung eines Modells im DirectQuery-Modus werden nur Metadaten kompiliert und bereitgestellt. Die Daten selbst befinden sich außerhalb des Modells in den Datenbankdateien der betriebsbereiten Datenquelle.|  
    |**Importieren**|Abfragen werden auf die tabellarische Datenbank in MDX oder DAX angewendet.<br /><br /> Wenn Sie ein Modell im Importmodus verarbeiten, werden Daten aus einer Back-End-Datenquelle abgerufen und auf dem Datenträger gespeichert. Beim Laden der Datenbank werden die Daten vollständig in den Arbeitsspeicher geladen, um sehr schnelle Tabellenscans und Abfragen zu ermöglichen.<br /><br /> Dies ist der Standardmodus für tabellarische Modelle und der einzige Modus für bestimmte (nicht relationale) Datenquellen.|  
  
## <a name="step-2b-switch-a-tabular-1100-1103-database-to-directquery-mode"></a>Schritt 2b: Ändern einer tabellarischen Datenbank mit Kompatibilitätsgrad 1100-1103 in den DirectQuery-Modus  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Datenbank > **Eigenschaften** > **Datenbank** > **DirectQueryMode**.  
  
2.  Legen Sie den Modus auf **DirectQuery** fest.  
  
     Es folgen die Standardeigenschaften des Modus:  
  
    |||  
    |-|-|  
    |**Gültige Werte**|**Description**|  
    |**InMemory**|Abfragen verwenden nur die im Arbeitsspeicher zwischengespeicherten Daten.|  
    |**InMemoryWithDirectQuery**|Für Abfragen wird standardmäßig der Cache verwendet, sofern in der Verbindungszeichenfolge vom Client nichts Gegenteiliges angegeben wurde.<br /><br /> Dies ist ein Hybridmodus, bei dem Partitionen einzeln für die Verwendung von „InMemory“ oder „DirectQuery“ konfiguriert werden.|  
    |**DirectQuery**|Für Abfragen wird nur die relationale Datenquelle verwendet.|  
    |**DirectQuerywithInMemory**|Bei Abfragen wird standardmäßig die relationale Datenquelle verwendet, sofern in der Verbindungszeichenfolge vom Client nichts Gegenteiliges angegeben wurde.<br /><br /> Dies ist ein Hybridmodus, bei dem Partitionen einzeln für die Verwendung von „InMemory“ oder „DirectQuery“ konfiguriert werden.|  
  
 **Hybrid-Datenspeicher**  
  
 Bei der Kombination des Zugriffs auf Arbeitsspeicher und Datenträger steht der Cache weiter zur Verfügung und kann für Abfragen genutzt werden. Ein Hybridmodus bietet Ihnen zahlreiche Optionen:  
  
-   Wenn sowohl der Cache als auch die relationale Datenquelle verfügbar sind, können Sie die bevorzugte Verbindungsmethode festlegen, doch letztlich wird die zu verwendende Quelle vom Client bestimmt. Dafür wird die DirectQueryMode-Eigenschaft der Verbindungszeichenfolge verwendet.  
  
-   Sie können Partitionen im Cache so konfigurieren, dass die primäre Partition, die für den DirectQuery-Modus verwendet wird, niemals verarbeitet wird und immer auf die relationale Quelle verweisen muss. Es gibt viele Möglichkeiten, mithilfe von Partitionen den Modellentwurf und die Berichtsfunktionen zu optimieren. Weitere Informationen finden Sie unter [Definieren von Partitionen im DirectQuery-Modellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md).  
  
-   Nach der Bereitstellung des Modells können Sie die bevorzugte Verbindungsmethode ändern. Sie können zum Beispiel einen Hybridmodus für Tests verwenden und den Modus **Nur DirectQuery** für das Modell erst nach gründlichen Tests von Berichten oder Abfragen, für die das Modell verwendet wird, festlegen. Weitere Informationen finden Sie unter [Festlegen oder Ändern der bevorzugten Verbindungsmethode für DirectQuery](http://msdn.microsoft.com/library/f10d5678-d678-4251-8cce-4e30cfe15751).  
  
## <a name="step-3-check-the-connection-properties-on-the-database"></a>Schritt 3: Überprüfen der Eigenschaften der Verbindung mit der Datenbank  
 Abhängig davon, wie die Datenquellenverbindung eingerichtet ist, kann sich beim Umschalten zu DirectQuery der Sicherheitskontext der Verbindung ändern. Überprüfen Sie beim Ändern des Datenzugriffsmodus die Identitätswechsel- und Verbindungszeichenfolgen-Eigenschaften, um festzustellen, ob die Anmeldung für fortlaufende Verbindungen mit der Back-End-Datenbank gültig ist.  
  
 Überprüfen Sie unter **Konfigurieren von Analysis Services für die eingeschränkte Kerberos-Delegierung** den Abschnitt [Konfigurieren von Analysis Services für die vertrauenswürdige Delegierung](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) auf Hintergrundinformationen zur Delegierung einer Benutzeridentität für DirectQuery-Szenarios.  
  
1.  Klappen Sie im Objekt-Explorer **Verbindungen** auf, und doppelklicken Sie auf eine Verbindung, um ihre Eigenschaften anzuzeigen.  
  
     Für DirectQuery-Modelle darf es nur eine für die Datenbank definierte Verbindung geben. Außerdem muss die Datenquelle relational sein und einen unterstützten Datenbanktyp haben. Eine Anleitung finden Sie unter [Unterstützte Datenquellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md).  
  
2.  Die**Verbindungszeichenfolge** muss den Server, Datenbanknamen und die Authentifizierungsmethode angeben, die für DirectQuery-Vorgänge verwendet werden. Wenn Sie die SQL Server-Authentifizierung verwenden, können Sie hier die Datenbankanmeldung angeben.  
  
3.  Die**Identitätswechselinformationen** werden für die Windows-Authentifizierung verwendet. Die folgenden Optionen sind für tabellarische Modelle im DirectQuery-Modus gültig:  
  
    -   **Dienstkonto verwenden**. Sie können diese Option wählen, wenn das Analysis Services-Dienstkonto über Leseberechtigungen für die relationale Datenbank verfügt.  
  
    -   **Bestimmten Benutzernamen und bestimmtes Kennwort verwenden**. Geben Sie ein Windows-Benutzerkonto an, das über Leseberechtigungen für die relationale Datenbank verfügt.  
  
 Diese Anmeldeinformationen werden nur zum Beantworten von Abfragen des relationalen Datenspeichers verwendet. Sie sind nicht mit den Anmeldeinformationen für die Verarbeitung des Caches eines Hybridmodells identisch.  
  
 Identitätswechsel kann nicht verwendet werden, wenn das Modell nur innerhalb des Arbeitsspeichers verwendet wird. Die Einstellung **ImpersonateCurrentUser**ist ungültig, sofern das Modell nicht den DirectQuery-Modus verwendet.  
  
## <a name="step-4-validate-directquery-access"></a>Schritt 4: Überprüfen des DirectQuery-Zugriffs  
  
1.  Starten Sie in Management Studio bei bestehender Verbindung mit der relationalen Datenbank in SQL Server eine Ablaufverfolgung mithilfe von SQL Server Profiler oder xEvents.  
  
     Wenn Sie mit Oracle oder Teradata arbeiten, verwenden Sie die Ablaufverfolgungstools dieser Systeme.  
  
2.  Führen Sie in Management Studio eine einfache MDX-Abfrage, wie z.B. `select <some measure> on 0 from model.`, aus.  
  
3.  Die Ablaufverfolgung sollte zeigen, dass die Abfrage auf die relationale Datenbank angewendet wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Unterstützte Datenquellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [Überwachen einer Instanz von Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  

