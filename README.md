# AZ-900: Introdução aos Conceitos Básicos do Microsoft Azure
## Módulo 3: Gerenciamento e Governança

### Visão Geral do Módulo

Este módulo da certificação AZ-900 foca em como os recursos do Azure são gerenciados e governados. Ele aborda as diversas ferramentas disponíveis para implantar e gerenciar recursos, a importância do Azure Resource Manager (ARM) como uma camada de gerenciamento central, e como o Azure Arc estende essas capacidades para ambientes híbridos e multinuvem.

---

### Ferramentas de Implantação e Gerenciamento

O Azure oferece várias ferramentas para interagir com seus serviços e recursos, permitindo flexibilidade para diferentes perfis de usuários, desde administradores de sistema até desenvolvedores.

**Principais Ferramentas de Interação:**
* [cite_start]**Portal do Azure:** Uma interface gráfica baseada na web que permite criar, gerenciar e monitorar todos os seus recursos do Azure de forma visual e intuitiva. [cite: 13, 22]
* [cite_start]**Azure PowerShell:** Um módulo que adiciona cmdlets específicos do Azure ao PowerShell, permitindo a automação e o gerenciamento de recursos através de scripts. [cite: 14, 22]
* [cite_start]**Interface de Linha de Comando (CLI) do Azure:** Uma ferramenta de linha de comando multiplataforma para gerenciar recursos do Azure. [cite: 14] É ideal para automação e para quem prefere trabalhar em terminais.
* [cite_start]**Azure Cloud Shell:** Um ambiente de shell interativo, autenticado e acessível pelo navegador para gerenciar recursos do Azure. [cite: 14, 22] [cite_start]Ele oferece a flexibilidade de escolher entre as experiências de shell Bash (com a CLI) ou PowerShell. [cite: 14]

**Domínio de Objetivos Abordados:**
* [cite_start]Descrever o portal do Azure. [cite: 13]
* [cite_start]Descrever o Azure Cloud Shell, incluindo a CLI do Azure e o Azure PowerShell. [cite: 14]

---

### Azure Resource Manager (ARM)

[cite_start]O ARM é a interface central para o gerenciamento de todos os recursos no Azure. [cite: 27] [cite_start]Ele funciona como uma camada de gerenciamento que processa todas as solicitações para criar, atualizar e excluir recursos na sua assinatura. [cite: 26]

**Como o ARM Funciona:**
1.  [cite_start]Um cliente (usuário ou ferramenta como Portal, PowerShell, CLI) envia uma solicitação. [cite: 30]
2.  [cite_start]A solicitação passa pelo `Azure Resource Manager`, que a autentica e autoriza. [cite: 30]
3.  [cite_start]O ARM encaminha a solicitação para o provedor de recursos apropriado (por exemplo, para máquinas virtuais, armazenamento, etc.). [cite: 30, 51]
4.  O provedor de recursos executa a ação solicitada.

Isso garante que todas as operações sejam consistentes e seguras, independentemente da ferramenta utilizada.

---

### Azure Arc

[cite_start]O Azure Arc estende o plano de gerenciamento do Azure para recursos localizados fora do Azure, como em datacenters locais, em outras nuvens (multinuvem) ou na borda (edge). [cite: 24]

**Propósito do Azure Arc:**
* Permite que você gerencie servidores, clusters Kubernetes e serviços de dados em ambientes híbridos usando as mesmas ferramentas e práticas de gerenciamento do Azure.
* [cite_start]Simplifica a governança e o gerenciamento ao fornecer um painel único para recursos no Azure e fora dele. [cite: 24]

---

### Infraestrutura como Código (IaC)

A Infraestrutura como Código é a prática de gerenciar e provisionar a infraestrutura de TI por meio de arquivos de definição legíveis por máquina, em vez de configuração manual.

**Benefícios da IaC:**
* [cite_start]**Consistência:** Garante que a infraestrutura seja implantada de forma consistente em todo o ecossistema de nuvem. [cite: 32]
* [cite_start]**Escalabilidade:** Permite gerenciar configurações em grande escala e provisionar rapidamente novos ambientes com base em uma configuração padrão. [cite: 33, 36]
* **Automação:** Reduz o esforço manual e o risco de erro humano.

---

### Modelos do Azure Resource Manager (ARM Templates)

Os modelos ARM são a principal forma de implementar a Infraestrutura como Código no Azure.

* [cite_start]**Definição:** São arquivos em formato JSON (JavaScript Object Notation) que definem os recursos que você deseja implantar no Azure sem a necessidade de escrever comandos de programação. [cite: 39]
* [cite_start]**Funcionamento:** Em vez de executar vários comandos para criar recursos (uma abordagem imperativa), você envia um único modelo ao ARM que declara o estado final desejado (uma abordagem declarativa). [cite: 51] O ARM então orquestra a implantação para que o resultado corresponda ao modelo.

**Vantagens dos Modelos ARM:**
* [cite_start]**Sintaxe Declarativa:** Você descreve *o que* quer implantar, não *como* implantar. [cite: 42]
* [cite_start]**Resultados Repetíveis:** Garante que a implantação seja idêntica todas as vezes. [cite: 43]
* [cite_start]**Orquestração:** O ARM gerencia as dependências e implanta os recursos na ordem correta. [cite: 44]
* [cite_start]**Modularidade:** Permite dividir modelos complexos em arquivos menores e reutilizáveis. [cite: 45]
* [cite_start]**Validação Integrada:** O ARM valida o modelo antes de iniciar a implantação para evitar erros. [cite: 46]
* [cite_start]**Código Exportável:** Você pode exportar o estado atual de um grupo de recursos para um modelo ARM. [cite: 47]

---

### Bicep

O Bicep é uma linguagem de domínio específico (DSL) que oferece uma sintaxe mais simples e limpa para criar modelos ARM. Ele serve como uma abstração sobre o JSON dos modelos ARM, tornando a criação de infraestrutura como código mais fácil e menos verbosa. O código Bicep é transpilado para um modelo ARM JSON padrão antes da implantação.

O slide mostra um exemplo de código Bicep para a criação de uma conta de armazenamento:

```bicep
param location string = resourceGroup().location
param storageAccountName string = 'toylaunch${uniqueString(resourceGroup().id)}'

resource storageAccount 'Microsoft.Storage/storageAccounts@2021-06-01' = {
  name: storageAccountName
  location: location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
  properties: {
    accessTier: 'Hot'
  }
}
```
[cite_start][cite: 54]
