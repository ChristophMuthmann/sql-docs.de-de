---
title: Speichereigenschaften | Microsoft Docs
ms.custom: 
ms.date: 11/17/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- LowMemoryLimit property
- MinimumAllocatedMemory property
- MidMemoryPrice property
- MemoryHeapType property
- memory [Analysis Services]
- DefaultPagesCountToReuse property
- TotalMemoryLimit property
- SessionMemoryLimit property
- VirtualMemoryLimit property
- WaitCountIfHighMemory property
- HighMemoryPrice property
- HeapTypeForObjects property
ms.assetid: 085f5195-7b2c-411a-9813-0ff5c6066d13
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 8aa2f5f5c3e39680a9b0fe41e1b92443db4c8509
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="memory-properties"></a>Speichereigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reserviert einen geringen Anteil Speicher beim Start einrichten, damit Anforderungen sofort verarbeitet werden können. Zusätzlicher Arbeitsspeicher wird belegt, wenn die Arbeitsauslastung durch Abfragen und Verarbeitung steigt. 
  
  Sie können die Schwellenwerte steuern, an denen Arbeitsspeicher freigegeben wird, indem Sie Konfigurationseinstellungen angeben. Die **HardMemoryLimit** -Einstellung gibt z.B. eine selbstauferlegte Speicherobergrenze an (dieser Schwellenwert ist standardmäßig nicht aktiviert), wobei neue Anfragen vollständig abgelehnt werden, bis mehr Ressourcen verfügbar sind.
  
 **Gilt für:** Mehrdimensionaler und tabellarischer Servermodus, sofern nichts anderes angegeben ist.  
 
## <a name="default-memory-configuration"></a>Standard-Arbeitsspeicherkonfiguration

Bei der Standardkonfiguration belegt jede Analysis Services-Instanz vorab eine kleine Menge an RAM (40 bis 50 MB), auch wenn sich die Instanz im Leerlauf befindet. 

Denken Sie daran, dass Konfigurationseinstellungen pro Instanz gelten. Wenn Sie mehrere Instanzen von Analysis Services wie z.B. eine tabellarische und mehrdimensionale Instanz auf der gleichen Hardware ausführen, wird jede Instanz unabhängig von anderen Instanzen ihren eigenen Arbeitsspeicher belegen.

In der nachstehenden Tabelle werden die am häufigsten verwendeten Arbeitsspeichereinstellungen (mit ausführlicheren Informationen im Verweisabschnitt) kurz beschrieben. Dies sind die Einstellungen, die Sie konfigurieren sollten, wenn Analysis Services für den Speicher mit anderen Anwendungen auf dem gleichen Server im Wettbewerb steht:

Einstellung | Description
--------|------------
LowMemoryLimit | Ein unterer Schwellenwert für mehrdimensionale Instanzen, ab dem der Server zunächst damit beginnt, Arbeitsspeicher freizugeben, der von selten verwendeten Objekten belegt wird.
VertiPaqMemoryLimit | Ein unterer Schwellenwert für tabellarische Instanzen, ab dem der Server zunächst damit beginnt, Arbeitsspeicher freizugeben, der von selten verwendeten Objekten belegt wird.
TotalMemoryLimit | Ein oberer Schwellenwert, ab dem Analysis Services damit beginnt, Arbeitsspeicher aggressiver freizugeben, um Platz für Anfragen zu schaffen, die sich in der Ausführung befinden, sowie für neue Anfragen mit hoher Priorität. 
HardMemoryLimit | Ein weiterer Schwellenwert, ab dem Analysis Services damit beginnt, Anfragen aufgrund zu hoher Arbeitsspeicherauslastung vollständig abzulehnen. 
 
## <a name="property-reference"></a>Eigenschaftsreferenz

Die folgenden Eigenschaften gelten sowohl für tabellarische als auch für mehrdimensionale Modi, sofern nicht anders angegeben.

 Werte zwischen 1 und 100 stellen Prozentsätze von **Gesamter physischer Speicher** bzw. **Virtueller Adressraum**dar, je nachdem, welcher geringer ist. Werte über 100 stellen Arbeitsspeichergrenzwerte in Bytes dar.
  
 **LowMemoryLimit**  
 Eine 64-Bit-Gleitkommazahl mit doppelter Genauigkeit und Vorzeichen, die den ersten Schwellenwert definiert, ab dem Analysis Services damit beginnt, Arbeitsspeicher für Objekte mit geringer Priorität wie z.B. einen selten verwendeten Cache freizugeben. Sobald der Speicher belegt wird, gibt der Server keinen Arbeitsspeicher unter diesem Grenzwert frei. Der Standardwert ist 65. Dieser Wert besagt, dass der Grenzwert für ungenügenden Arbeitsspeicher 65 % des physischen Speichers bzw. virtuellen Adressraums entspricht, je nachdem, welcher dieser Werte niedriger ist.  
  
 **TotalMemoryLimit**  
 Definiert einen Schwellenwert, ab dem der Server Arbeitsspeicher freigibt, um Platz für andere Anfragen zu schaffen. Wenn dieser Grenzwert erreicht wird, beginnt die Instanz langsam, Arbeitsspeicher in Caches zu bereinigen, indem abgelaufene Sitzungen geschlossen und nicht verwendete Berechnungen entladen werden. Der Standardwert ist 80 % des physischen Speichers oder des virtuellen Adressraums, je nachdem, welcher dieser Werte niedriger ist. Beachten Sie, dass **TotalMemoryLimit** immer kleiner als **HardMemoryLimit**sein muss.  
  
 **HardMemoryLimit**  
 Gibt einen Arbeitsspeicherschwellenwert an, ab dem die Instanz aktive Benutzersitzungen aggressiv beendet, um die Speicherauslastung zu reduzieren. Alle beendeten Sitzungen empfangen eine Fehlermeldung, dass der Abbruch der Sitzung durch ungenügenden Arbeitsspeicher bedingt ist. Der Standardwert 0 bedeutet, dass **HardMemoryLimit** auf einen mittleren Wert zwischen **TotalMemoryLimit** und dem gesamten physischen Speicher des Systems festgelegt wird. Wenn der physische Speicher größer als der virtuelle Adressraum des Prozesses ist, dann wird anstelle der Berechnung von **HardMemoryLimit**der virtuelle Adressraum verwendet.  
  
 **VirtualMemoryLimit**  
  Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **VertiPaqPagingPolicy**  
  Gibt nur für tabellarische Instanzen das Auslagerungsverhalten an, das bei wenig verfügbarem Arbeitsspeicher des Servers angewendet wird. Gültige Werte sind:  
  
  

