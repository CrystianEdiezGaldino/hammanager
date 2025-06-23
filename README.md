# 🍔 FastFoodRush - Jogo de Gerenciamento de Restaurante

## 📋 Visão Geral

FastFoodRush é um jogo de simulação de restaurante desenvolvido em Unity, onde o jogador gerencia um estabelecimento de fast-food. O jogo combina elementos de gerenciamento de negócios com mecânicas de ação, permitindo que o jogador construa, expanda e otimize seu restaurante através de múltiplos níveis.

### 🎯 Objetivo do Jogo
- Gerenciar um restaurante de fast-food de forma eficiente
- Atender clientes rapidamente para maximizar lucros
- Expandir o negócio através de upgrades e desbloqueios
- Progresar através de múltiplos restaurantes com complexidade crescente

## 🎮 Mecânicas Principais

### Sistema de Pilhas (WobblingStack)
- **Localização**: `Assets/FastFoodRush/Scripts/WobblingStack.cs`
- **Função**: Simula objetos empilhados com movimento realista
- **Tipos**: Comida, Lixo, Pacotes
- **Características**: 
  - Movimento de balanço baseado na entrada do jogador
  - Animação de salto ao adicionar itens
  - Diferentes deslocamentos para cada tipo de objeto
  - Sistema de bandeja que aparece quando há itens
  - Efeito de inclinação progressiva baseado na altura da pilha

### Sistema de Tutorial
- **Localização**: `Assets/FastFoodRush/Scripts/Tutorial.cs`
- **Função**: Guia o jogador através das mecânicas básicas
- **Estados**: 13 estados progressivos desde o início até a conclusão
- **Recursos**: 
  - Seta indicadora animada com movimento oscilante
  - Mensagens contextuais personalizáveis
  - Progressão automática baseada em ações do jogador
  - Persistência de progresso via PlayerPrefs

### Sistema de Pontos de Referência
- **Localização**: `Assets/FastFoodRush/Scripts/Waypoints.cs`
- **Função**: Define caminhos para movimento de objetos
- **Visualização**: Gizmos no editor para facilitar o design de níveis
- **Recursos**: 
  - Esferas coloridas para representar pontos
  - Linhas conectando pontos sequenciais
  - Configuração de cores e tamanhos personalizáveis

## 🏗️ Arquitetura do Projeto

### 📁 Estrutura de Pastas

```
Assets/FastFoodRush/Scripts/
├── Core/                    # Sistemas principais
│   ├── RestaurantManager.cs # Gerenciador central do jogo
│   ├── SaveSystem.cs        # Sistema de persistência
│   ├── AudioManager.cs      # Gerenciamento de áudio
│   ├── PoolManager.cs       # Sistema de pool de objetos
│   ├── MainMenuManager.cs   # Gerenciamento do menu principal
│   └── RestaurantData.cs    # Estrutura de dados do restaurante
├── Controllers/            # Controladores de entidades
│   ├── PlayerController.cs  # Controle do jogador
│   ├── CustomerController.cs # IA dos clientes
│   ├── EmployeeController.cs # IA dos funcionários
│   ├── CarController.cs     # Sistema de drive-thru
│   └── CameraController.cs  # Controle de câmera
├── Interactables/          # Objetos interativos
│   ├── Interactable.cs      # Classe base para interações
│   ├── ObjectPile.cs        # Pilhas de objetos
│   ├── ObjectStack.cs       # Pilhas organizadas
│   ├── TrashBin.cs          # Lixeiras
│   ├── MoneyPile.cs         # Pilhas de dinheiro
│   ├── Door.cs              # Sistema de portas
│   ├── WorkingSpot.cs       # Pontos de trabalho
│   └── Activator.cs         # Ativadores
├── UI/                     # Interface do usuário
│   ├── Map.cs               # Sistema de mapa
│   ├── UpgradeHandler.cs    # Gerenciamento de upgrades
│   ├── ScreenFader.cs       # Transições de tela
│   ├── OrderInfo.cs         # Informações de pedidos
│   ├── ProgressDisplay.cs   # Barras de progresso
│   └── SettingsWindow.cs    # Janela de configurações
├── Unlockables/           # Sistema de desbloqueios
│   ├── Unlockable.cs        # Classe base para desbloqueios
│   ├── UnlockableBuyer.cs   # Sistema de compra
│   ├── Seating.cs           # Sistema de assentos
│   ├── UpgradeableMesh.cs   # Meshes atualizáveis
│   ├── Workstations/        # Estações de trabalho
│   │   ├── Workstation.cs   # Classe base para estações
│   │   ├── CounterTable.cs  # Balcões de atendimento
│   │   ├── DriveThruCounter.cs # Balcão drive-thru
│   │   └── PackingTable.cs  # Mesa de empacotamento
│   └── Machines/           # Máquinas de produção
│       ├── FoodMachine.cs   # Máquina de comida
│       ├── BurgerMachine.cs # Máquina de hambúrgueres
│       └── DonutFryer.cs    # Fritadeira de donuts
├── Animations/            # Animações
└── Editor/                # Scripts específicos do editor
```

