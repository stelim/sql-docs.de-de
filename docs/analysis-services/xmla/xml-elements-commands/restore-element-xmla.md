---
title: Restore-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Restore Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Restore
- urn:schemas-microsoft-com:xml-analysis#Restore
- microsoft.xml.analysis.restore
helpviewer_keywords:
- Restore command
ms.assetid: bb5a0c92-3927-4fa4-975b-6e4d79e0a912
caps.latest.revision: 26
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 08586ce2b7d5126250b82bc65655c7b69872a346
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="restore-element-xmla"></a>Restore-Element (XMLA)
  Stellt eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank aus einer Sicherungsdatei.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <Restore>  
      <DatabaseName>...</DatabaseName>  
      <DatabaseID>...</DatabaseID>  
      <File>...</File>  
      <Security>...</Security>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <Locations>...</Locations>  
      <DbStorageLocation>...</DbStorageLocation>  
   </Restore>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md), [DatabaseName](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md), [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md), [Datei](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [Speicherorte](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md), [Kennwort](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md), [Sicherheit](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md), [DbStorageLocation](../../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)|  
  
## <a name="remarks"></a>Hinweise  
 Die **wiederherstellen** -Befehl wird eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank in der **DatabaseName** Elements aus einer Sicherungsdatei und optional Wiederherstellungen Remotepartitionen aus remotesicherungsdateien.  
  
 Je nach dem Speichermodus der in der Sicherungsdatei gespeicherten Objekte werden mit dem **Restore** -Befehl die in der folgenden Tabelle aufgelisteten Informationen wiederhergestellt.  
  
|Speichermodus|Informationen|  
|------------------|-----------------|  
|Mehrdimensionale OLAP (MOLAP)|Quelldaten, Aggregationen und Metadaten|  
|Hybride OLAP (HOLAP)|Aggregationen und Metadaten|  
|Relationale OLAP (ROLAP)|Metadaten|  
  
 Während einer **wiederherstellen** Befehl, eine exklusive Sperre befindet sich auf die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank in der **DatabaseName** Element. Die Sperre wird nach Abschluss des **Restore** -Befehls wieder aufgehoben.  
  
 Weitere Informationen zum Sichern und Wiederherstellen von Datenbanken finden Sie unter [sichern, wiederherstellen, und Synchronisieren von Datenbanken &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  Für jede Sicherungsdatei muss der Benutzer, der den Wiederherstellungsbefehl ausführt, über die Berechtigung zum Lesen von dem für jede Datei angegebenen Sicherungsspeicherort verfügen. Zum Wiederherstellen einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Datenbank, die nicht auf dem Server installiert ist, muss der Benutzer zusätzlich Mitglied der Serverrolle für die betreffende [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz sein. Zum Überschreiben einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Datenbank muss der Benutzer entweder Mitglied der Serverrolle für die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz oder Mitglied einer Datenbankrolle mit den Berechtigungen "Vollzugriff" (Administrator) für die wiederherzustellende Datenbank sein.  
  
> [!NOTE]  
>  Nach dem Wiederherstellen einer vorhandenen Datenbank verliert der Benutzer, der die Datenbank wiederhergestellt hat, möglicherweise den Zugriff auf diese Datenbank. Dies ist u. U. der Fall, wenn der Benutzer zum Zeitpunkt der Sicherung kein Mitglied der Serverrolle oder der Datenbankrolle mit der Berechtigung "Vollzugriff (Administrator)" war.  
  
## <a name="see-also"></a>Siehe auch  
 [Backup-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [Batch-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Parallel-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)   
 [Synchronisieren Sie-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  