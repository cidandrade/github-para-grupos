Github para trabalhos em grupo

Entre no Github (https://github.com/) e crie sua conta. 
Em “Name” preencha seu nome, não use apelidos. 
Escolha um nome de conta fácil de memorizar, falar e anotar.
Selecione uma foto com enquadramento próximo (dos ombros para cima) para que a imagem seja facilmente identificável, clara, bem iluminada, em boa resolução com fundo simples ou limpo que evite distrações visuais, com aspecto profissional e individual, sem óculos escuros ou acessórios que ocultem o rosto, mantendo consistência com outras redes profissionais.

Um dos alunos do grupo será o administrador, aquele que vai ser responsável por cuidar do repositório do trabalho.

Preparação



Clique sobre a foto no canto direito superior e selecione “Repositories”



Também na parte superior direita estará o botão “New” para criar um novo repositório. Pressione-o. 
Em “Repository Name”, adicione um nome que identifique claramente o conteúdo.
Em “Description”, descreva para que serve este repositório
Em “Choose visibility”, selecione Public, para que o professor possa ter acesso ao trabalho. Caso prefira trabalhar em Private para que ninguém acesse seu trabalho durante o desenvolvimento, jamais esqueça de convertê-lo para Public antes da entrega.
Em “Add README” marque para On, de forma a ter um arquivo que explica o repositório e que até pode ser o conteúdo do trabalho em si.
Em “License” selecione “MIT” para trabalhos com código (ou Apache 2.0 se o trabalho tiver potencial para virar produto) ou “CC BY-NC 4.0” para trabalhos sem código. No arquivo LICENSE que será criado liste todos os integrantes da equipe. Pesquise como utilizar a “CC BY-NC 4.0” no Github.

Glossário:
Git: O Git é um sistema de controle de versão distribuído que opera localmente, funcionando como o "motor" de um projeto para armazenar o histórico completo e os instantâneos (snapshots) de todas as alterações realizadas.
Github: O GitHub é uma plataforma baseada na nuvem para hospedagem de código-fonte e controle de versão usando o Git, que facilita a colaboração e o trabalho em equipe em projetos de desenvolvimento.
Repositório: Um repositório é o espaço de armazenamento do projeto (criado e gerenciado pelo administrador) onde ficam hospedados os arquivos e o histórico de colaboração da equipe.




====================


Confirme que o Git está instalado com git --version. Se não aparecer um número de versão, instale o Git a partir de git-scm.com.
1.2 Identidade do Git
O Git assina cada commit com um nome e um e-mail. Configure-os antes do primeiro commit:
git config --global user.name "Seu Nome Completo"
git config --global user.email "seu-email@exemplo.com"
Use o mesmo e-mail cadastrado no GitHub. Caso contrário, os commits aparecem no repositório mas não são vinculados ao seu perfil — e, em um trabalho avaliado, isso significa que a sua contribuição não é reconhecida.
1.3 Autenticação: senha não funciona mais
⚠️ Atenção: desde agosto de 2021 o GitHub não aceita mais a senha da conta na linha de comando. Quando o git push pedir "Password", você deve informar um Personal Access Token (PAT), e não a sua senha.
Para gerar o token:
Foto do perfil (canto superior direito) > Settings.
No fim do menu lateral: Developer settings > Personal access tokens > Tokens (classic).
Generate new token > Generate new token (classic).
Dê um nome, defina a validade e marque o escopo repo.
Copie o token e guarde em local seguro: ele só é exibido uma vez. Use-o no lugar da senha quando o terminal pedir.
Alternativas mais confortáveis: configurar uma chave SSH, ou instalar o GitHub CLI e rodar gh auth login, que resolve a autenticação pelo navegador e dispensa digitar token.


2. Parte 1 — O Administrador: setup e proteção da main
O administrador cria o repositório, dá acesso à equipe e configura a regra de segurança. Todas as ações desta etapa são feitas na interface web do GitHub.
⚠️ Requisito de plano: crie o repositório como Público. No plano gratuito do GitHub, as regras de proteção de branch (rulesets) só valem em repositórios públicos; em repositórios privados exigem GitHub Pro, Team ou Enterprise. Se o grupo precisar de repositório privado com proteção, ative antes o GitHub Education, que é gratuito para estudantes.
2.1 Criar o repositório
No GitHub, clique em New repository. Defina o nome, marque a visibilidade Public e marque a opção Add a README file. Clique em Create repository.
Vá em Settings > Collaborators > Add people e adicione o usuário de cada membro do grupo.
Passo frequentemente esquecido: cada colega recebe um convite por e-mail e por notificação, e precisa aceitá-lo. Enquanto o convite não for aceito, o colaborador consegue clonar o repositório público, mas o git push será recusado.
2.2 Proteger a branch main (regra obrigatória)
Vá em Settings > Rules > Rulesets > New ruleset > New branch ruleset.
Em Ruleset name, digite algo como Protecao da main.
Em Enforcement status, selecione Active.
⚠️ Armadilha silenciosa: o campo Enforcement status vem preenchido como Disabled por padrão. Se você criar o ruleset sem alterá-lo, a regra existe na tela mas não bloqueia nada — e os alunos continuarão empurrando código direto na main sem perceber.
Em Target branches, clique em Add target e escolha Include default branch (ou digite o padrão main).
Na lista de regras, marque Require a pull request before merging.
Deixe a Bypass list vazia. Assim a regra vale para todos, inclusive para o próprio administrador — que é exatamente o comportamento desejado no exercício.
Clique em Create.
Na interface antiga o caminho equivalente é Settings > Branches > Add branch protection rule, com o padrão main e a opção Require a pull request before merging marcada.
Dica pedagógica: não marque "Require approvals" neste primeiro exercício. Com essa opção ativa, ninguém pode aprovar o próprio Pull Request — e o administrador ficaria impedido de integrar o próprio trabalho, travando a turma.
Por fim, envie o link do repositório para o grupo.


3. Parte 2 — Os colaboradores: trabalhando localmente
Com a regra ativa, você não consegue editar a main diretamente. O caminho é criar uma ramificação (branch) para o seu trabalho. Abra o terminal do seu computador ou o terminal integrado do VS Code.
Passo 1 — Clonar o projeto
Substitua a URL pelo link enviado pelo administrador.
git clone <URL-DO-REPOSITORIO>
Passo 2 — Entrar na pasta do projeto
cd <nome-da-pasta>
Passo 3 — Criar a sua branch de trabalho
Escolha um nome descritivo, como feature-login ou edicao-introducao. O comando checkout -b cria a branch e já muda para ela.
git checkout -b <nome-da-sua-branch>
Confirme em qual branch você está com git branch — a atual aparece marcada com um asterisco. Em versões recentes do Git, git switch -c <nome> faz o mesmo que checkout -b.
Passo 4 — Fazer as alterações e salvar
Abra o VS Code, edite o README.md ou crie novos arquivos, e salve. Arquivo não salvo não é visto pelo Git.
Passo 5 — Preparar e commitar
De volta ao terminal, marque as alterações que entrarão no commit:
git add README.md
Para adicionar todos os arquivos modificados de uma vez, use git add . (com o ponto).
Crie o commit com uma mensagem clara do que foi feito:
git commit -m "Adiciona secao de introducao no README"
Passo 6 — Enviar a branch para o GitHub
git push origin <nome-da-sua-branch>
Se aparecer um pedido de usuário e senha, informe o seu Personal Access Token no campo de senha, conforme o item 1.3.


4. Parte 3 — O Colaborador: abrindo o Pull Request
Com o código enviado, solicite a integração à versão oficial. As ações são feitas na interface web do GitHub.
Acesse a página do repositório no GitHub.
Aparecerá um aviso destacado informando que a sua branch recebeu envios recentes. Clique no botão Compare & pull request. Se o aviso não aparecer, vá na aba Pull requests > New pull request.
Confira que a base (base) é a main e que a comparação (compare) é a sua branch.
Preencha o título, explique o que foi alterado e clique em Create pull request.
5. Parte 4 — O Administrador: revisão e merge
Acesse a aba Pull requests e abra o PR criado pelo colega.
Clique na aba Files changed para conferir linha a linha o que foi modificado. É possível comentar em linhas específicas.
Voltando à aba principal do PR, clique em Merge pull request e depois em Confirm merge.
Recomendado: clique em Delete branch para remover a branch já integrada e manter o repositório limpo.


6. Dica de ouro: mantendo-se atualizado
Sempre que um PR é integrado, a main muda. Antes de começar um novo trabalho, atualize a sua máquina:
git checkout main
git pull origin main
Depois, crie a nova branch com git checkout -b <nova-branch> e recomece o ciclo. Esse hábito reduz drasticamente a quantidade de conflitos.
7. Quando dá conflito
Conflito acontece quando dois colegas alteram a mesma linha do mesmo arquivo. O GitHub avisa com a mensagem de que a branch tem conflitos a resolver. É uma situação normal, não um erro do aluno.
Como reduzir a chance de conflito
Combine antes quem mexe em qual arquivo ou em qual seção.
Atualize a main antes de criar cada branch nova.
Faça Pull Requests pequenos e frequentes, em vez de um único PR gigante no fim do prazo.
Como resolver localmente
git checkout main
git pull origin main
git checkout <sua-branch>
git merge main
Abra o arquivo apontado pelo Git e procure os marcadores <<<<<<<, ======= e >>>>>>>. Entre eles estão as duas versões em disputa. Decida qual conteúdo permanece (às vezes, os dois), apague os marcadores e salve. Em seguida:
git add .
git commit -m "Resolve conflito com a main"
git push origin <sua-branch>


8. Referência rápida de comandos
Comando
O que faz
git clone <url>
Baixa o repositório para a sua máquina.
git status
Mostra em que branch você está e o que foi alterado.
git checkout -b <branch>
Cria uma nova branch e muda para ela.
git checkout <branch>
Muda para uma branch já existente.
git add .
Prepara todos os arquivos modificados para o commit.
git commit -m "msg"
Registra as alterações preparadas, com uma mensagem.
git push origin <branch>
Envia a sua branch para o GitHub.
git pull origin main
Traz para a sua máquina as novidades da main.
git log --oneline
Lista o histórico de commits de forma resumida.
git branch
Lista as branches locais e destaca a atual.



9. Bônus: executando o fluxo pelo celular
Longe do computador, todo o ciclo de clonagem, edição e Pull Request pode ser feito pelo smartphone. Para alunos de Computação, é um bom exercício de domínio de terminal.
9.1 Android — terminal com Termux
Correção importante: a versão do Termux publicada na Play Store está descontinuada e não é mantida pela equipe oficial do projeto. Instale apenas pelo F-Droid ou pelas releases oficiais no GitHub (github.com/termux/termux-app). As versões têm assinaturas diferentes e não atualizam uma sobre a outra.
Depois de instalar, no próprio Termux:
pkg update && pkg upgrade
pkg install git
pkg install nano
A partir daí, os comandos são exatamente os mesmos da Parte 2: git clone, cd, git checkout -b, git add, git commit e git push. Para editar textos sem sair do terminal, use nano README.md.
Dica que economiza muito sofrimento: digitar um token de acesso na tela do celular é penoso. Instale o GitHub CLI e autentique pelo navegador:
pkg install gh
gh auth login
9.2 iPhone e iPad
O Termux não existe para iOS — é um aplicativo exclusivamente Android. No iPhone ou iPad, use a-Shell ou iSH, disponíveis na App Store, que oferecem um ambiente de linha de comando com Git.
9.3 Abrindo e aprovando Pull Requests
Use o aplicativo oficial GitHub Mobile (Android e iOS) ou acesse o GitHub pelo navegador do celular. O app notifica quando há um novo envio ou PR. O colaborador abre o Pull Request com poucos toques, e o administrador consegue ver o diff, comentar, aprovar e fazer o merge diretamente pela interface do aplicativo.


10. Erros comuns e como resolver
Mensagem no terminal ou no site
O que significa e como resolver
Support for password authentication was removed
Você tentou usar a senha da conta. Gere um Personal Access Token (item 1.3) ou use gh auth login.
Permission denied / 403 Forbidden
Você não é colaborador ou ainda não aceitou o convite. Verifique suas notificações no GitHub.
Changes must be made through a pull request
A regra está funcionando: você tentou enviar direto para a main. Crie uma branch com git checkout -b <nome> e envie novamente.
fatal: not a git repository
O terminal não está dentro da pasta do projeto. Use cd <nome-da-pasta>.
Updates were rejected because the remote contains work
A branch remota tem commits que você não possui. Rode git pull origin <branch> antes do push.
nothing to commit, working tree clean
Nada foi alterado ou o arquivo não foi salvo no editor. Salve e repita git add e git commit.
This branch has conflicts that must be resolved
Duas pessoas editaram a mesma linha. Siga o procedimento da seção 7.


Documento revisado tecnicamente em setembro de 2026. Interfaces do GitHub mudam com frequência; se um menu não corresponder ao descrito, procure o termo em inglês indicado em negrito.

