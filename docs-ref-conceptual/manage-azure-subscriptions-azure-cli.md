---
title: Administración de suscripciones de Azure con la CLI de Azure
description: Administre las suscripciones de Azure con la CLI de Azure.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/09/2018
ms.topic: conceptual
ms.produdct: azure
ms.technology: azure-cli
ms.devlang: azure-cli
ms.openlocfilehash: 7bffd91fc31452fc745bc572262f10645e4179eb
ms.sourcegitcommit: f7554c00b5d5dca0ec716cbf996eb6654183ec37
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47237602"
---
# <a name="use-multiple-azure-subscriptions"></a>Uso de varias suscripciones de Azure

La mayoría de los usuarios de Azure solo tendrán una suscripción. Sin embargo, si forma parte de varias organizaciones o su organización ha dividido el acceso a determinados recursos mediante agrupaciones, habrá varias suscripciones dentro de Azure. La CLI admite la selección de una suscripción global y por comando.

## <a name="tenants-users-and-subscriptions"></a>Inquilinos, usuarios y suscripciones

Quizás no tenga muy clara la diferencia entre los inquilinos, los usuarios y las suscripciones de Azure. Un _inquilino_ es la entidad de Azure Active Directory que abarca toda la organización. Este inquilino tiene al menos una _suscripción_ y un _usuario_. Un usuario es un individuo que está asociado a un único inquilino, la organización a la que pertenece. Los usuarios son las cuentas que inician sesión en Azure para crear, administrar y usar los recursos.
Un usuario puede tener acceso a varias _suscripciones_, que son los acuerdos con Microsoft para usar los servicios en la nube, incluido Azure. Cada recurso está asociado a una suscripción.

Para más información sobre las diferencias entre inquilinos, usuarios y suscripciones, vea el [diccionario de terminología de la nube de Azure](/azure/azure-glossary-cloud-terminology).  Para más información sobre cómo agregar una nueva suscripción a su inquilino de Azure Active Directory, consulte [Adición de una suscripción de Azure a Azure Active Directory](/azure/active-directory/active-directory-how-subscriptions-associated-directory).
Para más información sobre cómo iniciar sesión un inquilino específico, consulte [Inicio de sesión con la CLI de Azure](/cli/azure/authenticate-azure-cli).

## <a name="change-the-active-subscription"></a>Cambio de la suscripción activa 

Para acceder a los recursos dentro de una suscripción, cambie la suscripción activa o use el argumento `--subscription`. Para cambiar la suscripción para todos los comandos, se usa [az account set](/cli/azure/account#az-account-set).

Para cambiar su suscripción activa:

1. Obtenga la lista de suscripciones con el comando [az account list](/cli/azure/account#az-account-list):

    ```azurecli-interactive
    az account list --output table
    ```
2. Use `az account set` con el identificador de suscripción o el nombre al que desee cambiar.

    ```azurecli-interactive
    az account set --subscription "My Demos"
    ```

Para ejecutar solo un comando con una suscripción diferente, use el argumento `--subscription`. Este argumento necesita un identificador o un nombre de suscripción:

```azurecli-interactive
az vm create --subscription "My Demos" --resource-group MyGroup --name NewVM --image Ubuntu
```