### 🎯 Sistemas Principais

#### 1. RestaurantManager (Core)
- **Arquivo**: `Assets/FastFoodRush/Scripts/Core/RestaurantManager.cs`
- **Função**: Gerenciador central do jogo (Singleton)
- **Responsabilidades**:
  - Gerenciamento de dinheiro com formatação automática
  - Sistema de upgrades com crescimento exponencial
  - Controle de funcionários com spawn aleatório
  - Sistema de desbloqueios progressivos
  - Persistência de dados por restaurante
  - Gerenciamento de pilhas de objetos
  - Sistema de eventos para upgrades e desbloqueios

#### 2. Controladores de Entidades

##### PlayerController
- **Movimento**: Baseado em CharacterController com entrada diagonal
- **Capacidades**: Pilha de objetos com limite configurável
- **Upgrades**: Velocidade e capacidade modificáveis
- **Animações**: Sistema IK para posicionamento de mãos
- **Áudio**: Sons de passos sincronizados com animações

##### CustomerController
- **IA**: Navegação via NavMeshAgent
- **Comportamento**: 
  - Entrada automática com abertura de portas
  - Sistema de fila para pedidos
  - Pedidos aleatórios (1-5 itens)
  - Movimento para assentos designados
  - Animação de comer e saída
- **Interação**: Sistema de pilha para carregar comida

##### EmployeeController
- **IA**: Movimento automático entre estações
- **Capacidades**: Carregamento, processamento, atendimento
- **Upgrades**: Velocidade e capacidade modificáveis
- **Spawn**: Posição aleatória dentro de raio configurável

##### CarController
- **Sistema**: Drive-thru automatizado
- **Movimento**: Seguindo waypoints
- **Interação**: Entrega de pedidos empacotados

#### 3. Sistema de Interação

##### Interactables
- **Interactable**: Classe base para objetos interativos
- **ObjectPile**: Pilhas de objetos coletáveis
- **ObjectStack**: Pilhas organizadas com limite
- **TrashBin**: Sistema de descarte de lixo
- **MoneyPile**: Coleta de receita
- **Door**: Sistema de portas automáticas
- **WorkingSpot**: Pontos de trabalho para funcionários
- **Activator**: Ativadores para eventos

##### Unlockables
- **Unlockable**: Classe base para itens desbloqueáveis
- **UnlockableBuyer**: Sistema de compra com interface
- **Seating**: Sistema de assentos para clientes
- **UpgradeableMesh**: Meshes que mudam com upgrades

##### Workstations
- **Workstation**: Classe base para estações de trabalho
- **CounterTable**: Balcões de atendimento
- **DriveThruCounter**: Balcão específico para drive-thru
- **PackingTable**: Mesa para empacotar pedidos

##### Machines
- **FoodMachine**: Máquina genérica de produção
- **BurgerMachine**: Máquina específica para hambúrgueres
- **DonutFryer**: Fritadeira para donuts

## 💼 Regras de Negócio

### Sistema Monetário
- **Dinheiro Inicial**: 1.000 unidades
- **Fonte de Receita**: 
  - Venda de comida individual
  - Venda de pacotes empacotados
  - Multiplicador de lucro baseado em upgrades
- **Custos**: 
  - Upgrades de funcionários e jogador
  - Desbloqueios de equipamentos
  - Contratação de funcionários

### Sistema de Upgrades
- **Tipos de Upgrade**:
  - `EmployeeSpeed`: Velocidade dos funcionários (+0.2 por nível)
  - `EmployeeCapacity`: Capacidade de carregamento (+3 por nível)
  - `EmployeeAmount`: Quantidade de funcionários (+1 por nível)
  - `PlayerSpeed`: Velocidade do jogador (+0.2 por nível)
  - `PlayerCapacity`: Capacidade do jogador (+3 por nível)
  - `Profit`: Multiplicador de lucro (+0.1 por nível)

