---
title: Eigenschaften von Datenbankdimensionen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- metadata [Analysis Services]
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 075548ef-08a3-413c-8ee0-4a074c276fcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e4dd5b6f8a241d3173cdca8b03cce4fb9a373b8d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196040"
---
# <a name="database-dimension-properties"></a>Eigenschaften von Datenbankdimensionen
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], die Merkmale einer Dimension sind definiert, indem die Metadaten für die Dimension basierend auf den Einstellungen der verschiedenen Dimensionseigenschaften und auf die Attribute oder Hierarchien, die der Dimension enthalten sind. In der folgenden Tabelle werden die Dimensionseigenschaften in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|`AttributeAllMemberName`|Gibt den Namen des Alle-Elements für Attribute in einer Dimension an.|  
|`Collation`|Bestimmt die von der Dimension verwendete Sortierung.|  
|`CurrentStorageMode`|Enthält den aktuellen Speichermodus für die Dimension.|  
|`DependsOnDimension`|Enthält die ID einer anderen Dimension, von der die Dimension abhängt, falls vorhanden.|  
|`Description`|Enthält die Beschreibung einer Dimension.|  
|`ErrorConfiguration`|Konfigurierbare Fehlerbehandlungseinstellungen für die Bearbeitung doppelter Schlüssel, unbekannter Schlüssel, für Fehlergrenzen, Aktionen bei Erkennung von Fehlern, Fehlerprotokolldateien und die Bearbeitung von NULL-Schlüsseln.|  
|`ID`|Enthält den eindeutigen Bezeichner (ID) der Dimension.|  
|`Language`|Gibt die Standardsprache für die Dimension an.|  
|`MdxMissingMemberMode`|Legt die Verarbeitung fehlender Elemente in MDX-Anweisungen (Multidimensional Expressions) fest.|  
|`MiningModelID`|Enthält die ID des Miningmodells, der die Data Mining-Dimension zugeordnet ist. Diese Eigenschaft kann nur angewendet werden, wenn die Dimension eine Miningmodelldimension ist.|  
|`Name`|Gibt den Namen der Dimension an.|  
|`ProactiveCaching`|Definiert die Einstellungen für die Dimension für die proaktive Zwischenspeicherung.|  
|`ProcessingGroup`|Gibt die Verarbeitungsgruppe an. Die Werte sind ByAttribute oder ByTable. Der Standardwert ist `ByAttribute`.|  
|`ProcessingMode`|Gibt an, ob [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] während oder nach der Verarbeitung indizieren und aggregieren soll.|  
|`ProcessingPriority`|Bestimmt die Verarbeitungspriorität der Dimension während Hintergrundvorgängen wie verzögerte Aggregation, Indizierung oder Clustererstellung.|  
|`Source`|Identifiziert die Datenquellensicht, an die die Dimension gebunden ist.|  
|`StorageMode`|Bestimmt den Speichermodus für die Dimension.|  
|`Type`|Gibt den Typ der Dimension an.|  
|`UnknownMember`|Gibt an, ob das unbekannte Element sichtbar ist.|  
|`UnknownMemberName`|Gibt die Beschriftung in der standardmäßigen Sprache der Dimension für das unbekannte Element der Dimension an.|  
|`WriteEnabled`|Gibt an, ob das Rückschreiben von Dimensionen unterstützt wird (unterliegt den Sicherheitsberechtigungen).|  
  
> [!NOTE]  
>  Weitere Informationen zum Festlegen der Werte für die Eigenschaften ErrorConfiguration und UnknownMember bei der Arbeit mit null-Werte und andere Probleme mit der Datenintegrität finden Sie unter [Handling Data Integrity Issues in Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Attributhierarchien](attributes-and-attribute-hierarchies.md)   
 [Benutzerhierarchien](user-hierarchies.md)   
 [Dimensionsbeziehungen](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Dimensionen &#40;Analysis Services – mehrdimensionale Daten&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
