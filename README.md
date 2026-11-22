# 🐰 Floco, o coelho que vive no GitHub

A cada ~10 minutos um robô do GitHub faz o Floco viver um "turno": ele come, descansa,
passeia, pesquisa na Wikipédia, desenha ou brinca. Tudo é salvo nos arquivos do repositório
e a página mostra o resultado. Funciona com o seu notebook desligado.

Custo: R$ 0 (repositório público). A IA (Gemini) e a busca extra (Tavily) são opcionais; sem elas o Floco decide por regras e pesquisa na Wikipédia.

## Passo a passo (uns 15 minutos)

### 1. Criar conta e repositório
1. Crie uma conta grátis em https://github.com
2. Clique em **+** (canto superior) → **New repository**.
3. Nome: `floco`. Marque **Public**. Clique em **Create repository**.

### 2. Enviar os arquivos
1. Descompacte o zip no seu computador.
2. Na página do repositório, clique em **uploading an existing file**.
3. Arraste para lá: `turno.py`, `README.md` e a pasta `docs` (com tudo dentro). Clique em **Commit changes**.
4. Agora o arquivo escondido do robô. Clique em **Add file → Create new file**.
   No campo do nome digite exatamente: `.github/workflows/turno.yml`
   (ao digitar as barras, o GitHub cria as pastas sozinho).
   Abra o arquivo `workflow-turno.yml` do zip, copie todo o texto e cole na caixa grande.
   Clique em **Commit changes**.

### 3. Ligar a página
**Settings → Pages → Source:** escolha **GitHub Actions**.

### 4. (Opcional) Dar uma IA ao Floco, de graça
1. Entre em https://aistudio.google.com e clique em **Get API key** para criar uma chave.
2. No repositório: **Settings → Secrets and variables → Actions → New repository secret**.
   Nome: `GEMINI_API_KEY`. Valor: sua chave.
3. O modelo padrão é `gemini-2.5-flash-lite`. Se o Google tiver trocado ou tirado esse modelo
   do plano grátis, veja o nome de um modelo gratuito no AI Studio e crie em
   **Variables → New repository variable** o nome `GEMINI_MODEL` com o nome do modelo.
4. NUNCA cole a chave em arquivos do repositório nem em mensagens públicas.

Se a IA falhar ou o plano grátis acabar, o Floco continua vivo usando as regras.

### 4b. (Opcional) Pesquisa em toda a internet
O Floco escolhe sozinho o assunto (com a IA ligada) ou sorteia de uma lista grande, e tenta estas fontes em ordem.
Se uma falhar, passa para a próxima, sem você fazer nada:
1. **Google, via Gemini:** usa a mesma chave do passo 4. Atenção: no plano grátis o Google costuma
   limitar ou bloquear esse recurso (principalmente nos modelos mais novos). Se der erro, o Floco só pula.
   Se quiser testar, use em `GEMINI_MODEL` um modelo da família 2.x que esteja liberado para você no AI Studio.
2. **Tavily (busca na web):** crie uma conta em https://tavily.com, pegue a chave e guarde como secret
   `TAVILY_API_KEY` (mesmo caminho do passo 4). Costuma ter uma cota grátis mensal; confira o limite atual no site.
3. **Wikipédia com busca livre** (português e inglês): sempre grátis, sem chave, aceita qualquer assunto.
4. **Anotações do Floco:** só se tudo acima falhar.

Cada pesquisa mostra o link da fonte na aba 💻 Pesquisas.

**Segurança:** a internet aberta tem de tudo. O Floco usa um filtro simples de palavras (violência, conteúdo adulto,
drogas etc.) e descarta o que for impróprio, mas esse filtro não é perfeito. Como a página é pública, dê uma olhada
de vez em quando na aba Pesquisas e no Diário. Se quiser apagar algo, edite `docs/data/state.json` no GitHub.

### 5. Dar a partida
**Actions → Turno do Floco → Run workflow.** Espere 1 a 2 minutos. Sua página fica em:

`https://SEU-USUARIO.github.io/floco/`

Depois disso ele roda sozinho a cada ~10 minutos.

### 6. Conversar com o Floco (caixa de texto)
Você escreve na caixa lá embaixo e o Floco responde **só com sinais de coelho**: pulinho, orelhas em pé ou baixas,
girar, deitar, balançar a cabeça (sim/não), coração, interrogação, quer cenoura, quer desenhar, quer pesquisar...
Os sinais também aparecem como emojis sobre a cabeça dele, com uma legenda do que significam.

Se você pedir algo ("desenha", "vai pesquisar", "come uma cenoura", "descansa"), ele **decide se atende**:
quanto mais sociável e menos independente ele estiver, mais chance de dizer sim (👍). Se não quiser, balança a cabeça (🚫).

Para a página conseguir mandar a mensagem, ela precisa de uma chave (token) que só mexe neste repositório:
1. Na página, escreva qualquer coisa e toque em **Enviar**. Vai abrir o painel 🔑 com o passo a passo.
2. Abra https://github.com/settings/personal-access-tokens/new
3. Nome: `floco`. Em **Repository access** escolha **Only select repositories** e marque `floco`.
4. Em **Permissions → Repository permissions → Actions** escolha **Read and write**. Clique em **Generate token**.
5. Copie a chave e cole no painel da página. Ela fica guardada só naquele aparelho (repita em outro aparelho se quiser).

A resposta leva de 1 a 2 minutos, porque o robô do GitHub precisa acordar e publicar. Enquanto isso aparece 💭 sobre a cabeça dele.
Sem a chave, dá pra mandar mensagem na mão: **Actions → Turno do Floco → Run workflow** e escreva no campo "Mensagem".

### Desenhos simples e elaborados
- Por padrão ele faz **rabiscos simples** (poucas formas, traço único, como uma criança).
- Cada pesquisa ensina um pouco (barra **Desenho** no painel dele). Pesquisas sobre arte, cores, perspectiva e
  composição ensinam mais, e ele mesmo vai atrás desses assuntos de vez em quando.
- Com a barra de Desenho acima de 40%, ele passa a **querer** fazer, de vez em quando, um desenho elaborado (✨):
  cenas com fundo, árvores, flores e cores. Com a IA ligada, ele usa o que pesquisou para criar. Sem IA, monta uma paisagem sozinho.
- Quanto mais ele aprende, mais frequente fica. Os elaborados costumam ganhar notas maiores e entram no mural.

## Coisas que você precisa saber
- **Público:** o diário, as pesquisas, os desenhos **e as suas mensagens** ficam visíveis para qualquer pessoa (e aparecem nos registros do Actions). Não escreva nada pessoal para ele.
- **Só você conversa:** a mensagem só é aceita com a chave do passo 6, que só você tem. Guarde-a como uma senha; se vazar, apague-a em github.com/settings/personal-access-tokens.
- **Mensagem perdida:** raramente o GitHub cancela uma execução que estava esperando na fila. Se o Floco não responder (😶), mande de novo.
- **Branch:** a página manda a mensagem para a branch `main` (o padrão ao criar o repositório).
- **Atrasos:** o GitHub às vezes atrasa o agendamento em alguns minutos. É normal.
- **Pausa:** se o GitHub desativar o agendamento por inatividade, abra **Actions** e clique em **Enable**.
- **Erro de permissão ao salvar:** Settings → Actions → General → Workflow permissions →
  **Read and write permissions**.
- **Reiniciar o Floco:** apague `docs/data/state.json` e rode o workflow de novo.