- **Fórmula de Preço**: `baseUpgradePrice * (upgradeGrowthFactor ^ nível_atual)`
- **Preço Base**: 250 unidades
- **Fator de Crescimento**: 1.5x
- **Máximo de Níveis**: Ilimitado (crescimento exponencial)

### Sistema de Desbloqueios
- **Preço Base**: 75 unidades
- **Fator de Crescimento**: 1.1x
- **Tipos de Desbloqueios**:
  - **Assentos**: Capacidade de atendimento
  - **Balcões**: Pontos de atendimento
  - **Máquinas**: Produção de comida
  - **Escritórios**: Contratação de funcionários
- **Progressão**: Sequencial (próximo item só disponível após comprar o anterior)

### Sistema de Funcionários
- **Spawn**: Posição aleatória dentro de raio de 3 unidades
- **IA**: 
  - Movimento automático entre estações de trabalho
  - Carregamento de itens até capacidade máxima
  - Processamento de pedidos
  - Atendimento de clientes
- **Capacidades**: 
  - Velocidade baseada em upgrades
  - Capacidade de carregamento configurável
  - Trabalho em múltiplas estações

### Sistema de Clientes
- **Geração**: Automática baseada em tempo
- **Comportamento**:
  - Entrada com abertura automática de portas
  - Formação de fila para pedidos
  - Pedidos aleatórios (1-5 itens)
  - Movimento para assentos disponíveis
  - Animação de comer
  - Saída automática
- **Tempo de Atendimento**: Baseado na eficiência do restaurante

## 🔧 Como Navegar no Código

### Para Adicionar Novos Objetos Interativos
1. **Crie um script** na pasta `Interactables/`
2. **Herde de `Interactable`** ou `ObjectPile` dependendo do tipo
3. **Implemente os métodos necessários**:
   - `OnInteract()` para interações básicas
   - `CanInteract()` para validações
   - `GetInteractionText()` para texto da UI
4. **Configure no Inspector** com tooltips em português

### Para Adicionar Novos Desbloqueios
1. **Crie um script** na pasta `Unlockables/`
2. **Herde de `Unlockable`** ou classes específicas
3. **Configure preços e requisitos**:
   - `basePrice`: Preço inicial
   - `growthFactor`: Fator de crescimento
   - `requirements`: Pré-requisitos
4. **Adicione à lista** no `RestaurantManager`
5. **Configure no Inspector** com tooltips

### Para Modificar Mecânicas de Jogo
1. **Dinheiro**: `RestaurantManager.AdjustMoney(int change)`
2. **Upgrades**: `RestaurantManager.PurchaseUpgrade(Upgrade upgrade)`
3. **Funcionários**: `RestaurantManager.SpawnEmployee()`
4. **Desbloqueios**: `RestaurantManager.BuyUnlockable()`

### Para Personalizar o Tutorial
1. **Edite `Tutorial.cs`**
2. **Adicione novos estados** ao enum `TutorialState`
3. **Configure mensagens** no Inspector via `StateMessage`
4. **Implemente lógica de progressão** nos loops while
5. **Adicione setas indicadoras** com `UpdateArrowPosition()`

### Para Adicionar Novos Tipos de Comida
1. **Crie prefabs** na pasta `Assets/FastFoodRush/Prefabs/`
2. **Configure componentes** necessários
3. **Adicione à pool** via `PoolManager`
4. **Configure máquinas** para produção
5. **Atualize UI** de pedidos se necessário

## 🎨 Sistema de UI

### Componentes Principais
- **OrderInfo**: Exibe informações de pedidos em tempo real
- **ProgressDisplay**: Barras de progresso para processos
- **SettingsWindow**: Configurações do jogo
- **ScreenFader**: Transições suaves entre cenas
- **Map**: Sistema de navegação e visualização
- **UpgradeHandler**: Interface para compra de upgrades

### Localização
- **Pasta**: `Assets/FastFoodRush/Scripts/UI/`
- **Integração**: Conectado ao `RestaurantManager`
- **Idioma**: Português brasileiro
- **Tooltips**: Todos traduzidos

### Responsividade
- **Adaptação**: Interface responsiva para diferentes resoluções
- **Animações**: Transições suaves com DOTween
- **Feedback**: Efeitos visuais para interações

