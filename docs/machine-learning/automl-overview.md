---
title: Aprendizado de máquina automatizado com o ML.NET
description: Visão geral do treinamento e seleção automáticos de modelos
author: natke
ms.date: 05/01/2019
ms.topic: overview
ms.custom: mvc
ms.author: nakersha
ms.openlocfilehash: 39e454d67f60280c6a43e3b80d788d873345ab77
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67307385"
---
# <a name="automated-machine-learning-with-mlnet"></a>Aprendizado de máquina automatizado com o ML.NET

O aprendizado de máquina automatizado é um recurso do ML.NET que executa a seleção e treinamento automáticos de modelos. Você especifica a tarefa de aprendizado de máquina e fornece um conjunto de dados. O ML automatizado escolhe o modelo com as melhores métricas. Ele produz:
- um arquivo de modelo que pode ser carregado em seu aplicativo de previsão
- código do aplicativo para fazer previsões
- o código-fonte usado para seleção de recursos e o treinamento do modelo (para entender o modelo)

> [!NOTE]
> Esse recurso está atualmente em versão prévia e o material pode estar sujeito a alterações. 

O ML automatizado é atualmente limitado a [tarefas](resources/tasks.md) de aprendizado de máquina de classificação binária, classificação multiclasse e regressão. As outras tarefas de aprendizado de máquina terão suporte em versões futuras.

Há três maneiras de usar o ML automatizado:
1. Na linha de comando, com a [CLI do ML.NET](automate-training-with-cli.md)
1. Por meio de um aplicativo com a [API de ML automatizada](how-to-guides/how-to-use-the-automl-api.md)
1. Com uma interface gráfica do usuário, com o construtor de modelo do ML.NET
