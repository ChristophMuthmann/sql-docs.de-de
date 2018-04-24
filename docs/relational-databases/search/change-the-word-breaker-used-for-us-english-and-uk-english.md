---
title: Ändern der für Englisch (USA) und Englisch (Vereinigtes Königreich) verwendeten Wörtertrennung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6b5d2177-db98-47f5-b32e-4b80a2f74ffe
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8969a3fe9e8f9722c90a90fe558f0e6c8c38d292
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="change-the-word-breaker-used-for-us-english-and-uk-english"></a>Ändern der für Englisch (USA) und Englisch (Großbritannien) verwendeten Wörtertrennung
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installiert eine neue Version (Version 14.0.4999.1038) der Wörtertrennung und der Wortstammerkennung für Englisch, die die frühere Version dieser Komponenten (Version 12.0.6828.0) ersetzt. Informationen zum geänderten Verhalten der neuen Komponenten finden Sie unter [Verhaltensänderungen der Volltextsuche](http://msdn.microsoft.com/library/573444e8-51bc-4f3d-9813-0037d2e13b8f). In diesem Thema wird beschrieben, wie von der neuen Version dieser Komponenten zur früheren Version gewechselt bzw. von der früheren Version zu der neuen Version zurückgewechselt wird. Bei Clusterinstallationen sollten diese Änderungen auf allen primären und passiven Knoten vorgenommen werden.  
  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wurden andere Wörtertrennungen verwendet, die durch andere CLSIDs für Englisch (USA) (LCID 1033) und Englisch (Großbritannien) (LCID 2057) dargestellt wurden. In dieser Version verwenden beide LCIDs die gleichen Komponenten mit den gleichen CLSIDs, wie in der folgenden Tabelle dargestellt:  
  
|LCID|Von früheren Versionen installierte Wörtertrennung<br /><br /> Version 12.0.6828.0|Von früheren Versionen installierte Wortstammerkennung|Von dieser Version installierte Wörtertrennung<br /><br /> Version 14.0.4999.1038|Von dieser Version installierte Wortstammerkennung|  
|----------|-------------------------------------------------------------------------|--------------------------------------------|-----------------------------------------------------------------------|---------------------------------------|  
|1033<br />(Englisch (USA))|188D6CC5-CB03-4C01-912E-47D21295D77E|EEED4C20-7F1B-11CE-BE57-00AA0051FE20|9faed859-0b30-4434-ae65-412e14a16fb8|e1e5ef84-c4a6-4e50-8188-99aef3de2659|  
|2057<br />(Englisch (Großbritannien))|173C97E2-AEBE-437C-9445-01B237ABF2F6|D99F7670-7F1A-11CE-BE57-00AA0051FE20|9faed859-0b30-4434-ae65-412e14a16fb8|e1e5ef84-c4a6-4e50-8188-99aef3de2659|  
  
 Bei den in diesem Thema beschriebenen Komponenten handelt es sich um DLL-Dateien, die im `MSSQL\Binn` -Ordner für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz installiert sind. Der vollständige Pfad ist in der Regel `C:\Program Files\Microsoft SQL Server\<instance>\MSSQL\Binn`.  
  
 Weitere Informationen zur Wörtertrennung und Wortstammerkennung finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
## <a name="switching-from-the-current-english-word-breaker-to-the-previous-english-word-breakers"></a>Wechseln von der aktuellen englischen Wörtertrennung zu den vorherigen englischen Wörtertrennungen  
  
#### <a name="to-switch-from-the-current-version-of-the-us-english-word-breaker-to-the-previous-version"></a>So wechseln Sie von der aktuellen Version der Wörtertrennung für Englisch (USA) zur früheren Version  
  
1.  Navigieren Sie in der Registrierung zu folgendem Knoten: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<Instanzstamm\>\MSSearch\CLSID**.  
  
2.  Fügen Sie mithilfe der folgenden Schritte für die COM ClassIDs für die Schnittstellen der früheren Wörtertrennung für Englisch (USA) und die Wortstammerkennung für LCID 1033 neue Schlüssel hinzu:  
  
    1.  Fügen Sie einen neuen Schlüssel mit dem Wert **{188D6CC5-CB03-4C01-912E-47D21295D77E}** für die frühere Wörtertrennung hinzu.  
  
    2.  Aktualisieren Sie die (standardmäßigen) Daten dieses Schlüsselwerts zu **langwrbk.dll**.  
  
    3.  Fügen Sie einen neuen Schlüssel mit dem Wert **{EEED4C20-7F1B-11CE-BE57-00AA0051FE20}** für die frühere Wortstammerkennung hinzu.  
  
    4.  Aktualisieren Sie die (standardmäßigen) Daten dieses Schlüsselwerts zu **infosoft.dll**.  
  
3.  Navigieren Sie in der Registrierung zu folgendem Knoten: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<Instanzstamm\>\MSSearch\Language\enu**.  
  
4.  Aktualisieren Sie den **WBreakerClass**-Schlüsselwert zu **{188D6CC5-CB03-4C01-912E-47D21295D77E}**.  
  
5.  Aktualisieren Sie den **StemmerClass** -Schlüsselwert zu **{EEED4C20-7F1B-11CE-BE57-00AA0051FE20}**.  
  
6.  Starten Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu.  
  
#### <a name="to-switch-from-the-current-version-of-the-uk-english-word-breaker-to-the-previous-version"></a>So wechseln Sie von der aktuellen Version der Wörtertrennung für Englisch (Vereinigtes Königreich) zur früheren Version  
  
1.  Navigieren Sie in der Registrierung zu folgendem Knoten: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<Instanzstamm\>\MSSearch\CLSID**.  
  
2.  Fügen Sie mithilfe der folgenden Schritte für die COM ClassIDs für die früheren Schnittstellen der Wörtertrennung für Englisch (Vereinigtes Königreich) und Wortstammerkennung für LCID 2057 einen neuen Schlüssel hinzu:  
  
    1.  Fügen Sie einen neuen Schlüssel mit dem Wert **{173C97E2-AEBE-437C-9445-01B237ABF2F6}** für die frühere Wörtertrennung hinzu.  
  
    2.  Aktualisieren Sie die (standardmäßigen) Daten dieses Schlüsselwerts zu **langwrbk.dll**.  
  
    3.  Fügen Sie einen neuen Schlüssel mit dem Wert **{D99F7670-7F1A-11CE-BE57-00AA0051FE20}** für die frühere Wortstammerkennung hinzu.  
  
    4.  Aktualisieren Sie die (standardmäßigen) Daten dieses Schlüsselwerts zu **infosoft.dll**.  
  
3.  Navigieren Sie in der Registrierung zu folgendem Knoten: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<Instanzstamm\>\MSSearch\Language\eng**.  
  
4.  Aktualisieren Sie den **WBreakerClass**-Schlüsselwert zu **{173C97E2-AEBE-437C-9445-01B237ABF2F6}**.  
  
5.  Aktualisieren Sie den **StemmerClass** -Schlüsselwert zu **{D99F7670-7F1A-11CE-BE57-00AA0051FE20}**.  
  
6.  Starten Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu.  
  
## <a name="switching-back-from-the-previous-english-word-breakers-to-the-current-english-word-breaker"></a>Zurückwechseln von der aktuellen englischen Wörtertrennung zu der früheren englischen Wörtertrennung  
  
#### <a name="to-switch-back-from-the-previous-version-of-the-us-english-word-breaker-to-the-current-version"></a>So wechseln Sie von der früheren Version der Wörtertrennung für Englisch (USA) zu der aktuellen Version zurück  
  
1.  Navigieren Sie in der Registrierung zu folgendem Knoten: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<Instanzstamm\>\MSSearch\CLSID**.  
  
2.  Wenn die folgenden Schlüssel nicht vorhanden sind, gehen Sie folgendermaßen vor, um einen neuen Schlüssel für die COM ClassIDs für die Schnittstellen der aktuellen Wörtertrennung für Englisch (USA) und die Wortstammerkennung für LCID 1033 hinzuzufügen:  
  
    1.  Fügen Sie einen neuen Schlüssel mit dem Wert **{9faed859-0b30-4434-ae65-412e14a16fb8}** für die aktuelle Wörtertrennung hinzu.  
  
    2.  Aktualisieren Sie die (standardmäßigen) Daten dieses Schlüsselwerts in **MsWb7.dll**.  
  
    3.  Fügen Sie einen neuen Schlüssel mit dem Wert **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}** für die aktuelle Wortstammerkennung hinzu.  
  
    4.  Aktualisieren Sie die (standardmäßigen) Daten dieses Schlüsselwerts in **MsWb7.dll**.  
  