Einstellung  |Description  
---------|---------
**0**     |  Deaktiviert das Auslagern. Wenn der Arbeitsspeicher nicht ausreicht, schlägt die Verarbeitung mit dem Fehler "Nicht genügend Arbeitsspeicher" fehl. Wenn Sie die Auslagerung deaktivieren, müssen Sie für das Dienstkonto Windows-Berechtigungen erteilen. Anweisungen finden Sie unter [Konfigurieren von Dienstkonten &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md). 
**1**     |  (Standard) Diese Eigenschaft ermöglicht die Auslagerung auf Datenträger unter Verwendung der Auslagerungsdatei des Betriebssystems (pagefile.sys).   
  
Wenn sie auf 1 festgelegt ist, ist es weniger wahrscheinlich, dass bei der Verarbeitung aufgrund von Arbeitsspeicherbeschränkungen ein Fehler auftritt, da der Server versucht, Daten anhand der von Ihnen angegebenen Methode auf den Datenträger auszulagern. Das Festlegen der **VertiPaqPagingPolicy** -Eigenschaft ist keine Garantie dafür, dass niemals Arbeitsspeicherfehler auftreten. Unter folgenden Bedingungen können weiterhin Fehler aufgrund von unzureichendem Arbeitsspeicher auftreten:  
  
-   Es ist nicht genügend Arbeitsspeicher für alle Wörterbücher verfügbar. Die Wörterbücher werden während der Verarbeitung von Analysis Services für jede Spalte im Arbeitsspeicher gesperrt, und diese dürfen in der Gesamtheit den für **VertiPaqMemoryLimit**angegebenen Wert nicht überschreiten.  
  
-   Der virtuelle Adressraum reicht nicht aus, um den Prozess aufzunehmen.  
  
 Um wiederholte Fehler aufgrund von unzureichendem Arbeitsspeicher zu vermeiden, können Sie das Modell umgestalten, um die verarbeitete Datenmenge zu reduzieren, oder den physischen Arbeitsspeicher des Computers erweitern.  
  
 **VertiPaqMemoryLimit**  
 Nur für tabellarische Instanzen – Wenn die Auslagerung auf den Datenträger zulässig ist, gibt diese Eigenschaft die Arbeitsspeichernutzung (als Prozentsatz des gesamten Arbeitsspeichers) an, ab der die Auslagerung beginnt. Der Standardwert ist 60. Wenn die Arbeitsspeichernutzung weniger als 60 Prozent beträgt, führt der Server keine Auslagerung auf Datenträger aus. Diese Eigenschaft hängt von **VertiPaqPagingPolicyProperty**ab, die auf 1 festgelegt werden muss, damit Auslagerungen stattfinden.  
  
 **HighMemoryPrice**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryHeapType**  
  Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte. Gültige Werte in Analysis Services in SQL Server 2016 SP1 und höher sind wie folgt:
  
  Einstellung | Description
--------|------------
**-1** | (Standard) Automatisch. Das Modul entscheidet, welcher Typ verwendet wird.
**1** | Analysis Services HEAP.
**2** | Windows LFH.
**5** | Hybridzuweisung. Diese Zuweisung verwendet Windows LFH für \<= Zuordnungen von 16 KB und für die AS-Heap > Zuordnungen von 16 KB. 
**6** | Intel TBB-Zuweisung. Verfügbar in SQL Server 2016 SP1 (und höher) Analysis Services.
  
  
 **HeapTypeForObjects**  
  Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte. Gültige Werte sind:
  
   Einstellung | Description
--------|------------
**0** | Windows-LFH-Heap.
**1** | Analysis Services-Slotzuweisung.
**3** | Jedes Objekt verfügt über einen eigenen Analysis Services-Heap.

 
 **DefaultPagesCountToReuse**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **HandleIA64AlignmentFaults**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MidMemoryPrice**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MinimumAllocatedMemory**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **PreAllocate**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **SessionMemoryLimit**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **WaitCountIfHighMemory**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="see-also"></a>Siehe auch  
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  [SQL Server 2008 R2 Analysis Services-Vorgangshandbuch](http://go.microsoft.com/fwlink/?LinkID=225539)
  