## 💾 Sistema de Salvamento

### Estrutura de Dados (RestaurantData)
```csharp
public class RestaurantData
{
    public string RestaurantID { get; set; }        // ID único do restaurante
    public long Money { get; set; }                 // Dinheiro atual
    public int EmployeeSpeed { get; set; }          // Nível de velocidade dos funcionários
    public int EmployeeCapacity { get; set; }       // Nível de capacidade dos funcionários
    public int EmployeeAmount { get; set; }         // Quantidade de funcionários
    public int PlayerSpeed { get; set; }            // Nível de velocidade do jogador
    public int PlayerCapacity { get; set; }         // Nível de capacidade do jogador
    public int Profit { get; set; }                 // Nível de multiplicador de lucro
    public int UnlockCount { get; set; }            // Quantidade de itens desbloqueados
    public int PaidAmount { get; set; }             // Valor pago pelo último desbloqueio
    public bool IsUnlocked { get; set; }            // Se o restaurante está desbloqueado
}
```

### Persistência (SaveSystem)
- **Arquivo**: `Assets/FastFoodRush/Scripts/Core/SaveSystem.cs`
- **Método**: Serialização JSON
- **Localização**: PlayerPrefs para dados críticos
- **Backup**: Sistema de backup automático

### Salvamento Automático
- **Ao pausar** o aplicativo
- **Ao sair** do jogo
- **Ao mudar** de cena
- **Após ações** importantes (compras, upgrades)

### Dados Salvos por Restaurante
- **Progresso monetário** e upgrades
- **Itens desbloqueados** e configurações
- **Quantidade de funcionários** contratados
- **Estado de desbloqueio** do restaurante

## 🎵 Sistema de Áudio

### Componentes
- **AudioManager**: Gerenciamento central de áudio (Singleton)
- **Músicas**: Trilha sonora de fundo por ambiente
- **Efeitos**: Sons de interação, feedback e ambiente
- **Sincronização**: Áudio sincronizado com animações

### Localização
- **Script**: `Assets/FastFoodRush/Scripts/Core/AudioManager.cs`
- **Assets**: `Assets/FastFoodRush/Sounds/`
- **Configuração**: Volumes separados para música e efeitos

### Tipos de Áudio
- **BGM**: Música de fundo por restaurante
- **SFX**: Efeitos sonoros de interação
- **Ambient**: Sons ambientais
- **UI**: Sons de interface

## 🎬 Sistema de Animações

### Componentes
- **Animator**: Controle de animações via Mecanim
- **IK System**: Posicionamento dinâmico de mãos
- **Animation Events**: Sincronização de áudio
- **Blend Trees**: Transições suaves entre animações

### Animações Principais
- **Movimento**: Caminhada, corrida, parado
- **Interação**: Carregar, descarregar, trabalhar
- **Cliente**: Sentar, comer, sair
- **Funcionário**: Trabalhar, carregar, processar

## 🚀 Como Executar

### Requisitos do Sistema
- **Unity**: 2022.3 LTS ou superior
- **Plataforma**: Windows, macOS, Linux
- **Memória**: 4GB RAM mínimo
- **GPU**: Compatível com DirectX 11 ou OpenGL 4.1

### Instalação
1. **Clone o repositório** ou baixe o projeto
2. **Abra o Unity Hub** e adicione o projeto
3. **Selecione a versão** do Unity (2022.3 LTS)
4. **Aguarde a importação** dos assets

### Execução
1. **Navegue até** `Assets/FastFoodRush/Scenes/`
2. **Abra a cena** `MainMenu.unity`
3. **Pressione Play** no Editor
4. **Selecione um restaurante** para começar

### Cenas Disponíveis
- **MainMenu**: Menu principal do jogo
- **Restaurant01**: Primeiro restaurante (tutorial)
- **Restaurant02**: Segundo restaurante (intermediário)
- **Restaurant03**: Terceiro restaurante (avançado)

## 🔍 Debug e Desenvolvimento

### Comandos de Debug
- **Adicionar Dinheiro**: Tecla configurável (padrão: F1)
- **Logs Detalhados**: Console do Unity
- **Gizmos**: Visualização no Scene View
- **Performance**: Profiler integrado

### Configurações do Editor
- **Gizmos**: Ativados para visualização de waypoints
- **Debug Mode**: Disponível durante desenvolvimento
- **Hot Reload**: Recarregamento automático de scripts
- **Scene View**: Visualização 3D com controles

