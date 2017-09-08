---
title: MeasureGroupAttributeBinding-Datentyp (Out-of-Line) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MeasureGroupAttributeBinding Data Type (out-of-line)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MeasureGroupAttributeBinding data type
ms.assetid: bfe09a95-4e04-4f93-9389-7dd0b4c8f5e4
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b6e2d9f373bd371b19bbedda669cd2e56352ec3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="measuregroupattributebinding-data-type-out-of-line-assl"></a>MeasureGroupAttributeBinding-Datentyp (Out-of-Line) (ASSL)
  Definiert einen abgeleiteten Datentyp, der die Out-of-Line-Bindung eines Attributs in einer Dimension, die in einer Measuregruppe enthalten ist, darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MeasureGroupAttributeBinding>  
   <!-- The following elements extend Binding -->  
   <DatabaseID>...</DatabaseID>  
   <CubeID>...</CubeID>  
   <MeasureGroupID>...</MeasureGroupID>  
   <GranularityAttributeID>...</GranularityAttributeID>  
   <Source>...</Source>  
</MeasureGroupAttributeBinding>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|[Bindung](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[CubeID](../../../analysis-services/scripting/properties/cubeid-element-assl.md), [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md), [MeasureGroupID](../../../analysis-services/scripting/properties/measuregroupid-element-assl.md), [GranularityAttributeID](../../../analysis-services/scripting/properties/granularityattributeid-element-assl.md), [Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|Abgeleitete Elemente|[Binden von](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md) ([Bindungen](../../../analysis-services/scripting/collections/attributes-element-assl.md) Auflistung von XML for Analysis (XMLA) [Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) und [Prozess](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) Befehle)|  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen über Out-of-Line-Bindungen finden Sie unter [&#40; Datenquellen und Bindungen SSAS – mehrdimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  