3.  Navigieren Sie in der Registrierung zu folgendem Knoten: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<Instanzstamm\>\MSSearch\Language\eng**.  
  
4.  Aktualisieren Sie den **WBreakerClass**-Schlüsselwert in **{9faed859-0b30-4434-ae65-412e14a16fb8}**.  
  
5.  Aktualisieren Sie den **StemmerClass** -Schlüsselwert in **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}**.  
  
6.  Starten Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu.  
  
#### <a name="to-switch-back-from-the-previous-version-of-the-uk-english-word-breaker-to-the-current-version"></a>So wechseln Sie von der früheren Version der Wörtertrennung für Englisch (Vereinigtes Königreich) zu der aktuellen Version zurück  
  
1.  Navigieren Sie in der Registrierung zu folgendem Knoten: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<Instanzstamm\>\MSSearch\CLSID**.  
  
2.  Wenn die folgenden Schlüssel nicht vorhanden sind, gehen Sie folgendermaßen vor, um einen neuen Schlüssel für die COM ClassIDs für die Schnittstellen der aktuellen Wörtertrennung für Englisch (Vereinigtes Königreich) und die Wortstammerkennung für LCID 2057 hinzuzufügen:  
  
    1.  Fügen Sie einen neuen Schlüssel mit dem Wert **{9faed859-0b30-4434-ae65-412e14a16fb8}** für die aktuelle Wörtertrennung hinzu.  
  
    2.  Aktualisieren Sie die (standardmäßigen) Daten dieses Schlüsselwerts in **MsWb7.dll**.  
  
    3.  Fügen Sie einen neuen Schlüssel mit dem Wert **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}** für die aktuelle Wortstammerkennung hinzu.  
  
    4.  Aktualisieren Sie die (standardmäßigen) Daten dieses Schlüsselwerts in **MsWb7.dll**.  
  
3.  Navigieren Sie in der Registrierung zu folgendem Knoten: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<Instanzstamm\>\MSSearch\Language\eng**.  
  
4.  Aktualisieren Sie den **WBreakerClass**-Schlüsselwert in **{9faed859-0b30-4434-ae65-412e14a16fb8}**.  
  
5.  Aktualisieren Sie den **StemmerClass** -Schlüsselwert in **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}**.  
  
6.  Starten Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Wiederherstellen der von der Suche verwendeten Wörtertrennungen auf die vorherige Version](../../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)   
 [Verhaltensänderungen der Volltextsuche](http://msdn.microsoft.com/library/573444e8-51bc-4f3d-9813-0037d2e13b8f)  
  
  