### Ferramentas de Desenvolvimento
- **Pool Manager**: Gerenciamento de objetos reutilizáveis
- **Save System**: Sistema de persistência robusto
- **Audio Manager**: Controle centralizado de áudio
- **Tutorial System**: Sistema flexível de tutoriais

## 📝 Convenções de Código

### Comentários
- **Todos os comentários** em português brasileiro
- **Documentação XML** para métodos públicos
- **Tooltips traduzidos** para elementos da UI
- **Comentários inline** explicativos para lógica complexa

### Nomenclatura
- **Classes**: PascalCase (`RestaurantManager`)
- **Métodos**: PascalCase (`AdjustMoney()`)
- **Variáveis**: camelCase (`baseSpeed`)
- **Constantes**: UPPER_CASE (`GRAVITY_VALUE`)
- **Enums**: PascalCase (`TutorialState`)

### Organização
- **Namespace**: `CryingSnow.FastFoodRush`
- **Regiões**: Para organização de código
- **Separação**: Clara de responsabilidades
- **Modularidade**: Componentes reutilizáveis

### Padrões de Design
- **Singleton**: Para gerenciadores globais
- **Observer**: Para eventos e notificações
- **Factory**: Para criação de objetos
- **Pool**: Para reutilização de objetos

## 🎯 Funcionalidades Avançadas

### Sistema de Drive-Thru
- **CarController**: Movimento automático de carros
- **Waypoints**: Sistema de navegação
- **Empacotamento**: Sistema de pacotes
- **Atendimento**: Balcão específico

### Sistema de Upgrades Dinâmicos
- **Crescimento Exponencial**: Preços aumentam progressivamente
- **Múltiplos Tipos**: 6 categorias de upgrades
- **Efeitos Visuais**: Partículas de desbloqueio
- **Persistência**: Salvamento automático

### Sistema de IA Avançada
- **NavMesh**: Navegação inteligente
- **Pathfinding**: Cálculo de rotas otimizadas
- **Comportamento**: Estados de máquina
- **Adaptação**: Baseada em upgrades

## 🤝 Contribuição

### Diretrizes para Contribuição
1. **Mantenha as convenções** de código estabelecidas
2. **Adicione comentários** em português brasileiro
3. **Teste as funcionalidades** antes de commitar
4. **Documente mudanças** significativas
5. **Use branches** para features novas
6. **Faça commits** atômicos e descritivos

### Processo de Desenvolvimento
1. **Fork** o repositório
2. **Crie uma branch** para sua feature
3. **Desenvolva** seguindo as convenções
4. **Teste** todas as funcionalidades
5. **Documente** as mudanças
6. **Submeta** um pull request

### Áreas de Melhoria
- **Performance**: Otimização de renderização
- **IA**: Comportamentos mais complexos
- **UI/UX**: Melhorias na interface
- **Áudio**: Mais variedade de sons
- **Animações**: Transições mais suaves

## 📊 Métricas e Performance

### Otimizações Implementadas
- **Object Pooling**: Reutilização de objetos
- **LOD System**: Níveis de detalhe
- **Culling**: Remoção de objetos fora de vista
- **Batching**: Agrupamento de renderização

### Monitoramento
- **FPS**: Controle de taxa de quadros
- **Memory**: Uso de memória otimizado
- **CPU**: Carga de processamento
- **GPU**: Utilização de gráficos

## 🔒 Segurança e Estabilidade

### Validações
- **Dados de Entrada**: Validação de parâmetros
- **Salvamento**: Verificação de integridade
- **Carregamento**: Tratamento de erros
- **UI**: Prevenção de estados inválidos

### Tratamento de Erros
- **Try-Catch**: Blocos de tratamento
- **Logs**: Sistema de logging
- **Fallbacks**: Valores padrão
- **Recovery**: Recuperação automática

## 📄 Licença

Este projeto é propriedade da Crystian . Todos os direitos reservados.

### Uso Comercial
- **Proibido** sem autorização expressa
- **Desenvolvimento**: Apenas para fins educacionais
- **Distribuição**: Restrita aos proprietários

---

**Desenvolvido com ❤️ usando Unity**

*Versão do Projeto: 1.0.0*  
*Última Atualização: Dezembro 23/06/2025*  
*Desenvolvedor: Crystian* 
