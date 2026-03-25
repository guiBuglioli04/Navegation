<img width="423" height="850" alt="image" src="https://github.com/user-attachments/assets/17eddba2-cab7-46d5-b5b8-e4425eb81450" />
<img width="399" height="860" alt="image" src="https://github.com/user-attachments/assets/05e17f6e-2f28-4ff7-8c74-48bc170af8a2" />
<img width="422" height="857" alt="image" src="https://github.com/user-attachments/assets/f86cc4ce-4bcd-4a7f-8daf-7e9a12691b0a" /><img width="416" height="856" alt="image" src="https://github.com/user-attachments/assets/ddce8963-21bf-42da-aaca-fc6840cb95f9" />

# Nome:Guilherme Buglioli RM:555273


# CHECKPOINT 1 EXPLICAÇÃO COMMITS

# Passagem de parâmetros obrigatórios na tela de Perfil


Este commit implementa a **navegação entre telas** no aplicativo Android.


## Principais mudanças

### 1. Criação das rotas
Define nomes para cada tela do app.

Exemplo:
- Home
- Details

Facilita organizar a navegação

---

###  2. Configuração da navegação
Adiciona o `NavHost`, que controla quais telas existem e qual é a inicial.

Define por onde o app começa

---

###  3. Navegar entre telas
Permite ir de uma tela para outra:

Exemplo:
- Clicar em um botão → ir para outra tela

---

###  4. Voltar para tela anterior
Adiciona suporte ao botão "voltar"

Melhora a experiência do usuário



##  Conclusão

Esse commit:

- Conecta as telas do app
- Organiza a navegação
- Deixa o app mais completo e funcional

---

# Passagem de parâmetros opcionais na tela de Pedidos

##  Objetivo
Refatorar e melhorar a **estrutura de navegação entre telas**, tornando o código mais organizado, seguro e fácil de manter.

---
## Principais mudanças

###  1. Uso de rotas centralizadas

navController.navigate(Screen.Details.route)

- Substitui strings como "details_screen" por uma estrutura (Screen)
- Evita erros de digitação
- Facilita manutenção e reutilização

2. Organização do NavHost
 ````kotlin
NavHost(
    navController = navController,
    startDestination = Screen.Home.route
) {
    composable(Screen.Home.route) {
        HomeScreen()
    }

    composable(Screen.Details.route) {
        DetailsScreen()
    }
}
````

- Centraliza todas as telas do app
-  claramente o fluxo de navegação
- Melhora a legibilidade do código

3. Navegação baseada em eventos
   Button(onClick = {
   navController.navigate(Screen.Details.route)
   }) {
   Text("Ir para detalhes")
   }

- A navegação acontece a partir de ações do usuário
- Conecta UI com fluxo do app

4. Controle do back stack
   navController.popBackStack()

- Permite voltar para a tela anterior
- Garante comportamento correto do botão "voltar"

5. Desacoplamento da navegação
   HomeScreen(
   onNavigateToDetails = {
   navController.navigate(Screen.Details.route)
   }
   )

- A tela não depende diretamente do NavController
- Melhor separação de responsabilidades
- Código mais testável e reutilizável

# Passagem de múltiplos parâmetros

## 🎯 Objetivo

Este commit introduz **melhorias na navegação e na passagem de informações entre telas**, evoluindo a estrutura criada anteriormente.

---

##  Principais mudanças

###  Inserindo valor ao parâmetro opcional na tela de Pedidos

```kotlin
navController.navigate("details_screen/$name")
````
- Permite enviar dados ao navegar
- Exemplo: enviar um nome ou id para outra tela

1. Definição de rota com argumento

````kotlin
composable(
    route = "details_screen/{name}",
    arguments = listOf(navArgument("name") {
        type = NavType.StringType
    })
) { backStackEntry ->
    val name = backStackEntry.arguments?.getString("name")
}
````
- Define que a tela espera um parâmetro
- Recupera o valor recebido

3. Uso do parâmetro na tela
   Text(text = "Olá, $name")

- A tela agora usa dados vindos da navegação
- Torna a UI dinâmica

4. Navegação mais flexível
````kotlin
onNavigate = { name ->
    navController.navigate("details_screen/$name")
}
````
- Permite passar valores dinamicamente
- Melhora reutilização do código

# Passagem de múltiplos parâmetros

## 🎯 Objetivo

Este commit faz **ajustes finais na navegação**, melhorando a forma como os dados são tratados e exibidos entre as telas.

---

##  Principais mudanças

### 1. Tratamento de argumentos recebidos

```kotlin
val name = backStackEntry.arguments?.getString("name") ?: ""
````

- Garante que o valor não seja nulo
- Evita possíveis crashes no app
- Define um valor padrão

2. Uso mais seguro dos dados
   Text(text = "Olá, $name")

- Exibe o dado recebido de forma segura
- Torna a interface dinâmica

3. Padronização da navegação com parâmetros
   navController.navigate("details_screen/$name")

- Mantém o padrão de envio de dados entre telas
- Facilita reutilização

4. Código mais consistente
   Melhor organização geral
   Pequenos ajustes de sintaxe
   Padronização com commits anteriores

- Código mais limpo e previsível

O que mudou na prática?

Antes:

Navegação com parâmetros, mas com risco de erro (null)

Depois:

Navegação mais segura
Dados tratados corretamente
Menor chance de crash

Impacto:
1. Aumenta a estabilidade do app
2. Melhora a segurança no uso de dados
3. Deixa o código mais profissional

