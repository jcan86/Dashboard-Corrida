🏁 Dashboard da Corrida de Pesquisas - in.cube 6

🎯 O que é isso?

Este é um painel "mãos na massa" criado para acompanhar em tempo real a "Corrida de Pesquisas - in.cube 6" do Inova HC.

O objetivo era ter uma solução ágil e de deploy rápido (arrastar e soltar no Netlify) que fosse 100% em tempo real, permitindo que um administrador atualizasse o progresso das equipes e que o público visse a "corrida" avançar sem precisar recarregar a página.

✨ Funcionalidades

✅ Visualização Pública: Uma "Pista da Corrida" com ícones de cavalos (SVG) e um Ranking de Barras que mostram o progresso de cada equipe.

✅ Atualização em Tempo Real: Usa Firebase Firestore (onSnapshot) para que os dados na tela de todos os espectadores mudem instantaneamente.

✅ Painel de Controle Seguro: Uma aba "Painel de Controle" protegida por senha, onde o admin pode logar (usando Firebase Auth) e atualizar o número de entrevistas e integrantes de cada time.

✅ Cálculo de Esforço (A Lógica): A posição não é só o número de entrevistas. Ela é calculada pela fórmula:

$$\\ \text{Índice} = \frac{\text{Nº de Entrevistas}}{\sqrt{\text{Nº de Integrantes}}}$$

$$$$

✅ Single-Page Vanilla JS: Todo o projeto está contido em um único arquivo index.html. Ele usa JavaScript moderno (ES Modules) e Tailwind CSS para o estilo.

🚀 Como Usar (Deploy Rápido)

Este projeto foi feito para ser simples de replicar.

Firebase (O "Backend"):

Crie um projeto no Firebase.

Ative o Firestore (banco de dados) e o Authentication (login).

No Authentication, ative o provedor "E-mail/Senha".

Cadastre o usuário administrador (ex: aaa@inova.hc e a senha Agoravai2025).

Copie as credenciais do seu projeto (apiKey, authDomain, etc.).

Código (index.html):

Cole as suas credenciais do Firebase no objeto HOSTED_FIREBASE_CONFIG dentro do <script type="module">.

Regras de Segurança (Firestore):

Vá na aba "Regras" do seu Firestore e cole o seguinte (isso permite que o público leia e que o admin "plante" os dados iniciais):

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read: if true; 
      allow write: if request.auth != null; 
    }
  }
}


Deploy (Netlify):

Coloque o arquivo index.html em uma pasta.

Arraste e solte essa pasta no Netlify.

Pronto. Está no ar.

🧠 A Lógica: Por que a Raiz Quadrada (√)?

Usar a fórmula Entrevistas / √ Integrantes foi uma decisão de "negócio" para tornar a corrida mais justa.

O Problema: Uma equipe com 6 pessoas consegue fazer mais entrevistas do que uma equipe com 2.

A Solução: Em vez de dividir linearmente (/ 6), usamos a raiz quadrada (/ √6 ≈ 2.44). Isso penaliza equipes grandes (valorizando o esforço de equipes pequenas), mas não de forma tão agressiva.

Status do Projeto: Concluído e funcionando. 🚀
