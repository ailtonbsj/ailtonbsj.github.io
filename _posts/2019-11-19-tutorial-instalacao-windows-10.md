---
layout: post
title:  "Tutorial para instalação do Windows 10 (Português / Brasil)"
date:   2019-11-19 11:32:00 -0300
categories: tutorial windows hardware
---
## Durante a instalação do Windows

> Após configurar as partições do sistema

- Escolha: Brasil
- Clique: Sim
- Escolha: Portugues (Brasil ABNT)
- Clique: Sim
- Clique: Pular
- Clique: Ignorar por enquanto
- Clique: Nao
- Digite o nome de usuario
- Clique: Avancar
- Digite a Senha
- Clique: Avançar
- Confirme a Senha
- Clique: Avançar
- Adicione as 3 perguntas de segurança
- Clique: Avançar
- Clique: Recusar
- Clique: Não
- Escolha: Não, Não, Não, Básico, Não, Não, Não
- Clique: Aceitar

## Após a instalação

- Instale o WinRAR
- Instale todos os Drivers
- Conecte-se a Internet via Wifi ou Ethernet
- Instale o Driver Easy
  (Verifique se todos os drivers estão ok)

## Na barra de tarefas

- Marque: Cortana > Mostrar ícone da Cortana
- Desmarque: Mostrar Pessoas na barra de tarefas
- Desafixe: Microsoft Edge, Microsoft Store, Mail
- Fixe o navegador Chrome ou Firefox

## Menu Iniciar

- Desafixe todos os itens para um menu slim

## Configurações > Aplicativos

- Desinstalar: Clima, Dicas, Hub de Comentários, Microsoft Notícias, Microsoft OneDrive, Mixed Reality Portal, Office, OneNote, Planos de Celular, Print 3D, Skype, Xbox Live, Candy Crush Friends, Candy Crush Saga, Spotify, Driver Easy.

## Configurações > Personalização > Cores

- Desative: Efeitos de transparência

## Configurações > Personalização > Tela de bloqueio

- Tela de fundo: Escolha a opção "Imagem"
- Desative: Receba dados interessantes, dicas e muito mais do Windows e Cortana
- Escolha Nenhum em "Escolher um aplicativo para mostrar o status detalhado"
- Escolha Nenhum pra todos os itens em "Escolher aplicativos para mostrar o status rápido"
- Desative: Mostrar a imagem de tela de fundo da tela de bloqueio do Windows

## Configurações > Personalização > Iniciar

- Desative: Mostrar aplicativos adicionados recentemente
- Desative: Mostrar aplicativos mais usados
- Desative: Mostrar sugestões ocasionalmente em Iniciar

## Configurações > Cortana > Conversar com a Cortana

- Desative: Usar a Cortana mesmo quando meu dispositivo estiver bloqueado

## Windows Explorer

- Arquivo > Opções > Geral
  - Selecione Meu Computador em "Abrir Explorador para"
  - Desative: Mostrar arquivos usados recentemente
  - Desative: Mostrar pastas mais usadas em Acesso rápido
- Arquivo > Opções > Modo de Exibição
  - Desative: Ocultar arquivos protegidos do sistema operacional
  - Desative: Ocultar as extensões dos tipos de arquivos conhecidos
  - Marque: Mostrar arquivos, pastas e unidades ocultas

## Painel de Controle > Sistema e Segurança > Opções de Energia > Escolher a função dos botões de energia

- Clique: Alternar configurações não disponíveis no momento
- Desmarque: Ligar inicialização rápida

## Painel de Controle > Sistema e Segurança > Sistema > Configurações avançadas do sistema

- Clique: Desempenho Configurações
- Escolha: Ajustar para obter melhor desempenho
- Marque: Mostrar miniaturas em vez de ícones
- Marque: Usar fontes de tela com cantos arredondados
- Marque: Usar sombras subjacentes para rótulos de ícones na area trabalho

## Configurações > Hora e Idioma

- Desative: Ajustar automaticamente para o horário de verão

## Configurações > Sistema > Notificações e ações

- Desative: Mostrar lembretes e chamados VoIP de entrada na tela de bloqueio
- Desative: Obter dicas, truques e sugestões de como usar o Windows

## Configurações > Sistema > Multitarefas

- Desative: Mostrar sugestões ocasionalmente em sua linha do tempo

## Configurações > Sistema > Sobre

- Clique: Renomear este Computador

## Configurações > Dispositivos > Bluetooth e outros dispositivos

- Desative: Bluetooth

## Configurações > Rede e Internet > Uso de dados

- Selecione Sempre em "Limitar o que os apps da Store e os recursos do Windows podem fazer em segundo plano"

## Configurações > Privacidade > Geral

- Desative: Mostrar-me o conteúdo sugerido no app Configurações

## Configurações > Privacidade > Histórico de atividades

- Desative: Armazenar meu histórico de atividades neste dispositivo
- Clique: Limpar histórico de atividades

# Configurações > Atualização e Segurança > Windows Update

- Alterar horário ativo: 7h as 23h

# Configurações > Atualização e Segurança > Otimização de Entrega

- Desative: Permitir downloads de outros computadores

# Serviços (services.msc)

- Windows Update: Parar e desativar

## Desktop

- Delete: Microsoft Edge (Depois de instalar o Chrome ou Firefox)
- Delete: desktop.ini

# Habilite o .NET 3.5

```
Dism.exe /online /enable-feature /featurename:NetFX3 /All /Source:E:\sources\sxs /LimitAccess
```

## To install

- Google Chrome
  - Desmarque a opção de enviar estatísticas de uso
  - Defina como padrão
- WPS Office
  - Desmarque: Utilizar o WPS para abrir ficheiros pdf
  - Instale como multicomponentes
- GIMP
- Adobe Reader
  - Habilite as miniaturas
- VLC
- K-Lite Codec Pack
- Fontes TTF de Terceiros
- Libre Office
- CCleaner
  - Customize Install. Desmarque tudo, menos Add Start Menu Shortcuts
  - Configure para não inicializar nem usar internet